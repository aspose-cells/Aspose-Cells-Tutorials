---
category: general
date: 2026-03-30
description: Aspose.Cells와 Aspose.Slides를 사용하여 Excel에서 빠르게 PowerPoint를 만들세요. 워크시트를
  이미지로 내보내고 C#에서 프레젠테이션을 PPTX 파일로 저장하는 방법을 배우세요.
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export worksheet as image
- save presentation as pptx
- export excel chart as picture
language: ko
og_description: Aspose를 사용하여 C#에서 Excel을 PowerPoint로 만들기. 워크시트를 이미지로 내보내고, 도형을 편집
  가능하게 유지하며, 결과를 PPTX로 저장합니다.
og_title: Excel에서 PowerPoint 만들기 – 완전한 C# 튜토리얼
tags:
- Aspose
- C#
- Office Automation
title: Excel에서 PowerPoint 만들기 – 단계별 C# 가이드
url: /ko/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel에서 PowerPoint 만들기 – 완전 C# 튜토리얼

Excel에서 **PowerPoint를 만들**고 싶지만 차트를 편집 가능한 상태로 유지할 수 있는 라이브러리를 몰라 고민한 적 있나요? 여러분만 그런 것이 아닙니다. 많은 보고서 시나리오에서 스프레드시트를 슬라이드 덱으로 변환하면서 텍스트 상자를 나중에 수정할 수 있기를 원합니다. 이 가이드는 Aspose.Cells와 Aspose.Slides를 사용해 **Excel을 PowerPoint로 변환**하는 방법을 정확히 보여주며, **워크시트를 이미지로 내보내는 방법**과 최종적으로 **프레젠테이션을 PPTX로 저장하는 방법**까지 다룹니다.

코드 한 줄 한 줄을 살펴보면서 각 설정이 왜 중요한지 설명하고, 복잡한 차트를 이미지로 내보내고 싶을 때는 어떻게 해야 하는지도 논의합니다. 최종적으로 `ShapesDemo.xlsx`를 받아 `Result.pptx`를 생성하는 실행 가능한 C# 콘솔 앱을 만들 수 있게 됩니다 – 텍스트 상자는 편집 가능하고 이미지도 선명합니다.

## 준비 사항

- .NET 6.0 이상 (API는 .NET Framework에서도 동작하지만 .NET 6이 가장 권장됩니다).  
- **Aspose.Cells**와 **Aspose.Slides** NuGet 패키지 (무료 체험 라이선스로 테스트 가능).  
- C# 문법에 대한 기본적인 이해 – `Console.WriteLine`을 쓸 수만 하면 충분합니다.  

추가적인 COM 인터옵, 서버에 Office 설치, 이미지 수동 복사‑붙여넣기 전혀 필요 없습니다. 모든 작업이 프로그래밍으로 처리됩니다.

---

## Excel에서 PowerPoint 만들기 – 워크북 로드 및 내보내기 옵션 설정

먼저 Excel 파일을 열고 Aspose.Cells에 시트를 어떻게 렌더링할지 알려줍니다. `ImageOrPrintOptions` 객체가 핵심이며, 여기서 `ExportShapes`와 `ExportEditableTextBoxes`를 활성화하면 모든 도형(차트 포함)이 슬라이드에 포함되면서 변환 후에도 편집이 가능합니다.

```csharp
using Aspose.Cells;
using Aspose.Slides;

// 1️⃣ Load the Excel workbook
string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
Workbook workbook = new Workbook(excelPath);
Worksheet worksheet = workbook.Worksheets[0];   // Grab the first sheet

// 2️⃣ Configure image export – keep shapes editable
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    OnePagePerSheet = true,          // Export the whole sheet as one slide
    ExportShapes = true,             // Include shapes (charts, drawings)
    ExportEditableTextBoxes = true   // Make text boxes editable in PPTX
};
```

**왜 이 플래그들을 사용하나요?**  
- `OnePagePerSheet`는 시트가 여러 슬라이드로 나뉘는 것을 방지하고, 한 장의 전체 크기 이미지를 얻을 수 있게 합니다.  
- `ExportShapes`는 Aspose.Cells가 차트와 벡터 도형을 래스터화하면서도 외관을 유지하도록 합니다.  
- `ExportEditableTextBoxes`는 PowerPoint에서 텍스트 상자를 더블 클릭해 Excel을 다시 열지 않고도 텍스트를 수정할 수 있게 해 주는 비밀 소스입니다.

