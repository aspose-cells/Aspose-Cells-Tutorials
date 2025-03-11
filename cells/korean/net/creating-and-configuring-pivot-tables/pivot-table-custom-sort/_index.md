---
title: .NET에서 피벗 테이블 사용자 정의 정렬 프로그래밍
linktitle: .NET에서 피벗 테이블 사용자 정의 정렬 프로그래밍
second_title: Aspose.Cells .NET Excel 처리 API
description: Aspose.Cells를 사용하여 .NET에서 피벗 테이블을 프로그래밍 방식으로 정렬하는 방법을 알아보세요. 설정, 구성, 정렬 및 결과를 Excel 및 PDF 파일로 저장하는 방법을 다루는 단계별 가이드입니다.
weight: 29
url: /ko/net/creating-and-configuring-pivot-tables/pivot-table-custom-sort/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET에서 피벗 테이블 사용자 정의 정렬 프로그래밍

## 소개
.NET 환경에서 Excel을 사용할 때, 다른 것들 중에서 두드러지는 라이브러리가 하나 있습니다. Aspose.Cells입니다. 이제, 도구로 스프레드시트를 프로그래밍 방식으로 조작할 수 있을 때 정말 좋아지지 않나요? Aspose.Cells가 하는 일이 바로 그것입니다! 오늘의 튜토리얼에서는 피벗 테이블의 세계를 깊이 파고들어 이 다재다능한 라이브러리를 사용하여 사용자 지정 정렬을 프로그래밍 방식으로 구현하는 방법을 보여드리겠습니다.
## 필수 조건
소매를 걷어붙이고 코드로 들어가기 전에 몇 가지가 준비되었는지 확인하세요.
1. Visual Studio: Visual Studio의 작동 버전이 필요합니다. 모든 마법이 일어나는 놀이터입니다.
2. .NET Framework: .NET 프로그래밍에 대한 지식이 필수적입니다. .NET Core나 .NET Framework 애호가이든, 누구나 시작할 수 있습니다.
3.  Aspose.Cells 라이브러리: Aspose.Cells 라이브러리를 설치해야 합니다. 다음에서 얻을 수 있습니다.[다운로드 링크](https://releases.aspose.com/cells/net/) 프로젝트에 추가하세요.
4. 피벗 테이블에 대한 기본적인 이해: 전문가가 될 필요는 없지만, 이 튜토리얼을 진행하면서 피벗 테이블의 작동 방식에 대한 약간의 지식이 있다면 도움이 될 것입니다.
5.  샘플 Excel 파일: 샘플 Excel 파일의 이름을 다음과 같이 지정하세요.`SamplePivotSort.xlsx` 테스트를 위해 작업 디렉토리에 준비되었습니다.
## 패키지 가져오기
모든 필수 구성 요소를 정렬했으면 첫 번째 단계는 필요한 패키지를 가져오는 것입니다. 이를 위해 코드 맨 위에 다음 줄을 포함합니다.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells;
using Aspose.Cells.Pivot;
```
이 패키지는 Aspose.Cells를 사용하여 Excel 파일을 조작하는 데 필요한 모든 기능을 제공합니다.

좋아요, 재밌는 부분으로 들어가보죠! 피벗 테이블을 만들고 사용자 지정 정렬을 적용하는 과정을 관리 가능한 단계로 나누어 설명하겠습니다.
## 1단계: 워크북 설정
시작하려면 워크북을 설정해야 합니다. 방법은 다음과 같습니다.
```csharp
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
Workbook wb = new Workbook(sourceDir + "SamplePivotSort.xlsx");
```
 이 단계에서는 새로운 것을 초기화합니다.`Workbook` 인스턴스는 Excel 파일에 대한 경로와 함께 제공됩니다. 이것은 피벗 테이블이 살아날 캔버스 역할을 합니다.
## 2단계: 워크시트에 액세스
다음으로, 피벗 테이블을 추가할 워크시트에 액세스해야 합니다.
```csharp
Worksheet sheet = wb.Worksheets[0];
PivotTableCollection pivotTables = sheet.PivotTables;
```
 여기서 우리는 워크북의 첫 번째 워크시트를 잡고 호출합니다.`PivotTableCollection`이 컬렉션을 사용하면 이 워크시트의 모든 피벗 테이블을 관리할 수 있습니다.
## 3단계: 첫 번째 피벗 테이블 만들기
이제 피벗 테이블을 만들 차례입니다.
```csharp
int index = pivotTables.Add("=Sheet1!A1:C10", "E3", "PivotTable1");
PivotTable pivotTable = pivotTables[index];
```
워크시트에 새 피벗 테이블을 추가하고 데이터 범위와 위치를 지정합니다. "E3"은 피벗 테이블이 시작되기를 원하는 위치를 나타냅니다. 그런 다음 인덱스를 사용하여 이 새 피벗 테이블을 참조합니다.
## 4단계: 피벗 테이블 설정 구성
피벗 테이블을 구성해 봅시다! 이는 총계와 필드 배열과 같은 측면을 제어하는 것을 의미합니다.
```csharp
pivotTable.RowGrand = false;
pivotTable.ColumnGrand = false;
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
PivotField rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
행과 열의 총계가 표시되지 않도록 하여 데이터를 더 깔끔하게 만들 수 있습니다. 그런 다음 첫 번째 필드를 행 영역에 추가하여 자동 정렬과 오름차순 정렬을 활성화합니다.
## 5단계: 열 및 데이터 필드 추가
행이 설정되면 열과 데이터 필드를 추가해 보겠습니다.
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Column,0);
PivotField colField = pivotTable.ColumnFields[0];
colField.NumberFormat = "dd/mm/yyyy";
colField.IsAutoSort = true;
colField.IsAscendSort = true;
```
두 번째 필드를 열로 추가하고 날짜로 포맷합니다. 다시 자동 정렬 및 오름차순을 활성화하여 정리합니다. 마지막으로 세 번째 필드를 데이터 영역에 추가해야 합니다.
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Data,2);
```
## 6단계: 피벗 테이블 새로 고침 및 계산
모든 필수 필드를 추가한 후 피벗 테이블이 새롭고 준비되었는지 확인해 보겠습니다.
```csharp
pivotTable.RefreshData();
pivotTable.CalculateData();
```
이러한 방법을 사용하면 데이터를 새로 고치고 다시 계산하여 모든 내용이 최신 상태로 유지되고 피벗 테이블에 올바르게 표시됩니다.
## 7단계: 행 필드 값을 기준으로 사용자 정의 정렬
"해산물"과 같은 특정 값을 기준으로 피벗 테이블을 정렬하여 약간의 멋을 더해 보겠습니다.
```csharp
index = pivotTables.Add("=Sheet1!A1:C10", "E10", "PivotTable2");
pivotTable = pivotTables[index];
```
우리는 또 다른 피벗 테이블을 만들고 첫 번째 피벗 테이블과 비슷하게 설정하여 프로세스를 반복합니다. 이제 우리는 그것을 더욱 사용자 정의할 수 있습니다.
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
## 8단계: 추가 정렬 사용자 지정특정 날짜를 기준으로 다른 정렬 방법을 시도해 보겠습니다.
```csharp
// 날짜별 정렬을 위한 또 다른 피벗 테이블 추가
index = pivotTables.Add("=Sheet1!A1:C10", "E18", "PivotTable3");
pivotTable = pivotTables[index];
// 이전 단계와 유사한 행 및 열 설정을 반복합니다.
```
동일한 프로세스를 반복하여 필요에 맞는 정렬 기준을 갖춘 세 번째 피벗 테이블을 만듭니다.
## 9단계: 통합 문서 저장하기이제까지 우리가 쏟은 모든 노고를 저장할 시간입니다!
```csharp
wb.Save(outputDir + "out.xlsx");
PdfSaveOptions options = new PdfSaveOptions();
options.OnePagePerSheet = true;
wb.Save(outputDir + "out.pdf", options);
```
 여기에서 통합 문서를 Excel 파일과 PDF로 저장합니다.`PdfSaveOptions` 더 나은 서식이 가능하여 변환 시 각 시트가 별도의 페이지에 표시됩니다.
