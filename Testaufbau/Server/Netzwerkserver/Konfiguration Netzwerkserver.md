# Konfiguration des Netzwerkservers
- Konfigurationsdatei muss mithilfe von `chirpstack-network-server configfile > chirpstack-network-server.toml` erstellt werden
- Datei muss bearbeitet werden
- Die Datenbank muss angegeben werden
```sql
# PostgreSQL settings.
[postgresql]
dsn="postgres://chirpstack_ns:datenbank_passwort_hier_eingeben@localhost/chirpstack_ns?sslmode=disable"
```