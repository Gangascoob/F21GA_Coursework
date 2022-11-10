# Importing files into Unreal Engine 5

Before being able to import the files into the UE5 project, the entire garage scene had to be exported from Blender.
This was done by first removing all the lights and cameras, selecting everything in the scene and exporting as an FBX. The export settings involved changing the path mode to copy and only including the selected objects and only the mesh types. The geometry smoothing was also changed to face.

Once the UE5 project was created and opened, a new scene was also created and the Blender scene FBX was imported into the content drawer. Selecting of the individual models that now appeared in the content drawer and dragging them all out into the scene in one go kept everything in its original place. This did mean the origins of each model was at the centre of the scene which made adjusting anything a bit of a nightmare, but it was better and faster than manually placing each thing in the right place again.

There were a couple of issues that came up with the import - the rust texture didn't move over and I was unable to rebuild it using Unreal's material editor and could not find a decent way to export it properly from Blender as its own material (there was an attempt at baking the material to an image but the UV unwrap wasn't playing nice with the array modifier used so I simply gave up on it).

Another issue was that Unreal appears to deal with planes differently and as such the yellow background of the logo simply disappeared - I got round this by rebuilding it from a solid mesh and moving it into the correct place.
Other than those two issues, there were no other glaring problems.


# Lights

The lighting was set up almost identically to the render scene in Blender (Rectangle lights, or area lights in Unreal, were set up underneath the ceiling lights facing onto the cars), but with one small difference. Due to Unreal's area lights being directional, the red colour from the cars would reflect up onto the ceiling light and so the light panel would be red rather than white. To fix this, duplicate area lights were created but rotated 180 degrees so they illuminated upwards into the ceiling light. This overrode the red reflections and produced a nice bright white colour on the light panels.

For the final animation of the opening garage door, a 64x64 area light was placed outside facing directly inside at the maximum strength of 160cd to imitate the blinding contrast of opening the door from a dark room into direct sunlight.

# Animations and Sequencing

Since the whole focus of this tv show idea is the cars, the animations for the opening sequence are majorly centred around them. 

Each shot was done using Unreal's sequencer and CineCamera in separate sequences, and then pieced together in a master sequence.

## Animations

The first animation is a wide-angle view of the entire garage starting in darkness, with the lights being turned on a couple of seconds in and illuminating the cars. This was achieved by setting each light in the scene as an actor and then adjusting the light values at certain keyframes. The sudden oncoming of the light had to be done by setting a keyframe with light values of zero a frame or two before the light values were increased to a very high value. This created a kind of 'flashing on' effect which then slowly illuminated the scene before the sequence cuts.

![First Sequence](./Render/Screenshots/opening_sequence.png)

The next few animations were just simple camera pans along the side, front, and top of the car. These were done by setting keyframes in the sequencer with different transform values for the camera. 

The final animation in the scene is a driver's POV from the seat of the car, facing out towards the garage door which opens and floods the camera with light, to which the cutscene fades out to white. The garage door opening was also done through transforms at keyframes, and the fade was done using Unreal's in-built Fade actor.

Additionally, the fade actor was also used to provide softer cuts between animations. However, the fades between sequences were all black whereas the final fade out is white - this was achieved by adding a second 'section' of the Fade actor which allows you to set a different colour for that specific section of Fade.

## Reflection

On reflection, I wish I had attempted some more complex animations - perhaps movement of the car or more exciting transitions, or maybe even having a title text fading in at the end. Unfortunately I didn't find much time to attempt these, but they would definitely have improved the work. Additionally, everything could potentially have been done in one sequence rather than having to put multiple sequences together and would have allowed for some less confusing file management. 
