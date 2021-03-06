---
title: ETW-Ereignisse in der Task Parallel Library und PLINQ
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- tasks, ETW events
ms.assetid: 87a9cff5-d86f-4e44-a06e-d12764d0dce2
caps.latest.revision: 7
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 9de80f9f2319caefbb7b716e17c43fddf9db67e4
ms.contentlocale: de-de
ms.lasthandoff: 08/21/2017

---
# <a name="etw-events-in-task-parallel-library-and-plinq"></a>ETW-Ereignisse in der Task Parallel Library und PLINQ
Die Task Parallel Library und PLINQ generieren Ereignisse für die Ereignisablaufverfolgung für Windows (ETW), die Sie zur Profilerstellung und Problembehebung für Anwendungen verwenden können, indem Sie Tools wie den Windows Performance Analyzer verwenden. In den meisten Szenarios ist der beste Weg der Profilerstellung für parallelen Anwendungscode jedoch das Verwenden der [Parallelitätsschnellansicht](/visualstudio/profiling/concurrency-visualizer) in [!INCLUDE[vsUltShort](../../../includes/vsultshort-md.md)].  
  
## <a name="task-parallel-library-etw-events"></a>Task Parallel Library-ETW-Ereignisse  
 In der EVENT_HEADER-Struktur, ist Folgendes die ProviderId-GUID für Ereignisse, die durch <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=fullName>, <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName> und <xref:System.Threading.Tasks.Parallel.Invoke%2A?displayProperty=fullName> generiert wurden:  
  
```  
0x2e5dba47, 0xa3d2, 0x4d16, 0x8e, 0xe0, 0x66, 0x71, 0xff, 0xdc, 0xd7, 0xb5  
```  
  
### <a name="parallel-loop-begin"></a>Beginn der parallelen Schleife  
 EVENT_DESCRIPTOR.Task = 1  
  
 EVENT_DESCRIPTOR.Id = 1  
  
#### <a name="user-data"></a>Benutzerdaten  
  
|**Name**|**Typ**|**Beschreibung**|  
|--------------|--------------|---------------------|  
|OriginatingTaskSchedulerID|<xref:System.Int32?displayProperty=fullName>|Die ID des TaskScheduler, der die Schleife gestartet hat.|  
|OriginatingTaskID|<xref:System.Int32?displayProperty=fullName>|Die ID der Aufgabe, die die Schleife gestartet hat.|  
|ForkJoinContextID|<xref:System.Int32?displayProperty=fullName>|Ein eindeutiger Bezeichner, der verwendet wird, um Schachteln und Paare für Ereignisse mit einer Semantik für Abzweigungen und Zusammenführungen anzugeben.|  
|OperationType|<xref:System.Int32?displayProperty=fullName>|Gibt den Typ der Schleife an:<br /><br /> 1 = ParallelInvoke<br /><br /> 2 = ParallelFor<br /><br /> 3 = ParallelForEach|  
|InclusiveFrom|<xref:System.Int64?displayProperty=fullName>|Der Anfangswert des Schleifenzählers|  
|ExclusiveTo|<xref:System.Int64?displayProperty=fullName>|Der Endwert des Schleifenzählers|  
  
### <a name="parallel-loop-end"></a>Ende der parallelen Schleife  
 EVENT_DESCRIPTOR.Task = 2  
  
 EVENT_DESCRIPTOR.Id = 2  
  
#### <a name="user-data"></a>Benutzerdaten  
  
|**Name**|**Typ**|**Beschreibung**|  
|--------------|--------------|---------------------|  
|OriginatingTaskSchedulerID|<xref:System.Int32?displayProperty=fullName>|Die ID des TaskScheduler, der die Schleife gestartet hat.|  
|OriginatingTaskID|<xref:System.Int32?displayProperty=fullName>|Die ID der Aufgabe, die die Schleife gestartet hat.|  
|ForkJoinContextID|<xref:System.Int32?displayProperty=fullName>|Ein eindeutiger Bezeichner, der verwendet wird, um Schachteln und Paare für Ereignisse mit einer Semantik für Abzweigungen und Zusammenführungen anzugeben.|  
|totalIterations|<xref:System.Int64?displayProperty=fullName>|Gesamtanzahl von Iterationen|  
  
### <a name="parallel-invoke-begin"></a>Beginn des parallelen Aufrufs  
 EVENT_DESCRIPTOR.Task = 3  
  
 EVENT_DESCRIPTOR.Id = 3  
  
#### <a name="user-data"></a>Benutzerdaten  
  
