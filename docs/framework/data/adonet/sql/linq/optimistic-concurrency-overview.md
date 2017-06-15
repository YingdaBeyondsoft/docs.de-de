---
title: "Vollst&#228;ndige Parallelit&#228;t: &#220;bersicht | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c2e38512-d0c8-4807-b30a-cb7e30338694
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Vollst&#228;ndige Parallelit&#228;t: &#220;bersicht
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] unterstützt die Steuerung der vollständigen Parallelität.  In der folgenden Tabelle werden Begriffe beschrieben, die in der [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]\-Dokumentation für vollständige Parallelität gelten:  
  
|Begriffe|Beschreibung|  
|--------------|------------------|  
|Parallelität|Die Situation, in der zwei oder mehr Benutzer gleichzeitig versuchen, die gleiche Datenbankzeile zu aktualisieren.|  
|Parallelitätskonflikt|Die Situation, in der zwei oder mehr Benutzer gleichzeitig versuchen, konkurrierende Werte an eine oder mehrere Datenbankzeilen zu übergeben.|  
|Parallelitätssteuerung|Die Technik zur Behebung von Parallelitätskonflikten.|  
|Steuerelement für vollständige Parallelität|Die Technik zur Prüfung, ob andere Transaktionen die Werte in einer Zeile geändert haben, bevor die Übergabe von Änderungen zugelassen wird.<br /><br /> Gegensatz zur *Steuerung der unvollständigen Parallelität*, die den Datensatz sperrt, um Parallelitätskonflikte zu vermeiden.<br /><br /> Die *vollständige*  Steuerung verdankt ihre Bezeichnung der Tatsache, dass sie davon ausgeht, dass ein Konflikt zwischen Transaktionen unwahrscheinlich ist.|  
|Konfliktlösung|Der Prozess des Aktualisierens eines problematischen Elements durch eine erneute Datenbankabfrage und Ausgleichen der Unterschiede.<br /><br /> Wenn ein Objekt aktualisiert wird, enthält der [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]\-Änderungsprotokollierer die folgenden Daten:<br /><br /> -   Die ursprünglich aus der Datenbank abgerufenen Werte, die für die Updateprüfung verwendet wurden.<br />-   Die neuen Datenbankwerte aus der nachfolgenden Abfrage.<br /><br /> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] ermittelt dann, ob ein Objektkonflikt vorliegt \(d. h., ob sich die Werte von einem oder mehreren Membern geändert haben\).  Liegt ein Objektkonflikt vor, ermittelt [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] dann, bei welchem Member dieser Konflikt auftritt.<br /><br /> Jeder von [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] erkannte Memberkonflikt wird einer Konfliktliste hinzugefügt.|  
  
 Im [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]\-Objektmodell tritt ein *Konflikt bei der vollständigen Parallelität* auf, wenn die beiden folgenden Bedingungen eintreten:  
  
-   Der Client versucht, Änderungen an die Datenbank zu übergeben.  
  
-   Ein oder mehrere Werte der Updateprüfung wurden in der Datenbank aktualisiert, seit der Client sie zuletzt gelesen hat.  
  
 Die Behebung dieses Konflikts umfasst die Erkennung der Member, bei deren Objekten der Konflikt auftritt. Anschließend wird entschieden, wie weiter vorgegangen wird.  
  
> [!NOTE]
>  Nur die als <xref:System.Data.Linq.Mapping.UpdateCheck> oder <xref:System.Data.Linq.Mapping.UpdateCheck> zugeordneten Member nehmen an Prüfungen der vollständigen Parallelität teil.  Für die als <xref:System.Data.Linq.Mapping.UpdateCheck> gekennzeichneten Member finden keine Prüfungen statt.  Weitere Informationen finden Sie unter <xref:System.Data.Linq.Mapping.UpdateCheck>.  
  
## Beispiel  
 Im folgenden Szenario bereitet beispielsweise User1 ein Update vor, indem er eine Zeile aus der Datenbank abruft.  User1 empfängt eine Zeile mit Werten von Alfreds, Maria und Sales.  
  
 User1 möchte den Wert der Manager\-Spalte in Alfred und den Wert der Department\-Spalte in Marketing ändern.  Bevor User1 diese Änderungen übergeben kann, hat User2 Änderungen an der Datenbank vorgenommen.  Damit wurde der Wert der Assistant\-Spalte in Mary und der Wert der Department\-Spalte in Service geändert.  
  
 Wenn User1 jetzt versucht, Änderungen zu übergeben, schlägt die Übergabe fehl, und eine <xref:System.Data.Linq.ChangeConflictException>\-Ausnahme wird ausgelöst.  Dieser Fall tritt ein, weil die Datenbankwerte der Assistant\-Spalte und der Department\-Spalte nicht den Erwartungen entsprechen.  Bei Membern, die die Assistant\-Spalte und die Department\-Spalte vertreten, tritt ein Konflikt auf.  Die folgende Tabelle fasst diese Situation zusammen.  
  
