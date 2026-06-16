# D) Schnittstellen und Protokolle nach MCU-Serien

Diese Tabelle ist als praktische Nachschlagetabelle gedacht: Welche Programmierschnittstelle ist bei welcher Serie wahrscheinlich? Konkrete Bausteine können abweichen; bei unmarkierten/gelaserten Chips ist immer das konkrete Datenblatt und das Board-Pinout entscheidend.

| Hersteller | Produktserie / Modellgruppe | Prozessor / Kern | Programmspeicher / Boot-Konzept | Schnittstelle(n) | Nutzbares Protokoll / Funktion | Typische Werkzeuge / Hinweise | Quellen |
|---|---|---|---|---|---|---|---|
| Microchip | PIC10/12/16/18 | PIC 8-bit | Flash/EEPROM, ältere OTP/EPROM | ICSP: PGC/PGD/MCLR/VPP | Flashen, Verify, Config Bits; Debug bei ICD-fähigen Derivaten | PICkit 4/5, ICD 4/5, SNAP | [ICSP][microchip-icsp], [PICkit 5][microchip-pickit5] |
| Microchip | PIC24/dsPIC33 | 16-bit PIC/dsPIC | Flash/Data EEPROM je Derivat | ICSP/ICD, JTAG bei einigen | Flashen, Debug, Config Bits | PICkit/ICD/MPLAB ICE | [ICSP][microchip-icsp] |
| Microchip | PIC32MX/MZ/MM/CM | MIPS M4K/MIPS32 oder Arm Cortex-M | Flash, Bootloader optional | ICSP/ICD, JTAG/SWD je Familie | Flashen, Debug, Bootloader | MPLAB X, PICkit/ICD; JTAG bei MIPS-PIC32 | [Microchip MCU Selector][microchip-parametric] |
| Microchip | AVR tiny/mega classic | AVR 8-bit | Flash/EEPROM/Fuses | ISP/SPI, debugWIRE, JTAG bei größeren | Flashen über ISP; Debug über debugWIRE/JTAG | Atmel-ICE, AVRISP, PICkit 4/5 teils | [AVR interfaces][avr-interfaces], [AVR ISP][avr-isp] |
| Microchip | tinyAVR 0/1/2, megaAVR 0, AVR Dx/Ex | AVR 8-bit | Flash/EEPROM/Fuses | UPDI | Programming + Debug über 1 Leitung | Atmel-ICE, MPLAB SNAP/PICkit, pyupdi/serialupdi inoffiziell | [UPDI][microchip-updi] |
| Microchip | SAM D/L/C/E/V | Arm Cortex-M0+/M3/M4/M7 | Flash + ROM Bootloader je Modell | SWD/JTAG, USB/UART/I²C/SPI Boot je Modell | Debug, Flashen, Bootloader | Atmel-ICE, CMSIS-DAP, J-Link, EDBG | [SAM D][microchip-samd], [CMSIS-DAP][cmsis-dap] |
| ST | STM8S/STM8L/STM8AF | STM8 8-bit | Flash/EEPROM | SWIM, UART Bootloader bei einigen | Flashen + Debug über SWIM | ST-LINK/V2, STLINK-V3 | [SWIM][st-stm8swim], [STLINK-V3][stm-stlinkv3set] |
| ST | STM32F/L/G/C/U/W/H/N | Arm Cortex-M | Flash + System-Memory Bootloader | SWD/JTAG, USB DFU, UART, CAN, I²C, SPI je Modell | Debug/Flash via SWD/JTAG; ROM-Bootloader via Peripherals | ST-LINK, J-Link, CMSIS-DAP, OpenOCD | [STM32][st-stm32], [AN2606][st-an2606] |
| NXP | LPC8xx/11xx/15xx/17xx/40xx/54xxx/55xxx | Arm Cortex-M | Flash + ISP ROM | SWD/JTAG, UART/USB/I²C/SPI ISP je Modell | Debug, SWD Flash, ROM ISP | MCU-Link, LPC-Link2, J-Link | [NXP MCU][nxp-mcu], [MCU Boot][nxp-mcu-boot] |
| NXP | MCX | Arm Cortex-M33/M33+NPU je Serie | Flash + ISP/ROM boot | SWD/JTAG, ISP/MCU Boot | Debug/Flash, provisioning | MCU-Link/Pro, J-Link | [NXP MCU][nxp-mcu], [MCU-Link Pro][nxp-mculinkpro] |
| NXP | Kinetis | Arm Cortex-M0+/M4/M7 | Flash + ROM bootloader bei vielen | SWD/JTAG, UART/USB/I²C/SPI/CAN je Modell | Debug/Flash, Kinetis Bootloader | J-Link, MCU-Link, OpenSDA | [MCU Boot][nxp-mcu-boot] |
| NXP | i.MX RT | Arm Cortex-M7/M33 | ROM + externes XiP-Flash | JTAG/SWD, USB/UART/SDP/serial downloader, QSPI/OSPI Flash | Debug, Boot/Provisioning, externes Flash programmieren | MCU-Link Pro, J-Link, NXP Secure Provisioning | [i.MX RT][nxp-imxrt], [MCU Boot][nxp-mcu-boot] |
| Renesas | RL78 | RL78 16-bit CISC | Flash/Data Flash | Renesas OCD/serial programming; E1/E2 interface | Flashen, Debug, Option bytes | E2 Lite/E2/E1 | [RL78][renesas-rl78], [E2 Lite][renesas-e2lite] |
| Renesas | RX | RX 32-bit | Flash/Data Flash | JTAG, FINE, SCI boot | Debug, Flashen, ID/security | E2/E2 Lite, J-Link für einige | [Renesas][renesas-company], [E2][renesas-e2] |
| Renesas | RA | Arm Cortex-M | Flash/Data Flash + SCI/USB Boot je Modell | SWD/JTAG, SCI/USB/CAN Boot je Modell | Debug/Flash, TrustZone/Secure Boot je Serie | E2/E2 Lite, J-Link, CMSIS-DAP | [Renesas][renesas-company] |
| Renesas | RH850 | RH850/RH850-U2A | Flash | JTAG/LPD, serial programming | Automotive Debug/Programming | E2/E2 Lite, Lauterbach/iSystem/PEMicro je Modell | [Renesas][renesas-company] |
| Infineon | AURIX TC2xx/TC3xx/TC4x | TriCore | Flash + Boot Firmware/BSL | JTAG, DAP, ASC/CAN boot je Modell | Debug/Trace, Flash, calibration | Infineon DAP miniWiggler, J-Link, Lauterbach | [Infineon MCU][infineon-mcu] |
| Infineon | XMC1000/4000 | Arm Cortex-M0/M4 | Flash + BMI/boot modes | SWD/JTAG, ASC/BSL bei einigen | Debug/Flash, boot mode selection | J-Link, XMC Link, DAVE tools | [Infineon MCU][infineon-mcu] |
| Infineon | PSOC 4/5/6 | M8C oder Arm Cortex-M | Flash/EEPROM-emulation | SWD/JTAG, KitProg/CMSIS-DAP | Debug/Flash, programming, bridge functions | KitProg, MiniProg, J-Link | [Infineon MCU][infineon-mcu] |
| TI | MSP430/MSP430FR | MSP430 16-bit | Flash oder FRAM | JTAG, Spy-Bi-Wire, BSL UART/I²C/SPI je Modell | Debug/Programming; Bootloader | MSP-FET, LaunchPad eZ-FET | [MSP-FET][ti-mspfet], [MSP430 Tools Guide][ti-msp430] |
| TI | C2000 | C28x/C28x+CLA | Flash/OTP sectors | JTAG, SCI/CAN boot je Modell | Real-time debug, flash | XDS110/XDS200/XDS560 | [XDS110][ti-xds110] |
| TI | SimpleLink CC13xx/CC26xx/CC32xx | Arm Cortex-M3/M4 | Flash/ROM wireless stacks | JTAG/SWD, serial bootloader, cJTAG bei einigen | Debug, Flash, RF test | XDS110, LaunchPad, UniFlash | [XDS110][ti-xds110] |
| Silicon Labs | EFM8/C8051F | 8051 | Flash | C2, JTAG/USB debug bei einigen | Debug, Flash/EPROM programming | Silicon Labs USB Debug Adapter, Simplicity Studio | [C2][silabs-c2], [Silabs debugger][silabs-debugger] |
| Silicon Labs | EFM32/EFR32 | Arm Cortex-M | Flash | SWD/JTAG, UART bootloader/application bootloader | Debug/Flash, wireless stack debug | J-Link, Simplicity Link Debugger | [EFM32][silabs-efm32] |
| Nordic | nRF51/nRF52/nRF53/nRF54 | Arm Cortex-M0/M4/M33 | Flash + UICR | SWD | Debug/Flash, recover, APPROTECT handling | J-Link, nRF DK onboard J-Link OB | [nRF52][nordic-nrf52], [nRF52 DK][nordic-nrf52dk] |
| Nordic | nRF91 | Arm Cortex-M33 + modem | Flash + modem firmware | SWD, UART/USB via DK | Debug/Flash, modem DFU via tools | J-Link, nRF Connect Programmer | [Nordic][nordic-about] |
| Espressif | ESP8266 | Tensilica L106 | externes SPI-Flash + ROM UART bootloader | UART, SPI Flash pins | Firmware Download, externes Flash lesen/schreiben | esptool.py, USB-UART | [ESP32 Datasheet family reference][espressif-esp32] |
| Espressif | ESP32 | Xtensa LX6 | internes ROM + meist externes SPI Flash | UART boot, JTAG | Flashen über UART, Debug über JTAG/OpenOCD | ESP-Prog, FT2232, J-Link teils | [ESP-Prog][esp-prog] |
| Espressif | ESP32-S2/S3/C3/C6/H2/P4 | Xtensa oder RISC-V | ROM + intern/extern Flash je Modell | UART, USB DFU/CDC, USB Serial/JTAG, JTAG | Flashen, Console, JTAG Debug | ESP-Prog, USB Serial/JTAG, OpenOCD | [USB Serial/JTAG][espressif-usbjtag] |
| Raspberry Pi | RP2040 | dual Arm Cortex-M0+ | ROM + externes QSPI Flash | SWD, USB BOOTSEL, QSPI direct | Debug/Flash; UF2/MSC Bootloader | Picoprobe/CMSIS-DAP, J-Link, OpenOCD | [RP2040][raspberrypi-rp2040] |
| Raspberry Pi | RP2350 | Arm Cortex-M33 + RISC-V Hazard3 option | ROM + externes Flash/PSRAM je Board | SWD, USB BOOTSEL, QSPI/PSRAM direct | Debug/Flash, secure boot je Konfiguration | Picoprobe/CMSIS-DAP, J-Link | [RP2350][raspberrypi-rp2350] |
| GigaDevice | GD32 Arm | Arm Cortex-M | Flash + bootloader | SWD/JTAG, UART/USB/CAN boot je Modell | Debug/Flash, ISP | GD-Link, J-Link, OpenOCD teils | [GD32][gigadevice-mcu], [GD-Link][gigadevice-gdlink] |
| GigaDevice | GD32V | RISC-V | Flash | JTAG/SWD-artig je Tool, serial boot | Debug/Flash | GD-Link, J-Link/OpenOCD teils | [GD32][gigadevice-mcu] |
| WCH | CH32V003 | RISC-V QingKe V2A | Flash | 1-wire SDI/RVSWD, UART boot teils | Debug/Download | WCH-LinkE, wlink/openocd forks | [CH32V003][wch-ch32v003], [WCH-LinkE][wch-linke] |
| WCH | CH32V/F/X/H | RISC-V/Arm je Serie | Flash | RVSWD/SWD/JTAG/UART boot je Modell | Debug/Download | WCH-LinkE, OpenOCD forks | [WCH MCU][wch-mcu] |
| MindMotion | MM32 | Arm Cortex-M | Flash | SWD/JTAG, UART boot je Serie | Debug/Flash | J-Link, CMSIS-DAP, vendor ICP | [MM32][mindmotion-mm32] |
| Nuvoton | NuMicro | Arm Cortex-M | Flash/Data Flash/LDROM | SWD, ISP/ICP UART/USB/I²C/SPI je Serie | Debug/Flash, offline programming | Nu-Link, Nu-Link2-Pro, ISP tools | [NuMicro][nuvoton-mcu], [Nu-Link][nuvoton-nulink] |
| Nuvoton | N76E/N78E/N79E 8051 | 8051 | Flash/LDROM/APROM | ICP/ISP, UART boot je Modell | Flashen, Option bytes | Nu-Link/ICP Programmer | [Nuvoton MCU][nuvoton-mcu] |
| Holtek | HT8 Flash | Holtek 8-bit | Flash/EEPROM je Modell | e-Writer/ICP, UART/I²C boot selten modellabhängig | Flashen, Option bytes, Verify | Holtek e-WriterPro/e-Link | [Holtek Flash][holtek-flash] |
| Holtek | HT8 OTP | Holtek 8-bit | OTP | Writer/Sockel/ICP | OTP Programming, Verify | Holtek Writer/Adapter | [Holtek OTP][holtek-otp] |
| Holtek | HT32 | Arm Cortex-M | Flash | SWD/Serial Wire | Debug/Flash | e-Link32, J-Link teils | [HT32][holtek-ht32], [e-Link32][holtek-elink32] |
| ELAN/EMC | EM78P | ELAN 8-bit RISC | OTP | UWTR/DWTR Writer; modellabhängige Pins | OTP Programming, Verify; selten Debug | ELAN UWTR, Adapter/Sockel | [EM78P153K][elan-em78p153k], [UWTR][elan-uwtr] |
| ELAN/EMC | EM78F | ELAN 8-bit RISC | Flash | UWTR/DWTR Writer; modellabhängige Pins | Flash Programming, Verify | ELAN UWTR | [UWTR][elan-uwtr] |
| Padauk | PMS/PMC/PFS/PFC | Padauk 8-bit | OTP/MTP/Flash je Serie | proprietärer Writer/ICE | Programming, erase bei Flash/MTP, Verify | Padauk Writer, Easy-PDK Programmer | [Padauk tools][padauk-tools], [Easy-PDK][easypdkprog] |
| STC | STC8/12/15/32 | 8051-erweitert / 32-bit je Serie | Flash/IAP | UART/USB BSL/ISP | Flashen, Option bytes | STC-ISP, stcgal | [STC][stc-official], [stcgal][stcgal] |
| Sonix | SN8P | Sonix 8-bit | OTP | OTP Writer/Sockel/ICP | OTP Programming, Verify | SN8P OTP Easy Writer | [Sonix OTP Writer][sonix-otpwriter] |
| Sonix | SN8F | Sonix 8-bit Flash | Flash | Flash Writer/ICP | Flash Programming, Debug je Modell | Sonix tools | [Sonix][sonix-sn8p] |
| Megawin | MG82/MG84 | 8051-kompatibel | Flash/IAP | ICP/ISP/UART | Flashen ohne Auslöten, IAP | Writer8_U1Plus, Megawin ISP | [MG82FG5B][megawin-mg82fg5b], [Writer8][megawin-writer8] |
| ABOV | 8-bit M8051 | M8051 | Flash | ICP/ISP/JTAG? modellabhängig | Flash/Debug je Serie | ABOV ISP/debug tools | [ABOV 8-bit][abov-8bit] |
| ABOV | 32-bit A31/A33/A34 | Arm Cortex-M | Flash | SWD/JTAG | Debug/Flash | J-Link/CMSIS-DAP/vendor tools | [ABOV 32-bit][abov-32bit] |
| Toshiba | TXZ/TX | Arm Cortex-M | Flash | SWD/JTAG, UART boot je Serie | Debug/Flash | J-Link, Toshiba tools | [TXZ][toshiba-txz] |
| Analog Devices | MAX32/MAX78 | Arm Cortex-M4 / RISC-V companion je Modell | Flash | SWD/JTAG, UART/USB boot je Modell | Debug/Flash, AI toolchain | MSDK, J-Link/CMSIS-DAP | [ADI MCUs][analog-max32], [MSDK][analog-msdk] |
| ROHM/LAPIS | ML62Q/ML63Q/ML610Q | 16-bit/low power | Flash | On-chip debug, ISP | Flash/debug/emulation | EASE1000 V2 | [ML62Q][rohm-ml62q], [EASE1000][rohm-ease1000] |
| Puya | PY32 | Arm Cortex-M0+/M3/M4 | Flash | SWD, bootloader je Modell | Debug/Flash | J-Link/CMSIS-DAP/vendor tools | [PY32][puya-py32], [PY32F030 RM][puya-py32f030] |

