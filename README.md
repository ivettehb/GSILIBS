# Instruction on building community GSI/EnKF

# 1. Hera, Jet, Orion, Cheyenne users:
For users on the following machines `Hera, Jet, Orion, Cheyenne`, the build process is very straight forward:

  run `ush/build.comgsi` under the main GSI directory and you will get executables, such as gsi.x, enkf-wrf.x, etc

# 2. Community users:

## 2.1 build required libraries
With the transition of NOAA GSI/EnKF codes to Github, the origial (outdated) libsrc/ was removed and those libraries will come from the [NCEPLIBS](https://github.com/NOAA-EMC/NCEPLIBS) repository released by [UFS](https://github.com/ufs-community/ufs-weather-model/wiki).  For how to build NCEPLIBS, please seek helps from the [UFS support forum](https://forums.ufscommunity.org).

## 2.2. build bufrlib and wrfio lib
This is a temporary solution as NCEPLIBS does not release bufrlib and wrfio lib at the moment. 
You can build these two libraries from the [comgsi/GSILIBS](https://github.com/comgsi/GSILIBS) repo at Github. 
```
mkdir build; cd build
cmake -DBUILD_CORELIBS=ON ..
make -j8
```
The libraries will be under build/lib

## 2.3. use ush/build.comgsi to do compling

#### (1) create a file to list all required modules for the build process:
for example, a file `modulefile.me.GSI_UPP_WRF` may looks like as follows:
```
module purge
module load intel/18.0.5 ncarenv ncarcompilers
module load impi/2018.4.274
module load mkl
module load netcdf
module load cmake/3.16.4
```
#### (2) change the following three variables accordingly in the ush/build.comgsi
    modulefile="/my/modulefile.me.GSI_UPP_WRF"
    NCEPLIBS="/my/NCEPLIBS/b_intel18.0.5_impi2018.4.274/install"
    GSILIBS="/my/GSILIBS/b_intel18.0.5_impi2018.4.274/"

#### (3) run "ush/build.comgsi" from the main GSI directory

**NOTE** For those who don't have module systems in HPCs, users can follow the ush/build.comgsi to set up enviormental variables and then do the compling.


