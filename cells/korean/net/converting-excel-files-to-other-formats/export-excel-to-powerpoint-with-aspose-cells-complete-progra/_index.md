---
category: general
date: 2026-08-14
description: Aspose.Cells를 사용하여 Excel을 PowerPoint로 내보내고 코드에서 Excel 수식을 계산하는 방법을 배웁니다.
  전체 소스가 포함된 단계별 C# 예제.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- calculate excel formulas in code
- Aspose.Cells copy pivot table
- export editable objects pptx
- dynamic array EXPAND function
- C# workbook automation
language: ko
lastmod: 2026-08-14
og_description: Aspose.Cells를 사용하여 Excel을 PowerPoint로 내보내고 코드에서 Excel 수식을 계산합니다. 이
  완전한 가이드를 따라 워크북에서 편집 가능한 PPTX 파일을 생성하세요.
og_image_alt: Screenshot showing an Excel sheet being exported to a PowerPoint slide
  with editable textboxes
og_title: Aspose.Cells를 사용하여 Excel을 PowerPoint로 내보내기 – 전체 C# 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  headline: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  type: TechArticle
- description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  name: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  steps:
  - name: Why this works
    text: '* **`Workbook`** loads the entire Excel file into memory, giving you full
      API access. * **`CopyRange`** with `CopyPivotTable = true` ensures the pivot
      table’s data source, cache, and layout are duplicated exactly—something older
      versions of Aspose.Cells could not do. * Adding a new worksheet (`Copy`'
  - name: Explanation
    text: '* **`WorkbookDesigner`** is a high‑level helper that prepares the workbook
      for export, handling Smart Markers, named ranges, and layout adjustments. *
      Setting `ExportEditableObjects = true` tells Aspose.Cells to translate Excel
      drawings into PowerPoint shapes rather than flattening them into images.'
  - name: Why you might use this
    text: '* **Uniform data type:** Exporting as strings avoids type‑mismatch errors
      when the consumer expects text. * **Custom formatting:** Replace `value.ToString()`
      with any custom formatter (e.g., `value.ToString("yyyy-MM-dd")` for dates).'
  - name: How the calculation engine works
    text: '* The `Formula` property stores the expression exactly as you would type
      it in Excel. * `CalculateFormula()` triggers a full workbook recalculation,
      respecting dependencies between cells. * The `EXPAND` function (available in
      Excel 365) returns a spill range based on the source cell (`B1`) and the s'
  - name: What to verify
    text: '* Open `result.xlsx` in Excel to confirm the pivot table copy, the `EXPAND`
      formula result, and any custom‑exported strings. * Open `output.pptx` in PowerPoint;
      you should see a slide that mirrors the Excel layout, and all charts/textboxes
      should be editable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
- Office 365 functions
title: Aspose.Cells를 사용한 Excel을 PowerPoint로 내보내기 – 완전한 프로그래밍 가이드
url: /ko/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-aspose-cells-complete-progra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells를 사용한 Excel을 PowerPoint로 내보내기 – 완전한 프로그래밍 가이드

프로그래밍 방식으로 **Excel을 PowerPoint로 내보내야** 하는 경우, 이 가이드는 Aspose.Cells for .NET을 사용하여 정확히 어떻게 수행하는지 보여줍니다. 또한 **코드에서 Excel 수식을 계산하는 방법**, 피벗 테이블을 정의를 잃지 않고 복사하는 방법, 그리고 동적 배열을 위한 새로운 Office‑365 EXPAND 함수 사용법을 배울 수 있습니다.

다음 섹션에서는 실제 C# 예제를 단계별로 살펴보고, 각 라인이 왜 중요한지 설명하며, 일반적인 함정들을 다루어 여러분이 이 솔루션을 자신의 프로젝트에 맞게 적용할 수 있도록 도와드립니다.

## 이 튜토리얼에서 다루는 내용

* 기존 워크북(`input.xlsx`) 로드  
* 피벗 테이블을 포함한 범위를 복사하면서 정의를 보존  
* 워크북을 편집 가능한 텍스트 상자와 도형이 포함된 PowerPoint(`.pptx`) 파일로 내보내기  
* 사용자 정의 로직을 사용해 셀 범위를 문자열로 내보내기  
* Office‑365 EXPAND 함수를 포함한 Excel 수식을 코드에서 계산하기  
* 모든 변경 사항이 적용된 최종 워크북 저장  

**전제 조건**  
* .NET 6.0 이상 (코드는 .NET Framework 4.7.2+에서도 작동)  
* Aspose.Cells for .NET v25.11 이상 (`CopyPivotTable` 옵션은 v25.11에서 도입)  
* C# 및 Excel 개념(범위, 피벗 테이블, 수식 등)에 대한 기본 이해  

> **Pro tip:** 최신 기능을 유지하려면 NuGet(`Install-Package Aspose.Cells`)을 통해 Aspose.Cells를 설치하세요.

## Aspose.Cells를 사용한 Excel을 PowerPoint로 내보내기

첫 번째 주요 작업은 워크북을 PowerPoint 프레젠테이션으로 변환하면서 모든 시각 요소를 편집 가능하게 유지하는 것입니다. 이는 재무 보고서나 대시보드에서 슬라이드 덱을 자동으로 생성하려는 경우에 필수적입니다.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;      // ExportTableOptions, ExportOptions, etc.
using Aspose.Cells.Pivot;      // Pivot‑table APIs
using Aspose.Cells.Drawing;    // Shapes, textboxes, etc.

// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Step 2: Copy a range that contains a pivot table (preserves the definition)
Worksheet sourceSheet = workbook.Worksheets["Source"];
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");   // includes a pivot table
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
destinationSheet.Cells.CopyRange(sourceRange, destinationSheet.Cells, new CopyOptions
{
    CopyPivotTable = true   // new option in v25.11
});
```

### 왜 이렇게 동작하는가

* **`Workbook`** 은 전체 Excel 파일을 메모리로 로드하여 전체 API에 접근할 수 있게 합니다.  
* **`CopyRange`** 에 `CopyPivotTable = true` 를 지정하면 피벗 테이블의 데이터 소스, 캐시 및 레이아웃이 정확히 복제됩니다—이는 이전 버전의 Aspose.Cells에서는 지원되지 않았습니다.  
* 새 워크시트(`Copy`)를 추가하면 원본 시트를 그대로 두고 작업할 수 있어 감사 추적에 유용합니다.

## 편집 가능한 개체와 함께 워크북을 PowerPoint로 내보내기

이제 워크북을 PowerPoint 파일로 변환합니다. `ExportEditableObjects` 를 활성화하면 모든 차트, 도형, 텍스트 상자가 내보낸 후에도 사용자가 직접 편집할 수 있는 네이티브 PowerPoint 개체가 됩니다.

```csharp
// Step 3: Export the workbook to PowerPoint with editable textboxes/shapes
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.Process();   // processes Smart Markers if present
designer.ExportToPptx("YOUR_DIRECTORY/output.pptx", new ExportOptions
{
    ExportEditableObjects = true   // makes objects editable in the PPTX
});
```

### 설명

* **`WorkbookDesigner`** 는 스마트 마커, 명명된 범위 및 레이아웃 조정을 처리하면서 워크북을 내보내기 위해 준비하는 고수준 헬퍼입니다.  
* `ExportEditableObjects = true` 로 설정하면 Aspose.Cells가 Excel 도면을 이미지가 아닌 PowerPoint 도형으로 변환합니다. 이를 통해 **완전히 편집 가능한** 슬라이드 덱을 얻을 수 있습니다.

> **Edge case:** 워크북에 외부 데이터 연결을 기반으로 만든 복잡한 차트가 포함된 경우, `ExportToPptx` 를 호출하기 전에 해당 연결이 해결되었는지 확인하세요. 그렇지 않으면 차트가 빈 상태로 나타날 수 있습니다.

## 사용자 정의 로직을 사용해 범위를 문자열로 내보내기

때때로 다운스트림 처리(예: CSV 파서에 전달)를 위해 원시 문자열 값이 필요합니다. `ExportTableOptions` 클래스를 사용하면 각 셀을 어떻게 변환할지 제어할 수 있습니다.

```csharp
// Step 4: Export a range as strings using custom logic
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true,
    CustomExport = (cell, value) => value.ToString()   // simple conversion for each cell
};
workbook.Worksheets[0].Cells.ExportTableAsString(tableOptions, "A1:D10");
```

### 이를 사용하는 이유

* **일관된 데이터 유형:** 문자열로 내보내면 소비자가 텍스트를 기대할 때 타입 불일치 오류를 방지합니다.  
* **사용자 정의 서식:** `value.ToString()` 을 `value.ToString("yyyy-MM-dd")` 와 같이 날짜 형식 지정자와 함께 교체해 원하는 형식으로 출력할 수 있습니다.  

## 코드에서 Excel 수식 계산하기

자주 요구되는 작업 중 하나는 **Excel 수식을 코드를 통해 계산** 하는 것입니다. Aspose.Cells는 오프라인에서도 작동하고 최신 Office‑365 함수(예: `EXPAND`)를 지원하는 내장 계산 엔진을 제공합니다.

```csharp
// Step 5: Use the new Office‑365 EXPAND function to create a dynamic array
Worksheet firstSheet = workbook.Worksheets[0];
firstSheet.Cells["A1"].Formula = "EXPAND(B1,5,3)";   // expands array starting at B1
workbook.CalculateFormula();   // forces recalculation of the formula
```

### 계산 엔진 작동 방식

* `Formula` 속성은 Excel에 입력하는 식을 그대로 저장합니다.  
* `CalculateFormula()` 를 호출하면 워크북 전체가 재계산되며, 셀 간 종속성을 고려합니다.  
* `EXPAND` 함수(Excel 365에서 사용 가능)는 원본 셀(`B1`)과 지정된 행(`5`) 및 열(`3`)을 기준으로 스필 범위를 반환합니다.  

> **Tip:** 워크북 전체가 아니라 일부만 계산하고 싶다면 `Worksheet.CalculateFormula()` 를 사용해 범위를 제한하고 성능을 향상시킬 수 있습니다.

## 모든 변경 사항이 적용된 워크북 저장하기

마지막으로 수정된 워크북을 디스크에 기록합니다. 파일 확장자를 변경하면 지원되는 모든 형식(`.xlsx`, `.xls`, `.csv` 등)으로 저장할 수 있습니다.

```csharp
// Step 6: Save the workbook with all changes applied
workbook.Save("YOUR_DIRECTORY/result.xlsx");
```

### 확인할 사항

* `result.xlsx` 를 Excel에서 열어 피벗 테이블 복사본, `EXPAND` 수식 결과 및 사용자 정의 문자열 내보내기가 정상인지 확인합니다.  
* `output.pptx` 를 PowerPoint에서 열어 Excel 레이아웃을 그대로 반영하고 차트·텍스트 상자가 모두 편집 가능한지 확인합니다.

## 일반적인 질문 및 문제 해결

| Question | Answer |
|----------|--------|
| **Aspose.Cells를 사용하려면 라이선스가 필요합니까?** | 예. 평가용 트라이얼은 평가에 사용할 수 있지만, 정식 라이선스를 적용하면 평가 워터마크가 제거되고 `CopyPivotTable` 기능이 활성화됩니다. |
| **내보낸 PPTX 파일에 빈 도형이 표시되면 어떻게 해야 하나요?** | 워크북의 그리기 개체가 숨겨져 있지 않은지(`Visible = true`) 확인하고, 외부 이미지 링크가 모두 임베드된 상태인지 확인한 후 내보내세요. |
| **여러 워크시트를 별개의 PPTX 슬라이드로 내보낼 수 있나요?** | `WorkbookDesigner.ExportToPptx` 를 루프에서 사용하고 각 워크시트마다 다른 `ExportOptions` 를 지정하거나, Aspose.Slides를 이용해 슬라이드를 수동으로 추가해 하나의 프레젠테이션으로 결합할 수 있습니다. |
| **`CalculateFormula` 가 스레드‑안전한가요?** | 아닙니다. 단일 스레드에서 계산을 수행하거나 스레드당 워크북을 복제하여 레이스 컨디션을 방지하세요. |

## 결론

이제 Aspose.Cells를 사용해 **Excel을 PowerPoint로 완전하게 내보내는** 엔드‑투‑엔드 솔루션을 갖추었으며, **코드에서 Excel 수식을 계산** 하는 방법도 이해했습니다—최신 `EXPAND` 함수까지 포함됩니다. 튜토리얼에서는 워크북 로드, 피벗 테이블 복사, 편집 가능한 PowerPoint 내보내기, 사용자 정의 문자열 내보내기, 수식 계산 및 최종 저장 과정을 모두 다루었습니다.

앞으로 할 수 있는 일:

* 워크시트당 여러 슬라이드를 포함하도록 내보내기를 확장하기(키워드: *코드에서 Excel 수식을 계산* 를 차트 데이터 생성 시 재활용).  
* Aspose.Slides를 통합해 애니메이션이나 마스터 슬라이드 레이아웃을 추가하기.  
* 간단한 `CustomExport` 대리자를 국제화된 포맷팅으로 교체해 다국어 프로젝트에 적용하기.  

다양한 범위를 실험해 보고, 다른 Office‑365 함수(`FILTER`, `SORT` 등)도 탐색하며, 자동 이메일 전송과 결합해 완전 자동화된 보고 파이프라인을 구축해 보세요.

---


## 다음에 배워야 할 내용은 무엇인가요?

다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하며, 관련 주제를 깊이 있게 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 제공하여 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용할 수 있도록 돕습니다.

- [Aspose.Cells for .NET을 사용한 Excel 데이터 자동 내보내기: 단계별 가이드](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)
- [Aspose.Cells for .NET을 사용한 Excel 차트를 PDF로 내보내는 방법: 단계별 가이드](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Aspose.Cells .NET을 사용한 Excel 셀을 이미지로 내보내기: 단계별 가이드](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}