# Server.sh

This section turns one of the Rasberry Pi into a server for the iperf3 command

1.Create script

```
touch server.sh
gedit server.sh
```

2. Edit the file

```
#!/bin/sh
iperf3 -s
```

3. Copy script to bin directory

```
sudo cp server.sh /usr/local/bin
```

4. Make the file executable by typing the following code into a terminal

```
sudo chmod +x /usr/local/bin/server.sh
```

5. Create unit file 

```
sudo gedit /etc/systemd/system/server.service
```

6. Edit unit file

```
[Unit]
Description= Raspberry Pi Server

Wants=network.target
After=syslog.target network-online.target

[Service]
Type=simple
ExecStart=/usr/local/bin/server.sh
Restart=on-failure
RestartSec=10
KillMode=process

[Install]
WantedBy=multi-user.target
```

7. Change permissions

```
sudo chmod 640 /etc/systemd/system/server.service
```

8. Reload file

```
sudo systemctl daemon-reload
```

9. Enable script at startup

```
sudo systemctl enable server
```

10. Reboot
