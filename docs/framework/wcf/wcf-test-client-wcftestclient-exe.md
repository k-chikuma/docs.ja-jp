---
title: WCF のテスト用クライアント (WcfTestClient.exe)
ms.date: 03/30/2017
ms.assetid: d4302855-677f-4640-aa90-c5d785d72fb7
ms.openlocfilehash: 9044dc2479e8e0a31a6152321231ee1936b74351
ms.sourcegitcommit: 2d42b7ae4252cfe1232777f501ea9ac97df31b63
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2019
ms.locfileid: "67487462"
---
# <a name="wcf-test-client-wcftestclientexe"></a>WCF のテスト用クライアント (WcfTestClient.exe)
Windows Communication Foundation (WCF) のテスト クライアント (WcfTestClient.exe) は、テスト パラメーターを入力し、そのサービスに入力するユーザーを有効にし、サービスが返送する応答を表示する GUI ツールです。 テストを行う WCF サービス ホストと組み合わせたときに、シームレスにサービスを提供します。  
  
 通常、次の場所で、WCF テスト クライアント (WcfTestClient.exe) を入手できます: `C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\Common7\IDE` - コミュニティがあります"Enterprise"、「担当者」のいずれかまたは Visual Studio のどのレベルに応じて「コミュニティ」をインストールします。
  
## <a name="scenarios-for-using-test-client"></a>テスト用クライアントを使用するシナリオ  
 次のセクションでは、開発プロセスを効率化する WCF テスト クライアントを使用する最も一般的なシナリオについて説明します。  
  
### <a name="inside-visual-studio"></a>Visual Studio 内  
  
#### <a name="wcf-service-host-starts-wcf-test-client-with-a-single-service"></a>WCF サービス ホストが、1 つのサービスを使用する WCF のテスト用クライアントを開始する  
 新しい WCF サービス プロジェクトを作成し、f5 キーを押してデバッガーを起動すると、プロジェクトでサービスをホストする WCF サービス ホストが開始されます。 次に、WCF テスト クライアントが開き、構成ファイルで定義されているサービス エンドポイントの一覧を表示します。 ユーザーは、パラメーターをテストしてサービスを呼び出すことができ、このプロセスを繰り返して、サービスのテストおよび検証を継続的に行うことができます。  
  
#### <a name="wcf-service-host-starts-wcf-test-client-with-multiple-services"></a>WCF サービス ホストが、複数のサービスを使用する WCF のテスト用クライアントを開始する  
 複数のサービスを含むサービス プロジェクトをデバッグする際に、WCF テスト クライアントを使用することもできます。 WCF テスト クライアントが開いたら、自動的に、プロジェクト内のサービスの一覧を繰り返し処理し、それらをテストするために開きます。  
  
### <a name="outside-visual-studio"></a>Visual Studio の外部  
 インターネット上の任意のサービスをテストする Visual Studio の外部 WCF テスト クライアント (WcfTestClient.exe) を呼び出すこともできます。 このツールを見つけるには、次の場所に移動します。  
  
 `C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\Common7\IDE` (コミュニティできる場所の"Enterprise"、"Professional"または"Community"に応じて Visual Studio のレベルはコンピューターにインストールされた 1 つ)
  
 ツールを使用するには、ファイル名をダブルクリックしてこの場所からツールを開くか、コマンド ラインからツールを起動します。  
  
 Uri の任意の数は、WCF テスト クライアントは、コマンドライン引数として受け取ります。  これらの引数には、テストできるサービスの URI を指定します。  
  
 `wcfTestClient.exe URI1 URI2 …`  
  
 WCF テスト クライアント ウィンドウが開かれた後にクリックして**ファイル**->**サービスの追加**、開きたいサービスのエンドポイント アドレスを入力します。  
  
## <a name="wcf-test-client-user-interface"></a>WCF のテスト用クライアントのユーザー インターフェイス  
 1 つのサービスまたは複数のサービスでは、WCF テスト クライアントを使用できます。  
  
