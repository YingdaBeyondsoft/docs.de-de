---
title: "Konfiguration und Metadatenunterst&#252;tzung | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 27c240cb-8cab-472c-87f8-c864f4978758
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Konfiguration und Metadatenunterst&#252;tzung
In diesem Thema wird beschrieben, wie Konfigurations\- und Metadatenunterstützung für Bindungen und Bindungselemente aktiviert wird.  
  
## Überblick über Konfiguration und Metadaten  
 Dieses Thema behandelt die folgenden Aufgaben, wobei es sich um die optionalen Posten 1, 2 und 4 in der Aufgabenliste [Entwickeln von Kanälen](../../../../docs/framework/wcf/extending/developing-channels.md) handelt.  
  
-   Aktivierung von Unterstützung der Konfigurationsdatei für ein Bindungselement.  
  
-   Aktivierung von Unterstützung der Konfigurationsdatei für eine Bindung.  
  
-   Export von WSDL und Richtlinienassertionen für ein Bindungselement.  
  
-   Identifizierung von WSDL und Richtlinienassertionen für das Einsetzen und Konfigurieren der Bindung oder des Bindungselements.  
  
 Weitere Informationen über die Erstellung von benutzerdefinierten Bindungen und Bindungselementen finden Sie unter [Erstellen benutzerdefinierter Bindungen](../../../../docs/framework/wcf/extending/creating-user-defined-bindings.md) und [Erstellen eines BindingElement](../../../../docs/framework/wcf/extending/creating-a-bindingelement.md).  
  
## Hinzufügen von Konfigurationsunterstützung  
 Zum Aktivieren der Konfigurationsdateiunterstützung für einen Kanal müssen Sie zwei Konfigurationsabschnitte implementieren, <xref:System.ServiceModel.Configuration.BindingElementExtensionElement?displayProperty=fullName>, wodurch die Konfigurationsunterstützung für Bindungselemente aktiviert wird, und das <xref:System.ServiceModel.Configuration.StandardBindingElement?displayProperty=fullName> sowie das <xref:System.ServiceModel.Configuration.StandardBindingCollectionElement%602?displayProperty=fullName> implementieren, wodurch die Konfigurationsunterstützung für Bindungen aktiviert wird.  
  
 Einfacher ist dies durch die Verwendung des [ConfigurationCodeGenerator](../../../../docs/framework/wcf/samples/configurationcodegenerator.md)\-Beispieltools zur Erzeugung eines Konfigurationscodes für Ihre Bindungen und Bindungselemente zu erreichen.  
  
### Erweitern von BindingElementExtensionElement  
 Der folgende Beispielcode stammt aus [Transport: UDP](../../../../docs/framework/wcf/samples/transport-udp.md).`UdpTransportElement` ist ein <xref:System.ServiceModel.Configuration.BindingElementExtensionElement>, das `UdpTransportBindingElement` für das Konfigurationssystem verfügbar macht.Mit wenigen grundlegenden Überschreibungen definiert das Beispiel den Konfigurationsabschnittsnamen, den Typ des Bindungselements und wie das Bindungselement erstellt wird.Benutzer können dann wie folgt den Erweiterungsabschnitt in einer Konfigurationsdatei registrieren.  
  
```  
<configuration>  
  <system.serviceModel>  
    <extensions>  
      <bindingElementExtensions>  
      <add name="udpTransport" type="Microsoft.ServiceModel.Samples.UdpTransportElement, UdpTransport />  
      </bindingElementExtensions>  
    </extensions>  
  </system.serviceModel>  
</configuration>  
  
```  
  
 Die Erweiterung kann von benutzerdefinierten Bindungen verwiesen werden, um UDP als Transport zu nutzen.  
  
```  
<configuration>  
  <system.serviceModel>  
    <bindings>  
      <customBinding>  
       <binding configurationName="UdpCustomBinding">  
         <udpTransport/>  
       </binding>  
      </customBinding>  
    </bindings>  
  </system.serviceModel>  
</configuration>  
  
```  
  
