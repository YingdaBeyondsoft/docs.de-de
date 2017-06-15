---
title: "Benutzerdefinierte Stream-Upgrades | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e3da85c8-57f3-4e32-a4cb-50123f30fea6
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Benutzerdefinierte Stream-Upgrades
Streamorientierte Transports wie TCP und benannte Pipes werden auf einem fortlaufenden Bytestream zwischen Client und Server ausgeführt.  Dieser Stream wird durch ein <xref:System.IO.Stream>\-Objekt realisiert.  Bei einem Stream\-Upgrade will der Client dem Kanalstapel eine optionale Protokollebene hinzufügen und fordert das andere Ende des Kommunikationskanals dazu auf.  Das Stream\-Upgrade besteht aus dem Ersetzen des ursprünglichen <xref:System.IO.Stream>\-Objekts durch ein aktualisiertes Objekt.  
  
 Sie können z. B. einen Komprimierungsstream direkt über dem Transportstream erstellen.  In diesem Fall wird der ursprüngliche Transport\-<xref:System.IO.Stream> durch einen Stream ersetzt, der den ursprünglichen Stream mit dem Komprimierungs\-<xref:System.IO.Stream> umschließt.  
  
 Sie können mehrere Stream\-Upgrades implementieren, die das jeweils vorangehende Upgrade umschließen.  
  
## Funktionsweise von Stream\-Upgrades  
 Der Stream\-Upgrade\-Prozess besteht aus vier Komponenten.  
  
1.  Der Vorgang wird mit einem *Initiator* für den Upgrade\-Stream gestartet: Er kann zur Laufzeit eine Anforderung an das andere Ende der Verbindung zum Upgrade der Kanaltransportebene initialisieren.  
  
2.  Ein *Annehmender* für den Upgrade\-Stream führt das Upgrade aus: Er empfängt zur Laufzeit die Upgradeanforderung von dem anderen Computer und akzeptiert ggf. das Upgrade.  
  
3.  Ein *Upgradeanbieter* erstellt den *Initiator* auf dem Client und den *Annehmenden* auf dem Server.  
  
4.  Ein *Bindungselement* für das Stream\-Upgrade wird den Bindungen auf dem Dienst und dem Client hinzugefügt und erstellt zur Laufzeit den Anbieter.  
  
 Bei mehreren Upgrades kapseln der Initiator und der Annehmende Zustandsautomaten, um zu erzwingen, welche Upgradeübergänge für jede Initiierung gültig sind.  
  
## So implementieren Sie ein Streamupgrade  
 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] stellt vier `abstract`\-Klassen bereit, die Sie implementieren können:  
  
-   <xref:System.ServiceModel.Channels.StreamUpgradeInitiator?displayProperty=fullName>  
  
-   <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor?displayProperty=fullName>  
  
-   <xref:System.ServiceModel.Channels.StreamUpgradeProvider?displayProperty=fullName>  
  
-   <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement?displayProperty=fullName>  
  
 Gehen Sie wie folgt vor, um ein benutzerdefiniertes Streamupgrade zu implementieren.  Bei dieser Prozedur wird ein minimaler Streamupgradevorgang auf den Client\- und Servercomputern implementiert.  
  
1.  Erstellen Sie eine Klasse, die das <xref:System.ServiceModel.Channels.StreamUpgradeInitiator> implementiert.  
  
    1.  Überschreiben Sie die <xref:System.ServiceModel.Channels.StreamUpgradeInitiator.InitiateUpgrade%2A>\-Methode, um den zu aktualisierenden Stream anzugeben, und geben Sie den aktualisierten Stream zurück.  Diese Methode funktioniert synchron; es gibt analoge Methoden, um das Upgrade asynchron zu initiieren.  
  
    2.  Überschreiben Sie die <xref:System.ServiceModel.Channels.StreamUpgradeInitiator.GetNextUpgrade%2A>\-Methode, um zusätzliche Upgrades zu suchen.  
  
2.  Erstellen Sie eine Klasse, die das <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor> implementiert.  
  
    1.  Überschreiben Sie die <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor.AcceptUpgrade%2A>\-Methode, um den zu aktualisierenden Stream anzugeben, und geben Sie den aktualisierten Stream zurück.  Diese Methode funktioniert synchron; es gibt analoge Methoden, um das Upgrade asynchron anzunehmen.  
  
    2.  Überschreiben Sie die <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor.CanUpgrade%2A>\-Methode, um festzulegen, ob das angeforderte Upgrade von dem Annehmenden des Upgrades an dieser Stelle im Upgradeprozess unterstützt wird.  
  
3.  Erstellen Sie eine Klasse, die den <xref:System.ServiceModel.Channels.StreamUpgradeProvider> implementiert.  Überschreiben Sie die <xref:System.ServiceModel.Channels.StreamUpgradeProvider.CreateUpgradeAcceptor%2A>\-Methode und die <xref:System.ServiceModel.Channels.StreamUpgradeProvider.CreateUpgradeInitiator%2A>\-Methode, um Instanzen des in Schritt 1 und 2 definierten Annehmenden und Initiators zurückzugeben.  
  
