---
title: "Webhosting einer Anwendung mit Queuing | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c7a539fa-e442-4c08-a7f1-17b7f5a03e88
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# Webhosting einer Anwendung mit Queuing
Der Windows Process Activation Service \(WAS\) verwaltet die Aktivierung und Lebensdauer der Arbeitsprozesse, die [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]\-Dienste hostende Anwendungen enthalten.  Das WAS\-Prozessmodell verallgemeinert das [!INCLUDE[iis601](../../../../includes/iis601-md.md)]\-Prozessmodell für den HTTP\-Server durch das Entfernen der Abhängigkeit von HTTP.  Dies ermöglicht [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Diensten die Verwendung von HTTP\- und andere Protokollen wie net.msmq und msmq.formatname in einer Hostumgebung, die nachrichtenbasierte Aktivierung unterstützt und die Möglichkeit zum Hosten vieler Anwendungen auf einem bestimmten Computer bietet.  
  
 WAS enthält einen Message Queuing \(MSMQ\)\-Aktivierungsdienst, der eine Anwendung mit Queuing aktiviert, wenn mindestens eine Nachricht in einer der von der Anwendung verwendeten Warteschlangen platziert wird.  Der MSMQ\-Aktivierungsdienst ist ein NT\-Dienst, der standardmäßig automatisch gestartet wird.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] zu WAS und seinen Vorteilen finden Sie unter [Hosten in WAS \(Windows Process Activation Service\)](../../../../docs/framework/wcf/feature-details/hosting-in-windows-process-activation-service.md).  [!INCLUDE[crabout](../../../../includes/crabout-md.md)] zu MSMQ finden Sie unter [Warteschlangenübersicht](../../../../docs/framework/wcf/feature-details/queues-overview.md)  
  
## Adressieren von Warteschlangen in WAS  
 WAS\-Anwendungen weisen Uniform Resource Identifier \(URI\)\-Adressen auf.  Anwendungsadressen haben zwei Teile: einen Basis\-URI\-Präfix und eine anwendungsspezifische, relative Adresse \(Pfad\).  Diese beiden Teile stellen beim Zusammenfügen die externe Adresse für eine Anwendung bereit.  Der Basis\-URI\-Präfix wird aus der Sitebindung erstellt und für alle Anwendungen unter der Site verwendet, beispielsweise "net.msmq:\/\/localhost", "msmq.formatname:\/\/localhost" oder "net.tcp:\/\/localhost".  Anwendungsadressen werden anschließend durch Anfügen anwendungsspezifischer Pfadfragmente \(wie "\/applicationOne"\) an den Basis\-URI\-Präfix erstellt, um den vollständigen Anwendungs\-URI zu bilden, z. B. "net.msmq:\/\/localhost\/applicationOne".  
  
 Der MSMQ\-Aktivierungsdienst verwendet den Anwendungs\-URI zum Abgleichen der Warteschlange, die der MSMQ\-Aktivierungsdienst auf Nachrichten überwachen muss.  Wenn der MSMQ\-Aktivierungsdienst startet, listet er alle öffentlichen und privaten Warteschlangen auf dem Computer auf, für deren Empfang er konfiguriert ist, und überwacht ihn auf Nachrichten.  Alle 10 Minuten aktualisiert der MSMQ\-Aktivierungsdienst die Liste der zu überwachenden Warteschlangen.  Wenn in einer Warteschlange eine Nachricht gefunden wird, gleicht der Aktivierungsdienst den Warteschlangennamen entsprechend dem längsten übereinstimmenden Anwendungs\-URI für die Bindung net.msmq ab, und aktiviert die Anwendung.  
  
