TEAMAUFGABE: 2 SchülerInnen bilden EIN Team
Aufgabenstellung: Aufbau einer DNS-Filter- und Load-Balancing-Infrastruktur für eine Schule
Szenario: Du bist Auszubildender bei einem IT-Dienstleister, der Schulen bei der Einrichtung und Wartung ihrer IT-Infrastruktur unterstützt. Die Stadt hat deinen Arbeitgeber beauftragt, in einer lokalen Schule eine sichere und zuverlässige DNS-Infrastruktur zu implementieren, die zentral DNS-Anfragen filtert, schadhafte Inhalte blockiert und die Netzwerksicherheit erhöht. Deine Aufgabe ist es, eine solche Infrastruktur basierend auf Docker-Containern zu installieren und zu konfigurieren.

Hintergrund und Anforderungen
Die Schule möchte eine Filterung für Werbe- und Tracking-Inhalte im gesamten Netzwerk erreichen und gleichzeitig die Netzwerksicherheit durch Blockieren gefährlicher Websites erhöhen. Zusätzlich soll die Lösung in der Lage sein, größere Anfragenmengen zu bewältigen, ohne die Leistung des Netzwerks zu beeinträchtigen. Ein Lastverteilungssystem mit mindestens zwei DNS-Servern wird gewünscht, um die Ausfallsicherheit zu erhöhen.

Ziele
Zentralisierte DNS-Filterung: Implementiere eine DNS-Filterlösung, die Werbung und gefährliche Inhalte für alle Geräte im Netzwerk blockiert.
Lastverteilung und Ausfallsicherheit: Erstelle ein Setup mit mindestens zwei DNS-Servern, um die Last zu verteilen und eine hohe Verfügbarkeit sicherzustellen.
Skalierbare und Container-basierte Lösung: Die gesamte Lösung soll mit Docker Containern realisiert und leicht erweiterbar sein.
Transparente Überwachung: Die Schule möchte ein Webinterface zur Überwachung der DNS-Aktivitäten, um Statistiken und Blockierprotokolle einsehen zu können.
Einfache Konfiguration und Wartung: Die Lösung sollte einfach zu konfigurieren und zu warten sein, um auch später von IT-Mitarbeitern der Schule bedient werden zu können.
Aufgabenbeschreibung
Installation und Konfiguration der DNS-Filter-Container (Pi-hole):

Setze zwei Instanzen von Pi-hole auf, die als DNS-Filter agieren und Inhalte blockieren.
Konfiguriere Pi-hole, um eine zentrale Filterliste zu verwenden, die Werbung und schadhafte Inhalte blockiert. Nutze hierzu vordefinierte Blocklisten.
Achte darauf, dass die Pi-hole-Container über Port 53 erreichbar sind, da dies der Standard-DNS-Port ist.
Einrichtung des DNS-Load-Balancers (dnsdist):

Verwende dnsdist als Load Balancer, um die DNS-Anfragen der Schule gleichmäßig auf die beiden Pi-hole Instanzen zu verteilen.
Konfiguriere dnsdist so, dass bei Ausfall einer Pi-hole Instanz alle Anfragen automatisch zur verbleibenden Instanz weitergeleitet werden.
Implementiere die Load-Balancing-Strategie (z. B. Round-Robin), die für eine gleichmäßige Verteilung der Anfragen sorgt.
Reverse Proxy für das Webinterface:

Richte einen nginx Container als Reverse Proxy für die Pi-hole Webinterfaces ein, sodass die Admins der Schule die Blockier- und Statistikdaten über einen zentralen Zugang verwalten können.
Schütze den Zugang zum Webinterface mit einem Passwort, um unbefugte Zugriffe zu verhindern.
Docker Compose Datei:

Erstelle eine docker-compose.yml Datei, die alle benötigten Services (zwei Pi-hole Instanzen, dnsdist und nginx) in einem Netzwerk verbindet und konfiguriert.
Nutze Volumes, um die Konfiguration und Daten von Pi-hole persistent zu speichern, damit sie bei einem Neustart der Container erhalten bleiben.
Test und Dokumentation:

Teste die DNS-Infrastruktur im Schulnetzwerk und prüfe, ob Werbung und schadhafte Inhalte effektiv gefiltert werden.
Verfasse eine Kurzanleitung für die IT-Mitarbeiter der Schule, die die grundlegende Nutzung und Wartung der DNS-Infrastruktur beschreibt.
Erwartete Ergebnisse:
Funktionierender DNS-Filter: Werbung und Tracking-Domains werden in allen Geräten im Schulnetzwerk blockiert.
Stabile DNS-Lastverteilung: Die Anfragen im Netzwerk werden gleichmäßig auf die Pi-hole Instanzen verteilt, und die Ausfallsicherheit ist gewährleistet.
Zentralisierte Überwachung: Das Schul-IT-Team kann über einen gesicherten Zugang auf das Pi-hole Webinterface zugreifen und die DNS-Aktivitäten überwachen.
Dokumentierte Docker Compose Datei: Eine gut strukturierte und kommentierte docker-compose.yml Datei, die die gesamte Konfiguration abdeckt und bei Bedarf erweiterbar ist.
Verständliche Anleitung: Eine kurze Dokumentation, die die wesentlichen Aspekte der Nutzung und Wartung beschreibt.
Zusätzliche Hinweise
Stelle sicher, dass alle Container mit Netzwerkschnittstellen verbunden sind, die eine sichere und isolierte Kommunikation im Schulnetzwerk ermöglichen.
Überlege dir Erweiterungsmöglichkeiten, falls die Schule später eine größere Anzahl an DNS-Instanzen oder zusätzliche Sicherheitsmaßnahmen hinzufügen möchte.