## Literaturverzeichnis

[microchip-icsp]: https://developerhelp.microchip.com/xwiki/bin/view/software-tools/programmers-and-debuggers/pic-and-dspic-downloads/ice4-icsp/
[microchip-pickit5]: https://www.microchip.com/en-us/development-tool/PG164150
[microchip-parametric]: https://www.microchip.com/en-us/products/microcontrollers-and-microprocessors
[avr-interfaces]: https://onlinedocs.microchip.com/oxy/GUID-5A56DB3A-31E1-4F46-984F-39186535C84E-en-US-7/GUID-8A20D003-86A9-45F0-91DD-81467B07AD2A.html
[avr-isp]: https://onlinedocs.microchip.com/oxy/GUID-33422CDF-8B41-417C-9C31-E4521ADAE9B4-en-US-2/GUID-D1F30594-B225-461C-91CC-EF14F6557C01.html
[microchip-updi]: https://onlinedocs.microchip.com/oxy/GUID-7056F141-DF07-46C5-A4B8-97EB46E9B945-en-US-12/GUID-EC6F68EF-2F0D-4D0E-A1FD-D266B695FCFE.html
[microchip-samd]: https://www.microchip.com/en-us/products/microcontrollers-and-microprocessors/32-bit-mcus/sam-32-bit-mcus/sam-d-mcus
[cmsis-dap]: https://arm-software.github.io/CMSIS_5/DAP/html/index.html
[st-stm8swim]: https://www.st.com/resource/en/user_manual/um0470-stm8-swim-communication-protocol-and-debug-module-stmicroelectronics.pdf
[stm-stlinkv3set]: https://www.st.com/en/development-tools/stlink-v3set.html
[st-stm32]: https://www.st.com/en/microcontrollers-microprocessors/stm32-32-bit-arm-cortex-mcus.html
[st-an2606]: https://www.st.com/resource/en/application_note/an2606-stm32-microcontroller-system-memory-boot-mode-stmicroelectronics.pdf
[nxp-mcu]: https://www.nxp.com/products/processors-and-microcontrollers:MICROCONTROLLERS-AND-PROCESSORS
[nxp-mcu-boot]: https://www.nxp.com/docs/en/user-guide/MCUBOOTUM.pdf
[nxp-mculinkpro]: https://www.nxp.com/design/design-center/development-boards-and-designs/mcu-link-pro-debug-probe:MCU-LINK-PRO
[nxp-imxrt]: https://www.nxp.com/products/processors-and-microcontrollers/arm-microcontrollers/i-mx-rt-crossover-mcus:IMX-RT-SERIES
[renesas-rl78]: https://www.renesas.com/en/products/microcontrollers-microprocessors/rl78-low-power-8-16-bit-mcus
[renesas-e2lite]: https://www.renesas.com/en/software-tool/e2-emulator-lite-rte0t0002lkce00000r
[renesas-company]: https://www.renesas.com/en/about/company
[renesas-e2]: https://www.renesas.com/en/software-tool/e2-emulator-rte0t00020kce00000r
[infineon-mcu]: https://www.infineon.com/cms/en/product/microcontroller/
[ti-mspfet]: https://www.ti.com/tool/MSP-FET
[ti-msp430]: https://www.ti.com/lit/ug/slau278/slu278.pdf
[ti-xds110]: https://www.ti.com/tool/TMDSEMU110-U
[silabs-c2]: https://www.silabs.com/documents/public/application-notes/an127.pdf
[silabs-debugger]: https://www.silabs.com/development-tools/mcu/8-bit/8-bit-usb-debug-adapter
[silabs-efm32]: https://www.silabs.com/mcu/32-bit/efm32
[nordic-nrf52]: https://www.nordicsemi.com/Products/nRF52-Series
[nordic-nrf52dk]: https://www.nordicsemi.com/Products/Development-hardware/nRF52-DK
[nordic-about]: https://www.nordicsemi.com/About-us
[espressif-esp32]: https://www.espressif.com/sites/default/files/documentation/esp32_datasheet_en.pdf
[esp-prog]: https://docs.espressif.com/projects/esp-iot-solution/en/latest/hw-reference/ESP-Prog_guide.html
[espressif-usbjtag]: https://docs.espressif.com/projects/esp-idf/en/latest/esp32s3/api-guides/usb-serial-jtag-console.html
[raspberrypi-rp2040]: https://www.raspberrypi.com/products/rp2040/
[raspberrypi-rp2350]: https://www.raspberrypi.com/products/rp2350/
[gigadevice-mcu]: https://www.gigadevice.com/products/microcontrollers/gd32/
[gigadevice-gdlink]: https://www.gigadevice.com/support/downloads/debug-tools/
[wch-ch32v003]: https://www.wch-ic.com/products/CH32V003.html
[wch-linke]: https://www.wch-ic.com/products/WCH-LinkE.html
[wch-mcu]: https://www.wch-ic.com/products/categories/32-bit-microcontroller.html
[mindmotion-mm32]: https://www.mindmotion.com.cn/en/products/mm32mcu/
[nuvoton-mcu]: https://www.nuvoton.com/products/microcontrollers/
[nuvoton-nulink]: https://www.nuvoton.com/tool-and-software/debugger-and-programmer/debugger-and-programmer-tools/numicro-ice-nu-link/
[holtek-flash]: https://www.holtek.com/page/en/8-bit-flash-mcu.html
[holtek-otp]: https://www.holtek.com/page/en/8-bit-otp-mcu.html
[holtek-ht32]: https://www.holtek.com/page/en/32-bit-arm-core-mcu.html
[holtek-elink32]: https://www.holtek.com/page/en/e-link32.html
[elan-em78p153k]: https://www.emc.com.tw/upload/2020_04_202/EM78P153K%20Product%20Spec.%20ver%201.5%20%2820160421%291.pdf
[elan-uwtr]: https://www.emc.com.tw/upload/2019_11_012/NUWTR-AN001-v5.09.00%2820190501%29.pdf
[padauk-tools]: https://www.padauk.com.tw/en/technical/show.aspx?num=4&page=1
[easypdkprog]: https://free-pdk.github.io/easy-pdk-programmer-software/
[stc-official]: https://www.stcmicro.com/
[stcgal]: https://github.com/grigorig/stcgal
[sonix-otpwriter]: https://www.sonix.com.tw/download/SN8P_OTP_Easy_Writer_User_Manual_V1.0_EN.pdf
[sonix-sn8p]: https://www.sonix.com.tw/page-en-1720-5388.html
[megawin-mg82fg5b]: https://www.megawin.com.tw/Files/Product/MG82FG5B/MG82FG5B_Users_Guide_EN.pdf
[megawin-writer8]: https://www.megawin.com.tw/Files/Tool/Writer8_U1Plus/Writer8_U1Plus_Users_Manual.pdf
[abov-8bit]: https://www.abovsemi.com/en/product/8bit-mcu
[abov-32bit]: https://www.abovsemi.com/en/product/32bit-mcu
[toshiba-txz]: https://toshiba.semicon-storage.com/info/docget.jsp?did=68819
[analog-max32]: https://www.analog.com/en/product-category/microcontrollers.html
[analog-msdk]: https://analogdevicesinc.github.io/msdk/USERGUIDE/
[rohm-ml62q]: https://fscdn.rohm.com/en/products/databook/datasheet/ic/micon/low_power/16bit/ml62q1300-e.pdf
[rohm-ease1000]: https://www.rohm.com/products/microcontrollers/tools/ease1000-v2-product
[puya-py32]: https://www.puyasemi.com/en/py32.html
[puya-py32f030]: https://www.puyasemi.com/download_path/%E5%85%AC%E5%8F%B8%E4%BA%A7%E5%93%81%E7%BA%BF/MCU/MCU/PY32F030/Reference%20Manual/PY32F030%20Reference%20Manual%20V1.8.pdf
