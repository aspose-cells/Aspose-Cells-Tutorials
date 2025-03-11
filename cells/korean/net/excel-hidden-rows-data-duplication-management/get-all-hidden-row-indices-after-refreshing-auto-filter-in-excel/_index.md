---
title: Excel에서 자동 필터를 새로 고친 후 숨겨진 행 인덱스 가져오기
linktitle: Excel에서 자동 필터를 새로 고친 후 숨겨진 행 인덱스 가져오기
second_title: Aspose.Cells .NET Excel 처리 API
description: Aspose.Cells for .NET을 사용하여 Excel에서 자동 필터를 새로 고친 후 숨겨진 행 인덱스를 검색하는 방법을 알아보세요. 데이터 관리를 간소화하세요.
weight: 10
url: /ko/net/excel-hidden-rows-data-duplication-management/get-all-hidden-row-indices-after-refreshing-auto-filter-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel에서 자동 필터를 새로 고친 후 숨겨진 행 인덱스 가져오기

## 소개

Excel 파일, 특히 대규모 데이터 세트로 작업할 때 필터링은 생명의 은인이 될 수 있습니다. 필터링은 특정 데이터 포인트에 집중하는 데 도움이 되지만 필터를 적용한 후 숨겨진 행을 식별하려고 할 때는 어떻게 해야 할까요? 이러한 숨겨진 세부 정보를 끌어내는 것에 대해 궁금해 했다면 올바른 위치에 있습니다! 이 가이드에서는 Aspose.Cells for .NET을 사용하여 Excel에서 자동 필터를 새로 고친 후 숨겨진 행 인덱스를 가져오는 방법을 살펴보겠습니다. 노련한 프로그래머이든 초보자이든 이 프로세스는 간단하고 매력적이라는 것을 알게 될 것입니다. 시작해 볼까요!

## 필수 조건

코드를 살펴보기 전에 염두에 두어야 할 몇 가지 전제 조건이 있습니다.

### .NET용 Aspose.Cells 이해

이 튜토리얼을 따라가려면 Aspose.Cells가 무엇인지 확실히 이해해야 합니다. 기본적으로, 그것은 Microsoft Excel을 설치하지 않고도 Excel 파일을 만들고, 조작하고, 변환할 수 있는 .NET용 강력한 라이브러리입니다. 그것은 간단한 데이터 입력에서 복잡한 데이터 분석까지 모든 것을 매끄럽게 처리할 수 있는 도구입니다.

### 개발 환경 설정

