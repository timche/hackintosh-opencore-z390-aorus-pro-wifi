# Hackintosh

> Personal OpenCore configuration and files for Intel Core i7-9700K, Gigabyte Z390 Aorus Pro WiFi and Intel UHD Graphics 630 (iGPU)

![](./.github/about-this-mac.png)

## Disclaimer

I don't recommend you to copy my configuration and files. You should know what you are doing and learn how to configure and use OpenCore. This repository is publicly available only for learning and inspiration purposes.

## Software Versions

- OpenCore: 0.5.9
- macOS: 10.5.5 (Catalina)

## Hardware

- CPU: Intel Core i7-9700K
- Motherboard: Gigabyte Z390 Aorus Pro WiFi
- iGPU: Intel UHD Graphics 630
- GPU: ASUS ROG Strix GeForce GTX 1070 Ti Advanced OC *(Disabled)*
- RAM: Corsair 16GB DDR4 Vengeance LPX 3200 MHz
- SSD:
  - Crucial MX500 500GB M.2
  - Crucial BX100 250GB 2.5"
  - Crucial M500 120GB 2.5"

### Peripherals

- Mouse: Logitech G Pro Wireless
- Keyboard: KBC Poker 3
- Headset: Kingston HyperX Cloud
- Speakers: Audioengine A2+
- Monitor: Acer Nitro XF252Q (1080p)

## Working

*Work in progress.*

Everything listed below is working out of the box unless stated otherwise.

- Hardware Acceleration
- Onboard Audio
- Front Audio
- HDMI Audio
- Ethernet
- USB 3.0
- iServices

## Not Working

*Work in progress.*

- USB 2.0
- Bluetooth
- WiFi *(Disabled anyway)*

## Geekbench

![](./.github/geekbench.png)

## Quirks

These quirks are only specific to this hardware.

### `config.plist`

#### `DeviceProperties/Add/PciRoot(0x0)/Pci(0x2,0x0)`

- With macOS 10.15.5 the recommended value `07009B3E` for `AAPL,ig-platform-id` isn't working (anymore) for UHD 630. 
  - Fix: The alternative value `00009B3E` is working.
- Using only the suggested keys from the [OpenCore Coffee Lake guide](https://dortania.github.io/OpenCore-Desktop-Guide/config.plist/coffee-lake.html#deviceproperties) `AAPL,ig-platform-id`, `framebuffer-patch-enable` and `framebuffer-stolenmem` isn't sufficient and will result in getting no video signal/black screen after OpenCore verbose/boot.
  - Fix: [iGPU BusID Patching](https://dortania.github.io/OpenCore-Desktop-Guide/extras/gpu-patches.html#igpu-busid-patching) is necessary. After several reboots, it's port 3 and busID `04` to get a video signal (`AAPL,ig-platform-id` must be working beforehand).