# knx-ets-inside-linux-install


Installing on a Raspberry Pi 4 with 2GB of memory:

Steps
- Install Raspberry Pi OS FULL (2.5gb file) - IT WILL NOT WORK on the lite version.
- after installing OS, copy ETS-inside to boot partition of MicroSD card (and add ssh file to boot partition to enable ssh)
- log in via ssh and copy ETS to home folder: sudo cp /boot/ets-inside-5.7.085.9540.tar.gz /home/pi/
- un-tar the file: tar -zxvf ets-inside-5.7.085.9540.tar.gz
- sudo apt-get update
- sudo apt-get upgrade




KNX ETS Inside Server
---------------------
5.7.085.9540


Installation
------------


1. Install dependencies (was not necessary for full OS install)

   $ sudo apt-get install libc6-dev libunwind8


2. Create a user to run the server

   $ sudo adduser --disabled-password --home /usr/share/KNX knx


3. Copy the content of "./ets-inside" to /opt/KNX/ETSInside

   $ sudo mkdir -p /opt/KNX/ETSInside
   $ sudo cp -r ./ets-inside/* /opt/KNX/ETSInside
   $ sudo chmod a+x /opt/KNX/ETSInside/Knx.Ets.Osprey


4. Add the udev rule for the KNX USB licence stick

   $ sudo cp ./udev/10-ets-inside.rules /etc/udev/rules.d/10-ets-inside.rules


5. Add the init script

   $ sudo cp ./init.d/ets-inside /etc/init.d/ets-inside
   $ sudo chmod a+x /etc/init.d/ets-inside


6. Reload configuration

   $ sudo udevadm control --reload-rules
   $ sudo systemctl daemon-reload
   $ sudo update-rc.d ets-inside defaults


7. Start the server

   $ service ets-inside start


For more information visit
https://help.knx.org/EtsInside

