---
title: "Sicherheitsprotokolle, Version&#160;1.0 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ee3402d2-1076-410b-a3cb-fae0372bd7af
caps.latest.revision: 4
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 4
---
# Sicherheitsprotokolle, Version&#160;1.0
Die Webdienste\-Sicherheitsprotokolle bieten Webdiensten Sicherheitsmechanismen, die alle vorhandenen Nachrichtensicherheitsanforderungen eines Unternehmens abdecken.  In diesem Abschnitt werden die Details von [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)], Version &\#160;1.0, \(implementiert im <xref:System.ServiceModel.Channels.SecurityBindingElement>\) der folgenden Webdienste\-Sicherheitsprotokolle beschrieben.  
  
|||  
|-|-|  
|Spezifikation\/Dokument|Link|  
|WSS: SOAP\-Nachrichtensicherheit 1,0|http:\/\/docs.oasis\-open.org\/wss\/2004\/01\/oasis\-200401\-wss\-soap\-message\-security\-1.0.pdf \(möglicherweise in englischer Sprache\)|  
|WSS: Username Token Profile 1.0|http:\/\/docs.oasis\-open.org\/wss\/2004\/01\/oasis\-200401\-wss\-username\-token\-profile\-1.0.pdf \(möglicherweise in englischer Sprache\)|  
|WSS: X509 Token Profile 1,0|http:\/\/docs.oasis\-open.org\/wss\/2004\/01\/oasis\-200401\-wss\-x509\-token\-profile\-1.0.pdf \(möglicherweise in englischer Sprache\)|  
|WSS: SAML 1.1 Token Profile 1,0|http:\/\/docs.oasis\-open.org\/wss\/oasis\-wss\-sam1\-token\-profile\-1.0.pdf \(möglicherweise in englischer Sprache\)|  
|WSS: SOAP\-Nachrichtensicherheit 1.1|http:\/\/www.oasis\-open.org\/committees\/download.php\/16790\/wss\-v1.1\-spec\-os\-SOAPMessageSecurity.pdf \(möglicherweise in englischer Sprache\)|  
|WSS: Username Token Profile 1.1|http:\/\/docs.oasis\-open.org\/wss\/2004\/01\/oasis\-200401\-wss\-username\-token\-profile\-1.0.pdf \(möglicherweise in englischer Sprache\)|  
|WSS: X.509 Token Profile 1,1|http:\/\/www.oasis\-open.org\/committees\/download.php\/16785\/wss\-v1.1\-spec\-os\-x509TokenProfile.pdf \(möglicherweise in englischer Sprache\)|  
|WSS: Kerberos Token Profile 1.1|http:\/\/www.oasis\-open.org\/committees\/download.php\/16788\/wss\-v1.1\-spec\-os\-KerberosTokenProfile.pdf \(möglicherweise in englischer Sprache\)|  
|WSS: SAML 1.1 Token Profile 1.1|http:\/\/www.oasis\-open.org\/committees\/download.php\/16768\/wss\-v1.1\-spec\-os\-SAMLTokenProfile.pdf \(möglicherweise in englischer Sprache\)|  
|WS\-Secure Conversation|http:\/\/msdn.microsoft.com\/ws\/2005\/02\/ws\-secure\-conversation\/ \(möglicherweise in englischer Sprache\)|  
|WS\-Trust|http:\/\/msdn.microsoft.com\/ws\/2005\/02\/ws\-trust\/ \(möglicherweise in englischer Sprache\)|  
|Anwendungshinweis:<br /><br /> Verwenden von WS\-Trust für TLS Handshake|Wird veröffentlicht|  
|Anwendungshinweis:<br /><br /> Verwenden von WS\-Trust für SPNEGO|Wird veröffentlicht|  
|Anwendungshinweis:<br /><br /> Webdienste\-Adressierungsendpunktverweise und \-identität|Wird veröffentlicht|  
|WS\-SecurityPolicy 1.1<br /><br /> \(2005\/07\)|http:\/\/msdn.microsoft.com\/ws\/2005\/07\/ws\-security\-policy\/ \(möglicherweise in englischer Sprache\)<br /><br /> Wurde gemäß den an das OASIS WS\-SX Technical Committee \(http:\/\/www.oasis\-open.org\/archives\/ws\-sx\/200512\/msg00017.html\) übermittelten Fehlerberichten geändert|  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], Version 1, bietet 17 Authentifizierungsmodi, die als Basis für die Webdienste\-Sicherheitskonfiguration verwendet werden können.  Jeder Modus wird für einen allgemeinen Satz von Bereitstellungsanforderungen optimiert, z.&\#160;B.:  
  
-   Anmeldeinformationen, die zum Authentifizieren von Client und Dienst verwendet werden  
  
-   Nachrichten\- oder Transportsicherheitsschutzmechanismen.  
  
-   Nachrichtenaustauschmuster  
  
|Authentifizierungsmodus|Clientauthentifizierung|Serverauthentifizierung|Modus|  
|-----------------------------|-----------------------------|-----------------------------|-----------|  
|UserNameOverTransport|Benutzername\/Kennwort|X509|Transport|  
|CertificateOverTransport|X509|X509|Transport|  
|KerberosOverTransport.|Windows|X509|Transport|  
|IssuedTokenOverTransport|Verbunden|X509|Transport|  
|SspiNegotiatedOverTransport|Windows Sspi wurde verhandelt|Windows Sspi wurde verhandelt|Transport|  
|AnonymousForCertificate|Keine|X509|Meldung|  
|UserNameForCertificate|Benutzername\/Kennwort|X509|Meldung|  
|MutualCertificate|X509|X509|Meldung|  
|MutualCertificateDuplex|X509|X509|Meldung|  
|IssuedTokenForCertificate|Verbunden|X509|Meldung|  
|Kerberos|Windows|Windows|Meldung|  
|IssuedToken|Verbunden|Verbunden|Meldung|  
|SspiNegotiated|Windows Sspi wurde verhandelt|Windows Sspi wurde verhandelt|Meldung|  
|AnonymousForSslNegotiated|Keine|X509, TLS\-Nego|Meldung|  
|UserNameForSslNegotiated|Benutzername\/Kennwort|X509, TLS\-Nego|Meldung|  
|MutualSslNegotiated|X509|X509, TLS\-Nego|Meldung|  
|IssuedTokenForSslNegotiated|Verbunden|X509, TLS\-Nego|Meldung|  
  
 Endpunkte, die solche Authentifizierungsmodi verwenden, können ihre Sicherheitsanforderungen über WS\-SecurityPolicy \(WS\-SP\) ausdrücken.  Dieses Dokument beschreibt die Struktur der Sicherheitsheader und der Infrastrukturnachrichten für jeden Authentifizierungsmodus und bietet Richtlinien\- und Nachrichtenbeispiele.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] setzt WS\-SecureConversation ein, um sicheren Sitzungssupport für den Schutz eines mehrteiligen Nachrichtenaustauschs zwischen Anwendungen zu bieten.  Weitere Informationen zur Implementierung finden Sie unten unter "Sichere Sitzungen".  
  
 Zusätzlich zu den Authentifizierungsmodi bietet [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] Einstellungen zum Kontrollieren der benutzerdefinierten Schutzmechanismen, die für die meisten auf Nachrichtensicherheit basierenden Authentifizierungsmodi gelten, z. B.: Reihenfolge von Signatur gg. Verschlüsselungsvorgängen, Algorithmussuites, Schlüsselableitung und Signaturbestätigung.  
  
 Die folgenden XML\-Präfixe und \-Namespaces werden in diesem Dokument verwendet.  
  
|Präfix|Namespace|  
|------------|---------------|  
|s|http:\/\/www.w3.org\/2003\/05\/soap\-envelope|  
|sp|http:\/\/schemas.xmlsoap.org\/ws\/2005\/07\/securitypolicy|  
|a|http:\/\/www.w3.org\/2005\/08\/addressing \(möglicherweise in englischer Sprache\)|  
|wsse|TBD – OASIS WSS 1,0 URI|  
|wsse11|TBD – OASIS WSS 1.1 URI|  
|wsu|TBD – OASIS WSS 1.0 Utility URI|  
|ds|TBD – W3C XMLDSig URI|  
|wst|TBD – WS\-Trust 2005\/02 URI|  
|wssc|TBD – WS\-SecureConversation 2005\/02 URI|  
|wsaw|TBD – WS\-Addressing\-Richtliniennamespace|  
|wsp|http:\/\/schemas.xmlsoap.org\/ws\/2004\/09\/policy|  
|mssp|http:\/\/schemas.microsoft.com\/ws\/2005\/07\/securitypolicy|  
  
## 1.Tokenprofile  
 Webdienst\-Sicherheitsspezifikationen stellen Anmeldeinformationen als Sicherheitstoken dar.  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] unterstützt die folgenden Tokentypen:  
  
### 1.1 UsernameToken  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] befolgt UsernameToken10\- und UsernameToken11\-Profile mit den folgenden Einschränkungen:  
  
 Das R1101 PasswordType\-Attribut auf Element UsernameToken\\Password MUSS entweder weggelassen werden oder über den Wert \#PasswordText \(Standard\) verfügen.  
  
 Man kann \#PasswordDigest über Erweiterbarkeit implementieren.  Es wurde beobachtet, dass \#PasswordDigest oft für einen Kennwortschutzmechanismus gehalten wurde, der sicher genug ist.  Aber \#PasswordDigest kann nicht als Ersatz für eine Verschlüsselung von UsernameToken dienen.  Das primäre Ziel von \#PasswordDigest ist ein Schutz vor Replay\-Angriffen.  In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Authentifizierungsmodi werden Replay\-Angriffsbedrohungen durch die Nutzung von Nachrichtensignaturen verringert.  
  
 B1102 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] gibt nie die Unterelemente "Nonce" und "Created" von "UsernameToken" aus.  
  
 Diese Unterelemente sollen die Replay\-Erkennung unterstützen.  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] verwendet stattdessen Nachrichtensignaturen.  
  
 OASIS WSS SOAP Message Security UsernameToken Profile&\#160;1.1 \(UsernameToken11\) hat eine Schlüsselableitung der Kennwortfunktion eingeführt.  
  
 B1103 Das UsernameToken\-Kennwort DARF NICHT für die Schlüsselableitung und daher nicht für kryptografische Vorgänge verwendet werden.  
  
 Begründung: Kennwörter werden im Allgemeinen als zu schwach für die Verwendung in kryptografischen Vorgängen angesehen.  
  
