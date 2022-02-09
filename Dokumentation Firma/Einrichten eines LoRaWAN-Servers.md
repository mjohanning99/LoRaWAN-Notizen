# Einrichten eines LoRaWAN-Servers
In diesem Dokument wird kurz die Einrichtung und Installation eines LoRaWAN-Servers erläutert. Es werden beide Bestandteile des Servers angesprochen, der Netzwerk- sowie auch der Anwendungsserver.

## Vorbedingungen
- Server mit Ubuntu 20.04 LTS (andere Versionen sind vermutlich auch verwendbar)
- Erstellen eines eigenen Benutzers für LoRaWAN
	- `sudo user lorawan -m -G sudo`
	- `sudo passwd lorawan`
		- Eingeben des neuen Passwortes für den Benutzer
- Installation notwendiger Pakete
	- `sudo apt update`
	- ggf. `sudo apt upgrade`
	- `sudo apt install mosquitto postgresql redis-server nginx -y`

## Netzwerkserver
Zuallererst wird der Netzwerkserver installiert und eingerichtet. Das `.deb`-Paket für den Netzwerkserver lässt sich auf der Seite von ChirpStack unter *Debian / Ubuntu Package* (https://www.chirpstack.io/network-server/downloads/) finden. Andernfalls gibt es in dem Ordner `Dateien` auch eine Version, welche allerdings ggf. nicht die neueste ist. 

Das Paket lässt sich mithilfe des Befehls `sudo dpkg -i paket_name.deb` in der Kommandozeile installieren.