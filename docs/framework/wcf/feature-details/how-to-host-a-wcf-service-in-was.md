---
title: "Gewusst wie: Hosten eines WCF-Diensts in WAS | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9e3e213e-2dce-4f98-81a3-f62f44caeb54
caps.latest.revision: 25
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 25
---
# Gewusst wie: Hosten eines WCF-Diensts in WAS
In diesem Thema werden die grundlegenden Schritte vorgestellt, die für die Erstellung eines in WAS (Windows Process Activation Services) gehosteten [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]-Diensts erforderlich sind. WAS ist der neue Prozessaktivierungsdienst, der eine Generalisierung der Funktionen der Internetinformationsdienste (IIS) darstellt, die mit Nicht-HTTP-Transportprotokollen arbeiten. [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] verwendet die Schnittstelle des Listeneradapters, um Aktivierungsanforderungen weiterzugeben, die über die von [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] unterstützten Nicht-HTTP-Protokolle, wie etwa TCP, Named Pipes und Message Queuing, empfangen wurden.  
  
 Diese Hostingoption erfordert, dass die WAS-Aktivierungskomponenten korrekt installiert und konfiguriert wurden. Es muss jedoch keinerlei Hostcode für die Anwendung geschrieben werden. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]Installieren und Konfigurieren von WAS finden Sie unter [Gewusst wie: Installieren und Konfigurieren von WCF-Aktivierungskomponenten](../../../../docs/framework/wcf/feature-details/how-to-install-and-configure-wcf-activation-components.md).  
  
> [!WARNING]
>  Die WAS-Aktivierung wird nicht unterstützt, wenn die Anforderungsverarbeitungspipeline des Webservers auf den klassischen Modus festgelegt ist. Die Anforderungsverarbeitungspipeline des Webservers muss auf den integrierten Modus festgelegt sein, wenn die WAS-Aktivierung verwendet werden soll.  
  
 Wenn ein [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]-Dienst in WAS gehostet wird, werden die Standardbindungen auf die übliche Weise verwendet. Allerdings bei Verwendung der <xref:System.ServiceModel.NetTcpBinding> und <xref:System.ServiceModel.NetNamedPipeBinding> um einen WAS-gehosteten Dienst zu konfigurieren, die eine Bedingung erfüllt sein muss. Wenn verschiedene Endpunkte denselben Transport verwenden, müssen die Bindungseinstellungen für die folgenden sieben Eigenschaften übereinstimmen:  
  
-   ConnectionBufferSize  
  
-   ChannelInitializationTimeout  
  
-   MaxPendingConnections  
  
-   MaxOutputDelay  
  
-   MaxPendingAccepts  
  
-   ConnectionPoolSettings.IdleTimeout  
  
-   ConnectionPoolSettings.MaxOutboundConnectionsPerEndpoint  
  
 Andernfalls bestimmt der Endpunkt initialisiert wird zunächst immer die Werte dieser Eigenschaften und später hinzugefügte Endpunkte lösen eine <xref:System.ServiceModel.ServiceActivationException> Wenn sie diese Einstellungen nicht übereinstimmen.  
  
 Die Quellkopie dieses Beispiels, finden Sie unter [TCP-Aktivierung](../../../../docs/framework/wcf/samples/tcp-activation.md).  
  
### <a name="to-create-a-basic-service-hosted-by-was"></a>So erstellen Sie einen grundlegenden durch WAS gehosteten Dienst  
  
1.  Definieren Sie einen Dienstvertrag für den Diensttyp.  
  
     [!code-csharp[C_HowTo_HostInWAS#1121](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinwas/cs/service.cs#1121)]  
  
2.  Implementieren Sie den Dienstvertrag in einer Dienstklasse. Beachten Sie, dass die Adresse oder die Bindungsinformationen in der Implementierung des Diensts nicht angegeben werden. Es muss auch kein Code geschrieben werden, um Informationen aus der Konfigurationsdatei abzurufen.  
  
     [!code-csharp[C_HowTo_HostInWAS#1122](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinwas/cs/service.cs#1122)]  
  
3.  Erstellen Sie eine Web.config-Datei definieren die <xref:System.ServiceModel.NetTcpBinding> Bindung durch die `CalculatorService` Endpunkte.  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <system.serviceModel>  
        <bindings>  
          <netTcpBinding>  
            <binding portSharingEnabled="true">  
              <security mode="None" />  
            </binding>  
          </netTcpBinding>  
        </bindings>  
      </system.serviceModel>  
    </configuration>  
    ```  
  
4.  Erstellen Sie eine Service.svc-Datei, die den folgenden Code enthält.  
  
    ```  
    <%@ServiceHost language=c# Service="CalculatorService" %>   
    ```  
  
5.  Stellen Sie die Service.svc-Datei in das virtuelle IIS-Verzeichnis.  
  
### <a name="to-create-a-client-to-use-the-service"></a>So erstellen Sie einen Client, der den Dienst verwendet  
  
1.  Verwendung [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) über die Befehlszeile zum Generieren von Code aus Dienstmetadaten.  
  
    ```  
    Svcutil.exe <service's Metadata Exchange (MEX) address or HTTP GET address>   
    ```  
  
2.  Der generierte Client enthält die `ICalculator`-Schnittstelle, die den Dienstvertrag definiert, dem die Clientimplementierung entsprechen muss.  
  
     [!code-csharp[C_HowTo_HostInWAS#1221](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinwas/cs/client.cs#1221)]  
  
3.  Die generierte Clientanwendung enthält außerdem die Implementierung von `ClientCalculator`. Beachten Sie, dass die Adresse und die Bindungsinformationen in der Implementierung des Diensts nirgendwo angegeben werden. Es muss auch kein Code geschrieben werden, um Informationen aus der Konfigurationsdatei abzurufen.  
  
     [!code-csharp[C_HowTo_HostInWAS#1222](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinwas/cs/client.cs#1222)]  
  
4.  Die Konfiguration für den Client, verwendet die <xref:System.ServiceModel.NetTcpBinding> wird auch von Svcutil.exe generiert. Wenn Sie Visual&#160;Studio verwenden, sollte diese Datei in der Datei App.config genannt werden.  
  
     <!-- TODO: review snippet reference [!code[C_HowTo_HostInWAS#2211](../../../../samples/snippets/common/VS_Snippets_CFX/c_howto_hostinwas/common/app.config#2211)]  -->  
  
5.  Erstellen Sie eine Instanz von `ClientCalculator` in einer Anwendung, und rufen Sie dann die Dienstvorgänge auf.  
  
     [!code-csharp[C_HowTo_HostInWAS#1223](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinwas/cs/client.cs#1223)]  
  
6.  Kompilieren Sie den Code, und führen Sie den Client aus.  
  
## <a name="see-also"></a>Siehe auch  
 [TCP-Aktivierung](../../../../docs/framework/wcf/samples/tcp-activation.md)   
 [Windows Server AppFabric-Hostingfunktionen](http://go.microsoft.com/fwlink/?LinkId=201276)