---
title: .NET에서 Excel 파일의 호환성을 프로그래밍 방식으로 지정
linktitle: .NET에서 Excel 파일의 호환성을 프로그래밍 방식으로 지정
second_title: Aspose.Cells .NET Excel 처리 API
description: Aspose.Cells for .NET을 사용하여 데이터 업데이트, 호환성 설정, 셀 서식을 포함하여 Excel 피벗 테이블을 조작하는 방법을 알아보세요.
weight: 23
url: /ko/net/creating-and-configuring-pivot-tables/specifying-compatibility/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET에서 Excel 파일의 호환성을 프로그래밍 방식으로 지정

## 소개

오늘날의 데이터 중심 세계에서 Excel 파일을 프로그래밍 방식으로 관리하고 조작하는 것은 많은 개발자에게 필수가 되었습니다. .NET에서 Excel로 작업하는 경우 Aspose.Cells는 Excel 파일을 쉽게 만들고, 읽고, 수정하고, 저장할 수 있는 강력한 라이브러리입니다. 이 라이브러리의 중요한 기능 중 하나는 Excel 파일의 호환성을 프로그래밍 방식으로 지정할 수 있다는 것입니다. 이 튜토리얼에서는 Excel 파일을 조작하는 방법을 살펴보겠습니다. 특히 Aspose.Cells for .NET을 사용하여 호환성을 관리하는 데 중점을 둡니다. 마지막에는 데이터를 새로 고치고 관리하는 동안 Excel 파일, 특히 피벗 테이블에 대한 호환성을 설정하는 방법을 이해하게 될 것입니다.

## 필수 조건

코딩 단계에 들어가기 전에 다음 사항이 있는지 확인하세요.

