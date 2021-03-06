---
title: "Diensttransaktionsverhalten | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Beispiel zum Diensttransaktionsverhalten [Windows Communication Foundation]"
ms.assetid: 1a9842a3-e84d-427c-b6ac-6999cbbc2612
caps.latest.revision: 28
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 28
---
# Diensttransaktionsverhalten
In diesem Beispiel werden die Verwendung einer clientkoordinierten Transaktion und die Einstellungen von ServiceBehaviorAttribute und OperationBehaviorAttribute zum Steuern des Diensttransaktionsverhaltens veranschaulicht.Dieses Beispiel basiert auf [Erste Schritte](../../../../docs/framework/wcf/samples/getting-started-sample.md), in dem ein Rechnerdienst implementiert wird. Dieses Beispiel wird jedoch erweitert, um ein Serverprotokoll der ausgeführten Vorgänge in einer Datenbanktabelle und eine statusbehaftete laufende Summe der Rechnervorgänge zu verwenden.Beibehaltene Schreibvorgänge in der Serverprotokolltabelle sind abhängig vom Ergebnis einer clientkoordinierten Transaktion. Wenn die Clienttransaktion nicht abgeschlossen wird, stellt die Webdiensttransaktion sicher, dass die Aktualisierungen der Datenbank nicht ausgeführt werden.  
  
> [!NOTE]
>  Die Setupprozedur und die Buildanweisungen für dieses Beispiel befinden sich am Ende dieses Themas.  
  
 Der Vertrag für den Dienst definiert, dass für alle Vorgänge eine Transaktion mit Anforderungen übergeben werden muss:  
  
```  
[ServiceContract(Namespace = "http://Microsoft.ServiceModel.Samples",  
                    SessionMode = SessionMode.Required)]  
public interface ICalculator  
{  
    [OperationContract]  
    [TransactionFlow(TransactionFlowOption.Mandatory)]  
    double Add(double n);  
    [OperationContract]  
    [TransactionFlow(TransactionFlowOption.Mandatory)]  
    double Subtract(double n);  
    [OperationContract]  
    [TransactionFlow(TransactionFlowOption.Mandatory)]  
    double Multiply(double n);  
    [OperationContract]  
    [TransactionFlow(TransactionFlowOption.Mandatory)]  
    double Divide(double n);  
}  
  
```  
  
 Zum Aktivieren des eingehenden Transaktionsflusses wird der Dienst mit der vom System bereitgestellten wsHttpBinding konfiguriert, wobei das transactionFlow\-Attribut auf `true` festgelegt ist.Diese Bindung verwendet das interoperable WSAtomicTransactionOctober2004\-Protokoll:  
  
```  
<bindings>  
  <wsHttpBinding>  
    <binding name="transactionalBinding" transactionFlow="true" />  
  </wsHttpBinding>  
</bindings>  
  
```  
  
 Nach dem Initiieren einer Verbindung mit dem Dienst und einer Transaktion greift der Client auf mehrere Dienstvorgänge im Bereich der Transaktion zu, schließt die Transaktion ab und trennt die Verbindung:  
  
```  
// Create a client  
CalculatorClient client = new CalculatorClient();  
  
// Create a transaction scope with the default isolation level of Serializable  
using (TransactionScope tx = new TransactionScope())  
{  
    Console.WriteLine("Starting transaction");  
  
    // Call the Add service operation.  
    double value = 100.00D;  
    Console.WriteLine("  Adding {0}, running total={1}",  
                                        value, client.Add(value));  
  
    // Call the Subtract service operation.  
    value = 45.00D;  
    Console.WriteLine("  Subtracting {0}, running total={1}",  
                                        value, client.Subtract(value));  
  
    // Call the Multiply service operation.  
    value = 9.00D;  
    Console.WriteLine("  Multiplying by {0}, running total={1}",  
                                        value, client.Multiply(value));  
  
    // Call the Divide service operation.  
    value = 15.00D;  
    Console.WriteLine("  Dividing by {0}, running total={1}",  
                                        value, client.Divide(value));  
  
    Console.WriteLine("  Completing transaction");  
    tx.Complete();  
}  
  
Console.WriteLine("Transaction committed");  
  
// Closing the client gracefully closes the connection and cleans up resources  
client.Close();  
```  
  
 Bei dem Dienst gibt es drei Attribute, die Auswirkungen auf das Diensttransaktionsverhalten haben. Dies geschieht wie folgt:  
  
