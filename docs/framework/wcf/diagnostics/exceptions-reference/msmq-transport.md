---
title: "MSMQ-Transport. | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3f29a2fe-24df-4614-b64c-b0c084fb7003
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# MSMQ-Transport.
In diesem Thema sind alle vom MSMQ\-Transport erzeugten Ausnahmen aufgeführt.  
  
## Ausnahmeliste  
  
|Ressourcencode|Ressourcenzeichenfolge|  
|--------------------|----------------------------|  
|MsmqActiveDirectoryRequiresNativeTransfer|Die Bindungsvalidierung für die Nachricht ist fehlgeschlagen.Der Client kann keine Nachrichten senden.Ein Konflikt in den Bindungseigenschaften hat diesen Fehler verursacht.Das UseActiveDirectory ist auf TRUE und das QueueTransferProtocol ist auf Native festgesetzt.Um den Konflikt zu lösen, korrigieren Sie eine der Eigenschaften.|  
|MsmqAuthNoneRequiresProtectionNone|Die Bindungsvalidierung für den Dienst ist fehlgeschlagen.Der Dienstendpunkt oder der Client kann nicht gestartet werden.Ein Konflikt in den Bindungseigenschaften hat diesen Fehler verursacht.Der MsmqTransportSecurity.MsmqAuthenticationMode ist auf None festgelegt, und MsmqTransportSecurity.MsmqProtectionLevel ist nicht auf None festgelegt.Um den Konflikt zu lösen, korrigieren Sie eine der Eigenschaften.|  
|MsmqCustomRequiresPerAddDLQ|Die Bindungsvalidierung für die Nachricht ist fehlgeschlagen.Der Client kann die Nachricht nicht senden.Der DeadLetterQueue wird auf Custom festgelegt, aber der CustomDeadLetterQueue wird nicht angegeben.Geben Sie den URI der Warteschlange für unzustellbare Nachrichten für jede Anwendung in der CustomDeadLetterQueue\-Eigenschaft an.|  
|MsmqDeserializationError|Beim Deserialisieren der XML\-Nachricht wurde ein Fehler entdeckt.Die Nachricht kann nicht empfangen werden und wird verworfen.|  
|MsmqDLQNotWriteable|Die Bindungsvalidierung für den Client ist fehlgeschlagen.Der Client kann keine Nachricht senden.Die angegebene Warteschlange für unzustellbare Nachrichten ist nicht vorhanden oder kann nicht geschrieben werden.Stellen Sie sicher, dass für die Warteschlange die richtige Autorisierung vorliegt, um darin zu schreiben.|  
|MsmqGetPrivateComputerInformationError|Die Versionsprüfung ist mit dem angegebenen Fehler fehlgeschlagen.Die Version der MSMQ kann nicht erkannt werden; alle Vorgänge auf dem Kanal, der in der Warteschlange steht, werden fehlschlagen.Stellen Sie sicher, dass MSQM installiert und aktiviert ist.|  
|MsmqNoAssurancesForVolatile|Die Bindungsvalidierung für den Dienst ist fehlgeschlagen.Der Dienstendpunkt oder der Client kann nicht gestartet werden.Die Eigenschaft "ExactlyOnce" wird auf True festgelegt, und die Eigenschaft "Durable" wird auf False festgelegt.Dies wird nicht unterstützt.Um den Konflikt zu lösen, korrigieren Sie eine dieser Eigenschaften.|  
|MsmqNonTransactionalQueueNeeded|Ein Konflikt zwischen der Bindung und der MSMQ\-Warteschlangenkonfiguration wurde erkannt.Der Dienstendpunkt kann nicht gestartet werden.Die Eigenschaft "ExactlyOnce" wird auf False festgelegt, und die Warteschlange zum Lesen von Nachrichten ist eine Transaktionswarteschlange.Korrigieren Sie den Fehler, indem Sie die Eigenschaft "ExactlyOnce" auf True festlegen, oder erstellen Sie eine nicht transaktionale Bindung.|  
|MsmqOpenError|Fehler beim Öffnen der angegebenen Warteschlange.Die Nachricht kann von der Warteschlange nicht gesendet oder empfangen werden.Stellen Sie sicher, dass MSMQ installiert ist und läuft.Stellen Sie auch sicher, dass die Warteschlange verfügbar ist, um mit dem erforderlichen Zugriffsmodus und der Autorisierung geöffnet zu werden.|  
|MsmqPathLookupError|Beim Umwandeln des angegebenen Warteschlangenpfads in den Formatnamen ist ein Fehler aufgetreten.Alle Vorgänge auf dem in der Warteschlange stehenden Kanal sind fehlgeschlagen.Stellen Sie sicher, dass die Warteschlangenadresse gültig ist.MSMQ muss mit aktivierter Active Directory\-Integration installiert und Zugriff darauf verfügbar sein.|  
|MsmqPerAppDLQRequiresCustom|Die Bindungsvalidierung auf dem Client ist fehlgeschlagen.Der Client kann keine Nachrichten senden.Die Eigenschaft "CustomDeadLetterQueue" ist festgelegt, aber die Eigenschaft "DeadLetterQueue" ist nicht auf Custom festgelegt.Legen Sie die Eigenschaft "DeadLetterQueue" auf Custom fest.|  
|MsmqPerAppDLQRequiresExactlyOnce|Die Bindungsvalidierung für den Client ist fehlgeschlagen.Der Client kann keine Nachrichten senden.Ein Konflikt in den Bindungseigenschaften verursacht diesen Fehler.Um die benutzerdefinierte Warteschlange für unzustellbare Nachrichten zu verwenden, muss ExactlyOnce auf True festgelegt werden, um den Konflikt zu lösen.|  
|MsmqPerAppDLQRequiresMsmq4|Es wurde ein Konflikt zwischen der Bindung und der MSMQ\-Konfiguration erkannt.Der Client kann keine Nachrichten senden.Um die benutzerdefinierte Warteschlange für unzustellbare Nachrichten zu verwenden, müssen Sie MSMQ Version 4.0 oder höher besitzen.Wenn Sie MSMQ Version 4.0 oder höher nicht besitzen, legen Sie die DeadLetterQueue\-Eigenschaft auf System oder None fest.|  
|MsmqReceiveError|Beim Erhalt einer Nachricht aus der Warteschlange ist ein Fehler aufgetreten.Stellen Sie sicher, dass MSMQ installiert ist und läuft.Stellen Sie sicher, dass die Warteschlange für den Empfang bereit ist.|  
|MsmqSameTransactionExpected|Für diese Sitzung ist ein Transaktionsfehler aufgetreten.Der Sitzungskanal ist beschädigt.Die Nachrichten in der Sitzung können weder gesendet noch empfangen werden.Eine in der Warteschleife stehende Sitzung kann nur einer Transaktion zugeordnet werden.Stellen Sie sicher, dass alle Nachrichten in der Sitzung im Rahmen einer einzelnen Transaktion gesendet oder empfangen werden.|  
|MsmqSendError|Beim Senden an die angegebene Warteschlange ist ein Fehler aufgetreten.Stellen Sie sicher, dass MSMQ installiert ist und läuft.Wenn Sie an eine lokale Warteschlange senden, sorgen Sie dafür, dass es die Warteschlange gibt und dass sie über den erforderlichen Zugriffsmodus und die erforderliche Autorisierung verfügt.|  
|MsmqTimeSpanTooLarge|Die Nachrichtengültigkeitsdauer ist zu groß.Die Nachricht kann nicht gesendet werden.Die Nachrichtengültigkeitsdauer \(TTL\) kann den Maximalwert für Int32 nicht überschreiten.|  
|MsmqTokenProviderNeededForCertificates|Es kann kein X509SecurityTokenProvider gefunden werden.Die Nachricht kann nicht gesendet werden.Der Zertifikatsauthentifizierungsmodus erfordert einen X.509\-Tokenanbieter.Stellen Sie sicher, dass ein Sicherheitstokenanbieter für das installierte Zertifikat verfügbar ist.|  
|MsmqTransactedDLQExpected|Zwischen der Bindung und der MSMQ\-Konfiguration ist ein Konflikt aufgetreten.Die Nachrichten können nicht gesendet werden.Bei der benutzerdefinierten Warteschlange, die in der Bindung angegeben ist, muss es sich um eine Transaktionswarteschlange handeln.Stellen Sie sicher, dass die Adresse der benutzerdefinierten Warteschlange korrekt ist und dass es sich bei der Warteschlange um eine Transaktionswarteschlange handelt.|  
|MsmqTransactionalQueueNeeded|Zwischen der Bindung und der MSMQ\-Warteschlangenkonfiguration ist ein Fehler aufgetreten.Der Dienstendpunkt kann nicht gestartet werden.Die Eigenschaft ExactlyOnce wird auf True festgelegt, und die Warteschlange zum Lesen von Nachrichten ist keine Transaktionswarteschlange.Legen Sie zum Korrigieren des Fehlers die Eigenschaft ExactlyOnce auf False fest, oder erstellen Sie eine Transaktionswarteschlange für diese Bindung.|  
|MsmqTransactionCurrentRequired|Es steht keine Transaktion bereit, um die Nachrichten in der Sitzung zu senden.Für das Senden einer Nachricht aus einer Sitzung, die in die Warteschlange gestellt wurde, ist eine Transaktion erforderlich.Stellen Sie sicher, dass ein Transaktionsbereich angegeben ist, um die Nachricht in der Sitzung zu senden.|  
|MsmqTransactionRequired|Es ist eine Transaktion erforderlich, aber nicht verfügbar.Es können keine Nachrichten gesendet oder empfangen werden.Stellen Sie sicher, dass der Transaktionsbereich angegeben ist, um Nachrichten zu senden oder zu empfangen.|  
|MsmqUnsupportedSerializationFormat|Ein Deserialisierungsfehler ist aufgetreten.Die Nachricht kann nicht empfangen werden und wird verworfen.Das angegebene Serialisierungsformat wird nicht unterstützt.|  
|MsmqWrongPrivateQueueSyntax|Die URL ist ungültig.Die URL für die Warteschlange darf das Zeichen "$" nicht enthalten.Verwenden Sie die Syntax in net.msmq:\/\/machine\/private\/queueName, um eine private Warteschlange zu adressieren.|