# Dispositif portable interactif inspiré de Totally Spies

| | |
|-|-|
|`Author` | Burlacu Ivona-Elena

## Description
Ce projet consiste en la réalisation d’un dispositif portable interactif basé sur Arduino Nano, inspiré du miroir compact utilisé dans la série Totally Spies. L’appareil aura la forme d’un petit miroir rond qui s’ouvre, avec une partie supérieure réfléchissante et une partie inférieure contenant un écran circulaire et plusieurs composants électroniques. Lors de l’ouverture, le système affichera un écran de démarrage, puis un menu principal permettant d’accéder à différentes fonctions, comme l’affichage de messages prédéfinis, la consultation de journaux enregistrés sur une carte microSD, le déclenchement d’alertes lumineuses, sonores et vibratoires, ainsi qu’un mini-jeu de type Snake contrôlé par l’inclinaison du dispositif.

## Motivation
Depuis mon enfance, la série Totally Spies m’a beaucoup plu et j’ai toujours voulu avoir un gadget semblable à celui utilisé par les personnages. Grâce à ce projet, j’ai enfin eu l’occasion d’en concevoir une version inspirée, en utilisant les notions techniques étudiées en laboratoire.

## Architecture
Le système est structuré en cinq sous-systèmes principaux : l'unité centrale de contrôle, le sous-système de détection, le sous-système d'affichage, le sous-système d'alertes et le sous-système de stockage.
L'unité centrale, basée sur l'Arduino Nano, coordonne l'ensemble des opérations et gère la communication entre les différents modules.
Le sous-système de détection comprend le capteur MPU-6050, qui fournit les données d'accélération et d'orientation via I2C — utilisées à la fois pour contrôler le jeu Snake par inclinaison et pour détecter l'ouverture du dispositif. Un reed switch couplé à un aimant détecte mécaniquement l'état ouvert ou fermé du couvercle via GPIO. Un potentiomètre permet une entrée analogique pour la navigation dans les menus.
Le sous-système d'affichage repose sur un écran circulaire GC9A01 de 1.28 pouces (240×240 pixels), communiquant avec l'Arduino Nano via le bus SPI. Il affiche le bootscreen, le menu principal, les mission logs et le jeu Snake.
Le sous-système de stockage utilise une carte microSD connectée via SPI, partageant le même bus que l'écran. Elle permet la sauvegarde et la lecture des mission logs (messages et notes de l'utilisateur).
Le sous-système d'alertes comprend un buzzer passif contrôlé par PWM pour les alertes sonores, une LED RGB et un moteur vibrant contrôlés via GPIO/PWM pour les retours visuels et haptiques.
L'ensemble du système est alimenté par une batterie Li-Po 3.7V, chargée via un module TP4056, avec un convertisseur step-up assurant une tension stable de 5V pour l'Arduino Nano et les périphériques.

### Block diagram

<!-- Make sure the path to the picture is correct -->
![Block Diagram](schematics<img width="773" height="554" alt="block_diagram png" src="https://github.com/user-attachments/assets/8c0b3560-3fc4-46a0-af07-fe20d5c8a713" />
/block_diagram.png)

### Schematic

![Schematic](schematics/kicad_schematic.png)

### Components


<!-- This is just an example, fill in with your actual components -->

