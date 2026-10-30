---
category: general
date: 2026-08-17
description: C#로 Excel을 PowerPoint로 저장하기 – XLSX 파일을 변환하고 텍스트 상자를 편집 가능하게 만든 뒤 PPTX
  파일을 생성하는 단계별 가이드.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- how to convert xlsx
- make textbox editable
- how to edit textboxes
language: ko
lastmod: 2026-08-17
og_description: 전체 코드 예제와 함께 C#에서 Excel을 PowerPoint로 저장하는 방법. XLSX 변환, 텍스트 상자를 편집
  가능하게 만들기, 그리고 PPTX로 내보내는 방법을 배워보세요.
og_image_alt: Screenshot showing Excel data saved as a PowerPoint slide
og_title: C#에서 Excel을 PowerPoint로 저장하기 – 완전 변환 가이드
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Save Excel as PowerPoint with C# – step‑by‑step guide to convert XLSX
    files, make textboxes editable, and generate PPTX output.
  headline: How to save Excel as PowerPoint using C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel-to-PowerPoint
title: C#와 Aspose.Cells를 사용하여 Excel을 PowerPoint로 저장하는 방법
url: /ko/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# 및 Aspose.Cells를 사용하여 Excel을 PowerPoint로 저장하는 방법

.NET 프로젝트에서 **Excel을 PowerPoint로 저장**해야 하는 경우, 이 가이드는 완전하고 바로 실행할 수 있는 솔루션을 보여줍니다. XLSX 워크북을 로드하고, 시트의 모든 텍스트 상자를 편집 가능하게 만든 다음, 결과를 PPTX 파일로 내보내는 방법을 몇 줄의 C# 코드만으로 확인할 수 있습니다.

Excel을 PowerPoint로 변환하는 것은 보고 대시보드, 슬라이드 데크, 또는 자동 프레젠테이션 생성 등에서 흔히 요구되는 작업입니다. 이 튜토리얼에서는 **텍스트 상자를 프로그래밍 방식으로 편집하는 방법**도 다루어, 저장하기 전에 슬라이드 내용을 맞춤 설정할 수 있습니다.

## 사전 요구 사항

