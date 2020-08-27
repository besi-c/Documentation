# Relay Setup

## Notes/To-Do
- Need to shebang script files so they can be executed without `bash <script>` or `python3 <script.py>`

## System Configuration
Assuming NOOBS SD card came with RPi Zero W
- Connect to network
- Install Rapsbian/RPiOS Lite (*Does not include GUI Elements*)
- Use `sudo raspi-config` to:
  - Enable (*interfaces*)
    - SSH
    - SPI
    - I2C
  - Connect to network (*if not already*)
  - Change Password

#### Update Modules  
```
sudo apt-get install update  
sudo apt-get install upgrade
```

#### Install Python3  
```
sudo apt-get install python3
```

#### Install git (*if not present*)  
```
sudo apt-get install git
```

### Relay Code Setup   
#### Clone Digital Relay Repo  
```
git clone https://github.com/yamartinez/BESI-Digital_Relays.git  
```

#### Change into that directory
```
cd BESI-Digital_Relays
```

#### Install Python Dependencies  
```
sudo bash Dependencies.sh
sudo pip3 install -r packages.pk
```

#### Configure iBeacon Packets to have unique ID
Use `nano` (or `vim`) to edit Beacon.sh 
```
nano Beacon.sh
```

Modify the two hex values before the values `BE 51` to the ID of the new relay on the last line.

> Ex) Relay ID 08 - the line should end with
> `08 BE 51 C8 00`

Exit and Save with `CTRL+X` and `Enter`/`Return` Twice

#### Setup periodic AWS Data Upload
**This section is work in progress**, right now, data is only zipped up periodically. Still working on S3 upload.

Add Execute permissions to Task.sh
```
chmod 777 create_ssh_tunnel.sh

```

This will be done using a periodic CRON job.
```
crontab -e
```
If prompt to select editor chose `nano` or what you're most comfortable with  

Go to the end of the file and add Task.sh on periodic task (below assumes every 30 mintues)
```
*/30 * * * * /home/pi/BESI-Digital_Relays/Task.sh
```

Exit and Save with `CTRL+X` and `Enter`/`Return` Twice

#### Set up I2S Library

**Warning:** this may take a long time but doesn't require much effort from user while kernel is building.  

I recommend changing to home directory with `cd ~` before following tutorial.

*The first tutorial linked is more complicated but near guaranteed to work - second one is much simpler but may not work.*

Follow tutorial [here](https://learn.adafruit.com/adafruit-i2s-mems-microphone-breakout/raspberry-pi-wiring-and-test).

There is a "newer" tutorial [here](https://learn.adafruit.com/adafruit-i2s-mems-microphone-breakout/raspberry-pi-wiring-test) but it did not work for me when I tried it - you can give it a try but your milage may vary.  

#### Add run.sh to Startup  
Edit rc.local file
```
sudo nano /etc/rc.local
```

And before the line that says `exit 0` add  
```
 bash /path/to/cloned/dir/run.sh &
```
*the `&` at the end allows it to run in the back ground*

save with `ctrl+x` then `enter`/`return` twice
