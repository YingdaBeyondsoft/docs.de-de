---
title: "Konfigurationskanalfactory | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3b749493-bd8a-4ccb-893e-5948901a1486
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Konfigurationskanalfactory
In diesem Beispiel wird die Verwendung von <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601> behandelt.<xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601> ermöglicht die zentrale Verwaltung der [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Clientkonfiguration.Dies kann auch in Szenarien nützlich sein, in denen die Konfiguration nach der Ladezeit der Anwendungsdomäne ausgewählt oder geändert wird.  
  
## Veranschaulicht  
 <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601>  
  
## Diskussion  
 In diesem Beispiel wird gezeigt, wie eine bestimmte Konfigurationsdatei mit <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601> zu einer Clientanwendung hinzugefügt wird, ohne die standardmäßige Anwendungskonfigurationsdatei verwenden zu müssen.  
  
 Das Beispiel umfasst zwei Projekte.Das erste Projekt ist ein einfacher Dienst, der auf Nachrichten von den Clients antwortet.Das zweite Projekt ist eine Clientanwendung, die für die Konfigurationsdatei Test.config mithilfe einer <xref:System.Configuration.ExeConfigurationFileMap> zwei <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601>\-Objekte erstellt und diese für die Kommunikation mit dem Dienst verwendet.Beide Clients verwenden die in Test.config angegebene Konfiguration für die Kommunikation mit dem Dienst.  
  
 Der folgende Code fügt einer Clientanwendung eine benutzerdefinierte Konfigurationsdatei hinzu.  
  
```  
ExeConfigurationFileMap fileMap = new ExeConfigurationFileMap();  
fileMap.ExeConfigFilename = "Test.config";  
Configuration newConfiguration = ConfigurationManager.OpenMappedExeConfiguration(fileMap, ConfigurationUserLevel.None);  
  
ConfigurationChannelFactory<ICalculatorChannel> factory1 = new ConfigurationChannelFactory<ICalculatorChannel>("endpoint1", newConfiguration, new EndpointAddress("http://localhost:8000/servicemodelsamples/service"));  
ICalculatorChannel client1 = factory1.CreateChannel();  
  
```  
  
#### So richten Sie das Beispiel ein, erstellen es und führen es aus  
  
1.  Öffnen Sie [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] mit Administratorrechten.  
  
2.  Klicken Sie mit der rechten Maustaste auf die Projektmappe ConfigurationChannelFactory \(2 Projekte\), und wählen Sie dann **Eigenschaften** aus.  
  
3.  Wählen Sie unter **Allgemeine Eigenschaften** die Option **Startprojekt** aus, und klicken Sie dann auf **Mehrere Startprojekte**.  
  
4.  Verschieben Sie das Projekt **Dienst** mit der **Aktion "Start"** an den Anfang der Liste, und verschieben Sie dann ebenfalls mit der **Aktion "Start"** das Projekt **Client** an die Stelle nach dem Projekt **Dienst**, damit das Projekt **Client** nach dem Projekt **Dienst** ausgeführt wird.  
  
5.  Klicken Sie auf **OK**, und drücken Sie dann F5 \(oder STRG\+F5\), um das Beispiel auszuführen.  
  
> [!IMPORTANT]
>  Die Beispiele sind möglicherweise bereits auf dem Computer installiert.Suchen Sie nach dem folgenden Verzeichnis \(Standardverzeichnis\), bevor Sie fortfahren.  
>   
>  `<Installationslaufwerk>:\WF_WCF_Samples`  
>   
>  Wenn dieses Verzeichnis nicht vorhanden ist, rufen Sie [Windows Communication Foundation \(WCF\) and Windows Workflow Foundation \(WF\) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) auf, um alle [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]\- und [!INCLUDE[wf1](../../../../includes/wf1-md.md)]\-Beispiele herunterzuladen.Dieses Beispiel befindet sich im folgenden Verzeichnis.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\ConfigurationChannelFactory`