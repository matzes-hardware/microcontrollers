# E) Übersicht Programmer/Debugger

Die Tabelle listet verbreitete Standard-, quasi-Standard- und Off-the-shelf-Geräte. Bei proprietären 8-bit/OTP-Familien sind oft **Sockeladapter** oder bausteinspezifische Adapter erforderlich.

| Hersteller / Anbieter | Serie / Modell | Modell-Variante | Ziel-Familien | Schnittstellen | Protokolle | Funktionen | Spannungs-/Betriebsnotizen | Quellen |
|---|---|---|---|---|---|---|---|---|
| SEGGER | J-Link | EDU, EDU Mini, BASE, PLUS, ULTRA+, PRO, OB | Arm Cortex-M/R/A, RISC-V, Renesas, Nordic, Silicon Labs, NXP, ST, viele weitere | JTAG, SWD, SWO, cJTAG je Modell, UART bridge bei manchen | Arm ADI/CoreSight, RISC-V Debug, vendor flash loaders | Debuggen, Flashen, RTT, SWO Trace, Ozone, Production-Flasher mit J-Flash | VTref-abhängige Pegel; Modellgrenzen und Lizenz beachten | [J-Link interface][segger-jlink] |
| STMicroelectronics | ST-LINK | ST-LINK/V2, V2-1, V3MINIE, V3SET, V3PWR | STM32, STM8; teils generisch CMSIS-DAP/JTAG/SWD in Tools | SWD, JTAG, SWIM, UART bridge/VCP, SPI/I²C/CAN bridge bei V3SET | ST-LINK protocol, SWD/JTAG, SWIM, STM32CubeProgrammer | Flashen, Debuggen, mass erase, option bytes, SWV | Zielspannung abhängig vom Modell; V3SET modular | [STLINK-V3SET][stm-stlinkv3set], [UM2448][stm-stlinkv3] |
| Microchip | PICkit | PICkit 4, PICkit 5 | PIC, dsPIC, PIC32, AVR, SAM je Tool/Device-Support | ICSP, SWD/JTAG, UPDI, AVR ISP/PDI/TPI/debugWIRE je Support | MPLAB/debug executive, UPDI/ICSP | Flashen, Debuggen, Production Programming light | PICkit 5 ist aktuelles off-the-shelf Tool; Device-support in MPLAB prüfen | [PICkit 5][microchip-pickit5] |
| Microchip | MPLAB ICD / ICE / SNAP | ICD 4/5, MPLAB ICE 4, SNAP | PIC/dsPIC/PIC32/AVR/SAM | ICSP, JTAG/SWD, UPDI, AVR interfaces je Tool | MPLAB X debug/program protocols | Debug, Flashen, Trace/Power-Messung je Modell | SNAP günstig, ICE leistungsfähiger | [ICSP][microchip-icsp] |
| Microchip / Atmel | Atmel-ICE | Basic, full kit | AVR, AVR32, SAM | JTAG, SWD, PDI, TPI, aWire, SPI, debugWIRE | AVR/SAM Programming und Debug | Flashen, Debuggen, Fuse/Lock-Bits | Dokumentierter Target-Voltage-Bereich typ. 1,62–5,5 V | [Atmel-ICE][atmel-ice] |
| NXP | MCU-Link | MCU-Link, MCU-Link Pro | NXP LPC, MCX, Kinetis, i.MX RT und generische Cortex-M | SWD/JTAG, VCOM, SPI/I²C bridge bei Pro | CMSIS-DAP, SWO/trace je Modell | Debug/Flash, energy measurement/serial bridge bei Pro | Pro bietet galvanische/Target features je Revision | [MCU-Link][nxp-mculink], [MCU-Link Pro][nxp-mculinkpro] |
| Renesas | E2 Emulator | E2, E2 Lite | RA, RX, RL78, RH850, RISC-V je Support | JTAG, SWD, FINE, LPD, serial programming je Familie | Renesas on-chip debug/prog | Debug, Flash Programming, power features je Modell | E2 Lite auch als Programmer verwendbar | [E2 Lite][renesas-e2lite], [E2][renesas-e2] |
| Texas Instruments | XDS | XDS110, XDS200, XDS560 | MSP432, C2000, SimpleLink, Hercules, AM/CCS targets | JTAG, cJTAG, SWD je Target | TI debug protocols, Arm/RISC-V/JTAG je Tool | Debug/Flash über CCS/UniFlash | XDS110 ist Standard-Low-cost Probe | [XDS110][ti-xds110] |
| Texas Instruments | MSP-FET | MSP-FET Flash Emulation Tool | MSP430/MSP430FR | MSP430 JTAG, Spy-Bi-Wire | MSP430 programming/debug | Flash/FRAM Programming, Debug, BSL support je Toolchain | Pin-sparendes SBW oder Standard-JTAG | [MSP-FET][ti-mspfet] |
| Arm/Keil | ULINK | ULINK2, ULINKplus, ULINKpro | Arm Cortex-M/R/A, Keil MDK targets | SWD, JTAG, SWO, ETM trace bei ULINKpro | CMSIS/Arm Debug, CoreSight | Debug, Flash, Trace, Event/Power analyse je Modell | Stark in Keil-MDK integriert | [ULINKpro][arm-ulink] |
| Arm / DAPLink | CMSIS-DAP / DAPLink | viele Boards/Probes: LPC-Link2, Picoprobe-Firmware, EDBG, KitProg | Arm Cortex-M targets | SWD/JTAG, SWO, UART, Mass-storage drag-and-drop je Firmware | CMSIS-DAP v1/v2, DAPLink MSC/CDC/HID | Debug, Flash, Serial bridge | Offener Standard; Performance variiert stark | [CMSIS-DAP][cmsis-dap], [DAPLink][daplink] |
| Black Magic | Black Magic Probe | BMP, BMP Mini, ST-Link converted firmware | Arm Cortex-M, einige RISC-V/ESP targets je Firmware | SWD, JTAG, UART | GDB-server direkt im Probe | Debug/Flash ohne OpenOCD auf Host | Sehr nützlich für RE/Lab; Zielsupport prüfen | [Black Magic][blackmagic], [Usage][blackmagic-doc] |
| Espressif | ESP-Prog | ESP-Prog board | ESP32/ESP8266/ESP32-S/C/H/P je Verdrahtung | JTAG, UART, auto-reset/boot | OpenOCD JTAG, esptool UART | Flashen, Debuggen, Console | Pegel/Jumper beachten; neue ESP32-S/C können USB Serial/JTAG direkt | [ESP-Prog][esp-prog], [USB Serial/JTAG][espressif-usbjtag] |
| GigaDevice | GD-Link | GD-Link, GD-Link V3 | GD32 Arm/RISC-V | SWD, JTAG, UART/serial/offline je Version | GD32 debug/programming | Debug, Flash, offline download | Offizielles GD32 Tool | [GD-Link][gigadevice-gdlink] |
| WCH | WCH-Link | WCH-LinkE, WCH-Link | WCH CH32V/CH32F/CH57x/CH58x | RVSWD/SDI, SWD, UART bridge je Version | WCH RISC-V/Arm download/debug | Flashen, Debuggen, Serial | CH32V003 nutzt 1-wire SDI; WCH-LinkE unterstützt RISC-V und Arm MCUs | [WCH-LinkE][wch-linke], [CH32V003][wch-ch32v003] |
| Nuvoton | Nu-Link | Nu-Link, Nu-Link2-Pro, Nu-Link2-Me | Nuvoton NuMicro, 8051 families je Tool | SWD, ISP/ICP, UART/USB bridge/offline je Modell | Nuvoton debug/program | Debug, Flashen, Offline Programming | Nu-Link2-Pro listet programmierbare VDD 1,8/2,5/3,3/5 V und Target-Input 1,8–5,5 V | [Nu-Link][nuvoton-nulink] |
| Holtek | e-Link32 | e-Link32 | Holtek HT32 | Serial Wire / SWD | HT32 debug/program | Debug, Flashen in Keil/IAR/HT-IDE | USB-zu-Serial-Wire Targetverbindung | [e-Link32][holtek-elink32] |
| Holtek | e-Writer / e-WriterPro | modellabhängige Adapter | Holtek HT8 Flash/OTP | proprietär, Sockel/ICP je Device | Holtek Writer-Protokoll | OTP/Flash Programming, Verify, Option bits | Adapterliste/Device-Support nötig | [Holtek Flash][holtek-flash], [Holtek OTP][holtek-otp] |
| ELAN/EMC | UWTR / DWTR | NUWTR Writer System, Adapter | ELAN EM78 Flash/OTP | proprietär, Sockel/ICP je Modell | ELAN Writer-Protokoll | Flash/OTP Programming, Blank Check, Verify | Für EM78-Identifikation relevant; konkrete Adapter/Pins per Device-Liste | [UWTR][elan-uwtr] |
| Padauk | Padauk Writer / ICE | PADAUK IDE, Writer, PMS/PMC/PFS tools | Padauk OTP/MTP/Flash MCUs | proprietär | Padauk programming/debug where available | Programming, Verify, Erase bei Flash/MTP | Ultra-low-cost MCUs oft OTP; Debug nur bei ICE-fähigen Varianten | [Padauk tools][padauk-tools] |
| Free-PDK community | Easy PDK Programmer | Easy-PDK programmer HW/SW | ausgewählte Padauk ICs | proprietär emuliert | probe/read/write/erase je unterstütztem IC | Open-source-orientiertes Tool zum Schreiben/Lesen/Erase | Nicht offizieller Padauk-Support; Device-Liste prüfen | [Easy-PDK][easypdkprog] |
| Silicon Labs | USB Debug Adapter / Simplicity Link | 8-bit USB Debug Adapter, J-Link OB auf Kits | EFM8/C8051F/EFM32/EFR32 | C2, JTAG, SWD je Tool/Target | C2/JTAG/SWD | Debug, Flashen | 8-bit Adapter für C2/8051; neuere Kits oft J-Link OB | [Silabs C2][silabs-c2], [Silabs debugger][silabs-debugger] |
| ROHM/LAPIS | EASE1000 V2 | Emulator/debugger/flash writer | ML62Q/ML610Q/ML620Q u. a. | ROHM/LAPIS OCD/ISP | on-chip debug, flash write | Debug, Flash Writer, Emulator | Für Lapis/Rohm Low-power-MCUs | [EASE1000 V2][rohm-ease1000] |
| Sonix | SN8P OTP Easy Writer | Easy Writer, Socketadapter | Sonix SN8P OTP | proprietär/Sockel | OTP Programming | OTP schreiben, Verify, Optionen | Für SN8P-OTP-Familien | [Sonix OTP Writer][sonix-otpwriter] |
| Megawin | Writer8_U1Plus | U1Plus | Megawin 8051/MCU families | ICP/ISP/Sockel je Adapter | Megawin programming | Flashen, Verify, Optionen, Seriennummern je Tool | Device-Support-Liste prüfen | [Writer8_U1Plus][megawin-writer8] |
| Generisch | FTDI FT2232H/FT232H-basierte Adapter | Olimex ARM-USB-OCD, Tigard, FTDI C232HM u. a. | JTAG/SWD/UART/SPI/I²C targets je Software | JTAG, SWD über OpenOCD adapter drivers, UART/SPI/I²C | OpenOCD, UrJTAG, flashrom, vendor bootloader tools | Debug, Boundary Scan, Bootloader, externes SPI-Flash | Pinout/Pegel/Level-Shifter entscheidend; nicht automatisch MCU-spezifischer Flashloader | [OpenOCD adapter config][openocd] |
| Generisch | USB-UART Adapter | CP210x, CH340, FT232, PL2303 usw. | UART-Bootloader: ESP, STM32, NXP, STC, WCH, viele 8051 | UART TX/RX, DTR/RTS für Reset/Boot | vendor Bootloader | Flashen, Console, RE/Logging | Pegel 1,8/3,3/5 V prüfen; nicht RS-232-Pegel | [ST AN2606][st-an2606], [stcgal][stcgal] |
| Generisch | Dediprog / flashrom-kompatible SPI-Flash-Programmer | SF100, CH341A, Bus Pirate, Tigard etc. | externe SPI/QSPI-Flashs auf MCU-Boards | SPI/QSPI | JEDEC SPI Flash | Direktes Lesen/Schreiben externer Firmware-Flashs | Board muss stromlos/isoliert sein oder in-circuit Konflikte lösen; Verschlüsselung möglich | [OpenOCD][openocd] |

