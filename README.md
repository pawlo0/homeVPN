# Summary
Instructions on how to set a home VPN using Raspberry Pi Zero w.

## 1.Prepare Raspberry OS SD card
- Download the [Raspberry Pi Imager](https://www.raspberrypi.com/software/).
- Pick Raspberry OS Lite. Don't forget to set the SSH password in the Raspberry Imager before burning the SD Card. Now just creating an emapty "ssh" file won't work. Also set the connection wi-fi details.  
![Pick Raspberry OS Lite](images/1.png)
![Set SSH password](images/2.png)

## 2. Update the Raspberry OS
- Access the RPi by ssh, using linux terminal or windows powesheel, by typing `ssh pi@raspberrypi.local` (assuming you're using "pi" as username) and then input the password you've entered before in the Raspberry OS Imager settings.
- Update the Raspberry OS `sudo apt update && sudo apt upgrade`
- Finally `sudo reboot`

## 3. Set dynamic DNS
- For this tutorial I'll use freeDNS. Go to [FreeDNS](https://freedns.afraid.org/) and signup. After registration and checking your email address, got to "Add subdomain".
- Chose any subdomain name you like, pick a domain and change destination (which should have your current IP) to **0.0.0.0**. The reason to pick this IP is to see it change afterwards, if all goes well.

![set freeDNS subdomain](images/3.png)

## 4. Install and set ddclient
- go back to the RPi and type `sudo apt install ddclient`. It is going to ask for a lot of questions, can press enter without typing anything.
- edit the config file by typing `sudo nano /etc/ddclinet.conf`. Delete all and replace by the below:
```
daemon=5m
timeout=10
syslog=no
pid=/var/run/ddclient.pid
ssl=yes

use=web, web=dynamicdns.park-your-domain.com/getip, web-skip='IP Address'
server=freedns.afraid.org
protocol=freedns
login='your freeDNS username'
password='your freeDNS password'
paulovpn.strangled.net
```
Notice I picked `use=web` instead of `use=if`. This is because the RPi Zero does not connect using Ethernet cable and I found this to be the way to find your current IP.

- There's another file we need to edit `sudo nano /etc/default/ddclient`. Make sure all is set to false and change the below to true. In my case it was there and I needed to add to the file:
```
run_daemon="true"
```

- The editing is done, now we need to restart ddclient:
```
sudo systemctl restart ddclient
```
and then type:
```
sudo systemctl status ddclient
```
Don't worry if it is showing an error. All will be fine if you go back to freeDNS page, refresh the subdomains page and now it should have changed from 0.0.0.0 to your current IP.

- Finally type the following to make sure ddclient is run everytime you reboot the RPi:
```
sudo systemctl enable ddclient
```



