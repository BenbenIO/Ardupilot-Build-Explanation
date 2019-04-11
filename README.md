# Flashing Pixhawk 

## A] Setup:
* Ubuntu 18.06
* QGroundControl software
* Build on ubuntu tuto from ardupilot website: using waf

## B] Flashing Process:
### 1/ Flash a default firmware:
* check the output from the consol to get which version they compile 
* You can also connect to Mission Planner (Windows) and see in the section "Messages" 
<p align="center">
  <img src="found_device.png">
</p>
<p align="center">
  <img src="firmware_version.png">
</p>
<p align="centxer">
  <img src="mission_planner.png">
</p>

### 2/ Build Ardupilot
#### 2.1/ Try to compile the code for the board
```sh
./waf configure --board ****
./waf copter
``` 

**Encountered Error:**

```diff
- Build failed
-Traceback (most recent call last):
-  File "/home/ben/Documents/Edge_drone/ardupilot_dev/ardupilot/modules/waf/waflib/Task.py", line 338, in process
-    ret = self.run()
-  File "Tools/ardupilotwaf/chibios.py", line 78, in run
-    if defaults.find():
-  File "/home/ben/Documents/Edge_drone/ardupilot_dev/ardupilot/Tools/scripts/apj_tool.py", line 93, in find
-    i = self.firmware[self.offset:].find(magic_str)
-TypeError: a bytes-like object is required, not 'str'**
```
**Solution**
> Switch to a python2 environnemt (conda)

#### 2.2/ Tested build
```sh
./waf configure --board fmuv3
./waf copter
```

```sh
./waf configure --board CubeBlack 
./waf copter
```
The firmware is generated in:
* build/--board/bin/arducopter.apj and arducopter.bin

#### 2.3/ Flash the board
Click to advance setting for custom firmware upload
Select the firmware arducopter.bin that you want to upload and wait...

#### 2.4/ Current result:
When configure with --board CubeBlack, the QGroundControl station cannot connect to the Pixhawk anymore but MissionPlanner can.
When configure with --board fmuv3 both QGroundControl and MissionPlanner connect correctly to the board.

### 3/ Following works:
#### 3.1/ Make the process more stable
- [ ] Need other people to try this methods and share experience on it

- [ ] Test the process inside a Virtual machine

- [ ] Create a docker container in order to make the environnemnt portable

#### 3.2/ Implement new function on ardupilot firmware :)


## Links:
[QGroundControl_install](https://docs.qgroundcontrol.com/en/getting_started/download_and_install.html)

[QGroundControl_explained](https://docs.qgroundcontrol.com/en/SetupView/Firmware.html)

[Ardupilot_building_explained](http://ardupilot.org/dev/docs/building-the-code.html)

[Ardupilot_building_setup](http://ardupilot.org/dev/docs/building-setup-linux.html)

[Ardupilot_build_waf](https://github.com/ArduPilot/ardupilot/blob/master/BUILD.md)

Link Error:
[Source_code](https://github.com/ArduPilot/ardupilot/blob/master/Tools/scripts/apj_tool.py)

Other:
[APJ_format](https://filext.com/file-extension/APJ)
