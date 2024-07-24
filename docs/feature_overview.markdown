---
nav_order: 2
layout: page
title: Features
---

# Applications

* [BaramFlow](#baramflow)
* [BaramMesh](#barammesh)

# BaramFlow

## Supported Mesh Types
* OpenFOAM PolyMesh
* Fluent case (.cas)
* Fluent mesh (.msh)
* Gmsh (.msh)
* I-deas Univesl (.unv)


## Mesh manipulation
* Scale
* Translate
* Rotate


## Turbulent Models
* Laminar
* Spalart-Allmaras
* k-epsilon
    * Standard
    * RNG
    * Realizable
* k-omega
    * SST
* LES
* DES


## Cell Zone Configuration
* Zone Types
    * Multiple Reference Frame (MRF)
    * Porous Zone
    * Sliding Mesh
    * Actuator Disk
* Source Terms
* Fixed Values


## Monitoring values
* Residual Values
* Force Coefficients
* Point Values
* Surface Values
* Volume Values


## Parallel Processing
* MPI Parallel Processing



# BaramMesh

* No limit on the number of input surfaces
* Automatic detection of closed surface composing a volume
* Automatic surface split based on face angle
* Support native simple geometry ( Hex, Sphere, Cylinder )
* Build prismatic boundary layers
* scales well when meshing in **parallel**
* can work with dirty surfaces, i.e. non-watertight surfaces
* Support **Multi-Region** Mesh for OpenFOAM Multi-Region cases
* Support both **conformal** and **non-conformal** interfaces
* Support Cell Zones
* Generate meshes for external flow and internal flow
* Mesh refinement based on surfaces, feature edges and volumes


