---
category: general
date: 2026-09-15
description: SVG에 글꼴을 삽입하고 Excel 차트를 PowerPoint로 내보내는 방법을 배우세요. XLSX를 SVG로 변환하고 XLSX를
  PPTX로 변환하는 전체 코드 예제를 포함합니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in SVG
- export excel chart to powerpoint
- convert xlsx to svg
- convert xlsx to pptx
- save workbook as svg
language: ko
lastmod: 2026-09-15
og_description: SVG에 글꼴을 포함하고 단계별 C# 코드로 Excel 차트를 PowerPoint로 내보내세요. XLSX를 SVG로,
  XLSX를 PPTX로 빠르고 안정적으로 변환합니다.
og_image_alt: Screenshot showing an Excel chart exported to PowerPoint with embedded
  fonts in the resulting SVG file
og_title: SVG에 폰트 삽입 및 Excel 차트를 PowerPoint로 내보내는 완전 가이드
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  headline: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  type: TechArticle
- description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  name: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  steps:
  - name: Open `EditableChart.pptx` in PowerPoint.
    text: Open `EditableChart.pptx` in PowerPoint.
  - name: Locate the slide containing the chart.
    text: Locate the slide containing the chart.
  - name: Choose **Chart Tools → Design → Edit Data**.
    text: Choose **Chart Tools → Design → Edit Data**.
  - name: Confirm that the Excel‑style data grid appears and that you can change values.
    text: Confirm that the Excel‑style data grid appears and that you can change values.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Excel 파일을 SVG와 PowerPoint로 변환할 때 SVG에 글꼴을 포함하는 방법
url: /ko/net/converting-excel-files-to-other-formats/how-to-embed-fonts-in-svg-when-converting-excel-files-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel 파일을 SVG 및 PowerPoint 로 변환할 때 SVG에 폰트 포함하는 방법  

Excel 통합 문서를 변환하면서 **SVG에 폰트를 포함**해야 하는 경우, 이 가이드에서 정확한 방법을 알려드립니다. 또한 **Excel 차트를 PowerPoint로 내보내는 방법**, **XLSX를 SVG로 변환** 및 **XLSX를 PPTX로 변환**하여 편집 가능한 차트를 만드는 방법도 배울 수 있습니다.  

프로그래밍 방식으로 Excel 데이터를 다루면 동일한 시각적 콘텐츠를 다양한 파일 형식으로 이동해야 할 때가 많습니다. PowerPoint에서 차트를 수동으로 다시 만들거나 SVG에서 폰트를 다시 적용하는 것은 오류가 발생하기 쉽고 시간이 많이 소요됩니다. 이 튜토리얼을 마치면 재사용 가능한 단일 C# 스니펫을 얻게 됩니다.

* 워크북을 폰트와 폰트‑variation 선택기가 포함된 SVG 파일로 저장합니다.  
* 동일한 워크북을 차트가 편집 가능한 상태로 유지되는 PPTX 파일로 내보냅니다.  

필수 조건은 최신 버전의 **Aspose.Cells for .NET** (2024‑x 이상)과 Visual Studio 2022와 같은 .NET 개발 환경입니다.

---

## 필요 사항  

* .NET 6.0 이상 (코드는 .NET Framework 4.8에서도 작동합니다).  
* Aspose.Cells for .NET NuGet 패키지 (`Install-Package Aspose.Cells`).  
* 하나 이상의 차트가 포함된 Excel 파일 (`input.xlsx`).  
* 출력 디렉터리에 대한 쓰기 권한.  

---

## XLSX를 SVG로 변환하면서 SVG에 폰트 포함하기  

폰트를 포함하면 대상 시스템에 원본 글꼴이 없더라도 SVG가 모든 장치에서 올바르게 렌더링됩니다. `SvgSaveOptions` 클래스는 이를 가능하게 하는 두 가지 플래그인 `EmbedFonts`와 `FontVariationSelectors`를 제공합니다.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Load the workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// OPTIONAL: Use WRAPCOLS to reshape data before export (demonstrates a formula)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)"; // 2 columns per wrap
sheet.Calculate(); // Force calculation so the formula result appears

// Configure SVG options to embed fonts
SvgSaveOptions svgOptions = new SvgSaveOptions
{
    EmbedFonts = true,                // embed fonts in the SVG
    FontVariationSelectors = true    // include variation selectors for better Unicode handling
};

