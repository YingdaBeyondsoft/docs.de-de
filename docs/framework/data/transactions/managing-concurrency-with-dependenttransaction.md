---
title: "Verwalten von Parallelit&#228;t mit DependentTransaction  | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b85a97d8-8e02-4555-95df-34c8af095148
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Verwalten von Parallelit&#228;t mit DependentTransaction 
Das <xref:System.Transactions.Transaction>\-Objekt wird mit der <xref:System.Transactions.Transaction.DependentClone%2A>\-Methode erstellt.Sein einziger Zweck besteht darin, sicherzustellen, dass die Transaktion keinen Commit durchführen kann, während andere Codeteile \(beispielsweise ein Arbeitsthread\) noch Aktionen für die Transaktion ausführen.Wenn die Aktionen innerhalb der geklonten Transaktion abgeschlossen und für den Commit bereit sind, kann es den Ersteller der Transaktion mithilfe der <xref:System.Transactions.DependentTransaction.Complete%2A>\-Methode informieren.Auf diese Weise können Sie Konsistenz und Richtigkeit der Daten bewahren.  
  
 Die <xref:System.Transactions.DependentTransaction>\-Klasse kann ebenfalls verwendet werden, um Parallelität zwischen asynchronen Aufgaben zu verwalten.Bei diesem Szenario kann das übergeordnete Element weiter Code ausführen, während der abhängige Klon seine eigenen Aufgaben ausführt.Anders ausgedrückt wird die Ausführung des übergeordneten Elements nicht blockiert, solange die Ausführung des abhängigen Elements nicht abgeschlossen ist.  
  
## Erstellen eines abhängigen Klons  
 Um eine abhängige Transaktion zu erstellen, rufen Sie die <xref:System.Transactions.Transaction.DependentClone%2A>\-Methode auf, und übergeben Sie die <xref:System.Transactions.DependentCloneOption>\-Enumeration als Parameter.Dieser Parameter definiert das Verhalten der Transaktion, wenn `Commit` für die übergeordnete Transaktion aufgerufen wird, bevor der abhängige Klon anzeigt, dass er für den Transaktionscommit bereit ist \(durch Aufrufen der <xref:System.Transactions.DependentTransaction.Complete%2A>\-Methode\).Die folgenden Werte sind für diesen Parameter gültig:  
  
-   <xref:System.Transactions.DependentCloneOption> erstellt eine abhängige Transaktion, die den Commitvorgang der übergeordneten Transaktion blockiert, bis das Zeitlimit überschritten wird oder der Aufruf von <xref:System.Transactions.DependentTransaction.Complete%2A> für alle abhängigen Transaktionen erfolgt ist, weil diese abgeschlossen wurden.Das ist nützlich, wenn der Client den Commit der übergeordneten Transaktion erst zulassen will, wenn die abhängigen Transaktionen abgeschlossen sind.Wenn die übergeordnete Transaktion ihre Aufgaben früher abschließt als die abhängige Transaktion und <xref:System.Transactions.CommittableTransaction.Commit%2A> für die Transaktion aufruft, wird der Commitprozess in einem Zustand blockiert, in dem weitere Aufgaben für die Transaktion ausgeführt und neue Eintragungen vorgenommen werden können, bis alle abhängigen Transaktionen <xref:System.Transactions.DependentTransaction.Complete%2A> aufrufen.Sobald alle ihre Aufgaben abgeschlossen und <xref:System.Transactions.DependentTransaction.Complete%2A> aufgerufen haben, beginnt der Commitprozess für die Transaktion.  
  
-   <xref:System.Transactions.DependentCloneOption> hingegen erstellt eine abhängige Transaktion, die automatisch abgebrochen wird, wenn <xref:System.Transactions.CommittableTransaction.Commit%2A> für die übergeordnete Transaktion aufgerufen wird, bevor <xref:System.Transactions.DependentTransaction.Complete%2A> aufgerufen wird.In diesem Fall bleiben alle für die abhängige Transaktion ausgeführten Aktionen innerhalb einer Transaktionslebensdauer intakt. Es ist nicht möglich, einen Commit nur für einen Teil davon auszuführen.  
  
 Die <xref:System.Transactions.DependentTransaction.Complete%2A>\-Methode darf nur einmal aufgerufen werden, wenn die Anwendung ihre Aufgaben für die abhängige Transaktion beendet hat; anderenfalls wird eine <xref:System.InvalidOperationException>\-Ausnahme ausgelöst.Führen Sie nach diesem Aufruf keine weiteren Aktionen für die Transaktion aus. Andernfalls wird eine Ausnahme ausgelöst.  
  
 Das folgende Codebeispiel zeigt, wie eine abhängige Transaktion mit dem Ziel erstellt wird, zwei parallele Aufgaben durch Klonen einer abhängigen Transaktion und Übergabe der Transaktion an einen Arbeitsthread zu verwalten.  
  