### 1.2 X509 Token  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] unterstützt X509v3\-Zertifikate als Anmeldeinformationstyp und folgt X509TokenProfile1.0 und X509TokenProfile1.1 mit den folgenden Einschränkungen:  
  
 R1201 Das ValueType\-Attribut auf dem BinarySecurityToken\-Element muss den Wert \#X509v3 besitzen, wenn es ein X509v3\-Zertifikat enthält.  
  
 WSS X509 Token Profile 1.0 und 1.1 definieren auch \#X509PKIPathv1 und \#PKCS7 als Werttypen.  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] unterstützt diese Typen nicht.  
  
 R1202 Wenn eine SubjectKeyIdentifier \(SKI\)\-Erweiterung in einem X509\-Zertifikat vorliegt, sollte wsse:KeyIdentifier als externe Referenz für das Token verwendet werden, wobei das ValueType\-Attribut \#X509SubjectKeyIdentifier und sein Inhalt der base64\-codierte Wert der SKI\-Erweiterung des Zertifikats ist.  
  
 SKI\-Verweise werden überall implementiert und haben sich als äußerst interoperabler Typ für externe Verweise erwiesen.  
  
 R1203 Ein externer Verweis auf das X509\-Sicherheitstoken SOLLTE NICHT ds:X509IssuerSerial verwenden.  
  
 R1204 Wenn X509TokenProfile1.1 verwendet wird, SOLLTE eine externe Referenz auf das X509\-Sicherheitstoken den Fingerabdruck, der von WS\-Sicherheit&\#160;1.1 eingeführt wird, verwenden.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] unterstützt X509IssuerSerial.  Es gibt jedoch Interoperabilitätsprobleme mit X509IssuerSerial: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] verwendet eine Zeichenfolge, um zwei Werte von X509IssuerSerial zu vergleichen.  Beim Neuordnen von Komponenten des Betreffsnamens und dem Senden eines Verweises auf ein Zertifikat an einen [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Dienst wird er möglicherweise nicht gefunden.  
  
### 1.3 Kerberos\-Token  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] unterstützt mit den folgenden Einschränkungen KerberosTokenProfile1.1 für den Zweck der Windows\-Authentifizierung:  
  
 R1301 Ein Kerberos\-Token muss den Wert eines GSS\-ummantelten Kerberos&\#160;v4&\#160;AP\_REQ tragen, gemäß der Definition in GSS\_API und der Kerberos\-Spezifikation, und muss das ValueType\-Attribut mit dem Wert \#GSS\_Kerberosv5\_AP\_REQ besitzen.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] verwendet einen GSS\-ummantelten Kerberos AP\-REQ und keinen reinen AP\-REQ.  Hierbei handelt es sich um eine empfohlene Vorgehensweise bezüglich der Sicherheit.  
  
### 1.4 SAML v1.1 Token  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] unterstützt WSS SAML Token\-Profile&\#160;1.0 und&\#160;1.1 für SAML\-v1.1\-Token.  Es ist möglich, andere Versionen von SAML\-Tokenformaten zu implementieren.  
  
### 1.5 Sicherheitskontexttoken  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] unterstützt das in WS\-SecureCoversation eingeführte Sicherheitskontexttoken \(SCT\).  SCT wird verwendet, um einen Sicherheitskontext darzustellen, der in SecureConversation genauso etabliert ist wie in den Binärverhandlungsprotokollen TLS und SSPI \(siehe unten\).  
  
## 2.Allgemeine Nachrichtensicherheitsparameter  
  
### 2.1 TimeStamp  
 Die <xref:System.ServiceModel.Channels.SecurityBindingElement.IncludeTimestamp%2A>\-Eigenschaft der <xref:System.ServiceModel.Channels.SecurityBindingElement>\-Klasse steuert, ob ein Zeitstempel vorhanden ist.  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] serialisiert wsse:TimeStamp immer mit dem wsse:Created\-Feld und dem wsse:Expires\-Feld.  Der wsse:TimeStamp wird immer signiert, wenn Signatur verwendet wird.  
  
### 2.2 Schutzreihenfolge  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] unterstützt die Nachrichtenschutzreihenfolgen "Sign Before Encrypt" und "Encrypt Before Sign" \(Sicherheitsrichtlinie&\#160;1.1\). "  Sign Before Encrypt" wird u. a. aus den folgenden Gründen empfohlen: Mit Encrypt Before Sign geschützte Nachrichten sind Signaturersatzangriffen ausgesetzt, sofern der WS\-Sicherheit 1.1 SignatureConfirmation\-Mechanismus nicht verwendet wird, und eine Signatur über verschlüsselten Inhalt erschwert die Überprüfung.  
  
### 2.3 Signaturschutz  
 Wenn Encrypt Before Sign verwendet wird, ist es empfehlenswert, die Signatur zu schützen, um Brute\-Force\-Angriffe zu verhindern, die versuchen, den verschlüsselten Inhalt oder den Signaturschlüssel zu erraten \(besonders dann, wenn ein benutzerdefiniertes Token zusammen mit schwachen Schlüsselmaterialien verwendet wird\).  
  
### 2.4 Algorithmussuites  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] unterstützt alle in der Sicherheitsrichtlinie&\#160;1.1 aufgeführten Algorithmussuites.  
  
### 2.5 Schlüsselableitung  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] verwendet die "Schlüsselableitung für symmetrische Schlüssel" gemäß ihrer Beschreibung in WS\-SecureConversation.  
  
### 2.6 Signaturbestätigung  
 Signaturbestätigung kann als Schutz gegen Angriffe von Mittelsmännern eingesetzt werden, um den Signatursatz zu schützen.  
  
### 2.7 Sicherheitsheader\-Layout  
 Jeder Authentifizierungsmodus beschreibt ein bestimmtes Layout für den Sicherheitsheader.  Elemente innerhalb des Sicherheitsheaders sind teilweise geordnet.  Um die Reihenfolge der untergeordneten Sicherheitsheaderelemente zu definieren, definiert die WS\-Sicherheitsrichtlinie die folgenden Sicherheitsheader\-Layoutmodi:  
  
|||  
|-|-|  
|Strict|Dem Sicherheitsheader werden Elemente gemäß den durchnummerierten Layout\-Regeln, die im Abschnitt&\#160;7.7.1 der Sicherheitsrichtlinien beschrieben werden, und gemäß dem allgemeinen Prinzip der "Deklaration vor der Verwendung" hinzugefügt.|  
|Lax|Die Elemente werden dem Sicherheitsheader in einer beliebigen Reihenfolge hinzugefügt, die der WSS: SOAP Message Security entspricht.|  
|LaxTimestampFirst|Ebenso wie Lax, nur dass das erste Element im Sicherheitsheader ein wsse:Timestamp sein muss|  
|LaxTimestampLast|Ebenso wie Lax, nur dass das letzte Element im Sicherheitsheader ein wsse:Timestamp sein muss|  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] unterstützt alle vier Modi für das Sicherheitsheader\-Layout.  Sicherheitsheader\-Struktur und Nachrichtenbeispiele für die Authentifizierungsmodi unten folgen dem "Strict"\-Modus.  
  
## 2.Allgemeine Nachrichtensicherheitsparameter  
 Dieser Abschnitt bietet Beispielrichtlinien für jeden Authentifizierungsmodus, zusammen mit Beispielen, die die Sicherheitsheader\-Struktur in Nachrichten, die zwischen Client und Dienst ausgetauscht werden, zeigen.  
  
### 6.1 Transportschutz  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] stellt fünf Authentifizierungsmodi bereit, die sicheren Transport verwenden, um Nachrichten zu schützen: UserNameOverTransport, CertificateOverTransport, KerberosOverTransport, IssuedTokenOverTransport und SspiNegotiatedOverTransport.  
  
 Diese Authentifizierungsmodi werden mit der in der Sicherheitsrichtlinie beschriebenen Transportbindung erstellt.  Für den UserNameOverTransport\-Authentifizierungsmodus ist das UsernameToken ein signiertes unterstützendes Token.  Für die anderen Authentifizierungsmodi wird das Token als signiertes unterzeichnendes Token angezeigt.  Anhang&\#160;C.1.2 und&\#160;C.1.3 von SecurityPolicy beschreiben detailliert das Sicherheitsheader\-Layout.  Die folgenden Beispielsicherheitsheader zeigen das "Strict"\-Layout für einen gegebenen Authentifizierungsmodus an.  
  
 Der Wert der "Derived\-Keys"\-Eigenschaft für die Token ist in allen Fällen "false".  
  
 Die Werte der verschiedenen Eigenschaften der Transportbindung sind wie folgt:  
  
 Timestamp: true  
  
 Sicherheitsheader\-Layout: Strict  
  
 Algorithmussuite: Basic256  
  
#### 6.1.1 UsernameOverTransport  
 Bei diesem Authentifizierungsmodus authentifiziert sich der Client über ein Benutzernamentoken, das auf der SOAP\-Schicht als signiertes unterstützendes Token angezeigt wird, das immer vom Initiator an den Empfänger gesendet wird.  Der Dienst wird über ein X.509\-Zertifikat auf der Transportschicht authentifiziert.  Die verwendete Bindung ist eine Transportbindung.  
  
 Richtlinie  
  
