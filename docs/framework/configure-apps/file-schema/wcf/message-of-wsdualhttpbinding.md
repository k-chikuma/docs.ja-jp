---
title: <message> の <wsDualHttpBinding>
ms.date: 03/30/2017
ms.assetid: 75101744-eed8-4d61-91f4-5fc4473a21f2
ms.openlocfilehash: 03a1ae9c220b6d7f84b501f26c5fe408fc702528
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61768941"
---
# <a name="message-of-wsdualhttpbinding"></a>\<メッセージ > の\<wsDualHttpBinding >
メッセージ レベル セキュリティを定義、 [ \<wsDualHttpBinding >](../../../../../docs/framework/configure-apps/file-schema/wcf/wsdualhttpbinding.md)します。  
  
 \<system.ServiceModel >  
\<bindings>  
\<wsDualHttpBinding >  
\<binding>  
\<セキュリティ >  
\<message>  
  
## <a name="syntax"></a>構文  
  
```xml  
<message clientCredentialType="None/Windows/UserName/Certificate/CardSpace"
         negotiateServiceCredential="Boolean"
         algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15" />
</message>
```  
  
## <a name="type"></a>型  
 <xref:System.ServiceModel.MessageSecurityOverHttp>  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|algorithmSuite|省略可能です。 メッセージの暗号化とキー ラップ アルゴリズムを設定します。 アルゴリズムとキー サイズは、<xref:System.ServiceModel.Security.SecurityAlgorithmSuite> クラスにより決まります。 これらのアルゴリズムは、Security Policy Language (WS-SecurityPolicy) の仕様で指定されているアルゴリズムに対応付けられています。<br /><br /> 有効値については、以下を参照してください。 既定値は `Basic256` です。|  
|clientCredentialType|省略可能です。 セキュリティ モード `Message` を使用してクライアント認証を実行するときに使用される資格情報の種類を指定します。 有効値については、以下を参照してください。 既定値は `Windows` です。<br /><br /> この属性は <xref:System.ServiceModel.MessageCredentialType> 型です。|  
|negotiateServiceCredential|任意。 サービス資格情報がクライアントの帯域外で提供されるか、ネゴシエーションのプロセスによってサービスからクライアントに取得されるかを指定するブール値。 そのようなネゴシエーションは、通常のメッセージ交換の準備です。<br /><br /> 場合、`clientCredentialType`属性が [なし]、ユーザー名、またはこの属性を設定、証明書に等しい`false`サービス証明書がクライアントの帯域外で使用可能であり、クライアントがサービス証明書を指定する必要があることを意味 (を使用して、[ \<serviceCertificate >](../../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)) で、 [ \<serviceCredentials >](../../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md)サービス動作。 このモードは、WS-Trust および WS-SecureConversation が実装された SOAP スタックと同時使用できます。<br /><br /> `ClientCredentialType` 属性が `Windows` に設定されている場合、この属性を `false` に設定すると Kerberos ベースの認証が指定されます。 これは、クライアントおよびサービスが同じ Kerberos ドメインの一部でなければならないことを意味します。 このモードは、Kerberos トークン プロファイル (OASIS WSS TC で定義) に加えて WS-Trust および WS-SecureConversation が実装された SOAP スタックと同時使用できます。 この属性が `true` の場合、SOAP メッセージを介して SPNego 交換をトンネル化する .NET SOAP ネゴシエーションが行われます。<br /><br /> 既定値は `true` です。|  
  
## <a name="algorithmsuite-attribute"></a>algorithmSuite 属性  
  
