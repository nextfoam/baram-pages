---
layout: post
title: Python Virtual Environment
category : installation
---

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
[solvers_windows_NF24.1.5.zip](https://d3c6e16xufx1gb.cloudfront.net/solvers_windows_NF24.1.5.zip)


### Linux
[solvers_linux_NF24.1.4.tar.xz](https://d3c6e16xufx1gb.cloudfront.net/solvers_linux_NF24.1.4.tar.xz)

You can download the file on command line with cURL or wget command like following.

```commandline
wget https://d3c6e16xufx1gb.cloudfront.net/solvers_linux_NF24.1.4.tar.xz
```

```commandline
curl -L https://d3c6e16xufx1gb.cloudfront.net/solvers_linux_NF24.1.4.tar.xz -o solvers_linux_NF24.1.4.tar.xz
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
