# BaseStation Setup

## System Configuration
Assuming NOOBS SD card came with RPi 4
- Connect to network
- Install `Rapsbian/RPiOS` *or* `Raspbian/RPiOS Lite`
- Use `sudo raspi-config` to:
  - Enable (*interfaces*)
    - SSH
    - VNC
  - Connect to network (*if not already*)
  - Change Password

#### Update Modules  
```
sudo apt-get install update  
sudo apt-get install upgrade
```

#### Set Up Router Mode
Follow tutorial [here](https://github.com/garyexplains/examples/blob/master/raspberry_pi_router.md) 

**Notes:** *Will rewrite to only contain relevant parts because we do not use Eth1*

#### Install TeamViewer  
Follow tutorial [here](https://pimylifeup.com/raspberry-pi-teamviewer/)

**Notes:** *Will rewrite to only contain relevant parts and the website has a lot of ads*