# batch_igv
Automating image generation in IGV by generating batch script.

**Warning: Make sure no other IGV sessions are being used at the same time because they may be closed out of!!!**

The script uses external packages, therefore, before attempting to use the script one needs to verify that the following libraries are installed:
 1. Pandas
 2. ArgParse
 3. os
 4. sys
 5. time
 
 One other dependecy that the script has is it requires **igvtools** to be downloaded and installed as well.

### Positional arguments:

 1. **igvSession** - Name of IGV Session
 2. **windowSize** - Size of Window
 3. **batchFile** - Batch File Name
 4. **snapshotDir** - Snapshots Directory
 5. **variantPos** - Variant Positions
 6. **pathToIGV** - Path to IGV batch

### Optional arguments:

  **-h, --help** - show this help message and exit
  
  **--runScript** - Choice to run script in IGV automatically (Optional)
  
  **--range RANGE** - Controls how many bases are seen on either side of position
  
  

The very first argument specifies the igv session that is being used for analysis, when specifying the name include the absolute path. 

**Ex:** *C:\Users\ank22\igv_session.xml* or *macOS_igv_test_session_ak_hg002.xml*

The second argument specifies the window size, which controls how many reads you will be able to see for each track. This also influences the size of the images.

**Ex:** *400*

The third argument is the name under which you would like to save the generated batch script.

**Ex:** *NameOfBatchFile*

The fourth argument designates the snapshot directory, which is the location where the images will be saved to. The script will create the directory if it is not an already existing one.

**Ex:** *C:\Users\ank22\Documents\SnapShots* or ../snapshots/test example_positions.csv*

The fifth arguement is the file with the variant positions/locations where the snapshots need to be taken, should be expressed as a path and name as well.

**Ex:** *C:\Users\ank22\Documents\PositionSet.csv* or or *../snapshots/test example_positions.csv*

**The variant positions need to be in a csv file with headers labeled Chromosome and Position, the file may contain other information as well, however, those two are mandatory to guarantee that the script runs.**

Finally, the sixth argument is the path to the IGV batch (igv.bat for Windows users) or IGV sh (igv.sh for macOS users), which is a crucial component if batch script needs to be run automatically. Also needs to be expressed as path. 

**Ex:** *C:\IGV_2.5.0\igv.bat* or *../IGV_2.5.3/igv.sh*


Listed above are the six mandatory arguments, nonetheless, there are two optional arguments (--runScript, --range).
Including the command **--runScript** will induce the script to automatically generate images, by opening IGV and running the unique batch script. And including the argument **--range (int value)** will change the default value of 50 bp on each side of the position to desired value, modifying the amount of visible bases, and adjusting window size horizontally.  

#### Down below are examples of how you would call the script in a command line:

Example w/o optional parameter: 
```
python batch_igv.py C:\Users\ank22\igv_session.xml 400 BatchScriptName C:\Users\ank22\Documents\SnapShots C:\Users\ank22\Documents\hg002_deepvar_manual_currate.csv C:\IGV_2.5.0\igv.bat
```

Example with optional parameter: 
```
python batch_igv.py Y:\data\igv_sessions\AndreySession.xml 400 VariantPositionBatch Y:\data\SnapShots C:\Users\ank22\Documents\hg002_deepvar_manual_currate.csv C:\IGV_2.5.0\igv.bat --runScript --range 500
```

Example for macOS:
```
python batch_igv.py macOS_igv_test_session_ak_hg002.xml 400 NewBatchFile ../snapshots ../snapshots/test example_positions.csv ../IGV_2.5.3/igv.sh –runScript --range 500
```
