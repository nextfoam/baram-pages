---
nav_order: 3
layout: page
title: Installation
---
# Installing BARAM for Windows and macOS
Binary installation package for 64-bit windows and disk image for macOS with Apple Silicon are here for convenience.
Download them from following links.

[Download BARAM v24.4.0 Installer for 64-bit Windows ›](https://d3c6e16xufx1gb.cloudfront.net/BARAM-24.4.0-setup.exe){: .btn .btn-purple .text-center .fs-5 onclick="trackDownload('BARAM-24.4.0-setup.exe')"}

**NOTE: For macOS, [*open-mpi*](https://formulae.brew.sh/formula/open-mpi) Homebrew Formula should be installed in advance.**

[Download BARAM v24.4.0 Disk Image(.dmg) for macOS with Apple Silicon ›](https://d3c6e16xufx1gb.cloudfront.net/BARAM-24.4.0.dmg){: .btn .btn-blue .text-center .fs-5onclick="trackDownload('BARAM-24.4.0.dmg')"}

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

# Installing BARAM from source code

<ul>
  {% assign sorted_posts = site.categories.installation | sort: 'title' %}
  {% for post in sorted_posts %}
    <li><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>


## Paraview [Optional]

*BaramFlow* has a menu that can launch [*ParaView*](https://www.paraview.org/) for convenience.
If *ParaView* is installed in the system, this menu launches *ParaView* in the case foler.
