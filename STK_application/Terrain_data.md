# Terrain Data
Although STK interfaces with Bing (?) to provide an accurate rendering of the Earth's surface, it is possible to use your own terrain data to more accurately capture how the local topology of Earth affects the scenario (such as Azimuth/Elevation masks, etc.)

Talk to Jesse about using the hard drive with high-quality terrain data.

### Accessing Terrain Data

The STK license that we have comes equipped with an example terrain data set. To access this data, first right-click on the scenario object in the "Object Browser" panel and click on "Properties". You should see:

![](terrain_window.PNG)

Navigate to the "Terrain" tab and click "Add" on the right-hand side. The example data set should be found at "C: \\Program Files\\AGI\\STK 12\\Data\\Resources\\stktraining\\samples\\hoquiam-e.dem". 

At the bottom, click "Apply" and then "OK". Doing so analytically adds this terrain data, HOWEVER, we must still visually apply the terrain data!

To do so, go to "Utilities -> Imagery and Terrain Converter". Navigate to the "Terrain Region" tab, as shown below. We need to convert the input ".dem" file to a ".pdtt" file. Under the "Terrain Source", select the desired ".dem" file. Then, choose the output directory and give a descriptive filename.

- - - 
**N.B. :** It is recommended to save the output file to your current scenario directory.
- - -
- - - 
**N.B. :** The provided ".dem" file is the area around Mt. St. Helen's in Washington.
- - -

![](terrain_converter_window.PNG)

To apply the terrain data to the 3D viewer window, select "Globe Manager" in the 3D window menu. In the panel, select "Add Terrain and Imagery" (the blue plus sign)

![](globe_manager.PNG)

In the window that opens, navigate to the directory where you saved your terrain data. Check the terrain data and click "Add". Click "YES" to include analytically.

![](terrain_window.PNG)

- - -
**N.B. :** Under the globe manager panel, you can highlight the terrain region in the 3D viewer window by right-clicking on the ".pdtt" file and selecting "toggle extents".
- - - 

### Accessing Terrain Data from Hard Drive
TODO
