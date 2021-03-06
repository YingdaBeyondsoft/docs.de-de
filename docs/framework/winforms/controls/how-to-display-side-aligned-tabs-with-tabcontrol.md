---
title: "Gewusst wie: Anzeigen von seitlich ausgerichteten Registerkarten mit TabControl | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Registerkarten, Anzeigen von seitlich ausgerichteten Registerkarten"
  - "TabControl-Steuerelement [Windows Forms], Anzeigen von seitlich ausgerichteten Registerkarten"
  - "Registerkarten, Anzeigen von seitlich ausgerichteten Registerkarten"
ms.assetid: 110d5abd-3ae3-4ded-95bf-778aaac798a0
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Gewusst wie: Anzeigen von seitlich ausgerichteten Registerkarten mit TabControl
Die <xref:System.Windows.Forms.TabControl.Alignment%2A>\-Eigenschaft des <xref:System.Windows.Forms.TabControl> unterstützt das vertikale Anzeigen von Registerkarten \(entlang des linken oder rechten Rands des Steuerelements\), im Gegensatz zu horizontal \(am oberen oder unteren Rand des Steuerelements\).  Standardmäßig führt diese vertikale Anzeige zu einer wenig benutzerfreundlichen Oberfläche, weil die <xref:System.Windows.Forms.TabPage.Text%2A>\-Eigenschaft des <xref:System.Windows.Forms.TabPage>\-Objekts nicht auf der Registerkarte angezeigt wird, wenn visuelle Stile aktiviert sind.  Es ist außerdem keine direkte Möglichkeit zur Steuerung der Richtung des Texts auf der Registerkarte.  Sie können Ownerdrawn in <xref:System.Windows.Forms.TabControl> verwenden, um die Oberfläche zu verbessern.  
  
 Das folgende Verfahren zeigt, wie rechtsbündig ausgerichtete Registerkarten gerendert werden, wobei der Registerkartentext von links nach rechts verläuft, indem Sie die Funktion "Ownerdrawn" verwenden.  
  
### So zeigen Sie rechtsbündig ausgerichtete Registerkarten an  
  
1.  Fügen Sie Ihrem Formular ein <xref:System.Windows.Forms.TabControl> hinzu.  
  
2.  Legen Sie die <xref:System.Windows.Forms.TabControl.Alignment%2A>\-Eigenschaft auf <xref:System.Windows.Forms.TabAlignment> fest.  
  
3.  Legen Sie die <xref:System.Windows.Forms.TabControl.SizeMode%2A>\-Eigenschaft auf <xref:System.Windows.Forms.TabSizeMode> fest, damit alle Registerkarten gleich breit sind.  
  
4.  Legen Sie die <xref:System.Windows.Forms.TabControl.ItemSize%2A>\-Eigenschaft auf die gewünschte feste Größe für die Registerkarten fest.  Denken Sie daran, dass sich die <xref:System.Windows.Forms.TabControl.ItemSize%2A>\-Eigenschaft verhält, als seien die Registerkarten am oberen Rand, obwohl sie rechtsbündig ausgerichtet sind.  Demzufolge müssen Sie, um die Registerkarten zu verbreitern, die <xref:System.Drawing.Size.Height%2A>\-Eigenschaft ändern, und um sie höher zu machen, müssen Sie die <xref:System.Drawing.Size.Width%2A>\-Eigenschaft ändern.  
  
     Für ein optimales Ergebnis mit dem folgenden Codebeispiel legen Sie die <xref:System.Drawing.Size.Width%2A> der Registerkarten auf 25 und die <xref:System.Drawing.Size.Height%2A> auf 100 fest.  
  
5.  Legen Sie die <xref:System.Windows.Forms.TabControl.DrawMode%2A>\-Eigenschaft auf <xref:System.Windows.Forms.TabDrawMode> fest.  
  
6.  Definieren Sie einen Ereignishandler für das <xref:System.Windows.Forms.TabControl.DrawItem>\-Ereignis des <xref:System.Windows.Forms.TabControl>, das den Text von links nach rechts rendert.  
  
     [!code-csharp[TabControl.RightAlignedTabs#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/TabControl.RightAlignedTabs/CS/Form1.cs#1)]
     [!code-vb[TabControl.RightAlignedTabs#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/TabControl.RightAlignedTabs/VB/Form1.vb#1)]  
  
## Siehe auch  
 [TabControl\-Steuerelement](../../../../docs/framework/winforms/controls/tabcontrol-control-windows-forms.md)