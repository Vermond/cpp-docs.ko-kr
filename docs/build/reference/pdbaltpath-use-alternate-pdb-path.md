---
title: /PDBALTPATH(대체 PDB 경로 사용)
ms.date: 11/04/2016
f1_keywords:
- /pdbaltpath
helpviewer_keywords:
- .pdb files, path
- PDBALTPATH dumpbin option
- -PDBALTPATH dumpbin option
- /PDBALTPATH dumpbin option
- PDB files, path
ms.assetid: 72e200aa-e2c3-4ad8-b687-25528da1aaaf
ms.openlocfilehash: dd7bdc8d161e92eedf4856fcd28d9f9f1ac781b8
ms.sourcegitcommit: 6052185696adca270bc9bdbec45a626dd89cdcdd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50551101"
---
# <a name="pdbaltpath-use-alternate-pdb-path"></a>/PDBALTPATH(대체 PDB 경로 사용)

```
/PDBALTPATH:pdb_file_name
```

## <a name="arguments"></a>인수

*pdb_file_name*<br/>
.pdb 파일의 경로 및 파일 이름입니다.

## <a name="remarks"></a>설명

이 옵션은 컴파일된 이진 파일에서 프로그램 데이터베이스(.pdb) 파일의 대체 위치를 제공하는 데 사용합니다. 일반적으로 링커는 자신이 생성한 이진 파일에 .pdb 파일의 위치를 기록합니다. 이 옵션을 사용하여 .pdb 파일의 다른 경로 및 파일 이름을 제공할 수 있습니다. /PDBALTPATH와 함께 제공되는 정보는 실제 .pdb 파일의 위치 또는 이름을 변경하지 않고 링커가 이진 파일에 쓴 정보를 변경합니다. 따라서 빌드 컴퓨터의 파일 구조와 독립적인 경로를 제공할 수 있습니다. 이 옵션은 일반적으로 네트워크 경로 또는 경로 정보가 없는 파일을 제공하는 두 가지 용도로 사용됩니다.

변수의 *pdb_file_name* 임의 문자열, 환경 변수 또는 **_PDB %** 합니다. 링커는 환경 변수를 같은 확장 **% SystemRoot %**, 해당 값입니다. 환경 변수를 정의 하는 링커 **% _PDB** 하 고 **_EXT %** 합니다. **% _PDB** 경로 정보가 없는 실제.pdb 파일의 파일 이름으로 확장 하 고 **_EXT %** 는 생성된 된 실행 파일의 확장명입니다.

## <a name="see-also"></a>참고 항목

[DUMPBIN 옵션](../../build/reference/dumpbin-options.md)<br/>
[/PDBPATH](../../build/reference/pdbpath.md)