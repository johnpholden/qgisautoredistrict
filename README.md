# qgisautoredistrict
An automated redistricting/reapportionment plugin for QGIS3.

This should be considered a proof-of-concept, as the plugin does a decent job of normalising populations but does not produce "perfect" districts at this time.

Installation:
Download as a zip and perform "install plugin from zip" from the plugin manager.

Instructions for use:
1. Load a vector file with a population column and an optional geography column.
2. Create a new integer (Whole Number) field on the vector file using the Field Calculator. (You can access the field calculator by right-clicking on the layer, selecting "Attributes...", and then clicking on the abacus icon in the Attributes toolbar. I typically call these columns AUTODIST01.)
  * Alternatively, you can reset a field/column of your choice to all zeroes using the field calculator. The column must be all zeroes for the plugin to run correctly.
3. Launch the plugin from the plugin menu and set the parameters. Click OK when you are ready.
4. Wait. This can take up to a couple hours.

Notes
* The plugin "sweeps" your file from a given starting direction when creating districts. By checking the box, you can rotate through directions, so your first district sweeps from west to east, then east to west, et cetera. This may or may not give better results, but the option's there.
* The plugin will do its best to create the target number of districts, but depending on how it runs may overshoot or undershoot the number slightly. The target number simply tells the program when it should stop trying to create districts based on population.
* The geography field tells the software to try to fill the current geography before moving on to any other geographies. That's a bit poorly worded, but imagine you have a map with 7-digit SA1s as a geography column. To start, the program will pick a mesh block, and then try to assign all of adjacent SA1 mesh blocks with the same SA1 value as the current mesh block before moving on to its neighbors. I highly recommend using a geography field for smoother results.
