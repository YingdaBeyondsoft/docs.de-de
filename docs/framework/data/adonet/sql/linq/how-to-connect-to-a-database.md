---
title: "Vorgehensweise: Herstellen einer Verbindung zu einer Datenbank | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c33d74b3-530d-421b-a121-96786dd263a5
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Vorgehensweise: Herstellen einer Verbindung zu einer Datenbank
Der <xref:System.Data.Linq.DataContext> ist die "Hauptleitung" für die Verbindung zu einer Datenbank, für das Abrufen von Objekten und für das Übergeben von Änderungen.  Sie verwenden den <xref:System.Data.Linq.DataContext> so wie eine [!INCLUDE[vstecado](../../../../../../includes/vstecado-md.md)] <xref:System.Data.SqlClient.SqlConnection>.  Tatsächlich wird der <xref:System.Data.Linq.DataContext> mit einer von Ihnen angegebenen Verbindung oder Verbindungszeichenfolge initialisiert.  Weitere Informationen finden Sie unter [DataContext\-Methoden \(O\/R\-Designer\)](../Topic/DataContext%20Methods%20\(O-R%20Designer\).md).  
  
 Der Zweck des <xref:System.Data.Linq.DataContext> besteht in der Übersetzung Ihrer Objektanforderungen in SQL\-Abfragen für die Datenbank und in der anschließenden Zusammenstellung von Objekten aus den Ergebnissen.  Der <xref:System.Data.Linq.DataContext> unterstützt [!INCLUDE[vbteclinqext](../../../../../../includes/vbteclinqext-md.md)] durch die Implementierung des gleichen Operatormusters wie bei den standardmäßigen Abfrageoperatoren, z. B. `Where` und `Select`.  
  
> [!IMPORTANT]
>  Der Erhalt einer sicheren Verbindung ist von grundlegender Bedeutung.  Weitere Informationen finden Sie unter [Sicherheit in LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/security-in-linq-to-sql.md).  
  
## Beispiel  
 Im folgenden Beispiel wird der <xref:System.Data.Linq.DataContext> zum Herstellen einer Verbindung zur Beispieldatenbank Nordwind und zum Abrufen von Zeilen mit Kunden aus London verwendet.  
  
 [!code-csharp[DLinqCommunicatingWithDatabase#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCommunicatingWithDatabase/cs/Program.cs#1)]
 [!code-vb[DLinqCommunicatingWithDatabase#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCommunicatingWithDatabase/vb/Module1.vb#1)]  
  
 Jede Datenbanktabelle wird als `Table`\-Auflistung dargestellt, die über die <xref:System.Data.Linq.DataContext.GetTable%2A>\-Methode zur Verfügung steht. Zur Identifikation wird hierbei die Entitätsklasse verwendet.  
  
## Beispiel  
 Die bewährte Methode besteht in der Deklaration eines starken <xref:System.Data.Linq.DataContext> anstelle der grundlegenden <xref:System.Data.Linq.DataContext>\-Klasse und der <xref:System.Data.Linq.DataContext.GetTable%2A>\-Methode.  Ein starker <xref:System.Data.Linq.DataContext> deklariert alle `Table`\-Auflistungen wie im folgenden Beispiel als Kontextmember.  
  
 [!code-csharp[DLinqCommunicatingWithDatabase#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCommunicatingWithDatabase/cs/Program.cs#2)]
 [!code-vb[DLinqCommunicatingWithDatabase#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCommunicatingWithDatabase/vb/Module1.vb#2)]  
  
 Sie können dann die Abfrage von Kunden aus London wie folgt einfacher ausdrücken:  
  
 [!code-csharp[DLinqCommunicatingWithDatabase#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCommunicatingWithDatabase/cs/Program.cs#5)]
 [!code-vb[DLinqCommunicatingWithDatabase#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCommunicatingWithDatabase/vb/Module1.vb#5)]  
  
## Siehe auch  
 [Kommunizieren mit der Datenbank](../../../../../../docs/framework/data/adonet/sql/linq/communicating-with-the-database.md)