1. There has been a data breach in the XXY stockbroker office. There are 4 valid employees account registered in a machine (192.168.77.130) which is used in the stockbroker's office: 'Guest', 'ceh'. 'Administrator', 'John'. Find out who the hacker is? 
username : admin
pass : aadmin123

First use RDP to connect to the windows machine by entering the IP Address (192.168.77.130) and username (admin) then you'll be asked for password (aadmin123)

after successfully connect open up Command Prompt (CMD) enter 
```
ipconfig 
```
make sure the IP address is correct 

and then check all existing user by using 
```
net user
```

as you can see kevin here is the only account not in the list 
