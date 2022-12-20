CircuitPythonukiah
==================

.. image:: https://img.shields.io/github/actions/workflow/status/tekktrik/CircuitPythonukiah/build.yml?branch=main
   :target:  https://github.com/tekktrik/CircuitPythonukiah/actions
   :alt: Build CI status (main branch)

.. image:: https://img.shields.io/badge/OSHWA-US002130-blue
   :target: https://certification.oshwa.org/us002130.html
   :alt: OSHWA Certified

.. image:: https://img.shields.io/maintenance/yes/2022
   :target: https://github.com/tekktrik/CircuitPythonukiah/issues
   :alt: Maintained

The CircuitPythonukiah project

Setup
-----

Setting up the CircuitPythonukiah is simple!  Using a Mirco USB C cable, plug into
the microcontroller board (the square board on the front) and connect it to your
computer.  The device will show up as a USB drive labelled ``CIRCUITPY``.  In this
folder you'll find a file named ``secrets.py``, in which you'll need to add a few
pieces of information.  You can open up this file using any text editor.

The first bit of information needed is your Wi-Fi name and password, which the
CircuitPythonukiah will need toconnect to your network.  Please note that this must
be a 2.4 GHz network, as it cannot use a 5 GHz netork.  The other piece of information
needed is your ZIP code, which is required in order to grab the candle lighting times
for your location.  An example of this filled out looks like this:

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
CircuitPythonukiah base and connect the other end of the cable to a power source,
such as a common USB charger brick.

Configurable Settings
---------------------

The CircuitPythonukiah currently has two configurable settings in a file named
``settings.py`` relating to candle "burnout". This setting controls the behavior
of the device with respect to letting the LED candles go out after an amount of
time to simulate the behavior of regular candles.  This will also let you watch
the CircuitPythonukiah fully light up the following night.  If this setting is
off, the candles will stay on until the next candle light, at which point another\
LED will turn on.

The ``BURNOUT`` variable turns this setting on/off.  To this setting, change
the line to either:

``BURNOUT = True``

or

``BURNOUT = False``

The second, related configurable setting is ``HOURS_BEFORE_BURNOUT``, and it
controls how long the candles will stay on before turning off.  For example,
if you wanted the candles to stay on for 3 hours, you should have the following
settings:

.. code-block:: python

    BURNOUT = True
    HOURS_BEFORE_BURNOUT = 3

Please note the specific capitalization of variables and values!

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

* If it is before the start of the first Hanukkah light time, the device will not
  light up any LEDs until it's time, at which point the shamash LED and first
  candle will turn on, accompanied by a small rendition of "Maoz Tzur" depending
  on your sound muting settings.
* If the device is plugged in during the holiday within the configured burnout time
  of candle lighting time, it will immediately light up and play the song depending on
  your sound muting settings.
* If you plug it in between the end of this time and the next candle lighting
  time (so, "HOURS_BEFORE_BURNOUT" hours before a candle lighting), the device will
  not do anything until the next candle lighting.
* After the holiday ("HOURS_BEFORE_BURNOUT hours after candle light for "burnout" mode
  or 24 hours otherwise) all the LEDs will turn off and remain as such forever. This means
  you MUST replug it in every year.

It is worth mentioning that it currently finds the candle lighting times for the
current calendar year, which means the earliest you can plug it in and expect it
to function properly is January.  Hence, I recommend that like your other hanukkiahs
you only bring it out just for the holiday and unplug and store it otherwise.

Troubleshooting
---------------

If any point the CircuitPythonukiah cannot retrieve the time from the internet
as it operates, it is programed to quickly light up the LEDs repeatedly to
alert you of a problem.  This can be caused by a number of issues but a likely
cause is that your Wi-Fi network is down.  It is programmed to loop like this
forever, so if it does not persist after lighting up for only a few sequences,
it's possible that one of the services required by the CircuitPythonukiah was
temporarily down.  If all your Wi-Fi information is correct, you can try unplugging
it from the power source for a moment, and then replugging it in to have it
reconnect.

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
* If you do use or share this, share it with the same licensing!

This is to ensure that the project remains perpetually open source.
