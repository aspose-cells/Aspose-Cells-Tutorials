---
category: general
date: 2026-11-16
description: Excel을 PowerPoint로 저장하고 프로그래밍 방식으로 Excel을 PowerPoint로 변환하는 방법을 배워보세요.
  이 단계별 가이드에서는 Excel을 PPTX로 내보내고 워크북을 PPTX로 저장하는 방법도 다룹니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- export excel to pptx
- how to convert excel slide
- save workbook as pptx
language: ko
lastmod: 2026-11-16
og_description: Aspose.Cells를 사용하여 Excel을 PowerPoint로 저장하십시오. 이 가이드를 따라 Excel을 PowerPoint로
  변환하고, Excel을 PPTX로 내보내며, 워크북을 몇 분 안에 PPTX로 저장하세요.
og_image_alt: Screenshot showing the result of saving Excel as PowerPoint with editable
  shapes
og_title: Excel을 PowerPoint로 저장 – 완전한 C# 가이드
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to save Excel as PowerPoint and convert Excel to PowerPoint
    programmatically. This step‑by‑step guide also covers export Excel to PPTX and
    saving a workbook as PPTX.
  headline: How to save Excel as PowerPoint with Aspose.Cells in C#
  type: TechArticle
tags:
- Excel
- PowerPoint
- Aspose.Cells
- C#
- Export
title: C#에서 Aspose.Cells를 사용하여 Excel을 PowerPoint로 저장하는 방법
url: /ko/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-with-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 Aspose.Cells를 사용하여 Excel을 PowerPoint로 저장하는 방법

프로그램matically **Excel을 PowerPoint로 저장**해야 한다면, 이 튜토리얼은 완전하고 바로 실행할 수 있는 솔루션을 제공합니다. 보고 엔진을 구축하거나 자동 슬라이드 생성기를 만들고 있든, 아래 단계들을 통해 Excel 워크시트를 몇 줄의 코드만으로 편집 가능한 PPTX 슬라이드로 변환할 수 있습니다.

**Excel을 PowerPoint로 변환**하는 방법, 시트를 PPTX 파일로 내보내는 방법, 그리고 텍스트 상자와 도형을 편집 가능하게 유지하는 방법을 배웁니다 – .NET 환경을 떠나지 않고.

## 사전 요구 사항