```  
<wsp:Policy wsu:Id='UsernameOverTransport_policy' >  
  <wsp:ExactlyOne>  
    <wsp:All>  
      <sp:TransportBinding >  
        <wsp:Policy>  
          <sp:TransportToken>  
            <wsp:Policy>  
              <sp:HttpsToken RequireClientCertificate='false' />   
            </wsp:Policy>  
          </sp:TransportToken>  
          <sp:AlgorithmSuite>  
            <wsp:Policy>  
              <sp:Basic256 />   
            </wsp:Policy>  
          </sp:AlgorithmSuite>  
          <sp:Layout>  
            <wsp:Policy>  
              <sp:Strict />   
            </wsp:Policy>  
          </sp:Layout>  
          <sp:IncludeTimestamp />   
        </wsp:Policy>  
      </sp:TransportBinding>  
      <sp:SignedSupportingTokens >  
        <wsp:Policy>  
          <sp:UsernameToken   
sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
            <wsp:Policy>  
              <sp:WssUsernameToken10 />   
            </wsp:Policy>  
          </sp:UsernameToken>  
        </wsp:Policy>  
      </sp:SignedSupportingTokens>  
      <sp:Wss11 >  
        <wsp:Policy>  
          <sp:MustSupportRefKeyIdentifier />   
          <sp:MustSupportRefIssuerSerial />   
          <sp:MustSupportRefThumbprint />   
          <sp:MustSupportRefEncryptedKey />   
        </wsp:Policy>  
      </sp:Wss11>  
      <sp:Trust10 >  
        <wsp:Policy>  
          <sp:MustSupportIssuedTokens />   
          <sp:RequireClientEntropy />   
          <sp:RequireServerEntropy />   
        </wsp:Policy>  
      </sp:Trust10>  
      <wsaw:UsingAddressing />   
    </wsp:All>  
  </wsp:ExactlyOne>  
</wsp:Policy>  
```  
  
 Sicherheitsheader\-Layout  
  
 Anforderung  
  
```  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <wsse:UsernameToken ... >  
  ...  
  </wsse:UsernameToken>  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
</wsse:Security>  
```  
  
#### 6.1.2 CertificateOverTransport  
 Bei diesem Authentifizierungsmodus authentifiziert sich der Client über ein X.509\-Zertifikat, das auf der SOAP\-Schicht als ausstellendes unterstützendes Token angezeigt wird, das immer vom Initiator an den Empfänger gesendet wird.  Der Dienst wird über ein X.509\-Zertifikat auf der Transportschicht authentifiziert.  Die verwendete Bindung ist eine Transportbindung.  
  
 Richtlinie  
  
```  
<wsp:Policy wsu:Id='CertificateOverTransport_policy' >  
  <wsp:ExactlyOne>  
    <wsp:All>  
      <sp:TransportBinding xmlns:sp='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy' >  
        <wsp:Policy>  
          <sp:TransportToken>  
            <wsp:Policy>  
             <sp:HttpsToken RequireClientCertificate='false' />   
            </wsp:Policy>  
          </sp:TransportToken>  
          <sp:AlgorithmSuite>  
            <wsp:Policy>  
              <sp:Basic256 />   
            </wsp:Policy>  
          </sp:AlgorithmSuite>  
          <sp:Layout>  
            <wsp:Policy>  
              <sp:Strict />   
            </wsp:Policy>  
          </sp:Layout>  
          <sp:IncludeTimestamp />   
        </wsp:Policy>  
      </sp:TransportBinding>  
      <sp:EndorsingSupportingTokens>  
        <wsp:Policy>  
          <sp:X509Token   
sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
            <wsp:Policy>  
              <sp:RequireThumbprintReference />   
              <sp:WssX509V3Token10 />   
            </wsp:Policy>  
          </sp:X509Token>  
          <sp:SignedParts>  
            <sp:Header Name='To'   
Namespace='http://www.w3.org/2005/08/addressing' />   
          </sp:SignedParts>  
        </wsp:Policy>  
      </sp:EndorsingSupportingTokens>  
      <sp:Wss11>  
        <wsp:Policy>  
          <sp:MustSupportRefKeyIdentifier />   
          <sp:MustSupportRefIssuerSerial />   
          <sp:MustSupportRefThumbprint />   
          <sp:MustSupportRefEncryptedKey />   
        </wsp:Policy>  
      </sp:Wss11>  
      <sp:Trust10>  
        <wsp:Policy>  
          <sp:MustSupportIssuedTokens />   
          <sp:RequireClientEntropy />   
          <sp:RequireServerEntropy />   
        </wsp:Policy>  
      </sp:Trust10>  
      <wsaw:UsingAddressing />   
    </wsp:All>  
  </wsp:ExactlyOne>  
</wsp:Policy>  
```  
  
 Sicherheitsheader\-Layout  
  
 Anforderung  
  
```  
<wsse:Security s:mustUnderstand="1">  
  <wse:Timestamp u:Id="_0">  
  ...  
  </wse:Timestamp>  
  <wsse:BinarySecurityToken>  
  ...  
  </wsse:BinarySecurityToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<o:Security>  
  <u:Timestamp u:Id="_0">  
  ...  
  </u:Timestamp>  
</o:Security>  
```  
  
#### 6.1.3 IssuedTokenOverTransport  
 In diesem Authentifizierungsmodus unterstützt der Client den Dienst als solchen nicht, sondern präsentiert ein Token, das von einem Sicherheitstokendienst \(Security Token Service, STS\) ausgegeben wird, und einen freigegebenen Schlüssel.  Das ausgegebene Token wird auf der SOAP\-Schicht als ausstellendes unterstützendes Token angezeigt, das immer vom Initiator an den Empfänger gesendet wird.  Der Dienst wird über ein X.509\-Zertifikat auf der Transportschicht authentifiziert.  Die Bindung ist eine Transportbindung.  
  
 Richtlinie  
  
```  
<wsp:Policy wsu:Id='IssuedTokenOverTransport_policy' >  
  <wsp:ExactlyOne>  
    <wsp:All>  
      <sp:TransportBinding >  
        <wsp:Policy>  
          <sp:TransportToken>  
            <wsp:Policy>  
              <sp:HttpsToken RequireClientCertificate='false' />   
            </wsp:Policy>  
          </sp:TransportToken>  
          <sp:AlgorithmSuite>  
            <wsp:Policy>  
              <sp:Basic256 />   
            </wsp:Policy>  
          </sp:AlgorithmSuite>  
          <sp:Layout>  
            <wsp:Policy>  
              <sp:Strict />   
            </wsp:Policy>  
          </sp:Layout>  
          <sp:IncludeTimestamp />   
        </wsp:Policy>  
      </sp:TransportBinding>  
      <sp:EndorsingSupportingTokens>  
        <wsp:Policy>  
          <sp:IssuedToken   
sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
            <sp:RequestSecurityTokenTemplate>  
              <wst:KeyType>  
              http://schemas.xmlsoap.org/ws/2005/02/trust/SymmetricKey  
              </wst:KeyType>   
            </sp:RequestSecurityTokenTemplate>  
            <wsp:Policy>  
              <sp:RequireInternalReference />   
            </wsp:Policy>  
          </sp:IssuedToken>  
          <sp:SignedParts>  
            <sp:Header Name='To'   
Namespace='http://www.w3.org/2005/08/addressing' />   
          </sp:SignedParts>  
        </wsp:Policy>  
      </sp:EndorsingSupportingTokens>  
      <sp:Wss11>  
        <wsp:Policy>  
          <sp:MustSupportRefKeyIdentifier />   
          <sp:MustSupportRefIssuerSerial />   
          <sp:MustSupportRefThumbprint />   
          <sp:MustSupportRefEncryptedKey />   
        </wsp:Policy>  
      </sp:Wss11>  
      <sp:Trust10>  
        <wsp:Policy>  
          <sp:MustSupportIssuedTokens />   
          <sp:RequireClientEntropy />   
          <sp:RequireServerEntropy />   
        </wsp:Policy>  
      </sp:Trust10>  
      <wsaw:UsingAddressing />   
    </wsp:All>  
  </wsp:ExactlyOne>  
</wsp:Policy>  
```  
  
 Sicherheitsheader\-Layout  
  
 Anforderung  
  
```  
<wsse:Security s:mustUnderstand="1" >  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <saml:Assertion ...>  
  ...  
  </saml:Assertion>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<wsse:Security>  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
</wsse:Security>  
```  
  
#### 6.1.4 KerberosOverTransport  
 Mit diesem Authentifizierungsmodus wird der Client mit einem Kerberos\-Ticket dem Dienst gegenüber authentifiziert.  Das Kerberos\-Token wird auf der SOAP\-Schicht als ausstellendes unterstützendes Token angezeigt.  Der Dienst wird über ein X.509\-Zertifikat auf der Transportschicht authentifiziert.  Die Bindung ist eine Transportbindung.  
  
 Richtlinie  
  
