---
title: "Angeben und Behandeln von Fehlern in Vertr&#228;gen und Diensten | Microsoft Docs"
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
  - "Behandeln von Fehlern [WCF]"
ms.assetid: a9696563-d404-4905-942d-1e0834c26dea
caps.latest.revision: 22
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 22
---
# Angeben und Behandeln von Fehlern in Vertr&#228;gen und Diensten
[!INCLUDE[indigo1](../../../includes/indigo1-md.md)]\-Anwendungen behandeln Fehler, indem sie verwaltete Ausnahmeobjekte SOAP\-Fehlerobjekten und SOAP\-Fehlerobjekte verwalteten Ausnahmeobjekten zuordnen.Die Themen in diesem Abschnitt erläutern, wie Verträge erstellt werden, die Fehlerbedingungen als benutzerdefinierte SOAP\-Fehler verfügbar machen, wie solche Fehler als Teil einer Dienstimplementierung zurückgegeben werden, und wie Clients diese Fehler abfangen.  
  
## Übersicht über die Fehlerbehandlung  
 In allen verwalteten Anwendungen werden Verarbeitungsfehler durch <xref:System.Exception>\-Objekte dargestellt.In SOAP\-basierten Anwendungen, wie z. B. [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]\-Anwendungen, übermitteln Dienstmethoden Verarbeitungsfehlerinformationen mit SOAP\-Fehlernachrichten.SOAP\-Fehler sind Nachrichtentypen, die in den Metadaten für einen Dienstvorgang enthalten sind und daher einen Fehlervertrag erstellen, den Clients nutzen können, um ihre Ausführung robuster oder interaktiver zu gestalten.Da darüber hinaus SOAP\-Fehler gegenüber Clients in XML\-Form ausgedrückt werden, sind sie ein sehr interoperables Typsystem, das Clients auf jeder SOAP\-Plattform verwenden können, wodurch sich die Reichweite Ihrer [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]\-Anwendung erhöht.  
  
 Da [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]\-Anwendungen unter beiden Fehlersystemtypen ausgeführt werden, müssen alle an den Client zu sendenden verwalteten Ausnahmeinformationen vom Dienst von Ausnahmen in SOAP\-Fehler konvertiert, gesendet und von [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]\-Clients von SOAP\-Fehlern in Ausnahmen konvertiert werden.Im Fall von Duplexclients können Clientverträge SOAP\-Fehler auch zurück an einen Dienst senden.In beiden Fällen können Sie die Standard\-Dienstausnahmeverhalten verwenden oder aber ausdrücklich steuern, ob und wie Ausnahmen Fehlernachrichten zugeordnet werden.  
  
 Zwei Typen von SOAP\-Fehlern können gesendet werden: *deklarierte* und *undeklarierte*.Deklarierte SOAP\-Fehler sind jene, bei denen ein Vorgang über ein <xref:System.ServiceModel.FaultContractAttribute?displayProperty=fullName>\-Attribut verfügt, das einen benutzerdefinierten SOAP\-Fehlertyp angibt.*Undeklarierte* SOAP\-Fehler sind jene, die nicht im Vertrag für einen Vorgang festgelegt wurden.  
  
 Es wird dringend empfohlen, dass Dienstvorgänge ihre Fehler mithilfe des <xref:System.ServiceModel.FaultContractAttribute>\-Attributs deklarieren, um alle SOAP\-Fehler formal anzugeben, die bei einem Client während des normalen Betriebs eingehen können.Es wird außerdem empfohlen, dass in einem SOAP\-Fehler nur die Informationen zurückgegeben werden, die ein Client erhalten muss, um die Offenlegung von Informationen möglichst gering zu halten.  
  
 In der Regel führen Dienste \(und Duplexclients\) die folgenden Schritte aus, um die Fehlerbehandlung erfolgreich in ihre Anwendungen zu integrieren:  
  
-   Sie ordnen Ausnahmebedingungen benutzerdefinierten SOAP\-Fehlern zu.  
  
