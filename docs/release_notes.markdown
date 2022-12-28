---
nav_order: 3
layout: page
title: Release Notes
---

# 22.1.0

## New Features
* Finnish(Suomi) translation has been added thanks to [Ricky Tigg](https://github.com/Ricky-Tigg)
* boundary selection/highlighting

## Improvements
* Transition between sequential and parallel calculation gets fluent

## Bug Fixes
* Residual chart was not displayed when a project is opened

## Know Issues
* Monitoring for a point that is not snapped on a surface is not working 
* Batch Processing is not implemented yet
* Rolling menus from Toolbar can be shown on the other display in multiple monitor configuration



# 22.0.7

## Bug Fixes
* Case loading failed when sliding mesh (MRF) does not have static boundaries
* "decompose" showed errors on some meshes

## Know Issues
* Monitoring for a point that is not snapped on a surface is not working 
* Batch Processing is not implemented yet
* Rolling menus from Toolbar can be shown on the other display in multiple monitor configuration



# 22.0.6

## New Features
* show/hide check box for each boundary

## Improvements
* [Internationalization support](https://nextfoam.github.io/baram-pages/docs/internationalization/)

## Bug Fixes
* Project name was not updated when the folder name was changed and reopened
* Dialog window to ask to save was popped up even when configuration was not changed
* `.gz` compressed polyMesh was not handled

## Know Issues
* Monitoring for a point that is not snapped on a surface is not working 
* Batch Processing is not implemented yet
* Rolling menus from Toolbar can be shown on the other display in multiple monitor configuration



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