```  
<wsp:Policy wsu:Id='KerberosOverTransport_policy' >  
  <wsp:ExactlyOne>  
    <wsp:All>  
      <sp:TransportBinding>  
        <wsp:Policy>  
          <sp:TransportToken>  
            <wsp:Policy>  
              <sp:HttpsToken RequireClientCertificate='false' />   
            </wsp:Policy>  
          </sp:TransportToken>  
          <sp:AlgorithmSuite>  
            <wsp:Policy>  
              <sp:Basic128 />   
            </wsp:Policy>  
          </sp:AlgorithmSuite>  
          <sp:Layout>  
            <wsp:Policy>  
              <sp:Strict />   
            </wsp:Policy>  
          </sp:Layout>  
          <sp:IncludeTimestamp />   
        </wsp:Policy>  
      </sp:TransportBinding>  
      <sp:EndorsingSupportingTokens>  
        <wsp:Policy>  
          <sp:KerberosToken  
sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/Once' >  
            <wsp:Policy>  
              <sp:WssGssKerberosV5ApReqToken11 />   
            </wsp:Policy>  
          </sp:KerberosToken>  
          <sp:SignedParts>  
            <sp:Header Name='To'   
Namespace='http://www.w3.org/2005/08/addressing' />   
          </sp:SignedParts>  
        </wsp:Policy>  
      </sp:EndorsingSupportingTokens>  
      <sp:Wss11>  
        <wsp:Policy>  
          <sp:MustSupportRefKeyIdentifier />   
          <sp:MustSupportRefIssuerSerial />   
          <sp:MustSupportRefThumbprint />   
          <sp:MustSupportRefEncryptedKey />   
        </wsp:Policy>  
      </sp:Wss11>  
      <sp:Trust10>  
        <wsp:Policy>  
          <sp:MustSupportIssuedTokens />   
          <sp:RequireClientEntropy />   
          <sp:RequireServerEntropy />   
        </wsp:Policy>  
      </sp:Trust10>  
      <wsaw:UsingAddressing />   
    </wsp:All>  
  </wsp:ExactlyOne>  
</wsp:Policy>  
```  
  
 Sicherheitsheader\-Layout  
  
 Anforderung  
  
```  
<wsse:Security s:mustUnderstand="1" >  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <wsse:BinarySecurityToken ValueType="...#GSS_Kerberosv5_AP_REQ">  
  ...  
  </wsse:BinarySecurityToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<wsse:Security>  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
</wsse:Security>  
```  
  
#### 6.1.5 SspiNegotiatedOverTransport  
 Bei diesem Modus wird ein Aushandlungsprotokoll verwendet, um Client\- und Serverauthentifizierung auszuführen.  Wenn möglich wird Kerberos verwendet, ansonsten NTLM.  Das resultierende SCT wird auf der SOAP\-Schicht als ausstellendes unterstützendes Token angezeigt, das immer vom Initiator an den Empfänger gesendet wird.  Der Dienst wird zusätzlich auf der Transportschicht über ein X.509\-Zertifikat authentifiziert.  Die verwendete Bindung ist eine Transportbindung. "  SPNEGO" \(Aushandlung\) beschreibt, wie [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] das binäre SSPI\-Aushandlungsprotokoll zusammen mit WS\-Trust verwendet.  Die Sicherheitsheaderbeispiele in diesem Abschnitt gelten, nachdem der SCT durch den SPNEGO\-Handshake eingeführt wurde.  
  
 Richtlinie  
  
```  
<wsp:Policy wsu:Id='SspiNegotiatedOverTransport_policy' >  
  <wsp:ExactlyOne>  
    <wsp:All>  
      <sp:TransportBinding>  
        <wsp:Policy>  
          <sp:TransportToken>  
            <wsp:Policy>  
              <sp:HttpsToken RequireClientCertificate='false' />   
            </wsp:Policy>  
          </sp:TransportToken>  
          <sp:AlgorithmSuite>  
            <wsp:Policy>  
              <sp:Basic256 />   
            </wsp:Policy>  
          </sp:AlgorithmSuite>  
          <sp:Layout>  
            <wsp:Policy>  
              <sp:Strict />   
            </wsp:Policy>  
          </sp:Layout>  
          <sp:IncludeTimestamp />   
        </wsp:Policy>  
      </sp:TransportBinding>  
      <sp:EndorsingSupportingTokens>  
        <wsp:Policy>  
          <sp:SpnegoContextToken   
sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
            <wsp:Policy />   
          </sp:SpnegoContextToken>  
          <sp:SignedParts>  
            <sp:Header Name='To'   
Namespace='http://www.w3.org/2005/08/addressing' />   
          </sp:SignedParts>  
        </wsp:Policy>  
      </sp:EndorsingSupportingTokens>  
      <sp:Wss11>  
        <wsp:Policy>  
          <sp:MustSupportRefKeyIdentifier />   
          <sp:MustSupportRefIssuerSerial />   
          <sp:MustSupportRefThumbprint />   
          <sp:MustSupportRefEncryptedKey />   
        </wsp:Policy>  
      </sp:Wss11>  
      <sp:Trust10>  
        <wsp:Policy>  
          <sp:MustSupportIssuedTokens />   
          <sp:RequireClientEntropy />   
          <sp:RequireServerEntropy />   
        </wsp:Policy>  
      </sp:Trust10>  
      <wsaw:UsingAddressing />   
    </wsp:All>  
  </wsp:ExactlyOne>  
</wsp:Policy>  
```  
  
### Beispiele für Sicherheitsheader  
 Sobald das Sicherheitskontexttoken einmal durch SPNEGO unter Verwendung der WS\-Trust\-Binäraushandlung eingeführt wurde, besitzen die Anwendungsnachrichten Sicherheitsheader mit der folgenden Struktur.  
  
 Anforderung  
  
```  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <wssc:SecurityContextToken u:Id="uuid-2202746a-7725-453d-8747-809cb718dab0-29" >  
  ...  
  </wssc:SecurityContextToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
</wsse:Security>  
```  
  
### 6.2 Verwenden von X.509\-Zertifikaten zur Dienstauthentifizierung  
 In diesem Abschnitt werden die folgenden Authentifizierungsmodi beschrieben: MutualCertificate WSS1.0, Mutual CertificateDuplex, MutualCertificate WSS1.1, AnonymousForCertificate, UserNameForCertificate und IssuedTokenForCertificate.  
  
#### 6.2.1 MutualCertificate WSS1.0  
 Bei diesem Authentifizierungsmodus authentifiziert sich der Client über ein X.509\-Zertifikat, das auf der SOAP\-Schicht als das Initiatortoken angezeigt wird.  Der Dienst wird ebenfalls über ein X.509\-Zertifikat authentifiziert.  
  
 Die verwendete Bindung ist eine asymmetrische Bindung mit den folgenden Eigenschaftswerten:  
  
 Initiator\-Token: das X.509\-Zertifikat des Clients, wobei der Inclusion\-Modus auf ...\/IncludeToken\/AlwaysToRecipient festgelegt ist  
  
 Empfängertoken: das X.509\-Zertifikat des Servers, wobei der Inclusion\-Modus auf ...\/IncludeToken\/Never festgelegt ist  
  
 Tokenschutz: False  
  
 Ganze Header\- und Textsignaturen: True  
  
 Schutzreihenfolge: SignBeforeEncrypt  
  
 Signaturverschlüsselung: True  
  
 Richtlinie  
  
```  
<wsp:Policy wsu:Id='MutualCertificate_WSS10_policy' >  
  <wsp:ExactlyOne>  
    <wsp:All>  
      <sp:AsymmetricBinding>  
        <wsp:Policy>  
          <sp:InitiatorToken>  
            <wsp:Policy>  
              <sp:X509Token   
sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
                <wsp:Policy>  
                  <sp:WssX509V3Token10 />   
                </wsp:Policy>  
              </sp:X509Token>  
            </wsp:Policy>  
          </sp:InitiatorToken>  
          <sp:RecipientToken>  
            <wsp:Policy>  
              <sp:X509Token   
sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/Never' >  
                <wsp:Policy>  
                  <sp:WssX509V3Token10 />   
                </wsp:Policy>  
              </sp:X509Token>  
            </wsp:Policy>  
          </sp:RecipientToken>  
          <sp:AlgorithmSuite>  
            <wsp:Policy>  
              <sp:Basic256 />   
            </wsp:Policy>  
          </sp:AlgorithmSuite>  
          <sp:Layout>  
            <wsp:Policy>  
              <sp:Strict />   
            </wsp:Policy>  
          </sp:Layout>  
          <sp:IncludeTimestamp />   
          <sp:EncryptSignature />   
          <sp:OnlySignEntireHeadersAndBody />   
        </wsp:Policy>  
      </sp:AsymmetricBinding>  
      <sp:Wss10>  
        <wsp:Policy>  
          <sp:MustSupportRefKeyIdentifier />   
          <sp:MustSupportRefIssuerSerial />   
        </wsp:Policy>  
      </sp:Wss10>  
      <sp:Trust10>  
        <wsp:Policy>  
          <sp:MustSupportIssuedTokens />   
          <sp:RequireClientEntropy />   
          <sp:RequireServerEntropy />   
        </wsp:Policy>  
      </sp:Trust10>  
      <wsaw:UsingAddressing />   
    </wsp:All>  
  </wsp:ExactlyOne>  
</wsp:Policy>  
```  
  
### Sicherheitsheaderbeispiele: SignBeforeEncrypt, EncryptSignature  
 Anforderung  
  
```  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <wsse:BinarySecurityToken>  
  ...  
  </wsse:BinarySecurityToken>  
  <xenc:EncryptedKey>  
  ...  
    <xenc:ReferenceList>  
    ...  
    </xenc:ReferenceList>  
  </xenc:EncryptedKey>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <xenc:EncryptedKey>  
  ...  
    <xenc:ReferenceList>  
    ...  
    </xenc:ReferenceList>  
  </xenc:EncryptedKey>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
 Sicherheitsheaderbeispiele: EncryptBeforeSign  
  
 Anforderung  
  
```  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <wsse:BinarySecurityToken>  
  ...  
  </wsse:BinarySecurityToken>  
  <xenc:EncryptedKey>  
  ...  
  </xenc:EncryptedKey>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <xenc:EncryptedKey>  
  ...  
  </xenc:EncryptedKey>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
