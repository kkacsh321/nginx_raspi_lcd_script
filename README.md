## Raspberry Pi Nginx LCD Screen Script
This script runs on my Nginx Reverse Proxy Raspberry Pi 4 to check current status of Disk, IP, Nginx Status, etc and print out on to a 1602A LCD IC2 LCD Screen

## Requirements
Raspberry Pi
Python3
1602 LCD Display
Running Nginx

## Installing Script as a service

Open a sample unit file using the command as shown below:

sudo cp lcd.service /lib/systemd/system/

Configure systemd Run a Program On Your Raspberry Pi At Startup

This defines a new service called “Nginx LCD Script” and we are requesting that it is launched once the multi-user environment is available. The “ExecStart” parameter is used to specify the command we want to run. The “Type” is set to “idle” to ensure that the ExecStart command is run only when everything else has loaded. Note that the paths are absolute and define the complete location of Python as well as the location of our Python script.

In order to store the script’s text output in a log file you can change the ExecStart line to:

ExecStart=/usr/bin/python /home/pi/nginx_raspi_lcd_script/nginx_lcd.py > /home/pi/sample.log 2>&1

The permission on the unit file needs to be set to 644 :

sudo chmod 644 /lib/systemd/system/lcd.service
Step 2 – Configure systemd
Now the unit file has been defined we can tell systemd to start it during the boot sequence :

sudo systemctl daemon-reload
sudo systemctl enable lcd.service

Reboot the Pi and your custom service should run:

sudo reboot

sudo systemctl status lcd.service
sudo systemctl stop lcd.service
sudo systemctl start lcd.service
sudo systemctl restart lcd.service