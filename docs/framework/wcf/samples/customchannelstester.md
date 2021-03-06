---
title: "CustomChannelsTester | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ee1fa307-98b1-4647-8860-2e9217ba6082
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# CustomChannelsTester
Der `CustomChannelsTester` ist ein Tool, das Sie zum Testen Ihrer benutzerdefinierten Channelimplementierungen mit einem Satz vordefinierter Dienstverträge verwenden können.  Sie können einen Satz von Dienstverträgen auswählen und diesen mithilfe einer XML\-Datei an das Tool übergeben.  Anschließend generiert das Tool den Dienst und den Client, die die benutzerdefinierten Channelimplementierungen während des Nachrichtenaustauschs ausführen.  
  
### So erstellen Sie das Tool  
  
1.  Befolgen Sie die Anweisungen unter [Erstellen der Windows Communication Foundation\-Beispiele](../../../../docs/framework/wcf/samples/building-the-samples.md), um die Projektmappe zu erstellen.  
  
2.  Während der Erstellung der Projektmappe werden drei Dateien generiert: "CustomChannelsTester.exe", "TestSpec.xml" und "SampleRun.cmd".  Die Datei "SampleRun.cmd" verfügt über eine Beispielbefehlszeile, die veranschaulicht, wie dieses Tool zum Testen des [Transport: UDP](../../../../docs/framework/wcf/samples/transport-udp.md)\-Beispiels verwendet wird.  
  
### So führen Sie das Tool aus  
  
-   Geben Sie an der Eingabeaufforderung folgenden Befehl ein:  
  
    ```  
    CustomChannelsTester.exe /binding:YourCustomBindngName /dll:TheAssemblyWhereThisTypeisDefined /testspec:XmlFileNameWhichContainsTestOptions  
    ```  
  
     Die Verwendung der `/binding`\-Option ist erforderlich.  
  
     `/dll` ist erforderlich, wenn die "Bindung" keine vom System und von [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] bereitgestellte Bindung ist.  
  
     `/testspec` ist optional.  
  
     Auf diese Weise werden Server und Clients auf der Grundlage der Testspezifikationen und der Bindung erstellt.  
  
     Der Client und der Server werden ausgeführt und die Ergebnisse zurückgegeben.  
  
     Folgendes ist der Beispiel\-XML\-Code für die Beschreibung der Testspezifikationen \(testspec.xml\):  
  
    ```  
    <TestSpec xmlns="http://WCF/TestSpec" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" >  
    <ServiceContract>  
    <!-- Test a contract which has oneway / twoway operations. If you set ExpandAll = true, both types of contracts are tested -->    <IsOneWay ExpandAll="true">true</IsOneWay>  
    <!-- Test a contract with Asynchronous / Synchronous Operations-->  
        <IsAsync>false</IsAsync>   
    <!-- Test a sessionful / sessionless contract-->      
        <IsSession ExpandAll="true">true</IsSession>  
    <!-- If the Service Contract includes a CallBack Contract-->      
        <IsCallBack ExpandAll="true">true</IsCallBack>  
    </ServiceContract>  
    <TestDetails>  
    <!-- Name of the machine that runs the server - required if you want to run the test crossmachine-->  
        <ServerName>ReplaceThisWithTheServerMachineName</ServerName>  
    <!-- Port Number - Optional-->  
        <Port>8000</Port>  
    <!--URI for the callBack address for the CLient. The client will receive the messages from the server on this address in case of a CallBack Contract-->  
        <ClientCallBackAddress/>      
    <!-- Duration (in sec) after the server has started, it times out - optional(default = 300sec) -->  
        <ServerTimeout>300</ServerTimeout>  
    <!-- Duration (in sec) before the Client initializes -optional(default = 60sec) -->  
        <ClientTimeout>60</ClientTimeout>  
    <!-- Number of clients for each service - optional(default = 1) -->  
        <NumberOfClients>1</NumberOfClients>  
    <!-- Number of messages each client sends to the service - optional(default = 1) -->  
        <MessagesPerClient>1</MessagesPerClient>  
    </TestDetails>  
    </TestSpec>  
    ```  
  
## Siehe auch