> **팁:** 차트의 정적 이미지만 필요하다면 `ExportShapes = false`로 설정하고, 이후에 `ExportExcelChartAsPicture` 메서드를 사용하세요 (마지막 섹션 참고).

---

## Excel을 PowerPoint로 변환 – 워크시트에서 이미지 생성

옵션을 준비했으니 이제 워크시트를 `System.Drawing.Image` 객체로 변환합니다. `WorksheetToImageConverter`가 무거운 작업을 수행하며, 앞서 정의한 설정을 적용합니다.

```csharp
// 3️⃣ Convert the worksheet to an image using the options above
WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
System.Drawing.Image sheetImage = converter.ConvertToImage(0, imageOptions);
```

`0` 인자는 첫 번째 페이지를 의미합니다 (`OnePagePerSheet` 덕분에 페이지가 하나뿐이므로). 결과인 `sheetImage`는 원본 DPI를 유지하므로 고해상도 디스플레이에서도 픽셀화되지 않은 슬라이드를 얻을 수 있습니다.

---

## PPTX로 저장 – 슬라이드에 이미지 삽입

이제 새 PowerPoint 파일을 만들고 슬라이드를 추가한 뒤 비트맵을 삽입합니다. Aspose.Slides는 그림을 *picture frame* 형태의 도형으로 취급하므로, 이후에 원본 PowerPoint 객체처럼 크기 조절이나 이동이 가능합니다.

```csharp
// 4️⃣ Create a new PowerPoint presentation
Presentation presentation = new Presentation();
ISlide slide = presentation.Slides[0];   // The default blank slide

// Add the Excel‑derived image as a picture frame
slide.Shapes.AddPictureFrame(
    ShapeType.Rectangle,                 // Simple rectangle container
    0, 0,                                // Top‑left corner (0,0)
    sheetImage.Width,                    // Width of the picture
    sheetImage.Height,                   // Height of the picture
    sheetImage);                         // The bitmap we generated
```

> **이미지가 슬라이드 크기보다 클 경우?**  
> PowerPoint는 슬라이드 영역을 초과하는 부분을 자동으로 잘라냅니다. 간단히 이미지 크기를 조정한 뒤 삽입하면 됩니다:

```csharp
float scale = Math.Min(presentation.SlideSize.Size.Width / (float)sheetImage.Width,
                       presentation.SlideSize.Size.Height / (float)sheetImage.Height);
int newWidth  = (int)(sheetImage.Width * scale);
int newHeight = (int)(sheetImage.Height * scale);
```

그 후 `newWidth`와 `newHeight` 값을 `AddPictureFrame`에 전달하면 됩니다.

---

## 워크시트를 이미지로 내보내기 – PPTX 파일 저장

마지막으로 프레젠테이션을 디스크에 저장합니다. `SaveFormat.Pptx` 플래그는 최신 OpenXML 형식을 보장하며, 모든 최신 버전의 PowerPoint에서 호환됩니다.

```csharp
// 5️⃣ Save the presentation as a PPTX file
string pptxPath = "YOUR_DIRECTORY/Result.pptx";
presentation.Save(pptxPath, SaveFormat.Pptx);
```

`Result.pptx`를 열면 Excel 시트와 똑같이 보이는 단일 슬라이드가 나타나지만, 텍스트 상자를 클릭하면 PowerPoint 내에서 바로 내용을 편집할 수 있습니다.

---

## Excel 차트를 이미지로 내보내기 – 래스터 이미지가 필요할 때

때로는 편집 가능한 도형이 필요 없고 차트의 고품질 PNG만 있으면 충분합니다. Aspose.Cells는 전체 시트를 변환하지 않고 특정 차트를 이미지로 내보낼 수 있습니다:

```csharp
// Example: Export the first chart on the sheet as a PNG
int chartIndex = 0; // Adjust if you have multiple charts
Chart chart = worksheet.Charts[chartIndex];
ImageOrPrintOptions chartOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    OnePagePerSheet = false
};
chart.ToImage("chart.png", chartOptions);
```

그 후 `chart.png`를 앞서 `sheetImage`를 삽입한 방식과 동일하게 슬라이드에 넣으면 됩니다. 이 방법은 PPTX 파일 크기를 줄이고, 슬라이드에 주변 데이터가 필요 없을 때 유용합니다.

