---
category: general
date: 2026-09-27
description: Excel에서 인쇄 영역을 설정하고 선택한 셀을 PNG 이미지로 내보내는 방법을 배웁니다. 이 가이드는 범위를 이미지로 저장하고
  워크시트에 그림을 추가하는 방법도 다룹니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- how to export png
- save range as image
- add picture to worksheet
- export selected cells image
language: ko
lastmod: 2026-09-27
og_description: Excel에서 인쇄 영역을 설정하고 Aspose.Cells로 PNG를 내보내세요. 단계별 가이드를 따라 범위를 이미지로
  저장하고 워크시트에 그림을 추가하세요.
og_image_alt: Screenshot showing set print area excel and exported PNG file
og_title: Excel에서 인쇄 영역 설정 – C#으로 PNG 내보내기
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Set print area in Excel and learn how to export PNG images of selected
    cells. This guide also covers saving range as image and adding picture to worksheet.
  headline: How to set print area in Excel and export PNG
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Excel에서 인쇄 영역을 설정하고 PNG로 내보내는 방법
url: /ko/net/rendering-and-export/how-to-set-print-area-in-excel-and-export-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel에서 인쇄 영역 설정 및 PNG 내보내기

이미지를 만들기 전에 **set print area excel**이 필요하다면, 이 가이드는 정확히 어떻게 하는지 보여줍니다. 또한 특정 범위에서 **how to export png** 파일을 내보내고, **save range as image**, **add picture to worksheet**을 한 번에 반복 가능한 워크플로우로 배우게 됩니다.

프로그래밍 방식으로 Excel을 다룰 때는 피벗 테이블이나 차트와 같이 셀의 일부만 이미지로 만들고 싶을 때가 많습니다. 먼저 인쇄 영역을 정의하면 내보낸 PNG에 정확히 원하는 셀만 포함되며, 불필요한 부분은 제외됩니다. 이 튜토리얼은 워크북을 로드하는 단계부터 최종 PNG 파일을 저장하는 단계까지 모든 과정을 자세히 안내하고, 각 설정이 왜 중요한지 설명합니다.

## 사전 요구 사항

시작하기 전에 다음이 설치되어 있는지 확인하세요:

