---
category: general
date: 2026-10-26
description: C#에서 인쇄 영역을 설정하고 Excel 시트를 PNG로 내보내기. 이미지 내보내기 옵션을 배우고, PNG를 내보내는 방법을
  익히며, 워크북에서 인쇄 가능한 이미지를 얻으세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area
- excel sheet to png
- how to export png
- export excel image
- image export options
language: ko
lastmod: 2026-10-26
og_description: C#에서 인쇄 영역을 설정하고 Excel 시트를 PNG로 내보내기. 이 단계별 튜토리얼은 이미지 내보내기 옵션과 워크북에서
  PNG를 내보내는 방법을 다룹니다.
og_image_alt: Screenshot showing an Excel worksheet with the print area set and exported
  as a PNG image
og_title: 인쇄 영역 설정 및 Excel 시트를 PNG로 내보내기 – C# 가이드
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Set print area and export an Excel sheet to PNG in C#. Learn image
    export options, how to export PNG, and get a printable image from a workbook.
  headline: Set print area and export Excel sheet to PNG in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: C#에서 인쇄 영역을 설정하고 Excel 시트를 PNG로 내보내기
url: /ko/net/rendering-and-export/set-print-area-and-export-excel-sheet-to-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 인쇄 영역을 설정하고 Excel 시트를 PNG로 내보내기

Excel 시트를 PNG로 내보내기 전에 **인쇄 영역을 설정**해야 하는 경우, 이 가이드에서 방법을 보여드립니다. 이미지 내보내기 옵션을 구성하고, 워크시트의 인쇄 영역을 조정한 뒤 결과를 이미지로 저장하는 완전한 C# 예제를 확인할 수 있습니다.

Excel 시트를 PNG로 내보내는 것은 보고서, 이메일 또는 웹 페이지에 워크시트 스냅샷을 삽입하고자 할 때 일반적인 요구 사항입니다. 아래 코드는 피벗 테이블이 포함된 모든 워크북에서 작동하지만, 일반 데이터 범위에도 동일한 기술을 적용할 수 있습니다. 외부 도구는 필요 없으며 Aspose.Cells for .NET 라이브러리만 있으면 됩니다.

## Prerequisites

- .NET 6.0 이상 (샘플은 .NET 6을 대상으로 하지만 최신 .NET 버전이면 모두 작동합니다)
- Aspose.Cells for .NET (NuGet를 통해 설치: `Install-Package Aspose.Cells`)
- 워크시트 및 인쇄 영역과 같은 Excel 개념에 대한 기본적인 C# 지식

## Step 1: 이미지 내보내기 옵션 구성

첫 번째로 `ImageOrPrintOptions` 인스턴스를 생성합니다. 이 객체는 Aspose.Cells에 시트를 이미지로 렌더링하는 방법을 알려줍니다.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

// Define image export options (PNG format)
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    // Export quality settings can be adjusted here
    ImageFormat = ImageFormat.Png,
    // Optional: set resolution (DPI) for higher‑quality PNGs
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

**Why this matters:** `ImageOrPrintOptions`는 출력 형식, 해상도 및 기타 렌더링 세부 정보를 제어합니다. PNG를 사용하면 무손실 품질을 보장하므로 선명한 텍스트와 그래픽이 필요한 보고서에 이상적입니다.

## Step 2: 워크북을 로드하고 대상 워크시트에 접근

특정 `Worksheet` 객체와 작업해야 인쇄 영역은 워크시트 수준 설정이기 때문입니다.

```csharp
// Load an existing workbook (replace with your file path)
Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

// Access the first worksheet in the workbook
Worksheet worksheet = wb.Worksheets[0];
```

**Why this matters:** 인쇄 영역은 워크시트‑레벨 설정이므로 정확한 `Worksheet` 객체를 사용해야 합니다.

## Step 3: 인쇄하려는 범위 식별

많은 경우 관심 있는 데이터는 피벗 테이블 내부에 있습니다. 다음 코드는 시트에 있는 첫 번째 피벗 테이블의 데이터 범위를 추출합니다.

```csharp
// Get the data range of the first pivot table on the worksheet
CellArea pivotDataRange = worksheet.PivotTables[0].PivotDataRange;
```

워크시트에 피벗 테이블이 없을 경우, `pivotDataRange`를 수동으로 만든任意의 `CellArea`로 교체할 수 있습니다. 예:

```csharp
CellArea customRange = new CellArea(0, 0, 20, 10); // A1:K21
```

