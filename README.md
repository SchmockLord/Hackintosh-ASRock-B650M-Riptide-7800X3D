# Hackintosh-ASRock-B650M-Riptide-7800X3D

![Thumbnail](Docs/Thumbnail.png)

# Current macOS

Current Version: macOS Ventura 13.3

# Hardware
- CPU: AMD Ryzen 7 7800X3D
- Board: ASRock B650M Riptide
- RAM: 32 GB (2x16GB) Kingston DDR5 6000Mhz CL32
- GPU: MSI Gaming Trio X 6900 XTX
- PSU: Corsair SF750
- Case: Asus AP201 (Micro-ATX)
- Wifi/BT: not yet

# Working
- CPU Power Management
- USB Ports
- Sleep/Wake
- Wifi/BT

# Not working
iGPU, but this is common. You should disable it in BIOS or via Device Properties just for macOS.

# BIOS Settings
You can use the default settings. But disable the iGPU. 

Appart from that, no change required. Above 4G Decording etc. are all already Enabled.

I also let Fast Boot Enabled, no issues so far.

Only if you need Secure Boot (Enable Secure Boot, Secure Boot Mode to Custom and then in the Key Management all .efi files in your EFI-folder need to be enrolled/whitelisted with "Enroll this EFI").

# USB Port Mapping

USB-Port Mapping is done via `SSDT-USB-B650M-Riptide.aml`:
- `XH00` is defined in `DSDT.aml`. 
- `XHC0`, `XHC1` and `XHC2` are defined in `SSDT-USB.aml`. 
- I had to fix all errors in `DSDT.aml` and removed USB-port definition from the `DSDT.aml`. 
- I also deleted the original `SSDT-USB.aml`. 
- The USB-Port Mapping for all controllers is in the `SSDT-USB-B650M-Riptide.aml`.

![USB-Port-Mapping_B650M-Riptide](Docs/USB-Port-Mapping_B650M-Riptide.png)

# Notes

- **iGPU is causing a crash on wake if enabled**. Disable iGPU in BIOS or disable it via Device Properties in your config.plist just for macOS
- **Two Keypresses to wake display after sleep** was solved by using `SSDT-USBW.aml` + `USBWakeFixup.kext` + Adding `acpi-wake-type=01` for every USB controller (`XH00`, `XHC0`, `XHC1` and `XHC2`) in the device properties.
