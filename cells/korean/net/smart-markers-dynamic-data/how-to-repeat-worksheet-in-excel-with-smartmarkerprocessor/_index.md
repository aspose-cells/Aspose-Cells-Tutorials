---
category: general
date: 2026-11-19
description: 배열 데이터를 사용해 Excel을 채우면서 워크시트를 반복하는 방법. 몇 단계만에 여러 워크시트를 생성하고 리스트에서 워크시트를
  채우는 방법을 배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to repeat worksheet
- populate excel with array
- generate multiple worksheets
- populate worksheet from list
language: ko
lastmod: 2026-11-19
og_description: SmartMarkerProcessor를 사용하여 워크시트를 반복하는 방법. 이 가이드를 따라 배열 데이터로 Excel을
  채우고, 여러 워크시트를 생성하며, 리스트에서 워크시트를 채우세요.
og_image_alt: Screenshot showing repeated worksheets in an Excel workbook after processing
og_title: Excel에서 워크시트를 반복하는 방법 – 단계별 가이드
schemas:
- author: GroupDocs
  dateModified: '2026-11-19'
  description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  headline: How to repeat worksheet in Excel with SmartMarkerProcessor
  type: TechArticle
- description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  name: How to repeat worksheet in Excel with SmartMarkerProcessor
  steps:
  - name: Expected output
    text: 'When you open the resulting workbook, you should see:'
  - name: Empty or null arrays
    text: 'If `Dept` is null or empty, the processor will not create any additional
      worksheets. To avoid a completely blank workbook, you can add a guard:'
  - name: Custom worksheet names
    text: 'The default naming scheme may not suit every reporting requirement. After
      processing, rename each sheet using a loop:'
  - name: Populating additional columns
    text: 'If you need to **populate excel with array** values beyond a single marker,
      extend the data object:'
  type: HowTo
tags:
- Excel automation
- SmartMarkerProcessor
- .NET
title: SmartMarkerProcessor를 사용하여 Excel에서 워크시트를 반복하는 방법
url: /ko/net/smart-markers-dynamic-data/how-to-repeat-worksheet-in-excel-with-smartmarkerprocessor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel에서 SmartMarkerProcessor를 사용해 워크시트 반복하기

Excel 보고서를 생성할 때 **워크시트를 반복하는 방법**이 필요하다면, 이 가이드는 완전하고 실행 가능한 솔루션을 제공합니다. 튜토리얼을 마치면 **배열 데이터로 Excel 채우기**, **다중 워크시트 생성**, **리스트에서 워크시트 채우기**를 SmartMarkerProcessor 라이브러리를 사용해 수행할 수 있게 됩니다.

워크시트 반복은 부서, 지역, 혹은 기간마다 별도의 탭이 필요할 때 흔히 요구되는 기능입니다. 아래 예시는 정확한 단계들을 보여주며, 각 설정이 왜 중요한지 설명하고, 빈 리스트나 사용자 지정 명명과 같은 엣지 케이스도 다룹니다.

## 사전 요구 사항

시작하기 전에 다음이 준비되어 있는지 확인하세요:

- .NET 6.0 이상이 설치되어 있음
- `SmartMarkerProcessor`를 포함하는 **GroupDocs.Viewer**(또는 동등한) NuGet 패키지에 대한 참조
- `${repeat:Dept}`와 같은 마커가 반복하고자 하는 행에 배치된 Excel 템플릿 워크북(`.xlsx`)
- C#와 LINQ에 대한 기본적인 이해(선택 사항이지만 도움이 됨)

추가 서드파티 라이브러리는 필요하지 않습니다.

## 1단계: SmartMarkerProcessor 인스턴스 생성

프로세서는 마커 교체와 워크시트 복제를 조정합니다. 인자를 전달하지 않고 인스턴스를 생성하면 기본 옵션이 사용됩니다.

