# UniLight
Synchronize Corsair CUE, Dell/Alienware LightFX/AlienFX, and/or Logitech Gaming LED devices with Windows accent/colorization color

## Demo
https://youtu.be/I3xfJtbLqgA

## Background
I have an Alienware 17R3 laptop and have been using AlienFX WinTheme to sync the color my LED's with the Windows 10 accent color. However, I just purchased a Logitech G502 Proteus Spectrum and wanted to have it work the same way. This inspired me to write a C++ application that accomplishes the same thing as AlienFX WinTheme but also adds support for Logitech RGB LED equipped devices.

## Usage
Simply launch UniLight and forget about it. Configure Windows to launch it at startup if you want.

UniLight appears as a system tray icon that looks like a color wheel, and listens for changes to accent color or other conditions that may affect LED color synchronization. On startup and whenever any relevant changes are detected, it calls the LightFX/AlienFX and Logitech Gaming LED APIs to set all RGB LEDs to the current accent color.

Hovering the mouse cursor over the UniLight tray icon will produce a tooltip containing status information, including the current and last accent colors, and whether they were successfully applied to Alienware and/or Logitech devices.

Right-clicking the tray icon will bring up a context menu with self-explanatory selections, while left-clicking performs a manual color synchronization.

## Troubleshooting
UniLight comes with DLLs for the various supported APIs. These are mainly included so that users without software from one or more of the supported vendors can still use UniLight. If you have trouble with the included DLLs, it's highly recommended that you try deleting/renaming the included DLLs for which you may have system-level counterparts installed.

Dell/Alienware LightFX/AlienFX DLLs are not included, because the fact that that SDK requires that I manually load the DLL anyway means that I can just disable support if the DLL is not available at the OS level.

## System Requirements
I'm not 100% sure about these. I tried to implement the API access in such a way that it will fail gracefully if a hardware vendor API is not supported on your system. UniLight will also attempt to re-apply the color on every color change, so that there is some hope of avoiding having to restart UniLight if relevant peripherals are (re)connected after UniLight has already been launched. I haven't tried to make it any more aggressive because I have to poll both APIs (neither provides a notification callback mechanism) and I don't want UniLight to have a noticeable performance impact on gaming or other tasks.

UniLight should load the AlienFX and/or Logitech Gaming LED DLLs that you have installed as part of Alienware Command Center (minimum version unknown; I'm currently on 4.5.19) and Logitech Gaming Software (version 8.55 or higher required for LED support), respectively. Also, the binary distribution of this program is 32-bit for maximum compatibility (I'm running it on 64-bit systems, so I know it works there).

As of version 1.1, UniLight is completely event-driven and no longer polls the Windows accent color on a timer. The result should be extremely minimal CPU usage.

## Tools used
This project was created with:
* Microsoft Visual Studio Community 2017: https://www.visualstudio.com/vs/community/
* Alienware AlienFX 1.0 SDK (formerly Dell LightFX): http://www.dell.com/support/home/us/en/19/drivers/driversdetails?driverId=T5GGP
* Corsair CUE SDK (Protocol version 4): http://forum.corsair.com/v3/showthread.php?t=156813
* Logitech LED Illumination SDK: https://www.logitechg.com/en-us/developers

## License
All code contained in this repository and binaries built from it are covered by the MIT open source license. See the LICENSE file for details. Usage of this code must be attributed to GitHub user HunterZ.

Included DLLs are owned by the hardware vendor companies (Corsair, Dell/Alienware, Logitech).
