# Report and Graph Manager

There are a number of types of reports and graphs that the STK application can generate for each of the [STK objects](STK_application/STK_objects.md) present in your scenario.

To make a report, either click on the "Report and Graph Manager" icon (a calculator with a graph behind it), or go to "Analysis -> Report and Graph Manager"

Depending on the type of object, different reports are available. To switch the type of object considered, click the "Object Type" scroll option.

![](STK_application/STK_application_figures/report_and_graph_window.PNG)

For example, we can generate a report for the "latitude, longitude, altitude" (LLA) of a satellite by choosing the "[satellite](STK_application/STK_App_Objects/Satellite.md)" object and then, in the panel on the right, choosing "LLA Position". Note that there are two options here:
	- *LLA Position with a graph next to it*: this option generates a plot of the LLA components over the simulation time
	- *LLA Position with a calculator next to it*: this option generates a report of the LLA components over the simulation time
Many of the options in the right-side panel have a similar choice.

The resulting report and graph should look like:

![](STK_application/STK_application_figures/report_and_graph_output.PNG)

- - - 
**N.B. :** To quickly access the report or graph in the future, click the "Quick Report" button at the top of the output window in the figure above. Once added, the report (or graph) can be easily accessed by clicking on the "Quick Report Manager" at the top of the STK window (it appears as a calculator with a lightening bolt)
- - -

### Custom Reports and Graphs
In the previous discussion, we used a template for the data that we include in the report and/or graph. STK additionally allows the option to create custom reports, which include any of a number of data options tracked for a given object.

Once the desired object is selected, the custom report should be added to the "*scenario name* Styles" folder in the right-side panel. Once this folder is selected, choose "create new style report" or "create new style graph", which are buttons in the menu above the panel with a "star" on them.

Clicking on one of these options will bring up a new window, where you can add the desired "data providers" (i.e. data that is being tracked about the object) to the report contents on the right.

Below, 

![](STK_application/STK_application_figures/custom_report.PNG)

- - - 
**N.B. :** You can both change the report units and export as a .csv file using the menu options at the top of the report window.
- - -