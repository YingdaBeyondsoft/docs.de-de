---
title: '@ (C#-Referenz)'
ms.date: 2017-02-09
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- '@_CSharpKeyword'
- '@'
dev_langs:
- CSharp
helpviewer_keywords:
- '@ special character [C#]'
- '@ language element [C#]'
ms.assetid: 89bc7e53-85f5-478a-866d-1cca003c4e8c
author: rpetrusha
ms.author: ronpet
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
ms.openlocfilehash: 08e3da6aaeee037d7272ea8cddc4382a436b683b
ms.contentlocale: de-de
ms.lasthandoff: 07/28/2017

---
# <a name="-c-reference"></a>@ (C#-Referenz)

Das Sonderzeichen `@` dient als ausführlicher Bezeichner. Er wird wie folgt verwendet:

1. Zum Aktivieren von C#-Schlüsselwörtern, die als Bezeichner verwendet werden sollen. Das Zeichen `@` steht vor einem Codeelement, das der Compiler als Bezeichner und nicht als C#-Schlüsselwort interpretieren soll. Im folgenden Beispiel wird das Zeichen `@` zum Definieren eines Bezeichners mit dem Namen `for` verwendet, der in einer `for`-Schleife verwendet wird.

   [!code-cs[verbatim1](../../../../samples/snippets/csharp/language-reference/keywords/verbatim1.cs#1)]

1. Zum Angeben, dass ein Zeichenfolgenliteral wörtlich interpretiert werden soll. Das Zeichen `@` in dieser Instanz definiert ein *ausführliches Zeichenfolgenliteral*. Einfache Escapesequenzen (z.B. `"\\"` für einen umgekehrten Schrägstrich), Escapesequenzen für Hexadezimalzahlen (z.B. `"\x0041"` für ein groß geschriebenes A) und Escapesequenzen für Unicodezeichen (wie z.B. `"\u0041"` für ein groß geschriebenes A) werden wörtlich interpretiert. Nur eine Escapesequenz für Anführungszeichen (`""`) wird nicht wörtlich interpretiert; es wird ein einfaches Anführungszeichen generiert. Im folgenden Beispiel werden zwei identische Dateipfade definiert – einer durch Verwendung eines regulären Zeichenfolgenliterals und der andere durch ein ausführliches Zeichenfolgenliteral. Dies ist einer der häufigeren Verwendungsarten von ausführlichen Zeichenfolgenliteralen.

   [!code-cs[verbatim2](../../../../samples/snippets/csharp/language-reference/keywords/verbatim1.cs#2)]

   Im folgenden Beispiel werden die Auswirkungen des Definierens eines regulären Zeichenfolgenliterals und eines ausführlichen Zeichenfolgenliterals mit identischen Zeichensequenzen dargestellt.

   [!code-cs[verbatim3](../../../../samples/snippets/csharp/language-reference/keywords/verbatim1.cs#3)]

1. Zum Zulassen, dass der Compiler im Fall eines Namenskonflikts zwischen Attributen unterscheiden kann. Ein Attribut ist ein von @System.Attribute abgeleiteter Typ. Der Name des Typs enthält normalerweise das Suffix **Attribute**, obwohl der Compiler diese Konvention nicht erzwingt. Auf das Attribut kann dann im Code entweder über den vollständigen Typnamen (z.B. `[InfoAttribute]`) oder über den gekürzten Namen (z.B. `[Info]`) verwiesen werden. Allerdings tritt ein Namenskonflikt auf, wenn zwei gekürzte Typnamen des Attributs identisch sind und ein Typname das Suffix **Attribute** enthält, der andere jedoch nicht. Der folgende Code kann z.B. nicht kompiliert werden, da der Compiler nicht bestimmen kann, ob das Attribut `Info` oder `InfoAttribute` auf die Methode `Main` angewendet wird.

   ```csharp
   using System;

   [AttributeUsage(AttributeTargets.Class)]
   public class Info : Attribute
   {
      private string information;
      
      public Info(string info)
      {
          information = info;
      }
   }

   [AttributeUsage(AttributeTargets.Method)]
   public class InfoAttribute : Attribute
   {
      private string information;
      
      public InfoAttribute(string info)
      {
          information = info;
      }
   }

   [Info("A simple executable.")]
   public class Example
   {
      [InfoAttribute("The entry point.")]
      public static void Main()
      {
      }
   }
   ```  

   Wenn der ausführliche Bezeichner zum Identifizieren des Attributs `Info` verwendet wird, kann das Beispiel erfolgreich kompiliert werden.

   [!code-cs[verbatim4](../../../../samples/snippets/csharp/language-reference/keywords/verbatim4.cs#1)]

## <a name="see-also"></a>Siehe auch  
 [C#-Referenz](../../../csharp/language-reference/index.md)   
 [C#-Programmierhandbuch](../../../csharp/programming-guide/index.md)   
 [C# Special Characters (C#-Sonderzeichen)](../../../csharp/language-reference/tokens/index.md)

