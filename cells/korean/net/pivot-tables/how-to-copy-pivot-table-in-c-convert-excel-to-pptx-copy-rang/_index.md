---
category: general
date: 2026-01-14
description: Aspose.Cells를 사용해 피벗 테이블을 복사하는 방법과 Excel을 PPTX로 변환하고, 범위를 다른 워크북에 복사하며,
  텍스트 상자를 편집 가능한 PPTX로 만드는 방법을 하나의 튜토리얼에서 배워보세요.
draft: false
keywords:
- how to copy pivot table
- convert excel to pptx
- copy range to another workbook
- make textbox editable pptx
- save workbook as pptx
language: ko
og_description: 피벗 테이블을 복사하고 Excel을 PPTX로 변환하며, 범위를 다른 워크북으로 복사하고, 텍스트 상자를 편집 가능한
  PPTX로 만드는 방법—모두 Aspose.Cells로.
og_title: C#에서 피벗 테이블 복사 방법 – Excel에서 PPTX까지 완전 가이드
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: C#에서 피벗 테이블 복사하기 – Excel을 PPTX로 변환, 범위 복사 및 텍스트 상자 편집 가능하게 만들기
url: /ko/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 피벗 테이블 복사하기 – 완전한 Excel → PPTX 가이드

피벗 테이블을 한 워크북에서 다른 워크북으로 복사하는 방법은 Excel 기반 보고서를 자동화할 때 자주 묻는 질문입니다. 이번 튜토리얼에서는 **Aspose.Cells for .NET**을 사용한 세 가지 실제 시나리오를 살펴봅니다: 피벗 테이블 범위 복사, 워크시트를 PPTX 파일로 내보내면서 편집 가능한 텍스트 상자 만들기, Smart Markers를 이용해 JSON 배열을 단일 셀에 채우기.  

또한 **Excel을 PPTX로 변환**, **범위를 다른 워크북에 복사**, **텍스트 상자를 편집 가능한 PPTX로 만들기**를 포맷을 깨뜨리지 않고 수행하는 방법을 보여드립니다. 마지막에는 .NET 프로젝트에 바로 넣어 실행할 수 있는 완전한 코드 베이스를 제공합니다.

> **Pro tip:** 모든 예제는 Aspose.Cells 23.12를 대상으로 하지만, 이전 버전에서도 API만 약간 수정하면 동일하게 적용됩니다.

![피벗 테이블이 복사되고, 워크시트가 PPTX로 내보내지며, JSON 배열이 삽입되는 흐름을 보여주는 다이어그램 – 피벗 테이블 복사 워크플로우](how-to-copy-pivot-table-diagram.png)

---

## 필요 사항

- Visual Studio 2022 (또는 기타 C# IDE)
- .NET 6.0 이상 런타임
- Aspose.Cells for .NET NuGet 패키지  
  ```bash
  dotnet add package Aspose.Cells
  ```
- 두 개의 샘플 Excel 파일(`source.xlsx`, `chartWithTextbox.xlsx`)을 직접 관리하는 폴더에 배치 (`YOUR_DIRECTORY`를 실제 경로로 교체).

추가 라이브러리는 필요하지 않으며, `Aspose.Cells` 어셈블리 하나로 Excel, PPTX, Smart Markers를 모두 처리합니다.

---

## 피벗 테이블 복사 및 데이터 보존 방법

피벗 테이블이 포함된 범위를 복사하면 기본 동작으로 **값만** 붙여넣어집니다. 피벗 정의를 그대로 유지하려면 `CopyPivotTable` 플래그를 활성화해야 합니다.

### 단계별 안내

1. **피벗 테이블이 들어 있는 소스 워크북을 로드**합니다.  
2. **빈 대상 워크북을 생성**합니다 – 복사된 범위가 여기로 들어갑니다.  
3. **`CopyRange`에 `CopyPivotTable = true`** 옵션을 지정해 피벗 정의가 데이터와 함께 이동하도록 합니다.  
4. **대상 파일을 원하는 위치에 저장**합니다.

#### 전체 코드 예시

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Step 1: Load the source workbook and define the range to copy
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        // Assuming the pivot table lives inside A1:G20
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // Step 2: Create a destination workbook (blank)
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

        // Step 3: Copy the range, preserving the pivot table
        destinationSheet.Cells.CopyRange(
            sourceRange,
            "B2", // paste start cell
            new CopyOptions { CopyPivotTable = true });

        // Step 4: Save the result
        destinationWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");
    }
}
```

**동작 원리:**  
`CopyOptions.CopyPivotTable`은 Aspose.Cells에게 렌더링된 값이 아니라 기본 `PivotTable` 객체 자체를 복제하도록 지시합니다. 이제 대상 워크북에는 프로그램matically 새로 고치거나 수정할 수 있는 완전한 피벗 테이블이 포함됩니다.

**예외 상황:** 소스 워크북이 외부 데이터 소스를 사용한다면, 복사 후 데이터 삽입 또는 연결 문자열을 조정해야 합니다. 그렇지 않으면 피벗이 “#REF!” 오류를 표시합니다.

---

## Excel을 PPTX로 변환하고 텍스트 상자를 편집 가능하게 만들기

워크시트를 PowerPoint로 내보내면 슬라이드 덱을 직접 데이터에서 생성할 수 있어 편리합니다. 기본적으로 내보낸 텍스트 상자는 정적 도형이지만, `IsTextBoxEditable`을 설정하면 편집 가능한 텍스트 상자로 바뀝니다.

### 단계별 안내

1. **차트와 텍스트 상자가 포함된 워크북을 엽니다.**  
2. **`ImageOrPrintOptions`에 `SaveFormat = SaveFormat.Pptx`**를 지정해 PPTX 형식으로 저장하도록 설정합니다.  
3. **텍스트 상자를 포함하는 인쇄 영역을 정의**합니다.  
4. **`IsTextBoxEditable`을 활성화**해 PPTX를 연 뒤 텍스트를 수정할 수 있게 합니다.  
5. **PPTX 파일을 저장**합니다.

#### 전체 코드 예시

```csharp
using Aspose.Cells;

