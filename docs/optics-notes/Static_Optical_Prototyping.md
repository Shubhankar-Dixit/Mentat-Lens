# Optical Bench Setup

To work on the optics portion you need to first work off of an optical bench. An optical bench is a flat surface with holes that are spaced apart equally to make it so that you can lock in objects into the holes. This allows you to have a stable platform to work on and to be able to easily move objects around without them falling over and to also keep them at measurable distances.

![alt text](optical_bench.png)

- The primary task here is to position the display so that its light reflects off of the combiner and into your eye at a comfortable focus. This has to be done by adjusting the position of the display and the combiner. The display should be positioned so that it is at a distance from the combiner that allows for a clear image to be reflected into your eye. This is entirely emperical and will require some trial and error to find the optimal position based on your eye.

- Keep your setup stable. A displacement of 0.5mm in your display position can shift the virtual image focus from 'infinity' to just a few inches away from your face. Having the image a few inches away from your face is not ideal for a comfortable viewing experience which will be discussed more in depth below.

- Before finalizing the mounts, you must calibrate the Field of View (FOV). The FOV is determined by the size of your display and its distance from the optical combiner. Moving the display closer to the optics typically increases the FOV but may introduce distortion or blur at the edges. Take the time to find the balance between a large, immersive screen and a crisp, readable image.

### Collimation

- In optics collimated light is light whose rays are parallel, and therefore will spread minimally as it propagates. This makes the image appear as if it is placed at infinity, which is ideal for a comfortable viewing experience. If the light is not collimated, the image will appear blurry and will be difficult to focus on, especially if it is close to your face. This is because the light rays will be diverging, causing the image to appear as if it is at a finite distance rather than at infinity.

- Nobody wants to have an image stuck at 2 inches away from their face for a long period of time, it causes eye strain from you trying to focus on the image and then back to the environment around you.

- Achieving this requires that the display be placed exactly one focal length away from the collimating lens.

### Focal Length Testing

- To achieve this comfortable focus, you must move the display along the Z-axis of your bench until the image appears sharp while your eyes are relaxed. If the display is too close to the lens, the image will be blurry; if it is at the exact focal point, the rays exit the lens parallel to each other. This physical distance is the most critical measurement you will record during this phase.

- An analogy to understand:

"Think of a magnifying glass: when you hold it at just the right distance from a leaf to make the sunlight a tiny, sharp dot, you have found the focal point. In AR, putting your display at that same 'sharp dot' distance ensures the light leaves the lens in straight, parallel lines."

# Image Stability and Distortion

- Now that you have the focus locked in, you need to check for spherical abberation. Spherical abberation is a type of distortion that occurs at the perimeter of the lens where the spherical shape of the lens causes light rays to bend more than they do at the center of the lens. This can cause the image to appear blurry or distorted at the edges, which can be distracting and reduce the overall quality of the AR experience. To check for this, you can move your eye around while looking at the image and see if it remains clear and stable. If you notice that the image becomes blurry or distorted as you move your eye, then you may need to adjust the position of the display or consider using a different lens with less spherical abberation.

![alt text](spherical_aberration.png)

- In DIY AR, this often looks like a 'glow' or 'halo' around text near the edges of the display.

- Engineers often solve this by using aspheric lenses, which have a more complex surface profile that reduces spherical aberration and provides a clearer image across the entire field of view. However, aspheric lenses can be more expensive and harder to source for DIY projects, so careful positioning and testing of your existing lenses is crucial to minimize this issue.

- Since we cannot easily source aspheric lenses, we can instead utilize an extension on top of our own glasses, where you can put a display and a lens on top of your glasses. This allows you to use the lenses in your glasses to help collimate the light from the display, which can help reduce spherical aberration and improve image clarity across the field of view. By leveraging the optics already present in your glasses, you can achieve a more stable and clear AR experience without needing specialized aspheric lenses.

- The final step in this phase is to check for Chromatic Aberration. Chromatic aberration is a type of distortion that occurs when different colors of light are refracted by different amounts as they pass through a lens. Alongside this ensure that there is no skew, which is a type of distortion that occurs when the image appears stretched or compressed in one direction. This is caused by the lens on the optical bench not being perpendicular to the surface.

# Finalizing Everything

- With the focus sharp and the display leveled, the final step is to check the stability of your image against external light. Because AR combiners like beamsplitters are semi-transparent, bright room lights can wash out the virtual image. To fix this, you may have to add a hood or shroud around the optics to ensure that the light reaches the combiner without interference from ambient light. This can be as simple as using black cardboard or foam to create a makeshift hood that blocks out unwanted light while still allowing you to see the real world through the combiner.
