---
title: db_command (c + + COM 특성) | Microsoft Docs
ms.custom: ''
ms.date: 07/10/2018
ms.technology:
- cpp-windows
ms.topic: reference
f1_keywords:
- vc-attr.db_command
dev_langs:
- C++
helpviewer_keywords:
- db_command attribute
ms.assetid: 714c3e15-85d7-408b-9a7c-88505c3e5d24
author: mikeblome
ms.author: mblome
ms.workload:
- cplusplus
- uwp
ms.openlocfilehash: 0111dfc424a99d413a217149b3c5e579a3999f13
ms.sourcegitcommit: 955ef0f9d966e7c9c65e040f1e28fa83abe102a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48791416"
---
# <a name="dbcommand"></a>db_command

OLE DB 명령을 만듭니다.

## <a name="syntax"></a>구문

```cpp
[ db_command(command, name, source_name, hresult, bindings, bulk_fetch)  
]
```

### <a name="parameters"></a>매개 변수

*command*<br/>
OLE DB 명령의 텍스트를 포함하는 명령 문자열입니다. 다음은 간단한 예제입니다.

```cpp
[ db_command ( command = "Select * from Products" ) ]
```

*command* 구문은 다음과 같습니다.

> 바인딩 매개 변수 블록 1 &nbsp; &nbsp;OLE DB 명령 바인딩 매개 변수 블록 2 &nbsp; &nbsp;OLE DB 명령 바인딩 매개 변수 블록 3의 연속 하는 중...

*binding parameter block* 은 다음과 같이 정의됩니다.

> **(\[**  *bindtype* **]** *szVar1* \[하십시오 *szVar2* \[합니다 *nVar3* \[,...]]] **)**

다음은 각 문자에 대한 설명입니다.

- **(** 는 데이터 바인딩 블록의 시작을 표시합니다.

- **\[** *bindtype* **]** 대/소문자 문자열 중 하나입니다.

  - **\[db_column]** 행 집합의 열에 각 멤버 변수를 바인딩합니다.

  - **\[bindto]** (동일  **\[db_column]**).

  - **\[in]** -멤버 변수를 입력된 매개 변수로 바인딩합니다.

  - **\[out]** -멤버 변수를 output 매개 변수로 바인딩합니다.

  - **\[in, out]** -멤버 변수를 입/출력 매개 변수로 바인딩합니다.

- *szVarX*하십시오 *nVarX* 현재 범위 내에서 멤버 변수를 확인 합니다.

- **)** 는 데이터 바인딩 블록의 끝을 표시합니다.

명령 문자열 같은 하나 이상의 지정 자가 포함 된 경우 \[에서]를 \[out], 또는 \[입/출력], **db_command** 매개 변수 맵을 작성 합니다.

명령 문자열 같은 하나 이상의 매개 변수를 포함 하는 경우 \[db_column] 또는 \[bindto], **db_command** 행 집합 및 이러한 바인딩된 변수를 서비스 하기 위해 접근자 맵을 생성 합니다. 참조 [db_accessor](db-accessor.md) 자세한 내용은 합니다.

> [!NOTE]
> \[*bindtype*] 구문 및 *바인딩을* 사용 하는 경우 매개 변수가 올바르지 않습니다 **db_command** 클래스 수준입니다.

바인딩 매개 변수 블록의 몇 가지 예는 다음과 같습니다. 다음 예제는 `m_au_fname` 및 `m_au_lname` 데이터 멤버를 각각 pubs 데이터베이스에 있는 authors 테이블의 `au_fname` 및 `au_lname` 열에 바인딩합니다.

```cpp
TCHAR m_au_fname[21];
TCHAR m_au_lname[41];
TCHAR m_state[3] = 'CA';

[db_command (command = "SELECT au_fname([bindto]m_au_fname), au_lname([bindto]m_au_lname) " \
   "FROM dbo.authors " \
   "WHERE state = ?([in]m_state)")  
]
```

*name*<br/>
(선택 사항) 행 집합을 사용 하는 데 핸들의 이름입니다. *name*을 지정하는 경우, **db_command** 는 지정된 *name*의 클래스를 생성하며, 이 클래스는 행 집합을 이동하거나 여러 작업 쿼리를 실행하는 데 사용할 수 있습니다. *name*을 지정하지 않으면 사용자에게 둘 이상의 결과 행을 반환할 수 없습니다.

