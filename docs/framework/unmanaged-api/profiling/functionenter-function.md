---
title: FunctionEnter 関数
ms.date: 03/30/2017
api_name:
- FunctionEnter
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- FunctionEnter
helpviewer_keywords:
- FunctionEnter function [.NET Framework profiling]
ms.assetid: bf4ffa50-4506-4dd4-aa13-a0457b47ca74
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 9279e50630ea074b70955ca8ed218cd39a613b58
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67781291"
---
# <a name="functionenter-function"></a>FunctionEnter 関数
コントロールが関数に渡されることをプロファイラーに通知します。  
  
> [!NOTE]
>  `FunctionEnter`関数は、.NET Framework version 2.0 では、非推奨し、その使用には、パフォーマンスの低下が発生します。 使用して、 [FunctionEnter2](../../../../docs/framework/unmanaged-api/profiling/functionenter2-function.md)関数を使用します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
void __stdcall FunctionEnter (  
    [in]  FunctionID funcID  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `funcID`  
 [in]コントロールが渡される関数の識別子。  
  
## <a name="remarks"></a>Remarks  
 `FunctionEnter`関数は、コールバックは、これを実装する必要があります。 実装を使用する必要があります、 `__declspec`(`naked`) ストレージ クラス属性。  
  
 実行エンジンは、この関数を呼び出す前に、レジスタを保存できません。  
  
- 項目で、浮動小数点ユニット (FPU) にあるなど、使用するすべてのレジスタを保存する必要があります。  
  
- 終了時に、その呼び出し元によってプッシュされたすべてのパラメーターをポップしてスタックを復元する必要があります。  
  
 実装`FunctionEnter`ガベージ コレクションは延期されますブロックしないでください。 実装は、ガベージ コレクションをしないで、スタックはガベージ コレクションに適した状態ではない可能性が。 ランタイムがまでブロックはガベージ コレクションが試行されると、`FunctionEnter`を返します。  
  
 また、`FunctionEnter`関数を呼び出してはならないようにまたはマネージ コードにマネージ メモリの割り当て。  
  
## <a name="requirements"></a>必要条件  
 **プラットフォーム:** [システム要件](../../../../docs/framework/get-started/system-requirements.md)に関するページを参照してください。  
  
 **ヘッダー:** CorProf.idl  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET framework のバージョン:** 1.1, 1.0  
  
## <a name="see-also"></a>関連項目

- [FunctionEnter2 関数](../../../../docs/framework/unmanaged-api/profiling/functionenter2-function.md)
- [FunctionLeave2 関数](../../../../docs/framework/unmanaged-api/profiling/functionleave2-function.md)
- [FunctionTailcall2 関数](../../../../docs/framework/unmanaged-api/profiling/functiontailcall2-function.md)
- [SetEnterLeaveFunctionHooks2 メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-setenterleavefunctionhooks2-method.md)
- [グローバル静的関数のプロファイル](../../../../docs/framework/unmanaged-api/profiling/profiling-global-static-functions.md)
