---
title: "Verwenden von Vertr&#228;gen im Workflow | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 939c64e9-e7cc-4abc-b41e-27cfce1d7e50
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Verwenden von Vertr&#228;gen im Workflow
Beim Implementieren eines Diensts definieren Sie eine Reihe von Verträgen, in denen der Dienst und die von ihm gesendeten und empfangenen Daten beschrieben werden.Die Daten werden als Datenverträge und Nachrichtenverträge dargestellt. Sowohl [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\- als auch Workflowdienste verwenden Datenvertrags\- und Nachrichtenvertragsdefinitionen als Teil ihrer Dienstbeschreibungen.Der Dienst selbst macht Metadaten \(im WSDL\-Format\) verfügbar, um die Vorgänge des Diensts zu beschreiben.In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] definieren Dienst\- und Vorgangsverträge den Dienst und seine unterstützten Vorgänge.In einem Workflowdienst sind diese Verträge jedoch Teil des eigentlichen Geschäftsprozesses. Sie werden in den Metadaten von einem Prozess verfügbar gemacht, der als Vertragsrückschluss bezeichnet wird.  
  
## Vertragsrückschluss  
 Wenn ein Workflowdienst mit <xref:System.ServiceModel.Activities.WorkflowServiceHost> gehostet wird, wird die Workflowdefinition untersucht, und basierend auf den im Workflow gefundenen Messagingaktivitäten wird ein Vertrag generiert.Zum Generieren des Vertrags werden insbesondere die folgenden Aktivitäten und Eigenschaften verwendet:  
  
 <xref:System.ServiceModel.Activities.Receive>\-Aktivität  
  
-   <xref:System.ServiceModel.Activities.Receive.ServiceContractName%2A>  
  
-   <xref:System.ServiceModel.Activities.Receive.OperationContractName%2A>  
  
-   <xref:System.ServiceModel.Activities.Receive.Action%2A>  
  
-   <xref:System.ServiceModel.Activities.Receive.ValueType%2A>  
  
 <xref:System.ServiceModel.Activities.SendReply>\-Aktivität  
  
-   <xref:System.ServiceModel.Activities.SendReply.Action%2A>  
  
-   <xref:System.ServiceModel.Activities.SendReply.ValueType%2A>  
  
 <xref:System.ServiceModel.Activities.TransactedReceiveScope>\-Aktivität  
  
 Das Endergebnis des Vertragsrückschlusses ist eine Beschreibung des Diensts, bei der die gleichen Datenstrukturen wie für WCF\-Dienstverträge und \-Vorgangsverträge verwendet werden.Diese Informationen werden dann verwendet, um WSDL für den Workflowdienst verfügbar zu machen.  
  
## Siehe auch  
 [Workflowdienste](../../../../docs/framework/wcf/feature-details/workflow-services.md)   
 [Messagingaktivitäten](../../../../docs/framework/wcf/feature-details/messaging-activities.md)   
 [Vorgehensweise: Erstellen eines Workflowdiensts mit Messagingaktivitäten](../../../../docs/framework/wcf/feature-details/how-to-create-a-workflow-service-with-messaging-activities.md)   
 [Vorgehensweise: Erstellen eines Workflowdiensts zum Verarbeiten eines vorhandenen Dienstvertrags](../../../../docs/framework/windows-workflow-foundation//how-to-create-a-workflow-service-that-consumes-an-existing-service-contract.md)