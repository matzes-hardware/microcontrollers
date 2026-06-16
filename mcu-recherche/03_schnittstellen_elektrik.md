# C) Elektrische Eigenschaften physischer MCU-Flash-/Debug-Schnittstellen

Allgemein gilt: Debugger/Programmer sollten **VTref/Target-VDD messen** und Pegel daran anpassen. Die Spannungsbereiche sind daher meist nicht durch das Protokoll allein festgelegt, sondern durch MCU, Programmer und Boarddesign.

| Schnittstellen-Name | Mögliche / typische Spannungsbereiche | Logische Pins | Elektrische Funktion/Eigenschaften auf MCU-Seite | Hinweise / Quellen |
|---|---|---|---|---|
| JTAG IEEE 1149.1 | typ. 1,2–5,0/5,5 V abhängig von Target/Probe; VTref üblich | TCK, TMS, TDI, TDO, nTRST optional, nRESET optional | TCK/TMS/TDI Eingänge; TDO Ausgang, meist push-pull/tri-state; Reset-Pins oft open-drain-tauglich; VTref nur Sense | Nicht hot-plug- oder 5V-tolerant annehmen; BSDL nur Boundary-Scan-Beschreibung, nicht automatisch Flash-Protokoll.[^ieee1149][^bsdl-vendors] |
| SWD | typ. 1,2–5,0 V; moderne Probes oft 1,8–3,3 V, einige 5 V-tolerant; VTref entscheidend | SWDIO, SWCLK, nRESET optional, SWO optional | SWCLK Eingang; SWDIO bidirektional, turn-around-Zyklen; SWO Ausgang; nRESET meist open-drain/low-active | J-Link, CMSIS-DAP, ST-LINK, ULINK, XDS u. a. implementieren SWD/ADI.[^arm-adi][^segger-jlink][^cmsis-dap] |
| SWO | Target-VDD-Logikpegel | SWO/TDO | Ausgang der MCU, meist push-pull, hohe Baudraten möglich | Nur Trace-Ausgang; kein Flashen ohne SWD/JTAG. |
| cJTAG | Target-VDD-Logikpegel | TMSC, TCKC, optional Reset/VTref | Reduzierte JTAG-Signale; genaue elektrische Modi abhängig von Implementierung | Weniger universal; Probe/MCU-Support gesondert prüfen. |
| SWIM | STM8 typ. 3,0–5,5 V je MCU; Probe muss Target-VDD folgen | SWIM, NRST, VDD, VSS | SWIM bidirektional, single-wire async; ST beschreibt high-sink/open-drain-Verhalten; NRST low-active | Für STM8 Programming/Debug; ST-LINK/STLINK-V3 unterstützen SWIM.[^st-stm8swim][^stm-stlinkv3set] |
| Microchip ICSP / ICD | VDD je PIC, häufig 1,8–5,5 V; MCLR/VPP kann beim High-Voltage-Programming deutlich über VDD liegen, device-abhängig | PGC/ICSPCLK, PGD/ICSPDAT, MCLR/VPP, VDD, VSS | PGC Eingang; PGD bidirektional; MCLR/VPP Reset- und Programmierspannungseingang; VDD kann vom Tool gespeist oder gemessen werden | VPP-Spannung nicht auf andere Pins leiten; Schaltung an PGC/PGD/MCLR muss Programmer erlauben.[^microchip-icsp][^microchip-pickit5] |
| AVR ISP/SPI | Target-VDD, typ. 1,8–5,5 V; Programmer muss Vtarget-kompatibel sein | RESET, SCK, MOSI, MISO, VCC, GND | RESET low aktiviert Programming; SCK/MOSI Eingänge, MISO Ausgang; SPI-Pins sind oft normale GPIOs im Betrieb | Externe Lasten an SPI/RESET können Programmierung stören.[^avr-isp] |
| debugWIRE | Target-VDD, typ. AVR-Bereich 1,8–5,5 V | RESET/dW, VCC, GND | RESET-Pin wird bidirektionale half-duplex Debug-Leitung; Pull-up/Reset-Beschaltung kritisch | debugWIRE ist Debug, nicht direkt Programmierschnittstelle; Aktivierung kann reguläres ISP blockieren.[^microchip-debugwire] |
| UPDI | Target-VDD; übliche AVR-Targets 1,8–5,5 V; HV-UPDI nutzt spezielle Hochspannungs-Entry-Sequenzen je Tool/Device | UPDI, VCC, GND | Single-wire bidirektional, half-duplex, UART-artig; interne Pull-ups/Break-Sequenzen | Für moderne AVR Programming + Debug; UPDI-Pin darf nicht hart belastet werden.[^microchip-updi] |
| PDI / TPI / aWire | Target-VDD, Atmel-/Microchip-toolabhängig; Atmel-ICE target range typ. 1,62–5,5 V | PDI_CLK/PDI_DATA oder TPI/RESET je Familie | Clock + bidirektionale Daten bzw. Reset-basierte Leitung; device-spezifisch | Historische AVR-Schnittstellen; Atmel-ICE als Referenztool.[^atmel-ice][^avr-interfaces] |
| MSP430 JTAG | Target-VDD; MSP-FET kann Zielsysteme versorgen bzw. referenzieren, genaue Bereiche device/toolabhängig | TCK, TMS, TDI, TDO, TEST, RST/NMI, VCC, GND | Klassische JTAG-Eingänge/Ausgang; TEST/RST steuern Entry-Sequenz; Reset low-active | MSP430 nutzt JTAG auch für Flash/FRAM-Programming.[^ti-msp430][^ti-mspfet] |
| Spy-Bi-Wire | Target-VDD, tool/deviceabhängig | SBWTCK/TEST, SBWTDIO/RST, VCC, GND | 2-wire JTAG: Taktleitung + bidirektionale Daten/Reset-Leitung | Platzsparend; Reset-Beschaltung beachten.[^ti-mspfet] |
| Silicon Labs C2 | Target-VDD; 8051/EFM8 deviceabhängig | C2CK, C2D, VDD, GND, RESET optional | C2CK Takt/Eingang; C2D bidirektionale Datenleitung; Reset/Power-Sequenz kann Entry bestimmen | Proprietär; nicht mit I²C verwechseln.[^silabs-c2] |
| UART Bootloader | CMOS-Logikpegel: 1,8/3,3/5 V je MCU; niemals direkt RS-232-Pegel ohne Pegelwandler | TXD, RXD, BOOT/ISP, RESET, VCC, GND | TXD Ausgang, RXD Eingang, BOOT/RESET Entry-Pins; ggf. auto-reset via DTR/RTS | ESP/STC/STM32/NXP/etc. nutzen unterschiedliche Protokolle über denselben UART-Grundbus.[^st-an2606][^stcgal] |
| USB Device Bootloader / USB Serial/JTAG | USB full-/high-speed: 3,3-V-Transceiver intern; VBUS 5 V Sense je Design | D+, D-, VBUS, GND, BOOT/RESET optional | Differentieller USB-Transceiver; VBUS-Erkennung; Pull-up/Pull-down gemäß USB | ROM DFU/HID/CDC/MSC oder proprietär; ESP USB Serial/JTAG kombiniert Download, JTAG Debug, Console.[^espressif-usbjtag][^raspberrypi-rp2040] |
| I²C Bootloader | typ. 1,8/3,3/5 V; Pull-ups auf Busspannung; Pegelwandler bei gemischten Domains | SDA, SCL, BOOT/RESET, VCC, GND | SDA bidirektional open-drain; SCL meist Eingang/open-drain-tauglich; beide brauchen Pull-ups | Lange Leitungen/kapazitive Lasten vermeiden; Busadressen/Boot-Pins prüfen.[^st-an2606] |
| SPI Bootloader / ISP | Target-VDD; typ. 1,8/3,3/5 V | SCK, MOSI, MISO, CS/NSS, RESET/BOOT, VCC, GND | SCK/MOSI/CS Eingänge; MISO Ausgang/tri-state; Boot-Pins als Entry | Nicht jedes SPI-Peripheral kann Bootloader; meist feste Pins. |
| CAN/CAN-FD Bootloader | MCU-Pins typ. 3,3/5 V; Bus über Transceiver gemäß CAN-Pegel | CAN_TX, CAN_RX an Transceiver; CANH/CANL auf Bus; BOOT/RESET | MCU-seitig TX push-pull, RX Eingang; Bus-seitig differentiell über Transceiver | Termination/Transceiver/Standby-Pin beachten; Protokoll meist vendor-spezifisch.[^st-an2606] |
| LIN Bootloader | MCU-UART-Pins typ. 3,3/5 V; LIN-Bus über LIN-Transceiver | LIN_TX/RX bzw. UART, RESET/BOOT | UART-artig an MCU; single-wire LIN-Bus über Transceiver | Häufig OEM/Application-Bootloader statt ROM. |
| WCH RVSWD / SDI | Target-VDD; WCH-Link misst/versorgt je Modell; meist 3,3 V | SWCLK/SWDIO-artig oder SDI single-wire, RESET, VCC, GND | proprietäre bidirektionale Debug-/Download-Signale; CH32V003 hat 1-wire SDI | Nicht vollständig ARM-SWD-kompatibel annehmen.[^wch-ch32v003][^wch-linke] |
| ELAN/EMC UWTR / DWTR | 3/5 V device- und adapterabhängig; Writer legt Versorgung/Programmiersequenzen fest | modellabhängige PROG/CLK/DATA/TEST/VDD/VSS-Pins | proprietär, oft Produktionsprogrammierung; einige OTP mit Socketadaptern | Für Reverse Engineering nur mit konkretem Datenblatt/Writer-Adapter sicher bestimmbar.[^elan-uwtr] |
| Holtek HT8 Writer/ICP | device-/writerabhängig, oft 3/5 V | PA-/PB-/TEST-/RES-/VDD-/VSS-ähnliche Pins modellabhängig | proprietär; OTP/Flash-Programming, Verify, Option bytes | HT32 dagegen nutzt Serial Wire/SWD über e-Link32.[^holtek-elink32][^holtek-flash] |
| Padauk Writer/ICE | device-/writerabhängig; low-cost OTP/MTP/Flash | VDD, GND, CLK/DATA/PROG/TEST modellabhängig | proprietär; viele Teile nur OTP oder MTP; Pinbelegung per Padauk-Tool/Adapter | Easy-PDK kann unterstützte ICs probe/read/write/erase je Typ.[^padauk-tools][^easypdkprog] |
| Externes SPI/QSPI/OSPI-Flash | Flash-VDD 1,8/3,3 V typ.; Pegel abhängig vom Flash, nicht nur MCU | CS, CLK, IO0-IO3/IO0-IO7, RESET/HOLD/WP | Flash-Pins bidirektional auf IO-Leitungen; WP/HOLD/RESET deviceabhängig | Firmwareauslesen oft möglich, wenn MCU-Code extern liegt; Security/Encryption kann Inhalt nutzlos machen. |

