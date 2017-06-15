---
title: "Ngen.exe (Native Image Generator) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "Native Image Generator"
  - "images [.NET Framework], native"
  - "side-by-side execution, native images"
  - "assemblies [.NET Framework], native image"
  - "Ngen.exe"
  - "native image generation"
  - "native image cache"
  - "publisher policy applied for native images"
  - "invalid images"
ms.assetid: 44bf97aa-a9a4-4eba-9a0d-cfaa6fc53a66
caps.latest.revision: 57
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 52
---
# Ngen.exe (Native Image Generator)
Native Image Generator \(Ngen.exe\) ist ein Tool zur Leistungsoptimierung verwalteter Anwendungen.  Mit "Ngen.exe" können Sie systemeigene Images erstellen, also Dateien mit kompiliertem prozessorspezifischem Computercode, die daraufhin im Cache für systemeigene Images auf dem lokalen Computer installiert werden.  Die Laufzeit kann systemeigene Abbilder aus dem Cache nutzen und muss nicht den JIT \(Just\-In\-Time\)\-Compiler verwenden, um die ursprüngliche Assembly zu kompilieren.  
  
 Änderungen an "Ngen.exe" in [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)]:  
  
-   Mit "Ngen.exe"können nun Assemblys mit vollständiger Vertrauenswürdigkeit kompiliert werden, und die Codezugriffssicherheitsrichtlinie \(CAS\) wird nicht mehr ausgewertet.  
  
-   Systemeigene Images, die mit "Ngen.exe" generiert werden, können nicht mehr in Anwendungen geladen werden, die mit partieller Vertrauenswürdigkeit ausgeführt werden.  
  
 Änderungen an "Ngen.exe" in .NET Framework Version 2.0:  
  
-   Mit der Installation einer Assembly werden auch ihre Abhängigkeiten installiert, und die Syntax von "Ngen.exe" wird vereinfacht.  
  
-   Systemeigene Images können jetzt für mehrere Anwendungsdomänen verwendet werden.  
  
-   Die neue Aktion `update` erstellt ungültig gewordene Images neu.  
  
-   Sie können Aktionen verzögern und von einem Dienst ausführen lassen, der die Leerlaufzeiten auf dem Computer nutzt, um Images zu generieren und zu installieren.  
  
