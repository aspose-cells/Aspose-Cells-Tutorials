---
category: general
date: 2026-06-24
description: C#에서 Aspose.Cells를 사용하여 PDF에 글꼴을 포함합니다. Excel을 PDF로 저장하는 방법, Excel을 HTML로
  내보내는 방법, Aspose로 xlsx를 PDF로 변환하는 방법, 그리고 피벗 테이블에서 행을 복제하는 방법을 배워보세요.
draft: false
keywords:
- embed fonts pdf
- save excel as pdf
- export excel to html
- xlsx to pdf aspose
- duplicate rows pivot
language: ko
og_description: C#에서 Aspose.Cells를 사용해 PDF에 글꼴을 포함합니다. 이 튜토리얼은 Excel을 PDF로 저장하고, Excel을
  HTML로 내보내는 방법 등을 단계별로 보여줍니다.
og_title: Aspose.Cells로 PDF에 폰트 삽입 – 완전 C# 가이드
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Embed fonts PDF using Aspose.Cells in C#. Learn how to save Excel as
    PDF, export Excel to HTML, convert xlsx to PDF with Aspose, and duplicate rows
    pivot.
  headline: Embed fonts PDF with Aspose.Cells – Complete C# Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
title: Aspose.Cells로 PDF에 폰트 포함하기 – 완전 C# 가이드
url: /ko/net/xps-and-pdf-operations/embed-fonts-pdf-with-aspose-cells-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells로 PDF에 폰트 포함 – 완전 C# 가이드

Excel 워크북을 Aspose.Cells로 변환할 때 **PDF에 폰트 포함** 방법이 궁금하셨나요? 당신만 그런 것이 아닙니다—많은 개발자들이 원본 폰트가 설치되지 않은 컴퓨터에서 생성된 PDF가 잘못 표시되는 문제에 부딪힙니다.  

이 가이드에서는 **PDF에 폰트 포함**은 물론 **Excel을 PDF로 저장**, **Excel을 HTML로 내보내기**, **xlsx를 Aspose로 PDF로 변환**, 그리고 피벗 테이블을 깨뜨리지 않고 **행 복제 피벗**까지 수행하는 실제 예제를 단계별로 살펴보겠습니다. 많은 내용처럼 보이시나요? 걱정 마세요—한 단계씩 차근차근 설명합니다.

## 배울 내용

- 피벗 테이블이 포함된 행을 복사하면서 피벗을 그대로 유지하는 방법.  
- 각 주문마다 상세 시트를 반복 생성하는 스마트‑마커 삽입 방법.  
- **PDF에 폰트 포함**, 차트를 편집 가능한 PPTX로 내보내기, 그리고 **Excel을 HTML로 내보낼 때** 고정 창을 유지하기 위한 정확한 설정.  
- 폰트 누락이나 손상된 OLE 객체와 같은 일반적인 문제를 해결하기 위한 팁.  

**Prerequisites:** .NET 6+ (or .NET Framework 4.6+), Aspose.Cells for .NET installed, and a basic C# development environment (Visual Studio, Rider, or VS Code). No extra NuGet packages beyond Aspose.Cells are required.

---

## Embed fonts PDF – 단계별 프로세스

아래는 전체 실행 가능한 코드입니다. 각 섹션에 주석을 달아 왜 이렇게 하는지 정확히 확인할 수 있습니다.

