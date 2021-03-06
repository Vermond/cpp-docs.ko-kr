---
title: 지역화 및 코드 페이지
ms.date: 11/04/2016
helpviewer_keywords:
- locales [C++], about locales
- locale IDs [C++]
- locales [C++]
- code pages [C++]
- code pages [C++], dynamically changing
- character sets [C++], code pages
- multibyte code pages [C++]
- character sets [C++], locales
- localization [C++], code pages
- localization [C++], locales
- code pages [C++], locales
- conventions [C++], international character support
ms.assetid: bd937361-b6d3-4c98-af95-beb7c903187b
ms.openlocfilehash: 0015e0a7a81abbd3472a8c845a9b8c0d8caf4618
ms.sourcegitcommit: 6052185696adca270bc9bdbec45a626dd89cdcdd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50610539"
---
# <a name="locales-and-code-pages"></a>지역화 및 코드 페이지

로캘 ID는 로컬 규칙 및 특정 지리적 지역에 대 한 언어를 반영합니다. 지정된 언어는 여러 국가/지역에서 통용될 수 있습니다. 예를 들어 포르투갈어는 브라질과 포르투갈에서 통용됩니다. 반대로 한 국가/지역에 여러 개의 공식 언어가 있을 수 있습니다. 예를 들어 캐나다는 두 가지 언어: 영어 및 프랑스어입니다. 따라서 캐나다에 두 개의 고유 로캘: 캐나다 영어와 프랑스어 (캐나다). 일부 로캘 종속 범주에는 날짜 형식 지정 및 통화 값의 형식 표시가 포함됩니다.

언어는 텍스트 및 데이터 형식 규칙을 결정하고 국가 및 지역은 지역 규칙을 결정합니다. 모든 언어는 알파벳 이외의 고유 문자, 예를 들어 문장 부호나 숫자와 같은 문자가 포함된 코드 페이지를 포함합니다. 코드 페이지는 문자 집합이며 언어와 관련 있습니다. 따라서 [로캘](../c-runtime-library/locale.md)이란 언어, 국가 및 지역, 코드 페이지의 고유한 조합을 말합니다. [setlocale](../c-runtime-library/reference/setlocale-wsetlocale.md) 함수를 이용해 런타임시 로캘 및 코드 페이지 설정을 변경할 수 있습니다.

언어간에는 서로 다른 코드 페이지를 사용할 수 있습니다. 예를 들어 ANSI 코드 페이지 1252는 영어와 대부분의 유럽 언어에서 사용되고 ANSI 코드 페이지 932는 일본어 간지(Kanji)에 사용 됩니다. 사실상 거의 모든 코드 페이지는 가장 처음 값인 0x00-0x7F의 128자에 대하여 ASCII 문자와 집합을 공유합니다.

숫자 및 문장 부호 등이 포함된 싱글 바이트 코드 페이지는 256개의 바이트 값과 문자 또는 문자 모양이 서로 매칭되는 표로 표현할 수 있습니다. 더블 바이트 문자 값 역시 64k의 매우 큰 표로 멀티 바이트 코드 페이지를 표현할 수 있습니다. 그러나 실제로는 싱글 바이트와 마찬가지로 처음 256자에 대한 더블 바이트 값의 범위로 표시됩니다.

코드 페이지에 대한 자세한 내용은 [코드 페이지](../c-runtime-library/code-pages.md)를 참조하세요.

C 런타임 라이브러리에 두 가지 유형의 내부 코드 페이지: 로캘 및 멀티 바이트입니다. 프로그램 실행 중 현재 코드 페이지를 변경할 수 있습니다 (에 대 한 설명서를 참조 합니다 [setlocale](../c-runtime-library/reference/setlocale-wsetlocale.md) 하 고 [_setmbcp](../c-runtime-library/reference/setmbcp.md) 함수). 또한 런타임 라이브러리를 가져올 하 고 프로그램의 실행 기간에 대 한 상수는 운영 체제 코드 페이지의 값을 사용할 수 있습니다.

로캘 코드 페이지가 변경되면 코드 페이지에 종속되어 있는 함수들 또한 선택된 코드 페이지로 동작이 변경됩니다. 기본적으로 모든 로캘 종속 함수는 'C' 로캘에 고유한 로캘 코드 페이지를 사용하여 실행됩니다. `setlocale` 함수를 이용해 내부 로캘 코드 페이지 및 기타 로캘 관련 등록 정보를 변경할 수 있습니다. `setlocale`을 호출하면 운영체제 사용자 로캘에 지정된 로캘로 설정됩니다.

마찬가지로 멀티바이트 코드 페이지가 변경되면 멀티바이트 함수의 동작이 선택한 코드 페이지에 의해 지정되고 변경됩니다. 기본적으로 모든 멀티바이트 함수는 운영체제의 기본 코드 페이지에 해당하는 멀티바이트 코드 페이지를 사용하여 실행을 시작합니다. `_setmbcp` 함수를 사용하여 내부 멀티바이트 코드 페이지를 변경할 수 있습니다.

C 런타임 함수를 `setlocale` 설정, 변경 하거나 일부 또는 모든 현재 프로그램 로캘 정보를 쿼리 합니다. 합니다 [_wsetlocale](../c-runtime-library/reference/setlocale-wsetlocale.md) 루틴의 와이드 문자 버전이 `setlocale`; 인수 및 반환 값의 `_wsetlocale` 는 와이드 문자 문자열입니다.

## <a name="see-also"></a>참고 항목

[유니코드 및 MBCS](../text/unicode-and-mbcs.md)<br/>
[문자 집합 이식성의 이점](../text/benefits-of-character-set-portability.md)