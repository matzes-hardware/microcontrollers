# A) MCU-Hersteller und MCU-Serien

Diese Tabelle ist ein **Best-Effort-Katalog** wichtiger aktueller und historisch relevanter MCU-Hersteller/Serien. Die Spalte **Gehäuse** wurde ergänzt und fasst mehrere konkrete Modelle/Ordering-Codes zusammen.

Abkürzungen: **n. ö. b.** = nicht öffentlich serienspezifisch belegt; **NRND** = not recommended for new designs / Legacy; **OTP** = one-time programmable; **MTP** = mehrfach beschreibbar, aber nicht beliebig wie Flash.

| Hersteller | Haupt-Geschäftssitz | Serie / Familie | Fertigungsland/-länder | Strukturbreite | Fertigung seit | ggf. bis / Status | Wiederbeschreibbar / OTP | Gehäuse (zusammenfassend) | Hinweise / Quellen |
|---|---|---|---|---|---:|---|---|---|---|
| Microchip | Chandler, Arizona, USA | PIC10/12/16/18 | n. ö. b.; Microchip besitzt eigene Fabs und nutzt zusätzlich Supply-Chain-Partner | n. ö. b.; nach Generation sehr unterschiedlich | 1970er/1980er bis heute | aktiv + Legacy | Flash/EEPROM; historische OTP-/EPROM-Varianten | SOT-23, DFN, PDIP, SOIC, SSOP, TSSOP, QFN, UQFN, QFP | 8-bit PIC-Familien; Package-Kategorien über Microchip-Selector.[^microchip-pic] |
| Microchip | Chandler, Arizona, USA | PIC24 / dsPIC33 | n. ö. b. | n. ö. b. | ca. 2000er | aktiv | Flash | SPDIP/PDIP, SOIC, SSOP, TSSOP, QFN, UQFN, QFP/BGA je Derivat | 16-bit MCU/DSP-Familien; packages über Parametric Search.[^microchip-parametric] |
| Microchip | Chandler, Arizona, USA | PIC32 | n. ö. b. | n. ö. b. | ca. 2007 | aktiv | Flash | QFN/UQFN, TQFP, LQFP, BGA, WLCSP; wenige ältere SOIC/SSOP-nahe Varianten modellabhängig | MIPS- und Arm-basierte 32-bit-Familien.[^microchip-parametric] |
| Microchip | Chandler, Arizona, USA | AVR tiny/mega/classic, AVR Dx/Ex | n. ö. b. | n. ö. b. | 1990er bis heute | aktiv + Legacy | Flash/EEPROM; wenige OTP/Mask-ROM historische Spezialfälle | SOT-23, DFN, PDIP, SOIC, SSOP, TSSOP, QFN/VQFN | 8-bit AVR; moderne tiny/mega/Dx/Ex nutzen UPDI, ältere oft ISP/debugWIRE.[^microchip-avr][^avr-interfaces] |
| Microchip | Chandler, Arizona, USA | SAM D/L/C/E/V, SAMx5x | n. ö. b. | n. ö. b. | ca. 2010er | aktiv | Flash | SOIC teils bei kleinen SAMD10/11; sonst QFN, TQFP, BGA, WLCSP | Arm Cortex-M0+/M3/M4/M7, Debug meist SWD/JTAG.[^microchip-samd] |
| STMicroelectronics | Genf, Schweiz | STM8 | n. ö. b.; ST betreibt globale Fertigung, konkrete Series-Waferfab meist nicht öffentlich | n. ö. b. | ca. 2007 | aktiv/Legacy je Linie | Flash; einige automotive/consumer Varianten | SOIC/SOP, TSSOP, UFQFPN/QFN, LQFP, WLCSP | 8-bit MCU; SWIM für Programming/Debug.[^st-stm8swim] |
| STMicroelectronics | Genf, Schweiz | STM32C/F/G/L/U/W/H/N | n. ö. b.; ST interne und externe Fertigung je Produkt | STM32H7 offiziell 40 nm; sonst serienspezifisch unterschiedlich/n. ö. b. | 2007 bis heute | aktiv | Flash; TrustZone/secure boot je Serie | SOIC bei einzelnen kleinen Serien, TSSOP, UFQFPN/QFN, LQFP, UFBGA/TFBGA, WLCSP | Arm Cortex-M Portfolio; System-Bootloader via USART/CAN/USB/I²C/SPI je Modell.[^st-stm32][^st-stm32h7][^st-an2606] |
| NXP | Eindhoven, Niederlande | LPC | n. ö. b.; NXP hat globale Fertigung/OSAT-Partner | n. ö. b. | 2000er | aktiv + Legacy | Flash | DIP/SOIC bei LPC1114/kleinen Derivaten; QFN, LQFP, BGA | Arm Cortex-M; ISP/ROM boot und SWD/JTAG je Familie.[^nxp-mcu][^nxp-mcu-boot] |
| NXP | Eindhoven, Niederlande | Kinetis | n. ö. b. | n. ö. b. | ca. 2010 | Legacy/aktiv je Linie | Flash | QFN, LQFP, MAPBGA/WLCSP | Arm Cortex-M; meist SWD/JTAG, ROM-Bootloader je Modell.[^nxp-mcu] |
| NXP | Eindhoven, Niederlande | MCX | n. ö. b. | n. ö. b. | ca. 2023 | aktiv | Flash | HVQFN, LQFP, BGA, WLCSP je Serie | Neue NXP Arm-Cortex-M-Familie; Debug über SWD/JTAG, ISP/MCU Boot je Modell.[^nxp-mcu] |
| NXP | Eindhoven, Niederlande | i.MX RT Crossover MCUs | n. ö. b. | n. ö. b. | ca. 2017 | aktiv | meist externes XiP-Flash + interne RAM/ROM | BGA, LQFP, MAPBGA | Cortex-M7/M33 Crossover MCUs mit ROM-Bootloader.[^nxp-imxrt] |
| NXP | Eindhoven, Niederlande | S32K | n. ö. b. | n. ö. b. | ca. 2017 | aktiv | Flash | LQFP, MAPBGA, BGA | Automotive Arm Cortex-M/R; SWD/JTAG, secure/debug auth modellabhängig.[^nxp-mcu] |
| Renesas | Tokio, Japan | RL78 | Japan; Renesas Semiconductor Manufacturing betreibt Front-End-Fabs in Japan; Assembly/Test je Lieferkette | n. ö. b. | ca. 2010 | aktiv | Flash/Data Flash; sehr alte NEC/78K OTP/Mask-ROM-Vorgänger | SSOP, TSSOP, LSSOP, QFN/HWQFN, LQFP, BGA | Low-power 8/16-bit; Debug/Programming über Renesas Toolchain/E1/E2/E2 Lite.[^renesas-rl78][^renesas-manufacturing] |
| Renesas | Tokio, Japan | RX | Japan/Global; serienspezifisch nicht öffentlich | n. ö. b. | ca. 2009 | aktiv | Flash/Data Flash | LQFP, LFQFP, QFN, BGA/WLBGA | 32-bit Renesas CISC/DSP-Kern; JTAG/FINE/Serial Boot je Modell.[^renesas-company] |
| Renesas | Tokio, Japan | RA | Japan/Global; serienspezifisch nicht öffentlich | n. ö. b. | ca. 2019 | aktiv | Flash/Data Flash | LQFP, QFN, BGA/WLCSP | Arm Cortex-M; SWD/JTAG, SCI/USB/CAN Boot je Serie.[^renesas-company] |
| Renesas | Tokio, Japan | RH850 | Japan/Global; serienspezifisch nicht öffentlich | n. ö. b. | ca. 2012 | aktiv | Flash | LQFP, BGA | Automotive 32-bit; JTAG/LPD und Renesas-Prog/Debug-Ökosystem.[^renesas-company] |
| Infineon | Neubiberg, Deutschland | AURIX TC2xx/TC3xx/TC4x | n. ö. b.; Infineon globale Front-/Back-End-Fertigung | n. ö. b. | ca. 2012 | aktiv | Flash | LQFP, BGA, LFBGA | Automotive TriCore; JTAG/DAP, HSM/security je Modell.[^infineon-mcu] |
| Infineon | Neubiberg, Deutschland | XMC1000/4000 | n. ö. b. | n. ö. b. | ca. 2012 | aktiv/Legacy | Flash | TSSOP, VQFN, LQFP, LFBGA | Arm Cortex-M0/M4; SWD/JTAG.[^infineon-mcu] |
| Infineon | Neubiberg, Deutschland | PSOC 4/5/6, PSOC Control | n. ö. b. | n. ö. b. | 2000er bis heute | aktiv + Legacy | Flash; UDB/analog blocks je Serie | SOIC/TSSOP bei kleinen PSoC; QFN, LQFP, WLCSP, BGA | Arm Cortex-M bzw. ältere M8C; SWD/JTAG/KitProg.[^infineon-mcu] |
| Infineon | Neubiberg, Deutschland | TRAVEO T2G | n. ö. b. | n. ö. b. | ca. 2018 | aktiv | Flash | LQFP, BGA | Automotive Arm Cortex-M; SWD/JTAG.[^infineon-mcu] |
| Texas Instruments | Dallas, Texas, USA | MSP430 / MSP430FR | TI betreibt 15 Fertigungsstandorte weltweit; serienspezifisch n. ö. b. | n. ö. b. | 1990er bis heute | aktiv + Legacy | Flash oder FRAM; ältere OTP/ROM-Varianten | PDIP, SOIC, TSSOP, VQFN, BGA, WLCSP | 16-bit ultra-low-power; JTAG/Spy-Bi-Wire.[^ti-manufacturing][^ti-msp430] |
| Texas Instruments | Dallas, Texas, USA | C2000 | TI global; serienspezifisch n. ö. b. | n. ö. b. | 1990er bis heute | aktiv | Flash/OTP-Zonen je Derivat | LQFP, QFN, BGA | Real-time control MCUs; JTAG/XDS.[^ti-xds110] |
| Texas Instruments | Dallas, Texas, USA | SimpleLink CC13xx/CC26xx/CC32xx | TI global; serienspezifisch n. ö. b. | n. ö. b. | ca. 2010er | aktiv | Flash/ROM; wireless stack in ROM/Flash je Serie | QFN, BGA, WCSP | Arm Cortex-M wireless MCUs; JTAG/SWD/XDS.[^ti-xds110] |
| Texas Instruments | Dallas, Texas, USA | TM4C / Hercules | TI global; serienspezifisch n. ö. b. | n. ö. b. | 2010er | aktiv/Legacy | Flash | LQFP, BGA | Arm Cortex-M4F bzw. Cortex-R; JTAG/SWD.[^ti-xds110] |
| Silicon Labs | Austin, Texas, USA | EFM8 / C8051F | fabless/partner-fertigung; serienspezifisch n. ö. b. | n. ö. b. | 2000er bis heute | aktiv + Legacy | Flash; ältere EPROM/OTP-C8051-Derivate historisch | SOIC, MSOP, QSOP, QFN, TQFP | 8051-MCU; C2/JTAG/USB debug je Serie.[^silabs-c2][^silabs-debugger] |
| Silicon Labs | Austin, Texas, USA | EFM32 / EFR32 | fabless/partner-fertigung; serienspezifisch n. ö. b. | n. ö. b. | ca. 2009 | aktiv | Flash | QFN, QFP, BGA, CSP | Arm Cortex-M; SWD/JTAG, wireless EFR32.[^silabs-efm32] |
| Nordic Semiconductor | Trondheim, Norwegen | nRF51/nRF52 | fabless; serienspezifisch n. ö. b. | nRF52 öffentlich meist 55 nm genannt; offiziell hier n. ö. b. | ca. 2012 | aktiv/Legacy | Flash | QFN, WLCSP, aQFN/BGA je Baustein | Arm Cortex-M BLE/2.4GHz; SWD; DK enthält J-Link OB.[^nordic-about][^nordic-nrf52][^nordic-nrf52dk] |
| Nordic Semiconductor | Trondheim, Norwegen | nRF53/nRF54/nRF91 | fabless; serienspezifisch n. ö. b. | n. ö. b. | ca. 2019 bis heute | aktiv | Flash | QFN, WLCSP/BGA, SiP-Module | Dual-core/wireless/cellular; SWD/J-Link.[^nordic-nrf52] |
| Espressif | Shanghai, China | ESP8266 | fabless; serienspezifisch n. ö. b. | n. ö. b. | ca. 2014 | aktiv/Legacy | externes SPI-Flash | QFN, Module | Wi-Fi MCU; UART-Bootloader; begrenztes Debug.[^espressif-esp32] |
| Espressif | Shanghai, China | ESP32 / ESP32-S/C/H/P | fabless; serienspezifisch n. ö. b. | ESP32 in öffentlichen Quellen oft 40 nm; serienspezifisch verifizieren | ca. 2016 bis heute | aktiv | internes/external Flash je Modell; meist externes SPI/Octal Flash | QFN, Module, SiP | Xtensa oder RISC-V; UART/USB Boot, JTAG/SWD-ähnlich nein; USB-Serial-JTAG bei S3/C3/P4.[^espressif-esp32][^espressif-usbjtag] |
| Raspberry Pi | Cambridge, UK | RP2040 | TSMC; offiziell als Raspberry-Pi-Siliconprodukt dokumentiert | öffentlich häufig 40 nm genannt; für Design ggf. Datenblatt prüfen | 2021 | aktiv | externes QSPI-Flash, ROM-Bootloader | QFN-56 | Dual Arm Cortex-M0+; SWD, USB-BOOTSEL.[^raspberrypi-rp2040] |
| Raspberry Pi | Cambridge, UK | RP2350 | n. ö. b. | n. ö. b. | 2024 | aktiv | externes QSPI/PSRAM je Design, ROM-Bootloader | QFN, Module/Boards | Arm Cortex-M33/RISC-V-Hazard3 optional; SWD/USB Boot.[^raspberrypi-rp2350] |
| GigaDevice | Peking, China | GD32F/E/C/L/G/H/A/W | fabless; serienspezifisch n. ö. b. | n. ö. b. | ca. 2013 | aktiv | Flash | SOP/SOIC bei kleinen Derivaten, QFN, LQFP, BGA, WLCSP | Arm Cortex-M; SWD/JTAG; GD-Link.[^gigadevice-about][^gigadevice-mcu][^gigadevice-gdlink] |
| GigaDevice | Peking, China | GD32V | fabless; serienspezifisch n. ö. b. | n. ö. b. | ca. 2019 | aktiv/Legacy je Linie | Flash | QFN, LQFP, BGA | RISC-V; JTAG/SWD-artige Debug-Tools je Derivat.[^gigadevice-mcu] |
| WCH / Nanjing Qinheng | Nanjing, China | CH32V | fabless/IC-design; serienspezifisch n. ö. b. | n. ö. b. | ca. 2020 | aktiv | Flash | TSSOP/SOP, QFN, LQFP | RISC-V; WCH-Link, RVSWD/1-wire SDI bei CH32V003.[^wch-about][^wch-mcu][^wch-ch32v003][^wch-linke] |
| WCH / Nanjing Qinheng | Nanjing, China | CH32F / CH32X / CH57x/58x | fabless/IC-design; serienspezifisch n. ö. b. | n. ö. b. | 2010er bis heute | aktiv | Flash | SOP/TSSOP, QFN, LQFP, Module | Arm/RISC-V/USB/wireless MCUs; SWD/RVSWD/UART boot je Serie.[^wch-mcu] |
| MindMotion | Shanghai, China | MM32 | fabless/partner-fertigung; serienspezifisch n. ö. b. | n. ö. b. | 2011+ | aktiv | Flash | SOP/TSSOP, QFN, LQFP, BGA | Arm Cortex-M0/M3/M4/M7; SWD/JTAG.[^mindmotion-about][^mindmotion-mm32] |
| Nuvoton | Hsinchu, Taiwan | NuMicro M0/M23/M4/M7, M251/M480/M55M1 usw. | Nuvoton/Winbond-Gruppe; serienspezifisch n. ö. b. | n. ö. b. | 2008+ | aktiv | Flash/Data Flash/LDROM | TSSOP, QFN, LQFP, BGA, WLCSP; teils SOP/SSOP bei kleinen Derivaten | Arm Cortex-M; SWD, ISP/ICP; Nu-Link.[^nuvoton-mcu][^nuvoton-nulink] |
| Nuvoton | Hsinchu, Taiwan | N76E/N78E/N79E 8051 | Taiwan/Partner; serienspezifisch n. ö. b. | n. ö. b. | 2000er bis heute | aktiv/Legacy | Flash; ältere OTP/Mask-ROM-Vorgänger | SOP, SSOP, TSSOP, QFN, LQFP | 8051-kompatibel; ICP/ISP, proprietäre Tools.[^nuvoton-mcu] |
| Holtek | Hsinchu, Taiwan | HT8 Flash MCU | Taiwan/Partner; serienspezifisch n. ö. b. | n. ö. b. | 1990er/2000er bis heute | aktiv | Flash/EEPROM je Modell | SOP/NSOP/SSOP, TSSOP, QFN, QFP | 8-bit Holtek; e-Writer/e-Link/ICP je Modell.[^holtek-flash] |
| Holtek | Hsinchu, Taiwan | HT8 OTP MCU | Taiwan/Partner; serienspezifisch n. ö. b. | n. ö. b. | 1990er bis heute | aktiv/Legacy | OTP | SOP/SSOP, DIP, QFP/QFN je Modell | OTP-/mask-nahe Haushalts-/Consumer-MCUs.[^holtek-otp] |
| Holtek | Hsinchu, Taiwan | HT32 | Taiwan/Partner; serienspezifisch n. ö. b. | n. ö. b. | ca. 2010er | aktiv | Flash | QFN, LQFP, BGA; kleine Gehäuse modellabhängig | Arm Cortex-M; Serial Wire Debug über e-Link32.[^holtek-ht32][^holtek-elink32] |
| ELAN / EMC | Hsinchu, Taiwan | EM78P / EM78F | Taiwan/Partner; serienspezifisch n. ö. b. | n. ö. b. | 1990er bis heute/Legacy | aktiv/Legacy | OTP, Flash je Suffix/Familie | SOP/SOIC, SSOP, DIP, QFP/QFN je Modell | 8-bit ELAN-RISC; UWTR/DWTR Writer; viele OTP-Consumer-MCUs.[^elan-em78p153k][^elan-uwtr] |
| Padauk | Taiwan | PMS/PMC/PFS/PFC | Taiwan/Partner; serienspezifisch n. ö. b. | n. ö. b. | 2000er bis heute | aktiv | OTP, MTP, Flash je Familie | SOT-23, SOP/SOIC, MSOP, DFN/QFN, TSSOP | Ultra-low-cost 8-bit; proprietäre Writer/ICE; freie Easy-PDK-Tools unterstützen Teile der Familie.[^padauk-pfs122b][^padauk-tools][^easypdkprog] |
| STCmicro | Shenzhen/China, öffentlich n. ö. b. | STC8/STC12/STC15/STC32 | n. ö. b. | n. ö. b. | 2000er bis heute | aktiv | Flash/IAP/ISP | DIP, SOP/SOIC, SSOP, TSSOP, LQFP, QFN | 8051-/8051-erweiterte und 32-bit-Derivate; UART/USB ISP via Bootloader.[^stc-official][^stcgal] |
| Sonix | Taiwan | SN8P / SN8F | Taiwan/Partner; serienspezifisch n. ö. b. | n. ö. b. | 1990er/2000er bis heute | aktiv/Legacy | OTP oder Flash | SOP/SOIC, SSOP, DIP, QFP/QFN je Modell | 8-bit Consumer-MCUs; OTP Easy Writer, ICE/Writer.[^sonix-sn8p][^sonix-otpwriter] |
| Megawin | Taiwan | MG82/MG84/MG32/MPC/MG88051 | Taiwan/Partner; serienspezifisch n. ö. b. | n. ö. b. | 2000er bis heute | aktiv/Legacy | Flash/IAP/ICP/ISP | SOP/SOIC, TSSOP, SSOP, QFN, LQFP | 8051- und 32-bit-MCUs; Writer8_U1Plus/ICP/ISP.[^megawin-mg82fg5b][^megawin-writer8] |
| ABOV Semiconductor | Südkorea | A96/MG/MH 8-bit | Südkorea/Partner; serienspezifisch n. ö. b. | n. ö. b. | 2000er bis heute | aktiv | Flash/EEPROM; ältere OTP möglich | SOP/SOIC, TSSOP, QFN, LQFP | 8051/M8051-basierte 8-bit-MCUs.[^abov-8bit] |
| ABOV Semiconductor | Südkorea | A31/A33/A34/A35 32-bit | Südkorea/Partner; serienspezifisch n. ö. b. | n. ö. b. | 2010er bis heute | aktiv | Flash | QFN, LQFP, BGA je Serie | Arm Cortex-M MCUs.[^abov-32bit] |
| Toshiba | Tokio, Japan | TX03/TX04/TXZ/TMPM/TMP89 | Japan/Global; serienspezifisch n. ö. b. | n. ö. b. | 2000er bis heute/Legacy | aktiv + Legacy | Flash; ältere mask-ROM/OTP-Varianten | SOP/SSOP bei kleinen 8-bit; QFN, LQFP, BGA bei 32-bit | Arm Cortex-M-basierte TXZ und 8-bit/16-bit Vorgänger; Serial/JTAG/SWD je Modell.[^toshiba-txz] |
| Analog Devices / Maxim Integrated | Wilmington, Massachusetts, USA | MAX32xxx / MAX78xxx | ADI globale Fertigung/Partner; serienspezifisch n. ö. b. | n. ö. b. | 2010er bis heute | aktiv | Flash | TQFN, WLP, BGA, LQFP je Modell | Arm Cortex-M4/RISC-V/AI-MCUs; MSDK/JTAG/SWD.[^analog-max32][^analog-msdk] |
| ROHM / LAPIS Technology | Kyoto, Japan | ML62Q/ML63Q/ML610Q/ML620Q | Japan/Partner; serienspezifisch n. ö. b. | n. ö. b. | 2000er bis heute | aktiv/Legacy | Flash; einige mask/OTP-Vorgänger | SOP/SSOP, TQFP, WQFN, BGA je Serie | Low-power 8/16/32-bit; on-chip debug/ISP, EASE1000.[^rohm-ml62q][^rohm-ease1000] |
| Generalplus | Hsinchu, Taiwan | GPL/GPM/GPCE consumer MCUs | Taiwan/Partner; serienspezifisch n. ö. b. | n. ö. b. | 1990er/2000er bis heute | aktiv/Legacy | OTP/MTP/Flash je Serie | SOP/SOIC, SSOP, QFP/QFN, COB/Die | Voice/toy/consumer-MCUs; häufig OTP/Mask-ROM-nahe.[^generalplus][^generalplus-gpl192c] |
| Puya Semiconductor | China | PY32 | fabless/partner-fertigung; serienspezifisch n. ö. b. | n. ö. b. | 2020er | aktiv | Flash | SOP/TSSOP, QFN, LQFP | Arm Cortex-M0+/M3/M4 je Serie; SWD/Bootloader je Modell.[^puya-py32][^puya-py32f030] |

