---
title: 자동 병렬화 및 자동 벡터화
ms.date: 11/04/2016
ms.assetid: ec71583a-287b-4599-8767-1d255e080fe3
ms.openlocfilehash: 06ab255e7769bfa56d5a8d22cdbe19d415ce6b31
ms.sourcegitcommit: 6052185696adca270bc9bdbec45a626dd89cdcdd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50618346"
---
# <a name="auto-parallelization-and-auto-vectorization"></a>자동 병렬화 및 자동 벡터화

자동 평행화 도우미 및 자동 벡터화 도우미는 코드의 루프 성능을 자동으로 향상시키기 위해 설계되었습니다.

## <a name="auto-parallelizer"></a>자동 평행화 도우미

합니다 [/Qpar](../build/reference/qpar-auto-parallelizer.md) 컴파일러 스위치를 사용 하면 *자동 병렬화* 코드에서 루프입니다. 기존 코드를 변경하지 않고 이 플래그를 지정하면 컴파일러는 코드를 평가하여 평행화에서 이점을 얻을 수 있는 루프를 찾습니다. 많은 작업을 수행하지 않아 평행화의 이점을 얻지 못하는 루프가 있을 수 있고 불필요한 모든 평행화가 스레드 풀 생성, 추가 동기화 또는 성능 향상보다는 성능을 저하시키는 기타 처리를 발생시킬 수 있으므로 컴파일러는 평행화할 루프를 선택하는 데 다소 신중합니다. 예를 들어 루프의 상한값이 컴파일 타임에 알려지지 않은 다음 예를 고려할 수 있습니다.

```cpp
void loop_test(int u) {
   for (int i=0; i<u; ++i)
      A[i] = B[i] * C[i];
}
```