### Hinzufügen einer Konfiguration für eine Bindung  
 Der Abschnitt `SampleProfileUdpBindingCollectionElement` ist ein <xref:System.ServiceModel.Configuration.StandardBindingCollectionElement%602>, das die `SampleProfileUdpBinding` für das Konfigurationssystem verfügbar macht.Dem `SampleProfileUdpBindingConfigurationElement`, das sich von <xref:System.ServiceModel.Configuration.StandardBindingElement> herleitet, wird der Großteil der Implementierung übertragen.Das `SampleProfileUdpBindingConfigurationElement` verfügt über Eigenschaften, die mit den Eigenschaften auf `SampleProfileUdpBinding` übereinstimmen, sowie über Funktionen für die Zuordnung von der `ConfigurationElement` \-Bindung.Schließlich wird die `OnApplyConfiguration`\-Methode in der `SampleProfileUdpBinding` überschrieben. Dies wird im folgenden Beispielcode veranschaulicht.  
  
```  
protected override void OnApplyConfiguration(string configurationName)  
{  
            if (binding == null)  
                throw new ArgumentNullException("binding");  
  
            if (binding.GetType() != typeof(SampleProfileUdpBinding))  
            {  
                throw new ArgumentException(string.Format(CultureInfo.CurrentCulture,  
                    "Invalid type for binding. Expected type: {0}. Type passed in: {1}.",  
                    typeof(SampleProfileUdpBinding).AssemblyQualifiedName,  
                    binding.GetType().AssemblyQualifiedName));  
            }  
            SampleProfileUdpBinding udpBinding = (SampleProfileUdpBinding)binding;  
  
            udpBinding.OrderedSession = this.OrderedSession;  
            udpBinding.ReliableSessionEnabled = this.ReliableSessionEnabled;  
            udpBinding.SessionInactivityTimeout = this.SessionInactivityTimeout;  
            if (this.ClientBaseAddress != null)  
                   udpBinding.ClientBaseAddress = ClientBaseAddress;  
}  
  
```  
  
 Um diesen Handler mit dem Konfigurationssystem zu registrieren, fügen Sie der relevanten Konfigurationsdatei den folgenden Abschnitt hinzu.  
  
```  
<configuration>  
  <configSections>  
     <sectionGroup name="system.serviceModel">  
         <sectionGroup name="bindings">  
                 <section name="sampleProfileUdpBinding" type="Microsoft.ServiceModel.Samples.SampleProfileUdpBindingCollectionElement, UdpTransport />  
         </sectionGroup>  
     </sectionGroup>  
  </configSections>  
</configuration>  
```  
  
 Darauf kann dann vom [\<system.serviceModel\>](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md)\-Konfigurationsabschnitt verwiesen werden.  
  
```  
<configuration>  
  <system.serviceModel>  
    <client>  
      <endpoint configurationName="calculator"  
                address="soap.udp://localhost:8001/"   
                bindingConfiguration="CalculatorServer"  
                binding="sampleProfileUdpBinding"   
                contract= "Microsoft.ServiceModel.Samples.ICalculatorContract">  
      </endpoint>  
    </client>  
  </system.serviceModel>  
</configuration>  
  
```  
  
## Hinzufügen von Metadatenunterstützung für ein Bindungselement  
 Um einen Kanal in ein Metadatensystem zu integrieren, muss dieser sowohl den Import als auch den Export von Richtlinien unterstützen.Dies ermöglicht es Tools wie [ServiceModel Metadata Utility\-Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md), Clients des Bindungselements zu generieren.  
  
### Hinzufügen von WSDL\-Unterstützung  
 Das Transportbindungselement in einer Bindung ist für den Export und Import von Adressierungsinformationen in\/zu Metadaten verantwortlich.Bei der Nutzung einer SOAP\-Bindung sollte das Transportbindungselement ebenfalls einen korrekten Transport\-URI in die Metadaten exportieren.Der folgende Beispielcode stammt aus [Transport: UDP](../../../../docs/framework/wcf/samples/transport-udp.md).  
  
#### WSDL\-Export  
 Um Adressierungsinformationen zu exportieren, implementiert das `UdpTransportBindingElement` die <xref:System.ServiceModel.Description.IWsdlExportExtension?displayProperty=fullName>\-Schnittstelle.Die <xref:System.ServiceModel.Description.IWsdlExportExtension.ExportEndpoint%2A?displayProperty=fullName>\-Methode fügt dem WSDL\-Port die richtigen Adressierungsinformationen hinzu.  
  
