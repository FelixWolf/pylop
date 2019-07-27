# Pylop

Single file python script executable maker thingermcbob.

Python version: 3.8

## About

This is designed to do the following:
1. Take your python script(s) as a module
2. Put it in a "zip"
3. Append it to a executable
4. Now you have a single executable file that you can send to people without having them install python

## Method

1. Built "Pylop" template executable will search the end of it's binary for a 4 byte magic number.
2. If magic number is found, seek back 4 bytes, this is the absolute position where the "zip" containing the files to load.
3. Seek to said position and read 4 bytes, this is the length of the zip.
4. Add a hook to the importlib to manage loading from this embedded zip.

## Planned features

* meta.info embedded in zip, allow for changing of various executable parameters(Hide or show console window, etc)

## Requirements

Visual Studio 2013 (or newer) or Linux with GCC. MinGW is sadly not supported, and clang has not been tested.

## Download

Don't forget to initialise and update the submodules! The cpython is +200MB so it may take some time to during `git submodule update`.

```
git clone https://github.com/FelixWolf/pylop
cd pylop
git submodule init
git submodule update --progress
```

## Build using Visual Studio on Windows

**Please note:** that you have to explicitly specify `CMAKE_BUILD_TYPE`. If you specify Debug, then you must use Debug in your Visual Studio. You won't be able to change to Release using the dropdown list in the main menu. Python will be build using the `CMAKE_BUILD_TYPE` flag regarding the chosen configuration in Visual Studio. To change from Debug to Release, re-run the cmake and set the `CMAKE_BUILD_TYPE` to Release.

```
cd python-embedded-example-project 
mkdir build
cd build
cmake .. -G "Visual Studio 15 2017" -DCMAKE_BUILD_TYPE=Debug
```

Then open the generated solution file "Pylop.sln" in the build folder. You should see the following projects:

* **ALL_BUILD** - Building this will build all projects
* **CPYTHON** - The embedded python project
* **PYBIND** - The pybind11 library for binding
* **PythonEmbeddedExample** - This is the example project

Build the Pylop and then use `generateApp.py --binary=pylop --library=lib.zip --source=whatever` from command line.

## Build using GCC on Linux

```
cd pylop
mkdir build
cd build
cmake .. -DCMAKE_BUILD_TYPE=Debug
```

Then build the example by running:

```
make
```

The `Pylop` executable will be generated.

## Changing python version

This project is using the latest stable version of python avaliable.
At the time of writing, this is version `3.8`.
If you want to change python version, change the `branch` in `.gitmodules` to `branch = 3.7` or any other version. See available branches at: <https://github.com/python/cpython>

## Credits

(These are credits, this does not mean they endorse this project)

* [Matusnovak](https://github.com/matusnovak) for the [Python embedded example project](https://github.com/matusnovak/python-embedded-example-project) which really helped me get a head start on embedding python when I had no idea what I was doing(I still don't know really what I am doing!).
* Everyone at [Python Software Foundation](https://python.org) for their amazing work on the Python programming language.
* God, Satan, Talos, or whatever deity or atoms that collided to create the universe.
* Mankind for creating frustrations in coding.
