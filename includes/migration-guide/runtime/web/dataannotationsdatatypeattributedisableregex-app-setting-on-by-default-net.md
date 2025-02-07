---
ms.openlocfilehash: 4a31310551cea4250275843da3eae927bad23840
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/18/2019
ms.locfileid: "59804347"
---
### <a name="dataannotationsdatatypeattributedisableregex-app-setting-is-on-by-default-in-net-framework-472"></a>.NET Framework 4.7.2 で "dataAnnotations:dataTypeAttribute:disableRegEx" アプリ設定が既定で有効になっている

|   |   |
|---|---|
|説明|.NET framework 4.6.1 で、データ型属性 (<xref:System.ComponentModel.DataAnnotations.EmailAddressAttribute?displayProperty=nameWithType>、<xref:System.ComponentModel.DataAnnotations.UrlAttribute?displayProperty=nameWithType>、<xref:System.ComponentModel.DataAnnotations.PhoneAttribute?displayProperty=nameWithType> など) で正規表現の使用を無効にするアプリ設定 (<code>&quot;dataAnnotations:dataTypeAttribute:disableRegEx&quot;</code>) が導入されました。 これにより、特定の正規表現を使用するサービス拒否攻撃の可能性を回避できるなど、セキュリティの脆弱性を軽減できます。<br/>.NET Framework 4.6.1 で、正規表現の使用を無効にするこのアプリ設定が、既定で <code>false</code> に設定されました。 .NET Framework 4.7.2 からは、この構成スイッチが既定で <code>true</code> に設定され、.NET Framework 4.7.2 以降を対象とする Web アプリケーションのセキュリティの脆弱性がさらに軽減されています。|
|提案される解決策|.NET Framework 4.7.2 へのアップグレード後に Web アプリケーションの正規表現が動作しない場合は、<code>&quot;dataAnnotations:dataTypeAttribute:disableRegEx&quot;</code> 設定の値を <code>false</code> に更新して以前の動作に戻すことができます。<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;appsettings&gt;&#13;&#10;...&#13;&#10;&lt;add key=&quot;dataAnnotations:dataTypeAttribute:disableRegEx&quot; value=&quot;false&quot;/&gt;&#13;&#10;...&#13;&#10;&lt;/appsettings&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>|
|スコープ|マイナー|
|Version|4.7.2|
|型|ランタイム|