```csharp
// Step 1: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

프로세서를 일찍 생성하면 데이터를 적용하기 전에 전역 옵션을 설정할 수 있습니다. 이는 **워크시트를 반복하는 방법**을 올바르게 수행하기 위한 기반이 됩니다.

## 2단계: 워크시트 반복 활성화

기본적으로 프로세서는 현재 시트에서만 마커를 교체합니다. `RepeatWorksheet`를 `true`로 설정하면 데이터 컬렉션의 각 항목에 대해 전체 워크시트를 복제하도록 엔진에 지시합니다.

```csharp
// Step 2: Enable worksheet repetition for the ${repeat:Dept} marker
processor.Options.RepeatWorksheet = true;
```

이 옵션을 활성화하는 것이 **다중 워크시트 생성**의 핵심이며, 프로세서는 `Dept` 배열의 각 요소마다 새로운 탭을 만들고 원본 서식을 유지합니다.

## 3단계: 데이터 소스를 배열 또는 리스트로 준비

SmartMarkerProcessor는 모든 열거형과 함께 사용할 수 있지만, 배열을 사용하면 **리스트에서 워크시트 채우기**를 할 때 의도가 명확해집니다. 여기서는 `Dept` 속성이 문자열 배열을 보유하는 익명 객체를 생성합니다.

```csharp
// Step 3: Prepare the data source with a list of departments
var data = new { Dept = new[] { "HR", "IT", "Finance" } };
```

이미 `List<string>`이 있다면 그대로 전달해도 됩니다; 프로세서는 동일하게 처리합니다. 중요한 점은 속성 이름(`Dept`)이 템플릿의 마커 `${repeat:Dept}`와 일치한다는 것입니다.

## 4단계: 템플릿 워크시트 로드

`ExcelPackage`(EPPlus) 혹은 `Workbook` 객체가 있다고 가정하고, 반복하고자 하는 워크시트를 가져옵니다. 변수 `ws`가 해당 시트를 나타냅니다.

```csharp
// Example using EPPlus to load the template workbook
using var package = new OfficeOpenXml.ExcelPackage(new FileInfo("Template.xlsx"));
var ws = package.Workbook.Worksheets[0]; // first worksheet
```

다른 라이브러리(예: ClosedXML)를 선호한다면 동일한 원칙이 적용됩니다: 필요한 인터페이스를 구현하는 워크시트 객체를 얻으면 됩니다.

## 5단계: 데이터와 함께 워크시트 처리

이제 템플릿에 데이터를 적용합니다. 프로세서는 각 부서마다 워크시트를 복제하고, `${repeat:Dept}` 마커를 실제 부서 이름으로 교체하며, 시트의 다른 부분은 그대로 둡니다.

```csharp
// Step 5: Apply the data to the template worksheet (ws)
processor.Process(ws, data);
```

`Process`가 완료되면 `ws`는 여러 워크시트 중 첫 번째가 됩니다—부서당 하나씩. 원본 시트 이름은 유지되고, 복제본은 순차적인 접미사(예: “Sheet1 (1)”, “Sheet1 (2)”)를 받습니다. 필요에 따라 사용자 지정 명명 규칙을 적용해 이름을 바꿀 수 있습니다.

### 예상 출력

완성된 워크북을 열면 다음과 같이 표시됩니다:

- **Sheet1** – 원본 템플릿(대개 비워두거나 마스터로 사용)
- **Sheet1 (1)** – “HR”로 채워짐
- **Sheet1 (2)** – “IT”로 채워짐
- **Sheet1 (3)** – “Finance”로 채워짐

각 시트는 동일한 레이아웃을 갖지만 `${repeat:Dept}`가 있던 위치에 부서명이 대입됩니다.

## 엣지 케이스 처리

### 빈 배열 또는 null 배열

`Dept`가 null이거나 비어 있으면 프로세서는 추가 워크시트를 만들지 않습니다. 완전히 빈 워크북이 되는 것을 방지하려면 방어 코드를 추가하세요:

```csharp
if (data.Dept != null && data.Dept.Any())
{
    processor.Process(ws, data);
}
else
{
    // Optionally write a warning or keep the original sheet unchanged
}
```

### 사용자 지정 워크시트 이름

기본 명명 방식이 모든 보고 요구에 맞지는 않을 수 있습니다. 처리 후 루프를 사용해 각 시트 이름을 바꾸세요:

```csharp
for (int i = 1; i <= data.Dept.Length; i++)
{
    var sheet = package.Workbook.Worksheets[i]; // index 0 is the original
    sheet.Name = data.Dept[i - 1]; // use department name as tab title
}
```

### 추가 열 채우기

단일 마커 외에 **배열로 Excel 채우기** 값을 더 채워야 한다면 데이터 객체를 확장합니다:

```csharp
var data = new
{
    Dept = new[]
    {
        new { Name = "HR", Headcount = 12 },
        new { Name = "IT", Headcount = 25 },
        new { Name = "Finance", Headcount = 8 }
    }
};
```

그런 다음 템플릿 마커를 `${repeat:Dept.Name}` 및 `${repeat:Dept.Headcount}`로 조정합니다. 프로세서는 각 부서마다 행을 반복하고 두 열을 모두 채웁니다.

## 전체 작동 예제

아래는 템플릿 로드부터 최종 워크북 저장까지 전체 흐름을 보여주는 독립 실행형 콘솔 애플리케이션입니다.

```csharp
using System;
using System.IO;
using OfficeOpenXml;               // Install-Package EPPlus
using GroupDocs.Viewer.Markup;    // SmartMarkerProcessor namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Create processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 2️⃣ Enable worksheet repetition
        processor.Options.RepeatWorksheet = true;

        // 3️⃣ Define data source (array of departments)
        var data = new { Dept = new[] { "HR", "IT", "Finance" } };

        // 4️⃣ Load template workbook (ensure Template.xlsx exists)
        var fileInfo = new FileInfo("Template.xlsx");
        using var package = new ExcelPackage(fileInfo);
        var ws = package.Workbook.Worksheets[0]; // first sheet contains ${repeat:Dept}

        // 5️⃣ Process template
        processor.Process(ws, data);

        // Optional: rename generated sheets
        for (int i = 1; i <= data.Dept.Length; i++)
        {
            var sheet = package.Workbook.Worksheets[i];
            sheet.Name = data.Dept[i - 1];
        }

        // Save the result
        var output = new FileInfo("Result.xlsx");
        package.SaveAs(output);

        Console.WriteLine("Workbook generated with repeated worksheets.");
    }
}
```

**핵심 섹션 설명**

- **프로세서 생성** – 마커를 해석할 엔진을 설정합니다.
- **RepeatWorksheet 옵션** – *워크시트를 반복하는 방법*을 구현하는 핵심 기능을 활성화합니다.
- **데이터 소스** – **배열로 Excel 채우기**를 만족시키기 위해 `new[]` 배열을 사용합니다.
- **템플릿 로드** – 워크시트 객체를 얻는 일반적인 방법을 보여줍니다.
- **처리** – 복제와 데이터 삽입을 한 번에 수행합니다.
- **이름 바꾸기** – 일반적인 “(1)”, “(2)” 이름을 의미 있는 제목으로 바꾸는 방법을 보여주며, 이는 **다중 워크시트 생성** 후 흔히 필요한 작업입니다.

이 프로그램을 실행하면 `Result.xlsx` 파일에 세 개의 부서별 탭이 생성되며, 각각이 배열에서 채워집니다.

## 흔히 발생하는 실수와 팁

- **마커 철자** – 마커는 속성 이름과 정확히 일치해야 합니다(`${repeat:Dept}`). 오타가 있으면 반복이 작동하지 않습니다.
- **워크시트 인덱스** – 처리 후 원본 시트는 인덱스 0에 남고, 생성된 시트가 순차적으로 뒤에 배치됩니다. 인덱스를 잘못 지정하면 잘못된 탭을 이름 바꾸게 될 수 있습니다.
- **대용량 데이터** – 수백 개의 워크시트를 생성하면 파일 크기가 급격히 증가합니다. 성능 문제가 발생하면 보고서를 분할하거나 하나의 시트에 그룹화된 섹션을 사용하는 것을 고려하세요.
- **스레드 안전성** – `SmartMarkerProcessor`는 스레드‑안전하지 않습니다. 여러 워크북을 병렬 처리해야 한다면 스레드당 별도 인스턴스를 생성하세요.

## 결론

이제 SmartMarkerProcessor를 사용해 Excel에서 **워크시트를 반복하는 방법**, **배열로 Excel 채우기**, **다중 워크시트 생성**, **리스트에서 워크시트 채우기**를 효율적으로 수행할 수 있습니다. 전체 예제는 모든 개념을 하나로 묶으며, 선택적인 이름 바꾸기 단계는 깔끔하고 사용자 친화적인 탭 이름을 만들 수 있게 해줍니다.

다음 단계로 살펴볼 내용:

- 복합 객체(중첩 컬렉션)를 사용한 **리스트에서 워크시트 채우기**
- 워크시트 복제 후 조건부 서식 적용
- 생성된 워크북을 PDF 또는 CSV로 내보내어 다운스트림에서 활용

코드를 자신의 보고 시나리오에 맞게 자유롭게 변형하고, Excel 워크북 자동화에 자신감을 가지세요!


## 다음에 배워야 할 내용


다음 튜토리얼들은 이 가이드에서 다룬 기술을 기반으로 하는 밀접한 주제를 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 포함해 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용하도록 돕습니다.

- [How to Repeat Worksheets – Complete Guide for Excel Automation](/cells/english/net/smart-markers-dynamic-data/how-to-repeat-worksheets-complete-guide-for-excel-automation/)
- [Create Worksheet Per Item – How to Repeat Worksheet in C#](/cells/english/net/worksheet-operations/create-worksheet-per-item-how-to-repeat-worksheet-in-c/)
- [How to expand array in Excel and populate a template](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}