---
nav_order: 4
layout: page
title: Apptainer
---

# Install apptainer in the Ubuntu Linux

To install [**BARAM-**](https://baramcfd.org) apptainer container, install [Apptainer](https://apptainer.org/) first.

- Install Apptainer in Ubuntu Linux 20.04 above. Below 18.04, you should install `apptainer` by yourself according to the instruction in https://github.com/apptainer/apptainer/blob/main/INSTALL.md

    ```
    $ sudo apt update
    $ sudo apt install -y software-properties-common
    $ sudo add-apt-repository -y ppa:apptainer/ppa
    $ sudo apt update
    $ sudo apt install -y apptainer
    ```


- Install Apptainer in CentOS Linux
    ```
    $ sudo yum install -y epel-release
    $ sudo yum install -y apptainer
    ```

# Install BARAM- Apptainer container

Download `baramxx.x.x.tar.gz` and unarchive as `tar zxf baramxx.x.x.tar.gz`. assign the excute permission to `install.sh`

[baram24.2.0.tar.gz]([https://drive.google.com/file/d/1gbTEtvSFPozhjtidOM5fHWli4uDOl7xI/view?usp=sharing](https://1drv.ms/u/s!AjRLfBSDK0kvfco1RpeJN9qzc3M?e=qsffG6))

```
$ tar zxf baram24.2.0.tar.gz
$ chmod +x install.sh
```

Execute the `install.sh` and input the installation path such as `~/baram-xx.x.x` You should have the write permission for the installation path.

```
$ ./install.sh
Enter the installation path: ~/baram-xx.x.x
```
If the installation is successful, apptainer container and icon images are located.
```
$ ls ~/baram-xx.x.x
baramxx.x.x.sif  baramFlow.png  baramMesh.png baramShell.png
```
And in the Desktop, `baramMesh` and `baramFlow` shourts are added.

You can run `baramMesh` and `baramFlow` by clicking the shortcut.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ApptainerImage.png"><br>
</p>

In the shell, you can run the application using `apptainer exec` command
```
$ apptainer exec ~/nextfoam/BARAM-24/baram-24.2.0.sif /opt/baram/baramMesh.sh
```
