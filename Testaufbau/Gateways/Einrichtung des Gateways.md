# Einrichtung des Gateways
![[gateway_test_1.jpg]]
## Erster Testaufbau
- Herunterladen und Flashen des [[GatewayOS]] auf den Raspberry Pi
	- GatewayOS 3.5.1 funktioniert auf dem Pi 4 scheinbar nicht
	- [GatewayOS 3.4.0](https://artifacts.chirpstack.io/downloads/chirpstack-gateway-os/raspberrypi/raspberrypi4/3.4.0/) könnte ggf. noch funktionieren
	- [GitHub issue](https://github.com/brocaar/chirpstack-gateway-os/issues/81) wurde bereits erstellt
- Installation verlief ohne Probleme
- Nach Installation via SSH auf Pi zugegriffen
- Ausführen des `sudo gateway-config`-Kommandos
	- Gateway-Einrichtung ziemlich simpel
	- __Beachten__: Wenn der [[iC880A-SPI]] nach der in dieser Dokumentation vorhandenen Anleitung an den RPi angeschlossen wird, so muss in der `gateway-config` der `Reset Pin` des Concatenator-Boards als `25` angegeben werden (da physischer Pin `22` = GPIO-Pin `25`)
- Wird diejenige Version des GatewayOS verwendet, das sowohl Gateway- als auch Anwendungsserver- und Netzwerkserversoftware enthält, müssen keine weiteren Einstellungen bezüglich der Netzwerkadresse des zentralen Servers vorgenommen werden
	- In diese Falle wird allerdings ein externer Server benutzt
- [[Einrichtung des Servers|Server]] wurde auf einem Serverblade mit der IP `192.168.8.22` eingerichtet 

## Verbindung mit Server
![[gateway-config.png]]
- [[MQTT-Broker]] des Server muss angegeben werde
- Ausführen von `sudo gateway-config` 
- Auswählen des Menü-Punktes `Edit Chirpstack Gateway Bridge Config`
- Dann `Edit configuration file`
- Folgende MQTT-Konfiguration einfügen:
```
# Generic MQTT authentication.
[integration.mqtt.auth.generic]
# MQTT server (e.g. scheme://host:port where scheme is tcp, ssl or ws)
server="tcp://192.168.8.22:1883"
```
- Notieren der Gateway-ID (steht oben bei `gateway-config`)
- Dieser muss im Server später eingetragen werden
- Gateway-ID kann auch manuell umgeändert werden
	- Dazu `gateway-config` ausführen
	- `Edit ChirpStack Concentratord Config`
	- `General Configuration`
	- Folgende Zeile bearbeiten: `gateway_id="gateway_id_hier_eingeben"`