1. C#에 대한 기본 지식: C#로 코드를 작성하므로 해당 언어에 익숙하면 튜토리얼을 더 잘 이해하는 데 도움이 됩니다.
2.  .NET 라이브러리용 Aspose.Cells: 여기에서 다운로드할 수 있습니다.[Aspose Cells 릴리스 페이지](https://releases.aspose.com/cells/net/)아직 체험판을 이용하지 않으셨다면, 무료 체험판을 이용해 먼저 기능을 탐색해 보세요.
3. Visual Studio: C# 코드를 효과적으로 작성하고 테스트할 수 있는 IDE입니다.
4.  샘플 Excel 파일: 데모를 위한 피벗 테이블이 포함된 샘플 Excel 파일이 있는지 확인하세요. 예를 들어 다음을 사용합니다.`sample-pivot-table.xlsx`.

이러한 전제 조건을 갖추었으니, 코딩 과정을 시작해 보겠습니다.

## 패키지 가져오기

애플리케이션을 작성하기 전에 Aspose.Cells 라이브러리를 효과적으로 활용하기 위해 코드에 필요한 네임스페이스를 포함해야 합니다. 방법은 다음과 같습니다.

### Aspose.Cells 네임스페이스 가져오기

```csharp
using System.IO;
using System;
using Aspose.Cells;
using Aspose.Cells.Pivot;
using System.Drawing;
```

이 코드 줄은 Aspose.Cells 라이브러리 내의 모든 클래스와 메서드에 액세스할 수 있도록 보장합니다.

이제 모든 것이 명확하고 이해하기 쉽도록 과정을 자세히 살펴보겠습니다.

## 1단계: 디렉토리 설정

먼저, Excel 파일이 있는 디렉토리를 설정하세요. 올바른 파일 경로를 제공하는 것이 중요합니다.

```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "Your Document Directory";
```

 여기서 교체하세요`"Your Document Directory"`Excel 파일에 대한 실제 경로와 함께. 여기에 샘플 피벗 테이블 파일이 있어야 합니다.

## 2단계: 소스 Excel 파일 로드

다음으로, 샘플 피벗 테이블이 포함된 Excel 파일을 로드해야 합니다. 

```csharp
// 샘플 피벗 테이블이 포함된 소스 Excel 파일 로드
Workbook wb = new Workbook(dataDir + "sample-pivot-table.xlsx");
```

 이 단계에서는 인스턴스를 생성합니다.`Workbook` 지정된 Excel 파일을 로드하는 클래스입니다. 

## 3단계: 워크시트에 접근

이제 통합 문서가 로드되었으므로 피벗 테이블 데이터가 포함된 워크시트에 액세스해야 합니다.

```csharp
// 피벗 테이블 데이터가 포함된 첫 번째 워크시트에 액세스합니다.
Worksheet dataSheet = wb.Worksheets[0];
```

여기서 피벗 테이블이 있는 첫 번째 워크시트에 액세스합니다. Excel 구조에 따라 다른 워크시트를 반복하거나 지정할 수도 있습니다.

## 4단계: 셀 데이터 조작

다음으로, 워크시트에서 일부 셀 값을 수정해 보겠습니다. 

### 4.1단계: 셀 A3 수정

먼저, 셀 A3에 접근하여 값을 설정해 보겠습니다.

```csharp
// 셀 A3에 접근하여 데이터를 설정합니다.
Cells cells = dataSheet.Cells;
Cell cell = cells["A3"];
cell.PutValue("FooBar");
```

이 코드 조각은 셀 A3을 값 "FooBar"로 업데이트합니다.

### 4.2단계: 긴 문자열로 셀 B3 수정

이제 Excel의 표준 문자 제한을 초과하는 긴 문자열을 셀 B3에 입력해 보겠습니다.

```csharp
// 셀 B3에 접근하여 데이터를 설정합니다.
string longStr = "Very long text 1. very long text 2.... [continue your long string]";
cell = cells["B3"];
cell.PutValue(longStr);
```

이 코드는 특히 Excel에서 호환성 설정을 사용할 때 데이터 제한에 대한 기대치를 설정하기 때문에 중요합니다.

## 5단계: 셀 B3의 길이 확인

입력한 문자열의 길이를 확인하는 것도 중요합니다.

```csharp
// 셀 B3 문자열의 길이를 출력하세요
Console.WriteLine("Length of original data string: " + cell.StringValue.Length);
```

이는 셀에 얼마나 많은 문자가 저장되어 있는지 확인하기 위한 것입니다.

## 6단계: 다른 셀 값 설정

이제 더 많은 셀에 접근하여 일부 값을 설정해 보겠습니다.

```csharp
// 셀 C3에 접근하여 데이터를 설정합니다.
cell = cells["C3"];
cell.PutValue("closed");

// 셀 D3에 접근하여 데이터를 설정합니다.
cell = cells["D3"];
cell.PutValue("2016/07/21");
```

이러한 각 조각은 워크시트 내의 여러 개의 추가 셀을 업데이트합니다.

## 7단계: 피벗 테이블에 액세스

다음으로, 피벗 테이블 데이터로 구성된 두 번째 워크시트에 액세스합니다.

```csharp
//피벗 테이블이 포함된 두 번째 워크시트에 액세스합니다.
Worksheet pivotSheet = wb.Worksheets[1];

// 피벗 테이블에 접근하기
PivotTable pivotTable = pivotSheet.PivotTables[0];
```

이 스니펫을 사용하면 피벗 테이블의 호환성 설정을 조작할 수 있습니다.

## 8단계: Excel 2003에 대한 호환성 설정

피벗 테이블이 Excel 2003과 호환되는지 여부를 설정하는 것이 중요합니다. 

```csharp
// IsExcel2003Compatible 속성은 PivotTable을 새로 고칠 때 PivotTable이 Excel2003과 호환되는지 알려줍니다.
pivotTable.IsExcel2003Compatible = true;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

 여기서 실제 변형이 시작됩니다. 설정하여`IsExcel2003Compatible` 에게`true`새로 고침할 때 문자 길이를 255자로 제한합니다.

## 9단계: 호환성 설정 후 길이 확인

호환성을 설정한 후, 데이터에 어떤 영향을 미치는지 살펴보겠습니다.

```csharp
// 피벗 시트의 셀 B5 값을 확인하세요.
Cell b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to True: " + b5.StringValue.Length);
```

초기 데이터가 255자를 초과하면 잘림 효과를 확인하는 출력이 표시될 가능성이 높습니다.

## 10단계: 호환성 설정 변경

이제 호환성 설정을 변경하여 다시 확인해 보겠습니다.

```csharp
//이제 IsExcel2003Compatible 속성을 false로 설정하고 다시 새로 고칩니다.
pivotTable.IsExcel2003Compatible = false;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

이를 통해 데이터는 이전 제한 없이 원래 길이를 반영할 수 있습니다.

## 11단계: 길이 다시 확인 

이제 데이터가 실제 길이를 정확하게 반영하는지 확인해 보겠습니다.

```csharp
// 이제 셀 데이터의 원래 길이를 인쇄합니다. 데이터는 지금 잘리지 않았습니다.
b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to False: " + b5.StringValue.Length);
```

출력에서 잘림이 제거되었음을 확인해야 합니다.

## 12단계: 셀 서식 지정

시각적 경험을 향상시키려면 셀 서식을 지정하는 것이 좋습니다. 

```csharp
// 셀 B5의 행 높이와 열 너비를 설정하고 텍스트 줄바꿈도 설정합니다.
pivotSheet.Cells.SetRowHeight(b5.Row, 100);
pivotSheet.Cells.SetColumnWidth(b5.Column, 65);
Style st = b5.GetStyle();
st.IsTextWrapped = true;
b5.SetStyle(st);
```

이러한 코드 줄은 셀 크기를 조정하고 텍스트 줄바꿈을 활성화하여 데이터를 읽기 쉽게 만듭니다.

## 13단계: 통합 문서 저장

마지막으로, 변경한 내용을 적용하여 통합 문서를 저장합니다.

```csharp
// xlsx 형식으로 통합 문서 저장
wb.Save(dataDir + "SpecifyCompatibility_out.xlsx", SaveFormat.Xlsx);
```

 Excel 파일을 저장할 때 적절한 파일 형식을 선택하는 것이 중요합니다.`Xlsx`이 형식은 널리 사용되고 있으며 다양한 Excel 버전과 호환됩니다.

## 결론

축하합니다! 이제 Aspose.Cells for .NET을 사용하여 Excel 파일 호환성 설정을 프로그래밍했습니다. 이 튜토리얼에서는 환경 설정부터 피벗 테이블의 호환성 설정 변경까지 각 단계를 설명했습니다. 특정 제한이나 호환성이 필요한 데이터로 작업한 적이 있다면 이 기술을 간과하고 싶지 않을 것입니다.

## 자주 묻는 질문

### Aspose.Cells란 무엇인가요?  
Aspose.Cells는 개발자가 Excel 파일을 원활하게 만들고, 조작하고, 변환할 수 있도록 설계된 .NET 라이브러리입니다.

### Excel 호환성이 중요한 이유는 무엇입니까?  
Excel 호환성은 파일을 의도한 Excel 버전에서 열고 사용할 수 있도록 하는 데 필수적입니다. 특히 이전 버전에서 지원되지 않는 기능이나 형식이 포함된 경우 더욱 그렇습니다.

### Aspose.Cells를 사용하여 프로그래밍 방식으로 피벗 테이블을 만들 수 있나요?  
네, Aspose.Cells를 사용하여 피벗 테이블을 프로그래밍 방식으로 만들고 조작할 수 있습니다. 라이브러리는 피벗 테이블과 관련된 데이터 소스, 필드 및 기능을 추가하는 다양한 방법을 제공합니다.

### Excel 셀에 있는 문자열의 길이를 확인하려면 어떻게 해야 하나요?  
당신은 사용할 수 있습니다`StringValue` 의 속성`Cell` 셀의 내용을 가져온 다음 호출하는 객체`.Length` 문자열의 길이를 알아내는 속성입니다.

### 행 높이와 너비 외에 셀 서식을 사용자 정의할 수 있나요?  
 물론입니다! Aspose.Cells는 광범위한 셀 서식을 허용합니다. 글꼴 스타일, 색상, 테두리, 숫자 서식 등을 다음을 통해 변경할 수 있습니다.`Style` 수업.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
