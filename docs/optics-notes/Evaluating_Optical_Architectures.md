The heart of AR Glasses is the optical engine.

An optical engine is the mechanism that helps to direct light from your display into your eye while letting you see the world.

For a project of our scope (DIY), the two best paths to choose between are:

# Birdbath Optics

- Birdbath optics use a spherical combiner and a 45 degree beamsplitter to reflect the image from the display into your eye.

A useful blog to go through on this is Near-Eye Bird Bath Optics Pros and Cons – And IMMY’s Different Approach(https://kguttag.com/2017/03/03/near-eye-bird-bath-optics-pros-and-cons-and-immys-different-approach/)

- The display is mounted at the top, shining downward into the beamsplitter. Light reflects off the curved 'bowl' surface and then passes through the beamsplitter into your eye.

# Waveguide Optics

- Waveguides work by 'trapping' light inside a thin pane of glass or plastic through total internal reflection. The light is injected into the edge of the waveguide and bounces around inside until it reaches your eye, where it exits through a partially reflective surface.

- Waveguide optics use a flat combiner with internal reflections to direct light from a microprojecter located near the temple of the glasses directly into your eyes.

- The display is mounted on the side, shining into the edge of the waveguide. Light is guided through the waveguide by total internal reflection and then exits through the surface in front of your eye.

- Waveguide optics can be more compact and lightweight than birdbath optics, but they can also be more complex to design and manufacture. Waveguide optics is what is seen in commercial AR glasses like the Microsoft HoloLens and Magic Leap One, while birdbath optics is more commonly used in DIY AR projects due to its simplicity and ease of prototyping.

---

The choice dictates how bulky your glasses will be, how much they will cost, and how immersive the final experience feels.

For this project (currently) the aim is to prototype a birdbath optical engine, as it is more accessible for DIY projects and allows for easier experimentation with different configurations and components. Birdbath optics can be built using readily available materials and do not require the precision manufacturing processes that waveguide optics often demand, making it an ideal choice for prototyping and learning about AR optical systems.

The main issue with using a birdbath optical engine is that they struggle with occlusion, which is the ability to block virtual objects behind real-world objects. This results in 'ghostly' or transparent images. Waveguides, while incredibly sleek, are typically beyond the reach of home manufacturing because they rely on microscopic structures etched into glass to bounce light internally.

![An astronaut tests a waveguide-based AR system, highlighting the slim profile achievable with this optical path.](astronaught_ar.png)

# The Display

The next layer of the optical engine is the display. Typically a Micro-OLED or LCoS panel is used for this. These displays are tiny (often less than an inch) but they have a high pixel density and are bright enough to overcome ambient light, especially in see-through designs where your display is competing with the real world for your attention.

---

## Alignment

* An Important thing to focus on is optical alignment. Optical alignment essentially means that all components should share the same optical axis. This means that the display, the combiner, and your pupil should fall on the same straight line. This is crucial for ensuring that the virtual image is properly focused and aligned with the real world.

- Misalignment doesn't just cause blur; it can introduce 'vignetting,' where the corners of your image get cut off by the edges of the lens housing.

- On a bench we use crosshair patterns on the display to help visually center everything before locking down the mounting screws.

---

* While waveguide optics looks perfect it does have a flaw as well which you should know. That flaw is that it suffers from Rainbow Artifacts. This is a phenomenon where the light exiting the waveguide can split into its component colors, creating a rainbow-like effect around bright objects. This can be distracting and reduce the overall image quality, especially in high-contrast scenes. Birdbath optics, on the other hand, typically do not suffer from this issue, making them a more straightforward choice for DIY projects where simplicity and ease of prototyping are key considerations.

* This happens due to Diffraction Gratings, which are a key component in waveguide optics.

- A diffraction grating is an optical component with a periodic structure that splits and diffracts light into several beams travelling in different directions. In waveguides, these are often etched into the glass at the nanometer scale. They serve as the 'doors' for light, telling the photons when to enter the glass and exactly when to exit to hit your pupil. Because the angle of diffraction depends on the wavelength (color) of the light, any slight imperfection in the grating causes colors to separate, leading to the 'rainbow' effect seen in lower-quality AR displays.

---

## Field of View (FOV) Compromise

Beyond image quality, you must decide on your target FOV. Field of View (FOV) describes the total area where digital content can appear. A larger FOV makes the experience more immersive, but it exponentially increases the size of the lenses and the weight of the glasses. Most DIY birdbath designs target a diagonal FOV of 30 to 45 degrees, which is roughly equivalent to looking at a laptop screen from a few feet away.

/\
This is for Birdbath optics.

---

## Managing Occlusion

- A final critical decision for your optical engine is managing occlusion. Most DIY projects use a semi-transparent mirror with a 50/50 split, meaning it reflects 50% of the display light and lets 50% of the real-world light pass through. This creates the 'ghostly' effect common in AR. To make a digital object look solid, you would need an active occlusion layer, like an LCD shutter, which can selectively block out the background light for specific pixels.

### Active Occlusion Layer (Turning off the Sun)

- An active occlusion layer is a technology that can selectively block or dim the real-world light in specific areas of the display to create the illusion of solid virtual objects.

- This is achieved by using a secondary display layer:
    - usually a pixelated liquid crystal panel
    - is placed behind the optical combiner

* When the system wants to show a 'solid' virtual rock on your desk, it turns those specific pixels on the LCD layer black to block the physical desk's light. While this makes the AR feel incredibly real, it is rarely seen in DIY builds because it doubles the complexity of the optics and requires perfect pixel-to-pixel alignment between two different displays.

- Because active occlusion is hard to calibrate at home, most DIY AR glasses opt for higher brightness MACRO-OLED panels to 'overpower' the background light. This approach keeps the weight down and the design simple while still providing a readable interface in most indoor environments.