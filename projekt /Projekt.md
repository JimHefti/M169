# Projekt Workspace auf Container

## Projekt Planung 

### Ziel der Projektarbeit 

### Komponenten 
Wir benutzen ein Nextcloud Image(https://hub.docker.com/_/nextcloud) in welchem wir einen reverse proxy, und ein Workspace aufsetzen.

Netzwerkplan 



-Workbook und Kalender - nextcloud 

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

## Nextcloud AIO 

### Domain auf Hostdatein hinzufügen

![hinzufügen](../Bilder/Host-datei_brearbeitung.PNG)

Ich habe hier die Domain die ich für nextcloud verwenden werde hinzugefügt.
Meine Domain(Nextcloud): www.jimheft.ch

### Submit Domain

![Submit](../bilder/Domain_Submit.PNG)