// Save the workbook as an SVG file
string svgPath = @"YOUR_DIRECTORY\WithFonts.svg";
workbook.Save(svgPath, svgOptions);
```

**왜 이렇게 동작할까요:**  
* `EmbedFonts = true`는 폰트 파일을 SVG의 `<defs>` 섹션에 복사하여 외부 종속성을 없앱니다.  
* `FontVariationSelectors = true`는 OpenType 기능을 지원하는 폰트에 필요한 선택자를 추가하여 합자와 같은 글리프 변형을 보존합니다.  

**예상 결과:** 모던 브라우저에서 `WithFonts.svg`를 열면 차트나 셀 내부의 텍스트가 Excel에서 사용된 정확한 글꼴로 표시되며, 해당 글꼴이 설치되지 않은 컴퓨터에서도 동일하게 보입니다.

---

## 편집 가능한 차트와 함께 Excel 차트를 PowerPoint로 내보내기  

PowerPoint 슬라이드에 차트를 삽입하면서도 수신자가 차트 데이터를 편집할 수 있도록 하려면, Aspose.Cells의 `PptxSaveOptions`에서 `ExportEditableChart` 플래그를 제공합니다.

```csharp
// Configure PPTX options to keep charts editable after export
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableChart = true   // allow chart editing in PowerPoint
};