```  
if (context.WsdlPort != null)  
{  
    AddAddressToWsdlPort(context.WsdlPort, context.Endpoint.Address, encodingBindingElement.MessageVersion.Addressing);  
}  
```  
  
 Die `UdpTransportBindingElement`\-Implementierung der <xref:System.ServiceModel.Description.IWsdlExportExtension.ExportEndpoint%2A>\-Methode exportiert ebenfalls einen Transport\-URI, wenn der Endpunkt eine SOAP\-Bindung verwendet.  
  
```  
WsdlNS.SoapBinding soapBinding = GetSoapBinding(context, exporter);  
if (soapBinding != null)  
{  
    soapBinding.Transport = UdpPolicyStrings.UdpNamespace;  
}  
```  
  
#### WSDL\-Import  
 Um das WSDL\-Importsystem auf die Handhabung des Imports von Adressen zu erweitern, fügen Sie die folgende Konfiguration zur Konfigurationsdatei für Svcutil.exe hinzu \(wie in der Datei Svcutil.exe.config gezeigt\):  
  
```  
<configuration>  
  <system.serviceModel>  
    <client>  
      <metadata>  
        <wsdlImporters>  
          <extension type=" Microsoft.ServiceModel.Samples.UdpBindingElementImporter, UdpTransport" />  
        </policyImporters>  
      </metadata>  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
 Bei der Ausführung von Svcutil.exe gibt es zwei Optionen, um Svcutil.exe dazu zu bewegen, die WSDL\-Importerweiterungen zu laden:  
  
1.  Verweisen Sie Svcutil.exe mithilfe der \/SvcutilConfig:\<\-Datei\> auf die Konfigurationsdatei.  
  
2.  Fügen Sie den Konfigurationsabschnitt zu Svcutil.exe.config im gleichen Verzeichnis wie Svcutil.exe hinzu.  
  
 Der `UdpBindingElementImporter`\-Typ implementiert die <xref:System.ServiceModel.Description.IWsdlImportExtension?displayProperty=fullName>\-Schnittstelle.Die `ImportEndpoint`\-Methode importiert die Adresse vom WSDL\-Anschluss:  
  
```  
BindingElementCollection bindingElements = context.Endpoint.Binding.CreateBindingElements();  
TransportBindingElement transportBindingElement = bindingElements.Find<TransportBindingElement>();  
if (transportBindingElement is UdpTransportBindingElement)  
{  
    ImportAddress(context);  
}  
```  
  
### Hinzufügen von Richtlinienunterstützung  
 Das benutzerdefinierte Bindungselement kann Richtlinienassertionen in die WSDL\-Bindung für einen Dienstendpunkt exportieren, um die Funktionen dieses Bindungselements auszudrücken.Der folgende Beispielcode stammt aus [Transport: UDP](../../../../docs/framework/wcf/samples/transport-udp.md).  
  
#### Richtlinienexport  
 Der `UdpTransportBindingElement`\-Typ implementiert ``<xref:System.ServiceModel.Description.IPolicyExportExtension?displayProperty=fullName>, um den Export von Richtlinien zu unterstützen.Als Ergebnis schließt <xref:System.ServiceModel.Description.MetadataExporter?displayProperty=fullName>`UdpTransportBindingElement` in die Generierung der Richtlinie für eine Bindung, die dieses enthält, ein.  
  
 Fügen Sie in <xref:System.ServiceModel.Description.IPolicyExportExtension.ExportPolicy%2A?displayProperty=fullName> eine Assertion für UDP und eine weitere Assertion ein, wenn der Kanal sich im Multicastmodus befindet.Grund hierfür ist, dass der Multicastmodus Einfluss auf die Art und Weise hat, in der der Kommunikationsstapel erstellt wird, weshalb eine Koordinierung zwischen beiden Seiten stattfinden muss.  
  
```  
ICollection<XmlElement> bindingAssertions = context.GetBindingAssertions();  
XmlDocument xmlDocument = new XmlDocument();  
bindingAssertions.Add(xmlDocument.CreateElement(  
UdpPolicyStrings.Prefix, UdpPolicyStrings.TransportAssertion, UdpPolicyStrings.UdpNamespace));  
if (Multicast)  
{  
    bindingAssertions.Add(xmlDocument.CreateElement(  
UdpPolicyStrings.Prefix, UdpPolicyStrings.MulticastAssertion,     UdpPolicyStrings.UdpNamespace));  
}  
```  
  
 Da benutzerdefinierte Transportbindungselemente für die Handhabung der Adressierung verantwortlich sind, muss die <xref:System.ServiceModel.Description.IPolicyExportExtension?displayProperty=fullName>\-Implementierung auf dem `UdpTransportBindingElement` auch den Export der geeigneten WS\-Adressierungsrichtlinienassertionen handhaben, um die Version der verwendeten WS\-Adressierung anzugeben.  
  
```  
AddWSAddressingAssertion(context, encodingBindingElement.MessageVersion.Addressing);  
```  
  
#### Richtlinienimport  
 Um das Richtlinienimportsystem zu erweitern, fügen Sie der Konfigurationsdatei für Svcutil.exe die folgende Konfiguration hinzu \(wie in der Datei Svcutil.exe.config gezeigt\):  
  
```  
<configuration>  
  <system.serviceModel>  
    <client>  
      <metadata>  
        <policyImporters>  
          <extension type=" Microsoft.ServiceModel.Samples.UdpBindingElementImporter, UdpTransport" />  
        </policyImporters>  
      </metadata>  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
 Dann implementieren Sie <xref:System.ServiceModel.Description.IPolicyImportExtension?displayProperty=fullName> aus der registrierten Klasse \(`UdpBindingElementImporter`\).Prüfen Sie in <xref:System.ServiceModel.Description.IPolicyImportExtension.ImportPolicy%2A?displayProperty=fullName> die Assertionen im entsprechenden Namespace, verarbeiten Sie sie für die Generierung des Transports, und prüfen Sie, ob Multicast vorliegt.Entfernen Sie darüber hinaus die Assertionen, die das Importprogramm handhabt, aus der Liste der Bindungsassertionen.Erneut stehen bei der Ausführung von Svcutil.exe zwei Optionen für die Integration zur Verfügung:  
  