#### 6.2.2 MutualCertificateDuplex  
 Bei diesem Authentifizierungsmodus authentifiziert sich der Client über ein X.509\-Zertifikat, das auf der SOAP\-Schicht als das Initiatortoken angezeigt wird.  Der Dienst wird ebenfalls über ein X.509\-Zertifikat authentifiziert.  
  
 Die verwendete Bindung ist eine asymmetrische Bindung mit den folgenden Eigenschaftswerten:  
  
 Initiator\-Token: das X.509\-Zertifikat des Clients, wobei der Inclusion\-Modus auf ...\/IncludeToken\/AlwaysToRecipient festgelegt ist  
  
 Empfänger\-Token: das X.509\-Zertifikat des Servers, wobei der Inclusion\-Modus auf ...\/IncludeToken\/AlwaysToInitiator festgelegt ist  
  
 Tokenschutz: False  
  
 Ganze Header\- und Textsignaturen: True  
  
 Schutzreihenfolge: SignBeforeEncrypt  
  
 Signaturverschlüsselung: True  
  
 Richtlinie  
  
```  
<wsp:Policy wsu:Id='MutualCertificateDuplex_policy' >  
  <wsp:ExactlyOne>  
    <wsp:All>  
      <sp:AsymmetricBinding>  
        <wsp:Policy>  
          <sp:InitiatorToken>  
            <wsp:Policy>  
              <sp:X509Token   
sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
                <wsp:Policy>  
                  <sp:WssX509V3Token10 />   
                </wsp:Policy>  
              </sp:X509Token>  
            </wsp:Policy>  
          </sp:InitiatorToken>  
          <sp:RecipientToken>  
            <wsp:Policy>  
              <sp:X509Token   
sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToInitiator' >  
                <wsp:Policy>  
                  <sp:WssX509V3Token10 />   
                </wsp:Policy>  
              </sp:X509Token>  
            </wsp:Policy>  
          </sp:RecipientToken>  
          <sp:AlgorithmSuite>  
            <wsp:Policy>  
              <sp:Basic256 />   
            </wsp:Policy>  
          </sp:AlgorithmSuite>  
          <sp:Layout>  
            <wsp:Policy>  
              <sp:Strict />   
            </wsp:Policy>  
          </sp:Layout>  
          <sp:IncludeTimestamp />   
          <sp:EncryptSignature />   
          <sp:OnlySignEntireHeadersAndBody />   
        </wsp:Policy>  
      </sp:AsymmetricBinding>  
      <sp:Wss10>  
        <wsp:Policy>  
          <sp:MustSupportRefKeyIdentifier />   
          <sp:MustSupportRefIssuerSerial />   
        </wsp:Policy>  
      </sp:Wss10>  
      <sp:Trust10>  
        <wsp:Policy>  
          <sp:MustSupportIssuedTokens />   
          <sp:RequireClientEntropy />   
          <sp:RequireServerEntropy />   
        </wsp:Policy>  
      </sp:Trust10>  
      <wsaw:UsingAddressing />   
    </wsp:All>  
  </wsp:ExactlyOne>  
</wsp:Policy>  
```  
  
### Sicherheitsheaderbeispiele: SignBeforeEncrypt, EncryptSignature  
 Anforderung und Antwort  
  
```  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <wsse:BinarySecurityToken>  
  ...  
  </wsse:BinarySecurityToken>  
  <xenc:EncryptedKey>  
  ...  
    <xenc:ReferenceList>  
    ...  
    </xenc:ReferenceList>  
  </xenc:EncryptedKey>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
### Sicherheitsheaderbeispiele: EncryptBeforeSign  
 Anforderung und Antwort  
  
```  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <wsse:BinarySecurityToken>  
  ...  
  </wsse:BinarySecurityToken>  
  <xenc:EncryptedKey>  
  ...  
  </xenc:EncryptedKey>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
#### 6.2.3 Verwenden von SymmetricBinding mit X.509\-Dienstauthentifizierung  
 "WSS10" bot lediglich eingeschränkten Support für Szenarien mit X509\-Token.  Beispielsweise gab es keine Möglichkeit, Signatur\- und Verschlüsselungsschutz für Nachrichten bereitzustellen, die nur Dienst\-X509\-Token verwenden. "  WSS11" hat die Verwendung von EncryptedKey als symmetrisches Token eingeführt.  Jetzt könnte ein temporärer Schlüssel, der für das X.509\-Zertifikat verschlüsselt wurde, sowohl für den Anforderungs\- als auch für den Antwortnachrichtenschutz verwendet werden.  Die unten in Abschnitt&\#160;6.4 beschriebenen Authentifizierungsmodi verwenden dieses Muster.  
  
 Die WS\-Sicherheitsrichtlinie beschreibt dieses Muster unter Verwendung von SymmetricBinding mit dem Dienst\-X509\-Token als Schutztoken.  
  
 Die Authentifizierungsmodi AnonymousForCertificate, UsernameForCertificate, MutualCertificate WSS11 und IssuedTokenForCertificate verwenden alle eine ähnliche Instanz von sp:SymmetricBinding mit den folgenden Eigenschaftswerten:  
  
 Schutztoken: das X.509\-Zertifikat des Servers, wobei der Einschlussmodus auf ...\/IncludeToken\/Never festgelegt ist                   
 Tokenschutz: False  
  
 Ganze Header\- und Textsignaturen: True  
  
 Schutzreihenfolge: SignBeforeEncrypt  
  
 Signaturverschlüsselung: True  
  
 Die oben erwähnten Authentifizierungsmodi unterscheiden sich nur durch die unterstützenden Token, die sie verwenden.  AnonymousForCertificate besitzt keine unterstützenden Token, MutualCertificate WSS 1.1 besitzt das X509\-Zertifikat des Clients als unterzeichnendes unterstützendes Token, UserNameForCertificate besitzt ein Benutzernamentoken als signiertes unterstützendes Token und IssuedTokenForCertificate besitzt das ausgestellte Token als unterzeichnendes unterstützendes Token.  
  
 Richtlinie  
  
 Symmetrische Bindung  
  
```  
<wsp:Policy wsu:Id='SymmetricCert_policy' >  
  <wsp:ExactlyOne>  
    <wsp:All>  
      <sp:SymmetricBinding>  
        <wsp:Policy>  
          <sp:ProtectionToken>  
            <wsp:Policy>  
              <sp:X509Token   
sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/Never' >  
                <wsp:Policy>  
                  <sp:RequireDerivedKeys />   
                  <sp:RequireThumbprintReference />   
                  <sp:WssX509V3Token10 />   
                </wsp:Policy>  
              </sp:X509Token>  
            </wsp:Policy>  
          </sp:ProtectionToken>  
          <sp:AlgorithmSuite>  
            <wsp:Policy>  
              <sp:Basic256 />   
            </wsp:Policy>  
          </sp:AlgorithmSuite>  
          <sp:Layout>  
            <wsp:Policy>  
              <sp:Strict />   
            </wsp:Policy>  
          </sp:Layout>  
          <sp:IncludeTimestamp />   
          <sp:EncryptSignature />   
          <sp:OnlySignEntireHeadersAndBody />  
        </wsp:Policy>  
      </sp:SymmetricBinding>  
      <!-- Supporting Token Assertions appear here -->  
      ...  
      <sp:Wss11>  
        <wsp:Policy>  
          <sp:MustSupportRefKeyIdentifier />   
          <sp:MustSupportRefIssuerSerial />   
          <sp:MustSupportRefThumbprint />   
          <sp:MustSupportRefEncryptedKey />   
          <sp:RequireSignatureConfirmation />   
        </wsp:Policy>  
      </sp:Wss11>  
      <sp:Trust10>  
        <wsp:Policy>  
          <sp:MustSupportIssuedTokens />   
          <sp:RequireClientEntropy />   
          <sp:RequireServerEntropy />   
        </wsp:Policy>  
      </sp:Trust10>  
      <wsaw:UsingAddressing />   
    </wsp:All>  
  </wsp:ExactlyOne>  
</wsp:Policy>  
```  
  
#### 6.2.4 AnonymousForCertificate  
 Mit diesem Authentifizierungsmodus ist der Client anonym, und der Dienst wird mit einem X.509\-Zertifikat authentifiziert.  Die verwendete Bindung ist eine Instanz einer symmetrischen Bindung gemäß der Beschreibung im Abschnitt&\#160;6.4.2.  
  
 Richtlinie  
  
 Weitere Informationen zu den Bindungen finden Sie unter "Richtlinie" im Abschnitt&\#160;6.2.3.  
  
### Sicherheitsheaderbeispiele: SignBeforeEncrypt, EncryptSignature  
 Anforderung  
  
```  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <xenc:EncryptedKey>  
  ...  
  </xenc:EncryptedKey>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
### Sicherheitsheaderbeispiele: EncryptBeforeSign  
 Anforderung  
  
```  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <xenc:EncryptedKey>  
  ...  
  </xenc:EncryptedKey>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wsse11:SignatureConfirmation />  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
#### 6.2.5 UserNameForCertificate  
 Bei diesem Authentifizierungsmodus authentifiziert sich der Client dem Dienst gegenüber mit einem Benutzernamentoken, das auf der SOAP\-Schicht als signiertes unterstützendes Token angezeigt wird.  Der Dienst wird über ein X.509\-Zertifikat am Client authentifiziert.  Die verwendete Bindung ist eine symmetrische Bindung, deren Schutztoken ein Schlüssel ist, der vom Client generiert und über den öffentlichen Schlüssel des Diensts verschlüsselt wurde.  
  
 Richtlinie  
  
 Weitere Informationen zu den Bindungen finden Sie unter "Richtlinie" im Abschnitt&\#160;6.2.3.  
  
 Signiertes unterstützendes Token  
  
```  
<sp:SignedSupportingTokens>  
  <wsp:Policy>  
    <sp:UsernameToken sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
      <wsp:Policy>  
        <sp:WssUsernameToken10 />   
      </wsp:Policy>  
    </sp:UsernameToken>  
  </wsp:Policy>  
</sp:SignedSupportingTokens>  
```  
  
