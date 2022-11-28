---
nav_order: 3
layout: page
title: Release Notes
---

# 22.0.5

## New Features
* Sliding Mesh Type in Cell Zone Configuration has been implemented ( "rotationMotion" of "solidBody" solver in dynamicMeshDict )
* Density of materials can be configured in polynomial values
* Monitoring field values for volume, surface, point snap on a surface, and force coefficient

## Improvements
* Default gravity value has changed to (0,0,0)
* Reference Values are now saved in configuration file

## Bug Fixes
* Turbulent intensity was set in percentage in the dictionaries
* Velocity Inlet Boundary Condition Dialog was not opened

## Know Issues
* Monitoring for a point that is not snapped on a surface is not working 
* Batch Processing is not implemented yet


# 22.0.4
The first release of BARAM
