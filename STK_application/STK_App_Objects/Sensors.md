# Sensors
A sensor is an [STK_Objects](STK_Objects.md) that can be thought of as a "child object" since it must be attached to a parent object, and takes on the location and orientation of the parent object, such as a [satellite](Satellite.md), [facility](Facility.md), or other stationary or moving object.

### Inserting a sensor
To insert a new sensor, go to "insert -> new" and click "sensor". The most simple choice is "insert default", for which you then choose an already-defined object to attach the sensor.

The sensor will then appear underneath the chosen object in the "Object browser" panel.

### Sensor Properties
Changing sensor properties is accomplished by right-clicking on the sensor in the "Object browser" panel.

Depending on the type of parent object that the sensor object is attached to, different options are possible to adjust. For example, when the sensor is attached to a place, one can adjust the cone half-angle. In the figure below, it is set to 90 degrees.

There are many constraints that can be applied to the sensor. The constraints section is located at the bottom of the left-hand side of the "properties" window.

In the figure below, we have added a maximum range constraint to a sensor placed in Austin, TX.

![](max_range_place_sensor.PNG)
