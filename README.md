# Aktīvās kontroles raķetes avionikas sistēma

## Projekta apraksts
Šis projekts paredz aktīvās kontroles raķetes avionikas sistēmas izstrādi, kas ietver gan raķetē iebūvētu avionikas datoru, gan zemes bāzi datu saņemšanai, uzglabāšanai un analīzei. Sistēma nodrošina aktīvu trajektorijas korekciju reāllaikā, izmantojot sensoru datus, vadības algoritmus un elektroniskos izpildmehānismus.

Projektā tiek apvienotas iegultās sistēmas, signālu apstrāde, vadības algoritmi, telemetrija un lietotāja saskarnes izstrāde.

**Projektu izstrādā:**  
Aleksandrs Jesiļevskis  
Miks Balodis  

---

## Projekta mērķis
Izstrādāt:
- raķetes avionikas datoru ar aktīvas trajektorijas korekcijas iespējām,
- zemes bāzi lidojuma datu saņemšanai un analīzei,
- drošu un papildināmu sistēmu, kas piemērota eksperimentālām lieljaudas raķetēm.

Sistēmai jāspēj:
- reāllaikā noteikt raķetes stāvokli,
- veikt aktīvo vadību ar vairākām kontroles spurām,
- ierakstīt un uzglabāt lidojuma datus,
- nodrošināt saziņu ar zemes bāzi lidojuma laikā.

---

## Idejas rašanās
Ideja radās, balstoties uz **RTU Lieljaudas raķeškomandas (RTU HPR)** 2025. gada 1. semestra projektu – aktīvās rotācijas kontroles raķeti. Šī projekta ietvaros tika izmantots RP2040 mikrokontrolieris, kuram konstatēti vairāki ierobežojumi:
- nav iebūvēta peldošā komata vienības (FPU),
- ierobežota programmas atmiņa,
- augsts enerģijas patēriņš.

Lai šos trūkumus novērstu, projektā tiek izvēlēts **STM32F405RGT6**, kas nodrošina augstāku veiktspēju, FPU atbalstu un DSP instrukcijas.

---

## Idejas apraksts

### Projekta lietotāji
- studentu raķešu komandas,
- augstskolu/vidusskolu eksperimentēšanas grupas,
- iegulto sistēmu un vadības algoritmu izstrādātāji,
- eksperimentālu raķešu un bezpilota sistēmu entuziasti.

### Izmantotās tehnoloģijas
- **Iegultās sistēmas:** STM32 (ARM Cortex-M4)
- **Sensori:** barometrs, IMU, GNSS
- **Vadības algoritmi:** PID, Kalmana filtrs
- **Telemetrija:** sub-GHz radio sakari
- **Programmatūra:** C/C++, MatLab/Simulink (simulācijas), JavaScript un Svelte (GUI)
- **Projektēšana:** KiCad

### Piegādes formāts
Projekta rezultāts būs:
- raķetes avionikas sistēmas plate (PCB),
- iegultā programmatūra gatava demonstratīvam raķetes lidojumam (firmware),
- zemes bāzes programmatūra (GUI),
- dokumentācija.

Šāda pieeja ļauj sistēmu izmantot gan eksperimentālos lidojumos, gan simulācijās.

---

## Aktīvā kontrole
Aktīvā kontrole ir vadības sistēma, kas lidojuma laikā nepārtraukti:
- mēra raķetes stāvokli (leņķi, ātrumu, rotāciju),
- aprēķina nepieciešamos labojumus,
- ģenerē PWM signālus izpildmehānismiem servo kontrolētām spurām.

Sistēma atbalsta līdz **4 aktīvām spurām**, katrai paredzot atsevišķu PWM kanālu. Salīdzinājumā ar pasīvo kontroli, aktīvā kontrole spēj reaģēt uz ārējiem traucējumiem un uzlabot stabilitāti un precizitāti.

---

## Risinājuma arhitektūra

### Konceptuālais modelis
Sistēma sastāv no trim galvenajiem blokiem:
1. **Sensoru slānis** – datu iegūšana
2. **Vadības un apstrādes slānis** – aprēķini un lēmumu pieņemšana
3. **Izpildes un komunikācijas slānis** – kontrole, datu uzglabāšana un pārraide

### Tehniskā arhitektūra

#### MCU
- **STM32F405RGT6** - mikrokontrolieris datu apstrādei un komandu nodošanai

#### Sensori
- **BMP388** – barometrs augstuma noteikšanai
- **LSM6DSO** – IMU (akselerometrs + žiroskops)
- **MAX-M10S** – GNSS modulis augstas precizitātes pozīcijai

#### Datu uzglabāšana
- **W25Q32JV** – lidojuma datu ierakstīšanai (USB Mass Storage režīms)
- **24LC64 EEPROM** – konfigurācijas datiem

#### Telemetrija
- **EBYTE E22-400M22S** - LoRa moudlis saziņai ar zemes bāzi (433 MHz)

#### Vadība
- PWM signāli spuru servo
- PID regulators
- Kalmana filtrs stāvokļa novērtēšanai

---

## Licence
Licence tiks noteikta projekta vēlākā izstrādes posmā.

---

## Kontakti
Jautājumu vai sadarbības gadījumā sazināties ar projekta izstrādātājiem.
