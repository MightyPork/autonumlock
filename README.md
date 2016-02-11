AutoNumlock
===========

This script runs a loop, checking USB devices with `lsusb`.

When a USB keyboard is connected or disconnected, it enables or disables numlock.

The change happens only when the device is connected or disconnected, you can adjust numlock manually otherwise.

Example usage
-------------

- `$ autonumlock 045e:0783 0.5` - detect keyboard '045e:0783', poll every 500ms
- `$ autonumlock Genius` - detect any USB device with Genius in the `lsusb` line

You can use the config file to add extra commands, eg. xmodmap. The config file is created
after you run for the first time.

When AutoNumlock runs, you'll see something like this:

```none
$ autonumlock 1c4f:0002 5

AutoNumlock v.1.1.4

Creating config file in ~/.autonumlock for device "1c4f:0002", interval 5 seconds.

Configured keyboards:

 - "1c4f:0002"

Interval: 5 s

Test cmd: lsusb | grep -i -e "1c4f:0002"

Loop running...

External keyboard CONNECTED.
External keyboard DISCONNECTED.
External keyboard CONNECTED.

```

It's best to run it as an autostart application in your DE.


Help page
---------

```none
$ autonumlock -h

AutoNumlock v.1.1.4

Monitors devices & enables numlock when USB keyboard is connected.
Intended for laptops without a numeric block.

Usage:

autonumlock [-h|-v|-l] [<device>] [<interval>]
    <device> ...... device ID of your external keyboard (obtained with lsusb)
    <interval> .... number of seconds between checking (default: 1)
    -h ... help
    -v ... version
    -l ... try to find USB keyboards

After first successful start (with device id), a config file is created:
  /home/ondra/.autonumlock

The settings are then taken from the config file.
You can also configure multiple keyboards there.

```

Keyboard finder
---------------

Use the `-l` flag to list your connected USB keyboards.

It searches `/sys/bus/usb/devices/` for HID devices with the keyboard protocol.

```none
$ autonumlock  -l

AutoNumlock v.1.1.4

=== USB keyboard found ===
ID:   04f2:0111
Name: Chicony Electronics Co., Ltd KU-9908 Keyboard

=== USB keyboard found ===
ID:   1c4f:0002
Name: SiGma Micro Keyboard TRACER Gamma Ivory

```

The keyboard finder is based on [this code](http://serverfault.com/a/126325/255963) by Juliano.


Config file
-----------

Autonumlock will create a config file in `~/.autonumlock` after you run it with the device ID for the first time.

It looks something like this:

```bash
#!/bin/bash

###########################
# AutoNumlock config file #
###########################

# List of USB keyboards to check for.
# You can specify multiple IDs, separated by space.
# To get your keyboard ID, run `autonumlock -l`
devices=('<DEVICE>')

# Refresh interval (seconds)
# Length of sleep between USB device checks
sleeptime=<SLEEP>

# Called when keyboard is added
function on_connect {
	numlockx on
	# ... add your custom commands ...
}

# Called when keyboard is removed
function on_disconnect {
	numlockx off
	# ... add your custom commands ...
}

```
