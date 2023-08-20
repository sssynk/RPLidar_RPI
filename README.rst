RPLidar for the Raspberry Pi
============

This version is made to fix any issues when running this library on a Raspberry Pi.

When running other versions, I had import errors and many errors with descriptors. This should fix all of them.

Introduction
============

.. image:: https://readthedocs.org/projects/adafruit-circuitpython-rplidar/badge/?version=latest
    :target: https://docs.circuitpython.org/projects/rplidar/en/latest/
    :alt: Documentation Status

.. image:: https://raw.githubusercontent.com/adafruit/Adafruit_CircuitPython_Bundle/main/badges/adafruit_discord.svg
    :target: https://adafru.it/discord
    :alt: Discord

.. image:: https://github.com/adafruit/Adafruit_CircuitPython_RPLIDAR/workflows/Build%20CI/badge.svg
    :target: https://github.com/adafruit/Adafruit_CircuitPython_RPLIDAR
    :alt: Build Status

.. image:: https://img.shields.io/badge/code%20style-black-000000.svg
    :target: https://github.com/psf/black
    :alt: Code Style: Black

.. Provide a convenient interface to the Slamtec RPLidar.

Dependencies
=============

To install:

cd to the directory and run this command:
`sudo python3 setup.py install`
(it will install as adafruit_rplidar!)

This driver depends on:

* `pySerial <https://github.com/pyserial/pyserial>`_

Designed to work with python3. For the CircuitPython version, please check the Adafruit version!

Usage Example
=============

- THIS INSTALLS AS adafruit_rplidar!

.. code-block:: python

    import os
    from math import floor
    from adafruit_rplidar import RPLidar


    # Setup the RPLidar
    PORT_NAME = '/dev/ttyUSB0'
    lidar = RPLidar(None, PORT_NAME, timeout=3)

    # used to scale data to fit on the screen
    max_distance = 0

    def process_data(data):
        print(data)

    scan_data = [0]*360

    try:
    #    print(lidar.get_info())
        for scan in lidar.iter_scans():
            for (_, angle, distance) in scan:
                scan_data[min([359, floor(angle)])] = distance
            process_data(scan_data)

    except KeyboardInterrupt:
        print('Stopping.')
    lidar.stop()
    lidar.disconnect()


Documentation
=============

There are no official docs for this version, but everything except motor speed should work the same as below.

API documentation for this library can be found on `Read the Docs <https://docs.circuitpython.org/projects/rplidar/en/latest/>`_.

For information on building library documentation, please check out `this guide <https://learn.adafruit.com/creating-and-sharing-a-circuitpython-library/sharing-our-docs-on-readthedocs#sphinx-5-1>`_.

Contributing
============

Contributions are welcome! Please read our `Code of Conduct
<https://github.com/adafruit/Adafruit_CircuitPython_RPLIDAR/blob/main/CODE_OF_CONDUCT.md>`_
before contributing to help this project stay welcoming.