## Literaturverzeichnis

[^ieee1149]: [IEEE 1149.1 JTAG standard][ieee1149]
[^bsdl-vendors]: [BSDL files overview][bsdl-vendors]
[^arm-adi]: [Arm ADI][arm-adi]
[^segger-jlink]: [SEGGER interface description][segger-jlink]
[^cmsis-dap]: [CMSIS-DAP][cmsis-dap]
[^st-stm8swim]: [ST STM8 SWIM][st-stm8swim]
[^stm-stlinkv3set]: [STLINK-V3SET][stm-stlinkv3set]
[^microchip-icsp]: [Microchip ICSP][microchip-icsp]
[^microchip-pickit5]: [Microchip PICkit 5][microchip-pickit5]
[^avr-isp]: [AVR ISP][avr-isp]
[^microchip-debugwire]: [Microchip debugWIRE][microchip-debugwire]
[^microchip-updi]: [Microchip UPDI][microchip-updi]
[^atmel-ice]: [Atmel-ICE][atmel-ice]
[^avr-interfaces]: [AVR target interfaces][avr-interfaces]
[^ti-msp430]: [MSP430 Hardware Tools User's Guide][ti-msp430]
[^ti-mspfet]: [MSP-FET][ti-mspfet]
[^silabs-c2]: [Silicon Labs C2][silabs-c2]
[^st-an2606]: [ST AN2606][st-an2606]
[^stcgal]: [stcgal][stcgal]
[^espressif-usbjtag]: [Espressif USB Serial/JTAG][espressif-usbjtag]
[^raspberrypi-rp2040]: [RP2040][raspberrypi-rp2040]
[^wch-ch32v003]: [CH32V003][wch-ch32v003]
[^wch-linke]: [WCH-LinkE][wch-linke]
[^elan-uwtr]: [ELAN/EMC NUWTR][elan-uwtr]
[^holtek-elink32]: [Holtek e-Link32][holtek-elink32]
[^holtek-flash]: [Holtek Flash MCU][holtek-flash]
[^padauk-tools]: [Padauk tools][padauk-tools]
[^easypdkprog]: [Easy-PDK Programmer][easypdkprog]

[ieee1149]: https://standards.ieee.org/ieee/1149.1/510/
[bsdl-vendors]: https://www.xjtag.com/about-jtag/bsdl-files/
[arm-adi]: https://developer.arm.com/documentation/ihi0031/latest/
[segger-jlink]: https://www.segger.com/products/debug-probes/j-link/technology/interface-description/
[cmsis-dap]: https://arm-software.github.io/CMSIS_5/DAP/html/index.html
[st-stm8swim]: https://www.st.com/resource/en/user_manual/um0470-stm8-swim-communication-protocol-and-debug-module-stmicroelectronics.pdf
[stm-stlinkv3set]: https://www.st.com/en/development-tools/stlink-v3set.html
[microchip-icsp]: https://developerhelp.microchip.com/xwiki/bin/view/software-tools/programmers-and-debuggers/pic-and-dspic-downloads/ice4-icsp/
[microchip-pickit5]: https://www.microchip.com/en-us/development-tool/PG164150
[avr-isp]: https://onlinedocs.microchip.com/oxy/GUID-33422CDF-8B41-417C-9C31-E4521ADAE9B4-en-US-2/GUID-D1F30594-B225-461C-91CC-EF14F6557C01.html
[microchip-debugwire]: https://onlinedocs.microchip.com/oxy/GUID-DDB0017E-84E3-4E77-AAE9-7AC4290E5E8B-en-US-4/GUID-7F2A4E92-8D08-4BA1-B705-1618F7EFBFC2.html
[microchip-updi]: https://onlinedocs.microchip.com/oxy/GUID-7056F141-DF07-46C5-A4B8-97EB46E9B945-en-US-12/GUID-EC6F68EF-2F0D-4D0E-A1FD-D266B695FCFE.html
[atmel-ice]: https://www.microchip.com/en-us/development-tool/ATATMEL-ICE
[avr-interfaces]: https://onlinedocs.microchip.com/oxy/GUID-5A56DB3A-31E1-4F46-984F-39186535C84E-en-US-7/GUID-8A20D003-86A9-45F0-91DD-81467B07AD2A.html
[ti-msp430]: https://www.ti.com/lit/ug/slau278/slu278.pdf
[ti-mspfet]: https://www.ti.com/tool/MSP-FET
[silabs-c2]: https://www.silabs.com/documents/public/application-notes/an127.pdf
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
