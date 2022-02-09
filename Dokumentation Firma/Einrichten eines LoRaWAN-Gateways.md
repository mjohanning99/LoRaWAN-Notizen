```toc
```

# Einrichten eines LoRaWAN-Gateways
Der Gateway wird mithilfe des ChirpStack Gateway OS realisiert. 

## Vorbedingungen
- Herunterladen des GatewayOS-base-Images (https://www.chirpstack.io/gateway-os/install/raspberrypi/) für die jeweilige Version des Raspberry Pi
- Ein iC880A-SPI-Concentratorboard
- Eine Handvoll Kabel zum Verbinden des Concentratorboards mit dem Pi
- Ein Raspberry Pi 3 (oder Raspberry Pi 4 HW 1.3 — *HW 1.4 geht derzeit noch nicht*)
- Eine SD-Karte mit mindestens 8 GB an Speicher
- Ein Gerät mit welchem ein Image auf eine SD-Karte geflasht werden kann
	- Das vorher heruntergeladene Image muss nun auf die SD-Karte geflasht werden — vorzugsweise mit _Win 32 Disk Imager_ oder _Balena Etcher_