|[値]|説明|  
|-----------|-----------------|  
|Basic128|Aes128 暗号化を使用し、メッセージ ダイジェストには Sha1 を、キー ラップには Rsa-oaep-mgf1p を使用します。|  
|Basic192|Aes192 暗号化を使用し、メッセージ ダイジェストには Sha1 を、キー ラップには Rsa-oaep-mgf1p を使用します。|  
|Basic256|Aes256 暗号化を使用し、メッセージ ダイジェストには Sha1 を、キー ラップには Rsa-oaep-mgf1p を使用します。|  
|Basic256Rsa15|メッセージの暗号化には Aes256 を使用し、メッセージ ダイジェストには Sha1 を、キー ラップには Rsa15 を使用します。|  
|Basic192Rsa15|メッセージの暗号化には Aes192 を使用し、メッセージ ダイジェストには Sha1 を、キー ラップには Rsa15 を使用します。|  
|TripleDes|TripleDes 暗号化を使用し、メッセージ ダイジェストには Sha1 を、キー ラップには Rsa-oaep-mgf1p を使用します。|  
|Basic128Rsa15|メッセージの暗号化には Aes128 を使用し、メッセージ ダイジェストには Sha1 を、キー ラップには Rsa15 を使用します。|  
|TripleDesRsa15|TripleDes 暗号化を使用し、メッセージ ダイジェストには Sha1 を、キー ラップには Rsa15 を使用します。|  
|Basic128Sha256|メッセージの暗号化には Aes256 を使用し、メッセージ ダイジェストには Sha256 を、キー ラップには Rsa-oaep-mgf1p を使用します。|  
|Basic192Sha256|メッセージの暗号化には Aes192 を使用し、メッセージ ダイジェストには Sha256 を、キー ラップには Rsa-oaep-mgf1p を使用します。|  
|Basic256Sha256|メッセージの暗号化には Aes256 を使用し、メッセージ ダイジェストには Sha256 を、キー ラップには Rsa-oaep-mgf1p を使用します。|  
|TripleDesSha256|メッセージの暗号化には TripleDes を使用し、メッセージ ダイジェストには Sha256 を、キー ラップには Rsa-oaep-mgf1p を使用します。|  
|Basic128Sha256Rsa15|メッセージの暗号化には Aes128 を使用し、メッセージ ダイジェストには Sha256 を、キー ラップには Rsa15 を使用します。|  
|Basic192Sha256Rsa15|メッセージの暗号化には Aes192 を使用し、メッセージ ダイジェストには Sha256 を、キー ラップには Rsa15 を使用します。|  
|Basic256Sha256Rsa15|メッセージの暗号化には Aes256 を使用し、メッセージ ダイジェストには Sha256 を、キー ラップには Rsa15 を使用します。|  
|TripleDesSha256Rsa15|メッセージの暗号化には TripleDes を使用し、メッセージ ダイジェストには Sha256 を、キー ラップには Rsa15 を使用します。|  
  
## <a name="clientcredentialtype-attribute"></a>clientCredentialType 属性  
  
|[値]|説明|  
|-----------|-----------------|  
|なし|サービスが匿名クライアントと対話できるようになります。 サービス側では、サービスがクライアントの資格情報を必要としないことを示しています。 クライアント側では、クライアントがクライアントの資格情報を提示しないことを示しています。|  
|Windows|SOAP 交換を、Windows 資格情報の認証されたコンテキストで行うことが可能になります。 `negotiateServiceCredential` 属性が `true` に設定されている場合、SSPI ネゴシエーションと Kerberos (同時使用可能な標準) のいずれかが実行されます。|  
|UserName|サービスが、UserName 資格情報を使用したクライアントの認証を要求できるようにします。 WCF は、パスワード ダイジェストの送信、またはパスワードを使用して、このようなキーを使用して、メッセージ セキュリティのためのキーの派生をサポートしていません。 そのため、WCF は、UserName 資格情報を使用する場合、トランスポート、セキュリティで保護を適用します。 この資格情報モードは、`negotiateServiceCredential` 属性に基づいて、同時実行可能な交換か、同時実行できないネゴシエーションのいずれかになります。|  
|証明書|証明書を使用したクライアントの認証を、サービスで要求することが可能になります。 メッセージのセキュリティ モードが使用されており、`negotiateServiceCredential` 属性が `false` に設定されている場合、クライアントをサービス証明書で準備する必要があります。|  
|IssuedToken|カスタム トークン (通常はセキュリティ トークン サービスにより発行される) を指定します。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<security>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-wsdualhttpbinding.md)|セキュリティ機能を定義、 [ \<wsDualHttpBinding >](../../../../../docs/framework/configure-apps/file-schema/wcf/wsdualhttpbinding.md)します。|  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.WSDualHttpSecurityElement.Message%2A>
- <xref:System.ServiceModel.WSDualHttpSecurity.Message%2A>
- <xref:System.ServiceModel.Configuration.MessageSecurityOverTcpElement>
- <xref:System.ServiceModel.MessageSecurityOverHttp>
- [サービスおよびクライアントのセキュリティ保護](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)
- [バインディング](../../../../../docs/framework/wcf/bindings.md)
- [システムが提供するバインディングの構成](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)
- [サービスとクライアントを構成するためのバインディングの使用](../../../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](../../../../../docs/framework/misc/binding.md)