1.  Visual Studio 설치: 컴퓨터에 Visual Studio가 설치되어 있는지 확인하세요. 다음에서 다운로드할 수 있습니다.[Visual Studio 웹사이트](https://visualstudio.microsoft.com/).

2. .NET Framework: 호환되는 버전의 .NET Framework 또는 .NET Core가 필요합니다. 이 라이브러리는 두 프레임워크 모두에서 잘 작동합니다.

3.  Aspose.Cells 라이브러리: Aspose.Cells 라이브러리를 다운로드하여 설치하세요.[이 링크](https://releases.aspose.com/cells/net/). 또는 NuGet을 통해 설치할 수 있습니다. 패키지 관리자 콘솔을 열고 다음을 실행하기만 하면 됩니다.
```
Install-Package Aspose.Cells
```

4.  샘플 Excel 파일: 이름이 지정된 샘플 Excel 파일을 준비하세요.`sampleGetAllHiddenRowsIndicesAfterRefreshingAutoFilter.xlsx` 테스트를 위해. 필터링할 수 있는 데이터를 포함해야 합니다.

## 패키지 가져오기

이 프로그래밍 여정을 시작하려면 필요한 네임스페이스를 가져와야 합니다. 이는 프로젝트에서 Aspose.Cells 기능을 사용할 수 있게 해주므로 중요한 단계입니다.

1. Visual Studio에서 프로젝트를 엽니다.
2. 코드 파일의 맨 위에 다음 using 지침을 추가합니다.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

이러한 지시어는 컴파일러에게 사용하려는 클래스와 메서드를 어디에서 찾아야 하는지 알려줍니다.

이 섹션에서는 프로세스를 쉽게 따를 수 있는 단계로 나누어 설명합니다. Excel 워크시트에 액세스하고, 필터를 적용하고, 숨겨진 행을 식별합니다. 모두 Aspose.Cells를 사용합니다.

## 1단계: 환경 설정

코딩에 들어가기 전에 환경을 설정하고 필요한 변수를 선언해 보겠습니다. 이 설정은 모든 것을 샘플 Excel 파일로 보내고 통합 문서를 준비합니다.

```csharp
string sourceDir = "Your Document Directory"; // 디렉토리를 지정하세요
```

## 2단계: 샘플 Excel 파일 로드

다음으로, Excel 파일을 통합 문서 개체에 로드해야 합니다. 이를 통해 프로그래밍 방식으로 조작할 수 있습니다. 

```csharp
Workbook wb = new Workbook(sourceDir + "sampleGetAllHiddenRowsIndicesAfterRefreshingAutoFilter.xlsx");
```

 여기서 우리는 새로운 것을 만들고 있습니다`Workbook` 지정된 Excel 파일을 로드하는 개체입니다.

## 3단계: 원하는 워크시트에 액세스

이제 워크북의 첫 번째 워크시트로 작업할 것입니다. 이 단계는 필터링하려는 데이터가 포함된 시트를 분리합니다.

```csharp
Worksheet ws = wb.Worksheets[0]; // 첫 번째 워크시트에 접근하기
```

## 4단계: 자동 필터 적용

자동 필터를 적용하는 것이 마법의 시작입니다! 필터링할 열을 지정하고 기준을 설정합니다. 여기서는 "Orange"를 필터링합니다. 

```csharp
ws.AutoFilter.AddFilter(0, "Orange"); // 첫 번째 열에 자동 필터 적용
```

## 5단계: 자동 필터 새로 고침 및 숨겨진 행 가져오기

다음 줄은 자동 필터를 새로 고칩니다. 필터를 적용한 후 숨겨진 행의 인덱스를 반환합니다. 매개변수를 true로 설정하면 필터가 효과적으로 새로 고침됩니다.

```csharp
int[] rowIndices = ws.AutoFilter.Refresh(true);
```

## 6단계: 숨겨진 행 인덱스 인쇄

이제 숨겨진 행 인덱스가 있으니 콘솔에 출력해 보겠습니다. 그러면 자동 필터로 인해 무엇이 숨겨졌는지 명확하게 알 수 있습니다.

```csharp
Console.WriteLine("Printing Rows Indices, Cell Names and Values Hidden By AutoFilter.");
Console.WriteLine("--------------------------");

for (int i = 0; i < rowIndices.Length; i++)
{
    int r = rowIndices[i];
    Cell cell = ws.Cells[r, 0];
    Console.WriteLine(r + "\t" + cell.Name + "\t" + cell.StringValue);
}

Console.WriteLine("GetAllHiddenRowsIndicesAfterRefreshingAutoFilter executed successfully.");
```

## 결론

이제 다 됐습니다! Aspose.Cells for .NET을 사용하여 Excel에서 자동 필터를 새로 고친 후 숨겨진 행의 인덱스를 성공적으로 가져왔습니다. 꽤 깔끔하죠? 이 기능은 데이터 분석 프로젝트를 극적으로 향상시켜 워크플로를 더 매끄럽고 효율적으로 만들어줍니다.

## 자주 묻는 질문

### Aspose.Cells란 무엇인가요?
Aspose.Cells는 개발자가 Microsoft Excel이 없어도 Excel 파일을 만들고, 조작하고, 내보낼 수 있는 강력한 .NET용 라이브러리입니다.

### Aspose.Cells를 사용하여 Excel에서 데이터를 필터링할 수 있나요?
네! Aspose.Cells에는 필터를 적용하고 Excel 데이터를 효과적으로 작업할 수 있는 내장 기능이 있습니다.

### Aspose.Cells는 무료로 사용할 수 있나요?
 Aspose.Cells는 무료 체험판을 제공하지만 계속 사용하려면 라이선스를 구매해야 합니다.[구매 페이지](https://purchase.aspose.com/buy) 자세한 내용은.

### Aspose.Cells에 대한 지원은 어떻게 받을 수 있나요?
 Aspose 커뮤니티를 통해 지원을 요청할 수 있습니다.[Aspose 포럼](https://forum.aspose.com/c/cells/9).

### Aspose.Cells에 대한 설명서는 어디서 찾을 수 있나요?
 전체 문서를 사용할 수 있습니다[여기](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
