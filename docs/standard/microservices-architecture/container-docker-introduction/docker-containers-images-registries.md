---
title: Docker コンテナー、イメージ、レジストリ
description: コンテナー化された .NET アプリケーションの .NET マイクロサービス アーキテクチャ | Docker コンテナー、イメージ、レジストリ
ms.date: 08/31/2018
ms.openlocfilehash: 520f8d4d54f1fdd227ff9a1e88660b62e75f927f
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65639909"
---
# <a name="docker-containers-images-and-registries"></a>Docker コンテナー、イメージ、レジストリ

Docker を使用する場合、開発者はアプリケーションまたはサービスを作成し、そのアプリケーションまたはサービスとその依存関係をコンテナー イメージにパッケージ化します。 イメージとは、アプリケーションまたはサービスと、その構成と依存関係の静的な表現です。

アプリケーションまたはサービスを実行するために、アプリケーションのイメージはインスタンス化され、コンテナーが作成されます。このコンテナーが Docker ホスト上で実行されます。 コンテナーは、最初に開発環境または PC でテストされます。

開発者はイメージをレジストリに保存する必要があります。レジストリはイメージのライブラリとして機能し、実稼働環境のオーケストレーターに展開するときに必要になります。 Docker は [Docker Hub](https://hub.docker.com/) 経由で公開レジストリを保守します。他のベンダーは、[Azure Container Registry](https://azure.microsoft.com/services/container-registry/)を含むさまざまなイメージのコレクション用のレジストリを用意しています。 また、企業は自社の Docker イメージ用に非公開のレジストリをオンプレミスに持つことができます。

図 2-4 は、Docker のイメージとレジストリが他のコンポーネントとどのように関係しているかを示しています。 また、ベンダーから提供される複数のレジストリも示しています。

![Docker での基本的な分類:レジストリはイメージが格納される本棚のようなものであり、サービスや Web アプリを実行するコンテナーを構築するためにプルして使用できます。 オンプレミス上とパブリック クラウド上にプライベート Docker レジストリがあります。 Docker Hub はエンタープライズ級のソリューションである Docker Trusted Registry と共に Docker によって管理されるパブリック レジストリであり、Azure では Azure Container Registry を提供しています。 AWS や Google などにもコンテナー レジストリがあります。](./media/image5.PNG)

**図 2-4** Docker の用語と概念の分類

レジストリにイメージを配置すると、フレームワーク レベルのすべての依存関係を含め、静的で不変なアプリケーション ビットを格納できます。 このようなイメージは複数の環境でバージョン管理および展開できるので、一貫した展開ユニットを提供できます。

オンプレミスまたはクラウドでホストされる非公開のイメージ レジストリは、次の場合に推奨されます。

- 機密保持のためにイメージを一般公開して共有することができない場合。

- イメージと選択した展開環境間のネットワーク待機時間を最小限に抑えたい場合。 たとえば、実稼働環境が Azure クラウドの場合は、[Azure Container Registry](https://azure.microsoft.com/services/container-registry/) にイメージを保存して、ネットワークの待機時間を最小限に抑える方法があります。 同様に、実稼働環境がオンプレミスの場合は、同じローカル ネットワーク内でオンプレミスの Docker Trusted Registry を使用できるようにする方法があります。

>[!div class="step-by-step"]
>[前へ](docker-terminology.md)
>[次へ](../net-core-net-framework-containers/index.md)
