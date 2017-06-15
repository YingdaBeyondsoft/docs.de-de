---
title: "Beschr&#228;nken der Nachrichtenverteilung | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8b5ec4b8-1ce9-45ef-bb90-2c840456bcc1
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Beschr&#228;nken der Nachrichtenverteilung
Der Peerkanal ist als Übertragungsnetz konzipiert.Das grundlegende Weitergabemodell umfasst die Verteilung jeder Nachricht, die von einem Mitglied eines Netzes gesendet wird, an alle anderen Mitglieder dieses Netzes.Dies ist besonders in Situationen von Vorteil, in denen jede von einem Mitglied generierte Nachricht für alle anderen Mitglieder relevant und hilfreich ist – beispielsweise in einem Chatraum.Bei vielen Anwendungen muss die Nachrichtenverteilung jedoch gelegentlich eingeschränkt werden.Tritt beispielsweise ein neues Mitglied dem Netz bei und möchte die letzte durch das Netz gesendete Nachricht abrufen, muss diese Anforderung nicht an alle Mitglieder des Netzes weitergeleitet werden.Die Anforderung kann auf nahe gelegene Nachbarn beschränkt werden, oder es können lokal generierte Nachrichten herausgefiltert werden.Nachrichten können auch an einen einzelnen Knoten des Netzes gesendet werden.In diesem Thema wird erläutert, wie mithilfe der Hopanzahl, eines Nachrichtenweitergabefilters, eines lokalen Filters oder einer Direktverbindung gesteuert werden kann, auf welche Weise Nachrichten innerhalb des Netzes weitergeleitet werden. Darüber hinaus finden Sie hier allgemeine Richtlinien für die Auswahl eines geeigneten Ansatzes.  
  
## Hopanzahl  
 Das `PeerHopCount`\-Konzept ähnelt dem im IP verwendeten TTL \(Time\-To\-Live\)\-Konzept.Der `PeerHopCount`\-Wert ist mit einer Nachrichteninstanz verknüpft und gibt an, wie häufig eine Nachricht weitergeleitet werden soll, bis sie verworfen wird.Jedes Mal, wenn eine Nachricht von einem Peerkanalclient empfangen wird, wird vom Client geprüft, ob für die Nachricht ein `PeerHopCount` angegeben ist.Ist ein solcher Wert vorhanden, wird die Hopanzahl durch den Client um "1" verringert, bevor die Nachricht an benachbarte Knoten weitergeleitet wird.Erhält ein Client eine Nachricht mit der Hopanzahl "0", wird die Nachricht zwar verarbeitet, aber nicht mehr an Nachbarn weitergeleitet.  
  
 Sie können die Hopanzahl zu einer Nachricht hinzufügen, indem Sie `PeerHopCount` bei der Implementierung der Nachrichtenklasse als Attribut zu der anwendbaren Eigenschaft oder dem anwendbaren Feld hinzufügen.Sie können hierfür vor dem Senden der Nachricht an das Netz einen bestimmten Wert festlegen.Auf diese Weise kann die Verteilung von Nachrichten innerhalb des Netzes mithilfe der Hopanzahl gegebenenfalls eingeschränkt werden, was zu einer Verringerung unnötiger doppelter Nachrichten führen kann.Dies ist hilfreich, wenn das Netz eine große Menge redundanter Daten enthält oder wenn Nachrichten nur an direkte Nachbarn \(oder an Nachbarn, die nur wenige Hops entfernt sind\) gesendet werden sollen.  
  