// Save the same workbook as a PPTX file
string pptxPath = @"YOUR_DIRECTORY\EditableChart.pptx";
workbook.Save(pptxPath, pptxOptions);
```

**왜 중요한가:**  
`ExportEditableChart`를 `true`로 설정하면 차트가 정적 이미지가 아니라 Office Open XML 차트 객체로 저장됩니다. PowerPoint에서 `EditableChart.pptx`를 열면 차트를 오른쪽 클릭 → **Edit Data**를 선택해 시리즈를 원본 PowerPoint 차트처럼 수정할 수 있습니다.

**검증 단계:**  

1. PowerPoint에서 `EditableChart.pptx`를 엽니다.  
2. 차트가 포함된 슬라이드를 찾습니다.  
3. **Chart Tools → Design → Edit Data**를 선택합니다.  
4. Excel 스타일의 데이터 그리드가 나타나고 값을 변경할 수 있는지 확인합니다.

---

## XLSX를 SVG로 변환 – 전체 워크플로우 요약  

아래는 로드, 선택적 데이터 조작 및 SVG 저장을 결합한 간결한 버전입니다. SVG 출력만 필요할 때 사용하세요.

```csharp
public void ConvertXlsxToSvg(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Example: apply a formula to demonstrate cell calculations
    Worksheet ws = wb.Worksheets[0];
    ws.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
    ws.Calculate();

    SvgSaveOptions opts = new SvgSaveOptions
    {
        EmbedFonts = true,
        FontVariationSelectors = true
    };

    wb.Save(outputPath, opts);
}
```

다음과 같이 메서드를 호출합니다:

```csharp
ConvertXlsxToSvg(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.svg");
```

**예외 상황 팁:** 워크북에 서버에 설치되지 않은 사용자 정의 폰트가 포함된 경우, `Save` 호출 전에 수동으로 폰트를 포함하세요. `FontInfoCollection`을 사용해 `SvgSaveOptions`의 `CustomFonts` 속성에 폰트 파일을 추가할 수 있습니다(새로운 Aspose.Cells 릴리스에서 제공).

---

## XLSX를 PPTX로 변환 – 차트 편집 가능성 유지  

다음 헬퍼 메서드는 차트가 편집 가능한 상태를 유지하면서 **XLSX를 PPTX로 변환**하는 경로를 보여줍니다.

```csharp
public void ConvertXlsxToPptx(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Ensure any chart you want to keep editable is on the first worksheet
    // (Aspose.Cells exports only the first worksheet by default for PPTX)
    PptxSaveOptions opts = new PptxSaveOptions
    {
        ExportEditableChart = true
    };

    wb.Save(outputPath, opts);
}
```

사용법:

```csharp
ConvertXlsxToPptx(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.pptx");
```

**자주 묻는 질문:** *워크북에 차트가 있는 여러 워크시트가 있는 경우는 어떻게 하나요?*  

**답변:** Aspose.Cells는 기본적으로 첫 번째 워크시트를 내보냅니다. 추가 시트를 포함하려면 `workbook.Worksheets`를 반복하면서 각 차트를 새 슬라이드에 복사하고, Aspose.Slides의 `Presentation` 객체를 사용해 각 슬라이드를 개별적으로 저장합니다. 이 고급 시나리오는 기본 “워크북을 SVG로 저장” 및 “Excel 차트를 PowerPoint로 내보내기” 흐름을 넘어서는 것이지만, 핵심 플래그는 동일합니다.

---

## 실용적인 팁 및 함정  

* **Performance:** 폰트를 포함하면 SVG 파일 크기가 증가합니다. 크기가 문제라면 `EmbedFonts = false`로 설정하고 웹 안전 폰트를 사용하세요.  
* **Font licensing:** 사용 중인 폰트를 포함할 권한이 있는지 확인하세요; 일부 상용 폰트는 포함을 제한합니다.  
* **Chart compatibility:** 편집 가능한 차트는 PPTX 내부의 `chart.xml` 파트로 저장됩니다. 매우 복잡한 차트(예: 3‑D 차트 또는 복합 차트)는 PowerPoint에서 편집할 때 일부 스타일이 손실될 수 있습니다. 필요한 가장 일반적인 차트 유형을 테스트하세요.  
* **Version mismatches:** `ExportEditableChart` 플래그는 Aspose.Cells 20.10 이상이 필요합니다. 이전 버전을 사용하면 자동으로 래스터 이미지로 대체됩니다.  
* **Thread safety:** Workbook 객체는 스레드에 안전하지 않습니다. 웹 서비스 시나리오에서는 요청당 새로운 `Workbook` 인스턴스를 생성하세요.  

---

## 전체 엔드‑투‑엔드 예제  

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class ExcelExportDemo
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputFile = @"YOUR_DIRECTORY\input.xlsx";
        string svgFile   = @"YOUR_DIRECTORY\WithFonts.svg";
        string pptxFile  = @"YOUR_DIRECTORY\EditableChart.pptx";

        // 1. Load workbook
        Workbook workbook = new Workbook(inputFile);

        // 2. Optional: reshape data using WRAPCOLS
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
        sheet.Calculate();

        // 3. Save as SVG with embedded fonts
        SvgSaveOptions svgOpts = new SvgSaveOptions
        {
            EmbedFonts = true,
            FontVariationSelectors = true
        };
        workbook.Save(svgFile, svgOpts);
        Console.WriteLine($"SVG saved with embedded fonts to: {svgFile}");

        // 4. Save as PPTX with editable chart
        PptxSaveOptions pptxOpts = new PptxSaveOptions
        {
            ExportEditableChart = true
        };
        workbook.Save(pptxFile, pptxOpts);
        Console.WriteLine($"PPTX saved with editable chart to: {pptxFile}");
    }
}
```

이 프로그램을 실행하면 두 개의 파일이 생성됩니다:

* **WithFonts.svg** – Excel 뷰와 동일하게 렌더링되는 SVG이며, 폰트가 포함됩니다.  
* **EditableChart.pptx** – 차트를 직접 편집할 수 있는 PowerPoint 프레젠테이션.

---

## 결론  

이제 **XLSX를 SVG로 변환할 때 SVG에 폰트를 포함**하는 방법과 차트를 편집 가능한 상태로 유지하면서 **Excel 차트를 PowerPoint로 내보내는** 방법을 알게 되었습니다. 동일한 코드는 **워크북을 SVG로 저장**하고 **XLSX를 PPTX로 변환**하는 간단한 방법도 보여줍니다.

여기서부터는 다음과 같은 추가 주제를 탐색할 수 있습니다:

* 프로그래밍 방식으로 사용자 정의 폰트 추가 (`svgOptions.CustomFonts`).  
* 백그라운드 서비스에서 여러 워크북을 일괄 처리.  
* Aspose.Slides를 사용해 여러 Excel 차트를 결합한 다중 슬라이드 PPTX 파일 만들기.

옵션을 실험하고 스니펫을 프로젝트에 맞게 조정하여 수동 후처리 없이도 안정적인 Excel‑to‑SVG/PPTX 변환을 즐기세요. 코딩 즐겁게!

## 다음에 배워야 할 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료에는 전체 코드 예제와 단계별 설명이 포함되어 있어 추가 API 기능을 숙달하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [Aspose.Cells for .NET을 사용하여 Excel 차트를 SVG로 변환하는 방법 (단계별 가이드)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Excel 차트를 SVG로 변환 Aspose Cells .NET](/cells/german/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Excel 차트를 SVG로 변환 Aspose Cells .NET](/cells/french/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}