# NeuroLux Software
## NeuroLux Bluetooth software installation:
All latest software can be found under Releases at https://github.com/NeuroLux-Inc/Neurolux-Software-Releases/releases/latest

NeuroLux recommends users employ the latest release of the acquisition software!

Use the NeuroLux Bluetooth Installer.msi file for the NeuroLux software installation. This is the only file you will need to get started with your Bluetooth-enabled Neurolux devices. Install on a computer with a dedicated graphics card for optimal performance. A shortcut to the application folder will be found on your desktop.

*Ensure use of BLE antenna provided with system to boost device connectivity.*

**Having trouble with your devices? Check the device troubleshooting wiki!**
https://github.com/NeuroLux-Inc/Neurolux-Software-Releases/wiki/Bluetooth-device-troubleshooting-guide

**If you discover any bugs, please feel free to post an issue on the issues page** 
https://github.com/NeuroLux-Inc/Neurolux-Software-Releases/issues

### Pairing:
Search for devices, select ‘connect’ to pair with NNV###, EEG###, IMA###, MA###. Select ‘start data stream’ to begin viewing data.

### Data saving:
‘Begin recording’ will save to a SQLite database. Date in name of file will update on pressing begin ‘Begin recording’.‘New savefile every X sec’ sets how often a new .csv (incrementally numbered) is created on export at end of session. **At end of recording, click 'batch export databases' to select a parent folder to recursively export data from all databases found in folder tree** Click 'batch export single database' to select a single SQLite file to export to .csv. A new db is created each time 'Begin recording' is pressed and for each unique device. Databases can be viewed in a SQLite viewer and manipulated as is. Note that the database needs to be sorted by time when queried, as it is not in order when saved initially. 

### Event Marking
Devices will be assigned a local event keyboard shortcut on connect, this shortcut can also be assigned by the user. A global event binding is also able to be assigned.

### Arduino Connection
An Arduino can be used to mark events and start/stop recording over serial communication. Connect to Arduinos by selecting the COM port corresponding to the Arduino in the 'Serial Ports' drop-down menu and selecting connect. By sending a 'g' over serial, a global event will be marked. Sending an 'r' will toggle starting and stopping recording data. Baud rate should be set to 9600.

### Plot Navigation
Shift + left click on plot = X axis zoom
Shift + right click on plot = X axis zoom out
Ctrl+ left click on plot = Y axis zoom
Ctrl+ right click on plot = Y axis zoom out

## Analysis

### First time setup:
1. Install a distribution of Anaconda following instructions at: https://www.anaconda.com/docs/getting-started/anaconda/install
   Note: you do not need to check the box to add anaconda to PATH environment variable
2. Open the freshly installed annaconda navigator and launch Jupyter Notebook from the navigator menu
3. Navigate to the analysis script (.ipynb) in the file browser on the left side of the window and double click to open the file. Make sure the .py file is in the same directory as the .ipynb file.
4. Click the fast-forward button at the top of the file to restart the kernel and run the notebook. 
5. You will be prompted to select the folder containing the .csv files you want to analyze. You can also select a folder containing multiple folders you want to analyze. If you are on a Mac and do not see the folder selection window, you may need to click on a python file in your dock. When selecting the folder, make sure the .csv files contain at least 1 minute of data each. Once selected, the code will execute for up to several minutes.
6. After running the code, several files will appear in the folder of the original .csv files you selected for analysis. Data is separated into chunks, demarcated by dropouts in device connectivity. Folders named "Chunk_1", "Chunk_2", etc will contain .csv's and images of chunked data. The folder named "Chunk_all" will contain .csv's and images of data from all chunks combined. The .csv ending in "_dropouts" indicated device connectivity rate. 

### Modifying CSV output/Plot output settings:
1. Install VS Code following instructions at: https://code.visualstudio.com/download
2. Open the folder containing the .ipynb and .py file. 
3. In the .py file, you can select the type of plots you want to output by toggling the plot booleans (plot_accel_x, plot_accel_y, etc). Set "scrolling" to "True" if you would like to zoom in on the data (recommended for verifying proper IMU placement). Adjust "scroll_window" to modify zoom. 
4. After modifying your parameters, save the .py file and run .ipynb in Jupyter Notebook, following the instructions above.

-------------------------------------------------------------------------------------------------

### Recommended settings for viewing overall data (no zoom):
plot_temperature = True\
plot_activity = True\
plot_HR = True\
plot_SQI = True\
use_hs_to_calculate_RR = True\
use_shannon_peaks_only_to_calculate_resp_env = True\
plot_RR = True\

-------------------------------------------------------------------------------------------------

### Recommended settings for viewing individual HR and RR peaks (with zoom):
plot_hs_sh_raw = True\
plot_hs_sh_filtered = True\
plot_HR_peaks = True\
use_hs_to_calculate_RR = True\
use_shannon_peaks_only_to_calculate_resp_env = True\
plot_resp_sig = True\
plot_RR_peaks = True\

scrolling = True\
scroll_window = 2\

-------------------------------------------------------------------------------------------------
