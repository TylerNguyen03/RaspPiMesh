# RaspPiMesh
The following website was used for reference: https://mjuenema.github.io/80211s_wireless_mesh/

1. Create a shell file. I named it boot in this scenario

```sudo nano ~/boot.sh```

2. edit the file to contain the following

```
#!/bin/sh
sudo iw dev wlan1 interface add mesh0 type mp mesh_id MYMESHID
sudo iw mesh0 set type mp
sudo iw dev mesh0 set channel 4
sudo ifconfig wlan1 down
sudo ifconfig mesh0 up
sudo ip addr add 192.168.1.3/24 dev mesh0
```
3. 
