# Modelling Process

The scene consists of 9 different models - described below.
1. The Garage
2. The Cars
3. Stools
4. Workstations
5. Laptops
6. Screens
7. Trolleys
8. Steering Wheels
9. Garage doors

## The Garage

The garage is probably the simplest model, and was the first to be created. It consists of various cube meshes - scaled, rotated, and joined so that they create a semi-enclosed room with 1 side open. Another cube mesh was used to create a central pillar so that the garage has two exits - one for each car.

Originally I had planned to go with a concrete-style material for the inner walls using the noise node with high detail to create a rough-looking surface. Unfortunately it just looked kind of ugly, so I decided to stick to using it only for the central pillar to showcase that it's a permanent part of the architecture. In order to emulate a modern F1 garage it seemed more appropriate for the walls and ceiling to have a glossy-looking clean material. This was done simply through adjusting the base colour, reducing metallic to zero and lowering the roughness so that light was reflected well but without being over-reflective.

## The Cars

The cars are the most important and central models of the scene - and thus the most time was put into them.
They're split into two parts - the main body (chassis) and the wheels. Keeping them as separate objects allows for the wheels to be animated separately from the rest of the body.

### Wheels
To generate the semi-filled cylinder type shape of a wheel, a cylinder mesh was created with a cap fill type of 'nothing', and then a solidify modifier was added to thicken the walls. Both the tyre and the wheel structure were created doing this and scaled to appropriate sizes.
Using just simple cylinders did cause the edges of the tyres to be very sharp, rather than the slight bulge outwards you'd expect, so some loop cuts were made around the circular face and the centre-most cuts pulled out slightly to create a curving effect and soften the edges. Finally, a subdivision surface modifier was added to add some extra resolution.
The spokes for the internal wheel structure involved loop cuts in the outside of the cylinder and then extruding specific faces at set intervals towards the wheel object. A subdivision surface modifier was added to this too to provide some curvature, as the initial extrusions looked quite 'blocky' and unsatisfying.

The materials for the wheels were also fairly simple - A dark grey material with fairly high roughness and zero metallic for the tyres, and then a light grey, high metallic, low roughness material for the wheel structure to create a silvery metal look.

### Car Body
As most great models do, the car body started as a cube. It was scaled lengthwise and loop cuts made to split the model into 3 sections. Creating the nose was as simple as scaling down the end face of the front section and moving the section down slightly. The front wing was made by performing a number of loop cuts on the underside of the nose and extruding out a small rectangle downwards. From this, the wing itself could be extruded sideways as well as the wing's endplates.

The back section was then widened and a long strip of the middle extruded upwards to create an upside down T-shape. These would serve as the sidepods, roll hoop and engine cover. Many more loop cuts were made to allow finer tuning of the shape of the chassis. On reflection, I should have utilised the mirror modifier available in Blender, rather than creating it all at once - since, despite using the grid to try mirror things by look, there are bits of the model that aren't perfectly even. Additionally, the shape of the sidepods could have been done using the sculpting tool for a more realistic look, but that may have taken away from the semi-lowpoly feel of the models.


## Stools

The inspiration and slight reference (not exact) for the garage stools was just the bog-standard breakfast stool (such as [this](https://www.simplybarstools.co.uk/semplice-bar-stool-black/)).

The main leg of the stool consisted of just an elongated cylinder, with the base support being modelled in a similar fashion to the wheels - an empty cylinder with the solidify modifier. The two were connected in the same kind of method used to model the spokes of the wheel too, with a loop cut near the base of the leg and extruding a section out to the outer ring. To create the footrest, the base ring was duplicated and the duplicate moved up to a reasonable height, and connected with the same kind of spokes. However, to add a bit more individuality to it the footrest was shortened to be only around 45 degrees rather than the full 360. This was done by performing loop cuts at each end of the desired area and then simply deleting the other edges and vertices. With a subdivision surface modifier, this actually came out better than I'd expected/hoped. 

Modelling the stool seat was a matter of creating a cylinder and then adding a loop cut near the top, selecting that top face and then scaling it down so a gradient was formed to give a rounder edge. A slightly squished sphere was cut in half and added to the underside of the seat as a support.

The seat uses a rough, dark grey material with a noise node added to simulate the rippling you'd see on the fake leather usually found on this type of stool. The leg and footrest materials were essentially the same as the wheel structures - a shiny, silvery metal.

## Workstations



