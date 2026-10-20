---
category: general
date: 2026-10-20
description: Aspose.Cells에서 wrapcols를 사용하는 방법, HTML에 글꼴을 포함하는 방법, 그리고 완전한 C# 예제로 Excel을
  HTML로 저장하는 방법을 배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- embed fonts in html
- save excel as html
- convert workbook to html
- use wrapcols function
language: ko
lastmod: 2026-10-20
og_description: Aspose.Cells에서 wrapcols를 사용하는 방법, HTML에 글꼴을 포함하는 방법, 그리고 개발자를 위한 명확한
  C# 단계별 가이드를 통해 워크북을 HTML로 변환하는 방법.
og_image_alt: Screenshot of an Excel workbook saved as HTML with embedded fonts using
  Aspose.Cells
og_title: Excel을 HTML로 내보낼 때 wrapcols와 폰트 삽입 방법
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to use wrapcols in Aspose.Cells, embed fonts in HTML, and
    save Excel as HTML with a complete C# example.
  headline: How to use wrapcols and embed fonts saving Excel to HTML
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel to HTML
- Smart Markers
title: Excel을 HTML로 저장할 때 wrapcols와 글꼴 삽입을 사용하는 방법
url: /ko/net/exporting-excel-to-html-with-advanced-options/how-to-use-wrapcols-and-embed-fonts-saving-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# wrapcols 사용 및 폰트 임베드로 Excel을 HTML로 저장하는 방법

Aspose.Cells 수식에서 **wrapcols 사용 방법**이 필요하다면, 이 가이드는 정확한 단계들을 보여줍니다. 또한 **HTML에 폰트 임베드**와 **Excel을 HTML로 저장**하는 방법을 배워 브라우저마다 동일한 출력 결과를 얻을 수 있습니다.  

이 튜토리얼은 세 가지 실용적인 시나리오를 다룹니다: `WRAPCOLS` 함수 사용, 임베드된 폰트와 함께 워크북 내보내기, Smart Markers를 이용한 마스터‑디테일 보고서 생성. 마지막에는 이러한 모든 기능을 시연하는 단일 C# 프로그램을 얻게 됩니다.

## Prerequisites

시작하기 전에 다음이 준비되어 있는지 확인하세요:

* .NET 6.0 (or later) installed.
* Aspose.Cells for .NET added to your project (`dotnet add package Aspose.Cells`).
* Basic familiarity with C# and Excel formulas.

추가 서드‑파티 라이브러리는 필요하지 않습니다; Aspose.Cells가 HTML 변환 및 폰트 임베드를 내부적으로 처리합니다.

## Step 1: Demonstrate the **how to use wrapcols** function in a formula

`WRAPCOLS` 함수는 1차원 범위를 2차원 배열로 나누며, 먼저 열을 채웁니다. 이는 보고서나 차트를 위해 데이터를 재구성해야 할 때 유용합니다.

```csharp
using Aspose.Cells;
using System;

class WrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Populate a vertical range A1:A3
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // Apply WRAPCOLS(A1:A3, 2) – this creates a 2‑column array {1,2}
        sheet.Cells["B1"].Formula = "=WRAPCOLS(A1:A3, 2)";

        // Force calculation so the formula result is materialized
        workbook.CalculateFormula();

        // Output the result to verify the function works
        Console.WriteLine("Result of WRAPCOLS: " + sheet.Cells["B1"].Value);
        // Expected output: Result of WRAPCOLS: 1
    }
}
```

**Why this works:**  
`WRAPCOLS`는 두 개의 인수를 받습니다 – 원본 범위와 열 개수. 함수는 배열을 열 단위로 채우며, 초과값(예시의 `3`)은 버립니다. 결과는 대상 범위(`B1`)의 좌측 상단 셀에 나타나며, 전체 배열이 필요하면 범위를 수동으로 확장할 수 있습니다.

> **Pro tip:** After setting the formula, call `workbook.CalculateFormula()` to ensure the result is up‑to‑date before reading cell values.

## Step 2: **Convert workbook to HTML** and **embed fonts in html**

Excel 파일을 HTML로 내보낼 때, 브라우저 기본 폰트로 대체되는 경우가 많아 시각적 레이아웃이 깨질 수 있습니다. Aspose.Cells를 사용하면 워크북에 사용된 정확한 폰트를 HTML 파일에 직접 임베드할 수 있습니다.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for HtmlSaveOptions
using System;

class HtmlExportDemo
{
    static void Main()
    {
        // Re‑use the workbook from the previous step
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue("Hello");
        sheet.Cells["A2"].PutValue("World");

        // Configure HTML save options
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            // Embedding fonts ensures the output looks the same on any device
            EmbedFonts = true,
            // Optional: specify a folder for supporting files (images, CSS)
            ExportEmbeddedImages = true
        };

        // Save the workbook as an HTML file with embedded fonts
        string outputPath = @"C:\Temp\WorkbookWithFonts.html";
        workbook.Save(outputPath, htmlOptions);

        Console.WriteLine($"Workbook saved to HTML with embedded fonts at: {outputPath}");
    }
}
```

**Why embedding fonts matters:**  
When `EmbedFonts` is `true`, Aspose.Cells converts each used TrueType/OpenType font into a Base64‑encoded `@font-face` rule inside the generated HTML. This eliminates the need for the client machine to have the same fonts installed, guaranteeing pixel‑perfect rendering.

> **Edge case:** If the source workbook references a font that is not installed on the server, Aspose.Cells will fall back to a default font and issue a warning. Ensure the required fonts are available


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [How to Embed Fonts in HTML – Convert Excel to HTML with C#](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-convert-excel-to-html-with-c/)
- [How to Convert Excel Files to HTML Using Aspose.Cells for .NET: Hiding Overlaid Content](/cells/english/net/workbook-operations/excel-to-html-hide-overlaid-content-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}