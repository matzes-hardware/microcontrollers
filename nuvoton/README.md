# Nuvoton

Eingeschlossen wurden Herstellerbezeichnungen der SOIC-Familie: SOP, NSOP, SSOP sowie EP-Varianten. Ausgeschlossen wurden TSSOP, MSOP, QFN, LQFP, DIP/PDIP und reine Bare-Die/COB-Varianten.

Nuvoton ist anhand der Nuvoton Low-Pin-Count-8051-Produktseiten und Datenblätter erfasst.

Pinout-Dateien liegen als `<mcu-modell>x.md` im Herstellerordner (ein Dokument pro MCU-Familie mit Legenden und `## Pinbelegung` / `###` je Gehäuse).

## N79 Low Pin Count 8051

| Modell | Gehäuse | Datenblatt / Download-Link |
|---|---:|---|
| N79E715AS16 | SOP-16 | https://www.nuvoton.com/export/resource-files/DS_N79E715_EN_Rev1.01.pdf |
| N79E715AS20 | SOP-20 | https://www.nuvoton.com/export/resource-files/DS_N79E715_EN_Rev1.01.pdf |
| N79E715AS28 | SOP-28 | https://www.nuvoton.com/export/resource-files/DS_N79E715_EN_Rev1.01.pdf |
| N79E8132AS16 | SOP-16 | https://www.nuvoton.com/export/resource-files/N79E815A_814A_8132A_datasheet_A2.1_SC5.pdf |
| N79E814AS20 | SOP-20 | https://www.nuvoton.com/export/resource-files/N79E815A_814A_8132A_datasheet_A2.1_SC5.pdf |
| N79E814AS28 | SOP-28 | https://www.nuvoton.com/export/resource-files/N79E815A_814A_8132A_datasheet_A2.1_SC5.pdf |
| N79E815AS20 | SOP-20 | https://www.nuvoton.com/export/resource-files/N79E815A_814A_8132A_datasheet_A2.1_SC5.pdf |
| N79E815AS28 | SOP-28 | https://www.nuvoton.com/export/resource-files/N79E815A_814A_8132A_datasheet_A2.1_SC5.pdf |
| N79E8432ASG | SOP-16 | https://www.nuvoton.com/export/resource-files/N79E845_844_8432_Data_Sheet_A2.6.pdf |
| N79E854ASG | SOP-28 | https://www.nuvoton.com/export/resource-files/N79E855_854_Data_Sheet_A2.5.pdf (Pinout: TSSOP/SOP 28-pin; Teileliste im PDF nennt nur AWG/TSSOP, Produktseite nennt SOP28 - verifizieren) |
| N79E855ASG | SOP-28 | https://www.nuvoton.com/export/resource-files/N79E855_854_Data_Sheet_A2.5.pdf (Pinout: TSSOP/SOP 28-pin; Teileliste im PDF nennt nur AWG/TSSOP, Produktseite nennt SOP28 - verifizieren) |
| N79E822ASG | SOP-20 | Hersteller-Produktseite/Downloadbereich: https://www.nuvoton.com/products/microcontrollers/8bit-8051-mcus/low-pin-count-8051-series/n79e822/ |
| N79E823ASG | SOP-20 | https://www.nuvoton.com/products/microcontrollers/8bit-8051-mcus/low-pin-count-8051-series/n79e823/ |
| N79E824ASG | SOP-20 | Hersteller-Produktseite/Downloadbereich: https://www.nuvoton.com/products/microcontrollers/8bit-8051-mcus/low-pin-count-8051-series/n79e824/ |
| N79E825ASG | SOP-20 | Hersteller-Produktseite/Downloadbereich: https://www.nuvoton.com/products/microcontrollers/8bit-8051-mcus/low-pin-count-8051-series/n79e825/ |

## Weitere Serien

| Serie | Modell | Gehäuse | Datenblatt / Download-Link |
|---|---|---:|---|
| W79 Low Pin Count 8051 | W79E2051ASG | SOP-20 | https://www.nuvoton.com/products/microcontrollers/8bit-8051-mcus/low-pin-count-8051-series/w79e2051/ |
| W79 Low Pin Count 8051 | W79E4051ASG | SOP-20 | https://www.nuvoton.com/products/microcontrollers/8bit-8051-mcus/low-pin-count-8051-series/w79e4051/ |

## Noch zu prüfen / bekannte Einschränkungen

- Nuvoton N79E854/N79E855: Produktseiten/Distribution führen SOP28; das Datenblatt A2.5 zeigt das 28-pin Pinout als TSSOP/SOP, die Parts-Information-Liste im PDF nennt jedoch AWG/TSSOP. In der Tabelle sind ASG/SOP28 deshalb als zu verifizieren gekennzeichnet.

## Pinout-Recherche

Stand: 2026-06-15.

| Modell | Gehäuse | Pins | Status | Datei |
|---|---|---:|---|---|
| N79E715AS16 | SOP | 16 | extrahiert | `n79e715x.md` |
| N79E715AS20 | SOP | 20 | extrahiert | `n79e715x.md` |
| N79E715AS28 | SOP | 28 | extrahiert | `n79e715x.md` |
| N79E8132AS16 | SOP | 16 | extrahiert | `n79e8132x.md` |
| N79E814AS20 | SOP | 20 | extrahiert | `n79e814x.md` |
| N79E814AS28 | SOP | 28 | extrahiert | `n79e814x.md` |
| N79E815AS20 | SOP | 20 | extrahiert | `n79e815x.md` |
| N79E815AS28 | SOP | 28 | extrahiert | `n79e815x.md` |
| N79E8432ASG | SOP | 16 | extrahiert | `n79e8432x.md` |
| N79E854ASG | SOP | 28 | extrahiert | `n79e854x.md` |
| N79E855ASG | SOP | 28 | extrahiert | `n79e855x.md` |
| N79E823ASG | SOP | 20 | offen | `n79e823x.md` |
| W79E2051ASG | SOP | 20 | offen | `w79e2051x.md` |
| W79E4051ASG | SOP | 20 | offen | `w79e4051x.md` |

### Zusammenfassung
- Tabellenzeilen: 14
- Pinbelegungen extrahiert: 11
- weiterhin offen/unklar: 3