| Device | Usage | Price |
|--------|--------|-------|
| Arduino Nano | Microcontrôleur principal | [34.84 RON](https://sigmanortec.ro/placa-dezvoltare-compatibila-arduino-nano-v30-atmega328p-au-ft232) |
| Écran LCD rond  | Écran avec slot SD | [31.48 RON](https://www.emag.ro/ecran-lcd-rotund-de-1-28-240x240-tft-slot-sd-controler-gc9a01-spi-3-3v-s-254/pd/DG8PHR3BM/?ref=fav_pd-title) |
| Kit Plusivo Pi 4 Super Starter| Kit comprenent: Capteur MPU6050, leds, led RGB, photorésistance, buzzer passif, résistance, fils | [54 RON](https://www.optimusdigital.ro/ro/kituri/9698-kit-plusivo-pi-4-fara-placa-i-fara-card.html?search_query=kituri&results=60) |
| Module de charge pour batterie au lithium, TP4056 | Module pour batterie | [4.72 RON](https://sigmanortec.ro/modul-incarcare-baterie-litiu-tp4056-typec-5v-1a-cu-protectie) |
| Batterie Li-Po Akyga AKY0571 | Batterie | [44.28 RON](https://www.emag.ro/acumulator-li-po-akyga-3-7v-1000mah-cu-conector-jst-2-pini-150mm-aky0571/pd/DGG2H23BM/) |
| Moteur vibrant plat, bouton | Moteur vibrante Arduino | [9.12 RON](https://sigmanortec.ro/motor-vibratii-plat-buton-1034-3v) |
| Reed switch | Détecter l’ouverture et la fermeture | [1.86 RON](https://sigmanortec.ro/Comutator-magnetic-Reed-N-O-p161249015) |
| Breadboard | Board pour le projet | [10 RON](https://www.emag.ro/breadboard-h-hct-tronic-830-puncte-de-conectare-abs-200x630-puncte-034-066/pd/DBNQ7R3BM/) |
| Potentiomètre | Réglage manuel d’un paramètre du système | [3.03 RON](https://sigmanortec.ro/Potentiometru-10K-ohm-6mm-p126029278) |
| Capuchon pour potentiomètre | Commande mécanique du potentiomètre | [1.94 RON](https://sigmanortec.ro/capac-knob-potentiometru-6mm-15x17-albastru) |
| Goldpin header | Souder et connecter les modules | [10.95 RON](https://www.emag.ro/goldpin-header-40-pini-tht-2-54-mm-tata-negru-5904162801701/pd/DQZ8KLMBM/) |
| Card SD | Stocker la mémoire | [21.99 RON](https://www.emag.ro/card-de-memorie-mediarange-micro-sdhc-8gb-clasa-10-cu-adaptor-sd-mr957/pd/DXJWRLMBM/) |
| Magnet | Fermez l'appareil | [9.79 RON](https://www.emag.ro/magneti-neodim-rotunzi-set-10-bucati-foarte-puternici-pentru-diferite-aplicatii-si-activitati-10x2-mm-01961/pd/D4BB3DYBM/) |
| Convertisseur de niveau logique | Adaptation des niveaux logiques entre les modules 5V et 3.3V | [11.3 RON](https://www.emag.ro/convertor-de-nivel-logic-cu-4-canale-elektroweb-5-v-3-3-v-2-8-v-1-8-v-2-a-018/pd/D7YW35MBM/) |
| Carte de prototypage | Assemblage de composants par soudure | [5.76 RON](https://sigmanortec.ro/Placa-PCB-prototipare-fata-dubla-7x9cm-p125747328) |
| Step-up | Transformez rapidement une batterie Li-ion 3,7 V en batterie externe. | [3.81 RON](https://sigmanortec.ro/Modul-incarcare-baterie-3-7V-cu-ridicator-la-5V-p160514049) |

### Libraries

<!-- This is just an example, fill in the table with your actual components -->

| Library | Description | Usage |
|---------|-------------|-------|
| [lib-name1](link-to-lib) | official description of the lib | Used for accesing the peripherals of the microcontroller  |
| [lib-name2](link-to-lib) | official description of the lib | Used for accesing the peripherals of the microcontroller  |

## Log

<!-- write every week your progress here -->

### Week 6 - 12 May

### Week 7 - 19 May

### Week 20 - 26 May


## Reference links

<!-- Fill in with appropriate links and link titles -->

[Tutorial 1](https://www.youtube.com/watch?v=wdgULBpRoXk&t=1s&ab_channel=BenEater)

[Article 1](https://www.explainthatstuff.com/induction-motors.html)

[Link title](https://projecthub.arduino.cc/)
