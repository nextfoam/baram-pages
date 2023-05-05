---
nav_order: 3
layout: page
title: Release Notes
---

# 23.1.0

## New Features
* Multi-Phase(VoF) problems can be simulated
* Feature Edge view mode added
* section initialization function (setFields) added
* About page added

## Improvements
* Previous console log and residuals are now shown when a project is opened
* Progress is displayed on reconstruction
* Locale change goes effective as soon as configured
* Finnish Translation updated thanks to Ricky-Tigg
* M1 macOS supported

## Bug Fixes
* Global fvSolution was not created in multi-region case

## Know Issues
* Monitoring for a point that is not snapped on a surface is not working 
* Batch Processing is not implemented yet
* Rolling menus from Toolbar can be shown on the other display in multiple monitor configuration



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
