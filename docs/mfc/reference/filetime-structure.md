---
title: "FILETIME 구조체 | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: cpp-windows
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: FILETIME
dev_langs: C++
helpviewer_keywords: FILETIME structure [MFC]
ms.assetid: e09557e2-b6d7-4dd5-a5b9-6328bca88595
caps.latest.revision: "11"
author: mikeblome
ms.author: mblome
manager: ghogen
ms.openlocfilehash: 1ecb4814a8bfc0b94bce8e160b973a81bb54cd48
ms.sourcegitcommit: ebec1d449f2bd98aa851667c2bfeb7e27ce657b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/24/2017
---
# <a name="filetime-structure"></a>FILETIME 구조체
`FILETIME` 구조는 1601 년 1 월 1 일 이후 100 나노초 간격의 수를 나타내는 64 비트 값입니다.  
  
## <a name="syntax"></a>구문  
  
```  
typedef struct _FILETIME {  
    DWORD dwLowDateTime;   /* low 32 bits */  
    DWORD dwHighDateTime;  /* high 32 bits */  
} FILETIME, *PFILETIME, *LPFILETIME;  
```  
  
#### <a name="parameters"></a>매개 변수  
 *dwLowDateTime*  
 저점을 파일 시간의 32 비트를 지정합니다.  
  
 *dwHighDateTime*  
 높은 32 비트 파일 시간을 지정합니다.  
  
## <a name="requirements"></a>요구 사항  
 **헤더:** windef.h  
  
## <a name="see-also"></a>참고 항목  
 [구조체, 스타일, 콜백 및 메시지 맵](../../mfc/reference/structures-styles-callbacks-and-message-maps.md)   
 [CTime::CTime](../../atl-mfc-shared/reference/ctime-class.md#ctime)
