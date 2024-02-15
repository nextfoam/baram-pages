---
nav_order: 4
layout: page
title: Apptainer
---

# Install apptainer in the Ubuntu Linux

To install [**BARAM-24**](https://baramcfd.org) apptainer container, install [Apptainer](https://apptainer.org/) first.

- Install Apptainer in Ubuntu Linux
    ```
    $ sudo apt update
    $ sudo apt install -y software-properties-common
    $ sudo add-apt-repository -y ppa:apptainer/ppa
    $ sudo apt update
    $ sudo apt install -y apptainer
    ```

(Note) in the Ubuntu 18.04 or below, you need to compile apptainer manually by yourself according to the instruction in the https://github.com/apptainer/apptainer/blob/main/INSTALL.md

- Install Apptainer in CentOS Linux
    ```
    $ sudo yum install -y epel-release
    $ sudo yum install -y apptainer
    ```

# Install BARAM-24 Apptainer container

Download `install.sh` and `BARAM24.0.1.tar` in the same directory and assign the excute permission to `install.sh`

[install.sh](https://drive.google.com/file/d/1TpdMS6-46aV4Iwx5Ab7FypWiiOYHkLiC/view?usp=sharing)

[BARAM24.0.1.tar](https://drive.google.com/file/d/1VgU-XnPKYDr6JGAYo_OU1RzIdPf_dCTQ/view?usp=sharing)

```
$ chmod +x install.sh
```

Execute the `install.sh` and input the installation path. You should have the write permission for the installation path.

```
$ ./install.sh
Enter the installation path: ~/nextfoam/BARAM-24
```
If the installation is successful, apptainer container and icon images are located.
```
$ ls ~/nextfoam/BARAM24
baram24.0.1-ubuntu22.04.sif  baramFlow.png  baramMesh.png baramShell.png
```
And in the Desktop, `baramMesh` and `baramFlow` shourts are added.

You can run `baramMesh` and `baramFlow` by clicking the shortcut.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ApptainerImage.png"><br>
</p>

In the shell, you can run the application using `apptainer exec` command
```
$ apptainer exec ~/nextfoam/BARAM-24/baram24.0.1-ubuntu22.04.sif /opt/baram/baramMesh.sh
```