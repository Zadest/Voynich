# Voynich Botanik Browser

Der Voynich Botanik Browser ist als Prototyp zur Darstellung der verschiedenen Klassifikationen der Illustrationen im botanischen Bereich des Voynich Manuskripts entstanden. Im Rahmen der Übung Verarbeitung enigmatischer Schriftstücke im Wintersemester 2020/21 entstand eine erste Ausarbeitung des Prototypen. Die Grundidee des Prototyps war die Darstellung der Pflanzenillustrationen als SVG in einer zufälligen Anordnung. Dabei sollten die SVG-Dateien die Illustrationen von ihrem Folio-Kontext trennen und nur die Illustration beinhalten.

Der Prototyp wurde mit dem Python Framework Django umgesetzt, das zur Zeit vielseitig eingesetzt wird und die Entwicklung komplexer, ebenso wie einfacher Webanwendungen angenehm gestaltet. Darüber hinaus bietet Django eine vorinstallierte Nutzerverwaltung, eine flexible Anbindung an die gängigsten Datenbanksysteme und ein mächtiges Modellierungssystem, das Objektorientierte Programmierung und Relationale Datenbanksysteme miteinander verbindet.

## Von Django-Webapp zum Fullstack
Der ursprüngliche Prototyp hatte eine experimentelle Weboberfläche, die aus einer Übersicht über alle Illustrationen und einer Detailansicht für jeweils eine Illustration bestand.
Für die Modulprüfung wurde der Prototyp um ein React Frontend erweitert. Die Kommunikation zwischen den beiden Bestandteilen React und Django findet über das Django Rest Framework auf der Backend-Seite und Axios im Frontend statt. 
React, ähnlich wie Angular oder Vue, eignet sich für das Frontend besonders durch die Modularität. Bestandteile einer Website werden in Komponenten ausgelagert und erlauben so eine strukturierte Entwicklungsarbeit. Zur Gestaltung wurde Tailwind CSS verwendet, um eine möglichst gut dokumentierte und einheitliche Darstellung der Komponenten zu erzeugen.

Dem Frontend wurden Filteroptionen hinzugefügt die auf der Übersichtsseite angezeigten Illustrationen eingrenzen können. So ist es neben der vollständigen Anzeige auch möglich sich lediglich Illustrationen anzeigen zu lassen, die in einer bestimmten Publikation klassifiziert wurden.

## REST-Endpoints
Zur Kommunikation zwischen Backend wurden die folgenden Endpoints angelegt:
- rest/plants
- rest/persons
- rest/publications 
- rest/classifications
- rest/plant/<int:pk>/
- rest/publication/<int:pubID>/

Diese Endpoints sollten primär alle Daten in den verschiedenen Modellen offenlegen. Im Verlauf der Entwicklung wurden die Serializer für Pflanzen und Zuordnungen sowie Publikationen soweit ausgebaut und verknüpft, dass lediglich ein Request pro View nötig ist.

## Datenanreicherung
Zur Bereitstellung eines möglichst ausgiebigen Datensatzes wurden alle Folios des Voynich Manuskriptes als JPG-Dateien hinzugefügt und mit Klassifikationen versehen.
Über ein Python-Skript wurden die Pflanzenbezeichnungen mit WikiData abgeglichen und mit Bildern der Public Domain versehen. So können auf der Detailseite zu jeder Illustration auch Fotos der klassifizierten Pflanze gegenübergestellt werden. Durch diese Visualisierung soll den NutzerInnen die Möglichkeit zur persönlichen Bewertung der Klassifikation gegeben werden. Da dieser Prozess automatisiert abgelaufen ist, besteht keine Garantie, dass die hinzugefügten Bilder, die in Wikidata gesuchten Begriffe abbilden.

## Dockerization
Abschließend wurden die Bestandteile des Prototypen dockerisiert, um eine reibungslose Entwicklung auf unterschiedlichen Systemen zu gewährleisten. Dadurch werden Systemeigenheiten und -probleme ausgeschlossen und die Lauffähigkeit der Anwendung verbessert.
Die angelegten Dockerfiles bieten einen geeigneten Startpunkt, um die Applikation vollständig auf ein Deployment vorzubereiten. Die nächsten Schritte sind das Hinzufügen eines Webservers, bspw. NGINX und einer SQL-Datenbank, etwa PostgreSQL als Services im Dockerstack.
Für die Demonstration der Anwendung und der Daten im Rahmen der Modulprüfung werden primär die Entwicklungs-Webserver verwendet. Im Backend werden die Daten zur Zeit in einer LiteSQL Datenbank gespeichert.

## Aussicht
Für die weitere Entwicklung bietet es sich an, das verwendete REST-Framework durch eine GraphQL Lösung zu ersetzen, da zur Zeit nur wenige Endpoints genutzt werden, dies aber zu unnötig angefragten Daten im Frontend führt. 
Außerdem könnte die Anwendung um eine Bewertungsfunktion erweitert werden, die es NutzerInnen erlaubt einzelne Klassifikationen zu bewerten.
Eine Oberfläche zur nutzergesteuerten Klassifikation von Illustrationen mit Anmerkungen wäre ebenfalls denkbar.