|**Name**|**Typ**|**Beschreibung**|  
|--------------|--------------|---------------------|  
|OriginatingTaskSchedulerID|<xref:System.Int32?displayProperty=fullName>|Die ID des TaskScheduler, der die Schleife gestartet hat.|  
|OriginatingTaskID|<xref:System.Int32?displayProperty=fullName>|Die ID der Aufgabe, die die Schleife gestartet hat.|  
|ForkJoinContextID|<xref:System.Int32?displayProperty=fullName>|Ein eindeutiger Bezeichner, der verwendet wird, um Schachteln und Paare für Ereignisse mit einer Semantik für Abzweigungen und Zusammenführungen anzugeben.|  
|totalIterations|<xref:System.Int64?displayProperty=fullName>|Gesamtanzahl von Iterationen|  
|operationType|<xref:System.Int32?displayProperty=fullName>|Gibt den Typ der Schleife an:<br /><br /> 1 = ParallelInvoke<br /><br /> 2 = ParallelFor<br /><br /> 3 = ParallelForEach|  
|ActionCount|<xref:System.Int32?displayProperty=fullName>|Die Anzahl der Aktionen, die im parallelen Aufruf ausgeführt wird.|  
  
### <a name="parallel-invoke-end"></a>Ende des parallelen Aufrufs  
 EVENT_DESCRIPTOR.Task = 4  
  
 EVENT_DESCRIPTOR.Id = 4  
  
#### <a name="user-data"></a>Benutzerdaten  
  
|**Name**|**Typ**|**Beschreibung**|  
|--------------|--------------|---------------------|  
|OriginatingTaskSchedulerID|<xref:System.Int32?displayProperty=fullName>|Die ID des TaskScheduler, der die Schleife gestartet hat.|  
|OriginatingTaskID|<xref:System.Int32?displayProperty=fullName>|Die ID der Aufgabe, die die Schleife gestartet hat.|  
|ForkJoinContextID|<xref:System.Int32?displayProperty=fullName>|Ein eindeutiger Bezeichner, der verwendet wird, um Schachteln und Paare für Ereignisse mit einer Semantik für Abzweigungen und Zusammenführungen anzugeben.|  
  
## <a name="plinq-etw-events"></a>PLINQ-ETW-Ereignisse  
 Die EVENT_HEADER.ProviderId-GUID für PLINQ ist:  
  
```  
0x159eeeec, 0x4a14, 0x4418, 0xa8, 0xfe, 0xfa, 0xab, 0xcd, 0x98, 0x78, 0x87  
```  
  
### <a name="parallel-query-begin"></a>Beginn der parallelen Abfrage  
 EVENT_DESCRIPTOR.Task = 1  
  
 EVENT_DESCRIPTOR.Id = 1  
  
#### <a name="user-data"></a>Benutzerdaten  
  
|**Name**|**Typ**|**Beschreibung**|  
|--------------|--------------|---------------------|  
|OriginatingTaskSchedulerID|<xref:System.Int32?displayProperty=fullName>|Die ID des TaskScheduler, der die Schleife gestartet hat.|  
|OriginatingTaskID|<xref:System.Int32?displayProperty=fullName>|Die ID der Aufgabe, die die Schleife gestartet hat.|  
|QueryID|<xref:System.Int32?displayProperty=fullName>|Ein eindeutiger Bezeichner der Abfrage.|  
  
### <a name="parallel-query-end"></a>Ende der parallelen Abfrage  
 EVENT_DESCRIPTOR.Task = 2  
  
 EVENT_DESCRIPTOR.Id = 2  
  
#### <a name="user-data"></a>Benutzerdaten  
  
|**Name**|**Typ**|**Beschreibung**|  
|--------------|--------------|---------------------|  
|OriginatingTaskSchedulerID|<xref:System.Int32?displayProperty=fullName>|Die ID des TaskScheduler, der die Schleife gestartet hat.|  
|OriginatingTaskID|<xref:System.Int32?displayProperty=fullName>|Die ID der Aufgabe, die die Schleife gestartet hat.|  
|QueryID|<xref:System.Int32?displayProperty=fullName>|Ein eindeutiger Bezeichner der Abfrage.|  
  
## <a name="see-also"></a>Siehe auch  
 [ETW-Ereignisse in .NET Framework](../../../docs/framework/performance/etw-events.md)   
 [Task Parallel Library (TPL)](../../../docs/standard/parallel-programming/task-parallel-library-tpl.md)   
 [Parallel LINQ (PLINQ) (Paralleles LINQ (PLINQ))](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)