```csharp
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Pivot;
using Aspose.Cells.SmartMarker;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the workbook that contains a pivot table and a shape
        // -------------------------------------------------
        var workbook = new Workbook("YOUR_DIRECTORY/template.xlsx");

        // -------------------------------------------------
        // Step 2: Duplicate the rows that include the pivot table (keeps the pivot intact)
        // -------------------------------------------------
        // The CopyRows method copies rows 0‑29 (30 rows) from the source worksheet
        // to the same worksheet, effectively duplicating the pivot area.
        workbook.Worksheets[0].Cells.CopyRows(0, 0, 30);

        // -------------------------------------------------
        // Step 3: Insert a smart‑marker to repeat a detail sheet for each order
        // -------------------------------------------------
        var orders = new[]
        {
            new { Id = 101, Items = new[] { "Pen", "Paper" } },
            new { Id = 102, Items = new[] { "Book" } }
        };
        var smartMarkerOptions = new SmartMarkerOptions { DetailSheetNewName = "OrderDetail" };
        workbook.Worksheets[0].SmartMarkerProcessing(new { Orders = orders }, smartMarkerOptions);

        // -------------------------------------------------
        // Step 4: Save the workbook as a PPTX file with editable charts, OLE objects, and text boxes
        // -------------------------------------------------
        var pptxOptions = new PptxSaveOptions
        {
            ExportChartsAsEditable = true,
            ExportOleObjects = true,
            ExportTextBoxesAsEditable = true
        };
        workbook.Save("YOUR_DIRECTORY/result.pptx", pptxOptions);

        // -------------------------------------------------
        // Step 5: Save the same workbook as a PDF while embedding standard fonts
        // -------------------------------------------------
        // This is where we actually **embed fonts PDF**.
        var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
        workbook.Save("YOUR_DIRECTORY/result.pdf", pdfOptions);

        // -------------------------------------------------
        // Step 6: Save the workbook as HTML, preserving frozen panes and embedding all fonts
        // -------------------------------------------------
        // The HTML export respects the original layout and keeps the fonts inside the file.
        var htmlOptions = new HtmlSaveOptions
        {
            PreserveFreezePanes = true,
            EmbedAllFonts = true
        };
        workbook.Save("YOUR_DIRECTORY/result.html", htmlOptions);
    }
}
```

### 왜 이렇게 동작하나요

- **CopyRows**는 피벗 테이블이 있는 행을 복제하므로 원본 피벗이 소스 데이터에 계속 연결됩니다. 이는 **duplicate rows pivot** 요구 사항을 충족합니다.  
- **SmartMarkerProcessing**은 각 주문마다 새로운 워크시트를 생성해 상세 시트 생성을 자동화합니다.  
- **PdfSaveOptions.EmbedStandardFonts = true**는 Aspose.Cells에게 폰트를 PDF 파일에 직접 포함하도록 지시합니다. 이것이 **embed fonts pdf**의 핵심이며, 이 플래그가 없으면 PDF가 시스템 폰트로 대체되어 다른 컴퓨터에서 레이아웃이 깨집니다.  
- `EmbedAllFonts`와 `PreserveFreezePanes`가 설정된 **HtmlSaveOptions**는 **Excel을 HTML로 내보낼 때** 시각적 일관성을 원본 워크북과 동일하게 유지합니다.  

#### 예상 출력

- `result.pdf` – 사용된 모든 폰트가 포함된 PDF; 어느 컴퓨터에서 열어도 텍스트가 원본과 동일하게 보입니다.  
- `result.pptx` – 편집 가능한 차트와 OLE 객체가 포함된 PowerPoint 파일.  
- `result.html` – HTML 폴더(`result.html` + `result_files`)로, 브라우저에서 워크북을 렌더링하면서 고정 창이 그대로 유지됩니다.  

---

## Save Excel as PDF with Aspose.Cells

목표가 **Excel을 PDF로 저장**하는 것뿐이라면, 불필요한 단계를 생략하고 PDF 옵션에만 집중하면 됩니다:

```csharp
var workbook = new Workbook("template.xlsx");

// Minimal PDF conversion – embed fonts for portability
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,   // crucial for embed fonts pdf
    Compliance = PdfCompliance.PdfA1b // optional: make the PDF archival‑friendly
};

workbook.Save("output.pdf", pdfOpts);
```

**Pro tip:** PDF/A 규격을 목표로 할 경우, Aspose가 자동으로 모든 폰트를 포함하므로 장기 보관 시 추가적인 안전성을 확보할 수 있습니다.

