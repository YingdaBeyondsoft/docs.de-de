---
title: "Erweitern von ServiceHost und der Dienstmodellebene | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Erweitern von Dienstmodellen [WCF]"
ms.assetid: 954c138a-1cd0-45a0-8abe-e4d2b8ff5400
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Erweitern von ServiceHost und der Dienstmodellebene
Die Dienstmodellebene ist dafür verantwortlich, eingehende Nachrichten aus den zugrunde liegenden Kanälen abzufangen, sie in Methodenaufrufe im Anwendungscode zu übersetzen und die Ergebnisse zurück an den Aufrufer zu senden.Dienstmodellerweiterungen ändern bzw. implementieren Ausführungs\- oder Kommunikationsverhalten und Features wie Verteileroptionen, benutzerefinierte Verhalten, Nachrichten\- oder Parameterinterceptoren und andere Erweiterbarkeitsfunktionen.  
  
## In diesem Abschnitt  
 [Erweitern von Clients](../../../../docs/framework/wcf/extending/extending-clients.md)  
 Beschreibt die Schnittstellen, die die Client\-Runtime abfangen und bearbeiten können, sowie die Klassen, in die Sie Ihre benutzerdefinierten Erweiterungen in Clientanwendungen einfügen können.Sie können beispielsweise eine benutzerdefinierte Clientnachrichtenprotokollierung, benutzerdefinierte Nachrichtenserialisierung usw. durchführen.  
  
 [Erweitern von Verteilern](../../../../docs/framework/wcf/extending/extending-dispatchers.md)  
 Beschreibt die Schnittstellen, die die Dienst\-Runtime abfangen und bearbeiten können, sowie die Klassen, in die Sie Ihre benutzerdefinierten Erweiterungen in Dienstanwendungen einfügen können.Sie können beispielsweise eine benutzerdefinierte Dienstprotokollierung, eine Nachrichtenvalidierung aufseiten des Dienstes, einen benutzerdefinierten Versand usw. durchführen.  
  
 [Erweiterbare Objekte](../../../../docs/framework/wcf/extending/extensible-objects.md)  
 Beschreibt die fünf erweiterbaren Objekte und das <xref:System.ServiceModel.IExtensibleObject%601>\-Muster.Das erweiterbare Objektmuster wird verwendet, um entweder vorhandene Laufzeitklassen um neue Funktionen zu erweitern oder um einem Objekt neue Zustandsfunktionen hinzuzufügen.Erweiterungen, die einem der erweiterbaren Objekte zugeordnet sind, ermöglichen es Verhalten in verschiedenen Phasen der Verarbeitung, auf gemeinsam verwendete Zustände und Funktionen zuzugreifen, die an ein zugängliches und allgemeines erweiterbares Objekt angefügt sind.  
  
 [Konfigurieren und Erweitern der Laufzeit mit Verhalten](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)  
 Um Einstellungen für die [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Laufzeit zu ändern bzw. um Erweiterungen einzufügen, verwenden Sie Verhalten.WCF umfasst vom System implementierte Verhalten zum Steuern von Einschränkungen, Instanzen und anderen Dienst\- und Vorgangsaspekten.Dieser Abschnitt beschreibt, wie Sie Ihre eigenen benutzerdefinierten Verhalten erstellen und sie programmatisch bzw. mit Konfigurationsdateien verfügbar machen können.  
  
 [Erweitern des Hosting mit ServiceHostFactory](../../../../docs/framework/wcf/extending/extending-hosting-using-servicehostfactory.md)  
 Beschreibt, wie Sie <xref:System.ServiceModel.ServiceHostBase?displayProperty=fullName>, <xref:System.ServiceModel.ServiceHost?displayProperty=fullName> erweitern und die <xref:System.ServiceModel.Activation.ServiceHostFactory?displayProperty=fullName>\-Klassen verwenden können, um die Hostumgebung anzupassen.  
  
## Referenz  
  
## Verwandte Abschnitte