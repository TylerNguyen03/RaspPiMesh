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

- you can specify how long the ping commands run for using the -c followed by a time. In this example, the ping command will run for 20 seconds

```
ping 192.168.1.3 -c 20
```

- you can specify how long the iperf3 command runs for using the -t followed by a time. In this example, the iperf command will run for 20 seconds

```
iperf3 -c 192.168.1.2 -t 20
```
