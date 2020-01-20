This is an automated redistricting plugin for QGIS. It's written as a proof-of-concept, though it will likely work in production environments.

This plugin takes an input file and automatically divides it into areas of roughly equal population using a flood fill method.

To use this plugin:
1. Create a new column on your target vector file and populate it with 0 as the default value. This will be your district column.
2. Open the auto redistricting plugin.
3. Select the population field of your target vector file, your district column, and any optional geography field. The geography field will force the program to fill any blocks in the active geography (for instance, a census tract) before selecting any blocks from any other geographies.
4. You can select your number of target districts. Note the program only uses this to calculate the cutoff population, and will not "force" this number of districts. This is by design, as you may have a target shapefile which is not contiguous, and where hitting the desired number of targets is impossible.
5. You can also select the cardinal direction in which you want the plugin to "sweep," or how the software selects the next active district. Default is west to east.

Please note this runs very slowly on block mesh files. Be prepared to give it a couple of hours. It's written to make sure QGIS doesn't go unresponsive while it runs.

The program's main loop:
+ Pick a polygon
+ Find that polygon's intersecting neighbors
+ If any of those neighbors do not have an assigned district, assign a district:
  - if a geography has been selected and the neighbor has the same geography as the active polygon;
  - if the district's population threshold has not yet been met.
+ If a district has no more available possibilities for expansion, determine whether the lower population threshold has not been met, or if the district is a one-polygon enclave. If either of these are true, then reassign the district to that of a neighboring district, even if that raises the district's population.

The plugin is (c) 2020 by John Holden and released under the GNU GPL v3.0.
