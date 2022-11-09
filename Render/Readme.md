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

Originally I had planned to go with a concrete-style material for the inner walls using the noise node with high detail to create a rough-looking surface. Unfortunately it just looked kind of ugly, so I decided to stick to using it only for the central pillar (to showcase that it's a permanent part of the architecture). In order to emulate a modern F1 garage it seemed more appropriate for the walls and ceiling to have a glossy-looking clean material. This was done simply through adjusting the base colour, reducing metallic to zero and lowering the roughness so that light was reflected well but without being over-reflective.

## The Cars

The cars are the most important and central models of the scene - and thus the most time was put into them.
They're split into two parts - the main body (chassis) and the wheels. Keeping them as separate objects allows for the wheels to be animated separately from the rest of the body.

### Wheels
To generate the semi-filled cylinder type shape of a wheel, a cylinder mesh was created with a cap fill type of 'nothing', and then a solidify modifier was added to thicken the walls. Both the tyre and the wheel structure were created doing this and scaled to appropriate sizes.
Using just simple cylinders did cause the edges of the tyres to be very sharp, rather than the slight bulge outwards you'd expect, so some loop cuts were made around the circular face and the centre-most cuts pulled out slightly to create a curving effect and soften the edges. Finally, a subdivision surface modifier was added to add some extra resolution.
The spokes for the internal wheel structure involved loop cuts in the outside of the cylinder and then extruding specific faces at set intervals towards the wheel object. A subdivision surface modifier was added to this too to provide some curvature, as the initial extrusions looked quite 'blocky' and unsatisfying.

The materials for the wheels were also fairly simple - A dark grey material with fairly high roughness and zero metallic for the tyres, and then a light grey, high metallic, low roughness material for the wheel structure to create a silvery metal look.

### Car Body