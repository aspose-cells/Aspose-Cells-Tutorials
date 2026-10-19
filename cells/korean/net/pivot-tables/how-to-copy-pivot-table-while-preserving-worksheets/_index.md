---
category: general
date: 2026-09-15
description: Aspose.Cells를 사용하여 C#에서 피벗 테이블 복사, 피벗이 포함된 워크시트 복사 및 워크북을 PPTX 파일로 저장하는
  방법을 배웁니다. 단계별 완전 가이드.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy worksheet with pivot
- save workbook as pptx
language: ko
lastmod: 2026-09-15
og_description: Aspose.Cells를 사용하여 피벗 테이블을 복사하고, 피벗이 포함된 워크시트를 복사하며, 워크북을 pptx 파일로
  저장하는 방법. 완전하고 실행 가능한 C# 예제를 따라 보세요.
og_image_alt: Screenshot showing how to copy pivot table in a C# code editor
og_title: 피벗 테이블 복사 및 워크시트 내보내기 방법 – 전체 C# 가이드
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  headline: How to copy pivot table while preserving worksheets
  type: TechArticle
- description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  name: How to copy pivot table while preserving worksheets
  steps:
  - name: – Load the source workbook that holds the pivot table
    text: '```csharp // Load the workbook that contains the pivot table you want to
      copy Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx"); ```'
  - name: – Create an empty destination workbook
    text: '```csharp // Create a new, empty workbook that will receive the copied
      data Workbook destinationWorkbook = new Workbook(); ```'
  - name: – Copy the rows that include the pivot table
    text: '```csharp // Copy rows 0‑19 (A1:G20) from the first worksheet of the source
      sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20); ```'
  - name: – Copy the columns that contain the pivot table
    text: '```csharp // Copy columns 0‑6 (A‑G) from the same worksheet sourceWorkbook.Worksheets[0].Cells.CopyColumns(0,
      0, 7); ```'
  - name: – Transfer the prepared sheet into the destination workbook
    text: '```csharp // Move the fully prepared worksheet into the destination workbook
      sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]); ```'
  - name: – Save the result – the pivot table remains intact
    text: '```csharp // Save the destination workbook; the pivot table works exactly
      like the original destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
      ```'
  - name: – Load the workbook that includes the textbox
    text: '```csharp // Load the Excel file that contains an editable textbox shape
      Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
      ```'
  - name: – Configure PPTX save options
    text: '```csharp // Create PPTX save options and enable the editable textbox feature
      (available from v25.11) PptxSaveOptions pptxOptions = new PptxSaveOptions {
      ExportEditableTextBox = true }; ```'
  - name: – Save the workbook as PPTX
    text: '```csharp // Export the workbook to a PPTX file; the textbox stays editable
      in PowerPoint workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
      ```'
  - name: – Prepare the SmartMarkerProcessor
    text: '```csharp // Initialise the processor that will fill Smart Markers SmartMarkerProcessor
      smartMarkerProcessor = new SmartMarkerProcessor(); ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: 워크시트를 보존하면서 피벗 테이블 복사하는 방법
url: /ko/net/pivot-tables/how-to-copy-pivot-table-while-preserving-worksheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 피벗 테이블을 복사하면서 워크시트를 보존하는 방법

하나의 워크북에서 다른 워크북으로 **how to copy pivot table** 하면서 기본 피벗 캐시를 잃지 않으려면, 이 가이드는 바로 실행 가능한 솔루션을 제공합니다. 또한 **copy worksheet with pivot** 및 **save workbook as pptx** 를 수행하면서 편집 가능한 텍스트 상자를 그대로 유지하는 방법도 확인할 수 있습니다. 모든 예제는 최신 Aspose.Cells for .NET을 사용하므로 코드를 C# 프로젝트에 바로 넣어 즉시 결과를 확인할 수 있습니다.

프로그래밍 방식으로 Excel 파일을 다룰 때는 워크북 간 데이터 이동, 프레젠테이션으로 내보내기, 복잡한 Smart Marker 삽입 등이 자주 발생합니다. 아래의 세 개 코드 스니펫은 이러한 일반적인 시나리오를 다루며 각 단계가 중요한 이유를 설명합니다.

## 사전 요구 사항

* .NET 6.0 이상이 설치되어 있어야 합니다  
* 프로젝트에 참조된 Aspose.Cells for .NET (버전 25.11 이상)  
* `YOUR_DIRECTORY` 라는 폴더가 필요하며, 샘플 파일을 읽고 쓸 때 사용됩니다  

추가적인 NuGet 패키지는 필요하지 않습니다.

---

## Aspose.Cells를 사용하여 피벗 테이블 복사하기

피벗 캐시를 보존하면서 피벗 테이블이 포함된 범위를 복사하는 것은 흔한 요구 사항입니다. 아래 단계는 필요한 정확한 순서를 보여줍니다.

