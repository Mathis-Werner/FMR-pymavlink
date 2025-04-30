<a id="readme-top"></a>
<!-- PROJECT SHIELDS -->
<!--
*** I'm using markdown "reference style" links for readability.
*** Reference links are enclosed in brackets [ ] instead of parentheses ( ).
*** See the bottom of this document for the declaration of the reference variables
*** for contributors-url, forks-url, etc. This is an optional, concise syntax you may use.
*** https://www.markdownguide.org/basic-syntax/#reference-style-links
-->



<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://github.com/Mathis-Werner/FMRCompanion">
    <img src="images/FMR-logo-blue.jpg" alt="Logo" width="200" height="200">
  </a>

<h3 align="center">FMRCompanion</h3>
</div>


<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li><a href="#about-the-project">About The Project</a>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#Setting up the RasPi">Setting up the RasPi</a></li>
        <li><a href="#Setup in QGroundcontrol">Setup in QGroundcontrol</a></li>
      </ul>
    </li>
    <li><a href="#Code Overview">Code Overview</a></li>
    <li><a href="#Required python packages">Required python packages</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
  </ol>
</details>



<!-- ABOUT THE PROJECT -->
## About The Project

This project contains a custom pymavlink fork including messages definitions in the common message set required to send custom messages to the pixhawk flightcontroller. 

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- Using the libary -->
## Using the libary

After cloning the repository in the desired location and installing the python packages in the section below the libary can be used like the default version of pymavlink as specified in the FMRCompanion repo.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- Development -->
## Developement

The common.py generated as explained in the corresponding FMR-mavlink repo must be copyed so that it replaces the common.py under dialects\v10

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- Required python packages -->
## Required python packages

* lxml>=3.6.0
* future>=0.15.2
* wheel>=0.37.1

<p align="right">(<a href="#readme-top">back to top</a>)</p>


<!-- LICENSE -->
## License

Distributed under the project_license. See `LICENSE.txt` for more information.

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- CONTACT -->
## Contact

Mathis Werner - wer.mathis@gmail.com

Project Link: [https://github.com/Mathis-Werner/FMR-pymavlink](https://github.com/Mathis-Werner/FMR-pymavlink)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

[![Build Status](https://travis-ci.org/ArduPilot/pymavlink.svg?branch=master)](https://travis-ci.org/ArduPilot/pymavlink)
# Pymavlink Original Doc
This is a Python implementation of the MAVLink protocol.
It includes a source code generator (generator/mavgen.py) to create MAVLink protocol implementations for other programming languages as well.
Also contains tools for analyzing flight logs.

# Documentation

Please see http://ardupilot.org/dev/docs/mavlink-commands.html for mavlink command reference.

For realtime discussion please see the pymavlink [Gitter channel](https://gitter.im/ArduPilot/pymavlink)

Examples can be found [in the repository](examples/) or in the [ArduSub book](https://www.ardusub.com/developers/pymavlink.html)


# Installation 

Pymavlink supports both Python 2 and Python 3.

The following instructions assume you are using Python 3 and a Debian-based (like Ubuntu) installation.

.. note::

   pymavlink assumes the command "python" is in your path.  Your distribution may provide a package such as "python-is-python3" to ensure that "python" is in your path.

## Dependencies

Pymavlink has several dependencies :

    - [future](http://python-future.org/) : for Python 2 and Python 3 interoperability
    - [lxml](http://lxml.de/installation.html) : for checking and parsing xml file 

Optional :

    - numpy : for FFT
    - pytest : for tests

### On Linux

lxml has some additional dependencies that can be installed with your package manager (here with `apt-get`) :

.. note::

   If you continue to use Python 2 you may need to change package names here (e.g. python3-numpy => python-numpy)

```bash
sudo apt-get install libxml2-dev libxslt-dev
```

Optional for FFT scripts and tests:

```bash
sudo apt-get install python3-numpy python3-pytest
```

Using pip you can install the required dependencies for pymavlink :

```bash
sudo python -m pip install --upgrade future lxml
```

### On Windows

Use pip to install future as for Linux.
Lxml can be installed with a Windows installer from here : https://pypi.org/project/lxml


## Installation

### For users

It is recommended to install pymavlink from PyPI with pip, that way dependencies should be auto installed by pip.

```bash
sudo python -m pip install --upgrade pymavlink
```

#### Mavnative

Starting from September 2022, mavnative, a C extension for parsing mavlink, was deprecated and removed. Mavnative developpement was stalled for long time, it only supports MAVLink1 and doesn't get any fix on the protocol.

### For developers

From the pymavlink directory, you can use :

```bash
sudo MDEF=PATH_TO_message_definitions python -m pip install . -v
```

Since pip installation is executed from /tmp, it is necessary to point to the directory containing message definitions with MDEF. MDEF should not be set to any particular message version directory but the parent folder instead. If you have cloned from mavlink/mavlink then this is ```/mavlink/message_definitions``` . Using pip should auto install dependencies and allow you to keep them up-to-date. 

Or:

```bash
sudo python setup.py install
```

### Ardupilot Custom Modes

By default, `pymavlink` will map the Ardupilot mode names to mode numbers per the definitions in the [ardupilotmega.xml](https://mavlink.io/en/messages/ardupilotmega.html#PLANE_MODE) file. However, during development, it can be useful to add to or update the default mode mappings.

To do this:
  - create a folder named `.pymavlink` in your home directory (i.e. `$HOME` on Linux, `$USERPROFILE` on Windows); and
  - add a JSON file called `custom_mode_map.json` to this new `.pymavlink` folder.

The JSON file is a dictionary that maps vehicle [`MAV_TYPE`](https://mavlink.io/en/messages/minimal.html#MAV_TYPE) value to a dictionary of mode numbers to mode names. An example that duplicates the existing mapping for `MAV_TYPE_FIXED_WING` (`enum` value of `1`) vehicles is as follows:
```json
{
    "1": {
        "0":  "MANUAL",
        "1":  "CIRCLE",
        "2":  "STABILIZE",
        "3":  "TRAINING",
        "4":  "ACRO",
        "5":  "FBWA",
        "6":  "FBWB",
        "7":  "CRUISE",
        "8":  "AUTOTUNE",
        "10": "AUTO",
        "11": "RTL",
        "12": "LOITER",
        "13": "TAKEOFF",
        "14": "AVOID_ADSB",
        "15": "GUIDED",
        "16": "INITIALISING",
        "17": "QSTABILIZE",
        "18": "QHOVER",
        "19": "QLOITER",
        "20": "QLAND",
        "21": "QRTL",
        "22": "QAUTOTUNE",
        "23": "QACRO",
        "24": "THERMAL"
    }
}
```

This `custom_mode_map.json` file can be used to:
  - change the display name of an existing mode (e.g. change `"TAKEOFF"` to `"LAUNCH"`);
  - add a new mode (e.g. add `"25": "NEW_MODE"`); and
  - add a mapping for an unsupported vehicle type (e.g. add a mapping for `MAV_TYPE_AIRSHIP` (`enum` value of `7`) vehicles).

Notes:
  - Whilst the `MAV_TYPE` and mode numbers are integers, they need to be defined as `string`s in the JSON file, as raw integers can't be used as dictionary keys in JSON.
  - This feature _updates_ the default definitions. You can use it to change the name-to-number mapping for a mode, but you completely can't remove an existing mapping.


# License
---------

pymavlink is released under the GNU Lesser General Public License v3 or later.

The source code generated by generator/mavgen.py is available under the permissive MIT License.
