---
nav_order: 6
layout: page
title: Release Notes
---

# 24.4.0

## New Features

### BaramFlow
* **Cavitation:** Mass transfer model for cavitation analysis has been added.
* **Non-Newtonian Viscosity:** Non-Newtonian viscosity model has been added for liquid material in laminar flow.
* **Multiple phases:** More than 2 phases can be set up in multiphase case.
* **FLUENT Mesh:** Fluent mesh with multiple cell zones can be imported into multiple regions.
* **FLUENT Mesh:** Fluent Mesh with non-tetrahedral cells can be imported.
* **Mesh:** Boundaries that have no face are automatically dropped when mesh is imported.
* **Maximum Diffusion Number:** *Maximum Diffusion Number* can be configured for transient multi-region case.
* **Thermal layers:**  Optional thin thermal layer resistances can be configured for convection boundaries.
* **Turbulent Viscosity Ratio:** *Turbulent Viscosity Ratio* spec. on boundaries for *Spalart-Allmaras* turbulence model is working now.
* **Ruler:** *Ruler* has been added in Graphics view.
* **Background Color:** Background color of Graphics view can be changed
* **Scalar Report:** Report for scalar values has added

### BaramMesh
* **Graphics View:** Graphics View can be disabled for fast navigation between steps.
* **Ruler:** *Ruler* has been added in Graphics view toolbar.
* **Background Color:** Background color of Graphics view can be changed
* **Export:** Boundaries that have no face are dropped when mesh is exported.

## Improvements

### BaramFlow
* **Update Configuration:** *Temperature limit* and *max viscosity ratio* settings in advanced numerical calculation can be applied on the fly during calculation
* **ABL Inlet:** Species fraction and User-defined Scalars values can be configured on ABL Inlet boundary.
* **NeighbourPatch:** Peer boundary for *cyclic* and *cyclicAMI* boundaries is set from *neighbourPatch* information.
* **Axes widget:** Axes widget is automatically scaled when mesh is transformed.
* **Zero Gravitation:** Gravitation can now be set to zero for multiphase VoF case.
* **User-defined Scalar:** User-defined Scalar configuration can be modified.
* **Material Spec.:** Viscosity spec. and Thermal conductivity spec. are linked.

### BaramMesh
* **Number of Cells per Direction:** *Number of Cells per Direction* in Base grid accepts only a value equal or greater than 2.
* **Export:** Boundaries that have no face are dropped when mesh is exported.
* **Castellation:** *Number of Cells between Levels* value of *zero* is not accepted.
* **Export 2D:** Generated mesh can be exported in 2D Axi-Symmetry form.
* **Export 2D:** Generated mesh can be exported in 2D planar form.

## Bug Fixes

### BaramFlow
* **Boundary:** Static Temperature configuration on *supersonic inflow* boundary was not used for calculation.
* **Monitoring:** Monitoring was not working for primary material field.
* **User-defined Scalars:** *Turbulent Viscosity* spec. has removed.

## Known Issues

### BaramFlow
* **Cavitation:** Cavitation(mass transfer) model allows only transient calculation.
* **Multiphase:** Steady state calculation is not allowed if the number of phases is greater than 2.
* **Cavitation:** *Zwart-Gerber-Belamri* mass transfer model is not supported yet
* **Residual:** Residual is not available for cases that have more than two phases
* **Cell Zone:** *mass source* is not working

### BaramMesh
* **Export:** 2D export does not support multi-region mesh.

# 24.3.3

## Bug Fixes

### BaramFlow
* **Save As:** Some configuration could not be changed after saving by *Save As*.

### BaramMesh
* **Export:** Application got stuck or missed *polyMesh* folder while exporting.

## Known Issues

### BaramFlow
* **Species Model:** Density is not calculated if energy model is not turned on.


# 24.3.2

## Bug Fixes

### BaramFlow
* **Section Initialization:** Volume fraction configuration in section initialization was not working
* **Monitoring:** Monitoring was not working for primary material

## Known Issues

### BaramFlow
* **Species Model:** Density is not calculated if energy model is not turned on.
* **Save As:** Some configuration cannot be changed after saving by *Save As*. The problem goes away once the application exits and restarts.

### BaramMesh
* **Export:** Application gets stuck or misses *polyMesh* folder while exporting. To add boundary layers prevents this problem.


# 24.3.1

## Bug Fixes

### BaramFlow
* **Cell Zone:** Cell Zone configuration is now working

## Known Issues

### BaramFlow
* **Species Model:** Density is not calculated if energy model is not turned on.
* **Section Initialization:** Volume fraction configuration in section initialization is not working
* **Monitoring:** Monitoring is not working for primary material


