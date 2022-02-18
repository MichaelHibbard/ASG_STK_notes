# Computing Ground Coverage in Python

In the [STK application](Coverage), coverage can be defined over specific countries or US states, or at a global scale. Similar capabilities are offered in the Python API

Exactly like the STK applicaiton, one can first construct a target area to obtain a user-defined coverage definition. However, due to the fact that the GUI is not available, it is likely more straightforward to simply directly start from the coverage definition object.


## Initialize Coverage Definition

In the STK application, the coverage definition is used to tell STK the area(s) on Earth that you are interested in observing. To create a coverage definition object in the Python API, execute the following command. Throughout this section, we will assume that the desired variable name is "coverage" and the desired reference name is "MyCoverage".

```
coverage = scenario.Children.New(AgESTKObjectType.eCoverageDefinition,'MyCoverage')
```

Or, using the coverage definition object value,

```
coverage = scenario.Children.New(7,'MyCoverage')
```

For our coverage definition, we now need to define what we want to see "covered". Like the STK application, there are numerous options for this choice. Here, we will go over some of the most likely ones.


### Grid and Resolution

To access the grid of the coverage area, use

```
grid = coverage.Grid
```

Below are the common boundary types. [Here](https://help.agi.com/stkdevkit/Content/DocX/STKObjects~Enumerations~AgECvBounds_EN.html) is the documentation for all choices of coverage boundaries.

To set the resolution of the grid,

#### Country Coverage

If you want to use a custom region, such as a country or US state, then you have to manually access the shape file, unlike in the STK application. For example, to set the gridded coverage region as the United States (adjust the file path if necessary)

```
grid.BoundsType = AgECvBounds.eBoundsCustomRegions
bounds = coverageDefinition.Grid.Bounds
bounds.RegionFiles.Add(r'C:\Program Files\AGI\STK 12\Data\Shapefiles\Countries\United_States_of_America\United_States_of_America.shp')
```

The first line above tells STK that you want to use a custom boundary region. Then, the bounds for the coverage definition are accessed and set to the desired shape file located within the directory. For more than one country, use a list of the shape files.


#### Global Coverage

To define global coverage, use:

``` 
grid.BoundsType = AgECvBounds.eBoundsGlobal
```

Since this is global coverage, there are no other parameters necessary.


#### Coverage between specified Latitudes

To define the coverage area in terms of a minimum/maximum latitude, use

```
grid.BoundsType = AgECvBounds.eBoundsLat
bounds = coverageDefinition.Grid.Bounds
bounds.MaxLatitude = <max latitude in degrees>
bounds.MinLatitude = <min latitude in degrees>
```


#### Setting the Resolution

The resolution defines the size of each square in the gridding of the coverage area. Each square is based on the degrees of latitude and longitude that it covers on the Earth's surface. The resolution can be set or changed according to

```
grid.ResolutionType = AgECvResolution.eResolutionLatLon
grid.Resolution.LatLon = <desired latitude/longitude resolution>
```

Alternatively, the grid resolution can be defined in terms of the distance in kilometers of each side of a grid square. To use this approach instead, use

```
grid.ResolutionType = AgECvResolution.eResolutionDistance
grid.Resolution.Distance = <desired resolution distance in km>
```


### Computing Coverage for Asset(s)

Now that we have constructed an area and defined the resolution of the grid characterizing it, we can add objects, such as a [satellite](Python_API_satellite.md) to consider when computing the coverage of the area. To add an object,

```
coverageDefinition.AssetList.Add(<object type>/<object reference name>)
```

If we have children objects that we want to use (e.g. a sensor on a satellite), then use:

```
coverageDefinition.AssetList.Add(<parent object type>/<parent object reference name>/<child object type>/<child object reference name>)
```

Once the object is added, you can compute the coverage over the scenario time horizon using

```
coverageDefinition.computeAccesses()
```


### Computing Coverage Over SubInterval

The default in STK (as well as the STK Python API) is to compute the coverage of the specified assets over the entirety of the scenario time interval. However, it is also possible to determine the coverage over sub-intervals of this time period. To do so in the Python API, use the following commands:

```
start = "<day of month> <first 3 letters of month> <year> <hh:mm:ss>"
stop = "<day of month> <first 3 letters of month> <year> <hh:mm:ss>"
coverageDefinition.Interval.AnalysisInterval.SetStartAndStopTimes(start,stop)
```


### Accessing Coverage Regions

Once the coverage has been determine over the access interval, it may be desired to have direct access to the data displaying which regions are covered. To save this data as a text file, use

``` 
coverageDefinition.ExportAccessesAsText('<file name>.txt')
```


## Visualizing Coverage

To visualize the coverage map obtained, one must insert a "figure of merit", as in the case of the STK application. To insert a figure of merit for the current coverage definition, use



