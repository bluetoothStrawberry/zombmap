# zombmap Idle Scan Poc? 

- The goal here is just to play with idle scan, and understand it at a deeper level.
-  I prefer using nmap anyway `nmap -n -Pn -sI zombie_boy target`

- Here we have our target   192.168.48.132
```
root@debianserver2:~# ip addr sh

2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether [REDACTED] brd ff:ff:ff:ff:ff:ff
    altname enp2s1
    inet 192.168.48.132/24 brd 192.168.48.255 scope global dynamic ens33
       valid_lft 1173sec preferred_lft 1173sec
    inet6 [REDACTED]scope link 
       valid_lft forever preferred_lft forever
root@debianserver2:~# 

```
- And the services running on port 22, 80 and 3306
```
root@debianserver2:~# ss -nlt 
State              Recv-Q              Send-Q                           Local Address:Port                           Peer Address:Port             Process             
LISTEN             0                   80                                   127.0.0.1:3306                                0.0.0.0:*                                    
LISTEN             0                   128                                    0.0.0.0:22                                  0.0.0.0:*                                    
LISTEN             0                   128                                       [::]:22                                     [::]:*                                    
LISTEN             0                   511                                          *:80                                        *:*                              

```
- Le's assume we wanna be sneaky for any number of reasons.
- And we found a network printer who nobody uses

  ```
  The printer is at the ip : 192.168.48.2 
  what we gonna do is write a short script
  that will take advatange of furture of ipv4 header.
  Every time our zombie boy sends a RST it inscreases it's ip Id by one on port 80
  here's the doc cus I'm lazy 
  ```
  [Idle scan Stuff](https://fr.wikipedia.org/wiki/Idle_scan)

- Running
  ```
  # From attacker, using printer as zombie,, scanning --> webserver
  # it will take long. I was a  bit scary or running this slowly(I'm using python)
  # So I tried to make even slower by adding sleep(wait_time) 
    root@debian:~# ./main.py 

    returns: 22, 80, 3306
  ```
