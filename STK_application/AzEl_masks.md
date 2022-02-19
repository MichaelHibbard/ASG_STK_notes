# Azimuth-Elevation Masks
Given [terrain data](STK_application/Terrain_data.md), it is often of interest to determine how the topology of the terrain affects [access](STK_application/Computing_Access.md) capabilities. For example, a [place](STK_application/STK_App_Objects/Place.md) may not be able to communicate with a [satellite](STK_application/STK_App_Objects/satellite.md) if there is a mountain obstructing the line-of-sight

A visualization of what is meant by an Azimuth-Elevation mask is shown below.

![](STK_application/STK_application_figures/az_el_mask.PNG)

### Include an Azimuth-Elevation Mask

To include the azimuth-elevation mask for a ground site (e.g. a [place](STK_application/Place.md) or a [facility](STK_application/STK_App_Objects/facility.md)) given the terrain data, right click on the desired object and select "Properties". Select the "AzElMask" tab under "Basic" options, and choose to use the terrain data. Furthemore, check "Use Mask for Access Constraint" to account for terrain when computing line-of-sight with a satellite.

![](STK_application/STK_application_figures/az_el_mask_window.PNG)


### Visualize an Azimuth-Elevation Mask

To visualize an AzEl mask, remain in the properties window and navigate to AzElMask in the 2D Graphics, and select "show at range".

![](STK_application/STK_application_figures/az_el_mask_show_window.PNG)

The resulting 3D viewer window should show something like:

![](STK_application/STK_application_figures/az_el_mask_3D.PNG)

The place (Mount_St_Helens_WA) is able to access any object (assuming it has a sensor) that has a line-of-sight above the blue area.