### <a name="service-operations"></a>サービス操作  
 WCF テスト クライアントのメイン ウィンドウの左側のウィンドウでは、すべての利用可能なサービスをそれぞれのエンドポイントおよび操作と共に一覧表示します。  
  
 操作をダブルクリックすると、その操作の名前が付いた新しいタブ内の右ペインで、操作の内容を表示できます。  
  
 左ペインには、クライアントの構成ファイルも表示されます。 いずれかの項目をダブルクリックすると、右ペインの新しいタブ付きウィンドウにファイルの内容が表示されます。  
  
### <a name="entering-test-parameters"></a>テスト パラメーターの入力  
 テスト パラメーターを表示するには、右ペインで操作をダブルクリックして開きます。 パラメーターが示した**書式付き**ビューに既定では、任意のサービスをテストするパラメーターの値を入力するとします。  
  
 メッセージの XML を表示する をクリックして**XML**します。 サービスにお送り、次のようにクリックします。 **Invoke**します。  
  
 データセット パラメーターをクリックして、 **.** ボタンの横に**を編集しています.** 新しいウィンドウに、データ グリッドで編集します。 外観に注意してください、 **DataSet のコピー**と**貼り付けデータセット**ボタン。 最初の編集時に DataSet オブジェクトのスキーマが不明の場合、DataGrid は空になります。 スキーマが同じ DataSet オブジェクトを DataGrid の現在のオブジェクトに貼り付ける必要があります (スキーマは、貼り付け操作の前に別の場所からコピーする必要があります)。クリックして、将来の使用量の Dataset オブジェクトをコピーすることも、 **DataSet のコピー**ボタンをクリックします。  
  
 サービスの応答がテスト パラメーターの下に表示されます。  
  
> [!NOTE]
>  想定される戻り値が文字列の場合、入力が引用符で囲まれていなくても、結果は引用符で囲まれた文字列として表示されます。  
  
 サービスのコントラクトの作成時に特定の操作を一方向として指定した場合は、サービスの応答は表示されません。 メッセージが配信のキューに置かれると、メッセージが正常に送信されたことを通知するダイアログ ボックスがすぐに表示されます。  
  
### <a name="session-support"></a>セッション サポート  
 **新しいプロキシを開始**サービス操作のタブのチェック ボックスは、セッションのサポートを切り替えることができます。 既定では、このチェック ボックスはオフになります。  
  
 特定の操作 (または同じサービス エンドポイントの別の操作) のテスト パラメーターを入力し、クリックしたときに**Invoke**複数回は、これらの操作が 1 つのプロキシを共有するチェック ボックスをオフにし、サービスの状態が複数の操作にわたって保持されます。  
  
 場合、**新しいプロキシを開始** チェック ボックスをオンになって、新しいプロキシが各開始**Invoke**、前のセッション シナリオが終了すると、およびサービスの状態をリセットします。  
  
### <a name="editing-client-configuration"></a>クライアント構成の編集  
 WCF テスト クライアントのメイン ウィンドウの左側のウィンドウには、クライアント構成ファイルが一覧表示します。 いずれかの項目をダブルクリックすると、右ペインにファイルの内容が表示されます。  
  
#### <a name="edit-with-service-configuration-editor"></a>サービス構成エディターを使用した編集  
 右クリック**Config ファイル**左側のウィンドウを選び、コンテキスト メニュー **SvcConfigEditor での編集**します。 サービス構成エディターが起動し、クライアント構成の内容が表示されます。 このツール内で構成を編集して保存できます。  
  
 サービス構成エディターでファイルを保存した後は、WCF テスト クライアントには、ファイルの外部で変更され、再読み込みするかどうかを確認することを通知する警告メッセージが表示されます。  
  
 選択した場合**はい**Client.dll.config タブで構成の内容がエディターで行った変更を反映します。  
  
 選択した場合**いいえ**Client.dll.config タブで構成の内容は変更されません、ソース ファイルに変更されたコンテンツを自動的に保存します。  
  
#### <a name="restore-to-default-configuration"></a>既定の構成への復元  
 すべての変更をキャンセルし、既定のクライアント構成に復元を右クリックしたい場合**Config ファイル**左側のウィンドウを選び、コンテキスト メニュー**既定の構成に復元**します。既定の構成値が読み込まれ、[Client.dll.config] タブの内容が復元されます。  
  
