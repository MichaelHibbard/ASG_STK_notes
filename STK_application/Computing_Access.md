# Computing Access
"Access" refers to the times of the simulation for which two objects can interact. Note that access requires each of these objects to have a [sensor](STK_application/STK_App_Objects/Sensors.md) attached to them.

In general access requires that there exists a line-of-sight between the sensors. However, STK allows a large number of alternative definitions. For our purposes, this definition of "access" is likely sufficient.

### Computing Access
To open the access tool, one can either click on the "green and yellow squares" icon in the top menu bar, or go to "Analysis -> Access".

The access window will look like the following:

![](STK_application/STK_application_figures/access_window.PNG)

The "Access for" at the top can be thought of as the "from sensor", which can be changed by clicking the "Select Object" button.

The panel on the left gives the options for the "to sensor". Note that clicking the "+" allows us to see the attached sensor on the satellite, or whatever other object you may have created.

Once you have chosen your desired "from sensor ... to sensor ...", click "Compute" to determine the access times between the sensors.

To view the results, click on the "Access" button on the "Reports" tab.

Note that it may be possible that the two sensors are never able to access one another, which means that the report will simply say "No Access Found".

Below, I have computed the access between sensor 2, located in Austin, TX, and sensor 3, attached to a new satellite named "Satellite2":

![](STK_application/STK_application_figures/access_report.PNG)

Similarly, from the same "Reports" tab, one can also generate a report that gives the azimuth and the elevation at each time step for which the sensors are able to access one another.

### Displaying Access Times
To display the time interval on the "Timeline" for which a pair of sensors are able to access one another, click on "Add Time Components" (icon second from left in the Timeline view). A computed access interval will appear as a "key" icon under the "from" sensor. Click on the desired interval.

Once clicked, in the panel on the right, an "AccessIntervals" option should be present. Click "OK" to add it to the Timeline.

![](STK_application/STK_application_figures/add_access_interval.PNG)

The access interval will now appear in the Timeline at the bottom of the STK window.

- - - 
**N.B. :** Once an access interval is computed, STK will automatically update it when either of the sensor properties are changed (either the "from" or the "to" sensor)!
_ _ _

