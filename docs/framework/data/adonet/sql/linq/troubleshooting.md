---
title: "Problembehandlung | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8cd4401c-b12c-4116-a421-f3dcffa65670
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Problembehandlung
Die folgenden Informationen beziehen sich auf Probleme, die in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]\-Anwendungen auftreten können, und enthalten Vorschläge dazu, wie diese Probleme vermieden bzw. deren Auswirkungen auf andere Weise verringert werden können.  
  
 Weitere Probleme werden in [Häufig gestellte Fragen](../../../../../../docs/framework/data/adonet/sql/linq/frequently-asked-questions.md) behandelt.  
  
## Nicht unterstützte Standardabfrageoperatoren  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] unterstützt nicht alle Standardabfrageoperator\-Methoden \(z. B. <xref:System.Linq.Enumerable.ElementAt%2A>\).  Folglich können Projekte, die kompiliert werden, immer noch Laufzeitfehler verursachen.  Weitere Informationen finden Sie unter [Übersetzung von Standardabfrageoperatoren](../../../../../../docs/framework/data/adonet/sql/linq/standard-query-operator-translation.md).  
  
## Arbeitsspeicherprobleme  
 Wenn eine Abfrage sowohl eine speicherinterne Auflistung als auch [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <xref:System.Data.Linq.Table%601> enthält, wird die Ausführung u. U. im Arbeitsspeicher ausgeführt. Dies hängt davon ab, in welcher Reihenfolge die beiden Auflistungen angegeben sind.  Wenn die Abfrage im Arbeitsspeicher ausgeführt werden muss, müssen die Daten aus der Datenbanktabelle abgerufen werden.  
  
 Dieser Ansatz ist ineffizient und könnte zu einem erheblichen Anstieg der Arbeitsspeicher\- und Prozessornutzung führen.  Versuchen Sie, derartige Abfragen über mehrere Domänen zu vermeiden.  
  
## Dateinamen und SQLMetal  
 Um einen Namen für eine Eingabedatei anzugeben, fügen Sie den Namen der Befehlszeile als Eingabedatei hinzu.  Die Angabe des Dateinamens in der Verbindungszeichenfolge \(unter Verwendung der **\/conn**\-Option\) wird nicht unterstützt.  Weitere Informationen finden Sie unter [SqlMetal.exe \(Tool zur Codegenerierung\)](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md).  
  
## Klassenbibliotheksprojekte  
 [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] erstellt in der Datei `app.config` des Projekts eine Verbindungszeichenfolge.  In Klassenbibliotheksprojekten wird die Datei `app.config` nicht verwendet.  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] verwendet die in den Entwurfszeitdateien bereitgestellte Verbindungszeichenfolge.  Wenn Sie den Wert in `app.config` ändern, wird die Datenbank, mit der die Anwendung eine Verbindung herstellt, nicht geändert.  
  
## Kaskadierte Löschung  
 Kaskadierte Löschvorgänge werden von [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] nicht unterstützt bzw. erkannt.  Wenn Sie eine Zeile in einer Tabelle löschen möchten, für die Einschränkungen gelten, führen Sie eines der folgenden Verfahren aus:  
  
-   Legen Sie die `ON DELETE CASCADE`\-Regel in der Fremdschlüsseleinschränkung in der Datenbank fest.  
  
-   Verwenden Sie eigenen Code, um zunächst die untergeordneten Objekte zu löschen, die das Löschen des übergeordneten Objekts verhindern.  
  
 Andernfalls wird eine <xref:System.Data.SqlClient.SqlException>\-Ausnahme ausgelöst.  
  
 Weitere Informationen finden Sie unter [Vorgehensweise: Löschen von Zeilen aus der Datenbank](../../../../../../docs/framework/data/adonet/sql/linq/how-to-delete-rows-from-the-database.md).  
  
## Ausdruck kann nicht abgefragt werden  
 Falls der Fehler "Der Ausdruck \[Ausdruck\] kann nicht abgefragt werden. Möglicherweise fehlt ein Assemblyverweis" auftritt, stellen Sie Folgendes sicher:  
  
-   Die Anwendung muss auf [!INCLUDE[compact_v35_short](../../../../../../includes/compact-v35-short-md.md)] abzielen.  
  
-   Sie müssen über einen Verweis auf `System.Core.dll` und `System.Data.Linq.dll` verfügen.  
  
