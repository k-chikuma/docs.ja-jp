---
title: メソッド アクセスの保護
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- code security, method access
- secure coding, method access
- security [.NET Framework], method access
- method access security
ms.assetid: f7c2d6ec-3b18-4e0e-9991-acd97189d818
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 8be971cee4aa2ae09745a090396269c80ca62198
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2019
ms.locfileid: "66487944"
---
# <a name="securing-method-access"></a>メソッド アクセスの保護
[!INCLUDE[net_security_note](../../../includes/net-security-note-md.md)]  
  
 信頼関係のない任意のコードに呼び出しを許可することが不適切なメソッドがあります。 このようなメソッドには、さまざまなリスクが発生し得る。制限された情報を提供それに渡されるすべての情報と思われる場合があります。エラーは、パラメーターのチェックを行わない可能性があります。または、誤ったのパラメーターには、誤動作したり何か問題を引き起こすこと可能性があります。 これらのケースを認識し、メソッドを保護するために役立つ措置を講じる必要があります。  
  
 パブリックでの使用を目的としていないメソッドをパブリックとして使用する場合は、メソッドを制限する必要があることがあります。 たとえば、独自の DLL 経由で呼び出すインターフェイスはパブリックにする必要があります。しかし、顧客がそのインターフェイスを使用したり、悪意のあるコードがコンポーネントへのエントリ ポイントとして攻略したりするのを防ぐために、そのインターフェイスをパブリックとして公開しない場合があります。 また、パブリックではあるものの、パブリック使用を想定していないメソッドを制限する一般的な理由として、非常に内部的なインターフェイスで、ドキュメントを残したり、サポートするのを避けたりする場合も考えられます。  
  
 マネージ コードには、メソッド アクセスを制限するいくつかの方法があります。  
  
- クラス、アセンブリ、派生クラスが信頼されている場合は、これらへのアクセシビリティのスコープを制限します。 これが、メソッド アクセスを制限する最も簡単な方法です。 派生クラスが親クラスの ID を共有することがありますが、一般的に、派生クラスは派生元のクラスよりも信頼度が低くなる可能性があります。 具体的には、キーワードの信頼を推測できません**保護**、必ずしもセキュリティ コンテキストで使用するされません。  
  
- 指定した id の基本的には、特定の呼び出し元にメソッド アクセスを制限[証拠](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/7y5x1hcd%28v=vs.100%29)(厳密な名前、発行者、ゾーン、およびなど) を選択します。  
  
- 選択したアクセス許可を持つ呼び出し元だけにメソッド アクセスを制限します。  
  
 同様に、宣言セキュリティを使用すると、クラスの継承を制御できます。 使用することができます**InheritanceDemand**以下を実行します。  
  
- 派生したクラスに、特定の ID またはアクセス許可を要求します。  
  
- 特定のメソッドをオーバーライドする派生クラスに、特定の ID またはアクセス許可を要求します。  
  
 呼び出し元に特定の厳密な名前による署名を要求することによってアクセスを制限し、パブリック クラスの保護に役立つ方法の例を次に示します。 この例では、<xref:System.Security.Permissions.StrongNameIdentityPermissionAttribute>で、**デマンド**の厳密な名前。 厳密な名前でアセンブリに署名する方法のタスク ベースの情報を参照してください。[の作成と using strong-named Assemblies](../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md)します。  
  
```vb  
<StrongNameIdentityPermissionAttribute(SecurityAction.Demand, PublicKey := "…hex…", Name := "App1", Version := "0.0.0.0")>  _  
Public Class Class1  
End Class  
```  
  
```csharp  
[StrongNameIdentityPermissionAttribute(SecurityAction.Demand, PublicKey="…hex…", Name="App1", Version="0.0.0.0")]  
public class Class1  
{  
  
}   
```  
  
