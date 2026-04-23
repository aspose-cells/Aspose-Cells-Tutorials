---
category: general
date: 2026-02-09
description: C#에서 피벗 참조 범위를 만들고 피벗 테이블 이미지를 내보내세요. Aspose.Cells를 사용해 Excel 범위를 PNG로
  저장하는 방법을 배우세요 – 빠르고 완전한 가이드.
draft: false
keywords:
- create pivot reference range
- export pivot table image
- save excel range as png
- Aspose.Cells C#
- Excel automation C#
language: ko
og_description: C#에서 피벗 참조 범위를 생성하고 피벗 테이블 이미지를 PNG로 내보내기. Excel 범위를 PNG로 저장하는 완전한
  단계별 가이드.
og_title: 피벗 참조 범위 만들기 – 피벗 테이블 이미지를 PNG로 내보내기
tags:
- Aspose.Cells
- C#
- Excel
title: 피벗 참조 범위 만들기 – 피벗 테이블 이미지를 PNG로 내보내기
url: /ko/net/rendering-and-export/create-pivot-reference-range-export-pivot-table-image-as-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 피벗 참조 범위 만들기 – 피벗 테이블 이미지를 PNG로 내보내기

C#을 사용하여 Excel 워크북에서 **피벗 참조 범위 만들기**가 필요하신가요? 몇 줄의 코드만으로 **피벗 테이블 이미지 내보내기**와 **Excel 범위를 PNG로 저장하기**를 할 수 있습니다. 실제 피벗을 정적인 이미지로 변환하면 전체 워크북을 함께 가져가지 않고도 보고서, 이메일 또는 대시보드에 분석 결과를 삽입할 수 있어 매우 편리합니다.

이 튜토리얼에서는 필요한 라이브러리, 정확한 코드, 각 호출이 중요한 이유, 그리고 마주칠 수 있는 몇 가지 함정에 대해 단계별로 살펴봅니다. 마지막까지 따라오시면 자신 있게 피벗 테이블의 PNG 파일을 생성할 수 있게 되며, 여러 워크시트나 사용자 지정 이미지 형식에 맞게 패턴을 확장하는 방법도 이해하게 됩니다.

## 사전 요구 사항

시작하기 전에 다음이 준비되어 있는지 확인하세요:

- **Aspose.Cells for .NET** (무료 체험판으로 테스트 가능).  
- **.NET 6.0** 이상 – 사용되는 API는 .NET Standard 2.0+와 완전히 호환되므로 이전 프레임워크에서도 컴파일됩니다.  
- 기본 C# 프로젝트 (콘솔 앱, WinForms, ASP.NET 등 – NuGet 패키지를 참조할 수 있는 환경).  

아직 Aspose.Cells를 설치하지 않으셨다면 다음을 실행하세요:

```bash
dotnet add package Aspose.Cells
```

이것만으로 충분합니다 – COM 인터옵, 서버에 Excel 설치 등이 필요 없습니다.

## 1단계: 워크북 열기 및 첫 번째 워크시트 접근

먼저 워크북 파일을 로드하고 피벗 테이블이 포함된 워크시트를 가져옵니다. 대부분의 데모 파일이 피벗을 첫 번째 시트에 두기 때문에 **첫 번째 워크시트**(`Worksheets[0]`)를 선택했지만, 필요에 따라 인덱스를 이름으로 교체할 수 있습니다.

```csharp
using Aspose.Cells;
using System;

// Load an existing Excel file (replace with your own path)
Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Access the first worksheet – this is where our pivot lives
Worksheet worksheet = wb.Worksheets[0];
```

*왜 중요한가:* `Worksheet`은 모든 범위 기반 작업의 진입점입니다. 잘못된 시트를 지정하면 이후 `PivotTables[0]` 호출에서 `IndexOutOfRangeException`이 발생합니다.

## 2단계: 피벗 참조 범위 만들기

