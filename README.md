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


Instalace OS:

V tomto tutoriálu se instalací samotného operačního systému na Raspberry Pi nebudeme zaobývat. K instalaci OS je zaměřen následující tutoriál (připravuje se)

Konfigurace:

1. Zjistěte IP adresu vašeho zařízení Raspberry Pi a pomocí SSH se k němu připojte (Použíjte např. PuTTY) Login: osmc Password: osmc. 
2. Přihlaste se jako root, vytvořte nový adresář Hyperion ve vašém domovském adresáři a přepněte se do něj
```
sudo -i
mkdir /home/osmc/Hyperion
cd /home/osmc/Hyperion
```
3. Stáhněte instalační skript hyperion a nastavte práva pro spouštění
```
wget -N https://raw.githubusercontent.com/tvdzwan/hyperion/master/bin/install_hyperion.sh
sudo chmod +x install_hyperion.sh
```
4. Nainstalujte potřebné repozitaře
```
sudo apt-get update && sudo apt-get -y install libqtcore4 libqtgui4 libqt4-network libusb-1.0-0
sudo apt-get -y install libprotobuf9 ca-certificates
```
5. Spusťte instalační skript stažený v bodě 3)
```
sudo sh ./install_hyperion.sh
```
6. Stáhněte .ZIP doplněk pro OSMC systém
```
wget -N https://github.com/LightberryEu/plugin.program.hyperion.configurator/archive/master.zip
```
7. Přejděte do prostředí OSMC a postupujte následujícími úkony:

1. Povolení SPI: My OSMC -> Pi Config -> Hardware Support -> Enable SPI support -> zapnout

2. Instalce doplňku hyperion: Doplňky -> Prohlížeč doplňků (ikona otevřené krabice) -> Instalovat ze zip souboru -> Domovská složka -> Hyperion -> master.zip

3. Konfigurace hyperion: Doplňky -> Doplňky programů -> Hyperion Config Creator -> Lightberry HD for Raspberry Pi (ws28010) -> vložte počet LED diod horizontálně -> vložte počet LED diod vertikálně -> zadejte, kde LED pásek začíná -> zadejte počet LED diod

8. Přistupte k příkazovému řádku a nastartujte službu hyperion

  sudo service hyperion start

9. Otestujte zadáním příkazů

  hyperion-remote --priority 50 --color red --duration 5000

  hyperion-remote --priority 50 --color green --duration 5000

  hyperion-remote --priority 50 --color blue --duration 5000

  hyperion-remote --priority 50 --color white --duration 5000

Užití dalších parametrů můžete nalézt zde ( odkaz )

10. Pokud je vše v pořádku, máte hotovo. Pokud ne, pokračujte následujícími body

11. V případě, že se vám zaměňují modrá a zelená barva, je potřeba upravit konfigurační soubor hyperion.config.json. V tomto souboru je potřeba vyhledat "colorOrder": "rgb" a samotné rgb nahradit na rbg. "colorOrder": "rbg". Službu je potřeba restartartovat.

  nano /etc/hyperion/hyperion.config.json

  sudo service hyperion restart

12. V případě, že se vám místo barvy bílé zobrazuje barva narůžovělá, je potřeba upravit konfigurační soubor hyperion.config.json, obdobně jako v bodě 12). V tomto konfigurační souboru je potřeba vyhledat sekci color a barvu red, ve které budeme snižovat hodnotu whitecolor (nastavte hodnotu whitecolor červené barvy napři na 0.5). Službu je potřeba restartovat.

  nano /etc/hyperion/hyperion.config.json

  sudo service hyperion restart

Vzádelé ovládání:

Následující aplikace dokáže nastavit statickou barvu hyperionu nebo spuštění světelného efektu a je možné ji stáhnout z obchodu Play ve free a placené verzi (více informací o vzdáleném ovládání hyperionu naleznete zde)
![alt text](https://github.com/davidvasicek/Hyperion-Ambilight-/blob/master/sch%C3%A9ma%20zapojen%C3%AD.png)
