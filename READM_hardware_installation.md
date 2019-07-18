# Install PointGrey camera on Linux computer

Tested hardware:

`1. Grasshopper3 GS3-U3-23S6M`

## 1. Install usb3.0 driver (APS-IT)

Use `lspci | grep USB` to see if system can see the USB controller

`02:00.0 USB controller: Fresco Logic FL1100 USB 3.0 Host Controller (rev 10)`

Plugin camera to one of the usb 3.0 port, use `dmesg` command to see if system can detect camera
```
usb 4-1: new SuperSpeed USB device number 3 using xhci_hcd  
usb 4-1: New USB device found, idVendor=1e10, idProduct=3300   
usb 4-1: New USB device strings: Mfr=1, Product=2, SerialNumber=3  
usb 4-1: Product: Grasshopper3 GS3-U3-23S6M  
usb 4-1: Manufacturer: Point Grey Research  
usb 4-1: SerialNumber: 0117xxxx  
```

## 2. Install Pointgrey driver (APS-IT)

* make sure account belongs to group "pgrimaging"
* `/etc/udev/rules.d/40-pgr.rules` should looks like below. (Note that KERNEL mode should be **"0666"**)
```
ATTRS{idVendor}=="1e10", ATTRS{idProduct}=="2000", MODE="0664", GROUP="pgrimaging"  
ATTRS{idVendor}=="1e10", ATTRS{idProduct}=="2001", MODE="0664", GROUP="pgrimaging"  
ATTRS{idVendor}=="1e10", ATTRS{idProduct}=="2002", MODE="0664", GROUP="pgrimaging"  
ATTRS{idVendor}=="1e10", ATTRS{idProduct}=="2003", MODE="0664", GROUP="pgrimaging"  
ATTRS{idVendor}=="1e10", ATTRS{idProduct}=="2004", MODE="0664", GROUP="pgrimaging"  
ATTRS{idVendor}=="1e10", ATTRS{idProduct}=="2005", MODE="0664", GROUP="pgrimaging"  
ATTRS{idVendor}=="1e10", ATTRS{idProduct}=="3000", MODE="0664", GROUP="pgrimaging"  
ATTRS{idVendor}=="1e10", ATTRS{idProduct}=="3001", MODE="0664", GROUP="pgrimaging"  
ATTRS{idVendor}=="1e10", ATTRS{idProduct}=="3004", MODE="0664", GROUP="pgrimaging"  
ATTRS{idVendor}=="1e10", ATTRS{idProduct}=="3005", MODE="0664", GROUP="pgrimaging"  
ATTRS{idVendor}=="1e10", ATTRS{idProduct}=="3006", MODE="0664", GROUP="pgrimaging"  
ATTRS{idVendor}=="1e10", ATTRS{idProduct}=="3007", MODE="0664", GROUP="pgrimaging"  
ATTRS{idVendor}=="1e10", ATTRS{idProduct}=="3008", MODE="0664", GROUP="pgrimaging"  
ATTRS{idVendor}=="1e10", ATTRS{idProduct}=="300A", MODE="0664", GROUP="pgrimaging"  
ATTRS{idVendor}=="1e10", ATTRS{idProduct}=="300B", MODE="0664", GROUP="pgrimaging"  
ATTRS{idVendor}=="1e10", ATTRS{idProduct}=="3100", MODE="0664", GROUP="pgrimaging"  
ATTRS{idVendor}=="1e10", ATTRS{idProduct}=="3101", MODE="0664", GROUP="pgrimaging"  
ATTRS{idVendor}=="1e10", ATTRS{idProduct}=="3102", MODE="0664", GROUP="pgrimaging"  
ATTRS{idVendor}=="1e10", ATTRS{idProduct}=="3103", MODE="0664", GROUP="pgrimaging"  
ATTRS{idVendor}=="1e10", ATTRS{idProduct}=="3104", MODE="0664", GROUP="pgrimaging"  
ATTRS{idVendor}=="1e10", ATTRS{idProduct}=="3105", MODE="0664", GROUP="pgrimaging"  
ATTRS{idVendor}=="1e10", ATTRS{idProduct}=="3106", MODE="0664", GROUP="pgrimaging"  
ATTRS{idVendor}=="1e10", ATTRS{idProduct}=="3107", MODE="0664", GROUP="pgrimaging"  
ATTRS{idVendor}=="1e10", ATTRS{idProduct}=="3108", MODE="0664", GROUP="pgrimaging"  
ATTRS{idVendor}=="1e10", ATTRS{idProduct}=="3109", MODE="0664", GROUP="pgrimaging"  
ATTRS{idVendor}=="1e10", ATTRS{idProduct}=="3300", MODE="0664", GROUP="pgrimaging"  
KERNEL=="raw1394", MODE="0666", GROUP="pgrimaging"  
KERNEL=="video1394*", MODE="0666", GROUP="pgrimaging"  
SUBSYSTEM=="firewire", GROUP="pgrimaging"  
SUBSYSTEM=="usb", GROUP="pgrimaging"  
```
* Use pre-compiled program to see if camera can take and save images
```
[bakfark ~/tmp/tmp1] FlyCapture2Test
FlyCapture2 library version: 2.9.3.43
Application build date: Apr  5 2016 15:31:54

Number of cameras detected: 1

*** CAMERA INFORMATION ***
Serial number -18301012
Camera model - Grasshopper3 GS3-U3-23S6M
Camera vendor - Point Grey Research
Sensor - Sony IMX174 (1/1.2" Mono CMOS)
Resolution - 1920x1200
Firmware version - 2.30.3.0
Firmware build time - Wed Mar 29 00:05:26 2017

Grabbed image 0
Grabbed image 1
Grabbed image 2
Grabbed image 3
Grabbed image 4
Grabbed image 5
Grabbed image 6
Grabbed image 7
Grabbed image 8
Grabbed image 9
Done! Press Enter to exit...
```
If you see 10 images are saved successfully in the current folder, you are in good shape.

## 3. Install Pointgrey IOC
