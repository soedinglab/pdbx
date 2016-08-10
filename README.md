# pdbx

Proper recognition to the [Protein Data Bank](http://mmcif.wwpdb.org/docs/sw-examples/python/html/index.html) where this library for protein structures in the mmCIF format initially came from. We modified the original library to support python3. This fork is used by scripts in the HHsuite [on GitHub](https://github.com/soedinglab/hh-suite).

## Requirements
 * python3

## Installation

        mkdir build
        cd build

### For user specific installation:
        cmake -DUserInstallOption=ON ../
        make install

### For global installation (requires root rights):
        cmake ../
        sudo make install



