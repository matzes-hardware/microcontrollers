# MCU-Recherche: Hersteller, Serien, Schnittstellen und Programmer

Stand: **2026-05-02**. Sprache: Deutsch. Ergebnisformat: Markdown-Dateien.

## Dateien

| Datei | Inhalt |
|---|---|
| `01_mcu_hersteller_serien.md` | Best-Effort-Katalog wichtiger MCU-Hersteller und -Serien; enthält die ergänzte Spalte **Gehäuse**. |
| `02_schnittstellen_protokolle.md` | Herstellerübergreifende Übersicht physischer Flash-/Debug-Schnittstellen und darauf genutzter Protokolle. |
| `03_schnittstellen_elektrik.md` | Elektrische Eigenschaften typischer MCU-seitiger Pins je Schnittstelle. |
| `04_schnittstellen_nach_mcu_serien.md` | Zuordnung von Schnittstellen/Protokollen zu Hersteller-Serien und Beispielmodellen. |
| `05_programmer_debugger.md` | Off-the-shelf Programmer/Debugger mit unterstützten Schnittstellen, Protokollen und Funktionen. |
| `99_quellen.md` | Aggregiertes Quellenverzeichnis. |

## Abgrenzung und Qualitätshinweise

- „Alle Hersteller“ ist in der MCU-Welt nicht abschließend erfüllbar: Es gibt viele historische, kundenspezifische, mask-ROM- und regionale Hersteller/ASIC-Derivate. Die Tabellen sind daher ein **breiter, praxisorientierter Best-Effort-Katalog** der gut dokumentierten, im Feld realistisch anzutreffenden Hersteller und Serien.
- **Fertigungsland/-länder** und **Strukturbreite** sind bei vielen MCU-Serien nicht öffentlich serienspezifisch belegt. Wo keine verlässliche öffentliche Angabe gefunden wurde, steht ausdrücklich „nicht öffentlich serienspezifisch belegt“ statt einer Schätzung.
- **Gehäuse** fasst Serienvarianten zusammen und ist nicht als vollständige Ordering-Code-Liste zu verstehen. Beispiel: „SOIC/SOP, SSOP, TSSOP, QFN, QFP“ bedeutet, dass diese Gehäusearten in der Serie/Familie vorkommen oder vom Hersteller-Selector als Package-Kategorien geführt werden; einzelne Modelle können abweichen.
- „Wiederbeschreibbar/OTP“ beschreibt den Programmspeicher-Typ auf Serienebene: Flash/FRAM/EEPROM-basierte MCUs sind typischerweise wiederbeschreibbar; OTP-/EPROM-/mask-ROM-Typen nur eingeschränkt oder gar nicht.

## Besonders relevante Quellen

- Microchip MCU-Parametric Search listet package-Kategorien wie PDIP, SOIC, SSOP, TSSOP, QFN, TQFP, BGA und WLCSP.[^microchip-parametric]
- ST beschreibt STM32 als Arm-Cortex-M-basiertes Portfolio und dokumentiert Bootloader-Schnittstellen in AN2606.[^st-stm32][^st-an2606]
- Arm dokumentiert ADI/SWD/CoreSight als Basis vieler moderner Debug-Protokolle.[^arm-adi]
- Microchip dokumentiert ICSP, UPDI, debugWIRE und AVR-Programmierschnittstellen in den Developer-Help- und Online-Docs.[^microchip-icsp][^microchip-updi][^microchip-debugwire][^avr-interfaces]
- ELAN/EMC UWTR ist die relevante Writer-Umgebung für viele EM78-OTP/Flash-Chips.[^elan-uwtr]

[^microchip-parametric]: [Microchip MCU and MPU products][microchip-parametric]
[^st-stm32]: [ST STM32 32-bit Arm Cortex MCUs][st-stm32]
[^st-an2606]: [ST AN2606 STM32 system memory boot mode][st-an2606]
[^arm-adi]: [Arm Debug Interface Architecture Specification][arm-adi]
[^microchip-icsp]: [Microchip ICSP programming/debugging signals][microchip-icsp]
[^microchip-updi]: [Microchip UPDI overview][microchip-updi]
[^microchip-debugwire]: [Microchip debugWIRE overview][microchip-debugwire]
[^avr-interfaces]: [Microchip AVR target interfaces][avr-interfaces]
[^elan-uwtr]: [ELAN/EMC NUWTR Writer System][elan-uwtr]

[microchip-parametric]: https://www.microchip.com/en-us/products/microcontrollers-and-microprocessors
[st-stm32]: https://www.st.com/en/microcontrollers-microprocessors/stm32-32-bit-arm-cortex-mcus.html
[st-an2606]: https://www.st.com/resource/en/application_note/an2606-stm32-microcontroller-system-memory-boot-mode-stmicroelectronics.pdf
[arm-adi]: https://developer.arm.com/documentation/ihi0031/latest/
[microchip-icsp]: https://developerhelp.microchip.com/xwiki/bin/view/software-tools/programmers-and-debuggers/pic-and-dspic-downloads/ice4-icsp/
[microchip-updi]: https://onlinedocs.microchip.com/oxy/GUID-7056F141-DF07-46C5-A4B8-97EB46E9B945-en-US-12/GUID-EC6F68EF-2F0D-4D0E-A1FD-D266B695FCFE.html
[microchip-debugwire]: https://onlinedocs.microchip.com/oxy/GUID-DDB0017E-84E3-4E77-AAE9-7AC4290E5E8B-en-US-4/GUID-7F2A4E92-8D08-4BA1-B705-1618F7EFBFC2.html
[avr-interfaces]: https://onlinedocs.microchip.com/oxy/GUID-5A56DB3A-31E1-4F46-984F-39186535C84E-en-US-7/GUID-8A20D003-86A9-45F0-91DD-81467B07AD2A.html
[elan-uwtr]: https://www.emc.com.tw/upload/2019_11_012/NUWTR-AN001-v5.09.00%2820190501%29.pdf
