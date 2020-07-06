# startup-fix-the-usb
startup&amp;fix the usb

If you wanna to start your program automatically when turn on the electricity to the TX2, these following steps may help you.
<br>
### 1.startuo application<br>
First, you can search the "startup application" in your TX2.<br>
![image](https://github.com/zhucheng725/startup-fix-the-usb/blob/master/1.png)
<br>
Then you click the "Add" button and find the /usr/bin/gnome-terminal<br>
![image](https://github.com/zhucheng725/startup-fix-the-usb/blob/master/2.png)
<br>
After that , click the rectangle.<br>
![image](https://github.com/zhucheng725/startup-fix-the-usb/blob/master/3.png)

Then find the .bashrc and add your grogram such as :<br>
```
python3 /xx/xx.py
```

### 2.sfix the usb<br>

There are two ways to fix the usb.<br>
One way is using the udev
```
sudo vim /etc/udev/rules.d/90-video-device.rules

SUBSYSTEM=="video*",ATTRS{idVendor}=="046d",ATTRS{idProduct}=="0826",KERNELS=="1-2.1",MODE="0666",SYMLINK+="video10"

```

idVendor and idProduct can use the command to find it:
```
lsusb
```

kernals can use this command to find it:<br>
```
find /sys/ -name "video*"
dmesg --follow
```

And restart the system.<br>

If you use python cv2, you can change the address as following:<br>

```
cap = cv2.VideoCapture("/dev/video10")
```

Another way is use the realtek_hub_power_cycle<br>

Follow the nvidia dev website: https://devtalk.nvidia.com/default/topic/1058341/jetson-nano/usb-power-control/post/5375784/#5375784<br>

download the realtek_hub_power_cycle.zip and unzip it.

```
sudo apt-get install libusb-1.0-0-dev
gcc -o power_cycle realtek_hub_power_cycle.c -lusb-1.0
sudo ./power_cycle
```

Then you can find the video1 which have changed to video0.<br>
```
ls /dev/video* -l
```