## Literaturverzeichnis

[^microchip-pic]: [Microchip PIC MCUs][microchip-pic]
[^microchip-parametric]: [Microchip MCU/MPU products and selector][microchip-parametric]
[^microchip-avr]: [Microchip AVR MCUs][microchip-avr]
[^avr-interfaces]: [Microchip AVR target interfaces][avr-interfaces]
[^microchip-samd]: [Microchip SAM D MCUs][microchip-samd]
[^st-stm8swim]: [ST STM8 SWIM communication protocol and debug module][st-stm8swim]
[^st-stm32]: [ST STM32 32-bit Arm Cortex MCUs][st-stm32]
[^st-stm32h7]: [ST STM32H7 series, 40 nm note][st-stm32h7]
[^st-an2606]: [ST AN2606 STM32 bootloader interfaces][st-an2606]
[^nxp-mcu]: [NXP processors and microcontrollers][nxp-mcu]
[^nxp-mcu-boot]: [NXP MCU Bootloader User Guide][nxp-mcu-boot]
[^nxp-imxrt]: [NXP i.MX RT crossover MCUs][nxp-imxrt]
[^renesas-rl78]: [Renesas RL78 low-power 8/16-bit MCUs][renesas-rl78]
[^renesas-manufacturing]: [Renesas Semiconductor Manufacturing front-end factories][renesas-manufacturing]
[^renesas-company]: [Renesas company and product information][renesas-company]
[^infineon-mcu]: [Infineon microcontroller portfolio][infineon-mcu]
[^ti-manufacturing]: [TI manufacturing sites][ti-manufacturing]
[^ti-msp430]: [TI MSP430 Hardware Tools User's Guide][ti-msp430]
[^ti-xds110]: [TI XDS110 Debug Probe][ti-xds110]
[^silabs-c2]: [Silicon Labs AN127 C2 interface][silabs-c2]
[^silabs-debugger]: [Silicon Labs 8-bit USB Debug Adapter][silabs-debugger]
[^silabs-efm32]: [Silicon Labs EFM32 MCUs][silabs-efm32]
[^nordic-about]: [Nordic Semiconductor about us][nordic-about]
[^nordic-nrf52]: [Nordic nRF52 series][nordic-nrf52]
[^nordic-nrf52dk]: [Nordic nRF52 DK][nordic-nrf52dk]
[^espressif-esp32]: [Espressif ESP32 datasheet][espressif-esp32]
[^espressif-usbjtag]: [Espressif USB Serial/JTAG Console][espressif-usbjtag]
[^raspberrypi-rp2040]: [Raspberry Pi RP2040][raspberrypi-rp2040]
[^raspberrypi-rp2350]: [Raspberry Pi RP2350][raspberrypi-rp2350]
[^gigadevice-about]: [GigaDevice about][gigadevice-about]
[^gigadevice-mcu]: [GigaDevice GD32 MCUs][gigadevice-mcu]
[^gigadevice-gdlink]: [GigaDevice GD-Link debug tools][gigadevice-gdlink]
[^wch-about]: [WCH about][wch-about]
[^wch-mcu]: [WCH 32-bit MCU products][wch-mcu]
[^wch-ch32v003]: [WCH CH32V003][wch-ch32v003]
[^wch-linke]: [WCH-LinkE][wch-linke]
[^mindmotion-about]: [MindMotion about][mindmotion-about]
[^mindmotion-mm32]: [MindMotion MM32 MCU products][mindmotion-mm32]
[^nuvoton-mcu]: [Nuvoton microcontrollers][nuvoton-mcu]
[^nuvoton-nulink]: [Nuvoton Nu-Link][nuvoton-nulink]
[^holtek-flash]: [Holtek 8-bit Flash MCU][holtek-flash]
[^holtek-otp]: [Holtek 8-bit OTP MCU][holtek-otp]
[^holtek-ht32]: [Holtek 32-bit Arm-core MCU][holtek-ht32]
[^holtek-elink32]: [Holtek e-Link32][holtek-elink32]
[^elan-em78p153k]: [ELAN/EMC EM78P153K datasheet][elan-em78p153k]
[^elan-uwtr]: [ELAN/EMC NUWTR Writer System][elan-uwtr]
[^padauk-pfs122b]: [Padauk PFS122B datasheet][padauk-pfs122b]
[^padauk-tools]: [Padauk technical/downloads][padauk-tools]
[^easypdkprog]: [Easy PDK Programmer software][easypdkprog]
[^stc-official]: [STCmicro official site][stc-official]
[^stcgal]: [stcgal open-source STC ISP tool][stcgal]
[^sonix-sn8p]: [Sonix SN8P OTP MCU product page][sonix-sn8p]
[^sonix-otpwriter]: [Sonix OTP Easy Writer user manual][sonix-otpwriter]
[^megawin-mg82fg5b]: [Megawin MG82FG5B User Guide][megawin-mg82fg5b]
[^megawin-writer8]: [Megawin Writer8_U1Plus User Manual][megawin-writer8]
[^abov-8bit]: [ABOV 8-bit MCU products][abov-8bit]
[^abov-32bit]: [ABOV 32-bit MCU products][abov-32bit]
[^toshiba-txz]: [Toshiba TXZ flash/programming documentation][toshiba-txz]
[^analog-max32]: [Analog Devices microcontrollers][analog-max32]
[^analog-msdk]: [Analog Devices MSDK user guide][analog-msdk]
[^rohm-ml62q]: [ROHM/LAPIS ML62Q1300 datasheet][rohm-ml62q]
[^rohm-ease1000]: [ROHM EASE1000 V2][rohm-ease1000]
[^generalplus]: [Generalplus products][generalplus]
[^generalplus-gpl192c]: [Generalplus GPL192C][generalplus-gpl192c]
[^puya-py32]: [Puya PY32 MCUs][puya-py32]
[^puya-py32f030]: [Puya PY32F030 Reference Manual][puya-py32f030]

[microchip-pic]: https://www.microchip.com/en-us/products/microcontrollers-and-microprocessors/8-bit-mcus/pic-mcus
[microchip-parametric]: https://www.microchip.com/en-us/products/microcontrollers-and-microprocessors
[microchip-avr]: https://www.microchip.com/en-us/products/microcontrollers-and-microprocessors/8-bit-mcus/avr-mcus
[avr-interfaces]: https://onlinedocs.microchip.com/oxy/GUID-5A56DB3A-31E1-4F46-984F-39186535C84E-en-US-7/GUID-8A20D003-86A9-45F0-91DD-81467B07AD2A.html
[microchip-samd]: https://www.microchip.com/en-us/products/microcontrollers-and-microprocessors/32-bit-mcus/sam-32-bit-mcus/sam-d-mcus
[st-stm8swim]: https://www.st.com/resource/en/user_manual/um0470-stm8-swim-communication-protocol-and-debug-module-stmicroelectronics.pdf
[st-stm32]: https://www.st.com/en/microcontrollers-microprocessors/stm32-32-bit-arm-cortex-mcus.html
[st-stm32h7]: https://www.st.com/en/microcontrollers-microprocessors/stm32h7-series.html
[st-an2606]: https://www.st.com/resource/en/application_note/an2606-stm32-microcontroller-system-memory-boot-mode-stmicroelectronics.pdf
[nxp-mcu]: https://www.nxp.com/products/processors-and-microcontrollers:MICROCONTROLLERS-AND-PROCESSORS
[nxp-mcu-boot]: https://www.nxp.com/docs/en/user-guide/MCUBOOTUM.pdf
[nxp-imxrt]: https://www.nxp.com/products/processors-and-microcontrollers/arm-microcontrollers/i-mx-rt-crossover-mcus:IMX-RT-SERIES
[renesas-rl78]: https://www.renesas.com/en/products/microcontrollers-microprocessors/rl78-low-power-8-16-bit-mcus
[renesas-manufacturing]: https://www.renesas.com/en/about/company/renesas-semiconductor-manufacturing-co-ltd
[renesas-company]: https://www.renesas.com/en/about/company
[infineon-mcu]: https://www.infineon.com/cms/en/product/microcontroller/
[ti-manufacturing]: https://www.ti.com/about-ti/company/manufacturing.html
[ti-msp430]: https://www.ti.com/lit/ug/slau278/slu278.pdf
[ti-xds110]: https://www.ti.com/tool/TMDSEMU110-U
[silabs-c2]: https://www.silabs.com/documents/public/application-notes/an127.pdf
[silabs-debugger]: https://www.silabs.com/development-tools/mcu/8-bit/8-bit-usb-debug-adapter
[silabs-efm32]: https://www.silabs.com/mcu/32-bit/efm32
[nordic-about]: https://www.nordicsemi.com/About-us
[nordic-nrf52]: https://www.nordicsemi.com/Products/nRF52-Series
[nordic-nrf52dk]: https://www.nordicsemi.com/Products/Development-hardware/nRF52-DK
[espressif-esp32]: https://www.espressif.com/sites/default/files/documentation/esp32_datasheet_en.pdf
[espressif-usbjtag]: https://docs.espressif.com/projects/esp-idf/en/latest/esp32s3/api-guides/usb-serial-jtag-console.html
[raspberrypi-rp2040]: https://www.raspberrypi.com/products/rp2040/
[raspberrypi-rp2350]: https://www.raspberrypi.com/products/rp2350/
[gigadevice-about]: https://www.gigadevice.com/about/about-gigadevice/
[gigadevice-mcu]: https://www.gigadevice.com/products/microcontrollers/gd32/
[gigadevice-gdlink]: https://www.gigadevice.com/support/downloads/debug-tools/
[wch-about]: https://www.wch-ic.com/about_us.html
[wch-mcu]: https://www.wch-ic.com/products/categories/32-bit-microcontroller.html
[wch-ch32v003]: https://www.wch-ic.com/products/CH32V003.html
[wch-linke]: https://www.wch-ic.com/products/WCH-LinkE.html
[mindmotion-about]: https://www.mindmotion.com.cn/en/about/index.aspx
[mindmotion-mm32]: https://www.mindmotion.com.cn/en/products/mm32mcu/
[nuvoton-mcu]: https://www.nuvoton.com/products/microcontrollers/
[nuvoton-nulink]: https://www.nuvoton.com/tool-and-software/debugger-and-programmer/debugger-and-programmer-tools/numicro-ice-nu-link/
[holtek-flash]: https://www.holtek.com/page/en/8-bit-flash-mcu.html
[holtek-otp]: https://www.holtek.com/page/en/8-bit-otp-mcu.html
[holtek-ht32]: https://www.holtek.com/page/en/32-bit-arm-core-mcu.html
[holtek-elink32]: https://www.holtek.com/page/en/e-link32.html
[elan-em78p153k]: https://www.emc.com.tw/upload/2020_04_202/EM78P153K%20Product%20Spec.%20ver%201.5%20%2820160421%291.pdf
[elan-uwtr]: https://www.emc.com.tw/upload/2019_11_012/NUWTR-AN001-v5.09.00%2820190501%29.pdf
[padauk-pfs122b]: https://www.padauk.com.tw/upload/doc/PFS122B%20datasheet%20V004_EN_20240401.pdf
[padauk-tools]: https://www.padauk.com.tw/en/technical/show.aspx?num=4&page=1
[easypdkprog]: https://free-pdk.github.io/easy-pdk-programmer-software/
[stc-official]: https://www.stcmicro.com/
[stcgal]: https://github.com/grigorig/stcgal
[sonix-sn8p]: https://www.sonix.com.tw/page-en-1720-5388.html
[sonix-otpwriter]: https://www.sonix.com.tw/download/SN8P_OTP_Easy_Writer_User_Manual_V1.0_EN.pdf
[megawin-mg82fg5b]: https://www.megawin.com.tw/Files/Product/MG82FG5B/MG82FG5B_Users_Guide_EN.pdf
[megawin-writer8]: https://www.megawin.com.tw/Files/Tool/Writer8_U1Plus/Writer8_U1Plus_Users_Manual.pdf
[abov-8bit]: https://www.abovsemi.com/en/product/8bit-mcu
[abov-32bit]: https://www.abovsemi.com/en/product/32bit-mcu
[toshiba-txz]: https://toshiba.semicon-storage.com/info/docget.jsp?did=68819
[analog-max32]: https://www.analog.com/en/product-category/microcontrollers.html
[analog-msdk]: https://analogdevicesinc.github.io/msdk/USERGUIDE/
[rohm-ml62q]: https://fscdn.rohm.com/en/products/databook/datasheet/ic/micon/low_power/16bit/ml62q1300-e.pdf
[rohm-ease1000]: https://www.rohm.com/products/microcontrollers/tools/ease1000-v2-product
[generalplus]: https://www.generalplus.com/products/
[generalplus-gpl192c]: https://www.generalplus.com/product/GPL192C
[puya-py32]: https://www.puyasemi.com/en/py32.html
[puya-py32f030]: https://www.puyasemi.com/download_path/%E5%85%AC%E5%8F%B8%E4%BA%A7%E5%93%81%E7%BA%BF/MCU/MCU/PY32F030/Reference%20Manual/PY32F030%20Reference%20Manual%20V1.8.pdf
