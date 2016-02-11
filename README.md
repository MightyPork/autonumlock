AutoNumlock
===========

This script runs a loop, checking USB devices with `lsusb`, and grepping it.

When a device matching the given identifier is found, numlock is enabled, otherwise it's disabled.

The change happens only when the device is connected or disconnected, you can adjust numlock manually otherwise.

```none
AutoNumlock v.1.1.3

Script for watching for external keyboard, and enabling numlock when found.
Intended for use with laptops that lack numeric block on internal keyboard.

USAGE: autonumlock [-h|-v] [<device>] [<interval>]
    <device> ...... device ID of your external keyboard (obtained with lsusb)
    <interval> .... number of seconds between checking (default: 1)
    -h ... help
    -v ... version

Options override values from config file:
  ~/.autonumlock
The config file is created after first successful start (with device id)

```

Example usage
-------------

- `$ autonumlock 045e:0783 0.5` ... identifier from lsusb
- `$ autonumlock Genius` ... Genius keyboard (part of line in lsusb, for grep)

You can use the config file to add extra commands, eg. xmodmap.

When AutoNumlock runs, you'll see something like this (using the config file):

```none
$ autonumlock 

Keyboards
 - "1c4f:0002"

Interval: 10 s

Test cmd: lsusb | grep -e "1c4f:0002"

--- checking started ---

External keyboard DETECTED, enabling numlock.
CONNECT

```

It's best to run it as an Autostart application, eg. in Xfce4 using the "Session and Startup" settings page.

