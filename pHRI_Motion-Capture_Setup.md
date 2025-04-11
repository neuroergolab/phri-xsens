## pHRI Motion Capture Documentation
### [NeuroErgonomics Lab](https://neuroergolab.org/)
- PI: Dr. Ranjana Mehta
- Mentor: Aakash Yadav
- Author: Shreyanshu Dekate

---

### Table of Contents:

1. [Download XSens Software](#1-download-xsens-software)
2. [Familiarity w/ XSens + Setup](#2-familiarity-w-xsens--setup)
3. [HTC Vive Integration (using SteamVR) w/ XSens MVN](#3-htc-vive-integration-using-steamvr-w-xsens-mvn)
4. [Position Aiding](#4-position-aiding)
5. [Object Tracking](#5-object-tracking)
6. [Starting a Data Recording with Position Aiding + Object Tracking](#6-starting-a-data-recording-with-position-aiding--object-tracking)
7. [(Pre-)Processing and Exporting Data](#7-pre-processing-and-exporting-data)
8. [Analyzing Data (in-progress)](#8-analyzing-data-tbd)


---

### 1. Download XSens Software
--- 
- Download [MVN Analyze](https://www.movella.com/support/software-documentation#:~:text=Tools-,MVN%20Analyze,-Latest%20stable%20software)
- Pay attention to Sections 3 and 4 of the [user manual](https://www.movella.com/hubfs/MVN_User_Manual.pdf?__hstc=233546881.1fa5198786ade7bb8cace6bc2dd887f0.1663745187069.1670919674447.1670940876901.93&__hssc=233546881.19.1670940876901&__hsfp=700330257)
- Ensure you plug in the dongle for license activation and to get full access to MVN features. **This is necessary for pHRI data collection.**

### 2. Familiarity w/ XSens + Setup
--- 
- **XSens Procedure**:
    - [Body Measurements](https://www.movella.com/tutorials?video=body-measurements)
    - [Placing Straps](https://www.movella.com/tutorials?video=placing-straps)
    - [Preparing/Placing Hardware (Sensors)](https://www.movella.com/tutorials?video=preparing-hardware-mvn-awinda)
    - [Setting up a Recording Session](https://www.movella.com/tutorials?video=set-up-a-recording-session)
        - Settings we use:
            - Full body sensors
            - 60 Hz
            - Use Generic Prop
            - Prop sensor mapped to the R Hand sensor
    - [Calibration](https://www.movella.com/tutorials?video=calibrating-awinda)
        - We prefer to use N-Pose but if it's too troublesome or quality of calibration is non-ideal, use T-Pose calibration.
    - [Setting up Prop Sensors (Video)](https://www.movella.com/tutorials?video=setting-up-props-for-awinda)
    - [Setting up Prop Sensors (Guide)](https://base.movella.com/s/article/Adding-a-Prop-Sensor)
        - Important Limitation: XSens prop sensors do NOT track 3D position, only 3D rotation
        - More info: croll to the section right above "Accepting a Prop Sensor on a New System" in the Prop Sensor Guide linked right above.
        - pHRI project goal: we want to track 3D position AND 3D rotation for the Human and Object.
> We will still physically attach the prop sensor to the object. We will map it to the XSens R Hand sensor as a "Generic Object" during set up.

### 3. HTC Vive Integration (using SteamVR) w/ XSens MVN
--- 
- For conciseness, this long title will be referred to as `SteamVR Sensors`
- Useful for tracking rotation AND position in 3D space, integrates with XSens (requires successfully [downloading MVN Analyze](#1-download-xsens-software))

#### Remember to plug in the dongle!

- We heavily rely on SteamVR Sensors in the pHRI project. They are used to track the Human and Object in 3D space (position and rotation).

> Please be sure to get SteamVR Sensors set up correctly - ask for help if needed! 

#### Follow instructions in the entire [Setup Guide](https://base.movella.com/s/article/HTC-Vive-Setup-Guide?language=en_US):

- WATCH: [Tutorial Video](https://www.movella.com/tutorials?video=htc-vive-integration) (Section 1)

- Install Software (Section 2):
    - Steam
    - SteamVR
    
- Set up Steam Hardware (Section 3):
    - Devices needed for set up: 
        - Base Stations, VR Headset, Tracker(s), Tracker Dongle(s), Controllers, etc.
    - Ensure you do the following: 
        - Base Station layout and setup
        - Pair devices
        - Perform Room Setup/Calibration
    - **We only use the headset during this setup and Room setup/calibration.** During the pHRI experiments, we will only need the base stations and trackers. We can and will be collecting data without the headset.

- Set up MVN (Section 4):
    - The instructions here are a bit outdated - you won't see "SteamVR" under "Options" in the MVN menu bar. 
    - Rather, ensure the [dongle is plugged in](#remember-to-plug-in-the-dongle) and click on "Start New Motion Capture". 
    - SteamVR should be detected automatically if installed and setup correctly. More information in [position aiding](#4-position-aiding) and [object tracking](#5-object-tracking) below.
    - pHRI does not use the headset or controllers! Accordingly, we need to chnage some settings. To enable data collection in MVN without the headset, be sure to follow the instructions and implement the suggested settings in "4.1 Setup SteamVR in MVN, subpoint 4."

#### Note: Combining Position Aiding + Object Tracking

- Object Tracking itself is enough to track the Object in 3D space (position + rotation), but not in conjunction with the XSens sensors' movements. 
This is due to the XSens sensors and SteamVR sensors having and using different coordinate systems, resulting in mismatched inputs and misaligned movements. 
    - During initial testing, there were cases where the XSens sensors detected the Human moving the Object to the left, but the SteamVR sensors detected the Object as moving to the right. 
- Therefore, it is important to ensure that both Position Aiding and Object Tracking are functional and set up correctly! This is becuase Position Aiding forces XSens to use the SteamVR coordinate system, meaning all movements become aligned among both systems with no mismatched inputs.
    - This is out current experimental setup! MVN supports this functionality. 

### 4. Position Aiding
--- 
- Read/follow this [Setup Guide + Other Important Information](https://base.movella.com/s/article/Position-Aiding-HTC-Vive?language=en_US)
- In terms of the pHRI expriment set up, the "Human" SteamVR Tracker **(LHH-some code)** attaches to the Human's pelvis, **right above the XSens Pelvis tracker**.

### 5. Object Tracking
--- 
- Read/follow this [Setup Guide + Other Important Information](https://base.movella.com/s/article/Object-Tracking-HTC-Vive-1605786850124?language=en_US) - pay close attention to "6. Position Aiding"
- In terms of the pHRI expriment set up, the "Object" SteamVR Tracker **(LHH-some code)** attaches to the Object. Have the prop sensor attached near the "Object" SteamVR Tracker, too!

### 6. Starting a Data Recording with Position Aiding + Object Tracking
--- 
#### Make sure the dongle is plugged in!
- Follow the [XSens Procedue](#2-familiarity-w-xsens--setup).
- Follow special setup instructions for [Position Aiding](#4-position-aiding) + [Object Tracking](#5-object-tracking).

- When calibrating the XSens sensors, **stay within the sight of the Base Stations** when folloing calibration cues and instructions.
- After calibration, ensure you place the Object on the floor and click, in the MVN Menu bar, "Tasks > Reset Floor".

- If the SteamVR Pelvis sensor and the XSens Pelvis seem to be slightly misaligned/have a weird distance between, click on "Reset Character Origin" and/or "Reset Axes" (or something similar) and follow any prompts that pop up.
    - Ex. SteamVR sensore requires subject to walk around to get calibration data or something similar.
- **Before** recording any data, ensure you can verify the XSens Human model is as it should be and that two (2) SteamVR Trackers in shown MVN. Ensure the Object Tracker is in the air, if placed on the table, and that the Pelvis Tracker is close to the position of the Pelvis XSens sensor.
> **Only proceed with a data recording if the aforementioned is ALL accounted for!**
- Record data and save it in an easily identifiable location!

### 7. (Pre-)Processing and Exporting Data
--- 
> **Make sure the dongle is plugged in!**
- Open the Motion Capture Session file(s).
- HD Preprocess the data - make sure both the XSens Sensors and SteamVR Sensors have been selected.
- Ensure "Single Level" has been selected.
- Ensure you click on "Use External Sensor" and make sure the computer does NOT go to sleep while processing the data.
- All this information is under [Position Aiding](#4-position-aiding) and [Object Tracking](#5-object-tracking) setup guides/tutorials!
- Once done processing the data, click on export (File > Export). Export at least:
    - `.xlsx` (Excel file - this option only exports XSens data, keep default options)
    - `.fbx` (FBX file - this option can export both XSens and SteamVR data, keep default options)
    - `.mov` (Movie file - this option exports a clip of the data recording session)
        - Ensure that the resolution is 1920x1080p, 60 fps, and while it'll take a long time to export, a `.mov` is great for visually verifying/analyzing Motion Capture sessions!
> **DO NOT let the computer sleep at any point** - processing data and exporting data (as a .mov, anyway) takes a LONG time, and interrupted/aborted progress means you have to restart.
- **At the very least, preprocess the data!** Preprocessing a session itself can take 20 minutes for a 2-4 minute Motion Capture session - now scale that up to an hour-long session...
-  Exporting data can still be done later, but please preprocess the data - this will take the longest amount of time. Moreover, these files WILL be big - 2 minute motion capture sessions at 60hz result in 300MB+ Excel files. Same for Movie files... so that means there's tons of data to process and parse through (yay...)

### 8. Analyzing Data (TBD)
--- 
- In-progress!
