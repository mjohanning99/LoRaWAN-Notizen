# Einrichtung des Servers
- Als Server wurde eine virtuelle Maschine auf einem Serverblade verwendet
- Auf den Server wurde Ubuntu Server 20.04 LTS installiert
- Durchlaufen der Betriebssysteminstallation (Standard)
- Nach Installation des Betriebssystems muss Chirpstack installiert und vorbereitet werden
- Erstellen eines neuen Ordners `~/chirpstack` in den alle Chirpstack-relevanten Dateien abelegt werden
- Anwendungsserversoftware muss heruntergeladen werden (https://www.chirpstack.io/application-server/downloads/)
- Netzwerkserversoftware muss heruntergeladen werden (https://www.chirpstack.io/network-server/install/debian/)
- Folgende Debian- bzw. Ubuntupakete müssen mithilfe von `sudo apt-get install paket_name` installiert werden, damit die obige Software laufen kann:
	- `mosquitto`, `postgresql`, `redis-server`
	- Die Einrichtung des Servers läuft nun wie folgt ab
		1. [[Einrichtung der PostgreSQL-Datenbank für den Netzwerkserver]]
		2. [[Einrichtung der PostgreSQL-Datenbank für den Anwendungsserver]]
		3. [[Konfiguration Netzwerkserver]]
		4. [[Konfiguration Anwendungsserver]]