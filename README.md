AutoNumlock
===========

This script runs a loop, checking USB devices with `lsusb`, and grepping it.

When a device matching the given identifier is found, numlock is enabled, otherwise it's disabled.autonumlock 045e:0783 0.5

The change happens only when the device is connected or disconnected, you can adjust numlock manually otherwise.

```none
AutoNumlock v.1.0

Script for watching for external keyboard, and enabling numlock when found.
Intended for use with laptops that lack numeric block on internal keyboard.

USAGE: autonumlock [-h] [-v] <device> [<interval>]
    <device> ...... device ID of your external keyboard (obtained with lsusb)
    <interval> .... number of seconds between checking (default: 1)
    -h ... help
    -v ... version
```

Example usage
-------------

- `$ autonumlock 045e:0783 0.5` ... identifier from lsusb
- `$ autonumlock Genius` ... Genius keyboard (part of line in lsusb, for grep)
