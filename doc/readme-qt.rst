litecoinplus-qt: Qt4 GUI for LitecoinPlus
===============================

Build instructions
===================

Debian
-------

First, make sure that the required packages for Qt4 development of your
distribution are installed, for Debian and Ubuntu these are:

::

    apt-get install qt4-qmake libqt4-dev build-essential libboost-dev libboost-system-dev \
        libboost-filesystem-dev libboost-program-options-dev libboost-thread-dev \
        libssl-dev libdb4.8++-dev

if you get an error that libdb4.8++-dev cannot be located, please do the following:

::

    sudo add-apt-repository ppa:bitcoin/bitcoin
    sudo apt-get update

then re-do the first step to install all dependencies. Then, execute the following:

::

    qmake
    make

Alternatively, install Qt Creator and open the `litecoinplus.pro` file.

An executable named `litecoinplus-qt` will be built.


Windows
--------

Windows build instructions:

- Download the `QT Windows SDK`_ and install it. You don't need the Symbian stuff, just the desktop Qt.

- Download and extract the `dependencies archive`_  [#]_, or compile openssl, boost and dbcxx yourself.

- Copy the contents of the folder "deps" to "X:\\QtSDK\\mingw", replace X:\\ with the location where you installed the Qt SDK. Make sure that the contents of "deps\\include" end up in the current "include" directory.

- Open the .pro file in QT creator and build as normal (ctrl-B)

.. _`QT Windows SDK`: http://qt.nokia.com/downloads/sdk-windows-cpp
.. _`dependencies archive`: https://download.visucore.com/bitcoin/qtgui_deps_1.zip
.. [#] PGP signature: https://download.visucore.com/bitcoin/qtgui_deps_1.zip.sig (signed with RSA key ID `610945D0`_)
.. _`610945D0`: http://pgp.mit.edu:11371/pks/lookup?op=get&search=0x610945D0


Mac OS X
--------

- Download and install the `Qt Mac OS X SDK`_. It is recommended to also install Apple's Xcode with UNIX tools.

- Download and install `MacPorts`_.

- Execute the following commands in a terminal to get the dependencies:

::

	sudo port selfupdate
	sudo port install boost db48 miniupnpc

- Open the .pro file in Qt Creator and build as normal (cmd-B)

.. _`Qt Mac OS X SDK`: http://qt.nokia.com/downloads/sdk-mac-os-cpp
.. _`MacPorts`: http://www.macports.org/install.php


Build configuration options
============================

UPNnP port forwarding
---------------------

To use UPnP for port forwarding behind a NAT router (recommended, as more connections overall allow for a faster and more stable litecoinplus experience), pass the following argument to qmake:

::

    qmake "USE_UPNP=1"

(in **Qt Creator**, you can find the setting for additional qmake arguments under "Projects" -> "Build Settings" -> "Build Steps", then click "Details" next to **qmake**)

This requires miniupnpc for UPnP port mapping.  It can be downloaded from
http://miniupnp.tuxfamily.org/files/.  UPnP support is not compiled in by default.

Set USE_UPNP to a different value to control this:

+------------+--------------------------------------------------------------------------+
| USE_UPNP=- | no UPnP support, miniupnpc not required;                                 |
+------------+--------------------------------------------------------------------------+
| USE_UPNP=0 | (the default) built with UPnP, support turned off by default at runtime; |
+------------+--------------------------------------------------------------------------+
| USE_UPNP=1 | build with UPnP support turned on by default at runtime.                 |
+------------+--------------------------------------------------------------------------+

Notification support for recent (k)ubuntu versions
---------------------------------------------------

To see desktop notifications on (k)ubuntu versions starting from 10.04, enable usage of the
FreeDesktop notification interface through DBUS using the following qmake option:

::

    qmake "USE_DBUS=1"

Generation of QR codes
-----------------------

libqrencode may be used to generate QRCode images for payment requests. 
It can be downloaded from http://fukuchi.org/works/qrencode/index.html.en, or installed via your package manager. Pass the USE_QRCODE 
flag to qmake to control this:

+--------------+--------------------------------------------------------------------------+
| USE_QRCODE=0 | (the default) No QRCode support - libarcode not required                 |
+--------------+--------------------------------------------------------------------------+
| USE_QRCODE=1 | QRCode support enabled                                                   |
+--------------+--------------------------------------------------------------------------+

