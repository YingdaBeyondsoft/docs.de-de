---
title: "Tabelle für Standardwerte (C#-Referenz)"
descripton: Learn what are the default values of value types returned by the default constructors.
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- constructors [C#], return values
- keywords [C#], new
- default constructor [C#]
- defaults [C#]
- value types [C#], initializing
- variables [C#], value types
- constructors [C#], default constructor
- types [C#], default constructor return values
ms.assetid: 4af2c1df-9e3a-48c1-83ac-b192986fc5bc
caps.latest.revision: 12
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: f8cf12317f1f0163028db003ff31604480da5d1c
ms.openlocfilehash: 975d416259778e0741347829d8a9c79aaa6cfc8c
ms.contentlocale: de-de
ms.lasthandoff: 08/12/2017

---
# <a name="default-values-table-c-reference"></a>Tabelle für Standardwerte (C#-Referenz)
In der folgenden Tabelle werden die Standardwerte von Werttypen gezeigt, die von den Standardkonstruktoren zurückgegeben werden. Standardkonstruktoren werden mit dem `new`-Operator wie folgt aufgerufen:

```csharp
int myInt = new int();
```

Die vorherige Anweisung hat den gleichen Effekt wie die folgende:

```csharp
int myInt = 0;
```

Denken Sie daran, dass die Verwendung von nicht initialisierten Variablen in C# nicht zulässig ist.

|Werttyp|Standardwert|
|----------------|-------------------|
|[bool](../../../csharp/language-reference/keywords/bool.md)|`false`|
|[byte](../../../csharp/language-reference/keywords/byte.md)|0|
|[char](../../../csharp/language-reference/keywords/char.md)|'\0'|
|[decimal](../../../csharp/language-reference/keywords/decimal.md)|0.0M|
|[double](../../../csharp/language-reference/keywords/double.md)|0.0D|
|[enum](../../../csharp/language-reference/keywords/enum.md)|Der Wert, der vom Ausdruck (E)0 erzeugt wird, bei dem E der Enumerationsbezeichner ist.|
|[float](../../../csharp/language-reference/keywords/float.md)|0.0F|
|[int](../../../csharp/language-reference/keywords/int.md)|0|
|[long](../../../csharp/language-reference/keywords/long.md)|0L|
|[sbyte](../../../csharp/language-reference/keywords/sbyte.md)|0|
|[short](../../../csharp/language-reference/keywords/short.md)|0|
|[struct](../../../csharp/language-reference/keywords/struct.md)|Der Wert, der erzeugt wird, indem alle Werttypfelder auf ihre Standardwerte festgelegt werden und alle Verweistypfelder auf `null`.|
|[uint](../../../csharp/language-reference/keywords/uint.md)|0|
|[ulong](../../../csharp/language-reference/keywords/ulong.md)|0|
|[ushort](../../../csharp/language-reference/keywords/ushort.md)|0|

## <a name="see-also"></a>Siehe auch
 [C#-Referenz](../../../csharp/language-reference/index.md)   
 [C#-Programmierhandbuch](../../../csharp/programming-guide/index.md)   
 [Tabelle der Werttypen](../../../csharp/language-reference/keywords/value-types-table.md)   
 [Werttypen](../../../csharp/language-reference/keywords/value-types.md)   
 [Tabelle integrierter Typen](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [Referenztabellen für Typen](../../../csharp/language-reference/keywords/reference-tables-for-types.md)

