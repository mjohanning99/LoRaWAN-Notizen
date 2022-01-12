# Anwendungsserver

* Auf Englisch *application server*
* Sein Aufgabengebiet ist eng mit der Kommunikation mit den *Nodes* bzw. *Gateways* verknüpft:
  * Verwaltet das Node-„Inventar“ (welche Nodes senden Daten an die Gateways?)
  * Bietet eine Verwaltungsoberfläche als Webanwendung (Benutzer, Organisationen und Nodes können hierüber verwaltet werden)
  * Node-Daten können per HTTP oder MQTT empfangen *und* gesendet werden und in die InfluxDB geschrieben werden
  * gRPC und RESTful APIs zur Integration in externe Dienste vorhanden
  * Ver- und Entschlüsselung der Node-Daten
  * For networks containing multiple gateways, ChirpStack Application Server provides a feature to test the gateway network coverage. By sending out periodical "pings" through each gateway, ChirpStack Application Server is able to discover how well these are received by other gateways in the same network. The collected data is displayed as a map in the web-interface.
