# Summary
Instructions on how to set a home VPN using Raspberry Pi Zero w.

## 1.Prepare Raspberry OS SD card
- Download the [Raspberry Pi Imager](https://www.raspberrypi.com/software/).
- Pick Raspberry OS Lite. Don't forget to set the SSH password in the Raspberry Imager before burning the SD Card. Now just creating an emapty "ssh" file won't work. Also set the connection wi-fi details.  
![Pick Raspberry OS Lite](images/1.png)
![Set SSH password](images/2.png)

## 2. Update the Raspberry OS
- Access the RPi by SSH using `ssh pi@raspberrypi.local` (assuming you're using "pi" as username) and then input the password you've entered before in the Raspberry OS Imager settings.
- Update the Raspberry OS `sudo apt update && sudo apt upgrade`
- Finally `sudo reboot`


