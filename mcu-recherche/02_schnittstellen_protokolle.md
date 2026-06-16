# B) Übersicht physischer MCU-Flash-/Debug-Schnittstellen und Protokolle

Diese Übersicht trennt **physische Schnittstelle** von **darüber gesprochenem Protokoll/Funktion**. Bei vielen MCUs ist die physische Schnittstelle identisch, aber das Protokoll herstellerspezifisch oder durch Boot-ROM/Fuse-Konfiguration eingeschränkt.

| Physische Schnittstelle | Typische Pins / Signale | Darüber mögliche Protokolle / Funktionen | Typische MCU-Familien / Hersteller | Bemerkungen / Quellen |
|---|---|---|---|---|
| JTAG IEEE 1149.1 TAP | TCK, TMS, TDI, TDO, nTRST optional, nRESET optional, VTref, GND | Boundary Scan, BSDL-basierte Tests, Debug Access Port, Flash-Programming über Debug-Agent, CoreSight, OpenOCD/J-Link/CMSIS-DAP | Arm Cortex-M/R/A, MIPS/PIC32, RISC-V, TI C2000/Hercules, Infineon AURIX, Renesas RX/RH850, ESP32 klassisch | IEEE 1149.1 definiert TAP; BSDL beschreibt die Boundary-Scan-Implementierung eines ICs.[^ieee1149][^bsdl-vendors] |
| SWD / Serial Wire Debug | SWDIO, SWCLK, optional SWO, nRESET, VTref, GND | Arm Debug Interface, CoreSight, Flash-Programming via debug probe, Breakpoints, Watchpoints, Trace über SWO | Arm Cortex-M: STM32, SAM, LPC/MCX/Kinetis, nRF, EFM32/EFR32, PSoC, GD32, MM32, PY32, HT32, NuMicro, ABOV 32-bit | 2-Draht-Alternative zu JTAG für Arm; weit verbreitetes Standard-Debuginterface.[^arm-adi][^segger-jlink] |
| SWO / Serial Wire Output | SWO/TDO, SWCLK/SWDIO separat; oft Teil des SWD-Headers | ITM/SWO Trace, printf-artiger Trace, Event-Counter, Sampling-Trace | Cortex-M3/M4/M7/M33/M55 je Implementierung | Nur Output/Trace, kein eigenständiges Programmiersignal. |
| cJTAG IEEE 1149.7 | TMSC/TCKC bzw. reduzierte JTAG-Pins | Compact JTAG, Debug/Test mit weniger Pins | Ausgewählte TI/Arm/RISC-V/Automotive-Bausteine | Weniger universell sichtbar als klassisches JTAG; Probe- und Device-Support prüfen. |
| SWIM (ST) | SWIM bidirektional, NRST, VDD/VTref, GND | STM8 In-circuit Programming und Debug | ST STM8 | Single-wire async protocol; bidirektional/open-drain-artig mit definiertem Sinkstrom.[^st-stm8swim] |
| Microchip ICSP / ICD | PGC/ICSPCLK, PGD/ICSPDAT, MCLR/VPP, VDD, VSS, ggf. AUX | PIC/dsPIC/PIC32 Flash-Programming, Debug Executive, HV/LV Programming | Microchip PIC, dsPIC, PIC32 | Zweidraht-Daten/Takt plus Reset/VPP; Toolfamilien PICkit/MPLAB ICD/SNAP/ICE.[^microchip-icsp] |
| AVR ISP über SPI | RESET, SCK, MOSI, MISO, VCC, GND | In-system Programming, Fuse/Lock-Bits, Flash/EEPROM schreiben/lesen | Ältere AVR tiny/mega/classic | Kein Live-Debug; debug meist debugWIRE/JTAG/PDI/UPDI.[^avr-isp][^avr-interfaces] |
| AVR JTAG | TCK, TMS, TDI, TDO, RESET, VCC, GND | Programming, On-chip Debug, Boundary Scan bei großen AVRs | ATmega16/32/128 u. a.; AVR32 | Wird bei neueren kleinen AVRs meist durch UPDI ersetzt.[^avr-interfaces] |
| debugWIRE | RESET/dW, VCC, GND | Single-wire On-chip Debug über RESET-Leitung | Viele ältere kleine AVR tiny/mega | Debug-Schnittstelle, nicht primär Programmierinterface; Aktivierung kann ISP-Zugriff beeinflussen.[^microchip-debugwire] |
| UPDI | UPDI, VCC, GND; optional HV-UPDI | Unified Program and Debug Interface: Programming, Debug, Fuses, NVM | Moderne AVR tinyAVR 0/1/2, megaAVR 0, AVR Dx/Ex | Proprietäre single-wire half-duplex UART-artige Schnittstelle.[^microchip-updi] |
| PDI / TPI / aWire | PDI_CLK/PDI_DATA bzw. TPI/RESET je Familie | Programming/Debug je AVR-XMEGA/tiny/AVR32 | AVR XMEGA, tinyAVR alt, AVR32 | Historische Microchip/Atmel-Schnittstellen; Atmel-ICE unterstützt viele davon.[^avr-interfaces][^atmel-ice] |
| MSP430 JTAG | TCK, TMS, TDI/TCLK, TDO/TDI, RST/NMI, TEST, VCC, GND | Flash/FRAM Programming, Debug, Fuse/BSL | TI MSP430/MSP430FR | Standard-JTAG-Variante für MSP430.[^ti-msp430] |
| MSP430 Spy-Bi-Wire | SBWTCK/TEST, SBWTDIO/RST, VCC, GND | Pin-sparendes 2-wire JTAG: Programming/Debug | TI MSP430/MSP430FR | MSP-FET unterstützt JTAG und Spy-Bi-Wire.[^ti-mspfet] |
| Silicon Labs C2 | C2CK, C2D, VDD, GND, RESET optional | In-system Flash/EPROM Programming und Debug | Silicon Labs C8051F, EFM8 | Proprietäre 2-wire Schnittstelle mit Clock und bidirektionalem Data.[^silabs-c2][^silabs-debugger] |
| UART Bootloader | TXD, RXD, RESET/BOOT/ISP, VCC, GND | ROM-Bootloader, ISP, Firmwaredownload, Monitor/Console | STM32, NXP LPC/MCX, ESP8266/ESP32, STC, Nuvoton, WCH, many 8051 MCUs | Protokoll ist fast immer herstellerspezifisch; Pegel meist CMOS/TTL, nicht RS-232 ±12 V.[^st-an2606][^stcgal] |
| USB Device Bootloader | USB D+, D-, VBUS/5V sense, GND, BOOT/RESET | DFU, HID, MSC drag-and-drop, CDC bootloader, vendor protocol, USB Serial/JTAG | STM32, SAM, NXP LPC/MCX, RP2040/RP2350, ESP32-S/C/P, Microchip PIC/SAM | Bei manchen MCUs ROM-Bootloader, bei anderen Application-Bootloader.[^st-an2606][^espressif-usbjtag][^raspberrypi-rp2040] |
| I²C Bootloader | SDA, SCL, BOOT/RESET, VCC, GND | ROM-Bootloader / ISP / EEPROM-like register protocol | STM32 ausgewählte Linien, NXP/Microchip ausgewählte Serien | Open-drain Bus; externe Pull-ups erforderlich; selten für Debug, eher Programming/Boot.[^st-an2606] |
| SPI Bootloader | SCK, MOSI, MISO, NSS/CS, BOOT/RESET, VCC, GND | ROM-Bootloader / ISP; externes Flash-Programming | STM32, NXP, AVR ISP, viele Boot-ROMs; externe QSPI-Flash Designs | Debug normalerweise nicht über SPI; meist nur Flash/Boot. |
| CAN / CAN-FD Bootloader | CANH/CANL über Transceiver, BOOT/RESET, VCC, GND | ROM/serial bootloader für automotive/industrial | STM32, NXP, Renesas, Infineon, automotive MCUs | Physisch braucht die MCU zusätzlich einen CAN-Transceiver; Boot-ROM-Protokolle herstellerspezifisch.[^st-an2606] |
| LIN Bootloader | UART/LIN pin über LIN-Transceiver, RESET/BOOT | In-field Programming in Automotive/Appliance | Automotive 8/16/32-bit MCUs | Meist Application-Bootloader oder OEM-Protokoll, selten Standard-Debug. |
| WCH RVSWD / SDI | SWDIO/SWCLK-artig bzw. 1-wire SDI bei CH32V003, VCC, GND, RESET optional | Download/Debug für WCH RISC-V | WCH CH32V/CH32X | WCH-LinkE unterstützt RISC-V/Arm Download/Debug; CH32V003 dokumentiert 1-wire debugging.[^wch-ch32v003][^wch-linke] |
| ELAN/EMC Writer-Interface | modellabhängige Writer-/Programming-Pins, VDD/VSS, ggf. OSC/Reset/Test | OTP/Flash Programming, Verify, Blank Check; meist kein universelles Debug | ELAN EM78P/EM78F | UWTR Writer-System für ELAN FLASH und OTP-Chips.[^elan-uwtr] |
| Holtek ICP / e-Link / e-Link32 | modellabhängig; HT32: Serial Wire; 8-bit: Writer-/ICP-Pins | Flash/OTP Programming; HT32 Debug über SWD | Holtek HT8/HT32 | e-Link32 verbindet Target über Serial Wire mit USB/IDE.[^holtek-elink32][^holtek-flash] |
| Padauk Writer/ICE | proprietäre Programmiersignale je IC/Package, VDD/GND | OTP/MTP/Flash Programming, ICE bei ausgewählten Familien | Padauk PMS/PMC/PFS/PFC | Offizielle Writer/IDE; freie Easy-PDK-Tools unterstützen Teile der Familien.[^padauk-tools][^easypdkprog] |
| Sonix OTP/Flash Writer | proprietär, oft Sockel/Adapter oder ICP | OTP/Flash Programming, Verify, Optionen/Fuses | Sonix SN8P/SN8F | Sonix OTP Easy Writer für SN8P-OTP-Familien.[^sonix-otpwriter] |
| Externes QSPI/OSPI/SPI-Flash | QSPI/OSPI: CLK, CS, IO0-IO3/IO0-IO7; VCC/GND | XiP-Firmware-Speicher programmieren; Debug separat über SWD/JTAG/UART | ESP32, RP2040/RP2350, i.MX RT, viele HMI/AI MCUs | Nicht MCU-internes Debug, aber praktisch relevant: Firmware liegt oft extern und kann direkt programmiert/ausgelesen werden. |