-   Sie müssen über eine `Imports`\-Direktive \([!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)]\) oder `using`\-Direktive \(C\#\) für <xref:System.Linq> und <xref:System.Data.Linq> verfügen.  
  
## DuplicateKeyException  
 Beim Debuggen eines [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]\-Projekts kann es vorkommen, dass die Beziehungen einer Entität durchlaufen werden.  Dadurch werden diese Elemente in den Cache eingefügt und von [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] erkannt.  Wenn Sie dann versuchen, <xref:System.Data.Linq.Table%601.Attach%2A> oder <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A> bzw. eine ähnliche Methode auszuführen, durch die mehrere Zeilen mit demselben Schlüssel generiert werden, wird eine <xref:System.Data.Linq.DuplicateKeyException> ausgelöst.  
  
## Ausnahmen bei der Zeichenfolgenverkettung  
 Die Verkettung von Operanden, die `[n]text` zugeordnet sind, und anderen, die `[n][var]char` zugeordnet sind, wird nicht unterstützt.  Bei der Verkettung von Zeichenfolgen, die zwei verschiedenen Typsätzen zugeordnet sind, wird eine Ausnahme ausgelöst.  Weitere Informationen finden Sie unter [System.String\-Methoden](../../../../../../docs/framework/data/adonet/sql/linq/system-string-methods.md).  
  
## Überspringen und Behandeln von Ausnahmen in SQL Server 2000  
 Bei Verwendung von <xref:System.Linq.Queryable.Take%2A> oder <xref:System.Linq.Queryable.Skip%2A> für eine SQL Server 2000\-Datenbank müssen Identitätsmember \(<xref:System.Data.Linq.Mapping.ColumnAttribute.IsPrimaryKey%2A>\) verwendet werden.  Die Abfrage muss gegen eine einzelne Tabelle \(keinen Join\) ausgeführt werden oder einen der Vorgänge <xref:System.Linq.Queryable.Distinct%2A>, <xref:System.Linq.Queryable.Except%2A>, <xref:System.Linq.Queryable.Intersect%2A> oder <xref:System.Linq.Queryable.Union%2A> darstellen und darf keinen <xref:System.Linq.Queryable.Concat%2A>\-Vorgang beinhalten.  Weitere Informationen finden Sie im Abschnitt "SQL Server 2000\-Unterstützung" unter [Übersetzung von Standardabfrageoperatoren](../../../../../../docs/framework/data/adonet/sql/linq/standard-query-operator-translation.md).  
  
 Diese Anforderung gilt nicht für [!INCLUDE[sqprsqlong](../../../../../../includes/sqprsqlong-md.md)].  
  
## GroupBy InvalidOperationException  
 Diese Ausnahme wird ausgelöst, wenn ein Spaltenwert in einer <xref:System.Linq.Enumerable.GroupBy%2A>\-Abfrage, die eine Gruppierung nach einem `boolean`\-Ausdruck ausführt, z. B. `group x by (Phone==@phone)`, NULL ist.  Da der Ausdruck `boolean` ist, wird davon ausgegangen, dass der Schlüssel `boolean` und nicht `nullable``boolean` ist.  Wenn der übersetzte Vergleich NULL ergibt, wird versucht, `boolean` den Wert `nullable` `boolean` zuzuweisen, und die Ausnahme wird ausgelöst.  
  
 Um diese Situation zu vermeiden \(vorausgesetzt, NULL soll als false behandelt werden\), verwenden Sie eine Lösung wie die folgende:  
  
 `GroupBy="(Phone != null) && (Phone=@Phone)"`  
  
## OnCreated\(\) \(Partielle Methode\)  
 Die generierte `OnCreated()`\-Methode wird jedes Mal aufgerufen, sobald der Objektkonstruktor aufgerufen wird, beispielsweise auch dann, wenn [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] den Konstruktor aufruft, um eine Kopie für ursprüngliche Werte zu erstellen.  Sie sollten dieses Verhalten berücksichtigen, wenn Sie die `OnCreated()`\-Methode in einer eigenen partiellen Klasse implementieren.  
  
## Siehe auch  
 [Debuggingunterstützung](../../../../../../docs/framework/data/adonet/sql/linq/debugging-support.md)   
 [Häufig gestellte Fragen](../../../../../../docs/framework/data/adonet/sql/linq/frequently-asked-questions.md)