---
title: "Verf&#252;gbarmachen von Daten mit CacheMetadata | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 34832f23-e93b-40e6-a80b-606a855a00d9
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# Verf&#252;gbarmachen von Daten mit CacheMetadata
Vor dem Ausführen einer Aktivität ruft die Workflowlaufzeit alle Aktivitätsinformationen ab, die für die Ausführung erforderlich sind.Die Workflowlaufzeit ruft diese Informationen während der Ausführung der <xref:System.Activities.Activity.CacheMetadata%2A>\-Methode ab.Die Standardimplementierung dieser Methode stellt der Laufzeit alle öffentlichen Argumente, Variablen und untergeordneten Aktivitäten bereit, die von der Aktivität zur Ausführungszeit verfügbar gemacht werden. Wenn die Aktivität mehr Informationen als diese an die Laufzeit übergeben muss \(z. B. private Member oder Aktivitäten, die von der Aktivität geplant werden sollen\), kann diese Methode überschrieben werden, um diese Informationen zur Verfügung zu stellen.  
  
## CacheMetadata\-Standardverhalten  
 Die Standardimplementierung von <xref:System.Activities.NativeActivity.CacheMetadata%2A> für Aktivitäten, die aus <xref:System.Activities.NativeActivity> abgeleitet werden, verarbeitet die folgenden Methodentypen auf folgende Weise:  
  
-   <xref:System.Activities.InArgument%601>, <xref:System.Activities.OutArgument%601> oder <xref:System.Activities.InOutArgument%601> \(generische Argumente\): Diese Argumente werden für die Laufzeit als Argumente verfügbar gemacht, deren Name und Typ mit dem verfügbar gemachten Eigenschaftsnamen und \-typ identisch ist. Zudem werden die entsprechende Argumentrichtung und einige Validierungsdaten bereitgestellt.  
  
-   <xref:System.Activities.Variable> oder eine beliebige Unterklasse davon: Diese Member werden für die Laufzeit als öffentliche Variablen verfügbar gemacht.  
  
-   <xref:System.Activities.Activity> oder eine beliebige Unterklasse davon: Diese Member werden für die Laufzeit als öffentliche untergeordnete Aktivitäten verfügbar gemacht.Das Standardverhalten kann explizit implementiert werden, indem <xref:System.Activities.ActivityMetadata.AddImportedChild%2A> aufgerufen und die untergeordnete Aktivität übergeben wird.  
  
-   <xref:System.Activities.ActivityDelegate> oder eine beliebige Unterklasse davon: Diese Member werden für die Laufzeit als öffentliche Delegaten verfügbar gemacht.  
  
-   <xref:System.Collections.ICollection> vom Typ <xref:System.Activities.Variable>: Alle Elemente in der Auflistung werden für die Laufzeit als öffentliche Variablen verfügbar gemacht.  
  
-   <xref:System.Collections.ICollection> vom Typ <xref:System.Activities.Activity>: Alle Elemente in der Auflistung werden für die Laufzeit als öffentliche untergeordnete Elemente verfügbar gemacht.  
  
-   <xref:System.Collections.ICollection> vom Typ <xref:System.Activities.ActivityDelegate>: Alle Elemente in der Auflistung werden für die Laufzeit als öffentliche Delegaten verfügbar gemacht.  
  
 <xref:System.Activities.Activity.CacheMetadata%2A> für Aktivitäten, die aus <xref:System.Activities.Activity>, <xref:System.Workflow.Activities.CodeActivity> abgeleitet werden, und <xref:System.Activities.AsyncCodeActivity> funktionieren auch wie oben beschrieben, mit Ausnahme der folgenden Unterschiede:  
  
-   Klassen, die aus <xref:System.Activities.Activity> abgeleitet werden, können keine untergeordneten Aktivitäten oder Delegaten planen. Daher werden solche Member als importierte untergeordnete Elemente und Delegaten verfügbar gemacht.  
  
-   Klassen, die aus <xref:System.Activities.CodeActivity> und <xref:System.Activities.AsyncCodeActivity> abgeleitet werden, unterstützen keine Variablen, untergeordneten Elemente oder Delegaten, sodass nur Argumente verfügbar gemacht werden.  
  
## Überschreiben von CacheMetadata zum Bereitstellen von Informationen für die Laufzeit  
 Der folgende Codeausschnitt veranschaulicht, wie den Metadaten einer Aktivität während der Ausführung der <xref:System.Activities.Activity.CacheMetadata%2A>\-Methode Informationen zu Membern hinzugefügt werden.Beachten Sie, dass die Basis der Methode aufgerufen wird, um alle öffentlichen Daten zur Aktivität zwischenzuspeichern.  
  
```  
protected override void CacheMetadata(NativeActivityMetadata metadata)  
{      
    base.CacheMetadata(metadata);  
    metadata.AddImplementationChild(this._writeLine);  
    metadata.AddVariable(this._myVariable);  
    metadata.AddImplementationVariable(this._myImplementationVariable);  
  
    RuntimeArgument argument = new RuntimeArgument("MyArgument", ArgumentDirection.In, typeof(SomeType));  
    metadata.Bind(argument, this.SomeName);  
    metadata.AddArgument(argument);  
}  
  
```  
  
## Verwenden von CacheMetadata zum Verfügbarmachen von untergeordneten Elementen der Implementierung  
 Zur Übergabe von Daten an untergeordnete Aktivitäten, die mithilfe von Variablen von einer Aktivität geplant werden sollen, müssen die Variablen als Implementierungsvariablen hinzugefügt werden. Die Werte von öffentlichen Variablen können nicht auf diese Weise festgelegt werden.Der Grund ist, dass Aktivitäten nach Möglichkeit eher als Implementierungen von Funktionen \(die über Parameter verfügen\) ausgeführt werden sollen und nicht als gekapselte Klassen \(die über Eigenschaften verfügen\).Es gibt jedoch Situationen, in denen die Argumente explizit festgelegt werden müssen, beispielsweise beim Verwenden von <xref:System.Activities.NativeActivityContext.ScheduleActivity%2A>, da die geplante Aktivität nicht so auf die Argumente der übergeordneten Aktivität zugreifen kann wie eine untergeordnete Aktivität.  
  
 Der folgende Codeausschnitt veranschaulicht, wie ein Argument aus einer systemeigene Aktivität mit <xref:System.Activities.Activity.CacheMetadata%2A> an eine geplante Aktivität übergeben wird.  
  
```  
public sealed class ChildActivity : NativeActivity  
{  
    public WriteLine _writeLine;  
    public InArgument<string> Message { get; set; }  
    private Variable<string> MessageVariable { get; set; }  
    public ChildActivity()  
    {  
        MessageVariable = new Variable<string>();  
        _writeLine = new WriteLine  
        {  
            Text = new InArgument<string>(MessageVariable),  
        };  
    }  
    protected override void CacheMetadata(NativeActivityMetadata metadata)  
    {  
        base.CacheMetadata(metadata);  
        metadata.AddImplementationVariable(this.MessageVariable);  
        metadata.AddImplementationChild(this._writeLine);  
    }  
    protected override void Execute(NativeActivityContext context)  
    {  
        string configuredMessage = context.GetValue(Message);  
        context.SetValue(MessageVariable, configuredMessage);  
        context.ScheduleActivity(this._writeLine);  
    }  
}  
  
```