1.  Verweisen Sie Svcutil.exe mithilfe der \/SvcutilConfig:\<\-Datei\> auf die Konfigurationsdatei.  
  
2.  Fügen Sie den Konfigurationsabschnitt zu Svcutil.exe.config im gleichen Verzeichnis wie Svcutil.exe hinzu.  
  
### Hinzufügen eines benutzerdefinierten Standardbindungsimportprogramms  
 Svcutil.exe und der <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=fullName>\-Typ erkennen und importieren vom System bereitgestellte Bindungen standardmäßig.Andernfalls wird die Bindung als <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=fullName>\-Instanz importiert.Zur Aktivierung des Imports der `SampleProfileUdpBinding` für Svcutil.exe und den <xref:System.ServiceModel.Description.WsdlImporter>, fungiert der `UdpBindingElementImporter` auch als benutzerdefiniertes Standardbindungsimportprogramm.  
  
 Ein benutzerdefiniertes Standardbindungsimportprogramm implementiert die `ImportEndpoint`\-Methode auf der <xref:System.ServiceModel.Description.IWsdlImportExtension?displayProperty=fullName>\-Schnittstelle, um zu prüfen, ob die aus den Metadaten importierte <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=fullName>\-Instanz von einer spezifischen Standardbindung hätte generiert werden können.  
  
```  
if (context.Endpoint.Binding is CustomBinding)  
{  
    Binding binding;  
    if (transportBindingElement is UdpTransportBindingElement)  
    {  
        //if TryCreate is true, the CustomBinding will be replace by a SampleProfileUdpBinding in the  
        //generated config file for better typed generation.  
        if (SampleProfileUdpBinding.TryCreate(bindingElements, out binding))  
        {  
            binding.Name = context.Endpoint.Binding.Name;  
            binding.Namespace = context.Endpoint.Binding.Namespace;  
            context.Endpoint.Binding = binding;  
        }  
    }  
}  
```  
  
 Allgemein beinhaltet die Implementierung eines benutzerdefinierten Standardbindungsimportprogramms die Überprüfung der Eigenschaften der importierten Bindungen, um zu bestätigen, dass sich nur Eigenschaften geändert haben, die von der Standardbindung hätten festgelegt werden können, und es sich bei allen anderen Eigenschaften um die Standardwerte handelt.Eine grundlegende Strategie für die Implementierung eines Standardbindungsimportprogramms ist die Erstellung einer Standardbindung, die Weitergabe der Eigenschaften von den Bindungselementen an die von der Standardbindung unterstützte Standardbindungsinstanz und der Vergleich der Bindungselemente der Standardbindung mit den importierten Bindungselementen.