-   Einige Ursachen für die Ungültigkeit von Images wurden eliminiert.  
  
 Unter Windows 8 finden Sie weitere Informationen unter [Native Image Task](http://msdn.microsoft.com/de-de/9b1f7590-4e0d-4737-90ef-eaf696932afb).  
  
 Weitere Informationen zur Verwendung von "Ngen.exe" und des Diensts für systemeigene Images finden Sie unter [Native Image Service](http://msdn.microsoft.com/de-de/b15e0e32-59cb-4ae4-967c-6c9527781309).  
  
> [!NOTE]
>  Die Syntax von "Ngen.exe" für die Versionen 1.0 und 1.1 von .NET Framework finden Sie unter [Native Image Generator \(Ngen.exe\) Legacy Syntax](http://msdn.microsoft.com/de-de/5a69fc7a-103f-4afc-8ab4-606adcb46324).  
  
 Dieses Tool wird automatisch mit Visual Studio installiert.  Zum Ausführen des Tools verwenden Sie die Developer\-Eingabeaufforderung \(oder die Visual Studio\-Eingabeaufforderung in Windows 7\).  Weitere Informationen finden Sie unter [Eingabeaufforderungen](../../../docs/framework/tools/developer-command-prompt-for-vs.md).  
  
 Geben Sie an der Eingabeaufforderung Folgendes ein:  
  
## Syntax  
  
```  
  
        ngen action [options]  
ngen /? | /help  
```  
  
## Vorgänge  
 In der folgenden Tabelle wird die Syntax für jede einzelne `action` dargestellt.  Beschreibungen der einzelnen Teile einer `action` finden Sie in den Tabellen [Argumente](#ArgumentTable), [Prioritätsebenen](#PriorityTable), [Szenarien](#ScenarioTable) und [Konfigurationen](#ConfigTable).  In der Tabelle [Optionen](#OptionTable) werden die `options` und die Hilfeschalter beschrieben.  
  
|Aktion|Beschreibung|  
|------------|------------------|  
|`install` \[`assemblyName` &#124; `assemblyPath`\] \[`scenarios`\] \[`config`\] \[`/queue`\[`:`{`1`&#124;`2`&#124;`3`}\]\]|Generiert systemeigene Images für eine Assembly und ihre Abhängigkeiten und installiert die Images im Cache für systemeigene Images.<br /><br /> Wenn `/queue` angegeben wird, wird die Aktion in die Warteschlange des Diensts für systemeigene Images gestellt.  Die Standardpriorität ist 3.  Informationen hierzu finden Sie in der Tabelle [Prioritätsebenen](#PriorityTable).|  
|`uninstall` \[`assemblyName` &#124; `assemblyPath`\] \[`scenarios`\] \[`config`\]|Löscht die systemeigenen Images einer Assembly und ihre Abhängigkeiten aus dem Cache für systemeigene Images.<br /><br /> Verwenden Sie zum Deinstallieren eines einzelnen Images und seiner Abhängigkeiten dieselben Befehlszeilenargumente wie beim Installieren des Images. **Note:**  In [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] wird die Aktion `uninstall` \* nicht mehr unterstützt.|  
|`update` \[`/queue`\]|Aktualisiert systemeigene Images, die ungültig geworden sind.<br /><br /> Wenn `/queue` angegeben wird, werden die Aktualisierungen in die Warteschlange des Diensts für systemeigene Images gestellt.  Aktualisierungen werden immer mit Priorität 3 geplant, sodass sie zu Leerlaufzeiten des Computers ausgeführt werden.|  
|`display` \[`assemblyName` &#124; `assemblyPath`\]|Zeigt den Zustand der systemeigenen Images für eine Assembly und ihre Abhängigkeiten an.<br /><br /> Wenn kein Argument angegeben wird, wird der gesamte Inhalt des Caches für systemeigene Images angezeigt.|  
|`executeQueuedItems` \[`1` `&#124;`  `2`  `&#124;` `3`\]<br /><br /> \- oder \-<br /><br /> `eqi` \[1&#124;2&#124;3\]|Führt die in der Warteschlange enthaltenen Kompilierungsaufträge aus.<br /><br /> Wenn eine Priorität angegeben wird, werden Kompilierungsaufträge mit höherer oder gleicher Priorität ausgeführt.  Wenn keine Priorität angegeben wird, werden alle in die Warteschlange gestellten Kompilierungsaufträge ausgeführt.|  
|`queue` {`pause` &#124; `continue` &#124; `status`}|Hält den Dienst für systemeigene Images an, setzt den angehaltenen Dienst fort bzw. fragt den Dienststatus ab.|  
  
<a name="ArgumentTable"></a>   
## Argumente  
  
|Argument|Beschreibung|  
|--------------|------------------|  
|`assemblyName`|Der vollständige Anzeigename der Assembly.  Beispielsweise `"myAssembly, Version=2.0.0.0, Culture=neutral, PublicKeyToken=0038abc9deabfle5"`. **Note:**  Sie können einen partiellen Assemblynamen wie `myAssembly` für die `display`\-Aktion und die `uninstall`\-Aktion angeben. <br /><br /> In jeder Befehlszeile von "Ngen.exe" kann nur eine Assembly angegeben werden.|  
|`assemblyPath`|Der explizite Pfad der Assembly.  Sie können einen vollständigen oder einen relativen Pfad angeben.<br /><br /> Wenn Sie einen Dateinamen ohne Pfad angeben, muss sich die Assembly im aktuellen Verzeichnis befinden.<br /><br /> In jeder Befehlszeile von "Ngen.exe" kann nur eine Assembly angegeben werden.|  
  
<a name="PriorityTable"></a>   
## Prioritätsebenen  
  
|Priorität|Beschreibung|  
|---------------|------------------|  
|`1`|Systemeigene Images werden sofort generiert und installiert, ohne dass auf Leerlaufzeit gewartet wird.|  
|`2`|Systemeigene Images werden ohne Warten auf Leerlaufzeit generiert und installiert, aber nachdem alle Aktionen mit Priorität 1 \(und ihre Abhängigkeiten\) abgeschlossen wurden.|  
|`3`|Systemeigene Images werden installiert, wenn der Dienst für systemeigene Images feststellt, dass sich der Computer im Leerlauf befindet.  Weitere Informationen finden Sie unter [Native Image Service](http://msdn.microsoft.com/de-de/b15e0e32-59cb-4ae4-967c-6c9527781309).|  
  
<a name="ScenarioTable"></a>   
## Szenarien  
  
|Szenario|Beschreibung|  
|--------------|------------------|  
|`/Debug`|Generiert systemeigene Images, die unter einem Debugger verwendet werden können.|  
|`/Profile`|Generiert systemeigene Images, die unter einem Profiler verwendet werden können.|  
|`/NoDependencies`|Generiert die Mindestanzahl systemeigener Images, die von den angegebenen Einsatzszenarien benötigt werden.|  
  
<a name="ConfigTable"></a>   
## Konfigurationen  
  
|Konfiguration|Beschreibung|  
|-------------------|------------------|  
|`/ExeConfig:` `exePath`|Verwendet die Konfiguration der angegebenen ausführbaren Assembly.<br /><br /> "Ngen.exe" muss beim Binden an Abhängigkeiten die gleichen Entscheidungen wie das Ladeprogramm treffen.  Wenn eine freigegebene Komponente zur Laufzeit mit der <xref:System.Reflection.Assembly.Load%2A>\-Methode geladen wird, bestimmt die Konfigurationsdatei der Anwendung die Abhängigkeiten, die für die freigegebene Komponente geladen werden, beispielsweise die Version einer zu ladenden Abhängigkeit.  Über den Schalter `/ExeConfig` erhält "Ngen.exe" Anweisungen dazu, welche Abhängigkeiten zur Laufzeit geladen werden.|  
|`/AppBase:` `directoryPath`|Verwendet das angegebene Verzeichnis beim Suchen nach Abhängigkeiten als Anwendungsbasis.|  
  
<a name="OptionTable"></a>   
## Optionen  
  
|Option|Beschreibung|  
|------------|------------------|  
|`/nologo`|Unterdrückt die Anzeige des Startbanners von Microsoft.|  
|`/silent`|Unterdrückt die Anzeige von Erfolgsmeldungen.|  
|`/verbose`|Zeigt ausführliche Informationen zum Debuggen an. **Note:**  Aufgrund von Beschränkungen im Betriebssystem werden in Windows 98 und Windows Millennium Edition durch diese Option nicht so viele zusätzliche Informationen angezeigt.|  
|`/help`, `/?`|Zeigt die Befehlssyntax sowie Optionen für die aktuelle Version an.|  
  
## Hinweise  
 Zum Ausführen von "Ngen.exe" müssen Sie über Administratorrechte verfügen.  
  
> [!CAUTION]
>  Führen Sie "Ngen.exe" nicht für Assemblys aus, die nicht vollständig vertrauenswürdig sind.  Ab [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] werden von "Ngen.exe" Assemblys mit vollständiger Vertrauenswürdigkeit kompiliert, und die Codezugriffssicherheitsrichtlinie \(CAS\) wird nicht mehr ausgewertet.  
  
 Ab [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] können die systemeigenen Images, die mit "Ngen.exe" generiert werden, nicht mehr in Anwendungen geladen werden, die mit partieller Vertrauenswürdigkeit ausgeführt werden.  Stattdessen wird der Just\-In\-Time \(JIT\)\-Compiler aufgerufen.  
  
 Mit "Ngen.exe" werden systemeigene Images für die angegebene Assembly und alle ihre Abhängigkeiten generiert.  Abhängigkeiten werden anhand von Verweisen im Assemblymanifest bestimmt.  Eine Abhängigkeit müssen Sie nur in einem Szenario separat installieren, in dem die Abhängigkeit von der Anwendung mittels Reflektion geladen wird, z. B. durch Aufrufen der <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName>\-Methode.  
  
> [!IMPORTANT]
>  Verwenden Sie die <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=fullName>\-Methode nicht für systemeigene Images.  Ein mit dieser Methode geladenes Image kann nicht von anderen Assemblys im Ausführungskontext verwendet werden.  
  
 Ngen.exe erfasst die Anzahl von Abhängigkeiten.  Angenommen, `MyAssembly.exe` und `YourAssembly.exe` sind im Cache für systemeigene Images installiert, und beide verfügen über Verweise auf `OurDependency.dll`.  Wenn `MyAssembly.exe` deinstalliert wird, wird `OurDependency.dll` nicht deinstalliert.  Die Deinstallation erfolgt erst, wenn auch `YourAssembly.exe` deinstalliert wird.  
  
 Wenn Sie ein systemeigenes Image für eine Assembly im globalen Assemblycache generieren, geben Sie deren Anzeigenamen an.  Siehe <xref:System.Reflection.Assembly.FullName%2A?displayProperty=fullName>.  
  
 Die mit Ngen.exe generierten systemeigenen Images können für andere Anwendungsdomänen freigegeben werden.  Dies bedeutet, dass "Ngen.exe" in Anwendungsszenarien verwendet werden kann, in denen Assemblys von mehreren Anwendungsdomänen gemeinsam genutzt werden müssen.  So geben Sie Domänenneutralität an:  
  
-   Wenden Sie das <xref:System.LoaderOptimizationAttribute>\-Attribut auf die Anwendung an.  
  
-   Legen Sie die <xref:System.AppDomainSetup.LoaderOptimization%2A?displayProperty=fullName>\-Eigenschaft fest, wenn Sie Setupinformationen für eine neue Anwendungsdomäne erstellen.  
  
 Verwenden Sie immer domänenneutralen Code, wenn Sie dieselbe Assembly in mehrere Anwendungsdomänen laden.  Wenn ein systemeigenes Image in eine nicht gemeinsam genutzte Anwendungsdomäne geladen wird, nachdem es in eine gemeinsam genutzte Domäne geladen wurde, kann es nicht verwendet werden.  
  
> [!NOTE]
>  Domänenneutraler Code kann nicht entladen werden, und die Leistung ist möglicherweise etwas vermindert, insbesondere beim Zugriff auf statische Member.  
  
## Generieren von Images für verschiedene Szenarien  
 Nachdem Sie ein systemeigenes Image für eine Assembly generiert haben, wird dieses bei jedem Ausführen der Assembly automatisch von der Laufzeit gesucht und verwendet.  Je nach Anwendungsszenario können mehrere Images generiert werden.  
  
 Wenn Sie beispielsweise eine Assembly in einem Debugging\- oder Profilerstellungsszenario ausführen, sucht die Laufzeit nach einem systemeigenen Image, das mit der Option `/Debug` bzw. `/Profile` generiert wurde.  Wenn kein entsprechendes systemeigenes Image gefunden wurde, wird die Laufzeit auf die standardmäßige JIT\-Kompilierung zurückgesetzt.  Die einzige Möglichkeit zum Debuggen systemeigener Images besteht darin, ein systemeigenes Image mit der Option `/Debug` zu erstellen.  
  
 Die Aktion `uninstall` erkennt auch Szenarien, sodass Sie alle oder nur ausgewählte Szenarien deinstallieren können.  
  
## Wann sollten systemeigene Images verwendet werden?  
 Systemeigene Images bieten Leistungsverbesserungen in zwei Bereichen: verbesserte Arbeitsspeichernutzung und beschleunigte Startzeit.  
  
> [!NOTE]
>  Die Leistung systemeigener Images hängt von einer Reihe von Faktoren ab, die die Leistungsanalyse erschweren. Dazu gehören Code\- und Datenzugriffsmuster, die Anzahl der über Modulgrenzen hinweg ausgeführten Aufrufe und die Anzahl der bereits von anderen Anwendungen geladenen Abhängigkeiten.  Die einzige Möglichkeit, einen eventuellen Nutzen systemeigener Images für Ihre Anwendung zu erkennen, besteht darin, gründliche Leistungsmessungen in den wichtigsten Bereitstellungsszenarien vorzunehmen.  
  
### Verbesserte Arbeitsspeichernutzung  
 Systemeigene Images können die Arbeitsspeichernutzung entscheidend verbessern, wenn Code zwischen Prozessen freigegeben wird.  Systemeigene Images werden in Form von Windows PE\-Dateien gespeichert. Eine einzelne Version einer DLL\-Datei kann also von mehreren Prozessen gemeinsam genutzt werden. Vom JIT\-Compiler erstellter systemeigener Code wird dagegen im privaten Speicher abgelegt und kann nicht freigegeben werden.  
  
 Unter Terminaldiensten ausgeführte Anwendungen können ebenfalls von freigegebenen Codepages profitieren.  
  
 Wenn der JIT\-Compiler nicht geladen wird, wird außerdem pro Anwendungsinstanz eine feste Speichergröße eingespart.  
  
### Schnellerer Anwendungsstart  
 Durch das Vorkompilieren von Assemblys mit Ngen.exe kann die Startzeit einiger Anwendungen beschleunigt werden.  Zeit lässt sich im Allgemeinen dadurch gewinnen, dass Anwendungen Komponentenassemblys gemeinsam nutzen, denn nachdem die erste Anwendung gestartet wurde, sind die freigegebenen Komponenten für nachfolgende Anwendungen bereits geladen.  Bei einem Kaltstart, bei dem alle Assemblys einer Anwendung von der Festplatte geladen werden müssen, fällt der Nutzen systemeigener Images geringer aus, da die Zeit für den Zugriff auf die Festplatte den Zeitgewinn wieder aufhebt.  
  
 Die feste Bindung kann die Startzeit verlangsamen, da alle Images, die eine feste Bindung an die Hauptassembly der Anwendung aufweisen, gleichzeitig geladen werden müssen.  
  
> [!NOTE]
>  Vor [!INCLUDE[net_v35SP1_long](../../../includes/net-v35sp1-long-md.md)] sollten Sie freigegebene, mit starken Bezeichnungen benannte Komponenten in den globalen Assemblycache einschließen, da das Ladeprogramm für Assemblys mit starkem Namen, die nicht im globalen Assemblycache enthalten sind, eine zusätzliche Überprüfung ausführt. Dadurch wird jegliche Beschleunigung der Startzeit aufgrund der Verwendung systemeigener Images wieder zunichte gemacht.  Aufgrund von Optimierungen, die in [!INCLUDE[net_v35SP1_short](../../../includes/net-v35sp1-short-md.md)] eingeführt wurden, wurden zusätzliche Überprüfungen überflüssig.  
  
### Wichtigkeit der Basisadressen von Assemblys  
 Da es sich bei systemeigenen Images um Windows PE\-Dateien handelt, unterliegen sie im Hinblick auf die Zurücksetzung denselben Voraussetzungen wie andere ausführbare Dateien.  Die Leistungseinbußen infolge der Umsetzung treten bei der festen Bindung sogar noch stärker hervor.  
  
 Verwenden Sie die geeignete Compileroption zum Festlegen der Basisadresse für die Assembly, um die Basisadresse für ein systemeigenes Image anzugeben.  Von "Ngen.exe" wird diese Basisadresse für das systemeigene Image verwendet.  
  
> [!NOTE]
>  Systemeigene Images sind größer als die verwalteten Assemblys, aus denen sie erstellt wurden.  Basisadressen müssen unter Berücksichtigung dieses Größenunterschieds berechnet werden.  
  
 Mit einem Tool wie "dumpbin.exe" können Sie die bevorzugte Basisadresse eines systemeigenen Images anzeigen.  
  
### Zusammenfassung der Überlegungen zur Verwendung  
 Anhand der folgenden allgemeinen und anwendungsspezifischen Überlegungen können Sie feststellen, ob es sich lohnt, systemeigene Images für die Anwendung auszuwerten:  
  
-   Systemeigene Images werden schneller geladen als MSIL, da dafür zahlreiche Startaktivitäten, z. B. JIT\-Kompilierung und Überprüfungen der Typsicherheit, nicht mehr notwendig sind.  
  
-   Systemeigene Images erfordern kleinere anfängliche Workingsets, da der JIT\-Compiler nicht benötigt wird.  
  
-   Systemeigene Images ermöglichen die gemeinsame Codenutzung durch Prozesse.  
  
-   Für systemeigene Images wird mehr Festplattenspeicher als für MSIL\-Assemblys benötigt, und für ihre Generierung ist möglicherweise wesentlich mehr Zeit erforderlich.  
  
-   Systemeigene Images müssen verwaltet werden.  
  
    -   Images müssen neu generiert werden, wenn die ursprüngliche Assembly oder eine ihrer Abhängigkeiten gewartet wird.  
  
    -   Für eine einzelne Assembly sind möglicherweise mehrere systemeigene Images zur Verwendung in verschiedenen Anwendungen oder verschiedenen Szenarien erforderlich.  Beispielsweise können die Konfigurationsinformationen in zwei Anwendungen zu unterschiedlichen Bindungsentscheidungen für dieselbe abhängige Assembly führen.  
  
    -   Systemeigene Images müssen von einem Administrator generiert werden, d. h. ausgehend von einem Windows\-Konto der Administratorgruppe.  
  
 Zusätzlich zu diesen allgemeinen Überlegungen muss bei der Frage, ob systemeigene Images einen Leistungsgewinn bringen, auch die Art der Anwendung berücksichtigt werden:  
  
-   Wenn die Anwendung in einer Umgebung ausgeführt wird, in der zahlreiche freigegebene Komponenten verwendet werden, können die Komponenten bei Verwendung systemeigener Images von mehreren Prozessen gemeinsam genutzt werden.  
  
-   Wenn die Anwendung mehrere Anwendungsdomänen verwendet, ermöglichen systemeigene Images die gemeinsame Nutzung von Codepages zwischen Domänen.  
  
    > [!NOTE]
    >  In .NET Framework Version 1.0 und 1.1 können systemeigene Images nicht zwischen Anwendungsdomänen freigegeben werden.  Dies trifft auf Version 2.0 oder höher nicht zu.  
  
-   Wenn die Anwendung unter Terminalserver ausgeführt wird, lassen systemeigene Images die Freigabe von Codepages zu.  
  
-   Bei umfangreicheren Anwendungen ist die Kompilierung in systemeigene Images normalerweise von Vorteil;  bei kleineren Anwendungen dagegen nicht.  
  
-   Bei Anwendungen mit langer Laufzeit weist die JIT\-Kompilierung zur Laufzeit eine etwas bessere Leistung als systemeigene Images auf.  \(Die feste Bindung kann diesen Leistungsunterschied in gewissem Umfang abschwächen.\)  
  
## Feste Bindung  
 Die feste Bindung erhöht den Durchsatz und reduziert die Größe des Workingsets für systemeigene Images.  Der Nachteil der festen Bindung besteht darin, dass sämtliche Images mit fester Bindung an eine Assembly beim Laden der Assembly ebenfalls geladen werden müssen.  Dies kann die Startzeit bei umfangreichen Anwendungen deutlich verlängern.  
  
 Die feste Bindung eignet sich für Abhängigkeiten, die in allen leistungskritischen Szenarien der Anwendung geladen werden.  Wie bereits bei anderen Verwendungsmöglichkeiten systemeigener Images stellen sorgfältige Leistungsmessungen auch hier den einzigen Indikator dafür dar, ob die Anwendungsleistung durch feste Bindung verbessert wird.  
  
 Über das <xref:System.Runtime.CompilerServices.DependencyAttribute>\-Attribut und das <xref:System.Runtime.CompilerServices.DefaultDependencyAttribute>\-Attribut können Sie "Ngen.exe" Hinweise zur Verwendung der festen Bindung übermitteln.  
  
> [!NOTE]
>  Diese Attribute stellen Hinweise und keine Befehle für Ngen.exe dar.  Die Verwendung der festen Bindung kann durch diese Hinweise nicht garantiert werden.  Die Bedeutung dieser Attribute kann sich in zukünftigen Versionen ändern.  
  
### Angeben eines Bindungshinweises für eine Abhängigkeit  
 Wenden Sie <xref:System.Runtime.CompilerServices.DependencyAttribute> auf eine Assembly an, um die Wahrscheinlichkeit anzugeben, dass eine angegebene Abhängigkeit geladen wird.  <xref:System.Runtime.CompilerServices.LoadHint?displayProperty=fullName> gibt an, dass harte Bindung angemessen ist, <xref:System.Runtime.CompilerServices.LoadHint> gibt an, dass der Standard für die Abhängigkeit verwendet werden soll, und <xref:System.Runtime.CompilerServices.LoadHint> gibt an, dass harte Bindung nicht angemessen ist.  
  
 Im folgenden Code werden die Attribute für eine Assembly veranschaulicht, die über zwei Abhängigkeiten verfügt.  Die erste Abhängigkeit \(Assembly1\) ist ein geeigneter Kandidat für die feste Bindung und die zweite Abhängigkeit \(Assembly2\) nicht.  
  
```vb  
Imports System.Runtime.CompilerServices  
<Assembly:DependencyAttribute("Assembly1", LoadHint.Always)>  
<Assembly:DependencyAttribute("Assembly2", LoadHint.Sometimes)>  
```  
  
```csharp  
using System.Runtime.CompilerServices;  
[assembly:DependencyAttribute("Assembly1", LoadHint.Always)]  
[assembly:DependencyAttribute("Assembly2", LoadHint.Sometimes)]  
```  
  
```cpp#  
using namespace System::Runtime::CompilerServices;  
[assembly:DependencyAttribute("Assembly1", LoadHint.Always)];  
[assembly:DependencyAttribute("Assembly2", LoadHint.Sometimes)];  
```  
  
 Der Assemblyname enthält keine Dateinamenerweiterung.  Anzeigenamen können verwendet werden.  
  
### Angeben eines standardmäßigen Bindungshinweises für eine Assembly  
 Standardmäßige Bindungshinweise werden nur für Assemblys benötigt, die direkt und häufig von einer Anwendung verwendet werden, die über eine Abhängigkeit zu diesen Assemblys verfügt.  Wenden Sie <xref:System.Runtime.CompilerServices.DefaultDependencyAttribute> mit <xref:System.Runtime.CompilerServices.LoadHint?displayProperty=fullName> auf diese Assemblys an, um anzugeben, dass die feste Bindung verwendet werden soll.  
  
> [!NOTE]
>  Es gibt keinen Grund, <xref:System.Runtime.CompilerServices.DefaultDependencyAttribute> auf DLL\-Assemblys anzuwenden, die nicht in diese Kategorie fallen, da das Anwenden des Attributs mit einem anderen Wert als <xref:System.Runtime.CompilerServices.LoadHint?displayProperty=fullName> ohne Auswirkung bleibt.  
  
 Microsoft verwendet das <xref:System.Runtime.CompilerServices.DefaultDependencyAttribute>, um die feste Bindung als Standard für eine verhältnismäßig kleine Anzahl von Assemblys in .NET Framework anzugeben, beispielsweise mscorlib.dll.  
  
## Problembehandlung  
 Um zu überprüfen, ob systemeigene Images von der Anwendung verwendet werden, können Sie den [Fuslogvw.exe \(Assembly Binding Log Viewer\)](../../../docs/framework/tools/fuslogvw-exe-assembly-binding-log-viewer.md) verwenden.  Wählen Sie im Fenster des Binding Log Viewer\-Tools im Feld **Kategorien protokollieren** die Option **Systemeigene Images** aus.  Fuslogvw.exe liefert Informationen über die Gründe, aus denen ein systemeigenes Image abgelehnt wurde.  
  
 Mit dem Assistent für verwaltetes Debuggen, [jitCompilationStart](../../../docs/framework/debug-trace-profile/jitcompilationstart-mda.md), können Sie bestimmen, wann der JIT\-Compiler mit der Kompilierung einer Funktion beginnt.  
  
## Verzögertes Verarbeiten  
 Die Generierung von systemeigenen Images für eine sehr große Anwendung kann sehr viel Zeit beanspruchen.  Entsprechend können Änderungen an einer freigegebenen Komponente oder an den Computereinstellungen die Aktualisierung vieler systemeigener Images erfordern.  Die Aktion `install` und die Aktion `update` verfügen über eine Option `/queue`, über die Sie den Vorgang zur verzögerten Ausführung in eine Warteschlange stellen und vom Dienst für systemeigene Images verarbeiten lassen können.  Außerdem verfügt "Ngen.exe" über die Aktion `queue` und die Aktion `executeQueuedItems`, mit der der Dienst in gewissem Umfang gesteuert werden kann.  Weitere Informationen finden Sie unter [Native Image Service](http://msdn.microsoft.com/de-de/b15e0e32-59cb-4ae4-967c-6c9527781309).  
  
## Systemeigene Images und JIT\-Kompilierung  
 Wenn Ngen.exe auf Methoden in einer Assembly trifft, die von diesem Programm nicht generiert werden können, werden diese Methoden aus dem systemeigenen Image ausgeschlossen.  Wenn die Laufzeit diese Assembly ausführt, werden die nicht im systemeigenen Image enthaltenen Methoden auf JIT\-Kompilierung zurückgesetzt.  
  
 Darüber hinaus werden systemeigene Images nicht verwendet, wenn die Assembly aktualisiert wurde bzw. das Image aus irgendeinem Grund ungültig geworden ist.  
  
### Ungültige Images  
 Wenn Sie mit "Ngen.exe" ein systemeigenes Image einer Assembly erstellen, hängt die Ausgabe von den Optionen in der Befehlszeile und den Computereinstellungen ab.  Dies betrifft folgende Einstellungen:  
  
-   Die Version von .NET Framework.  
  
-   Die Version des Betriebssystems, wenn der Wechsel von der Windows 9x\-Familie zur Windows NT\-Familie durchgeführt wird.  
  
-   Die genaue Identität der Assembly \(durch Neukompilierung wird die Identität geändert\).  
  
-   Die genaue Identität aller Assemblys, auf die die Assembly verweist \(durch Neukompilierung wird die Identität geändert\).  
  
-   Sicherheitsfaktoren.  
  
 Diese Daten werden beim Generieren eines systemeigenen Image von Ngen.exe aufgezeichnet.  Beim Ausführen einer Assembly sucht die Common Language Runtime nach dem systemeigenen Image, das mit den Optionen und Einstellungen in Übereinstimmung mit der aktuellen Computerumgebung generiert wurde.  Die Laufzeit wird auf die JIT\-Kompilierung einer Assembly zurückgesetzt, falls kein geeignetes systemeigenes Image gefunden werden kann.  Die folgenden Änderungen an den Einstellungen und der Umgebung eines Computers führen dazu, dass systemeigene Images ungültig werden:  
  
-   Die Version von .NET Framework.  
  
     Wenn Sie .NET Framework aktualisieren, werden alle von Ihnen mit Ngen.exe erstellten systemeigenen Images ungültig.  Aus diesem Grund wird bei allen Updates von .NET Framework der Befehl `Ngen Update` ausgeführt, um sicherzustellen, dass alle systemeigenen Images erneut generiert werden.  .NET Framework erzeugt automatisch neue systemeigene Images für die .NET Framework\-Bibliotheken, die installiert werden.  
  
-   Die Version des Betriebssystems, wenn der Wechsel von der Windows 9x\-Familie zur Windows NT\-Familie durchgeführt wird.  
  
     Wenn sich beispielsweise die Version des Betriebssystems eines Computers von Windows 98 in Windows XP ändert, werden alle systemeigenen Images im Cache für systemeigene Images ungültig.  Wenn sich das Betriebssystem jedoch von Windows 2000 in Windows XP ändert, werden die Images nicht ungültig.  
  
-   Die genaue Identität der Assembly.  
  
     Nach dem Neukompilieren einer Assembly wird das systemeigene Image der Assembly ungültig.  
  
-   Die genaue Identität aller Assemblys, auf die die Assembly verweist.  
  
     Wenn Sie eine verwaltete Assembly aktualisieren, werden alle systemeigenen Images, die direkt oder indirekt von dieser Assembly abhängen, ungültig und müssen erneut generiert werden.  Dies betrifft sowohl normale Verweise als auch fest gebundene Abhängigkeiten.  Bei jedem Softwareupdate sollte das Installationsprogramm den Befehl `Ngen Update` ausführen, um sicherzustellen, dass alle abhängigen systemeigenen Images erneut generiert werden.  
  
-   Sicherheitsfaktoren.  
  
     Wenn die Sicherheitsrichtlinien eines Computers so geändert werden, dass Berechtigungen für eine Assembly widerrufen werden, können vorher kompilierte systemeigene Images für die entsprechende Assembly ungültig werden.  
  
     Ausführliche Informationen über die Verwaltung der Codezugriffssicherheit durch die Common Language Runtime und die Verwendung von Berechtigungen finden Sie unter [Code Access Security](../../../docs/framework/misc/code-access-security.md).  
  
## Beispiele  
 Mit dem folgenden Befehl wird ein systemeigenes Image für `ClientApp.exe` generiert, im aktuellen Verzeichnis abgelegt und anschließend im Cache für systemeigene Images installiert.  Wenn eine Konfigurationsdatei für die Assembly vorhanden ist, wird sie von Ngen.exe verwendet.  Außerdem werden systemeigene Images für alle DLL\-Dateien generiert, auf die `ClientApp.exe` verweist.  
  
```  
ngen install ClientApp.exe  
```  
  
 Ein mit Ngen.exe installiertes Image wird auch als Stammelement bezeichnet.  Ein Stammelement kann eine Anwendung oder eine freigegebene Komponente sein.  
  
 Durch den folgenden Befehl wird ein systemeigenes Image für `MyAssembly.exe` mit dem angegebenen Pfad generiert.  
  
```  
ngen install c:\myfiles\MyAssembly.exe  
```  
  
 Bei der Suche nach Assemblys und ihren Abhängigkeiten verwendet Ngen.exe dieselbe Überprüfungslogik wie die Common Language Runtime.  Das Verzeichnis, in dem `ClientApp.exe` enthalten ist, wird standardmäßig als Basisverzeichnis der Anwendung verwendet, und sämtliche Überprüfungen von Assemblys werden in diesem Verzeichnis gestartet.  Sie können dieses Verhalten mit der Option `/AppBase` überschreiben.  
  
> [!NOTE]
>  Dies ist eine Änderung im Verhalten von "Ngen.exe" gegenüber .NET Framework Version 1.0 und 1.1, bei denen die Anwendungsbasis auf das aktuelle Verzeichnis festgelegt wird.  
  
 Eine Assembly kann über eine Abhängigkeit ohne Verweis verfügen, wenn sie beispielsweise eine DLL\-Datei mithilfe der <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName>\-Methode lädt.  Sie können mit der Option `/ExeConfig` ein systemeigenes Image für eine solche DLL\-Datei erstellen, indem Sie Konfigurationsinformationen für die Anwendungsassembly verwenden.  Der folgende Befehl generiert ein systemeigenes Image für `MyLib.dll,` mithilfe der Konfigurationsinformationen aus `MyApp.exe`.  
  
```  
ngen install c:\myfiles\MyLib.dll /ExeConfig:c:\myapps\MyApp.exe  
```  
  
 Auf diese Weise installierte Assemblys werden nicht entfernt, wenn die Anwendung entfernt wird.  
  
 Verwenden Sie zum Deinstallieren einer Abhängigkeit dieselben Befehlszeilenoptionen wie beim Installieren.  Durch den folgenden Befehl wird `MyLib.dll` aus dem vorherigen Beispiel deinstalliert.  
  
```  
ngen uninstall c:\myfiles\MyLib.dll /ExeConfig:c:\myapps\MyApp.exe  
```  
  
 Verwendung Sie zum Erstellen eines systemeigenen Images für eine Assembly im globalen Assemblycache den Anzeigenamen der Assembly.  Beispiel:  
  
```  
ngen install "ClientApp, Version=1.0.0.0, Culture=neutral,   
  PublicKeyToken=3c7ba247adcd2081, processorArchitecture=MSIL"  
```  
  
 Ngen.exe generiert einen separaten Satz von Images für jedes Szenario, das Sie installieren.  Durch die folgenden Befehle wird beispielsweise ein vollständiger Satz von systemeigenen Images für den normalen Ablauf, ein anderer vollständiger Satz für das Debuggen und ein dritter Satz für die Profilerstellung erstellt:  
  
```  
ngen install MyApp.exe  
ngen install MyApp.exe /debug  
ngen install MyApp.exe /profile  
```  
  
### Anzeigen des Caches für systemeigene Images  
 Sobald systemeigene Images im Cache installiert wurden, können sie mit "Ngen.exe" angezeigt werden.  Der folgende Befehl dient zur Anzeige aller systemeigenen Images im Cache für systemeigene Images.  
  
```  
ngen display  
```  
  
 Durch die Aktion `display` werden zuerst alle Stammassemblys und dann alle systemeigenen Images auf dem Computer aufgelistet.  
  
 Verwenden Sie den einfachen Namen einer Assembly, um nur Informationen für diese Assembly anzuzeigen.  Durch den folgenden Befehl werden alle systemeigenen Images aus dem Cache für systemeigene Images angezeigt, die den Teilnamen `MyAssembly` aufweisen, sowie ihre Abhängigkeiten und alle Stammassemblys, die über eine Abhängigkeit zu `MyAssembly` verfügen:  
  
```  
ngen display MyAssembly  
```  
  
 Zum Beurteilen des Einflusses, den eine `update`\-Aktion nach der Aktualisierung der freigegebenen Komponente hat, ist es hilfreich, die Stammassemblys zu kennen, die von der Assembly der freigegebenen Komponente abhängen.  
  
 Wenn Sie die Dateierweiterung einer Assembly angeben, müssen Sie entweder den Pfad angeben oder "Ngen.exe" von dem Verzeichnis aus ausführen, in dem die Assembly enthalten ist:  
  
```  
ngen display c:\myApps\MyAssembly.exe  
```  
  
 Der folgende Befehl dient zur Anzeige aller systemeigenen Images im Cache für systemeigene Images mit dem Namen `MyAssembly` und der Version 1.0.0.0.  
  
```  
ngen display "myAssembly, version=1.0.0.0"  
```  
  
### Aktualisieren von Images  
 Images werden normalerweise aktualisiert, nachdem eine freigegebene Komponente aktualisiert wurde.  Verwenden Sie zum Aktualisieren aller systemeigenen Images, die bzw. deren Abhängigkeiten geändert wurden, die Aktion `update` ohne Argumente.  
  
```  
ngen update  
```  
  
 Das Aktualisieren aller Images kann ein langwieriger Prozess sein.  Sie können die Updates mit der Option `/queue` in eine Warteschlange stellen, um sie vom Dienst für systemeigene Images ausführen zu lassen.  Weitere Informationen zur Option `/queue` und den Prioritäten bei der Installation finden Sie unter [Native Image Service](http://msdn.microsoft.com/de-de/b15e0e32-59cb-4ae4-967c-6c9527781309).  
  
```  
ngen update /queue  
```  
  
### Deinstallieren von Images  
 "Ngen.exe" verwaltet eine Liste von Abhängigkeiten. Freigegebene Komponenten können demnach nur entfernt werden, nachdem alle Assemblys, die von diesen Komponenten abhängen, entfernt wurden.  Darüber hinaus wird eine freigegebene Komponente, die als Stammelement installiert wurde, nicht entfernt.  
  
 Mit dem folgenden Befehl werden alle Szenarien für den Stamm `ClientApp.exe` deinstalliert:  
  
```  
ngen uninstall ClientApp  
```  
  
 Mit der Aktion `uninstall` können bestimmte Szenarien entfernt werden.  Mit dem folgenden Befehl werden alle Debugszenarien für `ClientApp.exe` deinstalliert:  
  
```  
ngen uninstall ClientApp /debug  
```  
  
> [!NOTE]
>  Beim Deinstallieren von `/debug`\-Szenarien werden keine Szenarien deinstalliert, die sowohl `/profile` als auch `/debug.` enthalten.  
  
 Mit dem folgenden Befehl werden alle Szenarien für eine bestimmte Version von `ClientApp.exe` deinstalliert:  
  
```  
ngen uninstall "ClientApp, Version=1.0.0.0"  
```  
  
 Mit den folgenden Befehlen werden alle Szenarien für `"ClientApp, Version=1.0.0.0, Culture=neutral, PublicKeyToken=3c7ba247adcd2081, processorArchitecture=MSIL",` oder nur das Debugszenario für diese Assembly deinstalliert:  
  
```  
ngen uninstall "ClientApp, Version=1.0.0.0, Culture=neutral,   
  PublicKeyToken=3c7ba247adcd2081, processorArchitecture=MSIL"  
ngen uninstall "ClientApp, Version=1.0.0.0, Culture=neutral,   
  PublicKeyToken=3c7ba247adcd2081, processorArchitecture=MSIL" /debug  
```  
  
 Wie bei der Aktion `install` erfordert die Angabe einer Erweiterung entweder, dass "Ngen.exe" von dem Verzeichnis aus ausgeführt werden muss, in dem die Assembly enthalten ist, oder dass der vollständige Pfad angegeben werden muss.  
  
 Beispiele, die sich auf den Dienst für systemeigene Images beziehen, finden Sie unter [Native Image Service](http://msdn.microsoft.com/de-de/b15e0e32-59cb-4ae4-967c-6c9527781309).  
  
## Aufgabe zur Generierung systemeigener Images  
 Die Aufgabe zur Generierung systemeigener Images ist eine Windows\-Aufgabe, die systemeigene Images generiert und verwaltet.  Die Aufgabe zur Generierung systemeigener Images geht so vor, dass sie automatisch systemeigene Images für die unterstützten Szenarien generiert und freigibt.  \(Weitere Informationen finden Sie unter [Creating Native Images](http://msdn.microsoft.com/de-de/2bc8b678-dd8d-4742-ad82-319e9bf52418).\) Sie ermöglichte es Installationsprogrammen außerdem, [Ngen.exe \(Native Image Generator\)](../../../docs/framework/tools/ngen-exe-native-image-generator.md) zu verwenden, um systemeigene Images nach einer Zeitverzögerung zu erstellen und zu aktualisieren.  
  
 Die Aufgabe zur Generierung systemeigener Images wird einmal für jede CPU\-Architektur registriert, die auf einem Computer unterstützt wird. Dadurch ist es möglich, Anwendungen zu kompilieren, die genau für jede Architektur angepasst sind:  
  
|Aufgabenname|32\-Bit\-Computer|64\-Bit\-Computer|  
|------------------|-----------------------|-----------------------|  
|NET Framework NGEN v4.0.30319|Ja|Ja|  
|NET Framework NGEN v4.0.30319 64|Nein|Ja|  
  
 Die Aufgabe zur Generierung systemeigener Images ist in .NET Framework 4.5 und höher verfügbar, wenn sie unter Windows 8 oder höher ausgeführt wird.  In früheren Versionen von Windows verwendet .NET Framework den [Native Image Service](http://msdn.microsoft.com/de-de/b15e0e32-59cb-4ae4-967c-6c9527781309).  
  
### Lebensdauer der Aufgabe  
 Üblicherweise startet der Windows\-Taskplaner die Aufgabe zur Generierung systemeigener Images jede Nacht, wenn sich der Computer im Leerlauf befindet.  Die Aufgabe prüft auf zurückgestellte Arbeit, die von Anwendungsinstallationsprogrammen in die Warteschlange eingereiht wurde, auf zurückgestellte Aktualisierungsanforderungen für systemeigene Images sowie auf automatische Imageerstellung.  Die Aufgabe schließt ausstehende Arbeitsaufgaben ab und fährt dann herunter.  Wird für den Computer der Leerlaufzustand beendet, während die Aufgabe ausgeführt wird, wird die Aufgabe beendet.  
  
 Sie können die Aufgabe zur Generierung systemeigener Images auch manuell über die Taskplaner\-Benutzeroberfläche oder durch manuelle Aufrufe von "NGen.exe" starten.  Wird die Aufgabe mit einer dieser Methoden gestartet, wird sie weiter ausgeführt, wenn der Computer nicht mehr im Leerlauf ist.  Images, die manuell mit "NGen.exe" erstellt wurden, werden priorisiert, um vorhersagbares Verhalten für Installationsprogramme von Anwendungen zu ermöglichen.  
  
## Dienst für systemeigene Abbilder  
 Der Dienst für systemeigene Abbilder ist ein Windows\-Dienst, der systemeigene Abbilder \(Images\) generiert und verwaltet.  Der Dienst für systemeigene Abbilder ermöglicht es dem Entwickler, die Installation und Aktualisierung von systemeigenen Abbildern in Zeiträume zu verschieben, in denen sich der Computer im Leerlauf befindet.  
  
 Normalerweise wird der Dienst für systemeigene Abbilder vom Installationsprogramm \(Installer\) für eine Anwendung oder ein Update gestartet.  Für Aktionen mit Priorität 3 wird der Dienst während Leerlaufzeiten des Computer ausgeführt.  Der Dienst speichert seinen Zustand und kann, sofern erforderlich, selbst nach mehreren Neustarts fortgesetzt werden.  Mehrere Imagekompilierungen können in die Warteschlange gestellt werden.  
  
 Der Dienst interagiert außerdem mit dem manuellen Befehl "Ngen.exe".  Manuelle Befehle haben Vorrang vor Hintergrundaktivitäten.  
  
> [!NOTE]
>  Unter Windows Vista ist der Anzeigenamen für den Dienst für systemeigene Abbilder "Microsoft.NET Framework NGEN 50727\_X86" oder "Microsoft.NET Framework NGEN 50727\_X64".  Bei allen früheren Versionen von Microsoft Windows lautet der Name ".NET Runtime Optimization Service 50727\_X86" oder ".NET Runtime Optimization Service 50727\_X64".  
  
### Starten verzögerter Vorgänge  
 Es empfiehlt sich, vor dem Starten einer Installation oder Aktualisierung den Dienst zu beenden.  Dadurch ist sichergestellt, dass der Dienst nicht ausgeführt wird, während das Installationsprogramm Dateien kopiert oder Assemblys im globalen Assemblycache ablegt.  Die folgende Befehlszeile von "Ngen.exe" beendet den Dienst:  
  
```  
ngen queue pause  
```  
  
 Nachdem alle verzögerten Vorgänge in die Warteschlange gestellt wurden, kann der Dienst mit dem folgenden Befehl fortgesetzt werden:  
  
```  
ngen queue continue  
```  
  
 Um die Generierung von systemeigenen Images zu verzögern, wenn eine neue Anwendung installiert oder eine freigegebene Komponente aktualisiert wird, verwenden Sie die `/queue`\-Option mit der `install`\- oder der `update`\-Aktion.  Mit den folgenden Befehlszeilen in "Ngen.exe" wird ein systemeigenes Image für eine freigegebene Komponente installiert und werden alle Stammelemente aktualisiert, die möglicherweise betroffen sind:  
  
```  
ngen install MyComponent /queue  
ngen update /queue  
```  
  
 Die `update`\-Aktion bewirkt, dass alle systemeigenen Images neu generiert werden, die ungültig geworden sind, nicht nur diejenigen, für die `MyComponent` verwendet wird.  
  
 Wenn die Anwendung aus vielen Stammelemente besteht, können Sie die Priorität der verzögerten Aktionen steuern.  Die folgenden Befehle stellen die Installation der drei Stammelemente in die Warteschlange.  `Assembly1` wird zuerst installiert, ohne dass auf eine Leerlaufzeit gewartet wird.  `Assembly2` wird ebenfalls ohne Warten auf eine Leerlaufzeit installiert, aber erst, nachdem alle Aktionen mit Priorität 1 abgeschlossen sind.  `Assembly3` wird installiert, wenn der Dienst feststellt, dass sich der Computer im Leerlauf befindet.  
  
```  
ngen install Assembly1 /queue:1  
ngen install Assembly2 /queue:2  
ngen install Assembly3 /queue:3  
```  
  
 Durch Verwenden der `executeQueuedItems`\-Aktion können Sie erzwingen, dass in der Warteschlange befindliche Aktionen gleichzeitig ausgeführt werden.  Wenn Sie die optionale Priorität angeben, wirkt sich diese Aktion nur auf die Aktionen in der Warteschlange aus, die dieselbe oder eine niedrigere Priorität haben.  Da die Standardpriorität gleich 3 ist, verarbeitet der folgende "Ngen.exe"\-Befehl alle in der Warteschlange befindlichen Aktionen sofort, und er wird erst beendet, wenn die Aktionen abgeschlossen sind:  
  
```  
ngen executeQueuedItems  
```  
  
 Synchrone Befehle werden von "Ngen.exe" ausgeführt, und für sie wird nicht Dienst für systemeigene Abbilder verwendet.  Sie können Aktionen mit "Ngen.exe" ausführen, während der Dienst für systemeigene Abbilder ausgeführt wird.  
  
### Beenden des Diensts  
 Nachdem der Dienst durch Ausführen eines "Ngen.exe"\-Befehls, der die `/queue`\-Option enthält, gestartet wurde, wird er im Hintergrund ausgeführt, bis alle Aktionen abgeschlossen wurden.  Der Dienst speichert seinen Zustand, sodass er, sofern erforderlich, selbst nach mehreren Neustarts fortgesetzt werden kann.  Wenn der Dienst feststellt, dass es keine weiteren Aktionen in der Warteschlange gibt, setzt er seinen Status zurück, sodass er beim nächsten Computerstart nicht neu gestartet wird, und dann beendet sich der Dienst selbst.  
  
### Dienstinteraktion mit Clients  
 In .NET Framework 2.0 erfolgt die einzige Interaktion mit dem Dienst für systemeigene Abbilder über das Befehlszeilentool "Ngen.exe".  Verwenden Sie das Befehlszeilentool in Installationsskripts, um Aktionen für den Dienst für systemeigene Abbilder in die Warteschlange zu stellen und mit dem Dienst zu interagieren.  
  
## Siehe auch  
 [Native Image Service](http://msdn.microsoft.com/de-de/b15e0e32-59cb-4ae4-967c-6c9527781309)   
 [Native Image Task](http://msdn.microsoft.com/de-de/9b1f7590-4e0d-4737-90ef-eaf696932afb)   
 [Tools](../../../docs/framework/tools/index.md)   
 [Der verwaltete Ausführungsprozess](../../../docs/standard/managed-execution-process.md)   
 [So sucht Common Language Runtime nach Assemblys](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)   
 [Eingabeaufforderungen](../../../docs/framework/tools/developer-command-prompt-for-vs.md)