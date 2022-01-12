# Zentraler Server — Allgemein
- Der zentrale Server erhält die von den einzelnen Gateways empfangenen Daten
- Ggf. werden diese Daten dedupliziert (Duplikate werden verworfen)
- Zentraler Server besteht aus zwei Komponenten
	- [[Anwendungsserver]] (Verwaltet das Node-„Inventar“, Web-Interface zur Verwaltung)
	- [[Netzwerkserver]] (Depulizierung der Daten, Authentifikation, Kommunikation mit dem Anwendungsserver)
- Muss mit dem Internet verbunden sein