### 단계 1 – 피벗 테이블이 포함된 원본 워크북 로드

```csharp
// Load the workbook that contains the pivot table you want to copy
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
```

*Why*: Aspose.Cells는 워크북을 메모리로 읽어들여 워크시트, 셀 및 피벗 테이블에 접근할 수 있게 합니다.

### 단계 2 – 빈 대상 워크북 생성

```csharp
// Create a new, empty workbook that will receive the copied data
Workbook destinationWorkbook = new Workbook();
```

*Why*: 빈 워크북으로 시작하면 숨겨진 스타일이나 이름이 정의된 범위가 복사 작업에 방해되지 않음을 보장합니다.

### 단계 3 – 피벗 테이블이 포함된 행 복사

```csharp
// Copy rows 0‑19 (A1:G20) from the first worksheet of the source
sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20);
```

*Why*: `CopyRows`는 원시 셀 값, 서식 및 기본 피벗 캐시 참조를 복사합니다. 범위에는 피벗 테이블 전체 영역이 포함되어야 합니다.

### 단계 4 – 피벗 테이블이 포함된 열 복사

```csharp
// Copy columns 0‑6 (A‑G) from the same worksheet
sourceWorkbook.Worksheets[0].Cells.CopyColumns(0, 0, 7);
```

*Why*: 피벗 테이블은 행과 열 모두에 걸쳐 있으므로, 열을 복사하면 전체 테이블 레이아웃이 유지됩니다.

### 단계 5 – 준비된 시트를 대상 워크북으로 전송

```csharp
// Move the fully prepared worksheet into the destination workbook
sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]);
```

*Why*: `Copy` 메서드는 피벗 캐시를 포함한 워크시트를 복제하므로, 대상 워크북에 동일한 피벗 테이블이 표시됩니다.

### 단계 6 – 결과 저장 – 피벗 테이블이 그대로 유지됨

```csharp
// Save the destination workbook; the pivot table works exactly like the original
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Why*: 워크북을 저장하면 모든 내부 구조가 기록되어 나중에 피벗을 새로 고칠 수 있음을 보장합니다.

**Pro tip**: 복사 후, 원본 데이터가 변경되었을 경우 `destinationWorkbook.Worksheets[0].PivotTables[0].Refresh()` 를 호출하여 데이터를 업데이트할 수 있습니다.

---

## 피벗이 포함된 워크시트 복사 – 간결한 대안

이미 피벗 테이블이 포함된 전체 워크시트를 복제하기만 하면 된다면, 행/열 복사 단계를 건너뛰고 워크시트 수준의 `Copy` 메서드를 직접 사용할 수 있습니다.

```csharp
// Load source workbook
Workbook src = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

// Create destination workbook
Workbook dst = new Workbook();

// Copy the first worksheet (including its pivot table) to the destination
src.Worksheets[0].Copy(dst.Worksheets[0]);

