# Installing Intel RealSense SDK 2.0
- Link: https://github.com/IntelRealSense/librealsense/blob/development/doc/distribution_linux.md

## Installation Steps
### Register the server's public key:
- `sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE || sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE`

### Add the server to the list of repositories:
- Command for ubuntu 20
	- `sudo add-apt-repository "deb https://librealsense.intel.com/Debian/apt-repo $(lsb_release -cs) main" -u`
- since this repo is not availabe in ubuntu 22 so we need to source it from ubuntu 20 repo, so replace `$(lsb_release -cs)` with `focal` i.e. name of ubuntu 20
	- `sudo add-apt-repository "deb https://librealsense.intel.com/Debian/apt-repo focal main" -u

### Install the libraries (see section below if upgrading packages)
- `sudo apt-get install librealsense2-dkms` 
- `sudo apt-get install librealsense2-utils`
	- The above two lines will deploy librealsense2 udev rules, **build and activate kernel modules**, runtime library and executable demos and tools.
-  `sudo apt-get install librealsense2-dev`  
- See below for details to properly install for ubuntu 22

#### Installing for packages for ubuntu 22
- `sudo apt-get install librealsense2-dkms` 
```
sudo apt-get install librealsense2-dkms
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  at librealsense2-udev-rules
Suggested packages:
  default-mta | mail-transport-agent
The following NEW packages will be installed:
  at librealsense2-dkms librealsense2-udev-rules
0 upgraded, 3 newly installed, 0 to remove and 4 not upgraded.
Need to get 4,324 kB of archives.
After this operation, 23.1 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://in.archive.ubuntu.com/ubuntu jammy/universe amd64 at amd64 3.2.5-1ubuntu1 [41.1 kB]
Get:2 https://librealsense.intel.com/Debian/apt-repo focal/main amd64 librealsense2-dkms all 1.3.18-0ubuntu1 [4,275 kB]
Get:3 https://librealsense.intel.com/Debian/apt-repo focal/main amd64 librealsense2-udev-rules amd64 2.50.0-0~realsense0.6128 [7,782 B]
Fetched 4,324 kB in 4s (1,011 kB/s)                  
Selecting previously unselected package at.
(Reading database ... 190028 files and directories currently installed.)
Preparing to unpack .../at_3.2.5-1ubuntu1_amd64.deb ...
Unpacking at (3.2.5-1ubuntu1) ...
Selecting previously unselected package librealsense2-dkms.
Preparing to unpack .../librealsense2-dkms_1.3.18-0ubuntu1_all.deb ...
Unpacking librealsense2-dkms (1.3.18-0ubuntu1) ...
Selecting previously unselected package librealsense2-udev-rules:amd64.
Preparing to unpack .../librealsense2-udev-rules_2.50.0-0~realsense0.6128_amd64.deb ...
Unpacking librealsense2-udev-rules:amd64 (2.50.0-0~realsense0.6128) ...
Setting up at (3.2.5-1ubuntu1) ...
Created symlink /etc/systemd/system/multi-user.target.wants/atd.service → /lib/systemd/system/atd.service.
Setting up librealsense2-udev-rules:amd64 (2.50.0-0~realsense0.6128) ...

Postinst script activated...
Presets deployment:
no src dir
tgt dir exists
Presets deployment is skipped
Setting up librealsense2-dkms (1.3.18-0ubuntu1) ...
Loading new librealsense2-dkms-1.3.18 DKMS files...
Building for 5.15.0-33-generic
Building initial module for 5.15.0-33-generic
Error! The /var/lib/dkms/librealsense2-dkms/1.3.18/5.15.0-33-generic/x86_64/dkms.conf for module librealsense2-dkms includes a BUILD_EXCLUSIVE directive which does not match this kernel/arch.
This indicates that it should not be built.
Skipped.

Loading the modified modules into kernel... complete
Current status:
bcmwl/6.30.223.271+bdcom, 5.15.0-30-generic, x86_64: installed
bcmwl/6.30.223.271+bdcom, 5.15.0-33-generic, x86_64: installed
librealsense2-dkms/1.3.18: added
mod: videodev 			
mod: uvcvideo 			 version: 1.1.1
mod: hid_sensor_gyro_3d 	
mod: hid_sensor_accel_3d 	
Processing triggers for man-db (2.10.2-1) ...
```
- Note **build and activate kernel modules** is not happening 

- `sudo apt-get install librealsense2-utils`
```
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Some packages could not be installed. This may mean that you have
requested an impossible situation or if you are using the unstable
distribution that some required packages have not yet been created
or been moved out of Incoming.
The following information may help to resolve the situation:

The following packages have unmet dependencies:
 librealsense2-utils : Depends: libssl1.1 (>= 1.1.1) but it is not installable
