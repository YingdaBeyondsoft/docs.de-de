---
title: "Entwurfsmuster: Listenbasiertes Ver&#246;ffentlichen-Abonnieren | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f4257abc-12df-4736-a03b-0731becf0fd4
caps.latest.revision: 16
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 16
---
# Entwurfsmuster: Listenbasiertes Ver&#246;ffentlichen-Abonnieren
In diesem Beispiel wird das als [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]\-Programm implementierte listenbasierte Veröffentlichen\-Abonnieren\-Muster veranschaulicht.  
  
> [!NOTE]
>  Die Setupprozedur und die Buildanweisungen für dieses Beispiel befinden sich am Ende dieses Themas.  
  
 Das listenbasierte Veröffentlichen\-Abonnieren\-Entwurfsmuster wird in der Publikation "Microsoft Patterns & Practices" unter [Integrationsmuster](http://go.microsoft.com/fwlink/?LinkId=95894) beschrieben.  Das Veröffentlichen\-Abonnieren\-Muster übergibt Informationen an eine Auflistung von Empfängern, die ein Informationsthema abonniert haben.  Listenbasiertes Veröffentlichen\-Abonnieren verwaltet eine Liste von Abonnenten.  Wenn für die Veröffentlichung bestimmte Informationen vorhanden sind, wird jedem Abonnenten auf der Liste ein Exemplar geschickt.  Dieses Beispiel veranschaulicht ein dynamisches listenbasiertes Veröffentlichen\-Abonnieren\-Muster, das von Kunden nach Bedarf abonniert und abbestellt werden kann.  
  
 Das Beispiel für listenbasiertes Veröffentlichen\-Abonnieren besteht aus einem Client, einem Dienst und einem Datenquellenprogramm.  Es können mehrere Clients und mehrere Datenquellenprogramme ausgeführt werden.  Clients abonnieren den Dienst, empfangen Benachrichtigungen und bestellen den Dienst ab.  Datenquellprogramme senden Informationen an den Dienst, die für alle aktuellen Abonnenten veröffentlicht werden sollte.  
  
 In diesem Beispiel sind der Client und die Datenquelle Konsolenprogramme \(.exe\-Dateien\), und der Dienst ist eine Bibliothek \(.dll\), die in Internet Information Services \(IIS\) gehostet wird.  Client\- und Datenquellenaktivität sind auf dem Desktop sichtbar.  
  
 Der Dienst verwendet Duplexkommunikation.  Der `ISampleContract`\-Dienstvertrag wird mit einem `ISampleClientCallback`\-Rückrufvertrag zusammengefasst.  Der Dienst implementiert Subscribe\- und Unsubscribe\-Dienstvorgänge, die von Clients verwendet werden, um der Liste der Abonnenten beizutreten oder diese zu verlassen.  Der Dienst implementiert außerdem den `PublishPriceChange`\-Dienstvorgang, der vom Datenquellenprogramm aufgerufen wird, um dem Dienst neue Informationen bereitzustellen.  Das Clientprogramm implementiert den `PriceChange`\-Dienstvorgang, der vom Dienst aufgerufen wird, um alle Abonnenten über Preisänderungen zu informieren.  
  
```  
// Create a service contract and define the service operations.  
// NOTE: The service operations must be declared explicitly.  
[ServiceContract(SessionMode=SessionMode.Required,  
      CallbackContract=typeof(ISampleClientContract))]  
public interface ISampleContract  
{  
    [OperationContract(IsOneWay = false, IsInitiating=true)]  
    void Subscribe();  
    [OperationContract(IsOneWay = false, IsTerminating=true)]  
    void Unsubscribe();  
    [OperationContract(IsOneWay = true)]  
    void PublishPriceChange(string item, double price,   
                                     double change);  
}  
  
public interface ISampleClientContract  
{  
    [OperationContract(IsOneWay = true)]  
    void PriceChange(string item, double price, double change);  
}  
```  
  
 Der Dienst verwendet ein .NET Framework\-Ereignis als Mechanismus, um alle Abonnenten über neue Informationen zu informieren.  Wenn ein Client dem Dienst beitritt, indem er Subscribe aufruft, wird ein Ereignishandler bereitgestellt.  Wenn ein Client den Dienst verlässt, wird sein Ereignishandler von dem Ereignis entfernt.  Wenn eine Datenquelle den Dienst aufruft, um eine Preisänderung mitzuteilen, löst der Dienst das Ereignis aus.  Daraufhin wird jede Instanz des Diensts aufgerufen, eine für jeden Client mit einem Abonnement, und die Ereignishandler werden ausgeführt.  Jeder Ereignishandler übermittelt die Informationen über seine Rückruffunktion an seinen Client.  
  
```  
public class PriceChangeEventArgs : EventArgs  
    {  
        public string Item;  
        public double Price;  
        public double Change;  
    }  
  
    // The Service implementation implements your service contract.  
    [ServiceBehavior(InstanceContextMode=InstanceContextMode.PerSession)]  
    public class SampleService : ISampleContract  
    {  
        public static event PriceChangeEventHandler PriceChangeEvent;  
        public delegate void PriceChangeEventHandler(object sender, PriceChangeEventArgs e);  
  
        ISampleClientContract callback = null;  
  
        PriceChangeEventHandler priceChangeHandler = null;  
  
        //Clients call this service operation to subscribe.  
        //A price change event handler is registered for this client instance.  
  
        public void Subscribe()  
        {  
            callback = OperationContext.Current.GetCallbackChannel<ISampleClientContract>();  
            priceChangeHandler = new PriceChangeEventHandler(PriceChangeHandler);  
            PriceChangeEvent += priceChangeHandler;  
        }  
  
        //Clients call this service operation to unsubscribe.  
        //The previous price change event handler is deregistered.  
  
        public void Unsubscribe()  
        {  
            PriceChangeEvent -= priceChangeHandler;  
        }  
  
        //Information source clients call this service operation to report a price change.  
        //A price change event is raised. The price change event handlers for each subscriber will execute.  
  
        public void PublishPriceChange(string item, double price, double change)  
        {  
            PriceChangeEventArgs e = new PriceChangeEventArgs();  
            e.Item = item;  
            e.Price = price;  
            e.Change = change;  
            PriceChangeEvent(this, e);  
        }  
  
        //This event handler runs when a PriceChange event is raised.  
        //The client's PriceChange service operation is invoked to provide notification about the price change.  
  
        public void PriceChangeHandler(object sender, PriceChangeEventArgs e)  
        {  
            callback.PriceChange(e.Item, e.Price, e.Change);  
        }  
  
    }  
  
```  
  
 Wenn Sie das Beispiel ausführen, starten Sie mehrere Clients.  Die Clients abonnieren den Dienst.  Führen Sie anschließend das Datenquellenprogramm aus, das Informationen an den Dienst sendet.  Der Dienst übergibt die Informationen an alle Abonnenten.  Sie können Aktivität auf jeder Clientkonsole sehen, sodass bestätigt wird, dass die Informationen empfangen wurden.  Drücken Sie im Clientfenster die EINGABETASTE, um den Client zu schließen.  
  
### So richten Sie das Beispiel ein und erstellen es  
  
1.  Stellen Sie sicher, dass Sie die [Einmaliges Setupverfahren für Windows Communication Foundation\-Beispiele](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md) ausgeführt haben.  
  
2.  Zum Erstellen der C\#\- oder Visual Basic .NET\-Edition der Projektmappe befolgen Sie die unter [Erstellen der Windows Communication Foundation\-Beispiele](../../../../docs/framework/wcf/samples/building-the-samples.md) aufgeführten Anweisungen.  
  
### So führen Sie das Beispiel auf demselben Computer aus  
  
1.  Prüfen Sie, ob Sie mit einem Browser auf den Dienst zugreifen können, indem Sie die folgende Adresse eingeben: http:\/\/localhost\/servicemodelsamples\/service.svc.  Als Antwort sollte eine Bestätigungsseite angezeigt werden.  
  
2.  Führen Sie die Datei "Client.exe" vom Ordner "\\client\\bin\\" unter dem sprachspezifischen Ordner aus.  Im Clientkonsolenfenster wird die Clientaktivität angezeigt.  Starten Sie mehrere Clients.  
  
3.  Führen Sie "Datasource.exe" von "\\datasource\\bin\\" im sprachspezifischen Ordner aus.  Die Datenquellenaktivität wird im Konsolenfenster angezeigt.  Sobald die Datenquelle Informationen an den Dienst sendet, sollten diese an jeden Client übergeben werden.  
  
4.  Wenn der Client, die Datenquelle und die Dienstprogramme nicht miteinander kommunizieren können, erhalten Sie weitere Informationen unter [Troubleshooting Tips](http://msdn.microsoft.com/de-de/8787c877-5e96-42da-8214-fa737a38f10b).  
  
### So führen Sie das Beispiel computerübergreifend aus  
  
1.  Einrichten des Dienstrechners:  
  
    1.  Erstellen Sie auf dem Dienstcomputer ein virtuelles Verzeichnis namens "ServiceModelSamples".  Zum Erstellen des Festplattenverzeichnisses und des virtuellen Verzeichnisses kann die Batchdatei "Setupvroot.bat" in [Einmaliges Setupverfahren für Windows Communication Foundation\-Beispiele](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md) verwendet werden.  
  
    2.  Kopieren Sie die Dienstprogrammdateien aus %SystemDrive%\\Inetpub\\wwwroot\\servicemodelsamples in das virtuelle Verzeichnis "ServiceModelSamples" auf dem Dienstcomputer.  Stellen Sie sicher, dass Sie die Dateien in das Verzeichnis \\bin einfügen.  
  
    3.  Testen Sie, ob Sie mit einem Browser vom Clientcomputer auf den Dienst zugreifen können.  
  
2.  Einrichten der Clientcomputer:  
  
    1.  Kopieren Sie die Clientprogrammdateien aus dem Ordner "\\client\\bin\\" \(unterhalb des sprachspezifischen Ordners\) auf die Clientcomputer.  
  
    2.  Ändern Sie in jeder Clientkonfigurationsdatei den Wert für die Adresse der Endpunktdefinition so, dass er mit der neuen Adresse Ihres Diensts übereinstimmt.  Ersetzen Sie alle Verweise auf localhost in der Adresse durch einen vollqualifizierten Domänennamen.  
  
3.  Einrichten des Datenquellencomputers:  
  
    1.  Kopieren Sie die Datenquellen\-Programmdateien aus dem Ordner "\\datasource\\bin\\" \(unterhalb des sprachspezifischen Ordners\) auf den Datenquellencomputer.  
  
    2.  Ändern Sie in der Datenquellen\-Konfigurationsdatei den Wert für die Adresse der Endpunktdefinition so, dass er mit der neuen Adresse Ihres Diensts übereinstimmt.  Ersetzen Sie alle Verweise auf localhost in der Adresse durch einen vollqualifizierten Domänennamen.  
  
4.  Starten Sie auf den Clientcomputern in einer Eingabeaufforderung die Datei "Client.exe".  
  
5.  Starten Sie auf dem Datenquellencomputer in einer Eingabeaufforderung die Datei "Datasource.exe".  
  
> [!IMPORTANT]
>  Die Beispiele sind möglicherweise bereits auf dem Computer installiert.  Suchen Sie nach dem folgenden Verzeichnis \(Standardverzeichnis\), bevor Sie fortfahren.  
>   
>  `<Installationslaufwerk>:\WF_WCF_Samples`  
>   
>  Wenn dieses Verzeichnis nicht vorhanden ist, rufen Sie [Windows Communication Foundation \(WCF\) and Windows Workflow Foundation \(WF\) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) auf, um alle [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]\- und [!INCLUDE[wf1](../../../../includes/wf1-md.md)]\-Beispiele herunterzuladen.  Dieses Beispiel befindet sich im folgenden Verzeichnis.  
>   
>  `<Installationslaufwerk>:\WF_WCF_Samples\WCF\Scenario\DesignPatterns/ListBasedPublishSubscribe`  
  
## Siehe auch