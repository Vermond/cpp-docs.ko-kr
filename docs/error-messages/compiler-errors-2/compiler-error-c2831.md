---
title: 컴파일러 오류 C2831
ms.date: 11/04/2016
f1_keywords:
- C2831
helpviewer_keywords:
- C2831
ms.assetid: c8c04288-0889-4265-a077-17f94cbcdcc9
ms.openlocfilehash: b0708a7c45f33e30280666cf9bc903723d6a9c26
ms.sourcegitcommit: 6052185696adca270bc9bdbec45a626dd89cdcdd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50628334"
---
# <a name="compiler-error-c2831"></a>컴파일러 오류 C2831

'operator o'는 기본 매개 변수를 사용할 수 없습니다.

세 명의 연산자는 기본 매개 변수를 포함할 수 있습니다.

- [new](../../cpp/new-operator-cpp.md)

- 할당 =

- 왼쪽된 괄호 (

다음 샘플에서는 C2831 오류가 생성 됩니다.

```
// C2831.cpp
// compile with: /c
#define BINOP <=
class A {
public:
   int i;
   int operator BINOP(int x = 1) {   // C2831
   // try the following line instead
   // int operator BINOP(int x) {
      return i+x;
   }
};
```