## Step 4: 선택한 범위에 맞게 **인쇄 영역 설정**

```csharp
// Set the worksheet's print area to match the pivot table's data range
worksheet.PageSetup.PrintArea = pivotDataRange.RefersTo;
```

**Why this matters:** 인쇄 영역은 Excel(및 Aspose.Cells)에 이미지로 렌더링할 때 포함할 셀을 알려줍니다. 인쇄 영역을 피벗 데이터 범위와 일치시키면 빈 여백을 방지하고 내보낸 PNG에 관련 데이터만 포함됩니다.

## Step 5: 워크시트를 PNG 이미지로 내보내기

```csharp
// Export the worksheet to an image using the defined options
// and assign the resulting image to the first picture shape on the sheet
worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);

// Optionally, save the image to a file for external use
worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);
```

**Why this matters:** `worksheet.ToImage`는 이전에 설정한 인쇄 영역을 존중하므로 PNG 파일에 정의한 셀만 정확히 포함됩니다. 이미지를 그림 모양에 할당하면 필요 시 워크북에 다시 삽입할 수 있고, 디스크에 저장하면 독립 파일이 됩니다.

## Full working example

모든 단계를 합치면 즉시 실행할 수 있는 독립 프로그램이 완성됩니다.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

class ExportExcelToPng
{
    static void Main()
    {
        // 1️⃣ Configure image export options (PNG format)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 2️⃣ Load the workbook
        Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

        // 3️⃣ Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // 4️⃣ Get the data range of the first pivot table (or define your own)
        CellArea dataRange = worksheet.PivotTables[0].PivotDataRange;

        // 5️⃣ **Set print area** to the data range
        worksheet.PageSetup.PrintArea = dataRange.RefersTo;

        // 6️⃣ Export the worksheet as PNG
        worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);
        worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);

        Console.WriteLine("Export complete: WorksheetExport.png created.");
    }
}
```

### Expected output

프로그램을 실행하면 `C:\Temp\WorksheetExport.png`가 생성됩니다. 파일을 열면 **인쇄 영역을 설정**한 셀(이 예에서는 피벗 테이블 데이터)만 포함된 선명한 PNG 이미지를 확인할 수 있습니다. 이 이미지는 추가 변환 없이 Word 문서, PowerPoint 슬라이드 또는 웹 페이지에 삽입할 수 있습니다.

## Handling multiple worksheets or pivot tables

- **여러 워크시트:** `wb.Worksheets`를 순회하면서 내보내야 하는 각 시트에 대해 단계 3‑5를 반복합니다.
- **여러 피벗 테이블:** 적절한 `PivotTables[index]`를 선택하거나 `worksheet.PivotTables`를 순회하여 각 테이블을 개별적으로 내보냅니다.
- **피벗 테이블 없음:** `CellArea`를 수동으로 생성(단계 3의 주석 참고)하고 `PrintArea`에 할당합니다.

## Practical tips (E‑E‑A‑T)

- **프로 팁:** 인쇄용 PNG를 위해 `HorizontalResolution` 및 `VerticalResolution`을 300 DPI로 설정합니다; 낮은 값은 웹용 파일 크기를 줄입니다.
- **빈 그림 모양 주의:** 워크시트에 그림 모양이 없으면 이미지를 할당하기 전에 하나 추가합니다:

```csharp
if (worksheet.Pictures.Count == 0)
{
    worksheet.Pictures.Add(0, 0, 0, 0);
}
```

- **성능:** 여러 워크시트에 대해 단일 `ImageOrPrintOptions` 인스턴스를 재사용하면 불필요한 할당을 방지합니다.
- **호환성:** Aspose.Cells 23.9+는 .NET 6 이상을 완전히 지원합니다; 이전 버전은 API 이름을 조정해야 할 수 있습니다.

## Conclusion

이제 **인쇄 영역을 설정**하고 Excel을 내보내는 방법을 알게 되었습니다.

## What Should You Learn Next?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접하게 관련된 주제를 다룹니다. 각 리소스에는 단계별 설명과 완전한 코드 예제가 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [Excel을 PNG로 내보내는 방법 – 전체 단계별 가이드](/cells/english/net/image-and-chart-operations/how-to-export-excel-to-png-full-step-by-step-guide/)
- [C#와 Aspose.Cells를 사용하여 Excel 범위를 이미지로 내보내는 방법](/cells/english/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/)
- [excel sheet to png – C#에서 피벗 테이블을 PNG로 내보내기](/cells/english/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}