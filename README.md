# GPS/Data Application

This repository contains everything needed to decode DMR GPS packets and SMS for HBLink3. This application can act as a master or peer and receive data as a group call or private call.

Files modified from original master branch of HBLink3:

* bridge.py
* config.py 

The pynmea2 module is required.

This should work for DMR radios that send location data as a UTF-8 NMEA sentence. I am hopping to add support for more radios in the future.

### Differences in branches

* **GPS**: Contains the GPS/Data Application.
* **aprs_features**: Contains the GPS/Data Application and a modified version of the APRS implementation for repeaters and hotspots by **IU7IGU**. (See [https://github.com/iu7igu/hblink3-aprs](https://github.com/iu7igu/hblink3-aprs) for his work). I combined these for convenience.

## Confirmed working:
Actually tested

* Anytone D878

## Most likely to work:
Not tested yet

* Anytone D868
* Anytone D578
* BTech DMR-6x2


## How it works

A user should configure their radio for the DMR ID of the application and private or group call. When a position is received by the application, it will extract the coordinates and create an APRS position packet. The application will find the callsign of the user based on the sending radio's DMR ID. It is essential to have an up to date subscriber_ids file for this to work. A predefined APRS SSID is appended to the callsign. The APRS location packet is then uploaded to APRS-IS. No setup is required beforehand on the part of the user. This is pretty much "plug and play."

For example, N0CALL has a DMR ID of 1234567. N0CALL's radio sends a position to the application. The application will query the subscriber_ids file for DMR ID 1234567. The result will be N0CALL. An APRS location pack is created and uploaded to APRS-IS.

## Configuration

See hblink_SAMPLE.cfg, rules_SAMPLE.py, and gps_data_SAMPLE.cfg for examples.



---
### FOR SUPPORT, DISCUSSION, GETTING INVOLVED ###

Please join the DVSwitch group at groups.io for online forum support, discussion, and to become part of the development team.

DVSwitch@groups.io 

A voluntary registrty for HBlink systems with public access has been created at http://hblink-register.com.es Please consider listing your system if you allow open access.

---

## PROJECT: Open Source HomeBrew Repeater Proctol Client/Master. ##

**UPDATES:**

**PURPOSE:** Thanks to the work of Jonathan Naylor, G4KLX; Hans Barthen, DL5DI; Torsten Shultze, DG1HT we have an open protocol for internetworking DMR repeaters. Unfortunately, there's no generic client and/or master stacks. This project is to build an open-source, python-based implementation. You are free to use this software however you want, however we ask that you provide attribution in some public venue (such as project, club, organization web site). This helps us see where the software is in use and track how it is used.

For those who will ask: This is a piece of software that implements an open-source, amateur radio networking protocol. It is not a network. It is not intended to be a network. It is not intended to replace or circumvent a network. People do those things, code doesn't.
  
**PROPERTY:**  
This work represents the author's interpretation of the HomeBrew Repeater Protocol, based on the 2015-07-26 documents from DMRplus, "IPSC Protocol Specs for homebrew DMR repeater" as written by Jonathan Naylor, G4KLX; Hans Barthen, DL5DI; Torsten Shultze, DG1HT, also licenced under Creative Commons BY-NC-SA license.

**WARRANTY**
None. The owners of this work make absolutely no warranty, express or implied. Use this software at your own risk.

**PRE-REQUISITE KNOWLEDGE:**  
This document assumes the reader is familiar with Linux/UNIX, the Python programming language and DMR.  

**Using docker version**

To work with provided docker setup you will need:
* A private repository with your configuration files (all .cfg files in repo will be copyed to the application root directory on start up)
* A service user able to read your private repository (or be brave and publish your configuration, or be really brave and give your username and password to the docker)
* A server with docker installed
* Follow this simple steps:

Build your own image from source

```bash

docker build . -t millaguie/hblink:3.0.0

```

Or user a prebuilt one in docker hub: millaguie/hblink:3.0.0

Wake up your container

```bash
touch /var/log/hblink.log
chown 65000  /var/log/hblink.log
 run -v /var/log/hblink.log:/var/log/hblink.log -e GIT_USER=$USER -e GIT_PASSWORD=$PASSWORD -e GIT_REPO=$URL_TO_REPO_WITHOUT_HTTPS://  -p 54000:54000  millaguie/hblink:3.0.0
 ```

**MORE DOCUMENTATION TO COME**

***0x49 DE N0MJS***

Copyright (C) 2016-2020 Cortney T. Buffington, N0MJS n0mjs@me.com

This program is free software; you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation; either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with this program; if not, write to the Free Software Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA
