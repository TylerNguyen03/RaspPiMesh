# Testing
This section will go over a few commands to test speed and bitrate

Bitrate: on the Raspberry Pi that isn't the server, use the following command. In this scenario, the Pi with the assigned ip address 192.168.1.2 was the server. 

```
iperf3 -c 192.168.1.2
```

Speed: use the ping command to test the speed between nodes

```
ping 192.168.1.2
```

Mpath: this command shows the path the mesh takes when communicating with one another

```
sudo iw dev mesh0 mpath dump
```

Station: use this command to see the signal as well as bitrate

```
sudo iw dev mesh0 station dump
```

Notes: 

- you can add ">" at the end of each of these commands to insert data into a file. In this example, the data from the ping command will go into a new file called "test".

```
ping 192.168.1.2 > test
```

- you can specify how much packets the ping commands run for using the -c followed by a number. In this example, the ping command will run for 20 packets

```
ping 192.168.1.3 -c 20
```

- you can increase the rate at which the ping collects data using the -i follwed by a number. The fastest rate of data collection for the ping command is 200 ms. This command can also be applied to the iperf3 command, except that command doesn't have the same limiation as the ping command. In this example, the ping command collect data every 0.2 seconds.

```
ping 192.168.1.3 -i .2
```

- if you want the ping command to only display time, use the following command. It's important to note that the last line of data should be disregarded

```
ping 192.168.1.2 | grep -Po '[0-9.]*(?= ms)'
```

- you can specify how long the iperf3 command runs for using the -t followed by a time. In this example, the iperf command will run for 20 seconds

```
iperf3 -c 192.168.1.2 -t 20
```

- you can use the following command to display only bitrate. It's important to note that the last 2 lines of data should be disregarded

```
iperf3 -c 192.168.1.2 | grep -Po '[0-9.]*(?= Mbits/sec)'
```

- you can add in -f [format] onto the iperf command to change units. For consistency reasons, I added in "m" so that the command will always print in mbits/sec

```
iperf3 -c 192.168.1.4 -f m
```

# Testing Part 2
This section goes over an executable file that can be used to collect data efficiently. Note that this script will need to be edited for each experiment

1. Create the script. I named it "datacollect" in this case

```
touch datacollect.sh
gedit datacollect.sh
```

2. Edit the file to contain the following. Note that the file destination can be changed. For example, ex1test1ping can be edited to ex1test2ping after a trial

```
#!/bin/sh
ping 192.168.1.4 -c 90 | grep -Po '[0-9.]*(?= ms)' > ex1test1ping
iperf3 -c 192.168.1.4 -t 90 -f m | grep -Po '[0-9.]*(?= Mbits/sec)' > ex1test1iperf
sudo iw dev mesh0 station dump > ex1test1stat
sudo iw dev mesh0 mpath dump > ex1test1mpath
```

3. Make the file executable

```
sudo chmod +x datacollect.sh
```

4. Execute the file via the following

```
sh datacollect.sh
```