#### <a name="validate-changes"></a>変更の検証  
 保存された変更は、WCF テスト クライアントで読み込まれているが、構成は、WCF スキーマに照らして有効性チェックされます。 エラーが見つかった場合は、エラーの詳細を示すダイアログ ボックスが表示されます。  
  
 プロキシの生成、バイナリのコンパイル中、またはサービスの呼び出し中に (つまり、および [編集]、「復元...」) の編集をサポートするメニュー項目が無効です。 サービスの呼び出しは、読み込みには、WCF テスト クライアントに構成が更新されたときにも無効になります。  
  
#### <a name="persist-client-configuration"></a>クライアント構成の保持  
 **ツール**->**オプション**->**クライアント構成** タブには、**常に再生成の構成と起動サービス**オプションは、既定で有効です。 このオプションは、WCF テスト クライアントがサービスを読み込むたびに、最新のサービス コントラクトとサービスの App.config ファイルに基づいて構成ファイルを再生するを指定します。  
  
 WCF サービスのクライアントの構成を編集し、常にこの更新されたファイルをオフにすることができます、サービスのデバッグに使用するかどうか、**再生成**オプション。 これにより、サービスを更新し、WCF テスト クライアントで再度開く場合でも、Client.dll.config ファイルは再生成された、更新されたサービスに基づくいずれかの代わりに以前に更新したは。  
  
 ただし、再生成されたプロキシとの一貫性を保つために、構成ファイルの編集が必要になる場合があります。 サービスを更新したことが原因で、再生成されたプロキシと構成ファイルが一致しなくなると、サービスを呼び出したときにエラーが発生します。  
  
> [!CAUTION]
>  変更したクライアント構成ファイルを後で再利用することにした場合、該当するファイルは次の場所で見つけることができます。  
>   
>  \Documents and Settings\\\My Documents\Test クライアント プロジェクトの [ユーザー アカウント]。  
>   
>  クライアント構成ファイルに格納されている更新された資格情報は、このフォルダーのアクセス制御リスト (ACL) によって保護されています。  
  
### <a name="adding-removing-and-refreshing-services"></a>サービスの追加、削除、および更新  
  
#### <a name="add-service"></a>サービスの追加  
 クリックして**ファイル**->**サービスの追加**WCF テスト クライアントにサービスを追加します。 次に、追加するサービスの URI (エンドポイント アドレス) を入力する必要があります。 サービスのアドレスには、MEX アドレスまたは WSDL アドレスを指定できます。  
  
 10 の最近追加されたサービスのエンドポイントの一覧を検索することもできます、**最近のサービス**サブメニューで開く。 それらのいずれかを選択した場合、指定されたサービスは、WCF テスト クライアントに追加されます。  
  
 また、サービス ツリーのルートを右クリックすることもできます。**マイ サービス プロジェクト**、選択と**サービスの追加**、同じ結果を実現するためにします。  
  
 プロキシの生成中、バイナリのコンパイル中、またはサービスの呼び出し中は、サービスの追加をサポートするメニュー項目が無効になります。 また、サービスの呼び出しも無効になります。  
  
#### <a name="remove-service"></a>サービスの削除  
 削除して、選択するサービスのサービス ルートを右クリックして**サービスの削除**WCF テスト クライアントからサービスを削除します。  
  
 プロキシの生成中、バイナリのコンパイル中、またはサービスの呼び出し中は、サービスの削除をサポートするメニュー項目が無効になります。 また、サービスの呼び出しも無効になります。  
  
#### <a name="refresh-service"></a>サービスの更新  
 変更されたサービスに WCF テスト クライアントが実行されていると、そのサービスの WCF テスト クライアント実装が最新であることを確認するときに、サービス、および select のサービス ルートを右クリックして**更新サービス**します。 更新後、サービスの状態はリセットされます。  
  
 プロキシの生成中、バイナリのコンパイル中、またはサービスの呼び出し中は、サービスの更新をサポートするメニュー項目が無効になります。 また、サービスの呼び出しも無効になります。  
  