### Sicherheitsheaderbeispiele: SignBeforeEncrypt, EncryptSignature  
 Anforderung  
  
```  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <xenc:EncryptedKey>  
  ...  
  </xenc:EncryptedKey>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
### Sicherheitsheaderbeispiele: EncryptBeforeSign  
 Anforderung  
  
```  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <xenc:EncryptedKey>  
  ...  
  </xenc:EncryptedKey>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
#### 6.2.6 MutualCertificate \(WSS 1.1\)  
 Bei diesem Authentifizierungsmodus authentifiziert sich der Client über ein X.509\-Zertifikat, das auf der SOAP\-Schicht als ausstellendes unterstützendes Token angezeigt wird.  Der Dienst wird ebenfalls über ein X.509\-Zertifikat authentifiziert.  Die verwendete Bindung ist eine symmetrische Bindung, deren Schutztoken ein Schlüssel ist, der vom Client generiert und über den öffentlichen Schlüssel des Diensts verschlüsselt wurde.  
  
 Richtlinie  
  
 Weitere Informationen zu den Bindungen finden Sie unter "Richtlinie" im Abschnitt&\#160;6.2.3.  
  
 Ausstellendes unterstützendes Token  
  
```  
<sp:EndorsingSupportingTokens>  
  <wsp:Policy>  
    <sp:X509Token sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
      <wsp:Policy>  
        <sp:RequireThumbprintReference />   
        <sp:WssX509V3Token10 />   
      </wsp:Policy>  
    </sp:X509Token>  
  </wsp:Policy>  
</sp:EndorsingSupportingTokens>  
```  
  
### Sicherheitsheaderbeispiele: SignBeforeEncrypt, EncryptSignature  
 Anforderung  
  
```  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <xenc:EncryptedKey>  
  ...  
  </xenc:EncryptedKey>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <wsse:BinarySecurityToken>  
  ...  
  </wsse:BinarySecurityToken>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <wsse:BinarySecurityToken>  
  ...  
  </wsse:BinarySecurityToken>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
### Sicherheitsheaderbeispiele: EncryptBeforeSign  
 Anforderung  
  
```  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <xenc:EncryptedKey>  
  ...  
  </xenc:EncryptedKey>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wsse:BinarySecurityToken>  
  ...  
  </wsse:BinarySecurityToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <xenc:EncryptedKey>  
  ...  
  </xenc:EncryptedKey>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wsse11:SignatureConfirmation />  
  <wsse11:SignatureConfirmation />  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
#### 6.2.7 IssuedTokenForCertificate  
 In diesem Authentifizierungsmodus unterstützt der Client den Dienst als solchen nicht, sondern präsentiert ein Token, das von einem Sicherheitstokendienst \(Security Token Service, STS\) ausgegeben wird, und einen geteilten Schlüssel.  Das ausgestellte Token wird auf der SOAP\-Schicht als ausstellendes unterstützendes Token angezeigt.  Der Dienst wird über ein X.509\-Zertifikat am Client authentifiziert.  Die verwendete Bindung ist eine symmetrische Bindung, deren Schutztoken ein Schlüssel ist, der vom Client generiert und über den öffentlichen Schlüssel des Diensts verschlüsselt wurde.  
  
 Richtlinie  
  
 Weitere Informationen zu den Bindungen finden Sie unter "Richtlinie" im Abschnitt&\#160;6.2.3.  
  
 Ausstellendes unterstützendes Token  
  
```  
<sp:EndorsingSupportingTokens>  
  <wsp:Policy>  
    <sp:IssuedToken sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
      <sp:RequestSecurityTokenTemplate>  
        <wst:KeyType>  
http://schemas.xmlsoap.org/ws/2005/02/trust/SymmetricKey  
       </wst:KeyType>  
     </sp:RequestSecurityTokenTemplate>  
     <wsp:Policy>  
       <sp:RequireDerivedKeys />   
       <sp:RequireInternalReference />   
     </wsp:Policy>  
   </sp:IssuedToken>  
  </wsp:Policy>  
</sp:EndorsingSupportingTokens>  
```  
  
### Sicherheitsheaderbeispiele: SignBeforeEncrypt, EncryptSignature  
 Anforderung  
  
```  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <xenc:EncryptedKey>  
  ...  
  </xenc:EncryptedKey>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <saml:Assertion>  
  ...  
  </saml:Assertion>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
### Sicherheitsheaderbeispiele: EncryptBeforeSign  
 Anforderung  
  
```  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <xenc:EncryptedKey>  
  ...  
  </xenc:EncryptedKey>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <saml:Assertion>  
  ...  
  </saml:Assertion>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wsse11:SignatureConfirmation />  
  <wsse11:SignatureConfirmation />  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
## 6.3 Kerberos  
 Mit diesem Authentifizierungsmodus wird der Client mit einem Kerberos\-Ticket dem Dienst gegenüber authentifiziert.  Dieses gleiche Ticket bietet auch Serverauthentifizierung.  Die verwendete Bindung ist eine symmetrische Bindung mit den folgenden Eigenschaften:  
  
 Schutztoken: Kerberos\-Ticket, Einschlussmodus ist auf ...\/IncludeToken\/Once festgelegt           
 Tokenschutz: False  
  
 Ganze Header\- und Textsignaturen: True  
  
 Schutzreihenfolge: SignBeforeEncrypt  
  
 Signaturverschlüsselung: True  
  
 Richtlinie  
  
```  
<wsp:Policy wsu:Id='Kerberos_policy' >  
  <wsp:ExactlyOne>  
    <wsp:All>  
      <sp:SymmetricBinding>  
        <wsp:Policy>  
          <sp:ProtectionToken>  
            <wsp:Policy>  
              <sp:KerberosToken sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/Once' >  
                <wsp:Policy>  
                  <sp:RequireDerivedKeys />   
                  <sp:WssGssKerberosV5ApReqToken11 />   
                </wsp:Policy>  
              </sp:KerberosToken>  
            </wsp:Policy>  
          </sp:ProtectionToken>  
          <sp:AlgorithmSuite>  
            <wsp:Policy>  
              <sp:Basic128 />   
            </wsp:Policy>  
          </sp:AlgorithmSuite>  
          <sp:Layout>  
            <wsp:Policy>  
              <sp:Strict />   
            </wsp:Policy>  
          </sp:Layout>  
          <sp:IncludeTimestamp />   
          <sp:EncryptSignature />   
          <sp:OnlySignEntireHeadersAndBody />   
        </wsp:Policy>  
      </sp:SymmetricBinding>  
      <sp:Wss11>  
        <wsp:Policy>  
          <sp:MustSupportRefKeyIdentifier />   
          <sp:MustSupportRefIssuerSerial />   
          <sp:MustSupportRefThumbprint />   
          <sp:MustSupportRefEncryptedKey />   
        </wsp:Policy>  
      </sp:Wss11>  
      <sp:Trust10>  
        <wsp:Policy>  
          <sp:MustSupportIssuedTokens />   
          <sp:RequireClientEntropy />   
          <sp:RequireServerEntropy />   
        </wsp:Policy>  
      </sp:Trust10>  
      <wsaw:UsingAddressing />   
    </wsp:All>  
  </wsp:ExactlyOne>  
</wsp:Policy>  
```  
  
### Sicherheitsheaderbeispiele: SignBeforeEncrypt, EncryptSignature  
 Anforderung  
  
```  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsse:BinarySecurityToken>  
  ...  
  </wsse:BinarySecurityToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>    
```  
  
### Sicherheitsheaderbeispiele: EncryptBeforeSign  
 Anforderung  
  
```  
<wsse:Security>  
TBD  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<wsse:Security>  
TBD  
</wsse:Security>  
```  
  
#### 6.4 IssuedToken  
 In diesem Authentifizierungsmodus unterstützt der Client den Dienst als solchen nicht. Stattdessen präsentiert der Client ein Token, das von einem Security Token Service \(STS\) ausgegeben wird, und einen freigegebenen Schlüssel.  Der Dienst wird dem Client gegenüber nicht authentifiziert. Stattdessen verschlüsselt STS den geteilten Schlüssel als Teil des ausgestellten Tokens, sodass nur der Dienst den Schlüssel entschlüsseln kann.  Die verwendete Bindung ist eine symmetrische Bindung mit den folgenden Eigenschaften:  
  
 Schutztoken: ausgestelltes Token, Einschlussmodus ist auf ...\/IncludeToken\/AlwaysToRecipient festgelegt                   
 Tokenschutz: False  
  
 Ganze Header\- und Textsignaturen: True  
  
 Schutzreihenfolge: SignBeforeEncrypt  
  
 Signaturverschlüsselung: True  
  
 Richtlinie  
  