class ExcelToPptxDemo
{
    static void Main()
    {
        // Step 1: Load the workbook with chart and textbox
        Workbook chartWorkbook = new Workbook(@"YOUR_DIRECTORY\chartWithTextbox.xlsx");

        // Step 2: Set export options for PPTX
        ImageOrPrintOptions pptxOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Pptx
        };

        // Step 3: Define the print area that captures the textbox (A1:D20)
        chartWorkbook.Worksheets[0].PageSetup.PrintArea = "A1:D20";

        // Step 4: Make the textbox editable in the exported PPTX
        chartWorkbook.Worksheets[0].PageSetup.IsTextBoxEditable = true;

        // Step 5: Export the worksheet to a PPTX file
        chartWorkbook.Save(@"YOUR_DIRECTORY\result.pptx", pptxOptions);
    }
}
```

**결과:** `result.pptx`를 PowerPoint에서 열면 Excel에 배치한 텍스트 상자가 일반 텍스트 박스로 변환되어 자유롭게 입력할 수 있습니다. 별도로 다시 만들 필요가 없습니다.

**흔한 실수:** 인쇄 영역에 병합 셀이 포함되어 있으면 슬라이드가 이동될 수 있습니다. 내보내기 전에 인쇄 영역을 조정하거나 셀 병합을 해제하세요.

---

## Smart Markers를 이용해 JSON → 단일 셀로 범위 복사

때때로 JSON 배열을 하나의 Excel 셀에 삽입해야 할 때가 있습니다. 예를 들어 하위 시스템에 JSON 문자열을 전달해야 할 경우가 그렇습니다. Aspose.Cells의 Smart Markers는 `ArrayAsSingle = true` 옵션을 사용하면 배열을 단일 셀에 직렬화할 수 있습니다.

### 단계별 안내

1. **Smart Marker 자리표시자(예: `&=Items.Name`)가 포함된 템플릿 워크북을 로드**합니다.  
2. **데이터 객체 준비** – `Items` 배열을 가진 익명 타입을 생성합니다.  
3. **`SmartMarkerProcessor`를 생성하고** `ArrayAsSingle` 옵션과 함께 데이터를 적용합니다.  
4. **채워진 워크북을 저장**합니다.

#### 전체 코드 예시

```csharp
using Aspose.Cells;
using System;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Load the template workbook containing a smart marker like "&=Items.Name"
        Workbook templateWorkbook = new Workbook(@"YOUR_DIRECTORY\SmartMarkerTemplate.xlsx");

        // Step 2: Prepare the data object with an array of items
        var data = new
        {
            Items = new[]
            {
                new { Name = "A" },
                new { Name = "B" }
            }
        };

        // Step 3: Apply the SmartMarkerProcessor with ArrayAsSingle option
        SmartMarkerProcessor processor = new SmartMarkerProcessor(templateWorkbook);
        processor.Apply(data, new SmartMarkerOptions { ArrayAsSingle = true });

        // Step 4: Save the result – the JSON array will appear in a single cell
        templateWorkbook.Save(@"YOUR_DIRECTORY\jsonSingleCell.xlsx");
    }
}
```

**설명:**  
`ArrayAsSingle`이 `true`이면 Aspose.Cells는 `Items.Name`의 각 요소를 JSON 형태 문자열(`["A","B"]`)로 연결하고, 스마트 마커가 있던 셀에 기록합니다. 이렇게 하면 배열 요소마다 별도 행을 만들 필요가 없습니다.

**사용 시점:** 구성 테이블, API 페이로드, 혹은 소비자가 탭ular 레이아웃이 아닌 압축된 JSON 문자열을 기대하는 모든 경우에 적합합니다.

---

## 추가 팁 및 예외 상황 처리

| 시나리오 | 주의할 점 | 권장 해결책 |
|----------|-------------------|---------------|
| **대형 피벗 테이블** | 피벗 캐시를 복사할 때 메모리 사용량이 급증합니다. | 로드하기 전에 `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference`를 사용하십시오. |
| **이미지가 포함된 PPTX 내보내기** | 이미지가 낮은 DPI로 래스터화될 수 있습니다. | `pptxOptions.ImageResolution = 300`를 설정하여 슬라이드를 선명하게 만드세요. |
| **스마트 마커 JSON 포맷팅** | 특수 문자(`"` , `\`)가 JSON을 깨뜨립니다. | 수동으로 이스케이프하거나 `JsonSerializer`를 사용해 사전 직렬화한 후 스마트 마커에 전달하십시오. |
| **다른 Excel 버전 간 범위 복사** | 오래된 `.xls` 파일은 서식이 손실될 수 있습니다. | 대상 파일을 `.xlsx`로 저장하여 최신 기능을 보존하십시오. |