`u`는 작은 값이 될 수 있으므로 컴파일러는 이 루프를 자동으로 평행화하지는 않습니다. 그러나 `u`가 항상 큰 값이 되는 것을 아는 경우 사용자는 이를 평행화하려 할 수 있습니다. 자동 병렬화를 사용 하려면 지정 [#pragma hint_parallel](../preprocessor/loop.md)여기서 `n` 평행 스레드 수입니다. 다음 예에서 컴파일러는 8개 스레드에 걸쳐 루프를 평행화하려고 합니다.

```cpp
void loop_test(int u) {
#pragma loop(hint_parallel(8))
   for (int i=0; i<u; ++i)
      A[i] = B[i] * C[i];
}
```

모든와 마찬가지로 [pragma 지시문](../preprocessor/pragma-directives-and-the-pragma-keyword.md), 대체 pragma 구문 `__pragma(loop(hint_parallel(n)))` 도 지원 됩니다.

사용자가 원하더라도 컴파일러가 평행화할 수 없는 루프도 있습니다. 예를 들면 다음과 같습니다.

```cpp
#pragma loop(hint_parallel(8))
for (int i=0; i<upper_bound(); ++i)
    A[i] = B[i] * C[i];
```

`upper_bound()` 함수는 호출될 때마다 변경될 수 있습니다. 상한값을 알 수 없으므로 컴파일러는 이 루프를 평행화할 수 없는 이유를 설명하는 진단 메시지를 내보낼 수 있습니다. 다음 예에서는 평행화할 수 있는 루프, 평행화할 수 없는 루프, 명령 프롬프트에서 사용할 컴파일러 구문 및 각 명령줄 옵션에 대한 컴파일러 구문을 보여 줍니다.

```cpp
int A[1000];
void test() {
#pragma loop(hint_parallel(0))
    for (int i=0; i<1000; ++i) {
        A[i] = A[i] + 1;
    }

    for (int i=1000; i<2000; ++i) {
        A[i] = A[i] + 1;
    }
}
```

다음 명령어를 사용하여 컴파일 시:

`cl d:\myproject\mylooptest.cpp /O2 /Qpar /Qpar-report:1`

출력 결과:

```Output
--- Analyzing function: void __cdecl test(void)
d:\myproject\mytest.cpp(4) : loop parallelized
```

다음 명령어를 사용하여 컴파일 시:

`cl d:\myproject\mylooptest.cpp /O2 /Qpar /Qpar-report:2`

출력 결과:

```Output
--- Analyzing function: void __cdecl test(void)
d:\myproject\mytest.cpp(4) : loop parallelized
d:\myproject\mytest.cpp(4) : loop not parallelized due to reason '1008'
```

두 가지 간 출력 차이 확인할 수 있습니다 [/Qpar-report (자동 평행 화 도우미 보고 수준)](../build/reference/qpar-report-auto-parallelizer-reporting-level.md) 옵션입니다. `/Qpar-report:1`은 공적으로 평행화된 루프에 대해서만 평행화 도우미 메시지를 출력합니다. `/Qpar-report:2`는 성공 및 실패한 루프 평행화 둘 모두에 대해 평행화 도우미 메시지를 출력합니다.

이유 코드 및 메시지에 대 한 자세한 내용은 참조 하세요. [벡터화 도우미 및 평행 화 도우미 메시지](../error-messages/tool-errors/vectorizer-and-parallelizer-messages.md)합니다.

## <a name="auto-vectorizer"></a>자동 벡터화 도우미

자동 벡터화 도우미는 코드의 루프를 분석하고 가능한 경우 대상 컴퓨터에서 벡터 레지스터 및 명령을 사용하여 루프를 실행합니다. 이를 통해 코드 성능을 향상시킬 수 있습니다. Intel 또는 AMD 프로세서의 SSE2, AVX 및 AVX2 지침 또는 ARM 프로세서의 NEON 명령을 대상으로 하는 컴파일러에 따라 합니다 [/arch](../build/reference/arch-minimum-cpu-architecture.md) 전환 합니다.

자동 벡터화 도우미는 `/arch` 스위치로 지정한 것과는 다른 명령을 생성할 수 있습니다. 이러한 명령은 런타임 검사를 통해 코드가 제대로 실행되는지 확인됩니다. 예를 들어 `/arch:SSE2`를 컴파일하는 경우 SSE4.2 명령을 내보낼 수 있습니다. 런타임 검사는 대상 프로세서에서 SSE4.2를 사용할 수 있는지 확인한 후 프로세서가 해당 명령을 지원하지 않을 경우 비 SSE4.2 버전의 루프로 건너뜁니다.

기본적으로 자동 벡터화 도우미는 사용할 수 있게 설정되어 있습니다. 벡터화 상태에서 코드의 성능을 비교 하려는 경우 사용할 수 있습니다 [#pragma loop (no_vector)](../preprocessor/loop.md) 지정된 된 루프의 벡터화를 사용 하지 않도록 설정 합니다.

```cpp
#pragma loop(no_vector)
for (int i = 0; i < 1000; ++i)
   A[i] = B[i] + C[i];
```

모든와 마찬가지로 [pragma 지시문](../preprocessor/pragma-directives-and-the-pragma-keyword.md), 대체 pragma 구문 `__pragma(loop(no_vector))` 도 지원 됩니다.

자동 병렬화를 사용 하 여 지정할 수는 [/Qvec-report (자동 벡터화 도우미 보고 수준)](../build/reference/qvec-report-auto-vectorizer-reporting-level.md) 명령줄 옵션을 보고 하거나 성공적으로 벡터화 된 루프만-`/Qvec-report:1`-또는 둘 다 성공적으로 및 실패 한 루프를 벡터화-`/Qvec-report:2`).

이유 코드 및 메시지에 대 한 자세한 내용은 참조 하세요. [벡터화 도우미 및 평행 화 도우미 메시지](../error-messages/tool-errors/vectorizer-and-parallelizer-messages.md)합니다.

실제로 벡터화 도우미가 작동 하는 방법을 보여 주는 예제를 참조 하세요. [프로젝트 오스틴 6의 2 부: 페이지 컬링](http://blogs.msdn.com/b/vcblog/archive/2012/09/27/10348494.aspx)

## <a name="see-also"></a>참고 항목

[loop](../preprocessor/loop.md)<br/>
[네이티브 코드의 병렬 프로그래밍](http://go.microsoft.com/fwlink/p/?linkid=263662)<br/>
[/Qpar(자동 평행화 도우미)](../build/reference/qpar-auto-parallelizer.md)<br/>
[/Qpar-report(자동 평행화 도우미 보고 수준)](../build/reference/qpar-report-auto-parallelizer-reporting-level.md)<br/>
[/Qvec-report(자동 벡터화 도우미 보고 수준)](../build/reference/qvec-report-auto-vectorizer-reporting-level.md)<br/>
[벡터화 도우미 및 평행화 도우미 메시지](../error-messages/tool-errors/vectorizer-and-parallelizer-messages.md)