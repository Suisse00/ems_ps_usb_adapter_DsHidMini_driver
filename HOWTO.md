# How to create the driver package

## Get latest DsHidMini driver

1. [Download the latest zip from the DsHidMini github](https://github.com/ViGEm/DsHidMini/releases). \
The INF has been created based on https://github.com/ViGEm/DsHidMini/releases/tag/v2.2.282.0. So it is likely to work only with the v2.
2. Unzip it
3. We will only need:
    - x86\dshidmini\LICENSE
    - x86\dshidmini\dshidmini.dll
    - x64\dshidmini\LICENSE
    - x64\dshidmini\dshidmini.dll
4. I then created a new directory (somewhere on your computer) where I moved AND renamed the dshidmini directories to their architecture. \
TLDR: `x86\dshidmini` become `x86` and `x64\dshidmini` become `x64`.

## Get the latest version of this repository

1. [Download the latest zip from this repository](https://github.com/suisse00/ems_ps_usb_adapter_DsHidMini_driver/releases)
2. Unzip it into the new directory you created from the section above. You should see a `dshidmini.inf` file within your `x86` and `x64` directories with `dshidmini.dll`.

## Get tools

As per the [WDK download page](https://docs.microsoft.com/en-us/windows-hardware/drivers/download-the-wdk) you will need:

- Visual Studio
- Windows SDK (may be installed trought Visual Studio)
- Windows WDK

## Sign the thing

1. Open a `Developer Command Prompt for VS` from your start menu as an administrator.
2. Navigate to the new directory you created with the simplified DsHidMini directories.
3. Execute `Inf2Cat.exe /driver:x86 /os:Vista_X86,Server2008_X86,7_X86,8_X86,6_3_X86,10_X86`
4. Execute `Inf2Cat.exe /driver:x64 /os:Vista_X64,Server2008_X64,7_X64,Server2008R2_X64,8_X64,Server8_X64,6_3_X64,Server6_3_X64,10_X64`
5. Execute `makecert -r -pe -a sha512 -n "CN=LazyNameOfWhoWillSign" -eku 1.3.6.1.5.5.7.3.3 -sv CodeSigning.pvk CodeSigning.cer`. \
Technically should be done once for all releases
6. Excute `pvk2pfx.exe -pvk CodeSigning.pvk -spc CodeSigning.cer -pfx CodeSigning.pfx`
7. Execute `certmgr /add CodeSigning.cer /s /r localMachine root` (this is the part that need to be administrator) \
Technically should be done once for all releases
8. Execute `Signtool sign /v /fd sha512 /f CodeSigning.pfx /t http://timestamp.digicert.com x86\dshidmini.cat x64\dshidmini.cat`.
9. Create the final release; zip everything in the current directory your prompt is at, except all `CodeSigning` files.
