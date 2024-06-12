# Setup Bloodhound Hardware for use

## BMC Serial Console Connection:
- Baud Rate 115200
- HW Flow control = off
- 8 Bits
- Parity = none

## Default Login:
Login: root
Password: 0penBmc

## Set Volatile BMC IP Address:
Note: All settings through console connections are not persistent!  Interface designations could be different on hardware (eth0/end0).
1. 'ifconfig eth0 up <ipaddress> netmask <subnet>'

## BMC Web Interface:
Once IP address is set through serial BMC login to the web console and set all static settings required (IP, reboot, users, etc).

## Load Virtual Media or bootable USB:
1. Virtual Media:
  a. Load required virtual media ISO
  b. Start vitual media
2. Plug-in USB

## Install Host OS Remotely:
1. Set 'Boot Settings Override' to 'BiosSetup'
2. Select proper boot device in BIOS
3. Power on server
4. Edit the 'Install Rocky Linux x.x' selection to add the following:
  a. Remove the 'quite' flag
  b. Add 'console=ttyS0, 115200' #This allows for the Serial Over LAN(SOL) conection from the web interface.
  c. Press "CTRL + X"