이제 피벗 테이블 자체에 **참조 범위**를 요청합니다. 이 범위는 피벗을 구성하는 정확한 셀(헤더, 데이터 행, 합계)을 모두 포함합니다. `CreateReferenceRange()` 메서드는 내부에서 병합 셀과 숨김 행을 처리해 주므로 직접 구현할 필요가 없습니다.

```csharp
// Grab the first pivot table on the worksheet
PivotTable pivot = worksheet.PivotTables[0];

// Build a reference range that covers the whole pivot
Range pivotReferenceRange = pivot.CreateReferenceRange();
```

> **팁:** 워크북에 피벗이 여러 개 있는 경우 `worksheet.PivotTables`를 순회하면서 `Name` 속성으로 원하는 피벗을 선택하세요.

## 3단계: 참조 범위를 이미지로 렌더링

Aspose.Cells는 어떤 `Range`든 이미지로 렌더링할 수 있습니다. 반환된 객체는 래스터(PNG, JPEG)와 벡터(SVG) 형식을 모두 지원합니다. 여기서는 기본 래스터 이미지를 요청하므로 `System.Drawing.Image`와 호환되는 객체를 얻습니다.

```csharp
// Convert the pivot reference range into an image object
ImageOrVector pivotImage = pivotReferenceRange.ToImage();
```

*내부 동작:* API는 셀 스타일, 폰트, 조건부 서식을 고려해 범위의 시각적 레이아웃을 스냅샷합니다. UI 없이 프로그래밍 방식으로 스크린샷을 찍는 것과 동일합니다.

## 4단계: 생성된 이미지를 파일로 저장

마지막으로 이미지를 영구 저장합니다. `Save` 메서드는 파일 확장자가 “.png”이면 자동으로 PNG 형식을 선택합니다. DPI 제어나 다른 형식이 필요하면 `SaveOptions` 객체를 전달할 수도 있습니다.

```csharp
// Save the image as PNG – the extension drives the format
pivotImage.Save("YOUR_DIRECTORY/pivot.png");
```

위 코드를 실행한 뒤 `pivot.png`를 열어 보면 피벗 테이블의 픽셀 단위 정확한 스냅샷이 표시되며, 어디에든 삽입할 준비가 된 상태입니다.

## 전체 작업 예제

전체 흐름을 한 번에 보여주는 콘솔 프로그램 예제입니다. 복사‑붙여넣기 후 바로 실행해 보세요:

```csharp
using Aspose.Cells;
using System;

namespace PivotExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

            // 2️⃣ Access first worksheet
            Worksheet worksheet = wb.Worksheets[0];

            // 3️⃣ Get first pivot table
            if (worksheet.PivotTables.Count == 0)
            {
                Console.WriteLine("No pivot tables found on the first sheet.");
                return;
            }
            PivotTable pivot = worksheet.PivotTables[0];

            // 4️⃣ Create a reference range that covers the whole pivot
            Range pivotReferenceRange = pivot.CreateReferenceRange();

            // 5️⃣ Render the range to an image
            ImageOrVector pivotImage = pivotReferenceRange.ToImage();

            // 6️⃣ Save as PNG
            string outputPath = "YOUR_DIRECTORY/pivot.png";
            pivotImage.Save(outputPath);

            Console.WriteLine($"Pivot table image saved to {outputPath}");
        }
    }
}
```

**예상 결과:** `YOUR_DIRECTORY`에 `pivot.png` 파일이 생성됩니다. 이미지 뷰어로 열면 원본 피벗과 동일한 레이아웃(열 헤더, 데이터 행, 총합)이 표시됩니다.

## 피벗 테이블 이미지 내보내기 – 크기 및 DPI 사용자 지정

기본 이미지가 프레젠테이션 슬라이드에 비해 작을 때가 있습니다. `ImageOrVectorSaveOptions` 객체를 전달해 해상도를 조절할 수 있습니다:

```csharp
using Aspose.Cells.Drawing;

// Define PNG options – 300 DPI for high‑quality print
ImageOrVectorSaveOptions options = new ImageOrVectorSaveOptions
{
    ImageFormat = ImageFormat.Png,
    Resolution = 300 // DPI
};

pivotImage.Save("YOUR_DIRECTORY/pivot_highres.png", options);
```

