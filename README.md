# WeyMK06

This is a repository of information gathered about the WeyTec MK06 trading keyboard.

## Hardware

The devices' main application processor is of type Coldfire v4 MCF5474 with a total of 32MB of flash (1 IC of S29GL256N for older variants and S29GL256P for newer version of the board) and 64MB of DRAMs (2 ICs of EDD2516AETA-6B-E). The displays are driven using a MB86276 display controller/graphics accelerator to which 2 ICs of IS42S16400B-7TL 64MBit DRAMs are connected.

The Keyboard matrix seems to be driven using multiple CPLDs which probably serialize the keystate and send it to the APU. The APU does not seem to drive the matrix directly.

## Firmware

The firmware is entirely proprietary and does not seem to implement any known RTOS or OS. Application parts are separated into modules:

* 0x00000500-0x0000256A: MK06-FlashBootloader
* 0x00020000-0x00023D9F: MK06-DynamicBootloader
* 0x00041000-0x00041FFF: [Serial/Configuration Information]
* 0x00060000-0x00073331: EP1C3-Configuration
* 0x00080000-0x00082FFF: MK06 HCS08 Interface Module
* 0x000A0000-0x000AF78A: MK06-Application MainModul
* 0x000C0000-0x000DCE8C: MK06-Application BiosModul
* 0x000E0000-0x000EC8D2: MK06-Application TerminalModul
* 0x00100000-0x0011FD10: MK06-Application DisplayModul
* 0x00120000-0x001288D0: MK06-Application UsbModul
* 0x00140000-0x0015F8B8: MK06-Application EthernetModul
* 0x00160000-0x0017F674: MK06-Application FifoCtrlModul
* 0x00180000-0x0019EECA: MK06-Application KeyModul
* 0x001A0000-0x001B7950: MK06-Application DownloadModul
* 0x001C0000-0x001DF618: MK06-Application SetupModul
* 0x001E0000-0x001ED454: MK06-Application WsEmuModul
* 0x00200000-0x0020CC41: MK06-Application Vss2Modul
* 0x00220000-0x00226A83: MK06-Application SecurityModul
* 0x00240000-0x0025F942: MK06-Application MacroModul
* 0x00260000-0x00276356: MK06-Application MiscModul
* 0x00280000-0x0028C886: MK06-Application DLinkModul
* 0x002A0000-0x002A79F6: MK06-Application TestModul
* 0x002C0000-0x002CFF3E: MK06-Application VssIPModul

For unlocking, the SetupModul and SecuritModul seem to be most interesting. I presume for driving a video source to the display, the EthernetModul and VssIPModul to be interesting.