||Manager|Assistant|Department|  
|------|-------------|---------------|----------------|  
|Ursprünglicher Zustand|Alfreds|Maria|Sales|  
|User1|Alfred||Marketing|  
|User2||Mary|Dienst|  
  
 Sie können Konflikte wie diesen auf verschiedene Weise lösen.  Weitere Informationen finden Sie unter [Vorgehensweise: Verwalten von Änderungskonflikten](../../../../../../docs/framework/data/adonet/sql/linq/how-to-manage-change-conflicts.md).  
  
## Checkliste für Konflikterkennung und \-behebung  
 Sie können Konflikte auf jeder Detailebene erkennen und beheben.  Einerseits können Sie alle Konflikte auf eine von drei Arten beheben \(siehe <xref:System.Data.Linq.RefreshMode>\). Hierbei müssen keine weiteren Aspekte berücksichtigt werden.  Andererseits können Sie für jeden Konflikttyp bei jedem Member eine bestimmte Aktion zuweisen.  
  
-   Definieren oder überarbeiten Sie die <xref:System.Data.Linq.Mapping.UpdateCheck>\-Optionen in Ihrem Objektmodell.  
  
     Weitere Informationen finden Sie unter [Vorgehensweise: Angeben, welche Member auf Parallelitätskonflikte getestet werden](../../../../../../docs/framework/data/adonet/sql/linq/how-to-specify-which-members-are-tested-for-concurrency-conflicts.md).  
  
-   Im Try\/Catch\-Block Ihres Aufrufs für <xref:System.Data.Linq.DataContext.SubmitChanges%2A> können Sie angeben, zu welchem Zeitpunkt die Ausnahmen ausgelöst werden sollen.  
  
     Weitere Informationen finden Sie unter [Vorgehensweise: Angeben des Zeitpunkts, zu dem Parallelitätsausnahmen ausgelöst werden](../../../../../../docs/framework/data/adonet/sql/linq/how-to-specify-when-concurrency-exceptions-are-thrown.md).  
  
-   Ermitteln Sie, wie viele Konfliktdetails Sie abrufen möchten, und gestalten Sie den Try\/Catch\-Block entsprechend.  
  
     Weitere Informationen finden Sie unter [Vorgehensweise: Abrufen von Entitätskonfliktinformationen](../../../../../../docs/framework/data/adonet/sql/linq/how-to-retrieve-entity-conflict-information.md) und [Vorgehensweise: Abrufen von Memberkonfliktinformationen](../../../../../../docs/framework/data/adonet/sql/linq/how-to-retrieve-member-conflict-information.md).  
  
-   Definieren Sie in Ihrem `try`\-\/`catch`\-Code, wie Sie die verschiedenen ermittelten Konflikte beheben möchten.  
  
     Weitere Informationen finden Sie unter [Vorgehensweise: Beheben von Konflikten durch Beibehalten von Datenbankwerten](../../../../../../docs/framework/data/adonet/sql/linq/how-to-resolve-conflicts-by-retaining-database-values.md), [Vorgehensweise: Beheben von Konflikten durch Überschreiben von Datenbankwerten](../../../../../../docs/framework/data/adonet/sql/linq/how-to-resolve-conflicts-by-overwriting-database-values.md) und [Vorgehensweise: Lösen von Konflikten durch Zusammenführen mit Datenbankwerten](../../../../../../docs/framework/data/adonet/sql/linq/how-to-resolve-conflicts-by-merging-with-database-values.md).  
  
## LINQ to SQL\-Typen, die Konfliktermittlung und \-behebung unterstützen  
 Zu den Klassen und Funktionen, die die Behebung von Konflikten bei der vollständigen Parallelität in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] unterstützen, zählen:  
  
-   <xref:System.Data.Linq.ObjectChangeConflict?displayProperty=fullName>  
  
-   <xref:System.Data.Linq.MemberChangeConflict?displayProperty=fullName>  
  
-   <xref:System.Data.Linq.ChangeConflictCollection?displayProperty=fullName>  
  
-   <xref:System.Data.Linq.ChangeConflictException?displayProperty=fullName>  
  
-   <xref:System.Data.Linq.DataContext.ChangeConflicts%2A?displayProperty=fullName>  
  
-   <xref:System.Data.Linq.DataContext.SubmitChanges%2A?displayProperty=fullName>  
  
-   <xref:System.Data.Linq.DataContext.Refresh%2A?displayProperty=fullName>  
  
-   <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A?displayProperty=fullName>  
  
-   <xref:System.Data.Linq.Mapping.UpdateCheck?displayProperty=fullName>  
  
-   <xref:System.Data.Linq.RefreshMode?displayProperty=fullName>  
  
## Siehe auch  
 [Vorgehensweise: Verwalten von Änderungskonflikten](../../../../../../docs/framework/data/adonet/sql/linq/how-to-manage-change-conflicts.md)