Environment
==============================================

Folder structure
----------------------------------------------

It is assumed that the following structure is placed directly in the user folder. For OS X this is denoted by ~. 

This repository only contains the workspace folder (named workspace_DDS below). Everything else needs to be created
first by installing the DDS libraries. This can be done by following the instructions from eProsima. This link shows
how to build it from source on OS X: https://fast-dds.docs.eprosima.com/en/latest/installation/sources/sources_mac.html
Please note that these instructions are slightly outdated since OS X default terminal switched from bash to z shell.
Otherwise the instructions were still successfully followed as of 20th of January 2024.

Once the installation is done you can clone this repository into the Fast-DDS folder. The workspace folder 
(workspace_DDS) can have any name. The test1 files are example files that can be used to build a working example 
of DDS publisher and subscriber.

::

  ~
  └── Fast-DDS
      ├── build
      │   └── ...
      ├── Fast-CDR
      │   └── ...
      ├── Fast-DDS
      │   └── ...
      ├── foonathan_memory_vendor
      │   └── ...
      ├── install
      │   ├── setup.zsh
      │   └── ...
      ├── log
      │   └── ...
      ├── src
      │   └── ...
      ├── workspace_DDS
      │   ├── build
      │   │   └── ...
      │   ├── src
      │   │   ├── <idl_file>.idl
      │   │   ├── <publisher>.cpp
      │   │   ├── <subscriber>.cpp
      │   │   └── ...
      │   ├── .gitignore
      │   ├── CMakeLists.txt
      │   ├── LICENSE
      │   ├── readme.rst
      │   └── workspace_DDS.code-workspace
      └── fastrtps.repos


Running the terminal
-----------------------

Every time a terminal is started and the it is desired to build files with DDS dependencies,
first rung the following ``% source ~/Fast-DDS/install/setup.zsh`` 

Building the code
#######################

All of the following lines reference the folder ``.`` to the current workspace folder 
(not to the Fast-DDS folder).

* open terminal in the workspace folder and run ``% source ~/Fast-DDS/install/setup.zsh``

* create the build directory ``% mkdir build``
  
* switch to the ``./src`` modify or replace the ``.idl`` file accordingly

* generate new files using FastDDS-Gen inside the ``./src`` folder

  * ``% <path/to/Fast DDS-Gen>/scripts/fastddsgen <name_of_idl_file>.idl``
  
  * remark: all files starting with ``test`` except for the test.idl file which are located in the 
    ``./src`` folder are ignored by git and will not be synced

* Modify the ``CMakeLists.txt`` file if necessary. It is currently configured to include 
  all from the ``./src`` directory and to create a publisher and a subscriber based on the 
  ``./src/publisher.cpp`` and the ``./src/subscriber.cpp`` files

* Modify the ``publisher.cpp`` and ``subscriber.cpp`` files. make sure to update the include
  files if you have changed the ``.idl`` file name.

* Switch to the ``./build`` directory and run the following commands

  * ``% cmake ..``
  
  * ``% cmake --build .``
  
  * This generates two executables: publisher and subscriber inside the build folder

* Open two terminals and run these two executables, each in its own terminal

  * ``% ./subscriber``

  * ``% ./publisher``