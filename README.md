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
   Note: you do not need to check the box to add anaconda to PATH environment variable.
2. Open the freshly installed annaconda navigator and launch Jupyter Notebook from the navigator menu.
3. Download and extract the nVital analysis .zip folder.
4. In Jupyter Notebook, navigate to the extracted analysis folder. Double click the .ipynb file inside to open it. Make sure the .py file is in the same directory as the .ipynb file.
5. Click the fast-forward button at the top of the file to restart the kernel and run the notebook. 
6. You will be prompted to select the folder containing the .csv files you want to analyze. You can also select a folder containing multiple folders you want to analyze. If you are on a Mac and do not see the folder selection window, you may need to click on a python file in your dock. When selecting the folder, make sure the .csv files contain at least 1 minute of data each. Once selected, the code will execute for up to several minutes.
7. After running the code, several files will appear in the folder of the original .csv files you selected for analysis. Data is separated into chunks, demarcated by dropouts in device connectivity. Folders named "chunk_0", "chunk_1", etc will contain chunked data. The folder named "chunk_all" will contain data from all chunks combined. The .csv ending in "_dropouts" indicates device connectivity rate. 

### Modifying CSV output/Plot output settings:
1. You can open the .py file in jupyter notebook to modify the plot settings.
2. You can select the type of plots you want to output by toggling the plot booleans (plot_accel_x, plot_accel_y, etc).
3. If using the respiratory envelope method for respiratory rate analysis, make sure to set the following to 'True' to see the lung sound: plot_hs_sh_filtered, plot_resp_sig_prefilt, use_hs_to_calculate_RR, overlay_resp_sig_prefilt_w_hs
4. In the .py file, you can change your parameters such as HR/RR window size (vital_w), HR/RR window overlap (vital_ovlp), expected respiratory range frequency (resp_freq), and respiratory peak detection parameters (resp_pk_dist, resp_pk_prom, etc.).
5. In the .py file, you can set the 'batch_process' parameter to 'True' to analyze multiple files at once. Ensure that you select the parent directory containing the various device directories when running the application.
6. After modifying your parameters, save the .py file and run .ipynb in Jupyter Notebook, following the instructions above.

### Navigating and saving time plots:
1. Once open in a browser tab, the time plots have a legend on the far right side. Click the button for horizontal and vertical zoom, then hover over the graph and scroll. Drag the plot to pan. 
2. To save the time plot, you will need to screenshot the graph, since the plot renderer does not support multi-plot PNG exports. 
3. If you closed the time plot and would like to view it again, simply run the cell labeled "Export time chunks for combined plots". You will be prompted to select the folder containing your data. 
4. If you get this error: "Only one usage of each socket address (protocol/network address/port) is normally permitted", first find the port your browser tried opening (it should be in the jupyter notebook printout). Then run the following command in Powershell (Windows) or Terminal (Mac): "netstat -ano | findstr :5005". Change the port number in the command accordingly. You will then see 1 or more 5-digit numbers next to the port number. Based on the 5-digit number, you will run this command: "taskkill /pid 27628 /F" (if the number is '27628'). Then, go back to your Jupyter notebook and try running your code again (by clicking the 'fast-forward' button). 

### Saving radar plots:
1. To save the radar plots, navigate to their location in the jupyter notebook (.ipynb file). You can click on a button next to the radar plot to save it. 
2. If you closed the radar plot and would like to view it again, simply run the cell labeled "Export radar plots for all data". You will be prompted to select the folder containing your data. 

-------------------------------------------------------------------------------------------------

### Recommended settings for viewing overall data:
plot_temperature = True\
plot_activity = True\
plot_HR = True\
plot_SQI = True\
use_shannon_peaks_only_to_calculate_resp_env = True\
plot_RR = True\
plot_SR = True\
