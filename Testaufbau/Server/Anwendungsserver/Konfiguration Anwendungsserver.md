# Konfiguration des Anwendungsservers
- Konfigurationsdatei muss mithilfe von `chirpstack-application-server configfile > chirpstack-application-server.toml` erstellt werden
- Datei muss bearbeitet werden
- Die Datenbank muss angegeben werden
```sql
# PostgreSQL settings.
[postgresql]
dsn="postgres://chirpstack_as:datenbank_passwort_hier_eingeben@localhost/chirpstack_as?sslmode=disable"
```
- Ein JWT-Secret muss mithilfe von `openssl rand -base64 32` erstellt werden
- Secret muss in die Konfigurationsdatei eingefügt werden
```sql
# This is the API and web-interface exposed to the end-user.
[application_server.external_api]
jwt_secret="secret_hier_einfügen"
```