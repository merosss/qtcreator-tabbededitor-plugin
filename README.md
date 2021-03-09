# Qt Creator Tabbed Editor Plugin

The aim of this plugin is to provide a tab-based experience in [Qt Creator](http://qt-project.org/wiki/Category:Tools::QtCreator). Since this project has never been updated since 2015 I'm making un updated version, with complete compile and install instructions, compliant to the most recent Qt Libraries and Qt Creator versions. This guide is meant mainly for Ubuntu users who installed the latest Qt Creator version from the [Qt website](https://www.qt.io/download-qt-installer), and not from the Ubuntu Store. Some steps may vary on different setups.

## Compiling the package

### Identify Qt Creator version and download the source code

1. To compile the package you firstly need to check your Qt Creator version from *"Help > About Qt Creator..."* (this package, for example, is targeting Qt Creator 4.14.1).

2. Then go to the official [Qt Creator repository](https://github.com/qt-creator/qt-creator) and download the branch corresponding your version (click on the `master` dropdown menu and check fot it in the Tags section.

### Clone the repository and adjust variables

After cloning the package you will need to edit the project build variables file to find your sources and libraries.

1. Go to **Progject > Build Environment** and add the following variables:
  - QTC_BUILD: `*your-Qt-Creator-install-folder*/Tools/QtCreator`.
  - QTC_SOURCE: The source code folder your downloaded in the previous step.

2. Build project

### Known issues

#### Library Linking

For some reasons unkown to my knowledge, the linker was not able to link the libraries found in *Qt/Tools/QtCreator/lib/qtcreator*, with the compile error:

```
/usr/bin/ld: cannot find -lQtcSsh
/usr/bin/ld: cannot find -lAggregation
/usr/bin/ld: cannot find -lExtensionSystem
/usr/bin/ld: cannot find -lUtils
/usr/bin/ld: cannot find -lKSyntaxHighlighting
```

To fix this problem I had to manually rename these libraries, removing the trailing **.4** in the name (for example *libQtcSsh.so.4* to *libQtcSsh.so*). I am sure there is another correct approach to solve this issue but I was unable to find one, any help is appreciated.

#### Dependencies not found at Qt Creator Startup

If you get the error of some Qt Dependencies not found, it is highly probable that you downloaded a mismatching version of the Qt Creator Sources (for example the master branch). To check if your branch is correct look inside the **qtcreator_ide_branding.pri** file, and check if the `QT_CREATOR_VERSION` variable, and the following ones are correct.

## Copyright / License

Copyright (C) 2021 Francesco Wanderlingh.

This software is available under the terms of the GNU Lesser General Public License version 3 (LGPLv3).

This project is a fork of [QtCreator Tabbed Editor Plugin](https://github.com/trollixx/qtcreator-tabbededitor-plugin) by Oleg Shparber.
