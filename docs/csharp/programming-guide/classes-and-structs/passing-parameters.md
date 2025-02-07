---
title: パラメーターの引き渡し - C# プログラミング ガイド
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- parameters [C#], passing
- passing parameters [C#]
- arguments [C#]
- methods [C#], passing parameters
- C# language, method parameters
ms.assetid: a5c3003f-7441-4710-b8b1-c79de77e0b77
ms.openlocfilehash: 77228def3a6426b6e0383d657c2eaeac37e5e273
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64600136"
---
# <a name="passing-parameters-c-programming-guide"></a>パラメーターの引き渡し (C# プログラミング ガイド)
C# では、引数を値または参照によってパラメーターに渡すことができます。 参照渡しでは、関数メンバー、メソッド、プロパティ、インデクサー、演算子、およびコンストラクターは、パラメーターの値を変更でき、その変更を呼び出し元の環境で永続化できます。 値を変更する目的でパラメーターを参照で渡すには、`ref` または `out` キーワードを使用します。 値を変更せずにコピーを回避する目的で参照で渡すには、`in` 修飾子を使用します。 ここでは、説明を簡単にするために、例に `ref` キーワードだけを使用しています。 `in`、`ref`、`out` の違いの詳細については、[in](../../../csharp/language-reference/keywords/in-parameter-modifier.md)、[ref](../../../csharp/language-reference/keywords/ref.md)、[out](../../../csharp/language-reference/keywords/out-parameter-modifier.md) に関するページを参照してください。  
  
 次の例は、値パラメーターと参照パラメーターの違いを示しています。  
  
 [!code-csharp[csProgGuideParameters#10](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideParameters/CS/Parameters.cs#10)]  
  
 詳細については、次のトピックを参照してください。  
  
- [値型パラメーターの引き渡し](../../../csharp/programming-guide/classes-and-structs/passing-value-type-parameters.md)  
  
- [参照型パラメーターの引き渡し](../../../csharp/programming-guide/classes-and-structs/passing-reference-type-parameters.md)  
  
## <a name="c-language-specification"></a>C# 言語仕様  

詳細については、[C# 言語の仕様](../../language-reference/language-specification/index.md)に関する記事の[引数リスト](~/_csharplang/spec/expressions.md#argument-lists)を参照してください。 言語仕様は、C# の構文と使用法に関する信頼性のある情報源です。
  
## <a name="see-also"></a>関連項目

- [C# プログラミング ガイド](../../../csharp/programming-guide/index.md)
- [メソッド](../../../csharp/programming-guide/classes-and-structs/methods.md)