## <a name="excluding-classes-and-members-from-use-by-untrusted-code"></a>クラスとメンバーを信頼関係のないコードが使用できないようにする  
 このセクションで示す宣言を使用すると、特定のクラスとメソッド、およびプロパティとイベントが部分的な信頼のコードによって使用されるのを防ぐことができます。 これらの宣言をクラスに適用すると、すべてのメソッド、プロパティ、イベントが保護されますが、フィールドへのアクセスは宣言セキュリティの影響を受けないため、注意が必要です。 また、リンク確認要求は直前の呼び出し元に対して保護できるようにするだけで、攻撃を受ける可能性が残っています。  
  
> [!NOTE]
>  新しい透過性モデルが .NET Framework 4 で導入されました。 [透過的セキュリティ コード、レベル 2](../../../docs/framework/misc/security-transparent-code-level-2.md)モデルをセキュリティで保護されたコードの識別、<xref:System.Security.SecurityCriticalAttribute>属性。 セキュリティ クリティカル コードでは、呼び出し元と継承先の両方が完全に信頼されていることが必要です。 .NET Framework の以前のバージョンのコード アクセス セキュリティ規則で実行されているアセンブリは、レベル 2 のアセンブリを呼び出すことができます。 この場合、セキュリティ クリティカル属性は、完全な信頼のためのリンク確認要求として扱われます。  
  
 アセンブリの厳密な名前で、 [LinkDemand](../../../docs/framework/misc/link-demands.md)すべてのパブリックにアクセスできるメソッド、プロパティ、および完全に信頼された呼び出し元への使用を制限するには、その中のイベントに適用されます。 この機能を無効にするには、<xref:System.Security.AllowPartiallyTrustedCallersAttribute> 属性を適用する必要があります。 このため、信頼関係のない呼び出し元を除外するクラスを明示的に指定することは、署名のないアセンブリまたはこの属性を持つアセンブリだけに必要です。これらの宣言を使用して、信頼関係のない呼び出し元からの利用を想定していない型のサブセットをマークできます。  
  
 クラスおよびメンバーを信頼関係のないコードによって使用されるのを防ぐ方法の例を次に示します。  
  
 パブリックの非シール クラスの場合:  
  
```vb  
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name := "FullTrust"), _   
System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name := "FullTrust")>  _  
Public Class CanDeriveFromMe  
End Class  
```  
  
```csharp  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name="FullTrust")]  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name="FullTrust")]  
public class CanDeriveFromMe  
{  
}  
```  
  
 パブリックのシール クラスの場合:  
  
```vb  
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name := "FullTrust")>  _  
NotInheritable Public Class CannotDeriveFromMe  
End Class  
```  
  
```csharp  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name="FullTrust")]  
public sealed class CannotDeriveFromMe  
{  
}  
```  
  
 パブリックの抽象クラスの場合:  
  
```vb  
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name := "FullTrust"), _  
System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name := "FullTrust")>  _  
MustInherit Public Class CannotCreateInstanceOfMe_CanCastToMe  
End Class  
```  
  
```csharp  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name="FullTrust")]  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name="FullTrust")]  
public abstract class CannotCreateInstanceOfMe_CanCastToMe {}  
```  
  
 パブリックの仮想関数の場合:  
  
```vb  
Class Base1   
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name:="FullTrust"), System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name:="FullTrust")> _  
    Public Overridable Sub CanOverrideOrCallMe()  
    End Sub 'CanOverrideOrCallMe  
End Class 'Base1  
```  
  
```csharp  
class Base1   
{  
[System.Security.Permissions.PermissionSetAttribute(  
System.Security.Permissions.SecurityAction.InheritanceDemand, Name="FullTrust")]  
[System.Security.Permissions.PermissionSetAttribute(  
System.Security.Permissions.SecurityAction.LinkDemand, Name="FullTrust")]  
    public virtual void CanOverrideOrCallMe() {}  
}  
```  
  
 パブリックの抽象関数の場合:  
  
```vb  
MustInherit Class Base2  
    <System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name:="FullTrust"), System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name:="FullTrust")> _  
    Public Sub MustOverrideMe()  
    End Sub  
End Class 'Base2  
```  
  
