---
title: '方法: コード内でクライアント バインディングを指定する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 6bee5da4-adf7-42e6-8f78-63a9e5c6dbad
ms.openlocfilehash: c95e30c65c6096140fca0c1241e76fbc7af4df3d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61929130"
---
# <a name="how-to-specify-a-client-binding-in-code"></a>方法: コード内でクライアント バインディングを指定する
この例では、電卓サービスを使用するためのクライアントを作成し、そのクライアントのバインディングを強制的にコードで指定します。 クライアントは `CalculatorService` にアクセスします。これにより、`ICalculator` インターフェイスが実装され、サービスとクライアントの両方で <xref:System.ServiceModel.BasicHttpBinding> クラスが使用されます。  
  
 ここで説明する手順では、電卓サービスが実行されていることを前提としています。 サービスの構築方法の詳細については、次を参照してください。[方法。構成でサービス バインディング指定](../../../docs/framework/wcf/how-to-specify-a-service-binding-in-configuration.md)します。 また、使用、 [ServiceModel メタデータ ユーティリティ ツール (Svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)クライアント コンポーネントを自動的に生成する Windows Communication Foundation (WCF) を提供します。 このツールでは、サービスにアクセスするためのクライアント コードが生成されます。  
  
 クライアントは 2 つの部分で構成されます。 Svcutil.exe によって、`ClientCalculator` インターフェイスを実装する `ICalculator` が生成されます。 次に、`ClientCalculator` のインスタンスを作成し、サービスのバインディングとアドレスをコードで指定して、このクライアント アプリケーションを作成します。  
  
 この例のソースのコピーを次を参照してください。、 [BasicBinding](../../../docs/framework/wcf/samples/basicbinding.md)サンプル。  
  
### <a name="to-specify-a-custom-binding-in-code"></a>コード内でカスタム バインドを指定するには  
  
1. コマンド ラインから Svcutil.exe を実行して、サービス メタデータからコードを生成します。  
  
    ```  
    Svcutil.exe <service's Metadata Exchange (MEX) address or HTTP GET address>   
    ```  
  
2. 生成されたクライアントには、クライアントの実装時に満たされなければならないサービス コントラクトを定義する `ICalculator` インターフェイスが含まれます。  
  
     [!code-csharp[C_HowTo_CodeClientBinding#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeclientbinding/cs/client.cs#1)]
     [!code-vb[C_HowTo_CodeClientBinding#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeclientbinding/vb/client.vb#1)]  
  
3. 生成されたクライアントは `ClientCalculator` も実装します。  
  
     [!code-csharp[C_HowTo_CodeClientBinding#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeclientbinding/cs/client.cs#2)]
     [!code-vb[C_HowTo_CodeClientBinding#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeclientbinding/vb/client.vb#2)]  
  
4. クライアント アプリケーション内で `ClientCalculator` クラスを使用する <xref:System.ServiceModel.BasicHttpBinding> のインスタンスを作成し、指定したアドレスのサービス操作を呼び出します。  
  
     [!code-csharp[C_HowTo_CodeClientBinding#3](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeclientbinding/cs/client.cs#3)]
     [!code-vb[C_HowTo_CodeClientBinding#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeclientbinding/vb/client.vb#3)]  
  
5. クライアントをコンパイルして実行します。  
  
## <a name="see-also"></a>関連項目

- [サービスとクライアントを構成するためのバインディングの使用](../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)