-   Für `ServiceBehaviorAttribute`:  
  
    -   Die `TransactionTimeout`\-Eigenschaft gibt den Zeitraum an, innerhalb dessen eine Transaktion abgeschlossen werden muss.In diesem Beispiel ist sie auf 30 Sekunden festgelegt.  
  
    -   Die `TransactionIsolationLevel`\-Eigenschaft gibt die Isolationsstufe an, die der Dienst unterstützt.Dies ist zur Übereinstimmung mit der Isolationsstufe des Clients erforderlich.  
  
    -   Die `ReleaseServiceInstanceOnTransactionComplete`\-Eigenschaft legt fest, ob die Dienstinstanz beim Abschluss einer Transaktion wiederverwendet wird.Durch das Festlegen auf `false` behält der Dienst die gleiche Dienstinstanz über die Vorgangsanforderungen hinweg bei.Dies ist für das Beibehalten der laufenden Gesamtsumme erforderlich.Beim Festlegen auf `true` wird nach jeder abgeschlossenen Aktion eine neue Instanz generiert.  
  
    -   Die `TransactionAutoCompleteOnSessionClose`\-Eigenschaft gibt an, ob ausstehende Transaktionen abgeschlossen werden, wenn die Sitzung geschlossen wird.Durch Festlegen auf `false` müssen die einzelnen Vorgänge die `OperationBehaviorAttribute``TransactionAutoComplete`\-Eigenschaft auf `true` festlegen oder explizit einen Aufruf der `SetTransactionComplete`\-Methode anfordern, um Transaktionen abzuschließen.In diesem Beispiel werden beide Ansätze veranschaulicht.  
  
-   Für `ServiceContractAttribute`:  
  
    -   Die `SessionMode`\-Eigenschaft gibt an, ob der Dienst die entsprechenden Anforderungen in eine logische Sitzung korreliert.Da dieser Dienst Vorgänge umfasst, bei denen die OperationBehaviorAttribute TransactionAutoComplete\-Eigenschaft auf `false` festgelegt ist \(Multiply und Divide\), muss `SessionMode.Required` angegeben werden.Der Multiply\-Vorgang schließt seine Transaktion beispielsweise nicht ab und benötigt stattdessen den Abschluss eines späteren Aufrufs von Divide mithilfe der `SetTransactionComplete`\-Methode. Der Dienst muss bestimmen können, dass diese Vorgänge in der gleichen Sitzung ausgeführt werden.  
  
-   Für `OperationBehaviorAttribute`:  
  
    -   Die `TransactionScopeRequired`\-Eigenschaft gibt an, ob die Aktionen des Vorgangs innerhalb eines Transaktionsbereichs ausgeführt werden sollen.Dies ist für alle Vorgänge in diesem Beispiel auf `true` festgelegt, und da der Client seine Transaktion auf alle Vorgänge überträgt, treten die Aktionen im Bereich dieser Clienttransaktion auf.  
  
    -   Die `TransactionAutoComplete`\-Eigenschaft legt fest, ob die Transaktion, in der die Methode ausgeführt wird, automatisch abgeschlossen wird, wenn keine nicht behandelten Ausnahmen ausgelöst werden.Wie oben beschrieben, ist dies für den Add\-Vorgang und den Subtract\-Vorgang auf `true` festgelegt, für den Multiply\-Vorgang und den Divide\-Vorgang jedoch auf `false`.Der Add\-Vorgang und der Subtract\-Vorgang schließen die Aktionen automatisch ab, der Divide\-Vorgang schließt seine Aktionen durch einen expliziten Aufruf der `SetTransactionComplete`\-Methode ab, und der Multiply\-Vorgang schließt die Aktionen nicht ab, sondern benötigt einen späteren Aufruf, beispielsweise von Divide, zum Abschließen der Aktionen.  
  
 Die attributierte Dienstimplementierung lautet wie folgt:  
  