```  
<wsp:Policy wsu:Id='CustomBinding_ISimple3_policy' >  
  <wsp:ExactlyOne>  
    <wsp:All>  
      <sp:SymmetricBinding>  
        <wsp:Policy>  
          <sp:ProtectionToken>  
            <wsp:Policy>  
              <sp:IssuedToken sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
                <sp:RequestSecurityTokenTemplate>  
                  <wst:KeyType>  
http://schemas.xmlsoap.org/ws/2005/02/trust/SymmetricKey  
                  </wst:KeyType>   
                </sp:RequestSecurityTokenTemplate>  
                <wsp:Policy>  
                  <sp:RequireDerivedKeys />   
                  <sp:RequireInternalReference />   
                </wsp:Policy>  
              </sp:IssuedToken>  
            </wsp:Policy>  
          </sp:ProtectionToken>  
          <sp:AlgorithmSuite>  
            <wsp:Policy>  
              <sp:Basic256 />   
            </wsp:Policy>  
          </sp:AlgorithmSuite>  
          <sp:Layout>  
            <wsp:Policy>  
              <sp:Strict />   
            </wsp:Policy>  
          </sp:Layout>  
          <sp:IncludeTimestamp />   
          <sp:EncryptSignature />   
          <sp:OnlySignEntireHeadersAndBody />   
        </wsp:Policy>  
      </sp:SymmetricBinding>  
      <sp:Wss11>  
        <wsp:Policy>  
          <sp:MustSupportRefKeyIdentifier />   
          <sp:MustSupportRefIssuerSerial />   
          <sp:MustSupportRefThumbprint />   
          <sp:MustSupportRefEncryptedKey />   
        </wsp:Policy>  
      </sp:Wss11>  
      <sp:Trust10>  
        <wsp:Policy>  
          <sp:MustSupportIssuedTokens />   
          <sp:RequireClientEntropy />   
          <sp:RequireServerEntropy />   
        </wsp:Policy>  
      </sp:Trust10>  
      <wsaw:UsingAddressing />   
    </wsp:All>  
  </wsp:ExactlyOne>  
</wsp:Policy>  
```  
  
### Sicherheitsheaderbeispiele: SignBeforeEncrypt, EncryptSignature  
 Anforderung  
  
```  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <saml:Assertion>  
  ...  
  </saml:Assertion>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>    
```  
  
### Sicherheitsheaderbeispiele: EncryptBeforeSign  
 Anforderung  
  
```  
<wsse:Security>  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <saml:Assertion>  
  ...  
  </saml:Assertion>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<wsse:Security>  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
### 6.5 Verwenden von SslNegotiated zur Dienstauthentifizierung  
 Dieser Abschnitt beschreibt eine Gruppe von Authentifizierungsmodi, die eine symmetrische Bindung verwenden, deren Schutztoken ein Sicherheitskontexttoken über WS\-SecureConversation \(WS\-SC\) ist, dessen Schlüsselwert ausgeführt wird, indem das TLS\-Protokoll über WS\-Trust \(WS\-T\) RST\/RSTR\-Nachrichten ausgeführt wird.  Genaue Informationen über die TLS\-Handshake\-Implementierung mit WS\-Trust werden in TLSNEGO beschrieben.  In diesen Nachrichtenbeispielen wird davon ausgegangen, dass SCT bereits mit einem verbundenen Sicherheitskontext über einen Handshake etabliert ist.  
  
 Die verwendete Bindung ist eine symmetrische Bindung mit den folgenden Eigenschaften:  
  
 Schutztoken: SslContextToken, Einschlussmodus ist auf ...\/IncludeToken\/Never festgelegt               
 Tokenschutz: False  
  
 Ganze Header\- und Textsignaturen: True  
  
 Schutzreihenfolge: SignBeforeEncrypt  
  
 Signaturverschlüsselung: True  
  
#### 6.5.1 Richtlinie für SslNegotiated\-Dienstauthentifizierung  
 Die Richtlinien für alle Authentifizierungsmodi in diesem Abschnitt sind ähnlich und unterscheiden sich nur durch bestimmte signierte unterstützende oder ausstellende Token, die verwendet werden.  
  
```  
<wsp:Policy wsu:Id='SslNegotiated_policy' >  
  <wsp:ExactlyOne>  
    <wsp:All>  
      <sp:SymmetricBinding>  
        <wsp:Policy>  
          <sp:ProtectionToken>  
            <wsp:Policy>  
              <mssp:SslContextToken sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' />  
                <wsp:Policy>  
                  <sp:RequireDerivedKeys />   
                </wsp:Policy>  
              </mssp:SslContextToken>  
            </wsp:Policy>  
          </sp:ProtectionToken>  
          <sp:AlgorithmSuite>  
            <wsp:Policy>  
              <sp:Basic256 />   
            </wsp:Policy>  
          </sp:AlgorithmSuite>  
          <sp:Layout>  
            <wsp:Policy>  
              <sp:Strict />   
            </wsp:Policy>  
          </sp:Layout>  
          <sp:IncludeTimestamp />   
          <sp:EncryptSignature />   
          <sp:OnlySignEntireHeadersAndBody />   
        </wsp:Policy>  
      </sp:SymmetricBinding>  
      <!-- Supporting token assertions go here -->  
      ..  
      <sp:Wss11>   
        <wsp:Policy>  
          <sp:MustSupportRefKeyIdentifier />   
          <sp:MustSupportRefIssuerSerial />   
          <sp:MustSupportRefThumbprint />   
          <sp:MustSupportRefEncryptedKey />   
        </wsp:Policy>  
      </sp:Wss11>  
      <sp:Trust10>  
        <wsp:Policy>  
          <sp:MustSupportIssuedTokens />   
          <sp:RequireClientEntropy />   
          <sp:RequireServerEntropy />   
        </wsp:Policy>  
      </sp:Trust10>  
      <wsaw:UsingAddressing />   
    </wsp:All>  
  </wsp:ExactlyOne>  
</wsp:Policy>  
```  
  
#### 6.5.2 AnonymousForSslNegotiated  
 Mit diesem Authentifizierungsmodus ist der Client anonym, und der Dienst wird mit einem X.509\-Zertifikat authentifiziert.  Die verwendete Bindung ist eine Instanz einer symmetrischen Bindung gemäß der Beschreibung in&\#160;6.5.1.  
  
 Richtlinie  
  
 Weitere Informationen zu den Bindungen finden Sie unter "Richtlinie" im Abschnitt&\#160;6.5.1.  
  
### Sicherheitsheaderbeispiele: SignBeforeEncrypt, EncryptSignature  
 Anforderung  
  
```  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:SecurityContextToken>  
  ...  
  </wsc:SecurityContextToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>    
```  
  
### Sicherheitsheaderbeispiele: EncryptBeforeSign  
 Anforderung  
  
```  
<wsse:Security>  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:SecurityContextToken>  
  ...  
  </wsc:SecurityContextToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<wsse:Security>  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
#### 6.5.3 UserNameForSslNegotiated  
 Bei diesem Authentifizierungsmodus wird der Client über ein Benutzernamentoken authentifiziert, das auf der SOAP\-Schicht als signiertes unterstützendes Token angezeigt wird.  Der Dienst wird über ein X.509\-Zertifikat authentifiziert.  Die verwendete Bindung ist eine Instanz einer symmetrischen Bindung gemäß der Beschreibung im Abschnitt&\#160;6.5.1.  
  
 Richtlinie  
  
 Weitere Informationen zu den Bindungen finden Sie im Abschnitt&\#160;6.5.1.  
  
 Signiertes unterstützendes Token  
  
```  
<sp:SignedSupportingTokens>  
  <wsp:Policy>  
    <sp:UsernameToken sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
      <wsp:Policy>  
        <sp:WssUsernameToken10 />   
      </wsp:Policy>  
    </sp:UsernameToken>  
  </wsp:Policy>  
</sp:SignedSupportingTokens>  
```  
  
### Sicherheitsheaderbeispiele: SignBeforeEncrypt, EncryptSignature  
 Anforderung  
  
```  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:SecurityContextToken>  
  ...  
  </wsc:SecurityContextToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>    
```  
  
### Sicherheitsheaderbeispiele: EncryptBeforeSign  
 Anforderung  
  
```  
<wsse:Security>  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:SecurityContextToken>  
  ...  
  </wsc:SecurityContextToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<wsse:Security>  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
#### 6.5.4 IssuedTokenForSslNegotiated  
 In diesem Authentifizierungsmodus unterstützt der Client den Dienst als solchen nicht, sondern präsentiert ein Token, das von einem Sicherheitstokendienst \(Security Token Service, STS\) ausgegeben wird, und einen freigegebenen Schlüssel.  Das ausgestellte Token wird auf der SOAP\-Schicht als ausstellendes unterstützendes Token angezeigt.  Der Dienst wird über ein X.509\-Zertifikat authentifiziert.  Die verwendete Bindung ist eine Instanz einer symmetrischen Bindung gemäß der Beschreibung in&\#160;6.5.1.  
  
 Richtlinie  
  
 Weitere Informationen zu den Bindungen finden Sie im Abschnitt&\#160;6.5.1.  
  
 Ausstellendes unterstützendes Token  
  
```  
<sp:EndorsingSupportingTokens>  
  <wsp:Policy>  
    <sp:IssuedToken sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
      <sp:RequestSecurityTokenTemplate>  
        <wst:KeyType>  
http://schemas.xmlsoap.org/ws/2005/02/trust/SymmetricKey  
        </wst:KeyType>   
      </sp:RequestSecurityTokenTemplate>  
      <wsp:Policy>  
        <sp:RequireDerivedKeys />   
        <sp:RequireInternalReference />   
      </wsp:Policy>  
    </sp:IssuedToken>  
  </wsp:Policy>  
</sp:EndorsingSupportingTokens>  
```  
  
### Sicherheitsheaderbeispiele: SignBeforeEncrypt, EncryptSignature  
 Anforderung  
  
```  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:SecurityContextToken>  
  ...  
  </wsc:SecurityContextToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <saml:Assertion>  
  ...  
  </saml:Assertion>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>    
```  
  
### Sicherheitsheaderbeispiele: EncryptBeforeSign  
 Anforderung  
  
```  
<wsse:Security>  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:SecurityContextToken>  
  ...  
  </wsc:SecurityContextToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <saml:Assertion>  
  ...  
  </saml:Assertion>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<wsse:Security>  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsse11:SignatureConfirmation />  
  <wsse11:SignatureConfirmation />  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
#### 6.5.5 MutualSslNegotiated  
 Bei diesem Authentifizierungsmodus werden sowohl der Client als auch der Dienst mit X.509\-Zertifikaten authentifiziert.  Die verwendete Bindung ist eine Instanz einer symmetrischen Bindung gemäß der Beschreibung in&\#160;6.5.1.  
  
 Richtlinie  
  
 Weitere Informationen zu den Bindungen finden Sie im Abschnitt&\#160;6.5.1.  
  
 Ausstellendes unterstützendes Token  
  