*source_name*<br/>
(선택 사항) 합니다 `CSession` 변수나 있는 클래스의 인스턴스는 `db_source` 명령을 실행 하는 것에 적용 된 특성입니다. 참조 [db_source](db-source.md)합니다.

**db_command** 는 지정된 변수가 함수 또는 전역 범위에 있도록, *source_name* 에 사용된 변수가 유효한지 확인합니다.

*hresult*<br/>
(선택 사항) 이 데이터베이스 명령의 HRESULT 받을 변수를 식별 합니다. 변수가 없으면 특성에 의해 자동으로 삽입됩니다.

*바인딩*<br/>
(선택 사항) OLE DB 명령에서 바인딩 매개 변수를 구분할 수 있습니다.

에 대 한 값을 지정 하는 경우 *바인딩을*를 **db_command** 는 연결된 된 값을 구문 분석 하 고 구문 분석 하지 것입니다는 \[ *bindtype*] 매개 변수입니다. 이 방법에서는 OLE DB 공급자 구문을 사용할 수 있습니다. 바인딩 매개 변수 없이 구문 분석을 사용 하지 않도록 설정 하려면 지정 `Bindings=""`합니다.

에 대 한 값을 지정 하지 않으면 *바인딩을*를 **db_command** 찾고자 하는 바인딩 매개 변수 블록을 구문 분석 됩니다 '**(**' 뒤 **\[** _bindtype_**]** 뒤에 하나 이상의 이전에 선언 된 c + + 멤버 변수를 대괄호로 뒤에 '**)**'. 괄호 안의 모든 텍스트는 결과 명령에서 제거되며, 이 명령에 대한 열 및 매개 변수 바인딩을 구성하는 데 이러한 매개 변수가 사용됩니다.

*bulk_fetch*<br/>
(선택 사항) 인출할 행 수를 지정 하는 정수 값입니다.

기본값은 단일 행 페치를 지정 하는 1 (행 집합 형식일 [CRowset](../../data/oledb/crowset-class.md)).

1보다 큰 값은 대량 행 페치를 지정합니다. 대량 행 페치는 여러 행 핸들을 가져오는 대량 행 집합의 기능을 말합니다 (행 집합 형식일 [CBulkRowset](../../data/oledb/cbulkrowset-class.md) 호출 및 `SetRows` 지정 된 행 수를 사용 하 여).

*bulk_fetch* 가 1 미만인 경우 `SetRows` 는 0을 반환합니다.

## <a name="remarks"></a>설명

**db_command** 만듭니다는 [CCommand](../../data/oledb/ccommand-class.md) 명령을 실행 하는 OLE DB 소비자에서 사용 되는 개체입니다.

**db_command** 는 클래스 또는 함수 범위와 함께 사용할 수 있습니다. 주요 차이점은 `CCommand` 개체의 범위입니다. 함수 범위를 사용하는 경우 바인딩 같은 데이터는 함수 끝에서 종료됩니다. OLE DB 소비자 템플릿 클래스를 포함 하는 클래스 및 함수 범위 사용 `CCommand<>`, 함수 및 클래스 사례에 대 한 템플릿 인수 다릅니다. 함수의 경우 바인딩을 적용 될를 `Accessor` 유추 클래스를 사용 하는 동안 로컬 변수를 포함 하는 `CAccessor`-인수로 클래스를 파생 합니다. 클래스 특성으로 사용하는 경우 **db_command** 는 **db_column**과 함께 작동합니다.

**db_command** 는 결과 집합을 반환하지 않는 명령을 실행하는 데 사용할 수 있습니다.

컴파일러는 클래스 이름을 소비자 특성 공급자가이 특성 클래스에 적용 될 때 \_ *YourClassName*접근자를 여기서 *YourClassName* 제공한 이름인는 클래스 및 컴파일러 라는 클래스를 만들 수도 됩니다 *YourClassName*에서 파생 되는 \_ *YourClassName*접근자입니다.  클래스 뷰에 두 클래스 모두 표시됩니다.

## <a name="example"></a>예제

이 샘플에서는 상태 열이 'CA'와 일치하는 테이블에서 성과 이름을 선택하는 명령을 정의합니다. **db_command** 같은 마법사에서 생성 한 함수 호출 수 하는 행 집합을 읽고 만듭니다 [OpenAll 및 CloseAll](../../data/oledb/consumer-wizard-generated-methods.md), 뿐만 `CRowset` 멤버 함수 [MoveNext](../../data/oledb/crowset-movenext.md)합니다.

