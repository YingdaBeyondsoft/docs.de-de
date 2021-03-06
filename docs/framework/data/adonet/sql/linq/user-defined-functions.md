---
title: "Benutzerdefinierte Funktionen | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3304c9b2-5c7a-4a95-9d45-4f260dcb606e
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Benutzerdefinierte Funktionen
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] verwendet Methoden in Ihrem Objektmodell, die benutzerdefinierte Funktionen darstellen.  Sie definieren die Methoden als Funktionen, indem Sie das <xref:System.Data.Linq.Mapping.FunctionAttribute>\-Attribut und bei Bedarf auch das <xref:System.Data.Linq.Mapping.ParameterAttribute>\-Attribut anwenden.  Weitere Informationen finden Sie unter [Das LINQ to SQL\-Objektmodell](../../../../../../docs/framework/data/adonet/sql/linq/the-linq-to-sql-object-model.md).  
  
 Zur Vermeidung einer <xref:System.InvalidOperationException> müssen benutzerdefinierte Funktionen in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] in einer der folgenden Formen vorliegen:  
  
-   Eine als Methodenaufruf eingebundene Funktion, die über die richtigen Zuordnungsattribute verfügt.  Weitere Informationen finden Sie unter [Attributbasierte Zuordnung](../../../../../../docs/framework/data/adonet/sql/linq/attribute-based-mapping.md).  
  
-   Eine spezifische statische SQL\-Methode für [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  
  
-   Eine von einer [!INCLUDE[dnprdnshort](../../../../../../includes/dnprdnshort-md.md)]\-Methode unterstützte Funktion.  
  
 Dieser Abschnitt erläutert das Bilden und Aufrufen dieser Methoden in Ihrer Anwendung, wenn Sie den Code selbst schreiben.  Entwickler, die [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] verwenden, ordnen benutzerdefinierte Funktionen normalerweise mit dem [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] zu.  
  
## In diesem Abschnitt  
 [Vorgehensweise: Verwenden von benutzerdefinierten Skalarwertfunktionen](../../../../../../docs/framework/data/adonet/sql/linq/how-to-use-scalar-valued-user-defined-functions.md)  
 Beschreibt, wie eine Funktion, die Skalarwerte zurückgibt, implementiert wird.  
  
 [Vorgehensweise: Verwenden von benutzerdefinierten Funktionen mit Tabellenwerten](../../../../../../docs/framework/data/adonet/sql/linq/how-to-use-table-valued-user-defined-functions.md)  
 Beschreibt, wie eine Funktion, die Tabellenwerte zurückgibt, implementiert wird.  
  
 [Vorgehensweise: Inline\-Aufrufen von benutzerdefinierten Funktionen](../../../../../../docs/framework/data/adonet/sql/linq/how-to-call-user-defined-functions-inline.md)  
 Erläutert Inline\-Funktionsaufrufe und die Ausführungsunterschiede, wenn der Aufruf inline erfolgt.