---

## Export Excel to HTML while Preserving Layout

HTML로 내보낼 때 원본 시트의 모양과 느낌이 손실되기 쉽습니다, 특히 고정 창이 있는 경우에 더욱 그렇습니다. 아래 스니펫은 필요한 정확한 설정을 보여줍니다:

```csharp
var wb = new Workbook("template.xlsx");

var htmlOpts = new HtmlSaveOptions
{
    PreserveFreezePanes = true, // keeps the top rows/columns locked
    EmbedAllFonts = true,       // embeds fonts so the page looks the same everywhere
    ExportActiveWorksheetOnly = true,
    ExportCellValueAsString = true
};

wb.Save("output.html", htmlOpts);
```

`EmbedAllFonts`를 설정했기 때문에 생성된 HTML에는 Base‑64 인코딩된 폰트 데이터가 포함되어, 외부 CSS 파일 없이도 **export excel to html** 요구 사항을 만족합니다.

---

## Convert Xlsx to PDF using Aspose.Cells

검색 시 “**xlsx to pdf aspose**”라는 용어가 종종 등장합니다. 아래 코드는 정확한 변환 파이프라인을 보여주며 몇 가지 추가적인 편의 기능도 포함합니다:

```csharp
var wb = new Workbook("template.xlsx");

// Optional: set page layout before conversion
wb.Worksheets[0].PageSetup.Orientation = PageOrientation.Landscape;
wb.Worksheets[0].PageSetup.FitToPagesWide = 1;
wb.Worksheets[0].PageSetup.FitToPagesTall = 0;

// PDF options – embed fonts and keep hyperlinks intact
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    ExportHyperlinks = true,
    OnePagePerSheet = false
};

wb.Save("converted.pdf", pdfOpts);
```

**페이지 설정을 왜 해야 할까요?** 이를 생략하면 기본 PDF가 열이나 행을 잘라낼 수 있습니다. 레이아웃을 먼저 조정하면 최종 PDF가 Excel에서 보는 모습과 일치합니다.

---

## Duplicate Rows Pivot – 피벗 유지하기

일반적인 난관은 피벗 테이블이 포함된 행을 복사하려 할 때 피벗이 데이터 소스와의 연결을 잃는 것입니다. 앞서 사용한 `CopyRows` 메서드가 이 작업을 대신해 줍니다:

```csharp
// Duplicate the first 30 rows (adjust as needed)
workbook.Worksheets[0].Cells.CopyRows(sourceRow: 0, destinationRow: 0, totalRows: 30);
```

- **sourceRow** – 복사하려는 범위의 첫 번째 행.  
- **destinationRow** – 복사본을 배치할 위치(같은 시트, 같은 시작 인덱스로 효과적으로 복제).  
- **totalRows** – 복사할 행 수.  

피벗의 캐시가 워크시트에 존재하기 때문에 행을 복사해도 피벗이 **깨지지** 않습니다. 이는 **duplicate rows pivot** 키워드를 만족하면서 워크북을 깔끔하게 유지합니다.

---

## Full Working Example Recap

모든 내용을 하나로 합치면, 바로 콘솔 앱에 넣어 실행할 수 있는 완전한 프로그램이 됩니다:



## 다음에 배워야 할 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 주제를 다룹니다. 각 리소스는 단계별 설명과 완전한 코드 예제를 포함하고 있어 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용하는 데 도움이 됩니다.

- [Aspose.Cells for .NET를 사용하여 사용자 지정 폰트로 Excel 워크북을 PDF로 저장](/cells/english/net/workbook-operations/save-excel-workbook-pdf-custom-fonts-aspose-cells-net/)
- [Aspose.Cells for .NET를 사용하여 Excel 차트를 PDF로 내보내는 방법: 단계별 가이드](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Aspose.Cells for .NET를 사용하여 Excel 슬라이서를 PDF로 내보내는 방법](/cells/english/net/workbook-operations/export-excel-slicers-to-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}