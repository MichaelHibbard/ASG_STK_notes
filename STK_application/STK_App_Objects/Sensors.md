# Sensors
A sensor is an [STK_Objects](STK_application/STK_Objects.md) that can be thought of as a "child object" since it must be attached to a parent object, and takes on the location and orientation of the parent object, such as a [satellite](STK_application/STK_App_Objects/Satellite.md), [facility](STK_application/STK_App_Objects/Facility.md), or other stationary or moving object.

### Inserting a sensor
To insert a new sensor, go to "insert -> new" and click "sensor". The most simple choice is "insert default", for which you then choose an already-defined object to attach the sensor.

The sensor will then appear underneath the chosen object in the "Object browser" panel.

### Sensor Properties
Changing sensor properties is accomplished by right-clicking on the sensor in the "Object browser" panel.

Depending on the type of parent object that the sensor object is attached to, different options are possible to adjust. For example, when the sensor is attached to a place, one can adjust the cone half-angle. In the figure below, it is set to 90 degrees.

There are many constraints that can be applied to the sensor. The constraints section is located at the bottom of the left-hand side of the "properties" window.

In the figure below, we have added a maximum range constraint to a sensor placed in Austin, TX.

![](STK_application/STK_application_figures/max_range_place_sensor.PNG)

### Sensors with AzEl Masks
[Azimuth-Elevation masks](STK_application/AzEl_masks.md) constrain the sensing region by considering how the topology of the terrain affects the line-of-sight of the sensor. To incorporate an AzElMask into sensor constraints, begin by loading the terrain data, as discussed [here](STK_application/Terrain_data.md).

Right clicking the sensor and selecting "properties", navigate to the constraints tab and under "basic", check "Az-El Mask", as shown below.

![](STK_application/STK_application_figures/AzEl_mask_constraints.PNG)

To visualize these constraints, go to the 2D graphics tab. Under "Field of View", select "Use constraints, AzElMask". For example, due to the occlusion of Mount St. Helen's, the resulting sensor access region (using the same maximum range constraint as before), should have a noticeable region occluded:

![](STK_application/STK_application_figures/azelmask_sensor_occlusion.PNG)

### Sensors with Occluding Buildings or Other Objects
It may also be the case that a building or other object may prevent a sensor from obtaining a line-of-sight with another sensor / object. In this case, STK also allows for modeling such a situation.

In this case, we can define our own AzEl Mask for this non-terrain occlusion.

To define a building, we can enter a new [facility](STK_application/STK_App_Objects/Facility.md) object. In the panel at the top, we can then move it to the desired location by clicking on the "Yellow box with a cursor" (the object to move is in the scroll menu at right, if it is not the desired occluder, change it to be so).

Shift + click to place the occluder at the desired location and check the "yellow box with a green check" to save the choice.

In the example below, we have placed our "river facility" near an occluding building. Clearly, the occulder should prevent some of the sensor's field-of-view from obtaining a valid line-of-sight.

![](STK_application/STK_application_figures/occlusion_not_accounted_for.PNG)

We need to construct an AzEl Mask for this occluding building. To do so, right click on the sensor that should have an occlusion, and go to "Sensor -> AzEl Mask...".

![](STK_application/STK_application_figures/az_el_mask_occluder_window.PNG)

Select the object that should occlude the sensor, in this case, the "Occluder" object. Give a descriptive name and click compute. In the resulting pop-up window, save the file to your scenario folder. After computing, select "Apply" and then close.

To apply the mask file, right-click on the sensor and select "Properties". Under the "Basic, sensor AzEl Mask" tab, select "Mask File" under use and navigate to the ".bmsk" file just saved.

![](STK_application/STK_application_figures/choose_mask.PNG)

To view the resulting mask, navigate to "2D graphics" and under "Projection -> Field of View", make sure that "Use constraints" is checked. Then, make sure that BOTH "AzElMask" and "SensorAzElMask" are selected (to ensure that both terrain and other occlusions are considered) by ctrl+clicking both of them. Click apply. The result should appear similar to:

![](STK_application/STK_application_figures/occluder_sensor_final.PNG)

