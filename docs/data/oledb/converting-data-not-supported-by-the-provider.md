---
title: 공급자가 지원하지 않는 데이터 변환
ms.date: 10/29/2018
helpviewer_keywords:
- OLE DB provider templates, unsupported data types
ms.assetid: f495e50f-530a-4fab-ab54-e0c359785845
ms.openlocfilehash: 44cdde2bad24d21adbc728c90ecd173717c02b04
ms.sourcegitcommit: 943c792fdabf01c98c31465f23949a829eab9aad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2018
ms.locfileid: "51265193"
---
# <a name="converting-data-not-supported-by-the-provider"></a>공급자가 지원하지 않는 데이터 변환

OLE DB 공급자 템플릿에 코드에 대 한 소비자를 요청 하면 공급자가 지원 되지 않는 데이터 형식, `IRowsetImpl::GetData` Msdadc.dll 데이터 형식을 변환을 호출 합니다.

같은 인터페이스를 구현 하는 경우 `IRowsetChange` 데이터 변환을 수행 해야 하는, 변환을 수행 하는 Msdaenum.dll를 호출할 수 있습니다. 사용 하 여 `GetData`예로 Atldb.h에 정의 된 합니다.

## <a name="see-also"></a>참고 항목

[OLE DB 공급자 템플릿을 사용하여 작업](../../data/oledb/working-with-ole-db-provider-templates.md)