# PostgreSQL Anwendungsserver
- Den PostgreSQL-Prompt mithilfe von `sudo -u postgres psql` aufrufen
```sql
-- chirpstack_as-Benutzer mit einem beliebigen Passwort einrichten
create role chirpstack_as with login password 'passwort_hier_eingeben'; 

-- chirpstack_as-Datenbank mit dem chirpstack_as-Benutzer als Owner einrichten;
create database chirpstack_as with owner chirpstack_as;

-- In die chirpstack_as-Datenbank wechseln
\c chirpstack_as;

-- Zwei Extensions müssen nun mithilfe der folgenden Befehle aktiviert werden
create extension pg_trgm; 
create extension hstore;

-- PostgreSQL-Prompt schließen 
\q
```

## Testen der Datenbank
- Die Datenbank nun mithilfe von `psql -h localhost -U chirpstack_as -W chirpstack_as` testen