이 코드를 사용하려면 pubs 데이터베이스에 연결되는 고유한 연결 문자열을 제공해야 합니다. 개발 환경에서이 작업을 수행 하는 방법에 대 한 자세한 내용은 [방법: 데이터베이스 및 기존 개체 찾아보기 연결할](/sql/ssdt/how-to-connect-to-a-database-and-browse-existing-objects) 및 [새 연결 추가](/visualstudio/data-tools/add-new-connections)합니다.

```cpp
// db_command.h
#include <atlbase.h>
#include <atlplus.h>
#include <atldbcli.h>

#pragma once

[  db_source(L"your connection string"), db_command(L" \
      SELECT au_lname, au_fname \
      FROM dbo.authors \
      WHERE state = 'CA'")  ]

struct CAuthors {
   // In order to fix several issues with some providers, the code below may bind
   // columns in a different order than reported by the provider

   DBSTATUS m_dwau_lnameStatus;
   DBSTATUS m_dwau_fnameStatus;
   DBLENGTH m_dwau_lnameLength;
   DBLENGTH m_dwau_fnameLength;

   [ db_column("au_lname", status="m_dwau_lnameStatus", length="m_dwau_lnameLength") ] TCHAR m_au_lname[41];
   [ db_column("au_fname", status="m_dwau_fnameStatus", length="m_dwau_fnameLength") ] TCHAR m_au_fname[21];

   [ db_param("7", paramtype="DBPARAMIO_INPUT") ] TCHAR m_state[3];

   void GetRowsetProperties(CDBPropSet* pPropSet) {
      pPropSet->AddProperty(DBPROP_CANFETCHBACKWARDS, true, DBPROPOPTIONS_OPTIONAL);
      pPropSet->AddProperty(DBPROP_CANSCROLLBACKWARDS, true, DBPROPOPTIONS_OPTIONAL);
   }
};
```

## <a name="example"></a>예제

```cpp
// db_command.cpp
// compile with: /c
#include "db_command.h"

int main(int argc, _TCHAR* argv[]) {
   HRESULT hr = CoInitialize(NULL);

   // Instantiate rowset
   CAuthors rs;

   // Open rowset and move to first row
   strcpy_s(rs.m_state, sizeof(rs.m_state), _T("CA"));
   hr = rs.OpenAll();
   hr = rs.MoveFirst();

   // Iterate through the rowset
   while( SUCCEEDED(hr) && hr != DB_S_ENDOFROWSET ) {
      // Print out the column information for each row
      printf("First Name: %s, Last Name: %s\n", rs.m_au_fname, rs.m_au_lname);
      hr = rs.MoveNext();
   }

   rs.CloseAll();
   CoUninitialize();
}
```

## <a name="example"></a>예제

이 샘플에서는 데이터 소스 클래스 `db_source` 의 `CMySource`, 명령 클래스 `db_command` 및 `CCommand1` 의 `CCommand2`를 사용합니다.

```cpp
// db_command_2.cpp
// compile with: /c
#include <atlbase.h>
#include <atlplus.h>
#include <atldbcli.h>
// class usage for both db_source and db_command

[  db_source(L"your connection string"), db_command(L" \
      SELECT au_lname, au_fname \
      FROM dbo.authors \
      WHERE state = 'CA'")  ]
struct CMySource {
   HRESULT OpenDataSource() {
      return S_OK;
   }
};

[db_command(command = "SELECT * FROM Products")]
class CCommand1 {};

[db_command(command = "SELECT FNAME, LNAME FROM Customers")]
class CCommand2 {};

int main() {
   CMySource s;
   HRESULT hr = s.OpenDataSource();
   if (SUCCEEDED(hr)) {
      CCommand1 c1;
      hr = c1.Open(s);

      CCommand2 c2;
      hr = c2.Open(s);
   }

   s.CloseDataSource();
}
```

## <a name="requirements"></a>요구 사항

### <a name="attribute-context"></a>특성 컨텍스트

|||
|-|-|
|**적용 대상**|**클래스**하십시오 **구조체**, 멤버, 메서드, 로컬|
|**반복 가능**|아니요|
|**필수 특성**|없음|
|**잘못된 특성**|없음|

특성 컨텍스트에 대 한 자세한 내용은 참조 하세요. [특성 컨텍스트](cpp-attributes-com-net.md#contexts)합니다.

## <a name="see-also"></a>참고자료

[OLE DB 소비자 특성](ole-db-consumer-attributes.md)<br/>
[독립 실행형 특성](stand-alone-attributes.md)  