## 10단계: 마무리하기 사용자에게 모든 것이 멋지다는 것을 알려주면서 마무리합니다.
```csharp
Console.WriteLine("PivotTableCustomSort executed successfully.");
```
## 결론
이제 Aspose.Cells의 힘을 활용하여 .NET 애플리케이션에서 피벗 테이블을 만들고 사용자 지정하는 방법을 배웠습니다. 초기 설정에서 사용자 지정 정렬까지 각 단계가 결합되어 매끄러운 경험을 제공합니다. 연간 판매 데이터를 제시하거나 재고 통계를 추적해야 하는 경우 이러한 기술이 도움이 될 것입니다!
## 자주 묻는 질문
### 피벗 테이블이란?
피벗 테이블은 Excel의 데이터 처리 도구로, 이를 통해 데이터를 요약하고 분석하여 쉽게 통찰력을 추출할 수 있는 유연한 방법을 제공합니다.
### Aspose.Cells를 어떻게 설치하나요?
 Visual Studio에서 NuGet을 통해 설치하거나 직접 다운로드할 수 있습니다.[다운로드 링크](https://releases.aspose.com/cells/net/).
### Aspose.Cells의 평가판이 있나요?
 네! 무료로 체험해보실 수 있습니다.[무료 체험 링크](https://releases.aspose.com/).
### 피벗 테이블에서 여러 필드를 정렬할 수 있나요?
물론입니다! 요구 사항에 따라 여러 필드를 추가하고 정렬할 수 있습니다.
### Aspose.Cells에 대한 지원은 어디에서 찾을 수 있나요?
 커뮤니티는 매우 활동적이며 포럼에서 질문을 할 수 있습니다.[여기](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