-   Clients und Dienste senden und empfangen SOAP\-Fehler als Ausnahmen.  
  
 Zusätzlich können [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]\-Clients und \-Dienste undeklarierte SOAP\-Fehler zu Debuggingzwecken verwenden und können ihr standardmäßiges Fehlerverhalten erweitern.Diese Aufgaben und Begriffe werden in den folgenden Abschnitten erläutert.  
  
## Zuordnen von Ausnahmen zu SOAP\-Fehlern  
 Der erste Schritt bei der Definition eines Verfahrens zur Behandlung von Fehlerbedingungen besteht darin zu entscheiden, unter welchen Bedingungen eine Clientanwendung über Fehler informiert werden sollte.Die Fehlerbedingungen mancher Vorgänge werden von ihrer Funktionalität bestimmt.Ein `PurchaseOrder`\-Vorgang könnte z. B. bestimmte Informationen an Kunden zurückgeben, denen es nicht mehr erlaubt ist, eine Bestellung zu tätigen.In anderen Fällen, etwa einem `Calculator`\-Dienst, könnte ein allgemeinerer `MathFault`\-SOAP\-Fehler ausreichen, um alle Fehlerbedingungen für den gesamten Dienst zu beschreiben.Nachdem die Fehlerbedingungen der Clients Ihres Diensts identifiziert wurden, kann ein benutzerdefinierter SOAP\-Fehler erstellt und der Vorgang dafür gekennzeichnet werden, dass er den SOAP\-Fehler zurückgibt, wenn die entsprechende Fehlerbedingung eintritt.  
  
 [!INCLUDE[crabout](../../../includes/crabout-md.md)] zu diesem Entwicklungsschritt für den Service oder Client finden Sie unter [Definieren und Angeben von Fehlern](../../../docs/framework/wcf/defining-and-specifying-faults.md).  
  