* .NET 6.0 이상 (코드는 .NET Framework 4.7.2+에서도 작동합니다)
* 유효한 Aspose.Cells 라이선스 (무료 체험판은 평가용으로 사용할 수 있습니다)
* Visual Studio 2022 (또는 모든 C# IDE)
* 내보내려는 데이터와 도형이 포함된 Excel 워크북

## 단계 1: Aspose.Cells 설치

프로젝트에 Aspose.Cells NuGet 패키지를 추가합니다:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** 특정 버전을 지정하려면 `-v` 플래그를 사용하세요, 예: `Aspose.Cells.24.5`.

## 단계 2: 내보낼 워크북 로드

**Excel을 PowerPoint로 저장** 워크플로우의 첫 번째 작업은 소스 워크북을 로드하는 것입니다.

```csharp
using Aspose.Cells;
using System;

// Load the workbook that contains the shapes
Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");
```

*왜 중요한가:* 워크북을 로드하면 워크시트, 페이지 설정 및 편집 가능한 PowerPoint 도형이 될 그리기 개체에 접근할 수 있습니다.

## 단계 3: 편집 가능한 PPTX 슬라이드를 위한 내보내기 옵션 구성

편집 가능성을 유지하면서 **Excel을 PowerPoint로 변환**하려면 `ImageOrPrintOptions`에 몇 가지 속성을 설정해야 합니다.

```csharp
// Prepare export options to generate an editable PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // Export format
    ExportEditableText = true,        // Keep text boxes editable
    ExportEditableShapes = true       // Keep shapes editable
};
```

*설명:*  
* `SaveFormat = SaveFormat.Pptx`는 Aspose.Cells에 PowerPoint 파일을 생성하도록 지시합니다.  
* `ExportEditableText`와 `ExportEditableShapes`는 결과 슬라이드가 기본 PowerPoint 슬라이드처럼 동작하도록 보장합니다—텍스트 상자나 도형을 클릭하여 PowerPoint에서 직접 편집할 수 있습니다.

## 단계 4: 내보내기 영역 정의 및 단일 슬라이드에 맞추기

**Excel을 PPTX로 내보낼** 때 일반적으로 특정 범위가 슬라이드에 표시되기를 원합니다. 인쇄 영역과 맞춤 옵션을 설정하면 깔끔한 단일 슬라이드 출력이 보장됩니다.

```csharp
// Define the area of the first worksheet to export
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G30";

// Fit the exported content to a single slide
sheet.PageSetup.FitToPagesTall = 1;
sheet.PageSetup.FitToPagesWide = 1;
```

*왜 중요한가:* `PrintArea`는 내보내기를 셀 A1부터 G30까지로 제한하고, `FitToPagesTall`와 `FitToPagesWide`는 모든 내용을 하나의 슬라이드로 압축하여 원치 않는 추가 페이지가 생기지 않게 합니다.

## 단계 5: 워크시트를 편집 가능한 PPTX 파일로 저장

이제 마침내 **워크북을 PPTX로 저장**하고 **Excel을 PowerPoint로 저장** 프로세스를 완료할 수 있습니다.

```csharp
// Save the worksheet as an editable PPTX file
workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
Console.WriteLine("Export completed: EditableShapes.pptx");
```

프로그램을 실행한 후 Microsoft PowerPoint에서 `EditableShapes.pptx`를 엽니다. 선택한 Excel 범위를 그대로 반영한 슬라이드가 표시되며, 모든 텍스트 상자와 도형을 완전히 편집할 수 있습니다.

### 예상 출력

* `C:\Output\`에 위치한 `EditableShapes.pptx` 파일.
* A1:G30 범위를 포함하는 PowerPoint 슬라이드 1장.
* PowerPoint에서 더블 클릭하여 직접 편집할 수 있는 텍스트 상자, 차트 및 도형.

## 전체 소스 코드 (복사 준비 완료)

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the shapes
            Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");

            // Step 2: Prepare export options to generate an editable PPTX slide
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportEditableText = true,   // keep text boxes editable
                ExportEditableShapes = true  // keep shapes editable
            };

            // Step 3: Define the area of the first worksheet to export
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";

            // Step 4: Fit the exported content to a single slide
            sheet.PageSetup.FitToPagesTall = 1;
            sheet.PageSetup.FitToPagesWide = 1;

            // Step 5: Save the worksheet as an editable PPTX file
            workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
            Console.WriteLine("Export completed: EditableShapes.pptx");
        }
    }
}
```

## 일반적인 질문 및 엣지 케이스 처리

| Question | Answer |
|----------|--------|
| **여러 워크시트가 있는 경우는 어떻게 하나요?** | `workbook.Worksheets`를 순회하면서 각 시트에 대해 단계 3‑5를 반복하고, 출력 파일 이름을 변경합니다(예: `Sheet1.pptx`, `Sheet2.pptx`). |
| **전체 워크북을 하나의 PowerPoint 프레젠테이션으로 내보낼 수 있나요?** | 예. `ImageOrPrintOptions`에서 `ExportAllSheets = true`로 설정합니다. 각 워크시트가 별개의 슬라이드가 됩니다. |
| **도형이 이미지로 표시되고 편집 가능한 객체가 아닙니다.** | `ExportEditableShapes = true`가 설정되어 있는지 확인하고, Aspose.Cells 24.5+를 사용하고 있는지 확인하세요(이전 버전에는 이 기능이 없습니다). |
| **생성된 PPTX 파일이 너무 큽니다.** | 인쇄 영역을 줄이거나 `exportOptions.ImageResolution`을 통해 이미지 해상도를 낮추세요. |
| **프로덕션 사용에 라이선스가 필요합니까?** | 유료 라이선스를 사용하면 평가 워터마크가 제거되고 전체 성능이 활성화됩니다. 무료 체험판은 테스트용으로 사용할 수 있습니다. |

## 안정적인 프로덕션 코드를 위한 팁

* `Workbook` 또는 `Save`를 호출하기 전에 **파일 경로를 검증**하여 `FileNotFoundException`을 방지합니다.  
* 라이선스 오류(`Aspose.Cells.LicenseException`)를 처리하려면 **내보내기를 try/catch 블록**으로 감싸세요.  
* 작업이 끝나면 **워크북을 Dispose**(`workbook.Dispose()`)하여 관리되지 않는 리소스를 해제합니다.  
* 웹 서비스에서 많은 대형 시트를 내보내는 경우 **async I/O**(`FileStream`와 `await`)를 사용하세요.

## 다음 단계

이제 **Excel을 PowerPoint로 저장**하는 방법을 알았으니, 관련 주제를 탐색할 수 있습니다:

* **맞춤 슬라이드 레이아웃으로 Excel을 PPTX로 내보내기** – `SlideSize`를 조정하고 마스터 슬라이드를 추가합니다.  
* **Excel 슬라이드를 PDF로 변환** – 인쇄용 버전으로 `SaveFormat.Pdf`를 사용합니다.  
* **워크북 폴더 일괄 변환** – 위에 보여진 루프와 `Directory.GetFiles`를 결합합니다.

다양한 인쇄 영역, 스케일 옵션 및 PowerPoint 테마를 실험하여 출력물을 조직의 브랜딩에 맞게 조정해 보세요.

---

*코딩을 즐기세요! 이 가이드가 **Excel을 PowerPoint로 변환**하는 데 도움이 되었다면, 팀원과 공유하거나 추가 지원을 위해 Aspose.Cells GitHub 저장소에 이슈를 열어 주세요.*

## 다음에 배워야 할 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료에는 전체 작업 코드 예제와 단계별 설명이 포함되어 있어 추가 API 기능을 마스터하고 자체 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [C#와 Aspose.Cells를 사용하여 Excel을 PowerPoint로 저장하는 방법](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/)
- [Excel에서 PPTX 저장 – Excel 시트를 PowerPoint로 내보내는 완전 가이드](/cells/english/java/integration-interoperability/how-to-save-pptx-from-excel-complete-guide-to-export-excel-s/)
- [Excel을 PowerPoint로 변환 – 전체 단계별 가이드](/cells/english/java/integration-interoperability/convert-excel-to-powerpoint-full-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}