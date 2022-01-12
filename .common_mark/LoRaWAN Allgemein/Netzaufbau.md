# Aufbau eines LoRaWAN-Netzes

* Sterntopologie
* Mehrere [Gateways](Gateways/Gateways%20Allgemein.md) in verschiedenen Objekten
* [Gateways](Gateways/Gateways%20Allgemein.md) mit [zentralem Server](Zentraler%20Server/Zentraler%20Server.md) verbunden (via Internet)
* [Zentraler Server](Zentraler%20Server/Zentraler%20Server.md) besteht aus [Anwendungsserver](Zentraler%20Server/Anwendungsserver.md) (Application server) und [Netzwerkserver](Zentraler%20Server/Netzwerkserver.md) (Network server)
* Mehrere [Nodes](Nodes/Nodes.md) (Endgeräte, LoRaWAN-Geräte) die Daten an Gateways senden

## Grober Beispielaufbau

![Netzwerkplan_Grob.jpg](../Medien/Bilder/Netzwerkplan_Grob.jpg)
Es wäre im obigen Beispiel auch gut möglich, dass die beiden [Nodes](Nodes/Nodes.md) Daten an beide [Gateways](Gateways/Gateways%20Allgemein.md) gleichzeitig senden — der LoRaWAN-Netzwerkserver würde die Daten in diesem Falle „deduplizieren“, also die mehrfach auftretenden Datensätze löschen, 
