# Constructing Satellites in the Python API
This page discusses the creation of satellites in the [Python API](STK_Python_Getting_started.md). The syntax used in creating a satellite object is essentially the same as the orbit wizard tool used in the creation of a [satellite object](STK_application/STK_App_Objects/Satellite.md) in the STK application.

A satellite object can be input into the current scenario using the following command:

```
<satellite variable name> = <current scenario name>.Children.New(AgESTKObjectType.eSatellite, <satellite reference name>)
```

- - -
**Note:** throughout this section, we will assume that the satellite variable name is "*satelllite*" and the reference name is "*mySatellite*".
- - -


## Defining the Satellite orbit

In the Python API, you can fill in the [Keplerian orbital elements](https://en.wikipedia.org/wiki/Kepler_orbit) as follows.


#### Setting the Propagator

First, set the propagator for the orbit (given the initial condition, what ODE solver to use):

```
satellite.SetPropagatorType(AgEVePropagatorType.<desired orbit propagator>)
propagator = satellite.Propagator
```

The utility of the second line is that it allows us to directly set the propagator parameters.

There are several options that you can use, which mostly differ in what forces are included (see the [STK API documentation](https://help.agi.com/stkdevkit/Content/DocX/STKObjects~Enumerations~AgEVePropagatorType_EN.html) for a complete list of all propagators). The likely ones that one may wish to include for satellites are:

- ```ePropagatorTwoBody``` : the "simplest" satellite orbit propagator, only includes the gravitational force of Earth (which is modeled as a point mass). *This is the standard Keplerian orbit which assumes a spherical Earth*
- ```ePropagatorJ2Perturbation``` : A satellite orbit propagator that additionally includes J2 (i.e. the first-order) perturbation forces, which stem from the fact that the Earth is not a perfect sphere, but an oblate spheroid.
- ```ePropagatorJ4Perturbation``` : A satellite orbit propagator that further includes the J4 (i.e. second-order) perturbation forces to the oblate-ness of the Earth.
- ```ePropagatorHPOP``` : **H**igh **P**recision **O**rbit **P**ropagator, which I believe includes the aforementioned perturbations as well as atmospheric forces (i.e. drag) as well as (???) lunar and solar forces

- - -
**N.B. :** For our purposes, simply using the ```ePropagatorTwoBody``` propagator is likely sufficient (will ignore station-keeping control actions).
- - -


#### Setting the Keplerian Orbital Parameters (i.e. the Initial State)

For our purposes, we will assume a standard Keplerian orbit for the satellites. In the above link, a Keplerian orbit can be parameterized by a set of five orbital elements:
	- *semimajor axis length*: radius of the largest dimension of the elliptical orbit
	- *eccentricty*: a value on (0,1] characterizing the oblateness of the elliptical orbit
	- *inclination*: angle between the reference plane and the orbit plane
	- *longitude of ascending node*: angle between the reference direction and the upward crossing of the orbit through the reference plane (in STK this parameter is known as the *RAAN* (right ascension angle))
	- *argument of periapsis*: angle between the ascending node and the periapsis (In STK this parameter is known as the *argument of perigee*)

and the position of a satellite on this orbit can be characterized by
	- *true anomaly*: measured from periapse (closest point to Earth in the orbit), the angle defining the position of the satellite in the orbit

To set these parameters, we need to access the propagator just created

```
orbitState = propagator.InitialState.Representation
orbitStateClassical = orbitState.ConvertTo(AgEOrbitStateType.eOrbitStateClassical)
```

Here, we have chosen to set the initial state of the orbit propagator to be defined by classical orbital elements using ```eOrbitStateClassical```. Again, there are several options for how to define the initial state. In orbital debris problems (or at least from my recollection of the class 😎), it may be preferable to set the initial state of the satellite (or other orbiting object) using the Cartesian orbital elements, consisting of the initial position and velocity. To use this choice, use ```eOrbitStateCartesian```. For now, I will assume that we are using the classical parameters.

Now, set the parameters:

```
# Set the size and shape of the orbital ellipse
orbitStateClassical.SizeShapeType = AgEClassicalSizeShape.eSizeShapeSemimajorAxis
orbitStateClassical.SizeShape.Eccentricty = <eccentricty value>
orbitStateClassical.SizeShape.SemiMajorAxis = <semimajor axis value>

# Set the orientation of the orbital ellipse, need to define RAAN type.
orbitStateClassical.Orientation.Inclination = <inclination value>
orbitStateClassical.Orientation.ArgOfPerigee = <argument of perigee value>
orbitStateClassical.Orientation.AscNodeType = AgEOrientationAscNode.eAscNodeRAAN
orbitStateClassical.Orientation.AscNode.Value = <RAAN value>

# Set the initial position of the satellite in the orbit through true anomaly. Since # there are multiple ways to characterize the initial position through classical
# orbit parameters, need to specify.
orbitStateClassical.LocationType = AgEClassicalLocation.eLocationTrueAnomaly
orbitStateClassical.Location.Value = <true anomaly value>
```


#### Propagating the Orbit

To propagate the position of the satellite over the time horizon of the current scenario given the initial position and the orbit, simpy execute the following commands:

```
orbitState.Assign(orbitStateClassical)
propagator.Propagate()
```


## Attaching a Sensor
As discussed in the [STK application notes](STK_application/STK_App_Objects/Sensors.md), a sensor is a "child" object that can be attached to a "parent" object, such as a satellite. Here, we will discuss the process of adding a sensor to a satellite, although sensors functionally work in the Python API for most other object types (e.g. a place or a facility).

To attach a sensor to a defined satellite with variable name "sensor" and reference name "MySensor" to a given satellite, use

``` 
sensor = satellite.Children.New(AgESTKObjectType.eSensor,'MySensor')
```

or using the object value index (which leads to code that is more compact but less readable, in my opinion),

```
sensor = satellite.Children.New(20,'MySensor')
```


### Sensor Properties

For our purposes, we will most often assume that the sensor onboard the satellite is the default sensor type, which is a [simple conic](STK_application/STK_App_Objects/Satellite.md) in the STK application, characterized by the sensor half-angle. To set this for the sensor attached to the satellite, use the following code:

```
sensor.CommonTasks.SetPatternSimpleConic(<cone half angle in degrees>,<angular resolution>)
```

- - - 
The [angular resolution](https://en.wikipedia.org/wiki/Angular_resolution) is the minimum angle at which different details can be detected. This parameter is necessary but I do not have much intuition. If you want a spatial resolution of $x$ meters at an altitude of $h$ kilometers, **then the angular resolution (using small angle identity for sin) is $x/(1000*h)$**. Use something reasonable unless specified in the project. Note that this angular resolution must satisfy the Rayleigh Criterion, where the angle must be greater than $1.22\lambda/D$, where $\lambda$ is the wavelength of the light (we are likely interested in visible light) and $D$ is the diameter of the len's aperture *on the satellite*. Note that the shortest wavelength of visible light is  is violet at about $0.4 \mu m$. Putting together this information, a reasonable guide to selecting this value is

$x/(1000*h) \geq 1.22 * 0.4*10^{-6} */D$ 

So, for example, using $D=1m$ and an altitude of $500km$, the minimum spatial resolution is about $0.25$ meters. Note that this ignores any atmospheric effects and is just a rough estimate.
- - - 

An alternative yet simple characterization of the sensor is by assuming that it is rectangular (note that this means that the attitude of the spacecraft now affects the sensing region!). To use a rectangular region, use the following command:

```
sensor.CommonTasks.SetPatternRectangular(<vertical half angle>,<horizontal half angle>)
```

Here the ```vertical half angle```  is the angle from the boresight direction to the edge of the sensor in the XZ plane, while the ```horizontal half angle```  is the angle from the boresight direction to the edge of the sensor in the YZ plane

Note that angular resolution is an optional field here.