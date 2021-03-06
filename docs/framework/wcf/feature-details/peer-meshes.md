---
title: "Peer-Meshs | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d93e312e-ac04-40f8-baea-5da1cacb546e
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Peer-Meshs
Ein *Mesh* ist eine benannte Auflistung \(ein verbundenes Diagramm\) von Peerknoten, die untereinander kommunizieren können und durch eine eindeutige Mesh\-ID gekennzeichnet sind.  Jeder Knoten ist mit mehreren anderen Knoten verbunden.  In einer gut organisierten Netzstruktur besteht zwischen zwei Knoten immer eine Verbindung, und zwischen den am weitesten außen liegenden Knoten liegen immer nur wenige Hops. Darüber hinaus bleibt die Verbindung des Netzes auch dann bestehen, wenn einige Knoten oder Verbindungen ausfallen.  Aktive Knoten im Mesh veröffentlichen ihre Endpunktinformationen mit einer entsprechenden Mesh\-ID, sodass andere Peers sie finden können.  
  
## Eigenschaften eines Netzes, das mit Peerkanal erstellt wurde  
  
#### Eindeutige Identifizierung  
  
-   Jedes Netz ist durch eine eindeutige ID gekennzeichnet.  Der Name des Meshs \(die Mesh\-ID\) hat das gleiche Format wie der Domain Name System \(DNS\)\-Hostname.  Diese Mesh\-ID muss für den vorgesehenen Client der Anwendung im Bereich des verwendeten Resolvers eindeutig sein.  Allgemeine Namen wie "MyFamilysPeers" oder "KevinsPokerTable" können sich schnell mit anderen Benutzernamen überschneiden und unter Umständen unerwünschte Peerendpunktinformationen zurückgeben, was zu Datenschutzproblemen führen oder die Verbindungswartezeit erhöhen kann.  Sie können eine eindeutige ID als Postfix zum Spitznamen für das Netz hinzufügen \(beispielsweise "KevinsPokerTable90210"\).  
  
#### Nachrichtenweiterleitung  
  
-   Das Mesh ermöglicht die Weitergabe von Nachrichten von einem oder mehreren Absender an alle anderen Peerknoten im gleichen Mesh.  Durch Peerknoten weitergeleitete Nachrichten verwenden Header, die im Namespace unter `http://schemas.microsoft.com/net/2006/05/peer` angegeben sind.  
  
#### Optimierte Verbindungen  
  
-   Ein Peerkanalnetz wird beim Hinzufügen und Entfernen von Knoten automatisch angepasst. Damit wird sichergestellt, dass die Verbindung für alle Knoten gut und die Wahrscheinlichkeit für die Entstehung von Partitionen \(voneinander isolierte Knotengruppen\) gering ist.  Verbindungen im Mesh werden auch auf der Grundlage aktueller Muster im Datenverkehr dynamisch optimiert, sodass die Nachrichtenwartezeit vom Absender zum Empfänger so kurz wie möglich ist.  
  
#### Gebräuchliche Netzwerkfunktionen, die von Peerkanal nicht bereitgestellt werden  
 Einige gebräuchliche Netzwerkfunktionen werden von Peerkanal nicht bereitgestellt.  Zu diesen Funktionen, die alle auf Peerkanal aufbauen können, gehören:  
  
-   **Nachrichtensortierung:** Nachrichten einer einzelnen Quelle kommen eventuell nicht an allen anderen Seiten in der gleichen Reihenfolge oder in der von der Quelle gesendeten Reihenfolge an.  Anwendungen, die erfordern, dass Nachrichten in einer bestimmten Reihenfolge übermittelt werden, müssen dies integrieren \(z. B. durch Einschließen einer gleichmäßig zunehmenden ID in alle Nachrichten\).  
  
-   **Zuverlässiges Messaging:** Peerkanal enthält keinen Mechanismus, um den Nachrichtenempfang durch alle Peers sicherzustellen.  Um die Meldungsübermittlung zu garantieren, müssen Sie eine Zuverlässigkeitsebene schreiben, die Peerkanal übergeordnet ist.