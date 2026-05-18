## Brain of the Motion System

For your glasses to know where exactly you're looking, you need a way to track the position and orientation of your head in real time. This is where the motion system comes into play. The motion system typically consists of a combination of sensors, such as accelerometers, gyroscopes, magnetometers, and sometimes even depth sensors or cameras for more advanced tracking.

This is done by the Inertial Measurement Unit (IMU).

The IMU is similar to the human vestibular system where it houses two distinct micro-mechanical systems. The accelerometer detects linear motion along the x, y, and z axes, while the gyroscope measures angular velocity(how fast you spin/tilt).

In AR, these two sensors work in tandem to counteract 'drift,' a common error where the software slowly loses track of the 'true north' of your head position. By fusing their data, the system maintains a stable horizon for your digital overlays.

By sampling this data at high speeds, usually hundreds of times per second, your compute module creates a mathematical model of your head's orientation in 3D space. This model is then used to update the position of virtual objects in your field of view, ensuring they stay anchored to the real world as you move around.

![The MPU-6050 is a common, low-cost IMU chip used in many DIY electronics projects to track motion and orientation.](imu_chip.png)

* Raw data from an IMU is notoriously 'noisy' (small vibrations or electrical interference can cause the digital image to jitter). To fix this, we implement a sensor fusion algorithm.

- Sensor fusion is the process of combining data from different sources to produce information that is more accurate than any single sensor could provide.
    - Accelerometers are great at telling you which way is 'down' due to gravity, but they are very sensitive to sudden bumps. Gyroscopes are excellent at tracking smooth rotations but tend to drift over time. 
    - Fusion algorithms weight these inputs against each other, trusting the gyroscope for quick movements and the accelerometer for long-term stability. This is what is responsible for creating the smooth feeling that is associated with high-quality AR headsets.

Once the data has been passed through the algorithm and cleaned, it is then fed into the rendering engine as a set of coordinate changes. This transforms your head movement into a digital viewport, allowing the software to draw 3D object at a specific point in space.

While sensor fusion gives us a clean signal, we must translate that signal into a language the rendering engine understands: **Quaternions** and **Coordinate Frames**.

### Quaternions

- Humans think in terms of angles (pitch, yaw, roll) which is 3D but computers often use quaternions, which are 4D complex numbers, to represent rotation.

*Why is this done though?*

Traditional 3D angles can suffer from 'gimbal lock', where two axes align and the system loses a degree of freedom, causing the image to flip and glitch. Quaternions avoid this problem entirely by treating rotation as a single four-part value. In AR development, using quaternions is standard practice because they allow for smoother interpolation between two points of view. This means that as your head moves from Point A to Point B, the rendering engine can fill in the gaps with mathematical precision, preventing the 'stutter' that would occur with simpler math.

In case this wasn't clear here is an example that should give you an idea of the problem:

- Because the computer uses quaternions, if I were to tilt my head or look up/down the digital overlays stay perfectly upright and don't flip or jitter. This is because the quaternion math allows the system to understand the full 3D rotation of my head without losing any information, even during complex movements. It does it all with respect to where I'm looking, my head's orientation, and tilt/rotation.

## Sensor Pipeline

To implement this into our code, we need to create a pipeline where the IMU hardware sends an uninterrupted signal to your compute module, every time a new sample is ready. The module then runs your fusion algorithm, updates its internal representation of your head's orientation, and passes those new coordinates to the graphics card. This cycle must happen faster than the blink of an eye (roughly 100 milliseconds) to maintain the illusion of reality and prevent the digital image from lagging behind the physical/real world.

| Step | Process |  Goal    |
|---|---------            |----------------|
| 1 | Data Aquisition     | Sample raw IMU values(gyro/accel) |
| 2 | Signal Pre-treatment| Filter out electrical noise and vibration   |
| 3 | State estimation    | Calculate 3D orientation(Quaternions)    |
| 4 | Coordinate Mapping  | Send updates to the graphics rendering engine |

Important Quote from research:

"**Motion-to-photon latency** is the total time it takes for a movement to be reflected on the display. In AR, **keeping this under 20 milliseconds is vital to prevent user discomfort and motion sickness**."

### Interruptions

Low latency is the goal as mentioned above to reach what we defined as Motion-to-photon Latency. Now to achieve this an important piece of this is to introduce Hardware Interrupts.

Hard Interrupts are specific 'trigger' mechanisms where instead of the CPU wasting time and energy constantly asking the sensor if it has a new reading (this process is called **Polling**), the interrupt signal allows the CPU to focus on other tasks until the IMU has a fresh measurement ready.

Think of it like a doorbell. Polling is you walking to the front door every ten seconds to check if a guest is there. An interrupt is the guest ringing the bell so you only go to the door when someone actually arrives.

By using interrupts, your compute module can sleep or handle graphics between samples, which dramatically reduces power consumption and ensures that the very latest motion data is processed the instant it exists. This 'on-demand' processing is what keeps the motion-to-photon latency low enough to prevent motion sickness. 

#### Interrupt Signal

In computing, an interrupt is a signal to the processor emitted by hardware or software indicating an event that needs immediate attention.

For AR, this is a dedicated physical wire between the IMU and the CPU. When the IMU finishes a new measurement, it sends a high-voltage pulse down this wire. (For not that is all that I have learnt so more improvements to this may be added in the future)

The CPU instantly pauses its current background work, runs the tracking code, and then returns to what it was doing. This ensures the rendering engine uses the absolute freshest data without the CPU having to wait around or 'guess' when the next sample will arrive.

![Types of Interrupt Signal](interrupt_signal.png)
/\ Here Polling is the one that we don't want to go with because it's inefficient and causes lag.

##### Polling

In polling your CPU runs in a continuous loop, where it checks a specific memory address associated with the sensor to see if a new data flag has been set. And even thought this is simpler to code it is terrible for the battery life as the CPU is forced to stay in a high-power state, cycling thousands of empty checks just to catch a single sensor update. In a device where battery life and thermal management is already a concern, polling can cause the glasses to overheat or die in minutes rather than hours.

By using interrupts instead of polling, your system ensures that the CPU only wakes up to process data when a new physical movement is actually detected. This efficiency is what allows a small battery to power your AR glasses for hours while maintaining the lightning-fast response times needed for spatial stability.

---

## Translating Data to Graphics

After we've obtained clean, interrupt-driven orientation data (from the IMU), the final step in the pipeline is to pass these coordinates to the graphics engine. The engine uses this data to update its view matrix(a 4x4 matrix used in 3D math to transform world coordinates into camera-relative coordinates), which is essentially a mathematical description of where your 'virtual eyes' are located in the digital scene. If the IMU says you rotated 5 degrees to the right, the engine shifts the entire rendered world 5 degrees to the left on your display to create the illusion that the virtual objects are anchored in the real world.
