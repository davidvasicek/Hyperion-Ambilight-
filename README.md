# Hyperion-Ambilight-

![alt text](https://github.com/davidvasicek/Hyperion-Ambilight-/blob/master/1416725488636120979.jpg)

Hyperion je opensource Ambilight implementace, která běží na mnoha platformách. 

### Ambilight

**Ambilight** , zkratka pro "okolní osvětlení", je osvětlovací systém pro televizory vyvinutý společností Philips . 

Ambilight vytváří světelné efekty kolem televizoru, které odpovídají videoobsahu. Společnost Philips tvrdí, že může dojít k "většímu zážitku ze sledování". Ambilight je osvětlovací systém, který aktivně upravuje jas i barvu podle obsahu obrazu. Integrovaný do televizní skříně je zaměřen na technologii Ambilight, která umožňuje divákovi zobrazit více detailů, kontrastu a barvy obrazu při odstraňování odrazů na obrazovce. [1]

### Tutorial

**Potřebný hardware:**

- Raspberry Pi (3 verze B)
- Zdroj pro napájení Rasberry Pi
- Paměťová karta micro SDHC (ideálně 16GB) + card reader
- LED pásek (WS2801) - délka dle velikosti TV
- Zdroj pro napájení LED pásku (5V alespoň 10A)

**Potřebný software:**

- OSMC ( download )
- Win32 Disk Imager ( download )
- SD Card Formatter ( download )
- PuTTy ( download )

Tipy:

Pozor v jakém směru LED pásek zapojujete. Dráty samotného LED pásku je nutné připájet na CK(in) a SI(in) - správný směr zapojení vyobrazuje šipka --> zakreslená na pásku LED

Nenapájejte samotné Raspberry Pi zdrojem určeným pro napájení LED (5V). Použíjte zdroj určený pro napájení Raspberry Pi (5,1V) - jinak bude zařízení padat

GND -> Pin 9, SI (také DI) -> Pin 19, CK (také CLK) -> Pin 23

