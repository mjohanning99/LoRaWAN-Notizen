# PostgreSQL Netzwerkserver
- Den PostgreSQL-Prompt mithilfe von `sudo -u postgres psql` aufrufen

```sql
-- chirpstack_ns-Benutzer mit einem beliebigen Passwort einrichten
create role chirpstack_ns with login password 'passwort_hier_eingeben'; 

-- chirpstack_ns-Datenbank mit dem chirpstack_ns-Benutzer als Owner einrichten;
create database chirpstack_ns with owner chirpstack_ns;

-- PostgreSQL-Prompt schließen 
\q
```

## Datenbank testen
- Datenbank mithilfe des folgenden Befehls testen: `psql -h localhost -U chirpstack_ns -W chirpstack_ns`