## Literaturverzeichnis

[^ieee1149]: [IEEE 1149.1 JTAG standard][ieee1149]
[^bsdl-vendors]: [BSDL files and JTAG implementation description][bsdl-vendors]
[^arm-adi]: [Arm Debug Interface Architecture Specification][arm-adi]
[^segger-jlink]: [SEGGER J-Link interface description][segger-jlink]
[^st-stm8swim]: [ST STM8 SWIM protocol][st-stm8swim]
[^microchip-icsp]: [Microchip ICSP][microchip-icsp]
[^avr-isp]: [AVR ISP/SPI programming notes][avr-isp]
[^avr-interfaces]: [Microchip AVR target interfaces][avr-interfaces]
[^microchip-debugwire]: [Microchip debugWIRE][microchip-debugwire]
[^microchip-updi]: [Microchip UPDI][microchip-updi]
[^atmel-ice]: [Microchip Atmel-ICE][atmel-ice]
[^ti-msp430]: [TI MSP430 Hardware Tools User's Guide][ti-msp430]
[^ti-mspfet]: [TI MSP-FET][ti-mspfet]
[^silabs-c2]: [Silicon Labs AN127 C2][silabs-c2]
[^silabs-debugger]: [Silicon Labs 8-bit USB Debug Adapter][silabs-debugger]
[^st-an2606]: [ST AN2606 bootloader interfaces][st-an2606]
[^stcgal]: [stcgal STC ISP tool][stcgal]
[^espressif-usbjtag]: [Espressif USB Serial/JTAG][espressif-usbjtag]
[^raspberrypi-rp2040]: [Raspberry Pi RP2040][raspberrypi-rp2040]
[^wch-ch32v003]: [WCH CH32V003][wch-ch32v003]
[^wch-linke]: [WCH-LinkE][wch-linke]
[^elan-uwtr]: [ELAN/EMC NUWTR Writer System][elan-uwtr]
[^holtek-elink32]: [Holtek e-Link32][holtek-elink32]
[^holtek-flash]: [Holtek 8-bit Flash MCU][holtek-flash]
[^padauk-tools]: [Padauk tools][padauk-tools]
[^easypdkprog]: [Easy PDK Programmer][easypdkprog]
[^sonix-otpwriter]: [Sonix OTP Easy Writer][sonix-otpwriter]

[ieee1149]: https://standards.ieee.org/ieee/1149.1/510/
[bsdl-vendors]: https://www.xjtag.com/about-jtag/bsdl-files/
[arm-adi]: https://developer.arm.com/documentation/ihi0031/latest/
[segger-jlink]: https://www.segger.com/products/debug-probes/j-link/technology/interface-description/
[st-stm8swim]: https://www.st.com/resource/en/user_manual/um0470-stm8-swim-communication-protocol-and-debug-module-stmicroelectronics.pdf
[microchip-icsp]: https://developerhelp.microchip.com/xwiki/bin/view/software-tools/programmers-and-debuggers/pic-and-dspic-downloads/ice4-icsp/
[avr-isp]: https://onlinedocs.microchip.com/oxy/GUID-33422CDF-8B41-417C-9C31-E4521ADAE9B4-en-US-2/GUID-D1F30594-B225-461C-91CC-EF14F6557C01.html
[avr-interfaces]: https://onlinedocs.microchip.com/oxy/GUID-5A56DB3A-31E1-4F46-984F-39186535C84E-en-US-7/GUID-8A20D003-86A9-45F0-91DD-81467B07AD2A.html
[microchip-debugwire]: https://onlinedocs.microchip.com/oxy/GUID-DDB0017E-84E3-4E77-AAE9-7AC4290E5E8B-en-US-4/GUID-7F2A4E92-8D08-4BA1-B705-1618F7EFBFC2.html
[microchip-updi]: https://onlinedocs.microchip.com/oxy/GUID-7056F141-DF07-46C5-A4B8-97EB46E9B945-en-US-12/GUID-EC6F68EF-2F0D-4D0E-A1FD-D266B695FCFE.html
[atmel-ice]: https://www.microchip.com/en-us/development-tool/ATATMEL-ICE
[ti-msp430]: https://www.ti.com/lit/ug/slau278/slu278.pdf
[ti-mspfet]: https://www.ti.com/tool/MSP-FET
[silabs-c2]: https://www.silabs.com/documents/public/application-notes/an127.pdf
[silabs-debugger]: https://www.silabs.com/development-tools/mcu/8-bit/8-bit-usb-debug-adapter
[st-an2606]: https://www.st.com/resource/en/application_note/an2606-stm32-microcontroller-system-memory-boot-mode-stmicroelectronics.pdf
[stcgal]: https://github.com/grigorig/stcgal
[espressif-usbjtag]: https://docs.espressif.com/projects/esp-idf/en/latest/esp32s3/api-guides/usb-serial-jtag-console.html
[raspberrypi-rp2040]: https://www.raspberrypi.com/products/rp2040/
[wch-ch32v003]: https://www.wch-ic.com/products/CH32V003.html
[wch-linke]: https://www.wch-ic.com/products/WCH-LinkE.html
[elan-uwtr]: https://www.emc.com.tw/upload/2019_11_012/NUWTR-AN001-v5.09.00%2820190501%29.pdf
[holtek-elink32]: https://www.holtek.com/page/en/e-link32.html
[holtek-flash]: https://www.holtek.com/page/en/8-bit-flash-mcu.html
[padauk-tools]: https://www.padauk.com.tw/en/technical/show.aspx?num=4&page=1
[easypdkprog]: https://free-pdk.github.io/easy-pdk-programmer-software/
[sonix-otpwriter]: https://www.sonix.com.tw/download/SN8P_OTP_Easy_Writer_User_Manual_V1.0_EN.pdf