```  
<sp:EndorsingSupportingTokens>  
  <wsp:Policy>  
    <sp:X509Token sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
      <wsp:Policy>  
        <sp:RequireThumbprintReference />   
        <sp:WssX509V3Token10 />   
      </wsp:Policy>  
    </sp:X509Token>  
  </wsp:Policy>  
</sp:EndorsingSupportingTokens>  
```  
  
### Sicherheitsheaderbeispiele: SignBeforeEncrypt, EncryptSignature  
 Anforderung  
  
```  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:SecurityContextToken>  
  ...  
  </wsc:SecurityContextToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>    
```  
  
### Sicherheitsheaderbeispiele: EncryptBeforeSign  
 Anforderung  
  
```  
<wsse:Security>  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:SecurityContextToken>  
  ...  
  </wsc:SecurityContextToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<wsse:Security>  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
### 6.6 SspiNegotiated  
 Bei diesem Authentifizierungsmodus wird ein Aushandlungsprotokoll verwendet, um Client\- und Serverauthentifizierung auszuführen.  Wenn möglich wird Kerberos verwendet, ansonsten NTLM.  Die verwendete Bindung ist eine symmetrische Bindung mit den folgenden Eigenschaften:  
  
 Schutztoken: SpnegoContextToken, Einschlussmodus ist auf ...\/IncludeToken\/AlwaysToRecipient festgelegt               
 Tokenschutz: False  
  
 Ganze Header\- und Textsignaturen: True  
  
 Schutzreihenfolge: SignBeforeEncrypt  
  
 Signaturverschlüsselung: True  
  
 Richtlinie  
  
```  
<wsp:Policy wsu:Id='CustomBinding_ISimple13_policy' >  
  <wsp:ExactlyOne>  
    <wsp:All>  
      <sp:SymmetricBinding>  
        <wsp:Policy>  
          <sp:ProtectionToken>  
            <wsp:Policy>  
              <sp:SpnegoContextToken sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
                <wsp:Policy>  
                  <sp:RequireDerivedKeys />   
                </wsp:Policy>  
              </sp:SpnegoContextToken>  
            </wsp:Policy>  
          </sp:ProtectionToken>  
          <sp:AlgorithmSuite>  
            <wsp:Policy>  
              <sp:Basic256 />   
            </wsp:Policy>  
          </sp:AlgorithmSuite>  
          <sp:Layout>  
            <wsp:Policy>  
              <sp:Strict />   
            </wsp:Policy>  
          </sp:Layout>  
          <sp:IncludeTimestamp />   
          <sp:EncryptSignature />   
          <sp:OnlySignEntireHeadersAndBody />   
        </wsp:Policy>  
      </sp:SymmetricBinding>  
      <sp:Wss11>  
        <wsp:Policy>  
          <sp:MustSupportRefKeyIdentifier />   
          <sp:MustSupportRefIssuerSerial />   
          <sp:MustSupportRefThumbprint />   
          <sp:MustSupportRefEncryptedKey />   
        </wsp:Policy>  
      </sp:Wss11>  
      <sp:Trust10>  
        <wsp:Policy>  
          <sp:MustSupportIssuedTokens />   
          <sp:RequireClientEntropy />   
          <sp:RequireServerEntropy />   
        </wsp:Policy>  
      </sp:Trust10>  
      <wsaw:UsingAddressing />   
    </wsp:All>  
  </wsp:ExactlyOne>  
</wsp:Policy>  
```  
  
### Sicherheitsheaderbeispiele: SignBeforeEncrypt, EncryptSignature  
 Anforderung  
  
```  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:SecurityContextToken>  
  ...  
  </wsc:SecurityContextToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>    
```  
  
### Sicherheitsheaderbeispiele: EncryptBeforeSign  
 Anforderung  
  
```  
<wsse:Security>  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:SecurityContextToken>  
  ...  
  </wsc:SecurityContextToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<wsse:Security>  
<wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
### 6.7 SecureConversation  
 Die verwendete Bindung ist eine symmetrische Bindung, wobei das Schutztoken ein SCT über WS\-SecureConversation \(WS\-SC\) ist.  Das SCT wird über WS\-Trust \(WS\-Trust\) oder WS\-SecureConversation \(WS\-SC\) gemäß einer ummantelten Bindung ausgehandelt, die selbst eine symmetrische Bindung ist und ein Aushandlungsprotokoll verwendet.  Das Aushandlungsprotokoll verwendet Kerberos, um, falls möglich, Client\- und Serverauthentifizierung auszuführen.  Wenn Kerberos nicht verwendet werden kann, greift es wieder auf NTLM zurück.  
  
 Richtlinie  
  
```  
<wsp:Policy wsu:Id='SecureConversation_policy' >  
  <wsp:ExactlyOne>  
    <wsp:All>  
      <sp:SymmetricBinding>  
        <wsp:Policy>  
          <sp:ProtectionToken>  
            <wsp:Policy>  
              <sp:SecureConversationToken sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
                <wsp:Policy>  
                  <sp:RequireDerivedKeys />   
                  <sp:BootstrapPolicy>  
                    <wsp:Policy>  
                      <sp:SignedParts>  
                        <sp:Body />   
                        <sp:Header Name='To' Namespace='http://www.w3.org/2005/08/addressing' />   
                        <sp:Header Name='From' Namespace='http://www.w3.org/2005/08/addressing' />   
                        <sp:Header Name='FaultTo' Namespace='http://www.w3.org/2005/08/addressing' />   
                        <sp:Header Name='ReplyTo' Namespace='http://www.w3.org/2005/08/addressing' />   
                        <sp:Header Name='MessageID' Namespace='http://www.w3.org/2005/08/addressing' />   
                        <sp:Header Name='RelatesTo' Namespace='http://www.w3.org/2005/08/addressing' />   
                        <sp:Header Name='Action' Namespace='http://www.w3.org/2005/08/addressing' />   
                      </sp:SignedParts>  
                      <sp:EncryptedParts>  
                        <sp:Body />   
                      </sp:EncryptedParts>  
                      <sp:SymmetricBinding>  
                        <wsp:Policy>  
                          <sp:ProtectionToken>  
                            <wsp:Policy>  
                              <sp:SpnegoContextToken sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
                                <wsp:Policy>  
                                  <sp:RequireDerivedKeys />   
                                </wsp:Policy>  
                              </sp:SpnegoContextToken>  
                            </wsp:Policy>  
                          </sp:ProtectionToken>  
                          <sp:AlgorithmSuite>  
                            <wsp:Policy>  
                              <sp:Basic256 />   
                            </wsp:Policy>  
                          </sp:AlgorithmSuite>  
                          <sp:Layout>  
                            <wsp:Policy>  
                              <sp:Strict />   
                            </wsp:Policy>  
                          </sp:Layout>  
                          <sp:IncludeTimestamp />   
                          <sp:EncryptSignature />   
                          <sp:OnlySignEntireHeadersAndBody />   
                        </wsp:Policy>  
                      </sp:SymmetricBinding>  
                      <sp:Wss11>  
                        <wsp:Policy>  
                          <sp:MustSupportRefKeyIdentifier />   
                          <sp:MustSupportRefIssuerSerial />   
                          <sp:MustSupportRefThumbprint />   
                          <sp:MustSupportRefEncryptedKey />   
                        </wsp:Policy>  
                      </sp:Wss11>  
                      <sp:Trust10>  
                        <wsp:Policy>  
                          <sp:MustSupportIssuedTokens />   
                          <sp:RequireClientEntropy />   
                          <sp:RequireServerEntropy />   
                        </wsp:Policy>  
                      </sp:Trust10>  
                    </wsp:Policy>  
                  </sp:BootstrapPolicy>  
                </wsp:Policy>  
              </sp:SecureConversationToken>  
            </wsp:Policy>  
          </sp:ProtectionToken>  
          <sp:AlgorithmSuite>  
            <wsp:Policy>  
              <sp:Basic256 />   
            </wsp:Policy>  
          </sp:AlgorithmSuite>  
          <sp:Layout>  
            <wsp:Policy>  
              <sp:Strict />   
            </wsp:Policy>  
          </sp:Layout>  
          <sp:IncludeTimestamp />   
          <sp:EncryptSignature />   
          <sp:OnlySignEntireHeadersAndBody />   
        </wsp:Policy>  
      </sp:SymmetricBinding>  
      <sp:Wss11>  
        <wsp:Policy>  
          <sp:MustSupportRefKeyIdentifier />   
          <sp:MustSupportRefIssuerSerial />   
          <sp:MustSupportRefThumbprint />   
          <sp:MustSupportRefEncryptedKey />   
        </wsp:Policy>  
      </sp:Wss11>  
      <sp:Trust10>  
        <wsp:Policy>  
          <sp:MustSupportIssuedTokens />   
          <sp:RequireClientEntropy />   
          <sp:RequireServerEntropy />   
        </wsp:Policy>  
      </sp:Trust10>  
      <wsaw:UsingAddressing />   
    </wsp:All>  
  </wsp:ExactlyOne>  
</wsp:Policy>  
```  
  
### Sicherheitsheaderbeispiele: SignBeforeEncrypt, EncryptSignature  
 Anforderung  
  
```  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:SecurityContextToken>  
  ...  
  </wsc:SecurityContextToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>    
```  
  
### Sicherheitsheaderbeispiele: EncryptBeforeSign  
 Anforderung  
  
```  
<wsse:Security>  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:SecurityContextToken>  
  ...  
  </wsc:SecurityContextToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
 Antwort  
  
```  
<wsse:Security>  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```