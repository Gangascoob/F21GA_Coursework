
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

## Lighting

Thankfully most of the code for a simple light was provided on Canvas, so the implementation was done as follows.

#### Source.cpp file

Firstly, in the main Source.cpp file I had to define the variables being sent to the shaders, as shown: 
![image](https://user-images.githubusercontent.com/67718774/205926422-a9186551-1e3c-475b-b2ad-03aea4b13ff5.png)

The values chosen as the vec3 starting points were simply just chosen through trial and error to find a nice starting effect, and the light position that was given in the lecture slides worked well for my object so I continued with that. 

Next, these variables had to be sent to the shaders. This was done with more template code, as below: 
![image](https://user-images.githubusercontent.com/67718774/205941734-07be495f-b514-4a96-bcea-c4c4f1c8b8c2.png)

Placing this just above the DrawModel call in Render() allows the lights to be created and then applied to anything that is drawn.

Next, the shaders had to be corrected.

#### Shaders

Both the new vertex shader and new fragment shader were taken from the provided code on Canvas. These are used to calculate the normals, and apply lighting based on those normals and the different variables for ambient, diffuse, and specular lighting.

These shaders can be seen below:

![image](https://user-images.githubusercontent.com/67718774/205948576-7a98a532-73e2-4cde-8e39-0872f1029640.png)

![image](https://user-images.githubusercontent.com/67718774/205948659-e4b2b8ac-c8a8-4b42-8e96-e0627976dea7.png)


After some playing around with the values of ia, id, and is (the colour values for ambient, diffuse, and specular), the resulting output was a car with working normals!

![image](https://user-images.githubusercontent.com/67718774/205949315-91258448-e1f9-4c63-b39b-8be9066e1b80.png)

Now I had to add some interactivity with the lights.

#### Light Interactivity

Firstly, keystrokes to move the light around the scene were implemented using the same technique as with the camera and object movement/rotation. Moving the light around was done by using the LightPos attribute that was created with the light, as shown:

![image](https://user-images.githubusercontent.com/67718774/205955923-8dc94990-5f14-4cbf-87f8-d6a6e9febea1.png)

The movement values were kept in line with the other movement values in the program.

Next, I added keystrokes to allow the user to change the strength of all three constants at once so the light could essentially be turned 'off' and 'on'. This was done by having certain keystrokes increase/decrease all 3 constants at once by a small amount in the Update() function, to allow for smooth adjustments to be done. Additionally to this, every time a constant's value was changed the new value was stored in a buffer variable. This allowed me to add an On/Off switch (with a keystroke in the key callback function that required a key to be pressed, rather than just be true) so that the constants' values could all be set to the minimum value and then set back to the previous value with the same button (O). This can be seen more clearly in the code below. 

![image](https://user-images.githubusercontent.com/67718774/205958681-17ba86f0-d0a1-42c8-9765-36473b20f32d.png)

![image](https://user-images.githubusercontent.com/67718774/205958744-29cd1a21-8dfb-4676-8be9-6ad22e4936e2.png)

Additionally, I set limits to how low/high the constant values could go so that diminishing returns on the values didn't become an issue. The values for these limits were found by adding a text value on the window to show the current value of ka, as shown: 
![image](https://user-images.githubusercontent.com/67718774/205959981-3d4c09e2-a1a2-46b6-9997-9589babc2f91.png)

I then adjusted the values through the previous keystrokes to find the values where the light was nonexistent, and where it completely washed out any colour.

## Final notes

Whilst I was unable to get the original mesh to work in the program, the new (quickly) remodelled version worked well with being able to demonstrate lighting and interaction etc. Due to personal circumstances, a lot less work was able to be done on this than originally intended - I had wished to load in multiple models or somehow find a way to get the original meshes to work, but this was beyond me at this time.

