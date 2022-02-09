# Einrichten eines LoRaWAN-Servers
In diesem Dokument wird kurz die Einrichtung und Installation eines LoRaWAN-Servers erläutert. Es werden beide Bestandteile des Servers angesprochen, der Netzwerk- sowie auch der Anwendungsserver.

## Vorbedingungen
- Server mit Ubuntu 20.04 LTS (andere Versionen sind vermutlich auch verwendbar)
- Erstellen eines eigenen Benutzers für LoRaWAN
	- `sudo adduser lorawan -m -G sudo`
	- `sudo passwd lorawan`
		- Eingeben des neuen Passwortes für den Benutzer
- Installation notwendiger Pakete
	- `sudo apt update`
	- ggf. `sudo apt upgrade`
	- `sudo apt install mosquitto postgresql redis-server nginx -y`

## Netzwerkserver
Zuallererst wird der Netzwerkserver installiert und eingerichtet. Das `.deb`-Paket für den Netzwerkserver lässt sich auf der Seite von ChirpStack unter *Debian / Ubuntu Package* (https://www.chirpstack.io/network-server/downloads/) finden. Andernfalls gibt es in dem Ordner `Dateien` auch eine Version, welche allerdings ggf. nicht die neueste ist. 

Das Paket lässt sich mithilfe des Befehls `sudo dpkg -i paket_name.deb` in der Kommandozeile installieren.

### Einrichten der PostgreSQL-Datenbank
Der Netzwerkserver – wie auch später der Anwendungsserver – benötigt eine eigene Datenbank. Diese wird mithilfe von PostgreSQL bereitgestellt. Folgende Befehle müssen hierfür eingegeben werden.

- `sudo -u postgresql psql`
	- Hiermit gelangt man in die PostgreSQL-Eingabeaufforderung
- Sobald man in der Eingabeaufforderung angekommen ist müssen folgende Befehle eingegeben werden:

```sql
-- chirpstack_ns-Benutzer mit einem beliebigen Passwort einrichten
create role chirpstack_ns with login password 'passwort_hier_eingeben'; 

-- chirpstack_ns-Datenbank mit dem chirpstack_ns-Benutzer als Owner einrichten;
create database chirpstack_ns with owner chirpstack_ns;

-- PostgreSQL-Prompt schließen 
\q
```

Die Datenbank kann mithilfe des folgenden Befehls getestet werden: `psql -h localhost -U chirpstack_ns -W chirpstack_ns`

### Konfiguration des Netzwerkservers
Nachdem die Datenbank eingerichtet wurde kann der Netzwerkserver konfiguriert werden. Die Konfigurationsdatei befindet sich in `/etc/chirpstack-network-server/chirpstack-network-server.toml`. Diese kann mithilfe von `vim` oder `nano` als Superuser bearbeitet werden.

Der wichtigste Schritt ist hierbei die korrekte Angabe der Datenbank und ihres Passwortes. 

```sql
# PostgreSQL settings.
[postgresql]
dsn="postgres://chirpstack_ns:datenbank_passwort_hier_eingeben@localhost/chirpstack_ns?sslmode=disable"
```