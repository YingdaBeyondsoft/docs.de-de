---
title: "Aktivieren von Abfragebenachrichtigungen | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a5333e19-8e55-4aa9-82dc-ca8745e516ed
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# Aktivieren von Abfragebenachrichtigungen
Anwendungen, die Abfragebenachrichtigungen verwenden, haben einige Anforderungen gemeinsam.  Ihre Datenquelle muss richtig konfiguriert sein, um SQL\-Abfragebenachrichtigungen zu unterstützen, und die Benutzer müssen über die richtigen client\- und serverseitigen Berechtigungen verfügen.  
  
 Zum Verwenden von Abfragebenachrichtigungen muss Folgendes erfüllt sein:  
  
-   Aktivieren von Abfragebenachrichtigungen für Ihre Datenbank.  
  
-   Sicherstellen, dass die zum Verbinden mit der Datenbank verwendete Benutzer\-ID über die erforderlichen Berechtigungen verfügt.  
  
-   Verwenden eines <xref:System.Data.SqlClient.SqlCommand>\-Objekts zum Ausführen einer gültigen SELECT\-Anweisung mit einem zugehörigen Benachrichtigungsobjekt, entweder <xref:System.Data.SqlClient.SqlDependency> oder <xref:System.Data.Sql.SqlNotificationRequest>.  
  
-   Bereitstellen von Code, um die Benachrichtigung zu verarbeiten, falls sich die überwachten Daten ändern.  
  
## Anforderungen für Abfragebenachrichtigungen  
 Abfragebenachrichtigungen werden nur für SELECT\-Anweisungen unterstützt, die bestimmte Anforderungen erfüllen.  Die folgende Tabelle enthält Links zur SQL Server\-Onlinedokumentation zu Service Broker und Abfragebenachrichtigungen.  
  
 **SQL Server\-Onlinedokumentation**  
  
