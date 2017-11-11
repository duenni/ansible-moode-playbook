**Note: this is a 'quick and dirty' solution which works but needs some optimization**

This Playbook reflects Tim Curtis' build_recipe for [moodeaudio](http://moodeaudio.org/). So a build of moode won't has to be done manually anymore.

Example `hosts` file:

```
[moode]
moode
```

What you need:
* RaspberryPi with [Raspbian Stretch Lite](http://downloads.raspberrypi.org/raspbian_lite/images/raspbian_lite-2017-09-08/2017-09-07-raspbian-stretch-lite.zip) installed and SSH access (Create an empty file named "ssh" in the boot directory)
* Ansible >v2.2 control machine
* Copy your public SSH key to the Raspi for passwordless access `cat ~/.ssh/id_rsa.pub | ssh pi@<IPADDRESS> 'umask 0077; mkdir -p .ssh; cat >> .ssh/authorized_keys && echo "Key copied"'` (pwd=raspberry)
* `ssh pi@raspberrypi` 
* `echo "pi:moodeaudio" | sudo chpasswd`
* `sudo sed -i "s/raspberrypi/moode/" /etc/hostname`
* `sudo sed -i "s/raspberrypi/moode/" /etc/hosts`
* `sudo reboot`
* Clone repo to control machine: `git clone https://github.com/duenni/ansible-moode-playbook.git`
* `cd ansible-moode-playbook`
* `ansible-playbook site.yml`

Tested with:
* `ansible 2.4.1.0`
* Raspberry Pi 3 Model B
* moode 4 Beta 8 with `build_recipe_v1.6.txt`