CircuitPythonukiah
==================

The CircuitPythonukiah project

Setup
-----

Setting up the CircuitPythonukiah is simple!  Using a Mirco USB C cable, plug into
the microcontroller board (the square board on the front) and connect it to your
computer.  The device will show up as a USB drive labelled ``CIRCUITPY``.  In this
folder you'll find a file named ``secrets.py``, in which you'll need to add a few
pieces of information.

The first is your Wi-Fi name and password, which the
CircuitPythonukiah will need to connect to your network.  The other pieec of
information is your ZIP code, which is needed in order to grab the candle lighting
times for your location.  An example of this filled out looks like this:

.. code-block:: python

    # SPDX-FileCopyrightText: 2022 Alec Delaney
    #
    # SPDX-License-Identifier: GPL-3.0-or-later

    """
    `secrets.py`
    ============

    Secret information for your menorah

    * Author: Alec Delaney

    """

    secrets = {
        "ssid": "DreidelNetwork",
        "password": "bagels&lox18",
    }
    location = {
        "zipcode": "05873",
    }

Notice that everything is wrapped in quotation marks and that many lines end
with a comma.  Make sure that you keep it like that, or the CircuitPythonukiah
won't function properly!

Additionally, there is a file named ``settings.py`` that contains optional
settings you can configure.  See the section below for what these settings do.

After saving these file with your information, you can unplug from the
microcontroller and use the USB C cable to plug into the back of the
CircuitPythonukiah and connect the other end of the cable to a power source,
such as a common USB charger brick.

Configurable Settings
---------------------

The CircuitPythonukiah currently has one configurable setting called "burnout".
This setting controls the behavior of the device with respect to letting the
LED candles go out 12 hours after lighting, to simulate the behavior of regular
candles.  This will also let you watch the CircuitPythonukiah fully light up
the following night.  If this setting is off, the candles will stay on until
the next candle light, at which point another LED will turn on.

To change this settings, change the line to ``BURNOUT = True`` or
``BURNOUT = False`` accordingly.  Please note the specific capitalization!

Functionality
-------------

When properly configured, the CircuitPythonukiah will go through a connection
sequence as it connects to your Wi-Fi network.  During this sequence, it will
slowly light up the candles sequentially to let you know that it is operational.
If this turns into a flashing of the lights, please make sure your Wi-Fi
information is correct.  Additionally, try unplug and reconnecting the
CircuitPythonukiah to the power source to have it retry the connection.

If conenction is successful, the CircuitPythonukiah should immediately begin
operating based on the current time relative to candle light.

* If it is before the start of the first Hanukkah light time the device will not
  light up any LEDs until it's time, at which point the shamash LED and first
  candle will turn on, accompanied by a small rendition of "Maoz Tzur" depending
  on your sound muting settings.
* If the device is plugged in during the holiday within 12 hours of candle
  lighting time, it will immediately light up and play the song depending on
  your sound muting settings.
* If you plug it in between the end of this time and the next candle lighting
  time (so, 12 hours before a candle lighting), the device will do anything
  until the next candle lighting.
* After the holiday (12 hours after candle light for "burnout" mode or 24 hours
  otherwise) all the LEDs will turn off and remain as such forever. This means
  you MUST replug it in every year.

It is worth mentioning that it currently finds the candle lighting times for the
current calendar year, which means the earliest you can plug it in and expect it
to function properly is January.  Hence, I recommend that like your other hanukkiahs
you only bring it out just for the holiday and unplug and store it otherwise.

Troubleshooting
---------------

If any point the CircuitPythonukiah cannot retrieve the time from the internet
as it operates, it is programed to quickly light up the LEDs sequentially to
alert you of a problem.  This can be caused by a number of issues but a likely
cause is that your Wi-Fi network is down.  It is programmed to loop like this
forever, so if it does not persist after lighting up for only a few sequences,
it's possible that one of the services required by the CircuitPythonukiah was
temporarily down.

Build, Learn, Share
-------------------

Please feel free to hack away at this project!  It was built with love, and
you are free to make any changes or improvements you want if you wish to.  I
would love to hear about or see any awesome modifications you make.  Whether
the CircuitPythonukiah is a new staple of the holidays for you, or an
opportunity to learn a new skill, I just hope you love it as much as I did
making it.

The only thing I ask is that if you want to distribute those changes, you
follow the licensing I've set up for the project.  You can find those in
the public project repositories, and while I am not a lawyer, essentially:

* Do what you want with this!
* You can share these designs and code or any modifications!
* If you do share, please share it with the same licensing as open source!

This is to ensure that the project remains perpetually open source.
