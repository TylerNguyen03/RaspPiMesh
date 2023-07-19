# Testing
This section will go over a few commands to test speed and bitrate

Bitrate: On the Raspberry Pi that isn't the server, use the following command. In this scenario, the Pi with the assigned ip address 192.168.1.2 was the server. 

```
iperf3 -c 192.168.1.2
```

Speed: use the ping command to test the speed between nodes

```
ping 192.168.1.2
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