## <a name="location-of-files-generated-by-the-test-client"></a>テスト クライアントが生成するファイルの場所  
 既定では、WCF テスト クライアントのストアは、"%appdata%\Local\temp\Test Client Projects"フォルダー内のクライアント コードと構成ファイルを生成します。 このフォルダーは、WCF テスト クライアントが終了した後に削除されます。 WCF テスト クライアントで構成ファイルが変更されたかどうか、**常に再生成の構成サービスの起動時**オプションが無効になっている、変更したファイルは"My Documents\Test Client Projects"の下の"CachedConfig"フォルダーにコピーされますインデックスとしてマッピング (メタデータのアドレス-ファイルの名前) XML ファイル。  
  
 コマンドラインを使用して、WCF テスト クライアントを起動することも、`/ProjectPath`生成されたファイルを格納する新しい目的のパスを指定するスイッチまたはを使用して、`/RestoreProjectPath`スイッチが既定の場所を復元します。 構文は次のとおりです。  
  
 `wcfTestClient.exe /ProjectPath [desired location]`  
  
 このコマンドを実行しても、WCF テスト クライアントは開きません。 フォルダーの場所が変更されるだけです。 WCF テスト クライアントが実行されているかどうかどうかは、このコマンドを実行することができます。 WCF テスト クライアントを再起動すると、新しい場所が適用されます。 位置情報は、レジストリ、または"%appdata%\Local\temp\Test Client Projects"フォルダーの WcfTestClient.exe.option ファイルに保存できます。  
  
## <a name="features-supported-by-wcf-test-client"></a>WCF のテスト用クライアントでサポートされる機能  
 WCF テスト クライアントでサポートされる機能の一覧を次には。  
  
- サービスの呼び出し:要求/応答、一方向のメッセージ。  
  
- バインディング : Svcutil.exe でサポートされるすべてのバインディング  
  
- セッションの制御  
  
- メッセージ コントラクト  
  
- XML シリアル化  
  
 WCF テスト クライアントでサポートされない機能の一覧を次には。  
  
- 型: <xref:System.IO.Stream>、<xref:System.ServiceModel.Channels.Message>、<xref:System.Xml.XmlElement>、<xref:System.Xml.XmlAttribute>、<xref:System.Xml.XmlNode>、<xref:System.Xml.Serialization.IXmlSerializable> インターフェイスを実装する型 (関連する <xref:System.Xml.Serialization.XmlSchemaProviderAttribute> 属性を含む)、<xref:System.Xml.Linq.XDocument> 型と <xref:System.Xml.Linq.XElement> 型、および ADO.NET <xref:System.Data.DataTable> 型。  
  
- 双方向コントラクト  
  
- トランザクション  
  
- セキュリティ:CardSpace、証明書、およびユーザー名とパスワード。  
  
- バインド:WSFederationbinding、任意のコンテキスト バインディングおよび Https バインディング、WebHttpbinding (Json 応答メッセージのサポート)。  
  
## <a name="closing-wcf-test-client"></a>WCF のテスト用クライアントの終了  
 次の方法では、WCF テスト クライアントを閉じることができます。  
  
- **ファイル** メニューのをクリックして**終了**します。 また、WCF テスト クライアントのメイン ウィンドウで次のようにクリックします。**閉じる**します。 これらのアクションも WCF サービスの自動ホストをシャット ダウン、および Visual Studio によって WCF テスト クライアントを起動した場合は、Visual Studio のデバッグ プロセスを停止します。  
  
- 右クリックし、 **WCF サービス ホスト**アイコン、通知領域とクリック**終了します。** これにより、シャット ダウン、WCF サービスの自動ホストと WCF テスト クライアントの両方と、Visual Studio のプロセスのデバッグを停止します。  
  
## <a name="see-also"></a>関連項目

- [WCF サービス ホスト (WcfSvcHost.exe)](../../../docs/framework/wcf/wcf-service-host-wcfsvchost-exe.md)
