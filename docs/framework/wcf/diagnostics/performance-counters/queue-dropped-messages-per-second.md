---
title: "Queued Messages Dropped Per Second | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 74540f52-8762-4147-b5ba-e171180515a3
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Queued Messages Dropped Per Second
Zählername: Queued Messages Dropped Per Second.  
  
## Beschreibung  
 Die Anzahl der Nachrichten, die vom Wartenschlangentransport für diesen Dienst pro Sekunde gelöscht werden.  
  
 Bei diesem Zähler handelt es sich um einen Leistungsindikator vom Typ [PERF\_COUNTER\_COUNTER](http://go.microsoft.com/fwlink/?LinkID=94649), dessen Wert anhand der folgenden Formel berechnet wird:  
  
 \(N 1 \- N 0\)\/\(\(D 1 \- D 0\)\/F\)