> [!NOTE]
>  Die aktivierte Anwendung muss mit dem Präfix des Warteschlangennamens übereinstimmen \(längstmögliche Übereinstimmung\).  
  
 Ein Warteschlangenname lautet beispielsweise msmqWebHost\/orderProcessing\/service.svc.  Wenn Anwendung 1 über ein virtuelles Verzeichnis \/msmqWebHost\/orderProcessing mit service.svc darunter verfügt und Anwendung 2 über ein virtuelles Verzeichnis \/msmqWebHost mit orderProcessing.svc darunter verfügt, wird Anwendung 1 aktiviert.  Wenn Anwendung 1 gelöscht wird, wird Anwendung 2 aktiviert.  
  
> [!NOTE]
>  Beim Erstellen einer Warteschlange aktivieren gesendete Nachrichten eine Anwendung erst dann, wenn der MSMQ\-Aktivierungsdienst die Warteschlangenliste aktiviert; dies geschieht maximal 10 Minuten nach dem Erstellen der Warteschlange.  Beim Neustart des Aktivierungsdienstes wird auch die Warteschlangenliste aktualisiert.  
  
### Die Auswirkung privater und öffentlicher Warteschlangen auf die Adressierung  
 Der MSMQ\-Aktivierungsdienst unterscheidet nicht zwischen privater und öffentlicher Warteschlangenüberwachung.  Öffentliche und private Warteschlangen sollten nicht den gleichen Namen haben.  Anderenfalls wird eine im Internet gehostete Anwendung möglicherweise beim Lesen aus einer der beiden Warteschlangen aktiviert.  
  
### Warteschlangenkonfiguration zur Aktivierung  
 Der MSMQ\-Aktivierungsdienst wird als NETZWERKDIENST ausgeführt.  Dieser Dienst überwacht Warteschlangen zum Aktivieren von Anwendungen.  Zum Aktivieren von Anwendungen aus der Warteschlange muss die Warteschlange NETZWERKDIENST\-Zugriff bieten, um Nachrichten in der Zugriffssteuerungsliste einzusehen.  
  
### Nicht verarbeitbare Nachrichten  
 Die Handhabung nicht verarbeitbarer Nachrichten in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] erfolgt durch den Kanal, der nicht nur feststellt, dass eine Nachricht nicht verarbeitbar ist, sondern basierend auf der Benutzerkonfiguration auch ein Disposition auswählt.  Als Ergebnis gibt es eine einzelne Nachricht in der Warteschlange.  Die im Internet gehostete Anwendung bricht mehrmals hintereinander ab, und die Nachricht wird in eine Wiederholungswarteschlange verschoben.  Zu einem von der Zeitverzögerung zwischen den Wiederholungszyklen festgelegten Zeitpunkt wird die Nachricht aus der Wiederholungswarteschlange für einen erneuten Versuch in die Hauptwarteschlange verschoben.  Dazu muss jedoch der in der Warteschlange stehende Kanal aktiv sein.  Wenn die Anwendung vom WAS wiederverwendet wird, verbleibt die Nachricht in der Wiederholungswarteschlange, bis eine weitere Nachricht zum Aktivieren der Anwendung mit Queuing in der Hauptwarteschlange eingeht.  In diesem Fall kann das Problem behoben werden, indem die Nachricht manuell aus der Wiederholungswarteschlange zurück in die Hauptwarteschlange verschoben wird, um die Anwendung erneut zu aktivieren.  
  
### Einschränkung für Unterwarteschlangen und Systemwarteschlangen  
 Eine in WAS gehostete Anwendungen kann in einer Systemwarteschlange wie der systemweiten Warteschlange für unzustellbare Nachrichten oder in Unterwarteschlangen wie der Unterwarteschlange für potenziell schädliche Nachrichten nicht basierend auf Nachrichten aktiviert werden.  Dies ist eine Einschränkung für diese Produktversion.  
  
## Siehe auch  
 [Behandlung nicht verarbeitbarer Nachrichten](../../../../docs/framework/wcf/feature-details/poison-message-handling.md)   
 [Dienstendpunkte und Adressieren von Warteschlangen](../../../../docs/framework/wcf/feature-details/service-endpoints-and-queue-addressing.md)