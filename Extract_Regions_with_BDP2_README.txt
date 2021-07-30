/** Extract_Regions_with_BDP2_
 * Marcel Boeglin 
 * boeglin@igbmc.fr
 * May - July 2021
 */

/**
Extracts regions from images that are too big to be opened in non virtual
mode in Fiji:
1. Choose input format and working-mode:
   Check "¤ Crop whole CZT domain" to crop all Channels, Z and T (Simple mode);
   Otherwise (Full mode), you can define different C, Z and T begins and ends for
   each crop.
2. Choose input image and output folder;
3. If Bio-formats Dialog box opens, check "¤ Use virtual stack";
4. Regions creation loop:
   ¤ Full mode:
     - draw a rectangle, select first slice, channel and time-point;
     - validate by OK;
     - select last slice, channel and timepoint;
       validate by OK to define another region;
                or SHIFT-OK to terminate;
   ¤ Simple mode :
     - draw a rectangle;
     - validate by OK to define another region;
                or SHIFT-OK to terminate;
5. Crop-ROIs are saved as a zip to output folder;
6. The image is opened using BigDataProcessor2;
7. Each region is cropped in a new viewer and saved to output folder;

Tested with following input types:
 - Metamorph Multi Dimensional series (input file: .nd);
 - Leica Image Files (.lif);
 - Zeiss (.czi) pyramidal images need the crop domains to be defined in the
   highest resolution image (#1). Each crop results in pyramidal image file
   containing a number of resolutions depending on the XY size of the crop- 
   regions. The resolution sequence of output images is 1, 1/2, 1/4, ...;
 - Single plane (Z*C*T = 1) TIFFs, PNG.

Dependencies:
If the 'MemoryMonitor_Launcher' plugin is installed, the 'Memory' window opens 
when the macro is started
MemoryMonitor_Launcher.jar can be downloaded here:
https://github.com/MicPhotonIGBMC/ImageJ-Macros/blob/master/Metamorph%20Utilities/MemoryMonitor_Launcher.jar


Notes:
1. To terminate the crop-regions creation:
   Keep the SHIFT key down until the image closes to avoid creation of a new region.
2. The macro launches the "Memory" window if not open and "MemoryMonitor_Launcher.jar" 
   is found in the "plugins" folder, works without otherwise.
   "MemoryMonitor_Launcher.jar" can be downloaded here:
   https://github.com/MicPhotonIGBMC/ImageJ-Macros/blob/master/Metamorph%20Utilities/MemoryMonitor_Launcher.jar

Known problems:
1. In case of multiple-series LIF files, the macro may process another series than the one
   which was selected in the Bio-Formats window.
   This is due to the fact that the series-names synthax differs from one experiment type
   to another, causing the series-index determination potentially to fail.
2. BDP2 doesn't open properly time-series from LIF files:
   - May open only first frame in a static image;
   - Sometimes opens properly a few frames from t = 0, for instance until t = 2, then
     repeats frame t = 0 untill end of timelapse.
*/
