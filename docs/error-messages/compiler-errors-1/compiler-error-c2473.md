---
title: 컴파일러 오류 C2473
ms.date: 11/04/2016
f1_keywords:
- C2473
helpviewer_keywords:
- C2473
ms.assetid: 6bb7dbf5-b198-490f-860e-fd64d0c2a284
ms.openlocfilehash: 232f89a714d70c6914b73a370c5f658ff4283ab4
ms.sourcegitcommit: 6052185696adca270bc9bdbec45a626dd89cdcdd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50631792"
---
# <a name="compiler-error-c2473"></a>컴파일러 오류 C2473

'identifier': 함수 정의로 보이지만 매개 변수 목록이 없습니다.

컴파일러가 매개 변수 목록 없이 함수처럼 보이는 항목을 발견했습니다.

## <a name="example"></a>예제

다음 샘플에서는 C2473을 생성합니다.

```
// C2473.cpp
// compile with: /clr /c
class A {
   int i {}   // C2473
};

class B {
   int i() {}   // OK
};
```