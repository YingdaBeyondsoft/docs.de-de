---
title: "SET (Entity SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "ESQL"
ms.assetid: 28b4deac-c7e4-4f09-b428-4d352ef2dc94
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# SET (Entity SQL)
Der SET\-Ausdruck wird verwendet, um eine Auflistung von Objekten in eine Menge zu konvertieren, indem eine neue Auflistung zurückgegeben wird, aus der alle doppelten Elemente entfernt wurden.  
  
## Syntax  
  
```  
  
SET (expression)  
```  
  
## Argumente  
 `expression`  
 Jeder gültige Abfrageausdruck, der eine Auflistung zurückgibt.  
  
## Hinweise  
 Der Mengenausdruck `SET(c)` ist logisch äquivalent zur folgenden SELECTAnweisung:  
  
```  
SELECT VALUE DISTINCT c FROM c  
```  
  
 `SET` ist einer der [!INCLUDE[esql](../../../../../../includes/esql-md.md)]\-Mengenoperatoren. Alle [!INCLUDE[esql](../../../../../../includes/esql-md.md)]\-Mengenoperatoren werden von links nach rechts ausgewertet. Informationen über die Rangfolge der [!INCLUDE[esql](../../../../../../includes/esql-md.md)]\-Mengenoperatoren finden Sie unter [EXCEPT](../../../../../../docs/framework/data/adonet/ef/language-reference/except-entity-sql.md).  
  
## Beispiel  
 Die folgende Entity SQL\-Abfrage verwendet den SET\-Ausdruck, um eine Auflistung von Objekten in eine Menge zu konvertieren. Diese Abfrage beruht auf dem "AdventureWorks Sales"\-Modell. Führen Sie folgende Schritte aus, um diese Abfrage zu kompilieren und auszuführen:  
  
1.  Verwenden Sie das Verfahren unter [Vorgehensweise: Ausführen einer Abfrage, die PrimitiveType\-Ergebnisse zurückgibt](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-primitivetype-results.md).  
  
2.  Übergeben Sie die folgende Abfrage als Argument an die `ExecutePrimitiveTypeQuery`\-Methode:  
  
 [!code-csharp[DP EntityServices Concepts 2#SET](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#set)]  
  
## Siehe auch  
 [Entity SQL\-Referenz](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)