E: Unable to correct problems, you have held broken packages.
sudhir@sudhir-MacBookAir:~$ sudo apt-get install libssl1.1
```

- libssl1.1 is not available in 22.04 (libssl3 is used in 22.04) so we need to download and install it manually
```
cd ~/Downloads
wget http://archive.ubuntu.com/ubuntu/pool/main/o/openssl/libssl1.1_1.1.1f-1ubuntu2.13_amd64.deb
sudo dpkg -i ./libssl1.1_1.1.1l-1ubuntu1_amd64.deb
```

- Now install using `sudo apt-get install librealsense2-utils`

### Optionally install the debug package
- `sudo apt-get install librealsense2-dbg`

# Installing on Raspberry Pi with Ubuntu 20.04
- Links:
	- https://answers.ros.org/question/363889/intel-realsens-on-ubuntu-2004-ros-noetic-installation-desription/
	- https://github.com/IntelRealSense/librealsense/blob/master/doc/installation.md
- Steps
	- Step 1: Install Dependencies
		- `sudo apt-get install git libssl-dev libusb-1.0-0-dev libudev-dev pkg-config libgtk-3-dev`
		- `sudo apt-get install guvcview git libssl-dev libusb-1.0-0-dev pkg-config libgtk-3-dev`
		- `sudo apt-get install libglfw3-dev libgl1-mesa-dev libglu1-mesa-dev`
	- Step 2: Download librealsense
		-  `git clone https://github.com/IntelRealSense/librealsense.git`
	- Step 3: Run below scripts
		- `cd librealsense`
		- `./scripts/setup_udev_rules.sh`
		- `./scripts/patch-realsense-ubuntu-lts.sh`
	- Step 3: Build
		- `mkdir build && cd build`
		- `cmake ../ -DFORCE_RSUSB_BACKEND=true -DBUILD_PYTHON_BINDINGS=true -DCMAKE_BUILD_TYPE=release -DBUILD_EXAMPLES=true -DBUILD_GRAPHICAL_EXAMPLES=true`
		- `sudo make uninstall && make clean`
		- `make -j4`
			- Note: This step will take much time (~1hr)
		- `sudo make instal`
	- Step 5: Reboot

# Installing ROS wrapper for librealsense
- Link
	- https://github.com/IntelRealSense/realsense-ros
- Install it from sources and not directly via apt to get latest package
- Steps:
	- Step 1: Create Workspace
		- `mkdir -p ~/realsense_ws/src`
		- `cd ~/realsense_ws/src/`
		- `catkin_init_workspace`
	- Step 2: Download Package
		- `git clone https://github.com/IntelRealSense/realsense-ros.git`
		- `cd realsense-ros/`
		- `git checkout git tag | sort -V | grep -P "^2.\d+\.\d+" | tail -1`
		- `cd ..`
	- Step 3: Build and Install
		- `cd ..`
			- To reach root of workspace
		- `catkin_make clean`
		- `catkin_make -DCATKIN_ENABLE_TESTING=False -DCMAKE_BUILD_TYPE=Release`
		- `catkin_make install`
	- Step 4: Source the workspace
		- `echo "source ~/realsense_ws/devel/setup.bash" >> ~/.bashrc`
		- `source ~/.bashrc`


# D455 Camera
- ![[Pasted image 20220705103137.png]]
	- X: 124.5 mm
	- Y: 29.5 mm
	- Z: 26.5 mm
	- 0.125, 0.03, 0.03
	- weight: 0.1kg
	- moment of interia
		- ixx = 1/12 x m(y^2 + z^2) = 1/12 x 0.1 (0.03^2 + 0.03^2) = 0.000015
		- iyy = 1/12 x m(x^2 + z^2) = 1/12 x 0.1 (0.125^2 + 0.03^2) = 0.000138
		- izz = 1/12 x m(x^2 + y^2) = 1/12 x 0.1 (0.125^2 + 0.03^2) = 0.000138
	- p3dx
		- 0.5 0.4 0.25
		-  ixx = 1/12 x m(y^2 + z^2) = (9(0.4^2 + 0.25^2))/12 = 0.166875
		-  iyy = 1/12 x m(x^2 + z^2) = (9(0.5^2 + 0.25^2))/12 = 0.234375
		- izz = 1/12 x m(x^2 + y^2) = (9(0.5^2 + 0.4^2))/12 = 0.3075
	- sensor box
		- 0.1 0.16 0.22
		-  ixx = 1/12 x m(y^2 + z^2) = (0.05(0.16^2 + 0.22^2))/12 = 0.0003
		-  iyy = 1/12 x m(x^2 + z^2) = (0.05(0.1^2 + 0.22^2))/12 = 0.00024
		- izz = 1/12 x m(x^2 + y^2) = (0.05(0.1^2 + 0.16^2))/12 = 0.00015
- ![[Pasted image 20220705103753.png]]
- ![[Pasted image 20220705103208.png]]


# Problems
- FPS: don't stream data at 10FPS or low reliably
- Unreliable depth
	- ![[Pasted image 20220715145257.png]]
	- ![[Pasted image 20220715152657.png]]
- solutions
	- https://www.intel.com/content/dam/support/us/en/documents/emerging-technologies/intel-realsense-technology/BKMs_Tuning_RealSense_D4xx_Cam.pdf


![[Pasted image 20220715154719.png]]![[Pasted image 20220715154745.png]]


# Other cameras
- https://www.baslerweb.com/en/products/cameras/3d-cameras/
- https://en.ids-imaging.com/ensenso-stereo-3d-camera.html
- https://www.luxonis.com/
- https://www.mdpi.com/2218-6581/9/3/56/htm
- https://discourse.ros.org/t/intel-cancelling-its-realsense-business-alternatives/21881/6
- https://structure.io/structure-core
- Others
	- Orbecc
	- pmd/IFM (albeit, no color)
	- Mynt
	- ZED (if you have a GPU and GPU power to spare)ow
- Things to look
	- Camera Quality
	- SDK
	- Computation
		- How much is onborad
		- How much is off-loaded
	- Power consumption and Heat
	- Compute required


- https://mdpi-res.com/d_attachment/robotics/robotics-09-00056/article_deploy/robotics-09-00056.pdf?version=1595331590
