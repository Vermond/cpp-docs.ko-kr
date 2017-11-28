---
title: noexcept (c + +) | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: cpp-language
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: noexcept_cpp
dev_langs: C++
ms.assetid: df24edb9-c6a6-4e37-9914-fd5c0c3716a8
caps.latest.revision: "5"
author: mikeblome
ms.author: mblome
manager: ghogen
ms.openlocfilehash: a45a15fcc2e29a31bc43ab493aa15b58985bf336
ms.sourcegitcommit: ebec1d449f2bd98aa851667c2bfeb7e27ce657b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/24/2017
---
# <a name="noexcept-c"></a>noexcept(C++)
**C + + 11:** 함수 예외가 throw 될 가능성이 있는지 여부를 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
> *noexcept 식*:  
> &nbsp;&nbsp;&nbsp;&nbsp;**noexcept**  
> &nbsp;&nbsp;&nbsp;&nbsp;**noexcept (** *문* **)**  
  
### <a name="parameters"></a>매개 변수  
 *상수 식*  
 형식의 상수 식은 `bool` 잠재적인 예외 형식 집합이 비어 있는지 여부를 나타내는입니다. 비 조건부 버전은 `noexcept(true)`합니다.  
  
## <a name="remarks"></a>설명  
 A *noexcept 식* 는 일종의 *예외 사양이*, 종료 하는 모든 예외에 대 한 예외 처리기에서 일치 시킬 수 있는 형식 집합을 나타내는 함수 선언에는 접미사는 함수입니다. 단항 조건부 연산자 `noexcept(` *constant_expression* `)` 여기서 *constant_expression* yeilds `true`, 및 해당 무조건 동의어 `noexcept`, 함수 종료 될 수 있는 잠재적인 예외 형식 집합이 비어 있는지를 지정 합니다. 즉, 함수는 예외를 throw 할 및 예외가 해당 범위 외부 전파는 사용할 수 있습니다. 연산자 `noexcept(` *constant_expression* `)` 여기서 *constant_expression* yeilds `false`, 또는 예외 사양이 없는 경우 (다른 보다에 대 한는 소멸자 또는 할당 해제 함수)는 함수가 종료 될 수 있는 잠재적인 예외 집합을 모든 형식의 집합 임을 나타냅니다.  
 
 함수로 표시 `noexcept` 직접 또는 간접적으로 호출 하는 모든 함수는 또한 하는 경우에 `noexcept` 또는 `const`합니다. 컴파일러 최대 생성 될 수 있는 예외에 대 한 모든 코드 경로 반드시 확인 하지 않습니다는 `noexcept` 함수입니다. 예외가 않습니다 표시 된 함수의 외부 범위를 종료 하는 경우 `noexcept`, [std:: terminate](../standard-library/exception-functions.md#terminate) 가 즉시 호출 및 모든 범위에 개체의 소멸자가 호출 될 보장 되지 않습니다. 사용 하 여 `noexcept` 동적 예외 지정자는 대신 `throw`, C + + 11에서 사용 되지 않습니다 되며 Visual Studio에서 나중에 완전히 구현입니다. 적용 하는 것이 좋습니다 `noexcept` 예외가 호출 스택으로 전파 하는 데는 사용할 수 있는 모든 함수에 있습니다. 함수를 선언 `noexcept`, 다양 한 컨텍스트에서 보다 효율적인 코드를 생성 하도록 컴파일러에 있습니다.    
  
## <a name="example"></a>예제  
해당 인수를 복사 하는 템플릿 함수를 선언할 수 있습니다 `noexcept` 복사 중인 개체가 일반 이전 데이터 형식 (POD) 조건을 사용 하 여 합니다. 이러한 함수는 다음과 같이 선언될 수 있습니다.  
  
```cpp  
#include <type_traits>  
  
template <typename T>  
T copy_object(const T& obj) noexcept(std::is_pod<T>)  
{  
   // ...   
}  
```  
  
## <a name="see-also"></a>참고 항목  
 [C + + 예외 처리](../cpp/cpp-exception-handling.md) [예외 사양 (throw, noexcept)](../cpp/exception-specifications-throw-cpp.md)