4.  Erstellen Sie eine Klasse, die das <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement> implementiert.  
  
    1.  Überschreiben Sie die <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement.BuildClientStreamUpgradeProvider%2A>\-Methode auf dem Client und die <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement.BuildServerStreamUpgradeProvider%2A>\-Methode auf dem Dienst.  
  
    2.  Überschreiben Sie die <xref:System.ServiceModel.Channels.BindingElement.BuildChannelFactory%2A>\-Methode auf dem Client und die <xref:System.ServiceModel.Channels.BindingElement.BuildChannelListener%2A>\-Methode auf dem Dienst, um das Upgrade\-Bindungselement zu <xref:System.ServiceModel.Channels.BindingContext.BindingParameters%2A> hinzuzufügen.  
  
5.  Fügen Sie das neue Stream\-Upgrade\-Bindungselement Bindungen auf den Server\- und Clientcomputern hinzu.  
  
## Sicherheitsupgrades  
 Das Hinzufügen eines Sicherheitsupgrades ist eine spezielle Version des allgemeinen Stream\-Upgrade\-Prozesses.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] stellt bereits zwei Bindungselemente für das Upgrade von Stream Security.  Die Konfiguration der Sicherheit auf Transportebene wird durch das <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement> und das <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement> gekapselt, die konfiguriert und einer benutzerdefinierten Bindung hinzugefügt werden können.  Diese Bindungselemente erweitern die <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement>\-Klasse, die den Client\- und Server\-Stream\-Upgrade\-Anbieter erstellt.  Diese Bindungselements enthalten Methoden zum Erstellen der speziellen Upgradeanbieterklassen für Sicherheitsstream, die nicht `public` sind, in diesen beiden Fällen müssen Sie lediglich das Bindungselement der Bindung hinzufügen.  
  
 Bei Sicherheitsszenarien, die die beiden oben angeführten Bindungselemente nicht erfüllen, werden drei sicherheitsrelevante `abstract`\-Klassen von den oben genannten Basisklassen für Initiator, Annehmender und Anbieter abgeleitet:  
  
1.  <xref:System.ServiceModel.Channels.StreamSecurityUpgradeInitiator?displayProperty=fullName>  
  
2.  <xref:System.ServiceModel.Channels.StreamSecurityUpgradeAcceptor?displayProperty=fullName>  
  
3.  <xref:System.ServiceModel.Channels.StreamSecurityUpgradeProvider?displayProperty=fullName>  
  
 Der Vorgang zum Implementieren eines Security Stream\-Upgrades ist der gleiche wie zuvor, mit dem Unterschied, dass Sie von diesen drei Klassen ableiten.  Überschreiben Sie die zusätzlichen Eigenschaften in diesen Klassen, um Sicherheitsinformationen zur Laufzeit anzugeben.  
  
## Mehrere Upgrades  
 Wiederholen Sie zum Erstellen zusätzlicher Upgradeanforderungen den oben aufgeführten Vorgang: Erstellen Sie zusätzliche Erweiterungen von <xref:System.ServiceModel.Channels.StreamUpgradeProvider> und Bindungselemente.  Fügen Sie die Bindungselemente der Bindung hinzu.  Die zusätzlichen Bindungselemente werden nacheinander verarbeitet, beginnend mit dem ersten der Bindung hinzugefügten Bindungselement.  In <xref:System.ServiceModel.Channels.BindingElement.BuildChannelFactory%2A> und <xref:System.ServiceModel.Channels.BindingElement.BuildChannelListener%2A> kann jeder Upgradeanbieter die eigene Anordnung auf bereits vorhandene Upgradebindungsparameter festlegen.  Anschließend muss der vorhandene Upgradebindungsparameter durch einen neuen zusammengesetzten Upgradebindungsparameter ersetzt werden.  
  
 Alternativ kann ein Upgradeanbieter mehrere Upgrades unterstützen.  Sie können z. B. einen benutzerdefinierten Stream\-Upgrade\-Anbieter implementieren, der Sicherheit und Komprimierung unterstützt.  Führen Sie die folgenden Schritte aus:  
  
1.  Bilden Sie eine Unterklasse für den <xref:System.ServiceModel.Channels.StreamSecurityUpgradeProvider>, um die Anbieterklasse zu schreiben, die den Initiator und Annehmenden erstellt.  
  
2.  Bilden Sie eine Unterklasse für den <xref:System.ServiceModel.Channels.StreamSecurityUpgradeInitiator>, und überschreiben Sie die <xref:System.ServiceModel.Channels.StreamUpgradeInitiator.GetNextUpgrade%2A>\-Methode, um die Inhaltstypen für den Komprimierungsstream und den sicheren Stream nacheinander zurückzugeben.  
  
3.  Bilden Sie eine Unterklasse für den <xref:System.ServiceModel.Channels.StreamSecurityUpgradeAcceptor>, der die benutzerdefinierten Inhaltstypen in seiner <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor.CanUpgrade%2A>\-Methode lesen kann.  
  
4.  Der Stream wird nach jedem Aufruf an <xref:System.ServiceModel.Channels.StreamUpgradeInitiator.GetNextUpgrade%2A> und <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor.CanUpgrade%2A> aktualisiert.  
  
## Siehe auch  
 <xref:System.ServiceModel.Channels.StreamUpgradeInitiator>   
 <xref:System.ServiceModel.Channels.StreamSecurityUpgradeInitiator>   
 <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor>   
 <xref:System.ServiceModel.Channels.StreamSecurityUpgradeAcceptor>   
 <xref:System.ServiceModel.Channels.StreamUpgradeProvider>   
 <xref:System.ServiceModel.Channels.StreamSecurityUpgradeProvider>   
 <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement>   
 <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement>   
 <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement>