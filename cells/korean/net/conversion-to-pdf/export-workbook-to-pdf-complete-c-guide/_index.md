---
category: general
date: 2026-02-26
description: 워크북을 PDF로 내보내면서 글꼴을 포함하고, C#에서 차트를 PowerPoint로 내보냅니다. 피벗 테이블 워크시트를 복사하고
  워크북을 PPTX 파일로 저장하는 방법을 배웁니다.
draft: false
keywords:
- export workbook to pdf
- export charts to powerpoint
- copy pivot table worksheet
- embed fonts pdf export
- save workbook as pptx
language: ko
og_description: 워크북을 임베디드 폰트와 함께 PDF로 내보내고, 차트를 C#에서 PowerPoint로 내보내세요. 피벗 테이블을 복사하고
  PPTX로 저장하는 단계별 가이드를 따라보세요.
og_title: 워크북을 PDF로 내보내기 – 완전한 C# 가이드
tags:
- Aspose.Cells
- Aspose.Slides
- C#
- Reporting
title: 워크북을 PDF로 내보내기 – 완전한 C# 가이드
url: /ko/net/conversion-to-pdf/export-workbook-to-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Workbook to PDF – Complete C# Guide

Export workbook to PDF는 Excel이 설치되지 않은 이해관계자와 보고서를 공유해야 할 때 흔히 필요한 기능입니다. 이 튜토리얼에서는 **차트를 PowerPoint로 내보내는 방법**, **피벗 테이블 워크시트를 복사하는 방법**, 그리고 PDF가 화면 디자인과 정확히 동일하게 보이도록 폰트를 포함시키는 방법도 함께 보여드립니다.  

PDF가 원본 레이아웃을 잃어버리거나 PowerPoint 슬라이드에서 도형이 사라지는 경우가 왜 발생하는지 궁금하셨나요? 대부분은 내보내기 과정에서 옵션이 누락되었기 때문입니다. 이 가이드를 끝까지 따라오시면 이러한 문제점을 한 번에 해결해 주는 재사용 가능한 C# 메서드를 얻을 수 있습니다—더 이상 수동 복사·붙여넣기나 내보내기 설정을 일일이 조정할 필요가 없습니다.

## What You’ll Learn

- 워크북을 생성하고 Smart Marker 식을 추가한 뒤 처리하는 방법.  
- 데이터 소스를 깨뜨리지 않고 **피벗 테이블 워크시트를 복사**하는 방법.  
- **차트, 도형, 텍스트 상자를 PowerPoint 프레젠테이션으로 내보내**면서 편집 가능하게 유지하는 방법.  
- PDF 내보내기 시 **표준 폰트를 포함**시켜 어떤 컴퓨터에서도 동일하게 렌더링되는 방법.  
- `save workbook as pptx` 방식을 사용해 **워크북을 PPTX로 저장**하는 방법.  

이 모든 작업은 최신 Aspose.Cells 및 Aspose.Slides .NET 라이브러리(작성 시점 버전 23.11)와 함께 동작합니다. 외부 도구나 사후 처리 스크립트가 필요 없으며 순수 C#만으로 구현됩니다.

> **Pro tip:** 프로젝트에 이미 Aspose를 사용하고 있다면 코드를 그대로 복사해 넣으면 되고, 그렇지 않은 경우 먼저 NuGet 패키지 `Aspose.Cells`와 `Aspose.Slides`를 추가하세요.

## Prerequisites

- .NET 6.0 이상(.NET Framework 4.7.2에서도 동작).  
- Visual Studio 2022(또는 선호하는 IDE).  
- NuGet을 통해 설치한 Aspose.Cells .NET 및 Aspose.Slides .NET.  
- C#와 Excel 개념(특히 Smart Markers와 PivotTables)에 대한 기본 지식.

---

![Export workbook to PDF diagram](export-workbook-to-pdf.png "Export workbook to PDF workflow showing PDF and PPTX outputs")

## Export Workbook to PDF – Step‑by‑Step Implementation

아래는 전체 실행 가능한 예제입니다. 워크북을 만들고, Smart Marker 식을 삽입하고, 이를 처리한 뒤 피벗 테이블 범위를 복사하고, 마지막으로 PDF와 PowerPoint 파일을 각각 저장합니다.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides.Export;

namespace ReportExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Build the workbook and add Smart Markers
            // -------------------------------------------------
            var reportWorkbook = new Workbook();
            Worksheet dataSheet = reportWorkbook.Worksheets[0];

            // Header with a variable department name
            dataSheet.Cells["A1"].PutValue("Report for ${$dept=Department}");

            // Conditional text based on department
            dataSheet.Cells["A2"].PutValue("${if $dept == \"Sales\"}Sales Summary${else}Other Summary${/if}");

            // Table header for orders – this will be repeated for each order
            dataSheet.Cells["A5:D5"].PutValue("${Orders.Product}|${Orders.Quantity}|${Orders.Price}");

            // -------------------------------------------------
            // Step 2: Process Smart Markers and name the detail sheet
            // -------------------------------------------------
            reportWorkbook.SmartMarkerProcessor.Options.DetailSheetNewName = "Orders_${$dept}";
            reportWorkbook.SmartMarkerProcessor.Process();

            // -------------------------------------------------
            // Step 3: Copy the range that contains the pivot table
            // -------------------------------------------------
            // Assume the pivot table lives in A1:G30 on the original sheet
            Range sourceRange = dataSheet.Cells.CreateRange("A1", "G30");
            Worksheet copySheet = reportWorkbook.Worksheets.Add("Copy");
            sourceRange.Copy(copySheet.Cells["A1"]);   // Pivot table is duplicated intact

            // -------------------------------------------------
            // Step 4: Export to PowerPoint (keep charts, shapes, text boxes)
            // -------------------------------------------------
            var pptOptions = new PresentationOptions
            {
                ExportCharts = true,
                ExportShapes = true,
                ExportTextBoxes = true
            };
            string pptPath = @"C:\Temp\FinalPresentation.pptx";
            reportWorkbook.Save(pptPath, SaveFormat.Pptx, pptOptions);

            // -------------------------------------------------
            // Step 5: Export to PDF and embed standard fonts
            // -------------------------------------------------
            var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
            string pdfPath = @"C:\Temp\FinalReport.pdf";
            reportWorkbook.Save(pdfPath, pdfOptions);

            Console.WriteLine("Export completed:");
            Console.WriteLine($" • PDF saved to {pdfPath}");
            Console.WriteLine($" • PowerPoint saved to {pptPath}");
        }
    }
}
```

### Why This Works

1. **Smart Marker processing**을 사용하면 JSON, DataTable 등 어떤 데이터 소스에서도 루프를 작성하지 않고 워크북을 채울 수 있습니다.  
2. **DetailSheetNewName**은 부서별로 별도의 시트를 생성해 부서별 탭을 깔끔하게 정리합니다.  
3. **Copying the range** (`sourceRange.Copy`)는 피벗 테이블 *캐시*까지 복제하므로 복사된 시트가 원본과 동일하게 동작합니다.  
4. **PresentationOptions**에 `ExportCharts`, `ExportShapes`, `ExportTextBoxes`를 지정하면 Aspose가 해당 객체들을 네이티브 PowerPoint 요소로 렌더링해 편집 가능성을 유지합니다.  
5. **PdfSaveOptions.EmbedStandardFonts**는 원본 폰트가 설치되지 않은 머신에서도 PDF가 동일하게 보이도록 가장 일반적인 폰트(Arial, Times New Roman 등)를 PDF 스트림에 포함시킵니다.

그 결과 `FinalReport.pdf`와 `FinalPresentation.pptx` 두 파일이 생성되며, 이메일, 보관, 혹은 어떤 뷰어에서도 품질 저하 없이 사용할 수 있습니다.

## Export Charts to PowerPoint (Save Workbook as PPTX)

보고서에 차트가 포함되어 있다면 PowerPoint에서 편집 가능하도록 내보내고 싶을 것입니다. `PresentationOptions` 클래스가 핵심입니다. 차트 내보내기 부분만 집중한 코드 스니펫은 다음과 같습니다:

```csharp
// Assuming reportWorkbook already contains charts
var pptExportOptions = new PresentationOptions
{
    ExportCharts = true,      // Convert Excel charts to PowerPoint chart objects
    ExportShapes = false,    // Skip shapes if you don’t need them
    ExportTextBoxes = true   // Keep any text boxes editable
};