```csharp  
abstract class Base2 {  
[System.Security.Permissions.PermissionSetAttribute(  
System.Security.Permissions.SecurityAction.InheritanceDemand, Name = "FullTrust")]  
[System.Security.Permissions.PermissionSetAttribute(  
System.Security.Permissions.SecurityAction.LinkDemand, Name = "FullTrust")]  
public abstract void MustOverrideMe();  
}  
```  
  
 基本クラスが完全な信頼を確認要求しない、パブリック オーバーライド関数の場合:  
  
```vb  
Class Derived  
    Inherits Base1  
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.Demand, Name:="FullTrust")> _  
    Public Overrides Sub CanOverrideOrCallMe()  
        MyBase.CanOverrideOrCallMe()  
    End Sub 'CanOverrideOrCallMe  
End Class 'Derived  
```  
  
```csharp  
class Derived : Base1  
{     
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.Demand, Name="FullTrust")]      
    public override void CanOverrideOrCallMe()   
    {  
        base.CanOverrideOrCallMe();  
    }  
}  
```  
  
 基本クラスが完全な信頼を確認要求する、パブリック オーバーライド関数の場合:  
  
```vb  
Class Derived  
    Inherits Base1  
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name:="FullTrust")> _  
    Public Overrides Sub CanOverrideOrCallMe()  
        MyBase.CanOverrideOrCallMe()  
    End Sub 'CanOverrideOrCallMe   
End Class 'Derived  
```  
  
```csharp  
class Derived : Base1  
{     
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name="FullTrust")]      
    public override void CanOverrideOrCallMe()   
    {  
        base.CanOverrideOrCallMe();  
    }  
}  
```  
  
 パブリック インターフェイスの場合:  
  
```vb  
Public Interface ICanCastToMe  
    <System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name:="FullTrust"), System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name:="FullTrust")> _  
    Sub CanImplementMe()  
End Interface 'ICanCastToMe  
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name:="FullTrust"), System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name:="FullTrust")> _  
Class Implemented  
    Implements ICanCastToMe  
    Public Sub CanImplementMe()  
    End Sub 'CanImplementMe  
```  
  
```csharp  
public interface ICanCastToMe   
{  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name = "FullTrust")]  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name = "FullTrust")]  
void CanImplementMe();  
}  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name = "FullTrust")]  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name = "FullTrust")]  
class Implemented : ICanCastToMe  
{  
    public void CanImplementMe()  
    {  
    }  
}  
```  
  
## <a name="virtual-internal-overrides-or-overloads-overridable-friend"></a>Virtual Internal Overrides または Overloads Overridable Friend  
  
> [!NOTE]
>  このセクションでは、両方のメソッドを宣言するときにセキュリティ上の問題について警告`virtual`と`internal`(`Overloads` `Overridable` `Friend` Visual Basic で)。 この警告は、.NET Framework version 1.0 および 1.1 にのみ適用されます、以降のバージョンには適用されません。  
  
 .NET Framework バージョン 1.0 および 1.1 では、する必要があります型システムのアクセシビリティの微妙な違いに注意してください。 コードが他のアセンブリを使用できないことを確認するときにします。 宣言されているメソッド**仮想**と**内部**(**Overloads Overridable Friend** Visual basic)、親クラスの vtable エントリを上書きできからのみ使用できます。同じアセンブリ内で内部があるためです。 ただし、オーバーライドのアクセシビリティはによって決定、**仮想**キーワード、およびそのコードがクラス自体へのアクセスを持っている限り、別のアセンブリからオーバーライドするこのことができます。 オーバーライドの可能性が問題を表している場合は、宣言セキュリティを使用して、修正するか、または削除する、**仮想**キーワードの場合、これは必須ではありません。  
  
 ある言語コンパイラがコンパイル エラーによってこれらのオーバーライドを防いだとしても、他のコンパイラによって記述されたコードがオーバーライドする可能性があります。  
  
## <a name="see-also"></a>関連項目

- [安全なコーディングのガイドライン](../../../docs/standard/security/secure-coding-guidelines.md)
