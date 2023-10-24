---
nav_order: 3
layout: page
title: Release Notes
---

# 23.3.2

## New Features
* None

## Improvements
* [Flow] "Reference Pressure Location" has been moved to "General" page
* [Flow] Boundary type is configured automatically according to the name of boundary
* [Mesh] Geometry import dialog now goes to the latest used folder
* [Mesh] "slipFeatureAngle" is configured as the half of featureAngle internally

## Bug Fixes
* [Flow] Chart Y range was not configured properly when the range value is big
* [Flow] "saveAs" menu is now stable.
* [Flow] "divSchemes" dictionary for Multi-phase(VoF) was not configured properly
* [Mesh] Default values of a few parameters have been changed

## Know Issues
* Monitoring for a point that is not snapped on a surface is not working in multi-region case


# 23.3.0

## New Features
* "BaramMesh" application for meshing job is added, and the name of "Baram" is changed to "BaramFlow" accordingly

## Improvements
* Time foler name in scientific notation like "1e-5" is properly handled now
* Monitoring for a point that is not snapped on a surface is now woring in single region case
* Parallel processing configuration is clear now. It's now not a configuration but an action to decompose/reconstruct
* Chart shows all the data when a project opened
* View alignment buttons on each Axis is simplified to one alignment button
* "Paraview" path configuration menu has been added

## Bug Fixes
* Chart could not be shown with an exception of "ValueError: Axis limits cannot be NaN or Inf"
* Residual chart was not shown for a copied project
* Gravity could be configured only for Multi-phase(VoF) case
* Initialization Parameters were not applied even though Initialization button was clicked if user stayed in the page
* Atmospheric Wall was not shown in wall boundary condition

## Know Issues
* Monitoring for a point that is not snapped on a surface is not working in multi-region case
* "save as" menu is not stable yet. Copy the project project manually



# 23.2.0

## New Features
* "hostfile" setting is possible for the calculation on a cluster

## Improvements
* Last position and size of Window are saved for next launch

## Bug Fixes
* Parallel calculations for more than 20 boundaries are working 
* mesh transformation is working for decomposed mesh
* Fixed: Rolling menus from Toolbar displayed on the other display in multiple monitor configuration

## Know Issues
* Monitoring for a point that is not snapped on a surface is not working 
* Batch Processing is not implemented yet
* "save as" menu is not stable yet. Copy the project project manually



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
