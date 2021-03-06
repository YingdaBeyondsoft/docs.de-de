---
title: Verzweigte Arrays (C#-Programmierhandbuch)
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- jagged arrays [C#]
- arrays [C#], jagged
ms.assetid: 537c65a6-0e0a-4a00-a2b8-086f38519c70
caps.latest.revision: 24
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: cb6c0823af37924235dba7daa20e607cb8402a79
ms.contentlocale: de-de
ms.lasthandoff: 07/28/2017

---
# <a name="jagged-arrays-c-programming-guide"></a>Verzweigte Arrays (C#-Programmierhandbuch)
Ein verzweigtes Array ist ein Array, dessen Elemente wiederum Arrays sind. Die Elemente eines verzweigten Arrays können eine unterschiedliche Dimension und Größe besitzen. Ein verzweigtes Array wird auch „Array aus Arrays“ genannt. Die folgenden Beispiele zeigen, wie Sie verzweigte Arrays deklarieren, initialisieren und auf sie zugreifen können.  
  
 Die folgende Deklaration veranschaulicht ein eindimensionales Array mit drei Elementen, von denen jedes wiederum ein eindimensionales Array aus ganzen Zahlen darstellt:  
  
 [!code-cs[csProgGuideArrays#19](../../../csharp/programming-guide/arrays/codesnippet/CSharp/jagged-arrays_1.cs)]  
  
 Vor der Verwendung von `jaggedArray` müssen seine Elemente initialisiert werden. Sie können die Elemente folgendermaßen initialisieren:  
  
 [!code-cs[csProgGuideArrays#20](../../../csharp/programming-guide/arrays/codesnippet/CSharp/jagged-arrays_2.cs)]  
  
 Jedes Element ist ein eindimensionales Array aus ganzen Zahlen. Das erste Element ist ein Array aus 5 ganzen Zahlen, das zweite aus 4 und das dritte aus 2.  
  
 Sie können auch Initialisierer verwenden, um die Arrayelemente mit Werten zu füllen. In diesem Fall wird die Arraygröße nicht benötigt. Zum Beispiel:  
  
 [!code-cs[csProgGuideArrays#21](../../../csharp/programming-guide/arrays/codesnippet/CSharp/jagged-arrays_3.cs)]  
  
 Sie können das Array auch nach der Deklaration folgendermaßen initialisieren:  
  
 [!code-cs[csProgGuideArrays#22](../../../csharp/programming-guide/arrays/codesnippet/CSharp/jagged-arrays_4.cs)]  
  
 Sie können folgende Kurzformen verwenden. Beachten Sie, dass der Operator `new` bei der Initialisierung der Elemente nicht ausgelassen werden kann, da es für die Elemente keine Standardinitialisierung gibt:  
  
 [!code-cs[csProgGuideArrays#23](../../../csharp/programming-guide/arrays/codesnippet/CSharp/jagged-arrays_5.cs)]  
  
 Ein verzweigtes Array ist ein Array von Arrays, und deshalb sind seine Elemente Referenztypen und werden mit `null` initialisiert.  
  
 In den folgenden Beispielen wird veranschaulicht, wie Sie auf einzelne Arrayelemente zugreifen können:  
  
 [!code-cs[csProgGuideArrays#24](../../../csharp/programming-guide/arrays/codesnippet/CSharp/jagged-arrays_6.cs)]  
  
 Es ist möglich, verzweigte und mehrdimensionale Arrays zu mischen. Das folgende Beispiel zeigt die Deklaration und Initialisierung eines eindimensionalen verzweigten Arrays, das drei zweidimensionale Arrayelemente unterschiedlicher Größe enthält. Weitere Informationen zu zweidimensionalen Arrays finden Sie unter [Mehrdimensionale Arrays](../../../csharp/programming-guide/arrays/multidimensional-arrays.md).  
  
 [!code-cs[csProgGuideArrays#25](../../../csharp/programming-guide/arrays/codesnippet/CSharp/jagged-arrays_7.cs)]  
  
 Im folgenden Beispiel wird dargestellt, wie Sie auf einzelne Elemente zugreifen können. Der Wert des Elements `[1,0]` des ersten Arrays (Wert `5`) wird angezeigt:  
  
 [!code-cs[csProgGuideArrays#26](../../../csharp/programming-guide/arrays/codesnippet/CSharp/jagged-arrays_8.cs)]  
  
 Die Methode `Length` gibt die Anzahl der Arrays zurück, die im verzweigten Array enthalten sind. Wenn Sie beispielsweise das vorherige Array deklariert haben, dann gibt die folgende Zeile:  
  
 [!code-cs[csProgGuideArrays#27](../../../csharp/programming-guide/arrays/codesnippet/CSharp/jagged-arrays_9.cs)]  
  
 den Wert 3 zurück.  
  
## <a name="example"></a>Beispiel  
 In diesem Beispiel wird ein Array erstellt, dessen Elemente wiederum selbst Arrays sind. Jedes Arrayelement hat eine unterschiedliche Größe.  
  
 [!code-cs[csProgGuideArrays#18](../../../csharp/programming-guide/arrays/codesnippet/CSharp/jagged-arrays_10.cs)]  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Array>   
 [C#-Programmierhandbuch](../../../csharp/programming-guide/index.md)   
 [Arrays](../../../csharp/programming-guide/arrays/index.md)   
 [Eindimensionale Arrays](../../../csharp/programming-guide/arrays/single-dimensional-arrays.md)   
 [Mehrdimensionale Arrays](../../../csharp/programming-guide/arrays/multidimensional-arrays.md)

