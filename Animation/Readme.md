# Importing files into Unreal Engine 5

Before being able to import the files into the UE5 project, the entire garage scene had to be exported from Blender.
This was done by first removing all the lights and cameras, selecting everything in the scene and exporting as an FBX. The export settings involved changing the path mode to copy and only including the selected objects and only the mesh types. The geometry smoothing was also changed to face.

Once the UE5 project was created and opened, a new scene was also created and the Blender scene FBX was imported into the content drawer. Selecting of the individual models that now appeared in the content drawer and dragging them all out into the scene in one go kept everything in its original place. This did mean the origins of each model was at the centre of the scene which made adjusting anything a bit of a nightmare, but it was better and faster than manually placing each thing in the right place again.

There were a couple of issues that came up with the import - the rust texture didn't move over and I was unable to rebuild it using Unreal's material editor and could not find a decent way to export it properly from Blender as its own material (there was an attempt at baking the material to an image but the UV unwrap wasn't playing nice with the array modifier used so I simply gave up on it).

Another issue was that Unreal appears to deal with planes differently and as such the yellow background of the logo simply disappeared - I got round this by rebuilding it from a solid mesh and moving it into the correct place.
Other than those two issues, there were no other glaring problems.


