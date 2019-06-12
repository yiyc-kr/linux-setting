# Nvidia Docker Setting

## Docker Install

1. Docker-ce Install
```
$ sudo apt-get remove docker docker-engine docker.io containerd runc
$ sudo apt autoremove
$ sudo apt-get update
$ sudo apt-get install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$ sudo apt-key fingerprint 0EBFCD88
$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
$ sudo apt-get update
$ sudo apt-get install -y docker-ce docker-ce-cli containerd.io
$ sudo docker run hello-world
```
  * Refer: <https://docs.docker.com/install/linux/docker-ce/ubuntu/>

2. Permission
```
$ sudo su
$ sudo usermod -aG docker [USER_NAME]
$ sudo service docker restart
```

## Install Cuda

1. Check OS version
```
$ uname -m && cat /etc/*release
```

2. Go to <https://developer.nvidia.com/cuda-downloads> & Download run file

3. Execute blow
```
$ sudo sh cuda_10.1...run
```

### Problems

* You appear to be running an X server
  1. Hit Ctrl+Alt+F1 and login using your credentials.
  2. kill your current X server session by typing sudo service lightdm stop or sudo lightdm stop
  3. Enter runlevel 3 by typing sudo init 3
  4. Install your *.run file.
    1. you change to the directory where you have downloaded the file by typing for instance cd Downloads. If it is in another directory, go there. Check if you see the file when you type ls NVIDIA*
    2. Make the file executable with chmod +x ./your-nvidia-file.run
    3. Execute the file with sudo ./your-nvidia-file.run
  5. You might be required to reboot when the installation finishes. If not, run sudo service lightdm start or sudo start lightdm to start your X server again.
  6. It's worth mentioning, that when installed this way, you'd have to redo the steps after each kernel update.
  * If you want to return X server. Hit Ctrl+Alt+F7
  * Refer: <https://askubuntu.com/questions/149206/how-to-install-nvidia-run>

* The Nouveau kernel driver is currently in use by your system.
  1. nano /etc/modprobe.d/blacklist-nouveau.conf
  2. with the following contents:
    ```
    $ blacklist nouveau
    $ options nouveau modeset=0
    ```
  3. Regenerate the kernel initramfs:
    ```
    $ sudo update-initramfs -u
    ```
  4. and finally: reboot
    ```
    sudo reboot
    ```
  * Refer: <https://askubuntu.com/questions/841876/how-to-disable-nouveau-kernel-driver>

## Readings

* Manual

<https://github.com/NVIDIA/nvidia-docker>

* Install docker-ce

<https://docs.docker.com/install/linux/docker-ce/ubuntu/>

* Environment

<http://drmola.com/bbs_free/318738>