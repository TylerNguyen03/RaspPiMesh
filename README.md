# RaspPiMesh

The following steps are for creating a file that executes each time a raspberry pi boots up. The files allow the raspberry pi to be a node for the mesh network

1. Create a shell file. I named it boot in this scenario

```sudo nano ~/boot.sh```

2. Edit the file to contain the following. Note that the ip address's last digit can vary. For example, 192.168.1.1 and 192.168.1.2

```
#!/bin/sh
sudo iw dev wlan1 interface add mesh0 type mp mesh_id MYMESHID
sleep 1
sudo iw mesh0 set type mp
sleep 1
sudo iw dev mesh0 set channel 4
sleep 1
sudo ifconfig wlan1 down
sleep 1
sudo ifconfig mesh0 up
sleep 1
sudo ip addr add 192.168.1.3/24 dev mesh0 
```
3. Make the file executable by typing the following code into a terminal

```sudo chmod +x boot.sh```

4. Type the following code in the terminal 

```sudo nano /etc/rc.local```

5. Scroll all the way down and then insert the following code before the line "exit 0." Note that the code will change based on the boot script location

```/home/rasp2/boot.sh &```

6. Go to dhcpcd

```sudo nano /etc/dhcpcd.conf```

7. Disable wpa_supplicant

```
denyinterfaces wlan1
denyinterfaces mesh0
```

8. Reboot

9. Test to see if the other Raspberry Pi works

```ping 192.168.1.3```

10. Collect Data

```iw mesh0 station dump```
