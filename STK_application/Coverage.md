# Coverage
For an [STK object](STK_application/STK_objects) that is non-stationary (e.g. a [satellite](STK_application/STK_App_Objects/Satellite.md) or an [aircraft](STK_application/STK_App_Objects/Aircraft.md)), it is often of interest to determine the area of Earth (or some region of Earth) that the object sensor is able to view over the course of the simulation. In other words, to determine the "Coverage" capabilities of the object.

STK provides functionalities to accomplish exactly this task. Specifically, STK allows you to analyze the global or regional coverage provided by one or more objects while considering accesses.

In this page, we will assume coverage for a satellite; however, it is straightforward to adapt to other non-stationary objects.

### How Coverage is Determined
Given a user-defined region of interest for which coverage is desired, the area is divided into a set of grid points in an area of coverage.

## Adding a Coverage Area
To add a target area for coverage, go to "Insert -> New" and select "Area Target". There are a number of options here, such as
	- Countries of the world (or states of the US)
	- Area target wizard
	- Insert Default
	- Define Properties

Alternatively, if you have a shapefile defining the points, you can use that as well.

The "area target wizard", "insert default", and "define properties" are all quite similar. Specifically, the "area target wizard" is essentially the "define properties" option, but includes a 2D world map to help guide and visualize the placement of the boundaries of the region of interest. "Insert default" simply inputs a single point; however, you can update the properties after-the-fact by right-clicking the "area target" object in the panel at left and selecting "properties".

- - - 
**N.B. :** If you want global coverage, or coverage between two latitudes, you do not need to include an "Area Target". Instead, proceed to the "Coverage Definition" section below.
- - -  

#### Area target wizard

Using the polygon shapes provided is counterintuitive since it automatically introduces curved lines between the vertices of the polygon. For this reason, I would recommend further investigating shape files rather than using any of these selection methods.

#### Select Countries
To choose multiple countries, you must "ctrl + click" the countries you wish to insert. Then, click "insert". For example, including the United States and Canada:

![](STK_application/STK_application_figures/us_canada.PNG)

## Coverage Definition
There are multiple ways to define "coverage" in STK. The specific coverage of interest is captured by a "Coverage Definition" object, which can be added by going to "Insert -> New" and choosing "Coverage Definition".

If you insert the default coverage definition, you can adjust it by later right-clicking on it in the "objects browser" and then right-clicking on "properties", and adjusting under grid. Otherwise, you can adjust these properties by choosing "Define Properties" before creating the coverage definition object.

- - -
**N.B. :** If global coverage is desired, set the minimum and maximum latitude as -90 and 90 degrees, respectively. Alternatively, set "Type" in the figure below to "global".
- - - 

You can additionally adjust the resolution of the gridding procedure that STK uses (note that an area is considered covered if a sensor can access it over the course of the simulation), as shown below. If you are working on a global scale, it is fine to use a higher point granularity.

![](STK_application/STK_application_figures/coverage_definition_properties.PNG)

To only grid a specific country change "Type" to "Custom Region". Then, select the countries that you wish to include in coverage. For countries, it is recommended to decrease the granularity of the grid. Below, we have selected to include the United States and Canada in the coverage definition, and set the point granularity to 1 degree in latitude/longitude.

![](STK_application/STK_application_figures/us_canada_gridded.PNG)

 To add which objects should be considered when determining coverage, navigate to the "Assets" tab in the above figure of the coverage definition properties.

![](STK_application/STK_application_figures/coverage_assign_asset.PNG)
 
To compute the coverage access, right-click on the coverage definition and select "Coverage Definition -> Compute Access".

## Coverage Quality
To define the quality of the coverage obtained by the chosen assets for the desired target region, you must add a "Figure of Merit" in STK, which can be added through "Insert -> new" and selecting "FIgure of Merit". Under "Define Properties", select the desired coverage definition. The default option is to consider "Simple Coverage", i.e., whether or not the the asset(s) pass over the grid region; however, many options are available. The figure below shows the simple coverage for a satellite with a target area of the United States and Canada.

![](STK_application/STK_application_figures/simple_coverage_satellite.PNG)

You can use the [report and graph manager](STK_application/Report_Graph_Manager.md) to display information related to the coverage.