* .NET 6.0 (또는 이후) SDK가 설치되어 있음  
* Visual Studio 2022 또는 VS Code와 같은 개발 환경  
* Aspose.Cells for .NET 라이선스(또는 무료 평가 키) – [Aspose 웹사이트](https://products.aspose.com/cells/net/)에서 다운로드  
* `input.xlsx` 변환하려는 파일  

> **Pro tip:** 무료 평가 버전을 사용하면 출력 PPTX에 워터마크가 포함됩니다. 라이선스 버전을 사용하면 워터마크가 제거됩니다.

## 1단계: Aspose.Cells NuGet 패키지 설치

프로젝트 폴더에서 터미널을 열고 다음을 실행합니다:

```bash
dotnet add package Aspose.Cells
```

이 명령은 변환에 필요한 `Workbook`, `Worksheet`, `Shape` 클래스를 제공하는 `Aspose.Cells` 어셈블리를 추가합니다.

## 2단계: 콘솔 애플리케이션 스켈레톤 만들기

새 콘솔 프로젝트를 생성합니다(아직 없는 경우):

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
```

생성된 `Program.cs`를 다음 단계에 표시된 코드로 교체합니다.

## 3단계: 워크북을 로드하고 첫 번째 워크시트 선택

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Load the workbook from a file – adjust the path to your environment
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];
```

**왜 중요한가:** `Workbook`은 Excel 파일을 메모리로 읽어들이고, `Worksheet`는 시트의 셀, 차트, 도형에 접근할 수 있게 해줍니다. 첫 번째 워크시트는 보통 표시하려는 기본 보고서입니다.

## 4단계: 시트의 모든 텍스트 상자를 편집 가능하게 만들기

```csharp
        // Iterate through all shapes on the worksheet
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            // Check if the shape is a textbox (ShapeType.TextBox)
            if (shapeItem.Type == ShapeType.TextBox)
            {
                // The IsEditable property was added in Aspose.Cells 25.11
                shapeItem.TextBox.IsEditable = true;
            }
        }
```

**왜 필요한가:** 기본적으로 Excel에서 가져온 텍스트 상자는 PowerPoint에서 렌더링될 때 읽기 전용입니다. `IsEditable = true`로 설정하면 여러분이나 이후 PowerPoint 사용자가 슬라이드에서 직접 텍스트를 수정할 수 있습니다.

## 5단계: 워크북을 PowerPoint 프레젠테이션으로 저장

```csharp
        // Define the output path for the PPTX file
        string outputPath = @"YOUR_DIRECTORY\output.pptx";

        // Save the workbook as a PowerPoint presentation
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

**내부 동작:** `Workbook.Save`는 `SaveFormat.Pptx` 열거값을 감지하고, 행, 열, 차트 및 이제 편집 가능한 텍스트 상자를 포함한 Excel 시트 레이아웃을 PowerPoint 슬라이드 객체로 변환합니다.

## 전체 소스 코드 (실행 가능)

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook from a file
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Step 2: Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Make every textbox on the sheet editable (property added in version 25.11)
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            if (shapeItem.Type == ShapeType.TextBox)
            {
                shapeItem.TextBox.IsEditable = true;
            }
        }

        // Step 4: Save the workbook as a PowerPoint presentation
        string outputPath = @"YOUR_DIRECTORY\output.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

### 예상 출력

프로그램을 실행(`dotnet run`)하면 다음과 같은 출력이 표시됩니다:

```
Conversion complete. PPTX saved to: YOUR_DIRECTORY\output.pptx
```

Microsoft PowerPoint에서 `output.pptx`를 열면 원본 Excel 시트를 그대로 복제한 슬라이드가 표시됩니다. 모든 텍스트 상자는 더블 클릭으로 직접 편집할 수 있습니다.

## 일반적인 질문 및 예외 상황

| Question | Answer |
|----------|--------|
| **첫 번째 워크시트가 아니라 특정 워크시트를 변환할 수 있나요?** | 예. `workbook.Worksheets[0]`을 `workbook.Worksheets["SheetName"]` 또는 필요한 인덱스로 교체하면 됩니다. |
| **워크북에 여러 시트가 포함되어 있으면 어떻게 하나요?** | `workbook.Save`를 각 워크시트마다 호출하고 각각 별도의 PPTX 파일명을 지정하거나, Aspose.Slides의 `Presentation` 객체를 사용해 하나의 프레젠테이션으로 결합할 수 있습니다. |
| **차트가 유지되나요?** | Aspose.Cells가 Excel 차트를 PowerPoint 차트 객체로 자동 변환합니다. 추가 코드는 필요하지 않습니다. |
| **슬라이드 크기를 어떻게 변경하나요?** | `workbook.Save` 후에 Aspose.Slides를 사용해 생성된 PPTX를 로드하고 `Presentation.SlideSize`를 조정하면 됩니다. |
| **저장하기 전에 텍스트 상자 텍스트를 편집해야 하면 어떻게 하나요?** | 루프 내부에서 `shapeItem.TextBox.Text`에 접근해 수정한 뒤 `IsEditable = true`로 설정합니다. 예시: `shapeItem.TextBox.Text = "New title";` |

## 문제 해결 팁

* **“ShapeType.TextBox”를 찾을 수 없음** – Aspose.Cells 버전 25.11 이상을 사용하고 있는지 확인하세요; 이전 버전에는 `IsEditable` 속성이 없습니다.  
* **파일을 찾을 수 없음 오류** – `YOUR_DIRECTORY`가 절대 경로인지, 혹은 상대 경로가 올바른 위치를 가리키는지 확인하세요.  
* **라이선스가 적용되지 않음** – 워크북을 로드하기 전에 `License license = new License(); license.SetLicense("Aspose.Total.NET.lic");`를 호출하여 평가 워터마크를 제거하세요.

## 결론

이제 C#로 XLSX 워크북을 로드하고, 모든 텍스트 상자를 편집 가능하게 만든 뒤 PPTX로 내보내어 **Excel을 PowerPoint로 저장**하는 방법을 알게 되었습니다. 이 방법은 차트, 이미지, 셀 서식을 자동으로 처리하여 바로 프레젠테이션할 수 있는 슬라이드 덱을 제공합니다.

다음으로 **Aspose.Slides를 사용한 Excel을 PowerPoint로 변환**, **변환 후 텍스트 상자를 프로그래밍 방식으로 편집하는 방법**, 혹은 **여러 워크북을 일괄 처리**와 같은 관련 주제를 살펴보세요. 이들 각각은 여기서 다룬 핵심 단계에 기반하여 보고 워크플로를 더욱 자동화할 수 있습니다.

## 다음에 배워야 할 내용은?

다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료에는 단계별 설명과 함께 완전한 동작 코드 예제가 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [Aspose.Cells for .NET를 사용하여 Excel을 PowerPoint로 변환하는 방법: 완전 가이드](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [C#에서 피벗 테이블 복사 – Excel을 PPTX로 변환, 범위 복사 및 텍스트 상자 만들기](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Aspose.Cells .NET를 사용하여 Excel 파일을 여러 형식으로 저장하는 방법 (2023 가이드)](/cells/english/net/workbook-operations/aspose-cells-net-save-excel-formats/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}