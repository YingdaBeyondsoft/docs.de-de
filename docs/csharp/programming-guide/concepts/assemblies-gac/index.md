---
title: Assemblys und der globale Assemblycache (C#)
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 149f5ca5-5b34-4746-9542-1ae43b2d0256
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 2b98bd872bfdcbebb34fff3d878b92f39e27bbe0
ms.contentlocale: de-de
ms.lasthandoff: 07/28/2017

---
# <a name="assemblies-and-the-global-assembly-cache-c"></a>Assemblys und der globale Assemblycache (C#)
Assemblys bilden die Grundlage für die Bereitstellung, die Versionskontrolle, die Wiederverwendung, die Festlegung des Aktivierungsumfangs und die Sicherheitsberechtigungen für eine .NET-basierte Anwendung. Assemblys sind ausführbare Dateien (EXE-Dateien) oder DLL-Dateien und bilden die Bausteine von .NET Framework. Sie stellen der Common Language Runtime die Informationen zur Verfügung, die sie zum Erkennen der Typimplementierungen benötigt. Sie können sich eine Assembly als Sammlung von Typen und Ressourcen vorstellen, die eine logische Funktionalitätseinheit bilden und zusammenarbeiten.  
  
 Assemblys können mindestens ein Modul enthalten. Beispiel: Größere Projekte können so geplant werden, dass verschiedene unabhängige Entwickler an verschiedenen Modulen arbeiten, die schließlich alle zusammen eine einzelne Assembly erstellen. Weitere Informationen zu Modulen finden Sie im Thema [Gewusst wie: Erstellen einer Mehrfachdateiassembly](https://msdn.microsoft.com/library/226t7yxe).  
  
 Assemblys verfügen über folgende Eigenschaften:  
  
-   Assemblys werden als EXE- oder DLL-Dateien implementiert.  
  
-   Sie können eine Assembly zwischen Anwendungen teilen, indem Sie sie im globalen Assemblycache ablegen. Assemblys müssen über einen starken Namen verfügen, bevor sie dem globalen Assemblycache hinzugefügt werden können. Weitere Informationen finden Sie unter [Assemblys mit starkem Namen](https://msdn.microsoft.com/library/wd40t7ad).  
  
-   Assemblys werden nur in den Arbeitsspeicher geladen, wenn sie erforderlich sind. Wenn sie nicht verwendet werden, werden sie nicht geladen. Dies bedeutet, dass Assemblys eine effiziente Möglichkeit zur Verwaltung von Ressourcen in größeren Projekten sein können.  
  
-   Sie können mithilfe der Reflektion programmgesteuert Informationen zu einer Assembly abrufen. Weitere Informationen finden Sie unter [Reflection (C#) (Reflexion (C#))](../../../../csharp/programming-guide/concepts/reflection.md).  
  
-   Wenn Sie eine Assembly nur zu Überprüfungszwecken laden möchten, verwenden Sie eine Methode wie z. B. <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A>.  
  
## <a name="assembly-manifest"></a>Assemblymanifest  
 Jede Assembly enthält ein *Assemblymanifest*. Ähnlich wie ein Inhaltsverzeichnis enthält das Assemblymanifest Folgendes:  
  
-   Die Identität der Assembly (Name und Version).  
  
-   Eine Dateitabelle, die alle anderen Dateien beschreibt, aus denen die Assembly besteht, z.B. alle weiteren Assemblys, die Sie erstellt haben, auf denen Ihre EXE- oder DLL-Datei basiert, oder sogar Bitmap- oder Infodateien.  
  
-   Eine *Assemblyverweisliste*, eine Liste aller externen Abhängigkeiten, z.B. DLL-Dateien oder andere Dateien, die Ihre Anwendung benötigt, die möglicherweise von einer anderen Person erstellt wurden. Assemblyverweise enthalten Verweise auf globale und private Objekte. Globale Objekte befinden sich im globalen Assemblycache, einem Bereich, der auch anderen Anwendungen zur Verfügung steht. Private Objekte müssen sich in einem Verzeichnis auf derselben Ebene oder unterhalb des Verzeichnisses befinden, in dem die Anwendung installiert ist.  
  
 Da Assemblys Informationen zu Inhalt, Versionsverwaltung und Abhängigkeiten enthalten, sind die Anwendungen, die Sie mit C# erstellen, nicht von Windows-Registrierungswerten abhängig, damit sie ordnungsgemäß funktionieren. Assemblys reduzieren DLL-Konflikte, verbessern die Zuverlässigkeit und vereinfachen die Bereitstellung Ihrer Anwendungen. In vielen Fällen können Sie eine .NET-basierte Anwendung einfach durch Kopieren der Dateien auf den Zielcomputer installieren.  
  
 Weitere Informationen dazu finden Sie unter [Assemblymanifest](https://msdn.microsoft.com/library/1w45z383).  
  
## <a name="adding-a-reference-to-an-assembly"></a>Hinzufügen eines Verweises auf eine Assembly  
 Um eine Assembly zu verwenden, müssen Sie einen Verweis darauf hinzufügen. Als Nächstes verwenden Sie [using directive (die Using-Direktive)](../../../../csharp/language-reference/keywords/using-directive.md), um den Namespace der Elemente zu wählen, die Sie verwenden möchten. Sobald auf eine Assembly verwiesen wird und sie importiert wird, sind alle zugänglichen Klassen, Eigenschaften, Methoden und anderen Member ihrer Namespaces für Ihre Anwendung verfügbar, als wäre ihr Code Teil der Quelldatei.  
  
 In C# können Sie auch zwei Versionen derselben Assembly in einer einzigen Anwendung verwenden. Weitere Informationen finden Sie unter [extern-Alias](../../../../csharp/language-reference/keywords/extern-alias.md).  
  
## <a name="creating-an-assembly"></a>Erstellen einer Assembly  
 Kompilieren Sie Ihre Anwendung, indem Sie **Build** im **Build**-Menü anklicken, oder indem Sie sie durch eine Befehlszeile mithilfe des Befehlszeilencompilers erstellen. Weitere Informationen zum Erstellen von Assemblys über die Befehlszeile finden Sie unter [Command-line Building With csc.exe (Erstellen von Befehlszeilen mit „csc.exe“)](../../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).  
  
> [!NOTE]
>  Sie erstellen eine Assembly in Visual Studio, indem Sie im Menü **Build** die Option **Build** wählen.  
  
## <a name="see-also"></a>Siehe auch  
 [C#-Programmierhandbuch](../../../../csharp/programming-guide/index.md)   
 [Assemblys in der Common Language Runtime (CLR)](https://msdn.microsoft.com/library/k3677y81)   
 [Friend-Assemblys (C#)](friend-assemblies.md)   
 [How to: Share an Assembly with Other Applications (C#) (Vorgehensweise: Freigeben einer Assembly für andere Anwendungen (C#))](how-to-share-an-assembly-with-other-applications.md)   
 [How to: Load and Unload Assemblies (C#) (Vorgehensweise: Laden und Entladen von Assemblys (C#))](how-to-load-and-unload-assemblies.md)   
 [How to: Determine If a File Is an Assembly (C#) (Vorgehensweise: Bestimmen, ob eine Datei eine Assembly ist (C#))](how-to-determine-if-a-file-is-an-assembly.md)   
 [How to: Create and Use Assemblies Using the Command Line (C#) (Vorgehensweise: Erstellen und Verwenden von Assemblys über die Befehlszeile (C#))](how-to-create-and-use-assemblies-using-the-command-line.md)   
 [Exemplarische Vorgehensweise: Einbetten von Typen aus verwalteten Assemblys in Visual Studio (C#)](walkthrough-embedding-types-from-managed-assemblies-in-visual-studio.md)   
 [Walkthrough: Embedding Type Information from Microsoft Office Assemblies in Visual Studio (C#) (Exemplarische Vorgehensweise: Einbetten von Typinformationen aus Microsoft Office-Assemblys in Visual Studio (C#))](walkthrough-embedding-type-information-from-microsoft-office-assemblies.md)

