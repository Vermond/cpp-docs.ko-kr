---
title: "CHtmlEditDoc 클래스 | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: cpp-windows
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- CHtmlEditDoc
- AFXHTML/CHtmlEditDoc
- AFXHTML/CHtmlEditDoc::CHtmlEditDoc
- AFXHTML/CHtmlEditDoc::GetView
- AFXHTML/CHtmlEditDoc::IsModified
- AFXHTML/CHtmlEditDoc::OpenURL
dev_langs: C++
helpviewer_keywords:
- CHtmlEditDoc [MFC], CHtmlEditDoc
- CHtmlEditDoc [MFC], GetView
- CHtmlEditDoc [MFC], IsModified
- CHtmlEditDoc [MFC], OpenURL
ms.assetid: b2cca61f-e5d6-4099-b0d1-46bf85f0bd64
caps.latest.revision: "24"
author: mikeblome
ms.author: mblome
manager: ghogen
ms.workload: cplusplus
ms.openlocfilehash: c1e60c3b175346268b2c6b755786adbd8eb86467
ms.sourcegitcommit: 8fa8fdf0fbb4f57950f1e8f4f9b81b4d39ec7d7a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="chtmleditdoc-class"></a>CHtmlEditDoc 클래스
와 [CHtmlEditView](../../mfc/reference/chtmleditview-class.md), MFC 문서 뷰 아키텍처 컨텍스트 내에서 WebBrowser 편집 플랫폼의 기능을 제공 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
class AFX_NOVTABLE CHtmlEditDoc : public CDocument  
```  
  
## <a name="members"></a>멤버  
  
### <a name="public-constructors"></a>Public 생성자  
  
|이름|설명|  
|----------|-----------------|  
|[CHtmlEditDoc::CHtmlEditDoc](#chtmleditdoc)|`CHtmlEditDoc` 개체를 생성합니다.|  
  
### <a name="public-methods"></a>Public 메서드  
  
|이름|설명|  
|----------|-----------------|  
|[CHtmlEditDoc::GetView](#getview)|검색 된 `CHtmlEditView` 개체는이 문서에 연결 합니다.|  
|[CHtmlEditDoc::IsModified](#ismodified)|관련된 보기 WebBrowser 컨트롤은 사용자가 수정 된 문서에 포함 되는지 여부를 반환 합니다.|  
|[CHtmlEditDoc::OpenURL](#openurl)|URL을 엽니다.|  
  
## <a name="inheritance-hierarchy"></a>상속 계층  
 [CObject](../../mfc/reference/cobject-class.md)  
  
 [CCmdTarget](../../mfc/reference/ccmdtarget-class.md)  
  
 [CDocument](../../mfc/reference/cdocument-class.md)  
  
 `CHtmlEditDoc`  
  
## <a name="requirements"></a>요구 사항  
 **헤더:** afxhtml.h  
  
##  <a name="chtmleditdoc"></a>CHtmlEditDoc::CHtmlEditDoc  
 생성 된 **CHtmlEditDoc** 개체입니다.  
  
```  
CHtmlEditDoc();
```  
  
##  <a name="getview"></a>CHtmlEditDoc::GetView  
 검색 된 [CHtmlEditView](../../mfc/reference/chtmleditview-class.md) 개체는이 문서에 연결 합니다.  
  
```  
virtual CHtmlEditView* GetView() const;  
```  
  
### <a name="return-value"></a>반환 값  
 다음은 문서에 대 한 포인터를 반환 **CHtmlEditView** 개체입니다.  
  
##  <a name="ismodified"></a>CHtmlEditDoc::IsModified  
 관련된 보기 WebBrowser 컨트롤은 사용자가 수정 된 문서에 포함 되는지 여부를 반환 합니다.  
  
```  
virtual BOOL IsModified();
```  
  
##  <a name="openurl"></a>CHtmlEditDoc::OpenURL  
 URL을 엽니다.  
  
```  
virtual BOOL OpenURL(LPCTSTR lpszURL);
```  
  
### <a name="parameters"></a>매개 변수  
 `lpszURL`  
 열려는 URL입니다.  
  
### <a name="return-value"></a>반환 값  
 반환 **TRUE** 성공 **FALSE** 실패 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [HTMLEdit 샘플](../../visual-cpp-samples.md)   
 [계층 구조 차트](../../mfc/hierarchy-chart.md)
