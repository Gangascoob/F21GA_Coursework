
# OpenGL Section

## Exporting Models from Blender

The first model I used for testing the object loading in the template project was the car model. The modifiers used were applied to each object and the chassis joined with the wheels, so that everything was enclosed in one model. The model was then exported in the .glTF format, where the model is exported as separate .glTF, .bin and texture files.

As this was modelled without any textures (only materials - more on this later), only a .glTF and .bin file were created.
Placing both of these files in the /assets folder of the directory would allow easy loading from the Source.

## First loading of car model

In the first attempt at loading the model, no real changes were made to the template - simply just changing the source file in the startup() function to /assets/car.gltf rather than /assets/dog.gltf.
The output was as seen below:
![image](https://user-images.githubusercontent.com/67718774/205511601-25add05f-415f-42d1-96b2-973da5bf6a74.png)

Clearly something was wrong here - and despite being able to rotate the object it was hard to see what was actually loading.

## Next steps - Camera Controls

In order to determine what was happening with the model, it was important to have better camera controls so I was able to see what had loaded. The following lines of code were added to allow the user to move the camera in each direction, but also most importantly move the camera forward and backwards so that we could zoom out and have a proper look at the model.

![image](https://user-images.githubusercontent.com/67718774/205512770-9f787bb0-034c-4547-b228-ce0f33cbdb20.png)


The camera controls are the standard WASD (forwards, back, left, right) but also include Q and E for moving upwards and downwards.