*왜 DPI를 조정하나요?* DPI가 높을수록 가장자리가 더 선명해지며, PNG를 PowerPoint나 PDF에서 확대할 때 품질이 유지됩니다.

## Excel 범위를 PNG로 저장 – 여러 워크시트 처리

여러 시트에서 피벗을 내보내야 한다면 `Workbook.Worksheets`를 순회하면서 위 과정을 반복하면 됩니다. 간결한 스니펫은 다음과 같습니다:

```csharp
foreach (Worksheet ws in wb.Worksheets)
{
    foreach (PivotTable pt in ws.PivotTables)
    {
        Range refRange = pt.CreateReferenceRange();
        ImageOrVector img = refRange.ToImage();
        string fileName = $"pivot_{ws.Name}_{pt.Name}.png";
        img.Save($"YOUR_DIRECTORY/{fileName}");
        Console.WriteLine($"Saved {fileName}");
    }
}
```

이 패턴은 워크북 전체의 모든 피벗에 대해 **피벗 테이블 이미지 내보내기**를 수행하며, 각 파일은 시트와 피벗 이름을 기반으로 저장돼 배치 처리에 적합합니다.

## 흔히 발생하는 문제와 해결 방법

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| `IndexOutOfRangeException` on `PivotTables[0]` | 워크시트에 피벗 테이블이 없음 | `worksheet.PivotTables.Count`를 확인한 후 접근 |
| Blank image output | 피벗이 모든 행을 숨기도록 필터링됨 | 피벗에 보이는 데이터가 있는지 확인하거나 `pivot.RefreshData();`를 호출 |
| Low‑resolution PNG | 기본 DPI가 96 | 위에서 보여준 대로 `ImageOrVectorSaveOptions.Resolution` 사용 |
| File‑path errors | `YOUR_DIRECTORY`에 잘못된 문자 포함 | `Path.Combine`과 `Path.GetInvalidPathChars()`로 경로 정리 |

## 검증 – 간단 테스트

전체 예제를 실행한 뒤:

1. Windows Photo Viewer에서 `pivot.png`를 엽니다.  
2. 열 헤더, 데이터 행, 합계 행이 Excel 화면과 일치하는지 확인합니다.  
3. 누락된 행이 보이면 `CreateReferenceRange()` 전에 피벗의 **RefreshData** 메서드가 호출됐는지 다시 확인합니다.

## 보너스: PNG를 Word 문서에 삽입하기

이미 PNG 형식이므로 바로 Aspose.Words에 전달할 수 있습니다:

```csharp
using Aspose.Words;
Document doc = new Document();
DocumentBuilder builder = new DocumentBuilder(doc);
builder.InsertImage("YOUR_DIRECTORY/pivot.png");
doc.Save("YOUR_DIRECTORY/report.docx");
```

이제 피벗 스냅샷이 포함된 Word 보고서를 자동으로 생성할 수 있으며, 수동 복사‑붙여넣기가 필요 없습니다.

## 결론

Aspose.Cells와 C#을 활용해 **피벗 참조 범위 만들기**, **피벗 테이블 이미지 내보내기**, **Excel 범위를 PNG로 저장하기**를 구현하는 방법을 배웠습니다. 핵심 포인트는:

- `PivotTable.CreateReferenceRange()`로 피벗의 시각 영역을 분리  
- `Range.ToImage()`로 해당 범위를 이미지로 변환  
- PNG로 저장하면서 필요 시 DPI를 조정해 인쇄 품질 확보  

이제 배치 내보내기, SVG·JPEG 등 다른 이미지 형식, 혹은 PNG를 PDF·Word에 삽입하는 작업까지 확장할 수 있습니다. 피벗을 정적인 그래픽으로 캡처하면 할 수 있는 것이 무궁무진합니다.

질문이나 어려운 상황이 있으면 아래 댓글로 알려 주세요. 즐거운 코딩 되세요!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}