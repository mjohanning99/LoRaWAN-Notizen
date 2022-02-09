# Einrichten eines LoRaWAN-Servers
In diesem Dokument wird kurz die Einrichtung und Installation eines LoRaWAN-Servers erläutert. Es werden beide Bestandteile des Servers angesprochen, der Netzwerk- sowie auch der Anwendungsserver.

## Vorbedingungen
- Server mit Ubuntu 20.04 LTS (andere Versionen sind vermutlich auch verwendbar)
- Erstellen eines eigenen Benutzers für LoRaWAN
	- `sudo user lorawan -m -G sudo`

	- `sudo passwd lorawan`
		- Eingeben des neuen Passwortes für den Benutzer

## Netzwerkserver
Zuallererst wird der Netzwerkserver installiert und eingerichtet. 