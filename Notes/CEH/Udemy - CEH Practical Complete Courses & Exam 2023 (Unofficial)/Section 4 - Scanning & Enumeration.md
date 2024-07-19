find out a machine's IP Address
on linux :
```
ifconfig
```

![[Pasted image 20240716170929.png]]
on windows :
```
ipconfig
```

# Netdiscover 

Finding subnets using netdiscover this will search from 0-255 (256 in total)
```
sudo netdiscover -r 192.168.77.0/24
```

![[Pasted image 20240716171448.png]]

Example question : what are the machines that are running on this [IP] and this [Subnet]
you'll be given [IP] then you put `0/24` on the last digit example : `192.168.77.129` become `192.168.77.0/24`

after finding IP then you need to find which port are open and what services are running using nmap of a particular IP

# Nmap

https://www.geeksforgeeks.org/nmap-command-in-linux-with-examples/

```
nmap [nameserver/IP_address]
```

![[Pasted image 20240716173004.png]]

using this you can also find the IP Address of a nameserver

verbose command (more detailed network scan) :
```
nmap -v [namserver/IP_address]
```

-v: Increase verbosity level (use -vv or more for greater effect) more in depth scan :
```
nmap -vv [namserver/IP_address]
```
scan multiple host :
```
nmap [nameserver1/IP_address1] [nameserver2/IP_address2] [nameserver3/IP_address3]
```

to scan the whole subnet using nmap :
```
nmap 192.168.77.0/24
```

scan firewall :
```
sudo nmap -sA 192.168.77.129
```

identify hostname/domain from an IP address:
```
sudo nmap -sL 192.168.77.129
```

Continue video from Nmap-part-2