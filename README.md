# download iso

open <http://www.ubuntu.com/download/desktop/>
![download_iso](https://raw.githubusercontent.com/ouiyeah/ubuntu/master/img/download_iso.png "download_iso")

use other software (e.g. ultraiso) to make boot disk if necessary

***
# install system

![install_start](https://raw.githubusercontent.com/ouiyeah/ubuntu/master/img/install_start.png "install_start")
![select_language](https://raw.githubusercontent.com/ouiyeah/ubuntu/master/img/select_language.png "select_language")
![select_custom](https://raw.githubusercontent.com/ouiyeah/ubuntu/master/img/select_custom.png "select_custom")
![select_type](https://raw.githubusercontent.com/ouiyeah/ubuntu/master/img/select_type.png "select_type")
![select_location](https://raw.githubusercontent.com/ouiyeah/ubuntu/master/img/select_location.png "select_location")
![select_keyboard](https://raw.githubusercontent.com/ouiyeah/ubuntu/master/img/select_keyboard.png "select_keyboard")
![install_wait](https://raw.githubusercontent.com/ouiyeah/ubuntu/master/img/install_wait.png "install_wait")
![install_complete](https://raw.githubusercontent.com/ouiyeah/ubuntu/master/img/install_complete.png "install_complete")

***
# ethernet connection

![ethernet_connection](https://raw.githubusercontent.com/ouiyeah/ubuntu/master/img/ethernet_connection.png "ethernet_connection")

set dns as network provider 

> 211.136.17.107 / 211.136.112.50 for china mobile

remember to set the link for network connection if failed to visit websites after installation

>$ sudo ln -s /run/resolvconf/resolv.conf /etc/resolv.conf

***
# remote desktop

set desktop sharing if it is used as host
![desktop_sharing](https://raw.githubusercontent.com/ouiyeah/ubuntu/master/img/desktop_sharing.png "desktop_sharing")
![desktop_settings](https://raw.githubusercontent.com/ouiyeah/ubuntu/master/img/desktop_settings.png "desktop_settings")

set remmina if it is used as terminal
![remmina_client](https://raw.githubusercontent.com/ouiyeah/ubuntu/master/img/remmina_client.png "remmina_client")
![remmina_add](https://raw.githubusercontent.com/ouiyeah/ubuntu/master/img/remmina_add.png "remmina_add")

***
# change hostname

>$ sudo vi /etc/hostname

    [hostname]

>$ sudo vi /etc/hosts

    127.0.0.1       localhost
    127.0.1.1       [hostname]

***
# auto startup

![startup_applications](https://raw.githubusercontent.com/ouiyeah/ubuntu/master/img/startup_applications.png "startup_applications")
![edit_preferences](https://raw.githubusercontent.com/ouiyeah/ubuntu/master/img/edit_preferences.png "edit_preferences")

edit the startup program command as follow if running boot.sh file

> gnome-terminal -x ./workspaces/boot.sh

>$ chmod +x ~/workspaces/boot.sh

edit the startup program command as follow if running ros file before calling .bashrc

> gnome-terminal -x bash -c 'export ROS_IP=`hostname -I`; source /opt/ros/indigo/setup.bash; source ~/catkin_ws/devel/setup.bash; roslaunch bringup bringup-boot.launch'

***
# auto shutdown

>$ pkexec visudo -f /etc/sudoers

add the following lines at the end of the file

    [user] [hostname]=NOPASSWD: /sbin/shutdown -h now
    [user] [hostname]=NOPASSWD: /sbin/reboot

save (ctrl^o) and exit (ctrl^x)

***
# usermod permission

>$ sudo usermod -aG dialout username

create tty rule file for current user

>$ echo 'KERNEL=="ttyUSB[0-9]*", MODE="0666"' | sudo tee -a /etc/udev/rules.d/70-ttyusb.rules

***
# remastersys backup

download [remastersys_3.0.3-1_all.deb](https://raw.githubusercontent.com/ouiyeah/ubuntu/master/pkg/remastersys_3.0.3-1_all.deb)
![install_remastersys](https://raw.githubusercontent.com/ouiyeah/ubuntu/master/img/install_remastersys.png "install_remastersys")

change "WORKDIR" to custom directory (e.g. /home/remastersys)

>$ sudo nano /etc/remastersys.conf

do the remastersys backup

>$ sudo remastersys backup

wait for a while and get the generated file <custom-backup.iso> at /home/remastersys/

use other software (e.g. ultraiso) to make boot disk if necessary
