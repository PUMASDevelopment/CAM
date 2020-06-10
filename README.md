# PUMAS CAM: The Community Atmosphere Model used by the PUMAS development team

CAM code is stored in this repository on branches other than master.  The details are explained below.

Please see the [wiki](https://github.com/ESCOMP/CAM/wiki) for complete documentation on CAM, getting started with git and how to contribute to CAM's development.

This repository has at least three branches:
* master - contains this readme and the Code of Conduct information (not used)
* cam_development - contains the current CAM development code mirrored from ESCOMP/CAM
* cam_pumas_development - the current CAM development code with changes required to run the unified ice closure and all PUMAS developments

## Workflow to make changes to PUMAS (unreleased) code:

1. Clone a copy of PUMASDevelopment/CAM
```
git clone https://github.com/PUMASDevelopment/CAM.git PUMASDev_CAM_Sandbox
cd PUMASDev_CAM_Sandbox/
```
2. Checkout the cam_pumas_development branch (note: the “git branch” command will show you which branch you are currently on. Use often!)
```
git checkout cam_pumas_development
git branch
```
3. Run manage_externals
```
./manage_externals/checkout_externals
```
4. Checkout PUMAS master branch (Steps 1-4 only if you haven’t already done these before)
```
cd src/physics/pumas/
git checkout master
```
5. Make a personal work branch (optional)   
```
git checkout -b kt_ppe_pumas_work
git push origin kt_ppe_pumas_work
```
(You can also, optionally, make a personal work branch in the CAM repo if there are a lot of changes to the cam_pumas_development branch.)
```
cd ../../..
git checkout -b kt_ppe_cam_work
git push origin kt_ppe_cam_work
```
6. Make changes anywhere you want in the sandbox
```
cd src/physics/pumas
emacs micro_mg4_0.F90
```
7. Run tests (optional)
```
cd ../../../cime/scripts
qcmd -- ./create_test ERP_Ln9.f09_f09_mg17.F2000climo.cheyenne_intel.cam-outfrq9s_mg3
```
8. Commit and push any pumas changes
```
cd ../../src/physics/pumas/
git add micro_mg4_0.F90
git commit -m "Example commit just adding whitespace"
git push
```
9. Update Externals_CAM.cfg (optional to point to your branch)
```
cd ../../..
emacs Externals_CAM.cfg
```
Under [pumas] ...
```
branch = kt_ppe_work
```
10. Commit and push CAM changes
```
git status
git add Externals_CAM.cfg 
git commit -m "Example changes to pumas dir"
git push
```
11. Eventually, make pull requests to master in the PUMAS repo or cam_pumas_development in the CAM repo if you made branches off of these. I can merge in your changes using these pull requests.

## Workflow to make changes to CAM Trunk (released) code:

1. Clone a copy of PUMASDevelopment/CAM
```
git clone https://github.com/PUMASDevelopment/CAM.git PUMASDev_CAM_Sandbox
cd PUMASDev_CAM_Sandbox/
```
2. Checkout the cam_development branch (note: the “git branch” command will show you which branch you are currently on. Use often!)
```
git checkout cam_development
git branch
```
3. Run manage_externals
```
./manage_externals/checkout_externals
```
4. Checkout PUMAS release/cam branch (Steps 1-4 only if you haven’t already done these before)
```
cd src/physics/pumas/
git checkout release/cam
```
5. Make changes anywhere you want in the sandbox
```
emacs micro_mg3_0.F90
```
6. Run tests (optional)
```
cd ../../../cime/scripts
qcmd -- ./create_test ERP_Ln9.f09_f09_mg17.F2000climo.cheyenne_intel.cam-outfrq9s_mg3
```
7. Commit and push any PUMAS changes
```
cd ../../src/physics/pumas/
git add micro_mg3_0.F90
git commit -m "Example commit just adding whitespace"
git push
```
8. Make a PUMAS tag, then push it to remote
```
git tag -l 
git tag -a pumas_cam-release_v1.4 -m "Example tag"
git push origin pumas_cam-release_v1.4
```
9. Update Externals_CAM.cfg
```
cd ../../..
emacs Externals_CAM.cfg
```
Under [pumas]
```
tag = pumas_cam-release_v1.4
```
10. Commit and push CAM changes
```
> git status
> git add Externals_CAM.cfg 
> git commit -m "Example changes to pumas dir"
> git push
```
11. Make a pull request to ESCOMP/CAM

(Note: I can make PUMAS tags and issue CAM pull requests for you if you are uncomfortable or too busy for steps 8-11, that is generally considered more of a SE task than a science task )


### CAM Documentation - https://ncar.github.io/CAM/doc/build/html/index.html

### CAM6 namelist settings - http://www.cesm.ucar.edu/models/cesm2/settings/current/cam_nml.html

