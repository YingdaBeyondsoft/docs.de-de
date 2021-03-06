---
title: "Clientkonfiguration | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5da5bd3b-65d9-43b7-91b9-cc9e989b1350
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Clientkonfiguration
Mit der Clientkonfiguration von [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] können Sie die Adressen, Bindungen, Verhaltensweisen sowie Verträge angeben, die von Clients zum Herstellen einer Verbindung mit Dienstendpunkten verwendet werden.  Das [\<client\>](../../../../docs/framework/configure-apps/file-schema/wcf/client.md)\-Element verfügt über ein [\<endpoint\>](http://msdn.microsoft.com/de-de/13aa23b7-2f08-4add-8dbf-a99f8127c017)\-Element, dessen Attribute zum Konfigurieren der Adressen, Bindungen, Verhaltensweisen und Verträge für den Endpunkt verwendet werden.  Diese Attribute werden im Abschnitt "Konfigurieren von Endpunkten" dieses Themas erläutert.  
  
 Das [\<endpoint\>](http://msdn.microsoft.com/de-de/13aa23b7-2f08-4add-8dbf-a99f8127c017)\-Element enthält außerdem ein [\<Metadaten\>](../../../../docs/framework/configure-apps/file-schema/wcf/metadata.md)\-Element, mit dem Einstellungen für das Importieren und Exportieren von Metadaten angegeben werden, ein [\<Kopfzeilen\>](../../../../docs/framework/configure-apps/file-schema/wcf/headers.md)\-Element mit einer Auflistung von benutzerdefinierten Adressheadern sowie ein [\<Identität\>](../../../../docs/framework/configure-apps/file-schema/wcf/identity.md)\-Element, das die Authentifizierung eines Endpunkts durch andere Endpunkte ermöglicht, die Nachrichten mit diesem austauschen.  Die Elemente [\<Kopfzeilen\>](../../../../docs/framework/configure-apps/file-schema/wcf/headers.md) und [\<Identität\>](../../../../docs/framework/configure-apps/file-schema/wcf/identity.md) sind Teil von <xref:System.ServiceModel.EndpointAddress> und werden im Thema [Adressen](../../../../docs/framework/wcf/feature-details/endpoint-addresses.md) behandelt.  Der Unterabschnitt "Konfigurieren von Metadaten" in diesem Thema enthält auch Hyperlinks zu Themen, in denen die Verwendung von Metadatenerweiterungen erläutert wird.  
  
## Konfigurieren von Endpunkten  
 Die Clientkonfiguration soll dem Client das Angeben mindestens eines Endpunkts ermöglichen, der jeweils über einen eigenen Namen, eine eigene Adresse und einen eigenen Vertrag verfügt. Diese sollen jeweils auf die Elemente [\<Bindungen\>](../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md) und [\<Verhalten\>](../../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md) in der Clientkonfiguration verweisen, die zum Konfigurieren des jeweiligen Endpunkts verwendet werden soll.  Die Clientkonfigurationsdatei sollte "App.config" benannt werden, da dieser Name von der Laufzeit von [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] erwartet wird.  Das folgende Beispiel zeigt eine Clientkonfigurationsdatei.  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
        <client>  
          <endpoint  
            name="endpoint1"  
            address="http://localhost/ServiceModelSamples/service.svc"  
            binding="wsHttpBinding"  
            bindingConfiguration="WSHttpBinding_IHello"  
            behaviorConfiguration="IHello_Behavior"  
            contract="IHello" >  
  
            <metadata>  
              <wsdlImporters>  
                <extension  
                  type="Microsoft.ServiceModel.Samples.WsdlDocumentationImporter, WsdlDocumentation"/>  
              </wsdlImporters>  
            </metadata>  
  
            <identity>  
              <servicePrincipalName value="host/localhost" />  
            </identity>  
          </endpoint>  
// Add another endpoint by adding another <endpoint> element.  
          <endpoint  
            name="endpoint2">  
           //Configure another endpoint here.  
          </endpoint>  
        </client>  
  
//The bindings section references by the bindingConfiguration endpoint attribute.  
    <bindings>  
      <wsHttpBinding>  
        <binding name="WSHttpBinding_IHello"   
                 bypassProxyOnLocal="false"   
                 hostNameComparisonMode="StrongWildcard">  
          <readerQuotas maxDepth="32"/>  
          <reliableSession ordered="true"   
                           enabled="false" />  
          <security mode="Message">  
           //Security settings go here.  
          </security>  
        </binding>  
        <binding name="Another Binding"  
        //Configure this binding here.  
        </binding>  
          </wsHttpBinding>  
        </bindings>  
  
//The behavior section references by the behaviorConfiguration endpoint attribute.  
        <behaviors>  
            <endpointBehaviors>  
                <behavior name=" IHello_Behavior ">  
                    <clientVia />  
                </behavior>  
            </endpointBehaviors>  
        </behaviors>  
  
    </system.serviceModel>  
</configuration>  
```  
  
 Das optionale `name`\-Attribut identifiziert eindeutig einen Endpunkt für einen angegebenen Vertrag.  Es wird von <xref:System.ServiceModel.ChannelFactory%601.%23ctor%2A> oder <xref:System.ServiceModel.ClientBase%601.%23ctor%2A> verwendet, um anzugeben, welcher Endpunkt in der Clientkonfiguration das Ziel ist, und muss beim Erstellen eines Kanals zur Verarbeitung geladen werden.  Als Name für die Endpunktkonfiguration kann auch ein Platzhalterzeichen \("\*"\) verwendet werden. Dadurch wird die <xref:System.ServiceModel.ChannelFactory.ApplyConfiguration%2A>\-Methode angewiesen, ggf. genau eine Endpunktkonfiguration in der Datei zu laden. Andernfalls wird eine Ausnahme ausgelöst.  Wenn dieses Attribut nicht angegeben wird, wird der entsprechende Endpunkt als Standardendpunkt verwendet, der mit dem angegebenen Vertragstyp verknüpft ist.  Der Standardwert für das `name`\-Attribut ist eine leere Zeichenfolge, die wie jeder andere Name abgeglichen wird.  
  
 Jedem Endpunkt muss eine Adresse zugeordnet sein, um diesen suchen und identifizieren zu können.  Das `address`\-Attribut kann verwendet werden, um die URL anzugeben, die den Speicherort des Endpunkts bereitstellt.  Die Adresse für einen Dienstendpunkt kann jedoch auch im Code angegeben werden, indem ein Uniform Resource Identifier \(URI\) erstellt und dem <xref:System.ServiceModel.ServiceHost> mit einer der <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%2A>\-Methoden hinzugefügt wird.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Adressen](../../../../docs/framework/wcf/feature-details/endpoint-addresses.md).  Wie bereits erwähnt, sind das [\<Kopfzeilen\>](../../../../docs/framework/configure-apps/file-schema/wcf/headers.md)\- und das[\<Identität\>](../../../../docs/framework/configure-apps/file-schema/wcf/identity.md)\-Element Teil der <xref:System.ServiceModel.EndpointAddress> und werden ebenfalls im Thema [Adressen](../../../../docs/framework/wcf/feature-details/endpoint-addresses.md) besprochen.  
  
 Das `binding`\-Attribut gibt den Typ der Bindung an, der vom Endpunkt beim Herstellen einer Verbindung zu einem Dienst erwartet wird.  Dieser muss einen registrierten Konfigurationsabschnitt aufweisen, um darauf verweisen zu können.  Im vorherigen Beispiel ist dies der Abschnitt [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md), der angibt, dass der Endpunkt ein <xref:System.ServiceModel.WSHttpBinding> verwendet.  Möglicherweise sind jedoch mehrere Bindungen eines angegebenen Typs vorhanden, die vom Endpunkt verwendet werden können.  Diese verfügen jeweils über ein eigenes [\<Bindung\>](../../../../docs/framework/misc/binding.md)\-Element im Typelement \(der Bindung\).  Das `bindingconfiguration`\-Attribut wird verwendet, um zwischen Bindungen des gleichen Typs zu unterscheiden.  Sein Wert wird mit dem `name`\-Attribut des [\<Bindung\>](../../../../docs/framework/misc/binding.md)\-Elements abgestimmt.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)] die Konfiguration einer Clientbindung finden Sie unter [Vorgehensweise: Angeben einer Clientbindung in einer Konfiguration](../../../../docs/framework/wcf/how-to-specify-a-client-binding-in-configuration.md).  
  
 Mit dem `behaviorConfiguration`\-Attribut wird das [\<Verhalten\>](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md) von [\<endpointBehaviors\>](../../../../docs/framework/configure-apps/file-schema/wcf/endpointbehaviors.md) angegeben, das vom Endpunkt verwendet werden soll.  Sein Wert wird mit dem `name`\-Attribut des [\<Verhalten\>](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)\-Elements abgestimmt.  Ein Beispiel zum Angeben von Clientverhaltensweisen mit der Konfiguration finden Sie unter [Konfigurieren von Clientverhalten](../../../../docs/framework/wcf/configuring-client-behaviors.md).  
  
 Das `contract`\-Attribut gibt den Vertrag an, den dieser Endpunkt verfügbar macht.  Dieser Wert wird dem <xref:System.ServiceModel.ServiceContractAttribute.ConfigurationName%2A> des <xref:System.ServiceModel.ServiceContractAttribute> zugeordnet.  Der Standardwert ist der vollständige Typname der Klasse, die den Dienst implementiert.  
  
### Konfigurieren von Metadaten  
 Mit dem [\<Metadaten\>](../../../../docs/framework/configure-apps/file-schema/wcf/metadata.md)\-Element werden Einstellungen zur Registrierung von Metadatenimporterweiterungen angegeben.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)] die Erweiterung des Metadatensystems finden Sie unter [Erweitern des Metadatensystems](../../../../docs/framework/wcf/extending/extending-the-metadata-system.md).  
  
## Siehe auch  
 [Endpunkte: Adressen, Bindungen und Verträge](../../../../docs/framework/wcf/feature-details/endpoints-addresses-bindings-and-contracts.md)   
 [Konfigurieren von Clientverhalten](../../../../docs/framework/wcf/configuring-client-behaviors.md)