```  
[ServiceBehavior(  
    TransactionIsolationLevel = System.Transactions.IsolationLevel.Serializable,  
    TransactionTimeout = "00:00:30",  
    ReleaseServiceInstanceOnTransactionComplete = false,  
    TransactionAutoCompleteOnSessionClose = false)]  
public class CalculatorService : ICalculator  
{  
    double runningTotal;  
  
    public CalculatorService()  
    {  
        Console.WriteLine("Creating new service instance...");  
    }  
  
    [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = true)]  
    public double Add(double n)  
    {  
        RecordToLog(String.Format(CultureInfo.CurrentCulture, "Adding {0} to {1}", n, runningTotal));  
        runningTotal = runningTotal + n;  
        return runningTotal;  
    }  
  
    [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = true)]  
    public double Subtract(double n)  
    {  
        RecordToLog(String.Format(CultureInfo.CurrentCulture, "Subtracting {0} from {1}", n, runningTotal));  
        runningTotal = runningTotal - n;  
        return runningTotal;  
    }  
  
    [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = false)]  
    public double Multiply(double n)  
    {  
        RecordToLog(String.Format(CultureInfo.CurrentCulture, "Multiplying {0} by {1}", runningTotal, n));  
        runningTotal = runningTotal * n;  
        return runningTotal;  
    }  
  
    [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = false)]  
    public double Divide(double n)  
    {  
        RecordToLog(String.Format(CultureInfo.CurrentCulture, "Dividing {0} by {1}", runningTotal, n));  
        runningTotal = runningTotal / n;  
        OperationContext.Current.SetTransactionComplete();  
        return runningTotal;  
    }  
  
    // Logging method ommitted for brevity  
}   
```  
  
 Wenn Sie das Beispiel ausführen, werden die Anforderungen und Antworten für den Vorgang im Clientkonsolenfenster angezeigt.Drücken Sie im Clientfenster die EINGABETASTE, um den Client zu schließen.  
  
```  
Starting transaction  
Performing calculations...  
  Adding 100, running total=100  
  Subtracting 45, running total=55  
  Multiplying by 9, running total=495  
  Dividing by 15, running total=33  
  Completing transaction  
Transaction committed  
Press <ENTER> to terminate client.  
```  
  
 Die Protokollierung der Dienstvorgangsanforderungen wird im Konsolenfenster des Diensts angezeigt.Drücken Sie im Clientfenster die EINGABETASTE, um den Client zu schließen.  
  
```  
Press <ENTER> to terminate service.  
Creating new service instance...  
  Writing row 1 to database: Adding 100 to 0  
  Writing row 2 to database: Subtracting 45 from 100  
  Writing row 3 to database: Multiplying 55 by 9  
  Writing row 4 to database: Dividing 495 by 15  
```  
  
 Zusätzlich zur laufenden Summe der Berechnungen erstellt der Dienst einen Bericht über die Instanzenerstellung \(eine Instanz zu diesem Beispiel\) und protokolliert die Vorgangsanforderungen in einer Datenbank.Da alle Anforderung die Transaktion des Clients übergeben, führt ein Fehler beim Abschließen dieser Transaktion zu einem Rollback aller Datenbankvorgänge.Dies kann auf mehrere Arten veranschaulicht werden:  
  
-   Kommentieren Sie den Aufruf von `tx.Complete`\(\) durch den Client aus, und führen Sie das Beispiel erneut aus. So verlässt der Client den Transaktionsbereich, ohne die Transaktion abzuschließen.  
  
-   Kommentieren Sie den Aufruf des Divide\-Dienstvorgangs aus. Dies führt dazu, dass die vom Multiply\-Vorgang initiierte Aktion nicht abgeschlossen werden kann. Die Transaktion des Clients kann somit auch nicht abgeschlossen werden.  
  
-   Lösen Sie an einer beliebigen Stelle im Transaktionsbereich des Clients eine nicht behandelte Ausnahme aus. Diese führt ebenfalls dazu, dass der Client die Transaktion nicht abschließen kann.  
  
 Alle diese Aktionen führen dazu, dass die in diesem Bereich ausgeführten Vorgänge beendet werden und dass die Anzahl der in der Datenbank beibehaltenen Zeilen nicht inkrementiert wird.  
  
> [!NOTE]
>  Während des Buildprozesses wird die Datenbankdatei in den bin\-Ordner kopiert.Sie müssen diese Kopie der Datenbankdatei betrachten, um die im Protokoll gespeicherten Zeilen zu ermitteln, und nicht die Datei im Visual Studio\-Projekt.  
  
### So richten Sie das Beispiel ein, erstellen es und führen es aus  
  
1.  Stellen Sie sicher, dass SQL Server 2005 Express Edition oder SQL Server 2005 installiert ist.In der Datei App.config des Diensts ist `connectionString` für die Datenbank möglicherweise festgelegt oder die Datenbankinteraktionen sind deaktiviert, indem der `usingSql`\-Wert für appSettings auf `false` festgelegt ist.  
  
2.  Zum Erstellen der C\#\- oder Visual Basic .NET\-Edition der Lösung befolgen Sie die in [Erstellen der Windows Communication Foundation\-Beispiele](../../../../docs/framework/wcf/samples/building-the-samples.md) aufgeführten Anweisungen.  
  
3.  Wenn Sie das Beispiel in einer Konfiguration mit einem Computer oder über Computer hinweg ausführen möchten, befolgen Sie die Anweisungen unter [Durchführen der Windows Communication Foundation\-Beispiele](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
 Wenn Sie das Beispiel computerübergreifend ausführen, müssen Sie Microsoft Distributed Transaction Coordinator \(MSDTC\) konfigurieren, um den Transaktionsfluss über das Netzwerk zu ermöglichen, und mit dem Tool WsatConfig.exe die Netzwerkunterstützung von [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]\-Transaktionen aktivieren.  
  
### So konfigurieren Sie Microsoft Distributed Transaction Coordinator \(MSDTC\) zum Ausführen des Beispiels computerübergreifend  
  
1.  Konfigurieren Sie auf dem Dienstcomputer MSDTC zum Zulassen von eingehenden Netzwerktransaktionen.  
  
    1.  Navigieren Sie im Menü **Start** zu **Systemsteuerung**, **Verwaltung** und **Komponentendienste**.  
  
    2.  Klicken Sie mit der rechten Maustaste auf **Arbeitsplatz**, und wählen Sie **Eigenschaften** aus.  
  
    3.  Klicken Sie auf der Registerkarte **MSDTC** auf **Sicherheitskonfiguration**.  
  
    4.  Aktivieren Sie **DTC\-Netzwerkzugriff** und **Eingehende zulassen**.  
  
    5.  Klicken Sie auf **Ja**, um den MS DTC\-Dienst neu zu starten, und klicken Sie dann auf **OK**.  
  
    6.  Klicken Sie auf **OK**, um das Dialogfeld zu schließen.  
  
2.  Konfigurieren Sie auf dem Dienstcomputer und auf dem Clientcomputer die Windows Firewall so, dass Microsoft Distributed Transaction Coordinator \(MSDTC\) in der Liste der ausgeschlossenen Anwendungen angezeigt wird:  
  
    1.  Führen Sie die Windows\-Firewall\-Anwendung über die Systemsteuerung aus.  
  
    2.  Klicken Sie auf der Registerkarte **Ausnahmen** auf **Programm hinzufügen**.  
  
    3.  Navigieren Sie zum Ordner C:\\WINDOWS\\System32.  
  
    4.  Wählen Sie "Msdtc.exe" aus, und klicken Sie auf **Öffnen**.  
  
    5.  Klicken Sie auf **OK** , um das Dialogfeld **Programm hinzufügen** zu schließen, und klicken Sie erneut auf  **OK**, um das Windows\-Firewall\-Applet zu schließen.  
  
3.  Konfigurieren Sie auf dem Clientcomputer MSDTC zum Zulassen von ausgehenden Netzwerktransaktionen:  
  
    1.  Navigieren Sie im Menü **Start** zu **Systemsteuerung**, **Verwaltung** und **Komponentendienste**.  
  
    2.  Klicken Sie mit der rechten Maustaste auf **Arbeitsplatz**, und wählen Sie **Eigenschaften** aus.  
  
    3.  Klicken Sie auf der Registerkarte **MSDTC** auf **Sicherheitskonfiguration**.  
  
    4.  Aktivieren Sie **DTC\-Netzwerkzugriff** und **Ausgehende zulassen**.  
  
    5.  Klicken Sie auf **Ja**, um den MS DTC\-Dienst neu zu starten, und klicken Sie dann auf **OK**.  
  
    6.  Klicken Sie auf **OK**, um das Dialogfeld zu schließen.  
  
> [!IMPORTANT]
>  Die Beispiele sind möglicherweise bereits auf dem Computer installiert.Suchen Sie nach dem folgenden Verzeichnis \(Standardverzeichnis\), bevor Sie fortfahren.  
>   
>  `<Installationslaufwerk>:\WF_WCF_Samples`  
>   
>  Wenn dieses Verzeichnis nicht vorhanden ist, rufen Sie [Windows Communication Foundation \(WCF\) and Windows Workflow Foundation \(WF\) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) auf, um alle [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]\- und [!INCLUDE[wf1](../../../../includes/wf1-md.md)]\-Beispiele herunterzuladen.Dieses Beispiel befindet sich im folgenden Verzeichnis.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Behaviors\Transactions`  
  
## Siehe auch