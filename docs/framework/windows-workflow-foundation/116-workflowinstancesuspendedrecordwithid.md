---
title: "116 - WorkflowInstanceSuspendedRecordWithId | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 38232c03-6139-4494-a020-79bc83eb9dce
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# 116 - WorkflowInstanceSuspendedRecordWithId
## Eigenschaften  
  
|||  
|-|-|  
|ID|116|  
|Schlüsselwörter|HealthMonitoring, WFTracking|  
|Ebene|Information|  
|Kanal|Microsoft\-Windows\-Application Server\-Applications\/Analytic|  
  
## Beschreibung  
 Dieses Ereignis wird vom ETW\-Überwachungsteilnehmer ausgegeben, wenn eine Workflowinstanz WorkflowInstanceSuspendedRecord ausgibt.  
  
## Meldung  
 TrackRecord \= WorkflowInstanceSuspendedRecord, InstanceID \= %1, RecordNumber \= %2, EventTime \= %3, ActivityDefinitionId \= %4, Reason \= %5, Annotations \= %6, ProfileName \= %7, WorkflowDefinitionIdentity \= %8  
  
## Details  
  
|Datenelementname|Datenelementtyp|Beschreibung|  
|----------------------|---------------------|------------------|  
|InstanceId|xs:GUID|Die Instanz\-ID für den Workflow.|  
|RecordNumber|xs:long|Die Sequenznummer des ausgegebenen Datensatzes.|  
|EventTime|xs:dateTime|Die Zeit in UTC, als das Ereignis ausgegeben wurde.|  
|ActivityDefinitionId|xs:string|Der Name der Stammaktivität im Workflow.|  
|Zustand|xs:string|Der aktuelle Zustand des Workflows.|  
|Anmerkungen|xs:string|Die Anmerkungen, die diesem Ereignis hinzugefügt wurden.  Die Werte werden in einem XML\-Element im Format \<items\>\< item name \= "annotationName" type\="System.String"\>annotationValue\<\/item\>\<\/items\> gespeichert.  Wenn keine Anmerkungen angegeben werden, enthält die Zeichenfolge \<items\/\>.  Die ETW\-Ereignisgröße wird von der ETW\-Puffergröße oder der maximalen Nutzlast für ein ETW\-Ereignis beschränkt.  Wenn die Größe des Ereignisses die ETW\-Beschränkung überschreitet, wird das Ereignis abgeschnitten, indem die Anmerkungen ausgelassen und der Anmerkungswert durch \<items\>...\<\/items\> ersetzt wird.|  
|ProfileName|xs:string|Der Name oder das Überwachungsprofil, das zur Ausgabe dieses Ereignisses geführt hat.|  
|WorkflowDefinitionIdentity|xs:string|Die ID der Workflowdefinition.|  
|AppDomain|xs:string|Die von AppDomain.CurrentDomain.FriendlyName zurückgegebene Zeichenfolge.|