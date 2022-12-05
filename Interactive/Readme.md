
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

## Inspecting the first model load

Now that we can control the camera better, we can look at what model is actually being displayed. 

![image](https://user-images.githubusercontent.com/67718774/205512879-6f4f5771-8e16-409b-bf0c-1d3a8951e357.png)


While this might not at first glance look like it is even distantly related to a car model, upon closer inspection at different angles it becomes clear that there is a car model *somewhere* in there.

There are telltale signs of potential wheels at each end - although grossly deformed.
![image](https://user-images.githubusercontent.com/67718774/205513009-1fd28578-7305-41fd-92c6-8ab5222a5754.png)
 
## Applying materials

Before trying to fix the horrendous deformation of the mesh, I decided to fix the material rendering first. The issue here was with Blender, rather than OpenGL - so to fix this I created a new UV map of the object and fed that into an image texture node on each material. This could then be baked to the object in the Rendering tab and set as an Image source for the texture. Doing this and running the OpenGL again then gave me this:

![image](https://user-images.githubusercontent.com/67718774/205650068-796069b5-a57f-4172-9e7d-31ea8cc5512c.png)

While the mesh is still deformed, at least now it's trying to render materials.

### Decision Making

At this point, I had to make the decision to focus on other parts of the coursework such as lighting. This was because of personal circumstances not leaving a lot of time to spare digging around trying to fix the model when I could get other parts done and come back to it.

For the sake of troubleshooting as well, I quickly modelled an incredibly low-poly mockup of my previous car just to get the general shape and tried importing that so that I'd be able to tell if lighting was working properly. The newly imported model had no issues with the mesh deforming, as seen:

![image](https://user-images.githubusercontent.com/67718774/205654957-f8fa17b8-a1d4-42fe-98f5-ff870ac57917.png)

So with a working mesh, I decided I could move on with the rest of the coursework and then come back to the original car if time allowed.

### Lighting

