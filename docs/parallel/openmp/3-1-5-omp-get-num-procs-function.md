---
title: 3.1.5 omp_get_num_procs 함수
ms.date: 11/04/2016
ms.assetid: bbfbf17b-0c68-4ba6-a25d-07c36ecb551f
ms.openlocfilehash: 3c515381bbd9bb654ef1f41a9ecab1bc138ca946
ms.sourcegitcommit: 6052185696adca270bc9bdbec45a626dd89cdcdd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50531224"
---
# <a name="315-ompgetnumprocs-function"></a>3.1.5 omp_get_num_procs 함수

`omp_get_num_procs` 함수의 함수 호출 시 프로그램에 사용할 수 있는 프로세서의 수를 반환 합니다. 형식은 다음과 같습니다.

```
#include <omp.h>
int omp_get_num_procs(void);
```