## Literaturverzeichnis

[segger-jlink]: https://www.segger.com/products/debug-probes/j-link/technology/interface-description/
[stm-stlinkv3set]: https://www.st.com/en/development-tools/stlink-v3set.html
[stm-stlinkv3]: https://www.st.com/resource/en/user_manual/um2448-stlinkv3set-debuggerprogrammer-for-stm8-and-stm32-stmicroelectronics.pdf
[microchip-pickit5]: https://www.microchip.com/en-us/development-tool/PG164150
[microchip-icsp]: https://developerhelp.microchip.com/xwiki/bin/view/software-tools/programmers-and-debuggers/pic-and-dspic-downloads/ice4-icsp/
[atmel-ice]: https://www.microchip.com/en-us/development-tool/ATATMEL-ICE
[nxp-mculink]: https://www.nxp.com/design/design-center/development-boards-and-designs/mcu-link-debug-probe:MCU-LINK
[nxp-mculinkpro]: https://www.nxp.com/design/design-center/development-boards-and-designs/mcu-link-pro-debug-probe:MCU-LINK-PRO
[renesas-e2lite]: https://www.renesas.com/en/software-tool/e2-emulator-lite-rte0t0002lkce00000r
[renesas-e2]: https://www.renesas.com/en/software-tool/e2-emulator-rte0t00020kce00000r
[ti-xds110]: https://www.ti.com/tool/TMDSEMU110-U
[ti-mspfet]: https://www.ti.com/tool/MSP-FET
[arm-ulink]: https://developer.arm.com/Tools%20and%20Software/ULINKpro
[cmsis-dap]: https://arm-software.github.io/CMSIS_5/DAP/html/index.html
[daplink]: https://armmbed.github.io/DAPLink/
[blackmagic]: https://black-magic.org/
[blackmagic-doc]: https://black-magic.org/usage/
[esp-prog]: https://docs.espressif.com/projects/esp-iot-solution/en/latest/hw-reference/ESP-Prog_guide.html
[espressif-usbjtag]: https://docs.espressif.com/projects/esp-idf/en/latest/esp32s3/api-guides/usb-serial-jtag-console.html
[gigadevice-gdlink]: https://www.gigadevice.com/support/downloads/debug-tools/
[wch-linke]: https://www.wch-ic.com/products/WCH-LinkE.html
[wch-ch32v003]: https://www.wch-ic.com/products/CH32V003.html
[nuvoton-nulink]: https://www.nuvoton.com/tool-and-software/debugger-and-programmer/debugger-and-programmer-tools/numicro-ice-nu-link/
[holtek-elink32]: https://www.holtek.com/page/en/e-link32.html
[holtek-flash]: https://www.holtek.com/page/en/8-bit-flash-mcu.html
[holtek-otp]: https://www.holtek.com/page/en/8-bit-otp-mcu.html
[elan-uwtr]: https://www.emc.com.tw/upload/2019_11_012/NUWTR-AN001-v5.09.00%2820190501%29.pdf
[padauk-tools]: https://www.padauk.com.tw/en/technical/show.aspx?num=4&page=1
[easypdkprog]: https://free-pdk.github.io/easy-pdk-programmer-software/
[silabs-c2]: https://www.silabs.com/documents/public/application-notes/an127.pdf
[silabs-debugger]: https://www.silabs.com/development-tools/mcu/8-bit/8-bit-usb-debug-adapter
[rohm-ease1000]: https://www.rohm.com/products/microcontrollers/tools/ease1000-v2-product
[sonix-otpwriter]: https://www.sonix.com.tw/download/SN8P_OTP_Easy_Writer_User_Manual_V1.0_EN.pdf
[megawin-writer8]: https://www.megawin.com.tw/Files/Tool/Writer8_U1Plus/Writer8_U1Plus_Users_Manual.pdf
[openocd]: https://openocd.org/doc/html/Debug-Adapter-Configuration.html
[st-an2606]: https://www.st.com/resource/en/application_note/an2606-stm32-microcontroller-system-memory-boot-mode-stmicroelectronics.pdf
[stcgal]: https://github.com/grigorig/stcgal
