---
category: general
date: 2026-10-20
description: Aspose.Cells를 사용하여 피벗 테이블을 새 워크북으로 복사하고, 편집 가능한 도형을 PowerPoint로 내보내는
  방법을 한 가이드에서 배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table to new workbook
- copy rows between worksheets
- Aspose.Cells copy rows
- export shape to PowerPoint
- editable textbox in PowerPoint
language: ko
lastmod: 2026-10-20
og_description: Aspose.Cells를 사용하여 피벗 테이블을 새 워크북으로 복사하고 편집 가능한 도형을 PowerPoint로 내보내기—오늘
  바로 실행할 수 있는 단계별 코드.
og_image_alt: Screenshot showing copy pivot table to new workbook using Aspose.Cells
og_title: 피벗 테이블을 새 워크북에 복사하고, 도형을 파워포인트로 내보내기
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  headline: Copy pivot table to new workbook, export shape to PowerPoint
  type: TechArticle
- description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  name: Copy pivot table to new workbook, export shape to PowerPoint
  steps:
  - name: – Load the source workbook and select the first worksheet
    text: '```csharp // Load the workbook that already contains the pivot table Workbook
      srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");'
  - name: – Define the cell area that includes the pivot table
    text: '```csharp // CellArea(startRow, startColumn, endRow, endColumn) // Here
      we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table CellArea
      sourceArea = new CellArea(0, 0, 20, 10); ```'
  - name: – Create the destination workbook and get its first worksheet
    text: '```csharp // Create an empty workbook that will receive the copied range
      Workbook destWorkbook = new Workbook();'
  - name: – Copy the rows from the source area to the destination sheet
    text: '```csharp // CopyRows(startRow, endRow, destinationCells, destinationStartRow)
      srcWorksheet.Cells.CopyRows( sourceArea.StartRow, sourceArea.EndRow, destWorksheet.Cells,
      0); // start at row 0 in the destination sheet ```'
  - name: – Save the new workbook
    text: '```csharp destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx"); ```'
  - name: – Create a new workbook and access its first worksheet
    text: '```csharp Workbook workbook = new Workbook(); // Empty workbook Worksheet
      worksheet = workbook.Worksheets[0]; // First (and only) sheet ```'
  - name: – Add a textbox shape to the worksheet
    text: '```csharp // AddTextBox(startRow, startColumn, width, height, text) int
      shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
      ```'
  - name: – Retrieve the shape and modify its text
    text: '```csharp Shape textShape = worksheet.Shapes[shapeIndex]; textShape.Text
      = "Change me in PowerPoint"; ```'
  - name: – Save the workbook as a PowerPoint presentation
    text: '```csharp workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
      ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Pivot Table
- PowerPoint Export
title: 피벗 테이블을 새 워크북에 복사하고, 도형을 PowerPoint로 내보내기
url: /ko/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 피벗 테이블을 새 워크북으로 복사하고, 도형을 PowerPoint로 내보내기

피벗 테이블을 기능을 유지한 채 **새 워크북으로 복사**해야 한다면, 이 가이드는 Aspose.Cells를 사용하여 정확히 수행하는 방법을 보여줍니다. 또한 **편집 가능한 도형을 PowerPoint로 내보내는** 가장 빠른 방법을 확인할 수 있으며, 변환 후에도 텍스트 상자가 편집 가능하게 유지됩니다.

많은 개발자들이 피벗 테이블이 포함된 범위를 복사하면 피벗 로직이 손실되거나, 도형을 PPTX로 저장하면 정적인 이미지가 된다고 생각합니다. 이 튜토리얼은 이러한 오해를 깨고 신뢰할 수 있는 프로덕션‑레디 솔루션을 제공합니다.

다음 섹션에서는:

* 소스 워크북을 로드하고 피벗 테이블이 포함된 범위를 복사합니다.
* 동일한 피벗 테이블을 포함하는 대상 워크북을 생성합니다.
* 텍스트 상자 도형을 추가하고 텍스트를 수정한 뒤, 텍스트 상자가 편집 가능한 상태로 유지되는 PowerPoint 프레젠테이션으로 워크북을 저장합니다.
* 각 API 호출이 필요한 이유와 일반적인 함정을 피하는 방법을 이해합니다.

**Prerequisites**

* .NET 6.0 이상 (코드는 .NET Framework 4.7+에서도 동작합니다).
* Aspose.Cells for .NET 설치 (`Install-Package Aspose.Cells`).
* C# 및 Visual Studio(또는 선호하는 IDE)에 대한 기본 지식.

---

## Copy pivot table to new workbook

이 단계별 섹션에서는 피벗 테이블이 포함된 범위를 복사하고 새 파일에서 피벗 정의를 유지하는 방법을 보여줍니다.

### Step 1 – Load the source workbook and select the first worksheet

```csharp
// Load the workbook that already contains the pivot table
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// The first worksheet (index 0) holds the pivot table we want to copy
Worksheet srcWorksheet = srcWorkbook.Worksheets[0];
```

*Why?*  
`Workbook`은 Aspose.Cells에서 Excel 조작을 위한 진입점입니다. 올바른 워크시트를 선택하면 정확한 피벗 테이블 위치에서 작업하게 됩니다.

### Step 2 – Define the cell area that includes the pivot table

```csharp
// CellArea(startRow, startColumn, endRow, endColumn)
// Here we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table
CellArea sourceArea = new CellArea(0, 0, 20, 10);
```

