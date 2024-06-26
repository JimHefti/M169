# Projekt Workspace auf Container

## Projekt Planung 

### Ziel der Projektarbeit 
Das Ziel der Projektarbeit ist es ein Workspace zu erstellen mit Workbook und Kalender das auf Containers leuft.

### Komponenten 
Wir benutzen ein Nextcloud Image(https://hub.docker.com/_/nextcloud) in welchem wir einen reverse proxy, und ein Workspace aufsetzen.
Für jeden Service einen verschiedenen Container (Reverse Proxy nginx, Webserserver 1&2 httpd)
Nextcloud als zentrale lösung in welcher einzelne komponenten als container hinzugefügt werden können.

Netzwerkplan 
-Workbook und Kalender - nextcloud 

### Evaluation Nextcloud
| Aspekt            | Separate Container | Bewertung (Separate Container) | Nextcloud | Bewertung (Nextcloud) |
|-------------------|--------------------|-------------------------------|-----------|-----------------------|
| Einfachheit      | Das Einrichten und Verwalten mehrerer Container kann besonders für Anfänger komplex sein. Jeder Service erfordert seine eigene Konfiguration und Verwaltung. | 3 | Nextcloud bietet eine einzige Plattform zur Verwaltung mehrerer Komponenten. Das Hinzufügen neuer Komponenten kann relativ einfacher sein, da es in das Nextcloud-Ökosystem integriert ist. | 5 |
| Funktionen         | Jeder Service kann unabhängig angepasst werden, was eine größere Flexibilität bei der Auswahl spezifischer Konfigurationen und Versionen ermöglicht. | 4 | Die Integration mit Nextcloud kann die Anpassungsoptionen einschränken, da die Komponenten mit der Nextcloud-Umgebung kompatibel sein müssen. Es bietet jedoch eine nahtlose Integration mit den bestehenden Funktionen und Funktionalitäten von Nextcloud. | 3 |
| Sicherheit          | Jeder Container kann isoliert werden, was die Sicherheit erhöhen kann, indem die Angriffsfläche reduziert wird. Die ordnungsgemäße Konfiguration der Sicherheit für jeden Container ist jedoch unerlässlich. | 4 | Nextcloud bietet ein zentrales Sicherheitsmodell, das die Verwaltung und Überwachung vereinfachen kann. Schwachstellen in den hinzugefügten Komponenten könnten jedoch die gesamte Nextcloud-Instanz beeinträchtigen. Regelmäßige Updates und Sicherheitspatches sind dennoch erforderlich. | 3 |
| Skalierbarkeit       | Die Skalierung einzelner Dienste kann mehr Aufwand erfordern, da jeder Container separat verwaltet werden muss. Es bietet jedoch eine genauere Kontrolle über die Ressourcenzuweisung für jeden Dienst. | 3 | Der modulare Ansatz von Nextcloud ermöglicht eine einfachere Skalierbarkeit durch Hinzufügen oder Entfernen von Komponenten nach Bedarf. Bei der Skalierung müssen jedoch Kompatibilitäts- und Leistungsüberlegungen berücksichtigt werden. | 4 |
| Wartung       | Das Aktualisieren und Verwalten mehrerer Container kann zeitaufwändig sein, da jeder Dienst seinen eigenen Update-Zeitplan und seine eigenen Abhängigkeiten haben kann. | 3 | Nextcloud vereinfacht die Wartung durch Konsolidierung von Updates und Verwaltungsaufgaben innerhalb einer einzigen Plattform. Bei Updates können jedoch Kompatibilitätsprobleme zwischen Nextcloud und den hinzugefügten Komponenten auftreten. | 4 |
| Integration       | Erfordert manuelle Konfiguration und Integration jedes Dienstes mit externen Komponenten wie Datenbanken, Authentifizierungssystemen usw. | 3 | Nextcloud bietet eine integrierte Integration mit verschiedenen Diensten und Anwendungen durch ihr App-Ökosystem. Nicht alle Drittanbieterdienste sind jedoch mit Nextcloud kompatibel oder erfordern möglicherweise zusätzliche Konfiguration. | 4 |
| Community-Support | Jeder Dienst kann seine eigene Community und Supportkanäle haben, die in Verfügbarkeit und Qualität variieren können. | 3 | Nextcloud hat eine große und aktive Community, die Unterstützung und Ressourcen für sowohl Kernfunktionen als auch Drittanbieterintegrationen bietet. | 5 |
| Gesamt           | Geeignet für Projekte, die spezifische Konfigurationen oder eigenständige Dienste erfordern. Bietet mehr Kontrolle, erfordert jedoch mehr Aufwand bei Einrichtung und Verwaltung. | 3,29 | Ideal für Projekte, die eine zentrale Lösung mit integrierten Funktionen suchen. Bietet Einfachheit und Bequemlichkeit, kann jedoch Einschränkungen bei Anpassung und Skalierbarkeit haben. | 4,00 |
### Netzwerkplan

![Netzwerkplan](../Bilder/Netzwerkplan.PNG)


## Nextcloud Container

### Image Nextcloud
```
docker run ^
--init ^
--sig-proxy=false ^
--name nextcloud-aio-mastercontainer ^
--restart always ^
--publish 80:80 ^
--publish 8080:8080 ^
--publish 8443:8443 ^
--volume nextcloud_aio_mastercontainer:/mnt/docker-aio-config ^
--volume //var/run/docker.sock:/var/run/docker.sock:ro ^
--env SKIP_DOMAIN_VALIDATION=true ^
nextcloud/all-in-one:latest
```
Das ist das Nextcloud Image das ich verwende für meinne Workspace.

# Nextcloud AIO 

## Domain auf Hostdatein hinzufügen

![hinzufügen](../Bilder/Host-datei_brearbeitung.PNG)

Ich habe hier die Domain die ich für nextcloud verwenden werde hinzugefügt.
Meine Domain(Nextcloud): www.jimheft.ch

## Submit Domain

![Submit](../Bilder/Domain_Submit.PNG)
Ich habe meine Domain bei nextcloud erfolgreich Submitet.
Meine Domain die Submitet habe ist www.jimhefti.ch

## Download und Start Containers

### Ausgewählte container 
![Container](../Bilder/Ausgewählte_container.PNG)

#### Begründung Container auswahl
ClamAV: Dieser Container dient als Antiviren-Backend für Nextcloud. Er scannt Dateien auf Viren, wenn sie zu Nextcloud hochgeladen werden, um die Sicherheit zu erhöhen. 

Collabora (Nextcloud Office): Collabora ermöglicht das Bearbeiten und Teilen von Office-Dokumenten direkt in Nextcloud, vergleichbar mit anderen Online-Office-Lösungen. Es unterstützt gängige Dateiformate wie DOCX, XLSX und PPTX.

Imaginary: Dieser Container wird für die Vorschau von verschiedenen Bild- und Dokumentenformaten wie heic, heif, Illustrator-Dateien, PDFs, SVGs, TIFFs und webp genutzt. Er wandelt diese Dateiformate um, sodass sie als Vorschauen in Nextcloud angezeigt werden können. 

Nextcloud Talk: Dies ist die Chat- und Videokonferenz-Komponente von Nextcloud. Für den Betrieb benötigt Nextcloud Talk die Ports 3478/TCP und 3478/UDP, die in Ihrer Firewall oder Ihrem Router geöffnet bzw. weitergeleitet sein müssen.

Docker Socket Proxy: Dieser Container dient der Sicherheit, indem er den Docker Socket schützt. Er wird benötigt, um die Nextcloud App API zu benutzen, und stellt sicher, dass Anwendungen nur die benötigten Informationen und Steuerbefehle an den Docker Daemon senden können.

![Downloade](../Bilder/Downloade_Containers.PNG)

Ich habe auf meinem Localhost keine SSL certificate bekommen deswegen konnte ich nicht auf Nextcloud zugreifen.
Da dies ein Problem ist welches nicht einfach mal so behoben werden kann, habe ich mich nach Beratung mit Valentin Binotto dazu entschieden dieses Setup auf einem Ubuntu Server von Hetzner Cloud aufsetzen.
Beim erwerb des Servers habe ich meinen SSH hinzugefügt um später eine schnelle Verbindung zu ermöglichen.
Nachdem der Server gestartet ist, konnte ich mich mit ssh root@116.203.41.190 verbinden.

Dann musste ich nur noch Docker mit dem Skript installieren.
Dann musste Ich Valentin nur noch darum beten einen A record DNS eintrag von meiner IP auf seine Domaine(static.190.41.203.116.clients.your-server.d) zu erstellen.

# Neu mit Server 
Ich habe auf meinem Localhost keine SSL certificate bekommen deswegen konnte ich nicht auf Nextcloud zugreifen.
Da dies ein Problem ist welches nicht einfach mal so behoben werden kann, habe ich mich nach Beratung mit Valentin Binotto dazu entschieden dieses Setup auf einem Ubuntu Server von Hetzner Cloud aufsetzen.
Beim erwerb des Servers habe ich meinen SSH hinzugefügt um später eine schnelle Verbindung zu ermöglichen.
Nachdem der Server gestartet ist, konnte ich mich mit ssh root@116.203.41.190 verbinden.

Dann musste ich nur noch Docker mit dem Skript installieren.
Dann musste Ich Valentin nur noch darum beten einen A record DNS eintrag von meiner IP auf seine Domaine(static.190.41.203.116.clients.your-server.d) zu erstellen.
Anfang an habe ich hier ein Verzeichniss erstellt indem verschiedenste Files gespeichert werden namens: Projekt_169.
### Docker Composefile 
```
version: "3.3"
services:
  nginx:
    image: 'nginx'
    container_name: nginx
    restart: always
    volumes:
      - ./conf:/etc/nginx/conf.d
      - ./data:/data
      - ./letsencrypt:/etc/certs
    ports:
      - '443:443'
  nextcloud:
    image: nextcloud/all-in-one:latest
    restart: always
    container_name: nextcloud-aio-mastercontainer
    ports:
      - '8080:8080'
    environment:
      - APACHE_PORT=11001
      - APACHE_IP_BINDING=0.0.0.0
      - SKIP_DOMAIN_VALIDATION=true
    volumes:
      - nextcloud_aio_mastercontainer:/mnt/docker-aio-config
      - /var/run/docker.sock:/var/run/docker.sock:ro
    depends_on:
      - nginx
volumes:
  nextcloud_aio_mastercontainer:
    name: nextcloud_aio_mastercontainer
```

Mit Sudo docker compose up -d ladet es die installation und ich konnte mit der IP=https://116.203.41.190:8080 auf nextcloud gehen.
Ich habe dan das ganze eingerichtet mit neuen Domain, Zeitzone und mit verschiedenen Services, jetzt geht es weiter mit der konfiguraiton von Nextcloud.

![Nextcloud-Containers](../Bilder/Container_nextcloud.PNG)

Nächste Schritte:
Nginx-conf file erstellen.
Zertifikat für den Reverse proxy erstellen.
Endgültiger Test

### Nginx Config File 

Die Konfigurationsdatei von Nginx dient dazu, Anfragen an einen spezifischen Port weiterzuleiten und definiert die Speicherorte für den öffentlichen und privaten Schlüssel.

![Nextcloud-Containers](../Bilder/Nginx-Configfile.PNG)

### Zertifikat
```
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout ./apache-selfsigned.key -out ./apache-selfsigned.crt
```
Für diesen Zweck haben wir selbstsignierte Zertifikate verwendet, die mit dem folgenden Befehl erstellt wurden. Es ist wichtig sicherzustellen, dass wir uns im korrekten Verzeichnis befinden (in meinem Fall /Projekt_M169/letsencrypt), um die Konsistenz der Verzeichnispfade in der Docker-compose- und Nginx-Konfigurationsdatei zu gewährleisten.

### Schluss Test

Jetzt probieren wir auf unser Nextcloud Dashboard zu zugereifen.

![Dashboard](../Bilder/Dashborad-Nextcloud.png)

Erfolgreich Nextcloud Funktioniert und ist online ereichbar.

Lodindaten:

username: admin

password: 939e019cffe62e01ff235d36b4d4a8571f9d65f4963155cf

Zum Abschluss noch die Notizen und Kalender.

![Kalender](../Bilder/Kalender.png)
![Notizen](../Bilder/Notizen.png)


## Überwachung 

![überwachung](../Bilder/überwachung.PNG)


### Überwachung Server 

![image](https://github.com/JimHefti/M169/assets/160615771/6aecb0aa-3ea9-47cd-8446-bb6e5ee122ee)
![image](https://github.com/JimHefti/M169/assets/160615771/fb49de2c-1e5b-4642-90fb-91494819491e)
![image](https://github.com/JimHefti/M169/assets/160615771/2ae20fb9-330c-4c97-8362-6ac094cbda33)