## Clients und Dienste behandeln SOAP\-Fehler als Ausnahmen  
 Die Identifizierung von Fehlerbedingungen bei Vorgängen, die Erstellung benutzerdefinierter SOAP\-Fehler sowie die Markierung dieser Vorgänge für die Rückgabe solcher Fehler sind die ersten Schritte einer erfolgreichen Fehlerbehandlung in [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]\-Anwendungen.Der nächste Schritt besteht darin, das Senden und Empfangen dieser Fehler korrekt zu implementieren.In der Regel werden Fehler von Diensten gesendet, um ihre Clientanwendungen über Fehlerbedingungen zu informieren. Duplexclients können jedoch selbst auch SOAP\-Fehler an Dienste senden.  
  
 [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [Senden und Empfangen von Fehlern](../../../docs/framework/wcf/sending-and-receiving-faults.md).  
  
## Undeklarierte SOAP\-Fehler und Debuggen  
 Deklarierte SOAP\-Fehler sind äußerst nützlich zur Erstellung interoperabler, verteilter Anwendungen.In manchen Fällen ist es jedoch für einen Dienst \(oder einen Duplexclient\) nützlich, einen undeklarierten SOAP\-Fehler zu senden, also einen, der in der Web Services Description Language \(WSDL\) für diesen Vorgang nicht erwähnt ist.Bei der Entwicklung eines Diensts können beispielsweise unerwartete Situationen eintreten, in denen es für Debuggingzwecke sinnvoll sein kann, Information an den Client zurückzusenden.Zusätzlich können Sie die <xref:System.ServiceModel.ServiceBehaviorAttribute.IncludeExceptionDetailInFaults%2A?displayProperty=fullName>\-Eigenschaft oder die <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A?displayProperty=fullName>\-Eigenschaft auf `true` festlegen, um [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]\-Clients zu ermöglichen, Informationen über interne Dienstvorgangsausnahmen abzurufen.Das Senden einzelner Fehler und das Festlegen der Eigenschaften des Debugverhaltens werden unter [Senden und Empfangen von Fehlern](../../../docs/framework/wcf/sending-and-receiving-faults.md) beschrieben.  
  
> [!IMPORTANT]
>  Da mit verwalteten Ausnahmen interne Anwendungsinformationen verfügbar gemacht werden können, kann mit der Festlegung von <xref:System.ServiceModel.ServiceBehaviorAttribute.IncludeExceptionDetailInFaults%2A?displayProperty=fullName> oder <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A?displayProperty=fullName> auf `true`[!INCLUDE[indigo2](../../../includes/indigo2-md.md)]\-Clients ermöglicht werden, Informationen über interne Dienstvorgangsausnahmen, einschließlich persönlich identifizierbarer oder anderer vertraulicher Informationen abzurufen.  
>   
>  Daher wird die Festlegung von <xref:System.ServiceModel.ServiceBehaviorAttribute.IncludeExceptionDetailInFaults%2A?displayProperty=fullName> oder <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A?displayProperty=fullName> auf `true` nur für das vorübergehende Debuggen einer Dienstanwendung empfohlen.Außerdem beinhaltet die WSDL für eine Methode, die nicht behandelte verwaltete Ausnahmen auf diese Weise zurückgibt, keinen Vertrag für die <xref:System.ServiceModel.FaultException%601> vom Typ <xref:System.ServiceModel.ExceptionDetail>.Clients müssen auf die Möglichkeit von unbekannten SOAP\-Fehlern vorbereitet sein, die an [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]\-Clients als <xref:System.ServiceModel.FaultException?displayProperty=fullName>\-Objekte zurückgegeben werden, damit sie die Debuginformationen korrekt abrufen können.  
  
## Anpassen der Fehlerbehandlung mit IErrorHandler  
 Wenn Sie spezielle Anforderungen bei der Anpassung der Antwortnachricht für den Client im Fall einer Ausnahme auf Anwendungsebene erfüllen oder spezielle Verarbeitungsschritte ausführen müssen, nachdem eine Antwortnachricht zurückgegeben wurde, dann implementieren Sie die <xref:System.ServiceModel.Dispatcher.IErrorHandler?displayProperty=fullName>\-Schnittstelle.  
  
## Probleme bei der Fehlerserialisierung  
 Beim Deserialisieren eines Fehlervertrags versucht WCF zunächst, den Namen des Fehlervertrags in der SOAP\-Nachricht einem Fehlervertragstyp zuzuordnen.Wenn keine exakte Übereinstimmung gefunden werden kann, wird die Liste der verfügbaren Fehlerverträge in alphabetischer Reihenfolge nach einem kompatiblen Typ durchsucht.Wenn zwei Fehlerverträge kompatible Typen darstellen \(beispielsweise ist einer die Unterklasse eines anderen\), wird möglicherweise der falsche Typ zum Deserialisieren des Fehlers verwendet.Dies geschieht nur, wenn im Fehlervertrag nicht sowohl Name, als auch Namespace und Aktion angegeben wurden.Um dieses Problem zu vermeiden, sollten Fehlerverträge daher stets durch Angabe von Attributen für Name, Namespace und Aktion vollständig qualifiziert werden.Darüber hinaus muss bei verwandten Fehlerverträgen, die von einer freigegebenen Basisklasse abgeleitet wurden, sichergestellt werden, dass neue Member mit `[DataMember(IsRequired=true)]` gekennzeichnet werden.Weitere Informationen über das `IsRequired`\-Attribut finden Sie unter <xref:System.Runtime.Serialization.DataMemberAttribute>.Dadurch wird verhindert, dass ein kompatibler Typ als Basisklasse verwendet wird, und die Deserialisierung des Fehlers in den richtigen abgeleiteten Typ wird erzwungen.  
  
## Siehe auch  
 <xref:System.ServiceModel.FaultException>   
 <xref:System.ServiceModel.FaultContractAttribute>   
 <xref:System.ServiceModel.FaultException>   
 <xref:System.Xml.Serialization.XmlSerializer>   
 <xref:System.ServiceModel.XmlSerializerFormatAttribute>   
 <xref:System.ServiceModel.FaultContractAttribute>   
 <xref:System.ServiceModel.CommunicationException>   
 <xref:System.ServiceModel.FaultContractAttribute.Action%2A>   
 <xref:System.ServiceModel.FaultException.Code%2A>   
 <xref:System.ServiceModel.FaultException.Reason%2A>   
 <xref:System.ServiceModel.FaultCode.SubCode%2A>   
 <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A>   
 [Definieren und Angeben von Fehlern](../../../docs/framework/wcf/defining-and-specifying-faults.md)