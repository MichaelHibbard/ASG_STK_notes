# Constellations
Constellations are arrays of [satellites](Satellite.md). To expedite the process of constructing arrays, STK offers the ability to directly define a constellation object.

### Seed Satellite
To construct a constellation of satellites, you must begin with a *seed satellite*, so begin by creating a satellite object. It is assumed that all satellites in the constellation have the same capabilities as the seed satellite, so you must add whatever [sensors](sensors.md) you want to include to this satellite.

### Walker Constellation
Although you can input a constellation through "Input -> new" and selecting "Constellation", STK allows for several pre-defined constellations to be constructed for satellites. These pre-defined constellations are commonly used in industry due to their favorable properties, such as [coverage](Coverage.md).

A *Walker constellation* is characterized by "i: T/P/F", where
	- "i" is the inclination of each orbit in the constellation
	- "T" is the total number of satellites in the constellation
	- "P" is the total number of unique orbital planes
	- "F" is the relative spacing between satellites in adjacent planes 

To insert a Walker constellation into the STK scenario, right-click on the seed satellite and select "Satellite -> Walker", which brings up the following window:

