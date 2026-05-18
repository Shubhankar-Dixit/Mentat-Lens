Once the optics have been configured (you've aligned your lens, display, etc.), the focus shifts to the brain that will drive the pixels. 

This happens through the SoC. In AR, unlike traditional computers, instead of using a standard CPU, GPU, and RAM setup, an SoC (System on a Chip) integrates all of these functions into a single chip. This is crucial for AR glasses, which need to be compact and power-efficient while still delivering high performance. By keeping these components physically close, data travels faster and consumes significantly less power than it would between discrete chips.

However, it also concentrates heat in one tiny area, which is a major engineering hurdle for wearable devices

# The Thermal Problem

Processing high-resolution AR frames generates significant heat. In a desktop computer, you can just add a bigger fan, but on a pair of glasses, excess heat causes thermal throttling and user discomfort

One important piece of information to take away from this is that you must decide if your computer module will be mounted on the frame itself which would require ultralow power draw or tethered to a pocket sized unit where you have more room for batteries and cooling.

The second one is easier and does not feel like the glasses from iron man which is why I will be going with the first option. The computer module will be mounted on the frame itself which would require ultralow power draw. This is a more challenging approach, but it allows for a more seamless and integrated design, which is crucial for user comfort and aesthetics in AR glasses. Plus its a fun challenge!

Here's a quote:

"Thermal Management: Integrating optics with ASICs concentrates heat in a very small area."

— Co-Packaged Optics – End of Pluggables? What It Is, Why It Matters, and Who Needs to Pay Attention

To keep the experience smooth, the compute platform must prioritize low-latency rendering. Every millisecond of delay between a sensor reading and a pixel update breaks the illusion of reality. You need to evaluate whether an embedded system like a Raspberry Pi Compute Module or a specialized mobile processor provides the best path for your specific power and weight constraints.

![A Raspberry Pi Compute Module uses a compact SO-DIMM form factor to save space in wearable designs.](rasberry_pi_computer_module1.png)

- Power consumption of these modules is measured in Watts(W), and for a wearable, you are typically targetting a total system draw between 3W to 8W. Staying in this range is what allows the device to run on a small battery without needing heavy, active cooling. If you exceed this, the battery drains in minutes and the frame of the glasses become hot enough to cause discomfort and too hot to touch.

- Basically make sure you don't exceed the power envelope (A power envelope describes the maximum amount of electrical power a system is allowed to consume and, by extension, the heat it must dissipate) or else you lose battery life and comfort.

---

* An important piece of advice is that when you select a compute module, you must verify if it has the right IO pins to talk to your specific display and sensors.  If your processor cannot communicate fast enough with your display, even the most powerful chip in the world won't prevent the lag that causes motion sickness.

---

## Offloading Strategy

- To do this we can offload some of the processing to a companion device, such as a smartphone or a small wearable computer that can be carried in a pocket. This allows the glasses to focus on rendering and display tasks while the companion device handles more intensive computations, such as sensor data processing and AI algorithms. The communication between the glasses and the companion device can be achieved through low-latency wireless protocols like Bluetooth Low Energy (BLE) or Wi-Fi Direct, ensuring that the user experience remains seamless and responsive.

- But I won't be going with this approach because it does not fit the vision of having a self-contained pair of AR glasses that can operate independently without relying on an external device. The goal is to create a truly standalone AR experience, which is more challenging but ultimately more rewarding in terms of user freedom and immersion.

- It should feel like using E.D.I.T.H. while moving towards the idea of becoming a Mentat.

## Data Pipe

* This is the communication link between the glasses and any external devices. If you choose to go with a tethered approach, this becomes a critical factor in ensuring low latency and high bandwidth for data transfer. This is extra information for those who want to go with the tethered approach.

- Even with a powerful external brain, the communication link between the tethered unit and the glasses must support high bandwith to prevent lag that causes motion sickness.

- The wiring used for these tethered systems typically relies on high-speed standards like USB-C or DisplayPort. These cables are thin enough to be wearable but can handle the gigabits of data per second required for high-resolution graphics. *When you select your compute module, you must ensure its 'I/O' can handle these speeds, or you'll find that your hardware can't actually display the complex applications you've designed it to run*.