-   Codeausschnitte und weitere Informationen finden Sie im [Peer Channel Team Blog](http://go.microsoft.com/fwlink/?LinkID=114531) \(http:\/\/go.microsoft.com\/fwlink\/?LinkID\=114531\).  
  
## Nachrichtenweitergabefilter  
 `MessagePropagationFilter` dient zum benutzerdefinierten Steuern der Nachrichtenweitergabe, besonders in Fällen, in denen die Weitergabe durch den Inhalt der Nachricht oder durch andere spezifische Szenarios bestimmt wird.Durch den Filter werden für jede Nachricht, die den Knoten passiert, Weitergabenentscheidungen getroffen.Dies gilt sowohl für Nachrichten, die von einem anderen Punkt innerhalb des Netzes stammen und von Ihrem Knoten empfangen werden, als auch für Nachrichten, die in Ihrer Anwendung erstellt wurden.Der Filter kann sowohl auf die Nachricht als auch auf deren Ursprung zugreifen, sodass Entscheidungen über die Weiterleitung oder das Verwerfen der Nachricht auf der Grundlage der vollständig verfügbaren Informationen getroffen werden können.  
  
 <xref:System.ServiceModel.PeerMessagePropagationFilter> ist eine abstrakte Basisklasse mit einer einzelnen Funktion: <xref:System.ServiceModel.PeerMessagePropagationFilter.ShouldMessagePropagate%2A>.Das erste Argument des Methodenaufrufs übergibt eine vollständige Kopie der Nachricht.Änderungen an der Nachricht wirken sich nicht auf die eigentliche Nachricht aus.Das letzte Argument des Methodenaufrufs identifiziert den Ursprung der Nachricht \(`PeerMessageOrigination.Local` oder `PeerMessageOrigination.Remote`\).Konkrete Implementierungen dieser Methode müssen eine Konstante aus der <xref:System.ServiceModel.PeerMessagePropagation>\-Enumeration zurückgeben, die angibt, dass die Nachricht an die lokale Anwendung \(`Local`\), an Remoteclients \(`Remote`\), an beide dieser Optionen \(`LocalAndRemote`\) oder an keine dieser Optionen \(`None`\) weitergeleitet werden soll.Sie können diesen Filter durch Zugreifen auf das entsprechende `PeerNode`\-Objekt und Angeben einer Instanz der abgeleiteten Weitergabefilterklasse in der `PeerNode.MessagePropagationFilter`\-Eigenschaft anwenden.Vergewissern Sie sich vor dem Öffnen des Peerkanals, dass der Weitergabefilter angefügt ist.  
  
-   Codeausschnitte und weitere Informationen finden Sie unter [Peer Channel Team Blog](http://go.microsoft.com/fwlink/?LinkID=114532) \(http:\/\/go.microsoft.com\/fwlink\/?LinkID\=114532\).  
  
## Kontaktieren eines einzelnen Netzknotens  
 Ein einzelner Netzknoten kann durch Einrichten eines lokalen Filters oder durch Einrichten einer Direktverbindung kontaktiert werden.  
  
 Besitzen die Knoten innerhalb eines Netzes individuelle IDs, können Sie in der Implementierung Ihrer Nachricht eine Ziel\-ID angeben.Ein lokaler Filter kann durch Schreiben einer Funktion in den Nachrichtenvertrag eingerichtet werden. Dadurch wird die Nachricht lediglich für den aktuellen Knoten angezeigt, wenn dessen ID mit der angegebenen Ziel\-ID übereinstimmt.Die Nachricht wird durch das Netz transportiert, weshalb kein Mehraufwand zum Einrichten einer neuen Verbindung entsteht.Es ergibt sich jedoch ein Verlust an Effizienz, da die Nachricht mehrmals durch das Netz gesendet wird.Dieses Verfahren eignet sich gut zum Senden von Nachrichten an einzelne Mitglieder eines Netzes, vorausgesetzt, die Nachrichten sind nicht zu umfangreich und werden nicht zu häufig gesendet.  
  
 Bei dauerhaften Verbindungen mit hoher Bandbreite empfiehlt sich die Verwendung einer Direktverbindung.Sie können Verbindungsinformationen über das Netz senden und anschließend eine Direktverbindung zum Senden\/Empfangen von Nachrichten einrichten.  
  
## Auswählen eines Ansatzes zum Beschränken der Nachrichtenverteilung  
 Ist eine Einschränkung der Nachrichtenverteilung erforderlich, sollten Sie sich die folgenden Fragen stellen:  
  
-   **Wer** muss die Nachricht empfangen?Lediglich ein Nachbarknoten?Ein Knoten an einem anderen Ort im Netz?Die Hälfte des Netzes?  
  
-   **Wie häufig** wird die Nachricht gesendet?  
  
-   Welche **Bandbreite** wird von der Nachricht verwendet?  
  
 Die Antworten auf die Fragen können Ihnen die Entscheidung für eine der Methoden – Hopanzahl, Nachrichtenweitergabefilter, lokaler Filter oder Direktverbindung – erleichtern.Berücksichtigen Sie die folgenden allgemeinen Richtlinien:  
  
-   **Wer**  
  
    -   *Einzelner Knoten*: lokaler Filter oder Direktverbindung.  
  
    -   *Nachbarn innerhalb einer bestimmten Umgebung*: PeerHopCount.  
  
    -   *Komplexe Teilmenge des Netzes*: MessagePropagationFilter.  
  
-   **Wie häufig**  
  
    -   *Sehr häufig*: Direktverbindung, PeerHopCount, MessagePropagationFilter.  
  
    -   *Gelegentlich*: lokaler Filter.  
  
-   **Bandbreitenauslastung**  
  
    -   *Hoch*: Direktverbindung; Verwendung von MessagePropagationFilter oder lokalem Filter nicht ratsam.  
  
    -   *Niedrig*: Beliebig; Direktverbindung wahrscheinlich nicht erforderlich.  
  
## Siehe auch  
 [Erstellen einer Peerkanalanwendung](../../../../docs/framework/wcf/feature-details/building-a-peer-channel-application.md)