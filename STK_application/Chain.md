# Chain

A chain is a sequential multi-link communication between multiple objects in STK. Whereas [computing access](Computing_Access) considered only a single pair of objects, a chain considers when a larger "chain" of objects have communication between one another, in a directional sense.

For example, if we had two [places](places.md), one could add a [satellite](satellite.md) and compute a chain of "place 1 -> satellite -> place 2" to determine when place 1 can transmit info to the satellite, which can directly transmit it to place 2.

- - - 
**N.B. :** A chain object only has "Access" if the individual link in the chain has access at the given time.
- - - 

### Adding a Chain
To add a chain, go to "Insert -> new" and select "Chain". Note that the order matters when defining a chain! The chain may not have full access in one permutation of the order, but have it in another permutation.

To define the chain of objects, right-click on the created chain and select "Properties". Choose the sequence of objects to add to the chain, as shown below.

![](chain_definition.PNG)

To see the access data of the chain, right-click on the chain and select "Report and graph manager". In the right-side panel, select "Access Data" to view the report. If there are no access times, the report will say so.

![](chain_access_report.PNG)

In the 2D and 3D viewer windows, you will be able to see if there exists chain access at a given time if there exists a link between the objects, as shown below:

![](chain_access.PNG)
