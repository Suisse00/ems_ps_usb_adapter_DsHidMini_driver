# EMS PlayStation to USB

If you find reference to `Play.com, Inc.` or Windows show it up with something with the address like HID\VID_0B43&PID_0003 (or USB\VID_0B43&PID_0003) then this project is for you!

## Description

If you try to use the EMS PlayStation (1 & 2) to USB adapter on a recent machine (>= Windows 7) the provided driver may not allow Windows to detect your Playstation device as a joystick.

So here's an adaptation of [DsHidMini](https://github.com/ViGEm/DsHidMini) so that adapter can now show up in Windows!

This projet is focused on making dance pads (from Dance Dance Revolution) from PlayStation 2 to work again. So joysticks may not work properly (see [Limitations](#limitations)).

## How to install

It is similar to [DsHidMini's How to Install v2](https://vigem.org/projects/DsHidMini/How-to-Install/#version-2xx).

1. [Get the latest ems_dshidmini_v2.X.X.X.zip](https://github.com/suisse00/ems_ps_usb_adapter_DsHidMini_driver/releases).
2. Unzip the file.
3. [Make sure you know your architecture](https://vigem.org/research/How-to-check-architecture/).
4. Navigate to the directory created from the unzip then if your architecture is:
    - x86 then navigate into the `x86` directory
    - x64 then navigate into the `x64` directory (likely to be that option)
5. Right click on the `dshidmini.inf` file then select the `Install` option.
6. Windows Security should ask you to confirm you want to install the device software. You will need to accept by clicking the `Install` button.
7. You may need to reboot.
8. If you want to quickly test your Playstation device:
    1. Open the old `Control Panel`, `Hardware and Sound` (if you display categories), then the `Devices and Printers` options.
    2. You will see a joystick listed (regardless if the driver works or not). Right click on it, then select the `Game controller settings`.
    3. If everything is installed as it should, you should see two options listed since it is a 2 ports adapter. Guess which one is your controller is currently connected to. Double click on one of the option in the list.
    4. A new window should open up, click the `Test` tab.
    5. Use your controller to see a visual feedback of what you do.

## Limitations

Tests were made from the Windows built-in game controller preview using two SCPH-10010 (PlayStation Dual Shock 2); one included with a Play Station 2 and the other bought from a retail shop.

- Vibration feedback hasn't been added.
- Analog sticks don't work.
- Analog sticks buttons don't work.
- Some joystick just go nuts with buttons. They keep telling buttons are pressed when they aren't (This was from the joystick bought from a retailer).
