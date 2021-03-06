---
title: "How to: Sign XML Documents with Digital Signatures | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "signatures, XML signing"
  - "System.Security.Cryptography.SignedXml class"
  - "digital signatures, XML signing"
  - "System.Security.Cryptography.RSACryptoServiceProvider class"
  - "XML digital signatures"
  - "XML signing"
  - "signing XML"
ms.assetid: 99692ac1-d8c9-42d7-b1bf-2737b01037e4
caps.latest.revision: 13
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 13
---
# How to: Sign XML Documents with Digital Signatures
Um ein XML\-Dokument teilweise oder vollständig mit einer digitalen Signatur zu versehen, können Sie die Klassen im <xref:System.Security.Cryptography.Xml>\-Namespace verwenden.  Über digitale XML\-Signaturen \(XMLDSIG\) können Sie sich vergewissern, dass Daten nicht mehr geändert wurden, nachdem sie signiert wurden.  Weitere Informationen zum XMLDSIG\-Standard, finden Sie in der W3C\-Empfehlung \(World Wide Web Consortium\) [XML Signature Syntax and Processing](http://go.microsoft.com/fwlink/?LinkID=136777).  
  
 Im Codebeispiel in dieser Vorgehensweise wird veranschaulicht, wie ein gesamtes XML\-Dokument digital signiert und die Signatur dem Dokument in einem \<`Signature`\>\-Element angefügt wird.  Im Beispiel wird ein RSA\-Signaturschlüssel erstellt, wird der Schlüssel einem sicheren Schlüsselcontainer hinzugefügt und wird der Schlüssel dann verwendet, um ein XML\-Dokument digital zu signieren.  Der Schlüssel kann danach abgerufen werden, um die digitale Signatur des XML\-Dokuments zu überprüfen oder ein anderes XML\-Dokument zu signieren.  
  
 Informationen dazu, wie eine digitale Signatur überprüft wird, die mit dieser Vorgehensweise erstellt wurde, finden Sie unter [How to: Verify the Digital Signatures of XML Documents](../../../docs/standard/security/how-to-verify-the-digital-signatures-of-xml-documents.md).  
  
### So signieren Sie ein XML\-Dokument digital  
  
1.  Erstellen Sie ein <xref:System.Security.Cryptography.CspParameters>\-Objekt, und geben Sie den Namen des Schlüsselcontainers an.  
  
     [!code-csharp[HowToSignXMLDocumentRSA#2](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#2)]
     [!code-vb[HowToSignXMLDocumentRSA#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#2)]  
  
2.  Generieren Sie mit der <xref:System.Security.Cryptography.RSACryptoServiceProvider>\-Klasse einen asymmetrischen Schlüssel.  Der Schlüssel wird automatisch im Schlüsselcontainer gespeichert, wenn Sie das <xref:System.Security.Cryptography.CspParameters>\-Objekt an den Konstruktor der <xref:System.Security.Cryptography.RSACryptoServiceProvider>\-Klasse übergeben.  Dieser Schlüssel wird zum Signieren des XML\-Dokuments verwendet.  
  
     [!code-csharp[HowToSignXMLDocumentRSA#3](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#3)]
     [!code-vb[HowToSignXMLDocumentRSA#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#3)]  
  
3.  Erstellen Sie ein <xref:System.Xml.XmlDocument>\-Objekt, indem Sie eine XML\-Datei von einem Datenträger laden.  Das <xref:System.Xml.XmlDocument>\-Objekt enthält das zu verschlüsselnde XML\-Element.  
  
     [!code-csharp[HowToSignXMLDocumentRSA#4](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#4)]
     [!code-vb[HowToSignXMLDocumentRSA#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#4)]  
  
4.  Erstellen Sie ein neues <xref:System.Security.Cryptography.Xml.SignedXml>\-Objekt, und übergeben Sie diesem das <xref:System.Xml.XmlDocument>\-Objekt.  
  
     [!code-csharp[HowToSignXMLDocumentRSA#5](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#5)]
     [!code-vb[HowToSignXMLDocumentRSA#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#5)]  
  
5.  Fügen Sie den RSA\-Signaturschlüssel dem <xref:System.Security.Cryptography.Xml.SignedXml>\-Objekt hinzu.  
  
     [!code-csharp[HowToSignXMLDocumentRSA#6](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#6)]
     [!code-vb[HowToSignXMLDocumentRSA#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#6)]  
  
6.  Erstellen Sie ein <xref:System.Security.Cryptography.Xml.Reference>\-Objekt, das beschreibt, was signiert werden soll.  Um das gesamte Dokument zu signieren, legen Sie die <xref:System.Security.Cryptography.Xml.Reference.Uri%2A>\-Eigenschaft auf `""` fest.  
  
     [!code-csharp[HowToSignXMLDocumentRSA#7](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#7)]
     [!code-vb[HowToSignXMLDocumentRSA#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#7)]  
  
7.  Fügen Sie dem <xref:System.Security.Cryptography.Xml.Reference>\-Objekt ein <xref:System.Security.Cryptography.Xml.XmlDsigEnvelopedSignatureTransform>\-Objekt hinzu.  Eine Transformation ermöglicht es dem Prüfer, die XML\-Daten auf genau die Weise darzustellen, die der Signaturgeber verwendet hat.  XML\-Daten können auf unterschiedliche Weise dargestellt werden, weshalb dieser Schritt für die Überprüfung unverzichtbar ist.  
  
     [!code-csharp[HowToSignXMLDocumentRSA#8](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#8)]
     [!code-vb[HowToSignXMLDocumentRSA#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#8)]  
  
8.  Fügen Sie dem <xref:System.Security.Cryptography.Xml.SignedXml>\-Objekt das <xref:System.Security.Cryptography.Xml.Reference>\-Objekt hinzu.  
  
     [!code-csharp[HowToSignXMLDocumentRSA#9](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#9)]
     [!code-vb[HowToSignXMLDocumentRSA#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#9)]  
  
9. Berechnen Sie die Signatur, indem Sie die <xref:System.Security.Cryptography.Xml.SignedXml.ComputeSignature%2A>\-Methode aufrufen.  
  
     [!code-csharp[HowToSignXMLDocumentRSA#10](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#10)]
     [!code-vb[HowToSignXMLDocumentRSA#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#10)]  
  
10. Rufen Sie die XML\-Darstellung der Signatur \(ein \<`Signature`\>\-Element\) ab, und speichern Sie die Darstellung in einem neuen <xref:System.Xml.XmlElement>\-Objekt.  
  
     [!code-csharp[HowToSignXMLDocumentRSA#11](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#11)]
     [!code-vb[HowToSignXMLDocumentRSA#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#11)]  
  
11. Fügen Sie das Element an das <xref:System.Xml.XmlDocument>\-Objekt an.  
  
     [!code-csharp[HowToSignXMLDocumentRSA#12](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#12)]
     [!code-vb[HowToSignXMLDocumentRSA#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#12)]  
  
12. Speichern Sie das Dokument.  
  
     [!code-csharp[HowToSignXMLDocumentRSA#13](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#13)]
     [!code-vb[HowToSignXMLDocumentRSA#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#13)]  
  
## Beispiel  
 Für dieses Beispiel wird angenommen, dass eine Datei namens `test.xml` im selben Verzeichnis wie das kompilierte Programm vorhanden ist.  Sie können den folgenden XML\-Code in eine Datei namens `test.xml` einfügen und mit diesem Beispiel verwenden.  
  
```  
<root>  
    <creditcard>  
        <number>19834209</number>  
        <expiry>02/02/2002</expiry>  
    </creditcard>  
</root>  
```  
  
 [!code-csharp[HowToSignXMLDocumentRSA#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#1)]
 [!code-vb[HowToSignXMLDocumentRSA#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#1)]  
  
## Kompilieren des Codes  
  
-   Um dieses Beispiel zu kompilieren, müssen Sie einen Verweis auf `System.Security.dll` einfügen.  
  
-   Fügen Sie die folgenden Namespaces hinzu: <xref:System.Xml>, <xref:System.Security.Cryptography> und <xref:System.Security.Cryptography.Xml>.  
  
## .NET Framework-Sicherheit  
 Sie sollten den privaten Schlüssel eines asymmetrischen Schlüsselpaars niemals in Klartext speichern oder übertragen.  Weitere Informationen über symmetrische und asymmetrische kryptografische Schlüssel finden Sie unter [Generating Keys for Encryption and Decryption](../../../docs/standard/security/generating-keys-for-encryption-and-decryption.md).  
  
 Sie sollten einen privaten Schlüssel niemals direkt in Ihren Quellcode einbetten.  Eingebettete Schlüssel können problemlos aus einer Assembly gelesen werden, indem [Ildasm.exe \(IL Disassembler\)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md) verwendet oder die Assembly in einem Texteditor wie Editor geöffnet wird.  
  
## Siehe auch  
 <xref:System.Security.Cryptography.Xml>   
 [How to: Verify the Digital Signatures of XML Documents](../../../docs/standard/security/how-to-verify-the-digital-signatures-of-xml-documents.md)