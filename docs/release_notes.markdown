---
nav_order: 6
layout: page
title: Release Notes
---

# 24.0.1

## New Features
* [Flow] Point location preview has been added in point monitoring setup
* [Mesh] Object preview has been added in Geometry step

## Improvements
* [Flow] `pRefCell` is used instead of `pRefPoint`. Users don't need to configure *Reference Pressure Location* any longer.
* [Mesh] surface refinement level(castellatedMeshControls.refinementSurfaces.level[0]) plus one is used for castellatedMeshControls.refinementSurfaces.level[1]

## Bug Fixes
* [Flow] Numerical Conditions page was not correctly shown if energy model was not turned on after reading multi-region mesh
* [Mesh] Export failed if HEX6 was used as cell zone boundary
* [Mesh] Castellation failed if imported volume was configured as cell zone while its surface was configured as None.

## Know Issues
* [Flow] Monitoring for a point that is not snapped on a surface is not working in multi-region case


# 23.3.5

## New Features
* None

## Improvements
* [Mesh] Crossing lines between Hex6 far-end boundary and other geometries are classified as feature edges
* [Flow] Relative pressure is shown in monitoring chart rather than absolute pressure
* [Mesh] Surface for cell zones are configured as internal type to make mesh conform the surface
* [Flow] Warning message is displayed if a user leaves initialization page without clicking *initialize* button after changing setup
* [Flow] If section initializer is configured, Fixed Value type boundary value configured on boundary condition will not change the initialized values until re-initialization

## Bug Fixes
* [Flow] Base grid for Hex6 far-end boundary was slightly bigger than the Hex6
* [Flow] Text filter in boundary condition list is now working
* [Flow] *Select Color* and *Opacity* windows in *display control* were not modal windows
* [Mesh] No-boundary geometries were shown in the list of boundaries in the boundary layer step
* [Flow] Mesh could not be loaded after project creation
* [Flow] Exception occurred when text is typed in the filter input in boundary conditions


## Know Issues
* [Flow] Monitoring for a point that is not snapped on a surface is not working in multi-region case


# 23.3.3

## New Features
* None

## Improvements
* [Mesh] Castellation/Snap/BoundaryLayer operation can be cancelled during operation
* [Mesh] Default name is applied for Geometry, Region, etc

## Bug Fixes
* [Flow] Mesh could not be loaded since v23.3.2
* [Flow] Module path error in baramFlow.sh has been fixed
* [Flow] MRFProperties file was not removed even when the property is turned off
* [Flow][Mesh] Window could be out of sight when display configuration is changed in multiple screen environment


## Know Issues
* [Flow] Monitoring for a point that is not snapped on a surface is not working in multi-region case
* [Flow] Text filter in boundary condition list is not working


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
* [Flow] Monitoring for a point that is not snapped on a surface is not working in multi-region case


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
