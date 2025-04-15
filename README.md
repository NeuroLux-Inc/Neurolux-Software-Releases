# NeuroLux Software
## NeuroLux Bluetooth software installation:
All latest software can be found under Releases at https://github.com/NeuroLux-Inc/Neurolux-Software-Releases/releases/latest

NeuroLux recommends users employ the latest release of the acquisition software!

Use the NeuroLux Bluetooth Installer.msi file for the NeuroLux software installation. This is the only file you will need to get started with your Bluetooth-enabled Neurolux devices. Install on a computer with a dedicated graphics card for optimal performance. A shortcut to the application folder will be found on your desktop.

*Ensure use of BLE antenna provided with system to boost device connectivity.*

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
1. Install a distribution of Anaconda following instructions at: https://docs.anaconda.com/free/anaconda/install/windows/
   Note: you do not need to check the box to add anaconda to PATH environment variable
2. Open the freshly installed annaconda navigator and launch Jupyter Notebook from the navigator menu
3. Navigate to the analysis script in the file browser on the left side of the window and double click to open the file

### Running the Python MA Analysis script:
1. In the settings cell, set "export_to_csv" and "plot_output" to "True" if you would like .csv's and .png's of the analyzed data, respectively. Select the type of plots you want to output by toggling the plot booleans (plot_accel_x, plot_accel_y, etc). Set "scrolling" to "True" if you would like to zoom in on the data (recommended for verifying proper IMU placement). Adjust "scroll_window" to modify zoom. 

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

2. Click the fast-forward button at the top of the file to restart the kernel and run the notebook. 
3. You will be prompted to select the folder containing the .csv files you want to analyze. When selecting the folder, make sure the .csv files contain at least 1 minute of data each. Once selected, the code will execute for up to several minutes.
4. After running the code, several files will appear in the folder of the original .csv files you selected for analysis. Data is separated into chunks, demarcated by dropouts in device connectivity. Folders named "Chunk_1", "Chunk_2", etc will contain .csv's and images of chunked data. The folder named "Chunk_all" will contain .csv's and images of data from all chunks combined. The .csv ending in "_dropouts" indicated device connectivity rate. 
5. To verify the integrity of your data, it is recommended you zoom into the individual HR and RR peaks using the "scrolling" setting. Additionally, an SQI > 0.5 indicates rhythmic heart sound peaks. Low SQI is a sign of improper IMU placement.  
