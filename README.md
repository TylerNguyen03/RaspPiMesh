# RaspPiMesh

This section should be applied to all of the Raspberry Pi

1. Update the Raspberry Pi

```
sudo apt-get update && sudo apt-get upgrade -y
```

2. Install gedit and iperf

```
sudo apt-get install gedit
sudo apt install -y iperf3
```

3. Create script

```
touch boot.sh
gedit boot.sh
```

4. Edit the file to contain the following. Note that the ip address's last digit can vary. For example, 192.168.1.1 and 192.168.1.2

```
#!/bin/sh
sudo iw dev wlan1 interface add mesh0 type mp mesh_id MYMESHID
sudo iw mesh0 set type mp
sudo iw dev mesh0 set channel 4
sudo ifconfig wlan1 down
sudo ifconfig mesh0 up
sudo ip addr add 192.168.1.3/24 dev mesh0 
```

5. Copy script to bin directory

```
sudo cp boot.sh /usr/local/bin
```

6. Make the file executable by typing the following code into a terminal

```
sudo chmod +x /usr/local/bin/boot.sh
```

7. Create unit file 

```
sudo gedit /etc/systemd/system/boot.service
```

8. Edit unit file

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

9. Change permissions

```
sudo chmod 640 /etc/systemd/system/boot.service
```

10. Reload file

```
sudo systemctl daemon-reload
```

11. Enable script at startup

```
sudo systemctl enable boot
```

12. Go to dhcpcd

```
sudo nano /etc/dhcpcd.conf
```

13. Disable wpa_supplicant by inserting commands

```
denyinterfaces wlan1
denyinterfaces mesh0
```

14. Reboot

The next step will go into turning one of the Raspberry Pi into a [server](raspberrypi_server.md) which will then go into [testing](testing.md).