*Why?*  
피벗 테이블은 특정 셀 블록 안에 존재합니다. 피벗을 완전히 포함하는 `CellArea`를 지정하면 Aspose.Cells가 기본 피벗 캐시까지 복사한다는 것을 인식합니다.

### Step 3 – Create the destination workbook and get its first worksheet

```csharp
// Create an empty workbook that will receive the copied range
Workbook destWorkbook = new Workbook();

// Destination worksheet (also index 0)
Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Why?*  
새 워크북을 사용하면 충돌하는 이름 범위나 기존 피벗이 없으므로 복사 작업이 깔끔하게 수행됩니다.

### Step 4 – Copy the rows from the source area to the destination sheet

```csharp
// CopyRows(startRow, endRow, destinationCells, destinationStartRow)
srcWorksheet.Cells.CopyRows(
    sourceArea.StartRow,
    sourceArea.EndRow,
    destWorksheet.Cells,
    0); // start at row 0 in the destination sheet
```

*Why?*  
`CopyRows`는 **Aspose.Cells copy rows** API의 일부입니다. 셀 값과 숨겨진 피벗 캐시를 모두 복사하므로 이동 후에도 피벗 테이블이 정상적으로 작동합니다.

### Step 5 – Save the new workbook

```csharp
destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Result*  
Excel에서 `CopyWithPivot.xlsx`를 열면 피벗 테이블이 원본 파일과 동일하게 표시되며, 정상적으로 새로 고침하거나 수정할 수 있습니다.

---

## Export editable shape to PowerPoint

이제 텍스트 상자 도형을 추가하고 내용을 변경한 뒤, 워크북을 PPTX 파일로 저장합니다. PowerPoint에서 열면 도형이 완전히 편집 가능한 상태로 유지됩니다.

### Step 1 – Create a new workbook and access its first worksheet

```csharp
Workbook workbook = new Workbook();          // Empty workbook
Worksheet worksheet = workbook.Worksheets[0]; // First (and only) sheet
```

### Step 2 – Add a textbox shape to the worksheet

```csharp
// AddTextBox(startRow, startColumn, width, height, text)
int shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
```

*Why?*  
`AddTextBox`는 **PowerPoint와 호환되는 편집 가능한 텍스트 상자** 도형을 생성합니다. 좌표는 포인트 단위이며, 레이아웃에 맞게 조정하면 됩니다.

### Step 3 – Retrieve the shape and modify its text

```csharp
Shape textShape = worksheet.Shapes[shapeIndex];
textShape.Text = "Change me in PowerPoint";
```

*Why?*  
`Shape` 객체에 직접 접근하면 `Text`, `Font`, `Fill` 등 속성을 변경할 수 있습니다. 이 단계에서는 초기 콘텐츠를 프로그래밍 방식으로 설정하는 방법을 보여줍니다.

### Step 4 – Save the workbook as a PowerPoint presentation

```csharp
workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
```

*Result*  
Microsoft PowerPoint에서 `Presentation.pptx`를 열면 첫 번째 슬라이드에 텍스트 상자가 나타나며, 더블 클릭하여 네이티브 PowerPoint 도형처럼 텍스트를 편집할 수 있습니다.

---

## Expected output

| File | What you’ll see |
|------|-----------------|
| `CopyWithPivot.xlsx` | 원본 피벗 테이블이 포함된 워크시트가 표시되며, 완전히 기능합니다(새로 고침 가능). |
| `Presentation.pptx` | “Change me in PowerPoint”라는 텍스트가 들어 있는 편집 가능한 텍스트 상자가 있는 단일 슬라이드가 표시됩니다. |

---

## Common pitfalls and best‑practice tips

* **Pivot cache loss** – 셀 값만 복사(`CopyRows`에 `PasteOptions` 플래그를 `PasteValues`로 설정)하면 피벗 캐시가 누락되어 테이블이 정적으로 변합니다. 반드시 예시와 같이 기본 `CopyRows` 오버로드를 사용하세요.
* **Shape positioning** – `AddTextBox`는 포인트 단위를 사용하며 Excel 셀 인덱스를 사용하지 않습니다. 샘플 파일에서 좌표를 테스트하여 슬라이드 밖에 배치되는 일을 방지하세요.
* **File format mismatch** – `SaveFormat.Pptx`로 워크북을 저장하면 지원되는 모든 도형이 자동으로 변환됩니다. `Pdf`로 저장하면 도형이 래스터화되어 편집이 불가능해집니다.

---

## Conclusion

이제 **새 워크북으로 피벗 테이블을 복사**하고 **편집 가능한 도형을 PowerPoint로 내보내는** 방법을 Aspose.Cells for .NET을 사용해 알게 되었습니다. 완전한 실행 가능한 코드 예제는 필요한 모든 API 호출을 다루고, 각 단계가 중요한 이유를 설명하며 기대 결과를 보여줍니다.

다음과 같은 주제를 탐색해 볼 수 있습니다:

* **Working with charts** – 피벗 테이블과 함께 차트를 복사(`Aspose.Cells copy rows between worksheets`).

## What Should You Learn Next?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 포함하여 추가 API 기능을 마스터하고 프로젝트에 적용할 수 있는 다양한 구현 방법을 탐색하도록 돕습니다.

- [새 워크북 만들기 – 피벗 테이블이 포함된 워크시트 복사 방법](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [피벗 테이블 복사 및 Excel을 PPTX로 내보내기 (Aspose.Cells 사용)](/cells/english/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/)
- [C#에서 새 워크북 만들기 – 피벗 테이블 복사](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}