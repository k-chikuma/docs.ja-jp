---
title: ML.NET CLI を使用してモデルのトレーニングを自動化する
description: ML.NET CLI ツールを使用してコマンドラインから最適なモデルを自動的にトレーニングする方法について説明します。
author: CESARDELATORRE
ms.date: 04/17/2019
ms.custom: how-to
ms.openlocfilehash: 33383582140d9df4290a0bbf30659301af837d1d
ms.sourcegitcommit: ca2ca60e6f5ea327f164be7ce26d9599e0f85fe4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65065895"
---
# <a name="automate-model-training-with-the-mlnet-cli"></a>ML.NET CLI を使用してモデルのトレーニングを自動化する

ML.NET CLI は、ML.NET を学習する .NET 開発者のために ML.NET を "民主化" するものです。

(ML.NET AutoML CLI を使用せずに) ML.NET API を単独で使用するには、トレーナー (特定のタスクに対する機械学習アルゴリズムの実装) と、データに適用する一連のデータ変換 (特徴エンジニアリング) を選択する必要があります。 最適なパイプラインはデータセットごとに異なるので、すべての選択肢から最適なアルゴリズムを選択すると、複雑さが増します。 さらに、各アルゴリズムには調整が必要な一連のハイパーパラメーターがあります。 そのため、特徴エンジニアリング、学習アルゴリズム、およびハイパーパラメーターの最適な組み合わせを見つけようとすると、機械学習モデルの最適化に数週間から数か月かかる可能性があります。

このプロセスは、ML.NET AutoML インテリジェント エンジンが実装されている ML.NET CLI を使用して自動化できます。 

> [!NOTE]
> このトピックは、現在プレビュー段階の ML.NET **CLI** と ML.NET **AutoML** について述べており、内容が変更される場合があります。 

## <a name="what-is-the-mlnet-command-line-interface-cli"></a>ML.NET コマンドライン インターフェイス (CLI) とは

ML.NET CLI は任意のコマンドプロンプト (Windows、Mac、または Linux) で実行して、トレーニング データセットに基づいて高品質の ML.NET モデルとソース コードを生成できます。

次の図に示すように、高品質の ML.NET モデル (シリアル化されたモデルの .zip ファイル) と、そのモデルを実行/スコア付けするサンプル C# コードを簡単に生成できます。 さらに、そのモデルを作成/トレーニングする C# コードも生成されるので、その生成された "最適なモデル" に使用されるアルゴリズムと設定を調べ、反復処理することができます。 

![画像](media/automate-training-with-cli/cli-high-level-process.png "ML.NET CLI 内で動作する AutoML エンジン")

自力でコーディングすることなく、所有しているデータセットからこうした資産を生成できるので、ML.NET について知っている場合でも生産性が向上します。

現在、ML.NET CLI でサポートされている ML タスクは次のとおりです。

- `binary-classification`
- `multiclass-classification` 
- `regression`
- 予定: `recommendation`、`ranking`、`anomaly-detection`、`clustering` などの他の機械学習タスク

使用例:

```console
> mlnet auto-train --task binary-classification --dataset "customer-feedback.tsv" --label-column-name Sentiment
```

![イメージ](media/automate-training-with-cli/cli-model-generation.gif)

*Windows PowerShell*、*macOS/Linux bash、または *Windows CMD* でも同じ方法で実行できます。 ただし、タブのオートコンプリート (パラメーター候補) は *Windows CMD* では機能しません。

## <a name="output-assets-generated"></a>生成される出力資産

CLI `auto-train` コマンドを使用すると、出力フォルダーに以下の資産が生成されます。

- 予測を実行する準備が完了したシリアル化されたモデル .zip ("最適なモデル")。 
- C# ソリューション:
    - その生成されたモデルを実行/スコア付けする C# コード (そのモデルを使用してエンドユーザー アプリで予測を行うため)。
    - そのモデルの生成に使用されるトレーニング コードを含む C# コード (学習目的またはモデルの再トレーニングのため)。
- 詳細な構成/パイプラインなど、評価される複数のアルゴリズム全体にわたるすべての反復処理/スイープの情報を含むログ ファイル。

最初の 2 つの資産は、その生成された ML モデルを使用して予測を行うために、エンドユーザー アプリ (ASP.NET Core Web アプリ、サービス、デスクトップ アプリなど) で直接使用できます。

3 つ目の資産のトレーニング コードは、生成されたモデルをトレーニングするために CLI によって使用された ML.NET API コードを示しています。そのため、モデルを再トレーニングし、背後で CLI および ML.NET AutoML エンジンによって選択された特定のトレーナー/アルゴリズムとハイパーパラメーターを調べて反復処理することができます。 

## <a name="understanding-the-quality-of-the-model"></a>モデルの品質を理解する

CLI ツールを使用して "最適なモデル" を生成すると、対象の ML タスクに適した品質メトリック (正確度、R-2 乗など) が表示されます。

ここでは、自動生成された "最適なモデル" の品質を理解できるように、これらのメトリックを ML タスク別にグループ化してまとめています。

### <a name="metrics-for-binary-classification-models"></a>二値分類モデルのメトリック

 CLI によって検出される上位 5 つのモデルの二項分類 ML タスク メトリック一覧を次に示します。 

![イメージ](media/automate-training-with-cli/cli-binary-classification-metrics.png)

正確度は分類問題の一般的なメトリックですが、以下のリファレンスで説明されているように、最適なモデルを選択する場合に正確度が常に最適なメトリックとは限りません。 必要に応じて追加のメトリックを使用してモデルの品質を評価する場合があります。

CLI によって出力されるメトリックを調べて理解するには、「[Metrics for binary classification (二項分類のメトリック)](resources/metrics.md#metrics-for-binary-classification)」を参照してください。

### <a name="metrics-for-multi-class-classification-models"></a>多クラス分類モデルのメトリック

 CLI によって検出される上位 5 つのモデルの多クラス分類 ML タスク メトリック一覧を次に示します。 

![イメージ](media/automate-training-with-cli/cli-multiclass-classification-metrics.png)

CLI によって出力されるメトリックを調べて理解するには、「[Metrics for multiclass classification (多クラス分類のメトリック)](resources/metrics.md#metrics-for-multi-class-classification)」を参照してください。

### <a name="metrics-for-regression-models"></a>回帰モデルのメトリック

観測値とモデルの予測値の差が小さく偏りがない場合、回帰モデルがデータに適しています。 回帰は特定のメトリックを使用して評価できます。

CLI によって検出される上位 5 つの高品質モデルの同様のメトリック一覧が表示されます。 回帰 ML タスクに関連するこの特定のケースでは、次のようになります。

![イメージ](media/automate-training-with-cli/cli-regression-metrics.png)

CLI によって出力されるメトリックを調べて理解するには、「[Metrics for regression (回帰のメトリック)](resources/metrics.md#metrics-for-regression)」を参照してください。

## <a name="see-also"></a>関連項目

- [ML.NET CLI ツールのインストール方法](how-to-guides/install-ml-net-cli.md)
- [チュートリアル: ML.NET CLI を使用して二項分類子を自動生成する](tutorials/mlnet-cli.md)
- [ML.NET CLI コマンド リファレンス](reference/ml-net-cli-reference.md)
- [ML.NET CLI のテレメトリ](resources/ml-net-cli-telemetry.md)
