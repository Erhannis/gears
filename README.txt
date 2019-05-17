                   .:                     :,                                          
,:::::::: ::`      :::                   :::                                          
,:::::::: ::`      :::                   :::                                          
.,,:::,,, ::`.:,   ... .. .:,     .:. ..`... ..`   ..   .:,    .. ::  .::,     .:,`   
   ,::    :::::::  ::, :::::::  `:::::::.,:: :::  ::: .::::::  ::::: ::::::  .::::::  
   ,::    :::::::: ::, :::::::: ::::::::.,:: :::  ::: :::,:::, ::::: ::::::, :::::::: 
   ,::    :::  ::: ::, :::  :::`::.  :::.,::  ::,`::`:::   ::: :::  `::,`   :::   ::: 
   ,::    ::.  ::: ::, ::`  :::.::    ::.,::  :::::: ::::::::: ::`   :::::: ::::::::: 
   ,::    ::.  ::: ::, ::`  :::.::    ::.,::  .::::: ::::::::: ::`    ::::::::::::::: 
   ,::    ::.  ::: ::, ::`  ::: ::: `:::.,::   ::::  :::`  ,,, ::`  .::  :::.::.  ,,, 
   ,::    ::.  ::: ::, ::`  ::: ::::::::.,::   ::::   :::::::` ::`   ::::::: :::::::. 
   ,::    ::.  ::: ::, ::`  :::  :::::::`,::    ::.    :::::`  ::`   ::::::   :::::.  
                                ::,  ,::                               ``             
                                ::::::::                                              
                                 ::::::                                               
                                  `,,`


https://www.thingiverse.com/thing:2854963
Public Domain Involute Parameterized Gears: Powered Up by TrinaryLogic is licensed under the Creative Commons - Public Domain Dedication license.
http://creativecommons.org/publicdomain/zero/1.0/

# Summary

This is an update to the Public Domain involute Gears library by @3dexplorer, with optimisations by @zkarcher. 

This library provides a module called gear(), which makes ordinary gears, helical gears (twisted like a screw), inner gears (teeth on the inside), and partial gears (a wedge rather than a full disk). It also provides a module called rack(), which creates a bar with teeth that will mesh with the gears (also optionally helical gears), so you can generate a rack and pinion set.

The SCAD file also includes an example gear train. If you use the View/Animate command in OpenSCAD, you can see the gears and rack mesh and rotate together. If you change the number of teeth, the animation still rotates correctly. 

This library is pretty basic compared to some others here on Thingiverse, but sticking to the basics gives you more freedom to customise the output. It's probably missing a few useful things, so feel free to make improvements!

It's also Public Domain, as the original authors wished, so you don't need to worry about any licensing problems if you redistribute it as part of a larger more complex project.

# Changes from previous versions

## General

The code has been bought up to date with the current versions of OpenSCAD, eliminating all the warnings it previously generated. No bleeding-edge features are used, so it still works on 2015 versions of OpenSCAD.

## Module: gear()

* **twist parameter has changed**
  twist is now specified as a helical angle, so 45 degrees will mesh the same regardless of gear height.
* Helical gears are now much smoother, with higher resolution produced for extreme twist angles or taller gears.
* Now supports hole sizes larger than the gear to produce inner gears that fit *inside* the given sized hole, with the teeth on the inside.
  Note that any clearance specified needs to be negative in this case.


## Module: rack()

* twist parameter added
  **You can now have racks that mesh with helical gears!**
  twist is specified as a helical angle, so 45 degrees will mesh the same regardless of gear height.
  This has changed positional parameters slightly, coming in after "height" and before "pressure angle". I recommend using named parameters when setting advanced parameters on the modules.

## New Function: foot_radius(mm_per_tooth,number_of_teeth,clearance)

This additional function calculates the radius at the inside of the teeth properly.

# Instructions

## Using this Library

This is a library for OpenSCAD and should be placed in your project directory and included by putting "**use &lt;publicDomainGearV1.3_trinarylogic.scad&gt;**" in your project file.

This will pull in the provided modules and functions, without generating the included example gear set.

Note that all gears intended to mesh should have the same mm_per_tooth, twist, and pressure_angle.

## Module: gear()

Generates involute spur gears, inner gears, helical gears, and inner helical gears.

The following parameters are available:
* **mm_per_tooth** *default: 3*
  This is the "circular pitch", the circumference of the pitch circle divided by the number of teeth
* **number_of_teeth** *default: 11*
  Total number of teeth around the entire perimeter
* **thickness** *default: 6*
  Thickness of gear in mm
* **hole_diameter** *default: 3*
  Diameter of the hole in the center, in mm
  If hole_diameter is larger than the gear radius, an inner gear is produced.
* **twist** *default: 0*
  Helical gear angle, in degrees.
  Positive values produce a left-hand helix, Negative values produce a right-hand helix.
* **teeth_to_hide** *default: 0*
  Number of teeth to delete to make this only a fraction of a circle
* **pressure_angle** *default: 28*
  Controls how straight or bulged the tooth sides are. In degrees.
  The default of 28 is good for most things, extremes don't work properly.
* **clearance** *default: 0.0*
  Gap between top of a tooth on one gear and bottom of valley on a meshing gear (in millimeters)
  This should be negative for inner gears.
* **backlash** *default: 0.0*
  gap between two meshing teeth, in the direction along the circumference of the pitch circle

## Module: rack()

Generates (involute) racks and helical racks for rack and pinion systems.

The following parameters are available:
* **mm_per_tooth** *default: 3*
  This is the "circular pitch", the circumference of the pitch circle divided by the number of teeth. For racks, this is simply the spacing of adjacent teeth.
* **number_of_teeth** *default: 11*
  Total number of teeth along the rack
* **thickness** *default: 6*
  Thickness of rack in mm
* **height** *default: 120*
  Height of rack in mm, from tooth top to far side of rack.
* **twist** *default: 0*
  Helical gear angle, in degrees.
  Positive values produce a left-sloping rack, Negative values produce a right-sloping rack.
* **pressure_angle** *default: 28*
  Controls how straight or bulged the tooth sides are. In degrees.
* **backlash** *default: 0.0*
  gap between two meshing teeth, in the direction along the circumference of the pitch circle


## Function: polar(r,theta)

Converts polar to cartesian coordinates.
Returns a coordinate at the given angle and distance from the origin.

It takes the following parameters:
* **r*
  The radius of the curcle the point lies on.
* **theta**
  The angle from the origin the point lies at.


## Function: pitch_radius(mm_per_tooth,number_of_teeth)

Calculates the gear radius at the middle of the tooth.
Gears should be placed apart at the distance of the sum of their pitch radii.

It takes the following parameters:
* **mm_per_tooth** *default: 3*
  This is the "circular pitch", the circumference of the pitch circle divided by the number of teeth
* **number_of_teeth** *default: 11*
  Total number of teeth around the entire perimeter


## Function: outer_radius(mm_per_tooth,number_of_teeth,clearance)

Calculates the gear radius at the outside of the tooth.

It takes the following parameters:
* **mm_per_tooth** *default: 3*
  This is the "circular pitch", the circumference of the pitch circle divided by the number of teeth
* **number_of_teeth** *default: 11*
  Total number of teeth around the entire perimeter
* **clearance** *default: 0.0*
  Gap between top of a tooth on one gear and bottom of valley on a meshing gear (in millimeters)
  This should be negative for inner gears.


## Function: foot_radius(mm_per_tooth,number_of_teeth,clearance)

Calculates the gear radius at the inside of the tooth.

It takes the following parameters:
* **mm_per_tooth** *default: 3*
  This is the "circular pitch", the circumference of the pitch circle divided by the number of teeth
* **number_of_teeth** *default: 11*
  Total number of teeth around the entire perimeter
* **clearance** *default: 0.0*
  Gap between top of a tooth on one gear and bottom of valley on a meshing gear (in millimeters)
  This should be negative for inner gears.