# 24.3.0

## New Features

### BaramFlow
* **Species Model:** A species model has been added.
* **Equation Control:** Equations can now be controlled to solve or not.
* **Energy Equation Terms:** Each term in the energy equation can be controlled to include or exclude it.
* **Boundary Condition Copy:** You can now copy a boundary condition to other boundary conditions.

### BaramMesh
* **Expected Cell Size Display:** The expected cell size is now shown in the refinement dialog.
* **Slice Cut Tool:** A Slice Cut tool has been added to the display control.

## Improvements

### BaramFlow
* **User-Defined Scalar Calculation:** User-defined scalar calculations converge better in steady-state cases.
* **Output Display:** Output from the decomposePar command is now displayed in the console window.
* **Viscosity Validation:** A Viscosity value of zero is now rejected in the material dialog.
* **Windows Docking:** Windows docking has become more versatile and convenient thanks to the [*QT Advanced Docking System*](https://github.com/githubuser0xFFFF/Qt-Advanced-Docking-System).

### BaramMesh
* **Feature Angle Threshold:** The default value for the Feature Angle Threshold has changed from 120 to 60.
* **Export Dialog Enhancement:** The Export dialog now allows separate configuration of project name and location.

## Bug Fixes

### BaramFlow
* **User-Defined Scalars:** The defaultFieldValues were incorrectly configured for user-defined scalars during section initialization.
* **Residual Value Display:** Residual values larger than 1 were clipped and not shown.
* **Energy Relaxation Factor:** The default value for the relaxation factor of Energy has been changed to 1.0 from 0.9.
* **Locale Compatibility:** BaramFlow now works correctly in locales where a comma (,) is used as the decimal separator.
* **OpenMPI Compatibility:** BaramFlow no longer has trouble working with the latest Homebrew OpenMPI version 5.0.3.

### BaramMesh
* **Mesh Quality Calculation:** Mesh quality information is now correctly calculated even if a boundary layer is not added.
* **Cell Count Update:** The cell count is now updated after mesh generation in each step.
* **Boundary Type Compatibility:** Interface can be used as cyclic boundaries. The boundary pair of an interface now have same face ordering. The order was different in some cases before.
* **Feature Edge Refinement:** Feature edge refinement is now applied only to cells that the feature edge penetrates (within 0.01m from the feature edge).
* **STL Splitter Fix:** The STL splitter now handles cases where some faces have an area of zero.
* **Boundary Layer Group Configuration:** The boundary layer group configuration no longer gets corrupted when both boundary layer group configuration and advanced configuration are modified.

## Known Issues

### BaramFlow
* **Species Model:** Density is not calculated if energy model is not turned on.
* **Cell Zone:** Cell Zone configuration is not working
* **Section Initialization:** Volume fraction configuration in section initialization is not working


# 24.2.0

## New Features

### BaramFlow
* LES/DES turbulence modeling
* User-defined scalar
* Non-Reflecting Boundary option in Pressure Outlet
* Calculation result is saved regardless of write interval when calculation ends

### BaramMesh
* Interactive splitting of surface based on feature angle during STL import
* Gap-Refinement in Volume Refinement

## Improvements

### BaramFlow
* Enhanced wall function has been applied
* Reference Pressure consideration in calculating force coefficients
* Maximum Viscosity ratio can be limited
* Margin around Y axis label has grown
* Default initial value for pressure is set to 101325 when density-based solver is chosen
* Solver NF24.2.1 is used as internal solver

### BaramMesh
* VTK pipeline processing in parallel(SMP)

## Bug Fixes

### BaramFlow
* "Prt", energy Prandtl number, setting was in wrong position in turbulenceProperties

### BaramMesh
* BaramMesh crashed sporadically when a project was closed
* "Cancel" button did not work in castellation and snap

----

# 24.1.3

## Improvements

### BaramFlow
* Cell Zone is hilighted when selected
* Solver NF24.1.6 is used as internal solver

## Bug Fixes

### BaramFlow
* Parallel configuration dialog hung if number of processors were not changed and *Apply* button was clicked
* Monitoring for a point that is not snapped on a surface is now working in multi-region case
* "saveAs" for Parallel-configured project is now working

### BaramMesh
* "Export" succeeded only when boundary layers were inserted and baramMesh run in parallel configuration

----

# 24.1.2

## New Features

### BaramFlow
* *User Parameters* can be defined and used for configuration
* Mesh information such as bounding box dimension, number of cells, and min/max cell volumes
* Density-base solver with far-field Riemann boundary condition for high Mach number external flow
* Batch processing: Users can setup *User Parameters* in combination and run them in sequence
* Multi-region case can be set up by importing separated multiple polyMesh which might be generated by other meshing tools
* Flow direction can be configured based on Angle of Attack(AoA) and Angle of Sideslip(AoS)

### BaramMesh
* Mesh Quality information can be checked interactively
* *Snap* step now supports *Implicit Feature Snapping*

## Improvements

### BaramFlow
* Wall function for Realizable k-e with enhanced wall treatment model has updated
* The concept of “Modified Pressure” has been deprecated. The solver now automatically applies pressure adjustments based on the selected solver type.
* Users can transfer steady-state calculation results as initial conditions for transient simulations.
* Units are now explicitly shown for cell zone source terms
* A pop-up window notifies users when the solver finishes its calculations
* Certain boundary condition types are inferred from mesh boundary names and geometric types
* Users can adjust the maximum Courant number for multi-phase steady simulations
* NF24.1.5 is used as internal solver

### BaramMesh
* Maximum surface refinement level can be configured. It was a fixed value of minimum plus one
* Spaces in geometry names are automaticall replaced with underscore('_')
* Users can now configure region steps to include solid regions only ( no fluid region )
* Fixed width font is used in console window

## Bug Fixes

### BaramFlow
* Prevented loading of multi-region meshes inappropriately for multi-phase projects

### BaramMesh
* Fixed a bug where castellation failed when a sphere was within a HEX6 bounding box

## Known Issues

### BaramFlow
* Monitoring for a point that is not snapped on a surface is not working in multi-region case
* "saveAs" for Parallel-configured project is not working

### BaramMesh
* "Export" succeeds only when boundary layers are inserted and baramMesh runs in parallel configuration

----

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

## Known Issues
* [Flow] Monitoring for a point that is not snapped on a surface is not working in multi-region case

----

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


## Known Issues
* [Flow] Monitoring for a point that is not snapped on a surface is not working in multi-region case

----

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


## Known Issues
* [Flow] Monitoring for a point that is not snapped on a surface is not working in multi-region case
* [Flow] Text filter in boundary condition list is not working

----

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

## Known Issues
* [Flow] Monitoring for a point that is not snapped on a surface is not working in multi-region case

----

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

## Known Issues
* Monitoring for a point that is not snapped on a surface is not working in multi-region case
* "save as" menu is not stable yet. Copy the project project manually

----

# 23.2.0

## New Features
* "hostfile" setting is possible for the calculation on a cluster

## Improvements
* Last position and size of Window are saved for next launch

## Bug Fixes
* Parallel calculations for more than 20 boundaries are working 
* mesh transformation is working for decomposed mesh
* Fixed: Rolling menus from Toolbar displayed on the other display in multiple monitor configuration

## Known Issues
* Monitoring for a point that is not snapped on a surface is not working 
* Batch Processing is not implemented yet
* "save as" menu is not stable yet. Copy the project project manually

----

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

## Known Issues
* Monitoring for a point that is not snapped on a surface is not working 
* Batch Processing is not implemented yet
* Rolling menus from Toolbar can be shown on the other display in multiple monitor configuration

----

# 22.1.0

## New Features
* Finnish(Suomi) translation has been added thanks to [Ricky Tigg](https://github.com/Ricky-Tigg)
* boundary selection/highlighting

## Improvements
* Transition between sequential and parallel calculation gets fluent

## Bug Fixes
* Residual chart was not displayed when a project is opened

## Known Issues
* Monitoring for a point that is not snapped on a surface is not working 
* Batch Processing is not implemented yet
* Rolling menus from Toolbar can be shown on the other display in multiple monitor configuration

----

# 22.0.7

## Bug Fixes
* Case loading failed when sliding mesh (MRF) does not have static boundaries
* "decompose" showed errors on some meshes

## Known Issues
* Monitoring for a point that is not snapped on a surface is not working 
* Batch Processing is not implemented yet
* Rolling menus from Toolbar can be shown on the other display in multiple monitor configuration

----

# 22.0.6

## New Features
* show/hide check box for each boundary

## Improvements
* [Internationalization support](https://nextfoam.github.io/baram-pages/docs/internationalization/)

## Bug Fixes
* Project name was not updated when the folder name was changed and reopened
* Dialog window to ask to save was popped up even when configuration was not changed
* `.gz` compressed polyMesh was not handled

## Known Issues
* Monitoring for a point that is not snapped on a surface is not working 
* Batch Processing is not implemented yet
* Rolling menus from Toolbar can be shown on the other display in multiple monitor configuration

----

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

## Known Issues
* Monitoring for a point that is not snapped on a surface is not working 
* Batch Processing is not implemented yet

----

# 22.0.4
The first release of BARAM
