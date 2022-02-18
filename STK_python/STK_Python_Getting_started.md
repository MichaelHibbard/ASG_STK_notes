# Getting Started in the Python API
Although the STK application provides a large number of functionalities, it may be preferable to integrate the capabilities of STK into your own code.

## Initialization
There are a few ways that you can integrate STK into your Python code:
	- *STK Engine* allows you to avoid opening the STK application while running code.
	- *STK* itself: opens the STK application in the process of running code.

Opening the STK application while running your code adds additional overhead, but may be more intuitive if you've familiarized yourself with the STK application.

Furthermore, you can still set the graphics to be visible when using STK engine, you simply don't open the entire STK application.

Depending on which one you want to use, it may be helpful to include the following lines of code at the beginning of your script, allowing you to easily switch between using STK and STK engine.

```

# Set whether to use STK or the STK engine
useStkEngine = True

# If you are using STK engine, set whether or not graphics are desired
noGraphics = True

############################################################################

# Scenario Setup

############################################################################

if (useStkEngine):

	# Launch STK Engine with NoGraphics mode
	print("Launching STK Engine...")
	stk = STKEngine.StartApplication(noGraphics)

	# Create root object
	stkRoot = stk.NewObjectRoot()

else:

	# Launch GUI
	print("Launching STK...")
	stk = STKDesktop.StartApplication(visible = True, userControl = True)

	# Get root object
	stkRoot = stk.Root

# Set date format 
stkRoot.UnitPreferences.SetCurrentUnit("DateFormat", "UTCG")
  
# Create new scenario
print("Creating scenario...")
stkRoot.NewScenario('PythonEngineExample')
scenario = stkRoot.CurrentScenario

# Set time period
scenario.SetTimePeriod("1 Aug 2020 16:00:00", "2 Aug 2020 16:00:00")

if (useStkEngine == False) and (noGraphics == True):
	# Graphics calls are not available when running STK Engine in NoGraphics mode
	stkRoot.Rewind()

```

The above block of code functionally performs the same task as the first two figures shown in the [STK basics](STK_Basics.md) page of the application notes.


## Adding Objects to the Scenario

As in the [STK application](STK_Basics.md), the scenario just created is populated by a set of objects, such as satellites, facilities, and places.

Whereas in the application one adds an object through "Insert -> New" and then selecting the desired object, one can add new "child" objects to the "parent" scenario created in the above code block through

```
<object variable name> = scenario.Children.New(AgESTKObjectType.e<Type of object>, "<Name of object>")
```

Upon creation, one can think of the above code as adding an object to the "object browser" in the STK application.

Below is an index for object "value" references. Rather than specifically using ```AgESTKObjectType.e<Type of Object>```, one could instead place the value code here:
[https://help.agi.com/stkdevkit/Content/DocX/STKObjects~Enumerations~AgESTKObjectType_EN.html](https://help.agi.com/stkdevkit/Content/DocX/STKObjects~Enumerations~AgESTKObjectType_EN.html)

### Removing objects
To remove an object from the scenario, use the following command:
```
<object variable name>.Unload()
```


## Shutting Down STK

When you are finished with STK in Python, use the following commands to shut it down (assuming the naming convention of the initialization code block above):

``` 
stkRoot.CloseScenario()
stk.ShutDown()
```

## Code Examples
AGI provides a number of example codes for the Python API, but sometimes it seems you have to go digging for them. Below are some of the helpful links that I've found:

[https://help.agi.com/stkdevkit/index.htm#python/pythonIntro.htm?TocPath=Development%2520Environments%257CSTK%2520Python%2520API%257C_____0](https://help.agi.com/stkdevkit/index.htm#python/pythonIntro.htm?TocPath=Development%2520Environments%257CSTK%2520Python%2520API%257C_____0)
[https://help.agi.com/stkdevkit/11.4.0/Content/stkObjects/ObjModPythonCodeSamples.htm#33](https://help.agi.com/stkdevkit/11.4.0/Content/stkObjects/ObjModPythonCodeSamples.htm#33)
[https://github.com/AnalyticalGraphicsInc/STKCodeExamples/blob/master/StkEngineApplications/Python/PythonEngineExample.py](https://github.com/AnalyticalGraphicsInc/STKCodeExamples/blob/master/StkEngineApplications/Python/PythonEngineExample.py)
