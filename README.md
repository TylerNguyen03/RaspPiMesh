# RaspPiMesh

1. Install gedit and iperf

```
sudo apt-get install gedit
sudo apt install -y iperf3
```

2. Create script

```
touch boot.sh
gedit boot.sh
```

3. Edit the file to contain the following. Note that the ip address's last digit can vary. For example, 192.168.1.1 and 192.168.1.2

```
#!/bin/sh
sudo iw dev wlan1 interface add mesh0 type mp mesh_id MYMESHID
sudo iw mesh0 set type mp
sudo iw dev mesh0 set channel 4
sudo ifconfig wlan1 down
sudo ifconfig mesh0 up
sudo ip addr add 192.168.1.3/24 dev mesh0 
```

4. Copy script to bin directory

```sudo cp boot.sh /usr/local/bin```

5. Make the file executable by typing the following code into a terminal

```sudo chmod +x /usr/local/bin/boot.sh```

6. Create unit file 

```sudo gedit /etc/systemd/system/boot.service```

7. Edit unit file

```
[Unit]
Description=Raspberry Pi Mesh

Wants=network.target
After=syslog.target network-online.target

[Service]
Type=simple
ExecStart=/usr/local/bin/boot.sh
Restart=on-failure
RestartSec=10
KillMode=process

[Install]
WantedBy=multi-user.target
```

8. Change permissions

```sudo chmod 640 /etc/systemd/system/boot.service```

9. Reload file

```sudo systemctl daemon-reload```

10. Enable script at startup

```sudo systemctl enable boot```

11. Go to dhcpcd

```sudo nano /etc/dhcpcd.conf```

12. Disable wpa_supplicant by inserting commands

```
denyinterfaces wlan1
denyinterfaces mesh0
```

13. Reboot

14. Collect data speed by inserting ip of address of other nodes. This command collects data and then puts it in a file named "test"

```
ping 192.168.1.3 > test
```

15. Collect birate by first making one of the raspberry pi a server and then connecting to that server using its ip in another raspberry pi 

```
iperf3 -s
```

```
iperf3 -c 10.106.94.250 > test1.1
```
