---
title: "Sicherheitsfunktionen mit benutzerdefinierten Bindungen | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a2425679-484a-4e6c-9c98-7da7304f1516
caps.latest.revision: 11
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 11
---
# Sicherheitsfunktionen mit benutzerdefinierten Bindungen
Sie können die meisten der allgemeinen Sicherheitsaufgaben mithilfe einer vom System bereitgestellten Bindung ausführen.Wenn Sie die Sicherheit jedoch detaillierter steuern müssen, können Sie mit <xref:System.ServiceModel.Channels.SecurityBindingElement> eine benutzerdefinierte Bindung erstellen, wie in diesen Themen erläutert.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] zu benutzerdefinierten Bindungen finden Sie unter [Benutzerdefinierte Bindungen](../../../../docs/framework/wcf/extending/custom-bindings.md).  
  
## In diesem Abschnitt  
 [SecurityBindingElement\-Authentifizierungsmodi](../../../../docs/framework/wcf/feature-details/securitybindingelement-authentication-modes.md)  
 Beschreibt die Authentifizierungsmodi, die mit einer benutzerdefinierten Bindung möglich sind.  
  
 [Vorgehensweise: Erstellen einer benutzerdefinierten Bindung mit dem SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)  
 Beschreibt die grundlegenden Schritte zum Erstellen einer benutzerdefinierten Bindung mit einem Sicherheitselement.  
  
 [Vorgehensweise: Erstellen eines SecurityBindingElement für einen angegebenen Authentifizierungsmodus](../../../../docs/framework/wcf/feature-details/how-to-create-a-securitybindingelement-for-a-specified-authentication-mode.md)  
 Beschreibt das Erstellen eines Sicherheitselements für einen angegebenen Authentifizierungsmodus.  
  
 [Vorgehensweise: Deaktivieren sicherer Sitzungen auf einer WSFederationHttpBinding](../../../../docs/framework/wcf/feature-details/how-to-disable-secure-sessions-on-a-wsfederationhttpbinding.md)  
 Beschreibt das Deaktivieren von Sicherheitssitzungen beim Erstellen eines Verbunddienstes.  
  
 [Vorgehensweise: Aktivieren der Nachrichtenreplay\-Erkennung](../../../../docs/framework/wcf/feature-details/how-to-enable-message-replay-detection.md)  
 Beschreibt, wie ein Replay\-Angriff entdeckt werden kann.  
  
 [Vorgehensweise: Erstellen unterstützender Anmeldeinformationen](../../../../docs/framework/wcf/feature-details/how-to-create-a-supporting-credential.md)  
 Beschreibt das Bereitstellen unterstützender Anmeldeinformationen für einen Dienst, wenn sie vom Dienst benötigt werden.  
  
 [Vorgehensweise: Einrichten einer Signaturbestätigung](../../../../docs/framework/wcf/feature-details/how-to-set-up-a-signature-confirmation.md)  
 Beschreibt die Schritte zum Bestätigen von Signaturen beim digitalen Signieren von Nachrichten.  
  
 [Vorgehensweise: Festlegen der maximalen Zeitdehnung \(Uhrabweichung\)](../../../../docs/framework/wcf/feature-details/how-to-set-a-max-clock-skew.md)  
 Beschreibt das Festlegen des maximal zulässigen Zeitunterschieds zwischen einem Dienst und einem Client.  
  
 [Vorgehensweise: Deaktivieren der Verschlüsselung digitaler Signaturen](../../../../docs/framework/wcf/feature-details/how-to-disable-encryption-of-digital-signatures.md)  
 Beschreibt, inwiefern das Deaktivieren der Verschlüsselung von digitalen Signaturen die Leistung verbessern kann.  
  
## Referenz  
 <xref:System.ServiceModel.Channels.SecurityBindingElement>  
  
 [\<Sicherheit\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)  
  
## Verwandte Abschnitte  
 [Grundlagen der Schutzebene](../../../../docs/framework/wcf/understanding-protection-level.md)  
  
 [Sichern von Diensten und Clients](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)  
  
## Siehe auch  
 [Bindungen und Sicherheit](../../../../docs/framework/wcf/feature-details/bindings-and-security.md)   
 [Übersicht über die Sicherheit](../../../../docs/framework/wcf/feature-details/security-overview.md)   
 [Vom System bereitgestellte Bindungen](../../../../docs/framework/wcf/system-provided-bindings.md)