---

## 흔히 겪는 문제와 해결 방법

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **텍스트가 흐릿하게 보임** | 낮은 DPI(기본 96)로 내보냈기 때문 | 변환 전에 `imageOptions.Dpi = 300;` 설정 |
| **도형이 사라짐** | `ExportShapes`가 `false`인 경우 | 편집 가능한 그래픽이 필요하면 `ExportShapes = true` 확인 |
| **슬라이드 크기 불일치** | 이미지가 슬라이드보다 큼 | 이미지 스케일링(코드 스니펫 참고) 또는 `presentation.SlideSize`로 슬라이드 크기 변경 |
| **라이선스 예외** | 트라이얼 버전을 활성화 없이 사용 | `License license = new License(); license.SetLicense("Aspose.Total.lic");` 를 `Main` 초기에 호출 |

---

## 전체 작업 예제 (복사‑붙여넣기 바로 사용)

아래는 새 콘솔 프로젝트에 바로 넣을 수 있는 전체 프로그램입니다. `YOUR_DIRECTORY`를 Excel 파일이 있는 폴더 경로로 바꾸세요.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;
using System.Drawing;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the Excel workbook
            // -----------------------------------------------------------------
            string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
            Workbook workbook = new Workbook(excelPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -----------------------------------------------------------------
            // 2️⃣ Set up export options – keep shapes editable
            // -----------------------------------------------------------------
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                OnePagePerSheet = true,
                ExportShapes = true,
                ExportEditableTextBoxes = true,
                Dpi = 300                 // High‑resolution output
            };

            // -----------------------------------------------------------------
            // 3️⃣ Convert worksheet to an image
            // -----------------------------------------------------------------
            WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
            Image sheetImage = converter.ConvertToImage(0, imageOptions);

            // -----------------------------------------------------------------
            // 4️⃣ Create PowerPoint and add the image as a slide
            // -----------------------------------------------------------------
            Presentation presentation = new Presentation();
            ISlide slide = presentation.Slides[0];
            slide.Shapes.AddPictureFrame(
                ShapeType.Rectangle,
                0, 0,
                sheetImage.Width,
                sheetImage.Height,
                sheetImage);

            // -----------------------------------------------------------------
            // 5️⃣ Save the PPTX file
            // -----------------------------------------------------------------
            string pptxPath = "YOUR_DIRECTORY/Result.pptx";
            presentation.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine("✅ PowerPoint created successfully at: " + pptxPath);
        }
    }
}
```

**예상 출력:**  
프로그램 실행 시 `✅ PowerPoint created successfully at: YOUR_DIRECTORY/Result.pptx` 가 콘솔에 표시됩니다. PPTX를 열면 원본 Excel 시트를 그대로 반영한 단일 슬라이드가 나타나며, 텍스트 상자는 편집 가능 상태입니다.

---

## 정리 및 다음 단계

이제 Aspose의 강력한 API를 활용해 **Excel에서 PowerPoint를 만들**는 방법, **워크시트를 이미지로 내보내는 방법**, 그리고 **편집 가능성을 유지하면서 PPTX로 저장하는 방법**을 알게 되었습니다. 동일한 패턴을 사용하면 다중 시트 워크북도 쉽게 처리할 수 있습니다—`workbook.Worksheets`를 순회하면서 각 시트마다 새 슬라이드를 추가하면 됩니다.

**다음에 탐구해볼 내용:**  

- **배치 변환:** 폴더에 있는 여러 Excel 파일을 순회하며 파일당 슬라이드 덱 생성  
- **동적 레이아웃:** `slide.LayoutSlide`를 사용해 미리 디자인된 PowerPoint 템플릿 적용  
- **차트 전용 내보내기:** “Excel 차트를 이미지로 내보내기” 스니펫을 슬라이드 플레이스홀더와 결합해 경량 덱 만들기  
- **고급 스타일링:** Aspose.Slides를 이용해 커스텀 슬라이드 배경, 전환 효과, 애니메이션 적용  

자유롭게 실험해 보세요—DPI를 바꾸거나 `ShapeType.Ellipse`를 원형 picture frame으로 교체하거나, 슬라이드당 여러 이미지를 삽입하는 등 프로그램matic 제어가 가능하면 가능성은 무한합니다.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}