string pptFile = @"C:\Temp\ChartsOnly.pptx";
reportWorkbook.Save(pptFile, SaveFormat.Pptx, pptExportOptions);
```

**What happens under the hood?** Aspose는 각 Excel 차트를 네이티브 PowerPoint 차트로 변환하면서 시리즈, 축 제목, 서식 등을 그대로 유지합니다. 정적인 이미지로 내보내는 것보다 훨씬 나은 접근 방식이며, 청중이 나중에 데이터 포인트를 조정할 수 있습니다.

## Copy Pivot Table Worksheet Without Losing Data

피벗 테이블은 숨겨진 캐시를 사용하기 때문에 내보내기 시 가장 까다로운 요소 중 하나입니다. 간단한 `Copy` 메서드가 작동하는 이유는 Aspose가 **보이는 범위와** 그 아래에 있는 캐시 객체를 모두 복제하기 때문입니다.

```csharp
// Copy the whole sheet (including pivot table) to a new workbook
Workbook clone = new Workbook();
reportWorkbook.Worksheets[0].CopyTo(clone.Worksheets[0]);
clone.Save(@"C:\Temp\PivotCopy.xlsx", SaveFormat.Xlsx);
```

> **Note:** 같은 워크북 내에서 새 시트에 피벗 테이블만 필요하다면, 앞서 소개한 `sourceRange.Copy` 방식이 더 가볍고 전체 워크북을 새로 만들 필요가 없습니다.

## Embed Fonts for PDF Export – Why It Matters

원본 폰트가 없는 컴퓨터에서 PDF를 열면 텍스트가 이동하거나 줄 바꿈이 바뀌고, 심지어 문자가 사라질 수도 있습니다. `EmbedStandardFonts = true`를 설정하면 Aspose가 가장 일반적인 폰트를 PDF 스트림에 직접 포함시켜 이러한 문제를 방지합니다.

사용자 정의 폰트를 사용한다면 `PdfSaveOptions.FontEmbeddingMode = FontEmbeddingMode.EmbedAll`로 전환하세요. 예시는 다음과 같습니다:

```csharp
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    FontEmbeddingMode = FontEmbeddingMode.EmbedAll   // For custom fonts
};
reportWorkbook.Save(@"C:\Temp\CustomFontReport.pdf", pdfOpts);
```

이제 모든 수신자는 디자인한 레이아웃과 정확히 동일한 모습을 보게 됩니다—예상치 못한 변형이 없습니다.

## Full Working Example Recap

전체 프로그램을 한 번에 정리하면 다음과 같은 흐름을 가집니다:

1. **Creates** a workbook with Smart Marker placeholders.  
2. **Processes** the markers, generating a detail sheet named after the department.  
3. **Copies** a range that contains a pivot table to a new worksheet, preserving its functionality.  
4. **Exports** the workbook to PowerPoint, keeping charts, shapes, and text boxes editable.  
5. **Exports** the same workbook to PDF while embedding standard fonts for reliable rendering.

프로그램을 실행하고 생성된 파일을 열어 보면:

- **PDF**: 선명한 테이블, 포함된 폰트, Excel 소스와 동일한 시각적 스타일.  
- **PowerPoint**: 차트를 오른쪽 클릭 → *Edit Data* 로 편집할 수 있고, 도형도 완전히 조작 가능.

---

## Frequently Asked Questions (FAQ)

**Q: Does this work with .NET Core?**  
Yes—Aspose.Cells and Aspose.Slides are cross‑platform. Just target .NET 6 or later and the same code runs on Windows, Linux, or macOS.

**Q: What if I need to export only a subset of sheets?**  
Use `Workbook.Save` with `SaveOptions` that let you specify `SheetNames`. Example: `new PresentationOptions { SheetNames = new[] { "Copy" } }`.

**Q: Can I encrypt the PDF?**  
Absolutely. Set `PdfSaveOptions.EncryptionDetails` with a password before calling `Save`.

**Q: My pivot table uses an external data source—will copying break the link?**  
The copy operation includes the cache, not the external connection. The pivot will still work offline, but it won’t refresh against the original source. If you need live refresh, export the source data together with the workbook.

---

## Next Steps & Related Topics

- **Dynamic Data Sources** – Learn how to feed JSON or a DataTable into Smart Markers for real‑time reporting.  
- **Advanced PDF Styling** – Explore `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}