-   [Erstellen einer Abfrage für die Benachrichtigung](http://msdn.microsoft.com/library/ms181122.aspx)  
  
-   [Sicherheitsaspekte für Service Broker](http://msdn.microsoft.com/library/ms166059.aspx)  
  
-   [Sicherheit und Schutz \(Service Broker\)](http://msdn.microsoft.com/library/bb522911.aspx)  
  
-   [Sicherheitsaspekte für Notification Services](http://msdn.microsoft.com/library/ms172604.aspx)  
  
-   [Berechtigungen für Abfragebenachrichtigungen](http://msdn.microsoft.com/library/ms188311.aspx)  
  
-   [Internationale Gesichtspunkte bei Service Broker](http://msdn.microsoft.com/library/ms166028.aspx)  
  
-   [Überlegungen zu Lösungsentwürfen \(Service Broker\)](http://msdn.microsoft.com/library/bb522899.aspx)  
  
-   [Service Broker \(InfoCenter für Entwickler\)](http://msdn.microsoft.com/library/ms166100.aspx)  
  
-   [Entwicklerhandbuch \(Service Broker\)](http://msdn.microsoft.com/library/bb522908.aspx)  
  
## Aktivieren von Abfragebenachrichtigungen für das Ausführen von Beispielcode  
 Führen Sie zum Aktivieren von Service Broker in der **AdventureWorks**\-Datenbank mit SQL Server Management Studio die folgende Transact\-SQL\-Anweisung aus:  
  
 `ALTER DATABASE AdventureWorks SET ENABLE_BROKER;`  
  
 Damit die Abfragebenachrichtigungsbeispiele ordnungsgemäß ausgeführt werden, müssen auf dem Datenbankserver die folgenden Transact\-SQL\-Anweisungen ausgeführt werden:  
  
```  
CREATE QUEUE ContactChangeMessages;  
  
CREATE SERVICE ContactChangeNotifications  
  ON QUEUE ContactChangeMessages  
([http://schemas.microsoft.com/SQL/Notifications/PostQueryNotification]);  
```  
  
## Berechtigungen für Abfragebenachrichtigungen  
 Benutzer, die Befehle ausführen, mit denen Benachrichtigung angefordert werden, müssen über eine SUBSCRIBE QUERY NOTIFICATIONS\-Datenbankberechtigung auf dem Server verfügen.  
  
 Clientseitiger Code, der in einem teilweise vertrauenswürdigen Kontext ausgeführt wird, erfordert die <xref:System.Data.SqlClient.SqlClientPermission>.  
  
 Im folgenden Code wird ein <xref:System.Data.SqlClient.SqlClientPermission>\-Objekt erstellt, das den <xref:System.Security.Permissions.PermissionState> auf <xref:System.Security.Permissions.PermissionState> setzt.  Die <xref:System.Security.CodeAccessPermission.Demand%2A> erzwingt zur Laufzeit eine <xref:System.Security.SecurityException>, wenn nicht allen Aufrufern, die sich in der Aufrufliste darüber befinden, die Berechtigung gewährt wurde.  
  
 [!code-csharp[DataWorks SqlNotification.Perms#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlNotification.Perms/CS/source.cs#1)]
 [!code-vb[DataWorks SqlNotification.Perms#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlNotification.Perms/VB/source.vb#1)]  
  
## Auswählen eines Benachrichtigungsobjekts  
 Die Abfragebenachrichtigungs\-API stellt zwei Objekte zum Verarbeiten von Benachrichtigungen zur Verfügung: <xref:System.Data.SqlClient.SqlDependency> und <xref:System.Data.Sql.SqlNotificationRequest>.  Im Allgemeinen sollten die meisten Nicht\-ASP.NET\-Anwendungen das <xref:System.Data.SqlClient.SqlDependency>\-Objekt verwenden.  ASP.NET\-Anwendungen sollten die übergeordnete <xref:System.Web.Caching.SqlCacheDependency> verwenden, die die <xref:System.Data.SqlClient.SqlDependency> umschließt und einen Rahmen für die Verwaltung der Benachrichtigungs\- und Zwischenspeicherobjekte bietet.  
  
### Verwenden von "SqlDependency"  
 Zum Verwenden des <xref:System.Data.SqlClient.SqlDependency>\-Objekts muss Service Broker für die verwendete SQL Server\-Datenbank aktiviert werden, und Benutzer müssen über Berechtigungen zum Erhalt von Benachrichtigungen verfügen.  Service Broker\-Objekte, z. B. Benachrichtigungswarteschlangen, werden vordefiniert.  
  
 Außerdem wird vom <xref:System.Data.SqlClient.SqlDependency>\-Objekt automatisch ein Arbeitsthread gestartet, um Benachrichtigungen zu verarbeiten, wenn sie zur Warteschlange gesendet werden. Außerdem wird die Service Broker\-Meldung analysiert, und die Informationen werden als Ereignisargumentdaten verfügbar gemacht.  Das <xref:System.Data.SqlClient.SqlDependency>\-Objekt muss initialisiert werden, indem die `Start`\-Methode aufgerufen wird, um eine Abhängigkeit zur Datenbank festzulegen.  Dies ist eine statische Methode, die nur einmal während der Initialisierung der Anwendung für jede erforderliche Datenbankverbindung aufgerufen werden muss.  Für jede Abhängigkeit, die hergestellt wurde, sollte die `Stop`\-Methode bei Beenden der Anwendung aufgerufen werden.  
  
### Verwenden von "SqlNotificationRequest"  
 Im Gegensatz dazu erfordert <xref:System.Data.Sql.SqlNotificationRequest> das eigene Implementieren der gesamten Empfangsinfrastruktur.  Zusätzlich müssen alle unterstützenden Service Broker\-Objekte \(z. B. die Warteschlange, der Dienst und die von der Warteschlange unterstützen Meldungstypen\) definiert werden.  Dieser manuelle Ansatz ist nützlich, wenn Ihre Anwendung besondere Benachrichtigungsmeldungen oder ein besonderes Benachrichtigungsverhalten erfordert oder wenn die Anwendung Teil einer größeren Service Broker\-Anwendung ist.  
  
## Siehe auch  
 [Abfragebenachrichtigungen in SQL Server](../../../../../docs/framework/data/adonet/sql/query-notifications-in-sql-server.md)   
 [ADO.NET Verwaltete Anbieter und DataSet\-Entwicklercenter](http://go.microsoft.com/fwlink/?LinkId=217917)