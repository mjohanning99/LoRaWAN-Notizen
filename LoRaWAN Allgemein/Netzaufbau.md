# Aufbau eines LoRaWAN-Netzes
- Sterntopologie
- Mehrere [[Gateways Allgemein|Gateways]] in verschiedenen Objekten
- [[Gateways Allgemein|Gateways]] mit [[Zentraler Server|zentralem Server]] verbunden (via Internet)
- [[Zentraler Server]] besteht aus [[Anwendungsserver]] (Application server) und [[Netzwerkserver]] (Network server)
- Mehrere [[Nodes]] (Endgeräte, LoRaWAN-Geräte) die Daten an Gateways senden

## Grober Beispielaufbau
![[Netzwerkplan_Grob.jpg]]
Es wäre im obigen Beispiel auch gut möglich, dass die beiden [[Nodes]] Daten an beide [[Gateways]] gleichzeitig senden — der LoRaWAN-Netzwerkserver würde die Daten in diesem Falle „deduplizieren“, also die mehrfach auftretenden Datensätze löschen, 