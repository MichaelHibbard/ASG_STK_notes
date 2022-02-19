# Satellite
A satellite is an [STK_Objects](STK_application/STK_Objects.md).

### Inserting a Satellite

To add a new satellite, go to "insert -> new" and click "satellite". If you are interested in adding a standard (or known) satellilte into the scenario, you can choose to add from the standard object database. For example, you could add the International Space Station in this manner. Using this approach is similar to the database search used for including a [facility](STK_application/STK_App_Objects/Facility.md).

Alternatively, one can define a new satellite using the "Orbit Wizard". The orbit wizard allows you to quickly construct a satellite orbit from a set of "types" of common orbits. It includes a handy visualization of the orbit as well. You can then adjust the [Keplerian parameters](https://en.wikipedia.org/wiki/Orbital_elements), a.k.a. the orbital elements, to suit your needs.

An example is shown below:

![](STK_application/STK_application_figures/orbit_wizard.PNG)

Choose the name to be more descriptive than what I have :)

Upon inserting, you will be able to see its orbit in both the 2D and the 3D plane.

- - - 
**N.B. :** You can choose to zoom to and rotate about a satellite by right-clicking the desired satellite in the object browser and selecting "zoom to". You can save this view to access quickly by 

![](STK_application/STK_application_figures/zoom_to_sat.PNG)
- - - 

### Satellite Sensors

When attaching a [sensor](STK_application/STK_App_Objects/Sensors.md) to a satellite, the default sensor is a conical viewing region, as shown below:

![](STK_application/STK_application_figures/sat_default_cone.PNG)

You can adjust the properties of the conical sensor by right-clicking the sensor in the Object browser and selecting "Properties". For this simple sensor, you are only able to change the half-angle of the cone (which defaults to 45 degrees).

### Satellite Properties
To change the properties of a satellite, right click on the desired satellite and select "Properties". In this tab, you can adjust a variety of parameters, such as
- the Keplerian parameters (such as the inclination, eccentricity, etc.)
- the attitude of the satellite (note that many pre-defined attitude controls are included, such as nadir-pointing with sun constraints)
- display properties of the satellite (such as the color of the orbit in the 2D and 3D visualizations (above, mine is set to yellow by default) )
- the model of the satellite (can choose from pre-defined model files)
- "DATA DISPLAY" in the properties window shown below allows you to include specified data in the 3D graphics window.

One possibly useful display property is to include **vectors** in the satellite visualization. These vectors can include the sun and the moon vector, as shown below (here, I have also included the sun-moon angle):

![](STK_application/STK_application_figures/vector_selection.PNG)

![](STK_application/STK_application_figures/sun_moon_vector.PNG)

These vectors may be useful to include since a common constraint is that the sensing region cannot be occluded by the Sun.

### Satellite Coverage
Please refer to [Coverage](STK_application/Coverage.md) for information on how to determine the region on Earth that a satellite is able to provide coverage of.

## Satellite Communications
STK offers the ability to model communications between satellites and stationary objects, such as [places](STK_application/STK_App_Objects/Place.md) or [facilities](STK_application/STK_App_Objects/Facility.md) on Earth.