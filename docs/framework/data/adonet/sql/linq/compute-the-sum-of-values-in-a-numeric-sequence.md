---
title: "Vorgehensweise: Berechnen der Summe von Werten in einer numerischen Sequenz | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 24e335b0-984e-4825-8721-0a91b533b7c3
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Vorgehensweise: Berechnen der Summe von Werten in einer numerischen Sequenz
Verwenden Sie den <xref:System.Linq.Enumerable.Sum%2A>\-Operator, um die Summe numerischer Werte in einer Sequenz zu berechnen.  
  
 Beachten Sie die folgenden Merkmale des `Sum`\-Operators in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]:  
  
-   Der `Sum`\-Operator für Standardabfragen führt bei einer leeren Sequenz oder bei einer aus Nullen bestehenden Sequenz zum Ergebnis NULL.  In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] bleibt die SQL\-Semantik unverändert.  Aus diesem Grund ergibt `Sum` bei einer leeren Sequenz oder bei einer aus Nullen bestehenden Sequenz den Wert NULL an Stelle von 0.  
  
-   SQL\-Einschränkungen für Zwischenergebnisse gelten in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] für Summen.  Die Summe von 32\-Bit\-Ganzzahlen wird nicht mithilfe von 64\-Bit\-Ergebnissen berechnet, und bei der [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]\-Übersetzung von `Sum` kann es zu einem Überlauf kommen.  Dies kann ggf. auch eintreten, wenn die standardmäßige Implementierung des Abfrageoperators bei der entsprechenden Sequenz im Arbeitsspeicher nicht zu einem Überlauf führt.  
  
## Beispiel  
 Im folgenden Beispiel wird die gesamte Fracht zu allen Bestellungen in der Tabelle `Order` ermittelt.  
  
 Wenn Sie diese Abfrage mit der Beispieldatenbank Northwind ausführen, lautet die Ausgabe `64942.6900`.  
  
 [!code-csharp[DLinqQueryExamples#12](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#12)]
 [!code-vb[DLinqQueryExamples#12](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#12)]  
  
## Beispiel  
 Im folgenden Beispiel wird die Gesamtzahl von bestellen Einheiten für alle Produkte ermittelt.  
  
 Wenn Sie diese Abfrage mit der Beispieldatenbank Northwind ausführen, lautet die Ausgabe `780`.  
  
 Beachten Sie, dass Sie `short`\-Typen \(z. B. `UnitsOnOrder`\) verwenden müssen, da `Sum` nicht über einen Überlauf für diese Typen verfügt.  
  
 [!code-csharp[DLinqQueryExamples#13](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#13)]
 [!code-vb[DLinqQueryExamples#13](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#13)]  
  
## Siehe auch  
 [Aggregatabfragen](../../../../../../docs/framework/data/adonet/sql/linq/aggregate-queries.md)   
 [Herunterladen von Beispieldatenbanken](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md)