```csharp  
public class WorkerThread  
{  
    public void DoWork(DependentTransaction dependentTransaction)  
    {  
        Thread thread = new Thread(ThreadMethod);  
        thread.Start(dependentTransaction);   
    }  
  
    public void ThreadMethod(object transaction)   
    {   
        DependentTransaction dependentTransaction = transaction as DependentTransaction;  
        Debug.Assert(dependentTransaction != null);   
        try  
        {  
            using(TransactionScope ts = new TransactionScope(dependentTransaction))  
            {  
                /* Perform transactional work here */   
                ts.Complete();  
            }  
        }  
        finally  
        {  
            dependentTransaction.Complete();   
             dependentTransaction.Dispose();   
        }  
    }  
  
//Client code   
using(TransactionScope scope = new TransactionScope())  
{  
    Transaction currentTransaction = Transaction.Current;  
    DependentTransaction dependentTransaction;      
    dependentTransaction = currentTransaction.DependentClone(DependentCloneOption.BlockCommitUntilComplete);  
    WorkerThread workerThread = new WorkerThread();  
    workerThread.DoWork(dependentTransaction);  
    /* Do some transactional work here, then: */  
    scope.Complete();  
}  
  
```  
  
 Der Clientcode erstellt einen Transaktionsbereich, der auch die Ambient\-Transaktion festlegt.Sie sollten die Ambient\-Transaktion nicht an den Arbeitsthread übergeben.Stattdessen sollten Sie die aktuelle \(Ambient\-\)Transaktion klonen, indem Sie die <xref:System.Transactions.Transaction.DependentClone%2A>\-Methode für die aktuelle Transaktion aufrufen und die abhängige an den Arbeitsthread übergeben.  
  
 Die `ThreadMethod`\-Methode wird für den neuen Thread ausgeführt.Der Client startet einen neuen Thread und übergibt die abhängige Transaktion als `ThreadMethod`\-Parameter.  
  
 Da die abhängige Transaktion mit <xref:System.Transactions.DependentCloneOption> erstellt wird, haben Sie die Gewissheit, dass der Transaktionscommit nicht ausgeführt werden kann, bevor alle Transaktionsaufgaben für den zweiten Thread abgeschlossen sind und <xref:System.Transactions.DependentTransaction.Complete%2A> für die abhängige Transaktion aufgerufen wurde.Das bedeutet: Wenn der Clientbereich endet \(wenn der Client versucht, am Ende der **using**\-Anweisung über das Transaktionsobjekt zu verfügen\), bevor der neue Thread <xref:System.Transactions.DependentTransaction.Complete%2A> für die abhängige Transaktion aufruft, blockiert der Clientcode, bis <xref:System.Transactions.DependentTransaction.Complete%2A> für die abhängige Transaktion aufgerufen wird.Dann kann die Transaktion durch Commit oder Abbruch beendet werden.  
  
## Parallelitätsprobleme  
 Es gibt noch einige weitere Parallelitätsaspekte, die Sie beachten müssen, wenn Sie die <xref:System.Transactions.DependentTransaction>\-Klasse verwenden:  
  
-   Wenn der Arbeitsthread einen Rollback für die Transaktion ausführt, die übergeordnete Transaktion jedoch versucht, einen Commit dafür auszuführen, wird eine <xref:System.Transactions.TransactionAbortedException>\-Ausnahme ausgelöst.  
  
-   Sie sollten einen neuen abhängigen Klon für jeden Arbeitsthread in der Transaktion erstellen.Übergeben Sie nicht denselben abhängigen Klon an mehrere Threads, da nur einer davon <xref:System.Transactions.DependentTransaction.Complete%2A> aufrufen kann.  
  
-   Wenn der Arbeitsthread einen neuen Arbeitsthread erzeugt, müssen Sie einen abhängigen Klon des abhängigen Klons erstellen und an den neuen Thread übergeben.  
  
## Siehe auch  
 <xref:System.Transactions.DependentTransaction>