// Save the new file
dst.Save("YOUR_DIRECTORY/WorksheetCopy.xlsx");
```

이 방법은 워크시트에 피벗 영역 외에 추가 데이터가 없을 때 유용합니다. **copy worksheet with pivot** 작업은 모든 서식, 이름이 정의된 범위 및 피벗 캐시를 자동으로 보존합니다.

---

## 편집 가능한 텍스트 상자를 포함한 PPTX 형식으로 워크북 저장

편집 가능한 텍스트 상자가 포함된 Excel 시트를 PowerPoint로 내보내야 하는 경우가 보고 대시보드에 필요할 수 있습니다. 아래 코드는 텍스트 상자를 편집 가능하게 유지하면서 **save workbook as pptx** 하는 방법을 보여줍니다.

### 단계 1 – 텍스트 상자가 포함된 워크북 로드

```csharp
// Load the Excel file that contains an editable textbox shape
Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
```

### 단계 2 – PPTX 저장 옵션 구성

```csharp
// Create PPTX save options and enable the editable textbox feature (available from v25.11)
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableTextBox = true
};
```

*Why*: `ExportEditableTextBox` 설정은 Aspose.Cells에게 Excel 텍스트 상자를 PowerPoint 도형으로 변환하도록 지시하며, 내보낸 후에도 편집 가능하도록 유지합니다.

### 단계 3 – 워크북을 PPTX로 저장

```csharp
// Export the workbook to a PPTX file; the textbox stays editable in PowerPoint
workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
```

**Expected result**: PowerPoint에서 `Result.pptx` 를 열고 텍스트 상자를 선택한 뒤, 마치 기본 도형처럼 내용을 편집할 수 있습니다.

**Common question**: *텍스트 상자를 잠금 상태로 유지하려면 어떻게 해야 하나요?*  
`pptxOptions.ExportEditableTextBox = false` 로 설정하면 도형이 정적 이미지로 변환됩니다.

## JSON 배열을 단일 셀 값으로 포함하는 Smart Marker 내보내기

Smart Marker를 사용하면 복잡한 데이터 구조로 Excel 템플릿을 채울 수 있습니다. 아래는 **how to copy pivot table** 스타일의 데이터 처리를 보여주면서 JSON 배열을 단일 셀에 삽입하는 전체 예제입니다.

### 단계 1 – SmartMarkerProcessor 준비

```csharp
// Initialise the processor that will fill Smart Markers
SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
```

### 단계 2 – 셀 A1에 Smart Marker 삽입

```csharp
// The marker ${Orders:ArrayAsSingle} tells the processor to write the whole array into one cell
Workbook workbook = new Workbook();
workbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
```

### 단계 3 – JSON 형태 배열을 사용한 데이터 소스 정의

```csharp
// Anonymous object that mimics a JSON array
var dataModel = new { Orders = new[] { "A", "B", "C" } };
```

### 단계 4 – 워크북 처리

```csharp
// Fill the Smart Marker with the array data; the array becomes a comma‑separated string
smartMarkerProcessor.Process(workbook, dataModel);
```

### 단계 5 – 결과 워크북 저장

```csharp
// Persist the workbook; cell A1 now contains "A,B,C"
workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
```

**Result verification**: `JsonSingleCell.xlsx` 를 열어 셀 A1에 `A,B,C` 가 표시되는지 확인합니다. 이는 컬렉션을 단일 셀 값으로 처리하는 방법을 보여주며, 하위 시스템으로 데이터를 내보낼 때 자주 필요한 패턴입니다.

## 전체 작업 예제

아래는 세 시나리오를 모두 결합한 단일 프로그램입니다. 코드를 콘솔 앱에 복사하고 파일 경로를 조정한 뒤 실행하면 세 가지 결과를 모두 확인할 수 있습니다.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1. How to copy pivot table (preserve pivot cache)
        // -------------------------------------------------
        Workbook srcPivot = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Workbook dstPivot = new Workbook();
        srcPivot.Worksheets[0].Cells.CopyRows(0, 0, 20);
        srcPivot.Worksheets[0].Cells.CopyColumns(0, 0, 7);
        srcPivot.Worksheets[0].Copy(dstPivot.Worksheets[0]);
        dstPivot.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");

        // -------------------------------------------------
        // 2. Save workbook as PPTX with editable textbox
        // -------------------------------------------------
        Workbook txtWorkbook = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
        PptxSaveOptions pptxOpts = new PptxSaveOptions { ExportEditableTextBox = true };
        txtWorkbook.Save("YOUR_DIRECTORY/Result.pptx", pptxOpts);

        // -------------------------------------------------
        // 3. Export Smart Marker containing a JSON array
        // -------------------------------------------------
        SmartMarkerProcessor smProcessor = new SmartMarkerProcessor();
        Workbook smWorkbook = new Workbook();
        smWorkbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
        var model = new { Orders = new[] { "A", "B", "C" } };
        smProcessor.Process(smWorkbook, model);
        smWorkbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
    }
}
```

이 프로그램을 실행하면 다음과 같은 결과가 생성됩니다:

* `CopyWithPivot.xlsx` – 원본 피벗 테이블을 완벽히 복사한 파일.  
* `Result.pptx` – 편집 가능한 텍스트 상자가 포함된 PowerPoint 슬라이드.  
* `JsonSingleCell.xlsx` – JSON 배열이 단일 셀에 표시되는 시트.

## 결론

이제 **how to copy pivot table** 를 안전하게 수행하는 방법, **copy worksheet with pivot** 를 한 번에 복사하는 방법, 그리고 편집 가능한 텍스트 상자를 보존하면서 **save workbook as pptx** 하는 방법을 알게 되었습니다. 이러한 패턴은 기업 자동화 프로젝트에서 마주하게 되는 가장 일반적인 Excel‑to‑PowerPoint 및 Excel‑to‑JSON 워크플로를 포괄합니다.

다음으로, 아래 항목들을 살펴보세요:

* 복사된 피벗 테이블을 프로그래밍 방식으로 새로 고치기 (`PivotTable.Refresh()`)  
* PDF 또는 HTML 등 다른 형식으로 내보내기 (`PdfSaveOptions`, `HtmlSaveOptions`)  
* 맞춤 함수나 조건부 서식과 같은 고급 Smart Marker 옵션 사용  

다양한 범위, 여러 워크시트, 더 큰 JSON 구조 등을 자유롭게 실험해 보세요. Aspose.Cells API는 세밀한 제어를 제공하므로 이 예제를 실제 시나리오에 맞게 조정할 수 있습니다. 즐거운 코딩 되세요!

## 다음에 배워야 할 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료에는 단계별 설명과 함께 완전한 코드 예제가 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Copy Sheets Within Workbook Using Aspose.Cells for .NET - Step‑By‑Step Guide](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}