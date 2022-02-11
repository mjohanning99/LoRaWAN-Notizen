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

## Anschluss des Concentrator-Boards
Es wird das Concentrator-Board iC880A verwendet.
### Anschluss an den Raspberry Pi
![[Screenshot 2022-01-12 at 18.02.00.png]]

### Raspberry Pi 3 Pinout
![[rp_pinout.png]]
## Konfiguration des Gateways
Zu allererst muss auf den Gateway per SSH zugegriffen werden. Die Standard-Logindaten sind `admin` als Benutzername sowie auch als Passwort. Danach wird `sudo gateway-config` ausgeführt und das folgende Menü sollte sichtbar werden:
![[gateway-config-allgemein.png]]
Es muss hier der Menüpunkt "1. Setup LoRa concentrator shield ausgewählt werden" und im darauffolgenden Schritt muss der iC880A-Concentrator ausgewählt werden:
![[gateway-config-concentrator.png]]
Als Channel-Plan wird EU868 genommen:
![[gateway-config-channel.png]]
Und anschließend muss der Reset-Pin angegeben werden; dieser ist GPIO-Pin 25, daher wird hier die "25" angegeben:
![[]]