---
title: for (C#-Referenz)
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- for
- for_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- for keyword [C#]
ms.assetid: 34041a40-2c87-467a-9ffb-a0417d8f67a8
caps.latest.revision: 39
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
ms.openlocfilehash: d65c198b0fd763bddae4832290af038b8992eb48
ms.contentlocale: de-de
ms.lasthandoff: 09/25/2017

---
# <a name="for-c-reference"></a>for (C#-Referenz)
Mithilfe einer `for`-Schleife können Sie eine Anweisung oder einen Anweisungsblock wiederholt ausführen, bis ein bestimmter Ausdruck nach `false` ausgewertet wird. Diese Art von Schleife eignet sich für Iterationen von Arrays und für andere Anwendungen, in denen Sie im Voraus wissen, wie oft die Schleife durchlaufen werden soll.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird der `i`-Wert in die Konsole geschrieben und bei jeder Iteration der Schleife um 1 erhöht.  
  
 [!code-cs[csrefKeywordsIteration#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/for_1.cs)]  
  
 Die `for`-Anweisung im vorherigen Beispiel führt die folgenden Aktionen aus.  
  
1.  Zuerst wird der Anfangswert der Variable `i` festgelegt. Dieser Schritt wird unabhängig davon, wie oft die Schleife wiederholt wird, nur einmal ausgeführt. Sie können sich diese Initialisierung als außerhalb der Schleife erfolgend vorstellen.  
  
2.  Um die Bedingung (`i <= 5`) auszuwerten, wird der Wert `i` mit 5 verglichen.  
  
    -   Wenn `i` ist kleiner als oder gleich 5 ist, wird die Bedingung nach `true` ausgewertet, und die folgenden Aktionen werden ausgeführt.  
  
        1.  In der `Console.WriteLine`-Anweisung im Hauptteil der Schleife wird der `i`-Wert dargestellt.  
  
        2.  Der `i`-Wert wird um 1 inkrementiert.  
  
        3.  Die Schleife kehrt zum Start von Schritt 2 zurück, um die Bedingung erneut auszuwerten.  
  
    -   Wenn `i` größer als 5 ist, wird die Bedingung nach `false` ausgewertet, und Sie beenden die Schleife.  
  
 Beachten Sie, dass wenn der ursprüngliche `i`-Wert größer als 5 ist, wird der Hauptteil der Schleife kein einziges Mal ausgeführt.  
  
 Jede `for`-Anweisung definiert die Abschnitte „Initialisierer“, „Bedingung“ und „Iterator“. Diese Abschnitte bestimmen, wie oft die Schleife in der Regel durchlaufen wird.  
  
```csharp  
for (initializer; condition; iterator)  
    body  
```  
  
 Diese Abschnitte dienen den folgenden Zwecken.  
  
-   Im Initialisiererabschnitt werden die anfänglichen Bedingung festgelegt. Die Anweisungen in diesem Abschnitt werden nur einmal ausgeführt, bevor die Schleife beginnt. Der Abschnitt kann nur eine der beiden folgenden Optionen enthalten.  
  
    -   Die Deklaration und die Initialisierung einer lokalen Schleifenvariablen, wie das erste Beispiel zeigt (`int i = 1`). Die Variable ist in der Schleife lokal; ein Zugriff darauf von außerhalb der Schleife ist nicht möglich.  
  
    -   Null oder mehr Anweisungsausdrücke aus der folgenden Liste, durch Kommas getrennt.  
  
        -   [Zuweisungsanweisung](../../../csharp/language-reference/operators/assignment-operator.md)  
  
        -   Aufruf einer Methode  
  
        -   Präfix- oder Postfix-[Inkrementausdruck](../../../csharp/language-reference/operators/increment-operator.md), z.B. `++i` oder `i++`  
  
        -   Präfix- oder Postfix-[Dekrementausdruck](../../../csharp/language-reference/operators/decrement-operator.md), z.B. `--i` oder `i--`  
  
        -   Erstellung eines Objekts mithilfe von [new](../../../csharp/language-reference/keywords/new-operator.md)  
  
        -   [await](../../../csharp/language-reference/keywords/await.md)-Ausdruck  
  
-   Der Bedingungsabschnitt enthält einen booleschen Ausdruck, der ausgewertet wird, um festzustellen, ob die Schleife beendet oder erneut ausgeführt werden soll.  
  
-   Der Iteratorabschnitt definiert, was nach jeder Iteration des Hauptteils der Schleife geschieht. Der Iteratorabschnitt enthält keine oder mehrere der folgenden Anweisungsausdrücke, durch Kommas getrennt:  
  
    -   [Zuweisungsanweisung](../../../csharp/language-reference/operators/assignment-operator.md)  
  
    -   Aufruf einer Methode  
  
    -   Präfix- oder Postfix-[Inkrementausdruck](../../../csharp/language-reference/operators/increment-operator.md), z.B. `++i` oder `i++`  
  
    -   Präfix- oder Postfix-[Dekrementausdruck](../../../csharp/language-reference/operators/decrement-operator.md), z.B. `--i` oder `i--`  
  
    -   Erstellung eines Objekts mithilfe von [new](../../../csharp/language-reference/keywords/new-operator.md)  
  
    -   [await](../../../csharp/language-reference/keywords/await.md)-Ausdruck  
  
-   Der Hauptteil der Schleife besteht aus einer Anweisung, einer leeren Anweisung oder einem Block von Anweisungen, die Sie erstellen, indem Sie 0 (null) oder mehrere Anweisungen in Klammern einschließen.  
  
     Sie können die Schleife an jedem Punkt im `for`-Block mit dem Schlüsselwort [break](../../../csharp/language-reference/keywords/break.md) unterbrechen oder mit dem Schlüsselwort [continue](../../../csharp/language-reference/keywords/continue.md) direkt zur nächsten Iteration der Schleife springen. Sie können jede beliebige Schleife auch mit einer [goto](../../../csharp/language-reference/keywords/goto.md)-, [return](../../../csharp/language-reference/keywords/return.md)- oder [throw](../../../csharp/language-reference/keywords/throw.md)-Anweisung beenden.  
  
 Im ersten Beispiel in diesem Thema wird die häufigste Art der `for`-Schleife dargestellt, die die folgenden Optionen für die Abschnitte bereitstellt.  
  
-   Der Initialisierer deklariert und initialisiert Sie eine lokale Schleifenvariable, `i`, die die Iterationen der Schleife mitzählt.  
  
-   Die Bedingung überprüft den Wert der Schleifenvariablen gegen einen bekannten endgültigen Wert, 5.  
  
-   Der Iterator verwendet eine Postfix-Inkrementanweisung, `i++`, um den Zählerstand jeder Schleife festzuhalten.  
  
 Das folgende Beispiel veranschaulicht mehrere weniger gängige Optionen: das Zuweisen eines Werts zu einer externen Schleifenvariablen im Initialisierer, das Aufrufen der `Console.WriteLine`-Methode im Initialisierer und im Iterator und das Ändern die Werte von zwei Variablen im Iterator.  
  
 [!code-cs[csrefKeywordsIteration#8](../../../csharp/language-reference/keywords/codesnippet/CSharp/for_2.cs)]  
  
 Alle Ausdrücke, die eine `for`-Anweisung definieren, sind optional. Die folgende Anweisung erstellt z.B. eine Endlosschleife.  
  
 [!code-cs[csrefKeywordsIteration#3](../../../csharp/language-reference/keywords/codesnippet/CSharp/for_3.cs)]  
  
## <a name="c-language-specification"></a>C#-Programmiersprachenspezifikation  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [C#-Referenz](../../../csharp/language-reference/index.md)   
 [C#-Programmierhandbuch](../../../csharp/programming-guide/index.md)   
 [C#-Schlüsselwörter](../../../csharp/language-reference/keywords/index.md)   
 [foreach, in](../../../csharp/language-reference/keywords/foreach-in.md)   
 [for-Anweisung (C++)](/cpp/cpp/for-statement-cpp)   
 [Iterationsanweisungen](../../../csharp/language-reference/keywords/iteration-statements.md)