---

## 요약 – 피벗 테이블 복사와 그 외 다양한 활용

우선 **피벗 테이블을 복사하면서 기능을 유지**하는 방법을 다루었고, 이어서 **Excel을 PPTX로 변환**, **텍스트 상자를 편집 가능한 PPTX로 만들기**, 마지막으로 **Smart Markers를 이용해 JSON 배열을 단일 셀에 삽입**하는 방법을 소개했습니다.  

세 가지 코드 스니펫은 모두 독립적이며, 새 콘솔 앱에 붙여넣고 파일 경로만 조정하면 바로 실행할 수 있습니다.

---

## 다음 단계

- **다른 내보내기 형식 탐색** – Aspose.Cells는 PDF, XPS, HTML도 지원합니다.  
- **피벗 테이블을 프로그래밍으로 새로 고침**하려면 복사 후 `PivotTable.RefreshData()`를 호출하세요.  
- **Smart Markers와 차트를 결합**해 자동으로 업데이트되는 대시보드를 생성해 보세요.  

**워크북을 PPTX로 저장**하면서 사용자 정의 슬라이드 레이아웃을 사용하고 싶다면 `SlideOptions`에 관한 Aspose.Cells 문서를 참고하세요.  

자유롭게 실험해 보세요—인쇄 영역을 바꾸거나, 다양한 `CopyOptions`를 시도하거나, 더 복잡한 JSON 페이로드를 넣어 보세요. 대부분의 보고 파이프라인에 충분히 유연한 API입니다.

---

### 자주 묻는 질문

**Q: `CopyPivotTable` 옵션이 슬라이서도 복사하나요?**  
A: 직접 복사되지 않습니다. 슬라이서는 별도 객체이므로 복사 후 `Worksheet.Shapes` 컬렉션을 통해 다시 만들거나 복사해야 합니다.

**Q: 여러 워크시트를 하나의 PPTX 데크에 내보낼 수 있나요?**  
A: 가능합니다. 각 워크시트를 순회하면서 동일한 `ImageOrPrintOptions`로 `Save`를 호출하고, `pptxOptions.StartSlideNumber`를 설정해 슬라이드 번호를 이어가면 됩니다.

**Q: JSON 배열에 중첩 객체가 포함된 경우는 어떻게 해야 하나요?**  
A: `ArrayAsSingle = false`로 설정하고, 중첩 구조를 반복 처리할 수 있는 커스텀 템플릿을 사용하십시오.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}