* .NET 6.0 이상 설치  
* Visual Studio 2022 (또는 기타 C# IDE)  
* **Aspose.Cells for .NET** NuGet 패키지 (`Install-Package Aspose.Cells`)  
* 알려진 디렉터리에 위치한 Excel 파일 (`input.xlsx`)  

이 요구 사항은 추가 설정 없이 코드를 실행할 수 있도록 보장합니다.

## 단계 1: 작업할 워크북 로드하기

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Load the workbook from disk
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

`Workbook` 클래스는 전체 Excel 파일을 나타냅니다. 먼저 로드하면 워크시트, 셀 및 페이지 설정 옵션에 접근할 수 있습니다.

## 단계 2: 대상 범위에 **Set print area excel** 적용

```csharp
// Define the range you want to capture
string printArea = "A1:G20";

// Apply the range as the print area on the first worksheet
workbook.Worksheets[0].PageSetup.PrintArea = printArea;
```

**print area**를 설정하면 Excel(및 Aspose.Cells)에 어떤 셀이 인쇄 가능한 페이지에 포함되는지 알려줍니다. 이후 시트를 이미지로 내보낼 때 이 영역만 렌더링되므로 깔끔한 **export selected cells image**를 만들 수 있습니다.

## 단계 3: 이미지 내보내기 옵션 구성 – **how to export png**

```csharp
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG ensures lossless quality
    OnePagePerSheet = true           // Export the defined print area as a single page
};
```

`ImageOrPrintOptions`는 출력 형식을 제어합니다. `ImageFormat.Png`를 선택하면 웹 및 데스크톱 환경 모두에서 잘 작동하는 고해상도 투명 배경 이미지를 보장합니다.

## 단계 4: 정의된 범위에서 그림 만들기 및 **add picture to worksheet**

```csharp
// Create a picture object from the selected range
Picture picture = workbook.Worksheets[0].Pictures.Add(
    0,                                     // top‑left row index where the picture will be placed
    0,                                     // top‑left column index where the picture will be placed
    workbook.Worksheets[0].Cells.CreateRange(printArea));
```

`Pictures.Add` 메서드는 워크시트에 새 그림을 삽입합니다. 2단계에서 만든 범위를 전달하면 **save range as image**를 직접 시트에 삽입할 수 있어, 이후 워크북의 다른 부분에서 해당 그림을 참조할 때 유용합니다.

## 단계 5: **Save the picture as an image file** – **export selected cells image** 워크플로우 완료

```csharp
// Save the picture to disk as a PNG file
picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);
```

`Save`를 호출하면 3단계에서 정의한 옵션을 사용해 파일 시스템에 그림을 저장합니다. 결과물인 `selected_range.png`는 **set print area excel** 명령으로 정의된 셀만 정확히 포함합니다.

## 전체 실행 가능한 예제

모든 코드를 합치면 콘솔 애플리케이션 어디에든 넣을 수 있는 간결한 프로그램이 완성됩니다:

```csharp
using System;
using Aspose.Cells;
using System.Drawing.Imaging;

class ExportExcelRangeAsPng
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Set print area excel
        string printArea = "A1:G20";
        workbook.Worksheets[0].PageSetup.PrintArea = printArea;

        // 3️⃣ Configure how to export png
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            OnePagePerSheet = true
        };

        // 4️⃣ Add picture to worksheet (save range as image)
        Picture picture = workbook.Worksheets[0].Pictures.Add(
            0,
            0,
            workbook.Worksheets[0].Cells.CreateRange(printArea));

        // 5️⃣ Export selected cells image
        picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);

        Console.WriteLine("PNG exported successfully to YOUR_DIRECTORY\\selected_range.png");
    }
}
```

### 예상 출력

프로그램을 실행하면 다음과 같이 출력됩니다:

```
PNG exported successfully to YOUR_DIRECTORY\selected_range.png
```

그리고 `input.xlsx`의 A1부터 G20까지 셀만 표시된 `selected_range.png` 파일이 생성됩니다.

## 일반적인 함정 및 회피 방법

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| The exported image contains the whole sheet | No print area was defined | Ensure you **set print area excel** before creating the picture |
| PNG is blurry | Default DPI is low | Set `imageOptions.DpiX` and `imageOptions.DpiY` to a higher value (e.g., 300) |
| File not found error | Wrong directory path | Use `Path.Combine` or double‑check the folder exists |
| Picture appears offset | Incorrect row/column indices | The first two parameters of `Pictures.Add` are the top‑left cell where the picture is placed; keep them at `0,0` for a clean export |

## 전문가 팁: 한 번에 여러 범위 내보내기

여러 영역에 대해 **export selected cells image**가 필요하다면 2‑5단계를 루프 안에서 반복하고 각 반복마다 `printArea`를 변경하세요. 각 그림에 고유한 파일 이름을 부여하지 않으면 나중에 저장할 때 이전 파일을 덮어쓰게 됩니다.

## 결론

이제 **set print area excel**, **how to export png** 구성, **save range as image**, **add picture to worksheet**을 Aspose.Cells를 사용해 수행하는 방법을 알게 되었습니다. 이 엔드‑투‑엔드 솔루션을 통해 몇 줄의 C# 코드만으로 어떤 셀 블록도 고품질 PNG로 변환할 수 있습니다.

다음 단계로 살펴볼 내용:

* 내보낸 PNG에 테두리나 워터마크 추가하기 (*add picture to worksheet*와 스타일링 검색)
* 인쇄 가능한 보고서를 위해 PDF로 직접 내보내기 (*export selected cells image* → PDF 워크플로우)
* 배치 작업으로 여러 워크북 자동 처리하기

다양한 범위, DPI 설정, 이미지 포맷을 실험해 보면서 프로젝트 요구에 맞게 조정해 보세요. 즐거운 코딩 되세요!

## 다음에 배울 내용은?

다음 튜토리얼들은 이 가이드에서 다룬 기술을 기반으로 하는 밀접한 주제를 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 포함하고 있어 추가 API 기능을 마스터하고 프로젝트에 적용할 수 있는 다양한 구현 방법을 탐색하는 데 도움이 됩니다.

- [Excel에서 인쇄 영역을 설정하고 PowerPoint로 내보내기 – 단계별 가이드](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Aspose.Cells Java로 Excel 인쇄 영역을 HTML로 내보내기](/cells/english/java/workbook-operations/export-excel-print-area-html-aspose-cells-java/)
- [Aspose.Cells for .NET을 사용해 Excel에서 인쇄 영역 설정하기](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}