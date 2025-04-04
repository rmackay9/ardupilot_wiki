.. _building-setup-mac:

=========================================
Setting up the Build Environment (MacOSX)
=========================================

This article shows how to manually setup a minimal build environment on MacOS (ver 10.6 onwards).

..  youtube:: wLK2wLwEXm4
    :width: 100%


There is a `pre-built script  <https://github.com/ArduPilot/ardupilot/blob/master/Tools/environment_install/install-prereqs-mac.sh>`__ that will install these pre-requisites.

How to use it, cd to your ardupilot directory, and execute:

::

    sh ./Tools/environment_install/install-prereqs-mac.sh


Setup steps
-----------

#. MacOS will alert you when you enter a command in the terminal that requires Xcode Command Line Tools. You can also install Xcode Command Line Tools manually

   ::
   
       xcode-select --install

#. Install `Homebrew <http://brew.sh>`__ for MacOS (Homebrew is a respected package manager for MacOS)

   ::
   
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
 
#. Install the following packages using brew

   ::

       brew update
       brew install genromfs
       brew install gcc-arm-none-eabi

#. Install the latest version of awk using brew (make sure
   **/usr/local/bin** takes precedence in your path):

   ::

       brew install gawk

#. Install *pip* and *pyserial* using the following commands:

   ::

       sudo easy_install pip
       sudo pip install pyserial future empy
       
   ::
   
       ** Starting with MacOS Mojave (10.14.x) you might want to install the SDK headers
       
       open /Library/Developer/CommandLineTools/Packages/macOS_SDK_headers_for_macOS_10.14.pkg


#. Follow the :ref:`MAVProxy documentation <mavproxy:mavproxy-downloadinstallmac>` if you plan to use the simulator.

Now you should be able to build with waf as described in `BUILD.md <https://github.com/ArduPilot/ardupilot/blob/master/BUILD.md>`__.

Additional Steps for macOS mojave
---------------------------------
Due to some changes binutils installed via brew have stopped working for macOS mojave leading to crashing builds. So if installed, remove via following command:

::

    brew uninstall binutils

Also you will need to install the c++ include headers to /usr/include to do that. Run the following in commandline and follow the installation routine:

::

    open /Library/Developer/CommandLineTools/Packages/macOS_SDK_headers_for_macOS_10.14.pkg

Cleaning
--------

If there have been updates to some git submodules you may need to do a full clean build. To do that use:

::

    ./waf distclean

Commands `clean` and `distclean` can be used to clean the objects produced by the build.
`clean` keeps the configure information, cleaning only the objects for the current board. `distclean` cleans everything for every board, including the saved configure information.

Follow the instructions for `build <https://github.com/ArduPilot/ardupilot/blob/master/BUILD.md>`__ .
