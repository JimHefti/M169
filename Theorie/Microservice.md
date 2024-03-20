# Microservice-Architektur


## Definition Microservice
Ein Microservice ist ein Architekturtyp, der in einen Container gepackt wurde. Diese Dienste werden häufig verwendet, um eine Plattform für eine Anwendung bereitzustellen. Gute Beispiele für Microservices sind Monitoring-Software, DBMS-Software und Serving-Software wie Apache oder Unicorn.

Kurz gesagt handelt es sich bei Microservices um unabhängige, lose gekoppelte Services, die sich um ein Produkt oder eine Geschäftsfähigkeit drehen.

## Grundlagen der Microservice-Architektur
Die Microservice-Architektur ist ein Ansatz zur Entwicklung von Softwareanwendungen als Sammlung kleiner, unabhängiger Dienste, die jeweils einen spezifischen Geschäftsbereich oder eine Funktion abdecken. Jeder Microservice wird unabhängig von den anderen entwickelt, deployt und betrieben und kommuniziert über wohldefinierte APIs mit den anderen Services.

## Vorteile der Nutzung der Microservices-Architektur
Die Nutzung von Microservices bietet zahlreiche Vorteile und bietet ein erhebliches Maß an Flexibilität, Redundanz und Überwachungsmöglichkeiten, insbesondere bei der Nutzung von Orchestrierungstools wie Red Hat OpenShift oder Kubernetes. Lassen Sie mich dies anhand eines Beispiels veranschaulichen: Angenommen, Sie haben eine Webanwendung, die für die Bereitstellung von Daten aus einer Datenbank verantwortlich ist. Wenn Sie feststellen, dass die Anwendung nicht ordnungsgemäß funktioniert, können Sie dies mithilfe der Protokolle untersuchen. In diesem Szenario stellen Sie möglicherweise fest, dass die Datenbank nicht wie erwartet funktioniert. Mit der Microservices-Architektur können Sie das Problem lokalisieren, zum spezifischen Datenbankcontainer navigieren und einen Neustart einleiten. Nach dem Neustart nimmt die Datenbank den normalen Betrieb wieder auf. Dieser Prozess zeigt die Einfachheit und Effizienz, die Microservices in Verbindung mit Orchestrierungstools für die Systemwartung und Fehlerbehebung bieten.

## Nachteile der Verwendung der Microservices-Architektur
Die mit Microservices verbundenen Nachteile variieren je nach Umfang der Bereitstellung, Produkt oder Geschäftsfähigkeit. Bei der Verwaltung und Überwachung mehrerer Microservices besteht jedoch eine ständige Herausforderung in Form einer zunehmenden Komplexität und einer höheren Qualifikationsgrenze. Die Datenverwaltung wird mit zunehmender Bereitstellung komplexer und je umfangreicher die Tests werden. Darüber hinaus erhöhen sich die Sicherheitsrisiken, da viele Microservices Sicherheitslücken aufweisen. Die Kosten können auch aufgrund der Notwendigkeit zusätzlicher Software für eine effektive Überwachung, Verwaltung und den gesamten Lebenszyklusprozess von Microservices steigen, was von Natur aus teuer ist.


## Microservice-Paradigma und Systemarchitektur
Das Microservice-Paradigma beeinflusst die Systemarchitektur grundlegend durch die Förderung von Modularität, verteilten Systemen und unabhängigen Deployment-Zyklen. Es ermöglicht eine dezentralisierte Datenverwaltung, bei der jeder Service seine eigene Datenbank verwaltet, was die Kopplung zwischen Services reduziert und die unabhängige Evolution der Services unterstützt.

## Microservices und Container
Container-Technologien, wie Docker und Kubernetes, haben die Adoption und das Management von Microservices wesentlich erleichtert. Container bieten eine isolierte Umgebung für jeden Microservice, was die Konsistenz über Entwicklungs-, Test- und Produktionsumgebungen hinweg gewährleistet. Dies erleichtert das Deployment und die Skalierung von Microservices erheblich, da jeder Container als eine eigenständige Einheit betrachtet werden kann, die alles enthält, was ein Microservice zum Ausführen benötigt.

#### Schnelles Deployment und Continuous Integration/Continuous Deployment (CI/CD): 
Container unterstützen die Philosophie von Microservices, schnell und oft zu deployen, indem sie das Verpacken, Versenden und Ausführen von Anwendungen vereinfachen.
#### Unabhängigkeit:
Die Verwendung von Containern ermöglicht es, dass Microservices unabhängig voneinander entwickelt und skaliert werden können, ohne dass dies Auswirkungen auf andere Services hat.
#### Entwicklung und Testing: 
Container bieten eine konsistente Umgebung für die Entwicklung und das Testing von Microservices, was die "es funktioniert auf meinem Rechner" Problematik eliminiert.
