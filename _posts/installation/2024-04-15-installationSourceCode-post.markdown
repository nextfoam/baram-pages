---
layout: post
title: Installation with NextFOAM build
category : installation
---
# Installation with NextFOAM build

## Supported Platforms
<!--* Windows 10 or newer
* macOS 10.14 or newer (Apple Silicon only)-->
* Ubuntu 20.04 or newer
<!--* CentOS 8.2 or alternatives ( Rocky Linux, AlmaLinux, ... )-->
<!--* OpenSUSE Leap 15.4-->
<!--* Linux Mint 21 "Vanessa"-->

## BARAM requires following installed software:

* Python *3.9.x*
<!--* [MS-MPI](https://docs.microsoft.com/en-us/message-passing-interface/microsoft-mpi) 10.0 or newer ( Windows Only )-->
* OpenMPI 4.1 or newer ( Linux, macOS )
* GNU C Compiler or any other C Compiler ( Linux, macOS )


## Install BARAM, NextFOAM, OpenMPI

- OpenMPI is installed in the `/opt/openmpi-4.1.6` with `--prefix` option at `configure` command

```
sudo apt-get -y update 
sudo apt-get -y install build-essential flex zlib1g-dev libgmp-dev libmpfr-dev
wget https://download.open-mpi.org/release/open-mpi/v4.1/openmpi-4.1.6.tar.gz 
tar zxf openmpi-4.1.6.tar.gz 
rm openmpi-4.1.6.tar.gz 
cd openmpi-4.1.6 
./configure --prefix=/opt/openmpi-4.1.6 
make -j 4 all 
sudo make install 
echo 'export PATH=$PATH:/opt/openmpi-4.1.6/bin' | sudo tee -a /etc/bash.bashrc
```

- Install BARAM at `/opt/baram` with required packages. **pip3** should be used instead of default `pip` command
    
```
sudo apt install -y  qtbase5-dev
sudo apt-get install -y '^libxcb.*-dev' libx11-xcb-dev libglu1-mesa-dev libxrender-dev libxi-dev libxkbcommon-dev libxkbcommon-x11-dev texinfo
pip3 install --upgrade pip
cd /opt
sudo git clone https://github.com/nextfoam/baram.git
cd baram
sudo pip3 install --ignore-installed -r requirements.txt
sudo pip3 install https://d3c6e16xufx1gb.cloudfront.net/wheels/PySide6_QtAds-4.2.1.2.dev0-cp38-abi3-linux_x86_64.whl
```

- Build latest `NextFOAM-CFD` solver according to the instruction at [*https://github.com/nextfoam/nextfoam-cfd*](https://github.com/nextfoam/nextfoam-cfd)

- Copy compiled `NextFOAM-cfd` solvers and `Third-Party` libraries to `/opt/baram/solvers/openfoam`
    
```
export BARAM_DIR="/opt/baram"
    
sudo mkdir -p $BARAM_DIR/solvers/openfoam
sudo cp -a $WM_PROJECT_DIR/platforms/linux64GccDPInt32Opt/bin $BARAM_DIR/solvers/openfoam/
sudo cp -a $WM_PROJECT_DIR/platforms/linux64GccDPInt32Opt/lib $BARAM_DIR/solvers/openfoam/
sudo cp -a $WM_PROJECT_DIR/etc $BARAM_DIR/solvers/openfoam/

sudo mkdir -p $BARAM_DIR/solvers/openfoam/tlib

sudo cp -a $WM_THIRD_PARTY_DIR/platforms/linux64GccDPInt32/lib/* $BARAM_DIR/solvers/openfoam/tlib/
sudo cp -a $WM_THIRD_PARTY_DIR/platforms/linux64GccDPInt32/lib/libscotch* $BARAM_DIR/solvers/openfoam/tlib/
sudo cp -a $WM_THIRD_PARTY_DIR/platforms/linux64GccDPInt32/lib/sys-openmpi/libptscotch* $BARAM_DIR/solvers/openfoam/tlib/
sudo cp -a $WM_THIRD_PARTY_DIR/platforms/linux64Gcc/fftw-3.3.10/lib/libfftw3* $BARAM_DIR/solvers/openfoam/tlib/
sudo cp -a $WM_THIRD_PARTY_DIR/platforms/linux64Gcc/kahip-3.15/lib/libkahip_static.a $BARAM_DIR/solvers/openfoam/tlib/
```

- Compile Demonizer and resource
```
cd /opt/baram
sudo gcc -o solvers/openfoam/bin/baramd misc/baramd.c
sudo python3 convertUi.py
```

- Edit `baramMesh.sh`

    
```
sudo vi /opt/baram/baramMesh.sh
```
Comment out `source` and change `python` to `python3`
    
```
#source venv/bin/activate
python3 -m baramMesh.main
```

- Edit `baramFlow.sh`
```
sudo vi /opt/baram/baramFlow.sh
```

Comment out `source` and change `python` to `python3`
    
```
#source venv/bin/activate
python3 -m baramFlow.main
```

## Install `paraview`

- Install paraview using `apt-get` command. You can install `paraview` from the [paraview official download](https://www.paraview.org/download/) page.

```
sudo apt-get install paraview
```

## Create desktop shortcuts

- Create `Desktop` directory under `/etc/skel` for all users
- 

```
sudo mkdir -p /etc/skel/Desktop
```

- Create `baramMesh.desktop` under `/etc/skel/Desktop`

```
sudo vi /etc/skel/Desktop/baramMesh.desktop
```

```
[Desktop Entry]
Encoding=UTF-8
Name=baramMesh
Comment=baram Mesh
Icon=/opt/baram/baramMesh.png
Exec=bash -c '/opt/baram/baramMesh.sh'
Terminal=false
Type=Application
Categories=Science
```

- Create `baramFlow.desktop` under `/etc/skel/Desktop`

```
sudo vi /etc/skel/Desktop/baramFlow.desktop
```

```
[Desktop Entry]
Encoding=UTF-8
Name=baramFlow
Comment=baram Flow
Icon=/opt/baram/baramFlow.png
Exec=bash -c '/opt/baram/baramFlow.sh'
Terminal=false
Type=Application
Categories=Science
```
    
Change permission of shortcuts

```
sudo chmod +x /etc/skel/Desktop/*
```

**(NOTE)** You should upload `baramMesh.png` and `baramFlow.png` to `/opt/baram` directory.
