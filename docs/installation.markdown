---
nav_order: 3
layout: page
title: Installation
---

# Installing BARAM for Windows and macOS
Binary installation package for 64-bit windows and disk image for macOS with Apple Silicon are here for convenience.
Download them from following links.

[Download BARAM v24.1.3 Installer for 64-bit Windows ›](https://d3c6e16xufx1gb.cloudfront.net/BARAM-24.1.3-setup.exe){: .btn .btn-purple .text-center .fs-5 onclick="trackDownload('BARAM-24.1.3-setup.exe')"}

**NOTE: For macOS, [*open-mpi*](https://formulae.brew.sh/formula/open-mpi) Homebrew Formula should be installed in advance.**

[Download BARAM v24.1.2 Disk Image(.dmg) for macOS with Apple Silicon ›](https://d3c6e16xufx1gb.cloudfront.net/BARAM-24.1.2.dmg){: .btn .btn-blue .text-center .fs-5onclick="trackDownload('BARAM-24.1.2.dmg')"}

# Installing BARAM from Source Code

## Supported Platforms
* Windows 10 or newer
* macOS 10.14 or newer (Apple Silicon only)
* Ubuntu 20.04 or newer
* CentOS 8.2 or alternatives ( Rocky Linux, AlmaLinux, ... )
* OpenSUSE Leap 15.4
* Linux Mint 21 "Vanessa"

## BARAM requires following installed software:

* Python *3.9.x*
* [MS-MPI](https://docs.microsoft.com/en-us/message-passing-interface/microsoft-mpi) 10.0 or newer ( Windows Only )
* OpenMPI 4.1 or newer ( Linux, macOS )
* GNU C Compiler or any other C Compiler ( Linux, macOS )

## Clone the source code
```commandline
git clone https://github.com/nextfoam/baram.git
cd baram
```

## Setup Python virtual environment

Run following command in the top directory of downloaded source code.
Please don't forget that Python **3.9.x** is required.
You can check it with the command of `python3 -V`.

```commandline
python3.9 -m venv venv
```

## Enter into virtual environment
Run following command in the top directory of downloaded source code

### On Windows
```commandline
.\venv\Scripts\activate.bat
```

### On Linux or macOS
```commandline
source ./venv/bin/activate
```

### Upgrade pip version
```commandline
pip install --upgrade pip
```

## Install Python packages
Run following command in the top directory of downloaded source code
```commandline
pip install -r requirements.txt
```

## Copy Solver Executables
Download and uncompress solver executables into the top directory of downloaded source code.
The compressed files have _**solvers**_ folder in it.
Put _**solvers**_ folder into the top directory.
The final directory structure may look like following.
```
($BARAM)
|
+-- requirements.txt
+-- ...
+-- solvers/
|   |
|   +-- openfoam/
|       |
|       +-- bin/
|       +-- etc/
|       +-- ...
+-- ...
```

### Windows
[solvers_windows_NF24.1.6.zip](https://d3c6e16xufx1gb.cloudfront.net/solvers_windows_NF24.1.6.zip)


### Linux
[solvers_linux_NF24.1.6.tar.xz](https://d3c6e16xufx1gb.cloudfront.net/solvers_linux_NF24.1.6.tar.xz)

You can download the file on command line with cURL or wget command like following.

```commandline
wget https://d3c6e16xufx1gb.cloudfront.net/solvers_linux_NF24.1.6.tar.xz
```

```commandline
curl -L https://d3c6e16xufx1gb.cloudfront.net/solvers_linux_NF24.1.6.tar.xz -o solvers_linux_NF24.1.6.tar.xz
```

### macOS (Apple Silicon only)
Not yet prepared due to the strict code signing policy from Apple


## Compile Daemonizer ( only for Linux and macOS )
"solvers" directory was created when the compressed file was uncompressed.
```commandline
gcc -o solvers/openfoam/bin/baramd misc/baramd.c
```

## Compile Resource Files
```commandline
python convertUi.py
```

## Run BaramFlow
```commandline
python -m baramFlow.main
```

## Run BaramMesh
```commandline
python -m baramMesh.main
```

## Convenient Scripts that do not require manual *venv* activation

```commandline
baramFlow.sh
```
```commandline
baramMesh.sh
```

## Paraview [Optional]

*BaramFlow* has a menu that can launch [*ParaView*](https://www.paraview.org/) for convenience.
If *ParaView* is installed in the system, this menu launches *ParaView* in the case foler.
