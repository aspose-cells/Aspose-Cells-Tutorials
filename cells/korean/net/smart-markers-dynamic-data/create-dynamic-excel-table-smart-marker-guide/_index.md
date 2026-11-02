---
category: general
date: 2026-05-23
description: 템플릿과 JSON 데이터를 사용하여 동적 엑셀 테이블을 만들세요. 엑셀 템플릿을 로드하고, 엑셀 보고서를 자동화하며, JSON으로부터
  엑셀을 빠르게 채우는 방법을 배우세요.
draft: false
keywords:
- create dynamic excel table
- load excel template
- automate excel report
- populate excel from json
- generate excel report json
language: ko
og_description: 템플릿과 JSON을 사용하여 몇 분 안에 동적 엑셀 테이블을 만들 수 있습니다. 이 튜토리얼에서는 엑셀 템플릿을 로드하고,
  엑셀 보고서를 자동화하며, JSON으로 엑셀을 채우는 방법을 보여줍니다.
og_title: 동적 엑셀 테이블 만들기 – 스마트 마커 가이드
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create dynamic excel table using a template and JSON data. Learn how
    to load excel template, automate excel report, and populate excel from json quickly.
  headline: Create Dynamic Excel Table – Smart Marker Guide
  type: TechArticle
tags:
- Excel
- Smart Markers
- JSON
- .NET
title: 동적 엑셀 테이블 만들기 – 스마트 마커 가이드
url: /ko/net/smart-markers-dynamic-data/create-dynamic-excel-table-smart-marker-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 동적 Excel 테이블 만들기 – Smart Marker 가이드

데이터 세트의 각 레코드마다 자동으로 확장되는 **동적 Excel 테이블 만들기**가 필요했던 적이 있나요? 여러분만 그런 것이 아닙니다. 월간 판매 대시보드나 고객별 인보이스 팩을 만들 때, **JSON에서 Excel을 채우기** 기능을 사용하면 무한 반복 코드를 작성하지 않아도 몇 시간을 절약할 수 있습니다.

이 튜토리얼에서는 **Excel 템플릿 로드** 방법, Smart Marker 삽입, JSON 제공, 그리고 최종적으로 **Excel 보고서 자동화** 생성까지 전체적인 실습 솔루션을 단계별로 안내합니다. 끝까지 따라오면 단일 JSON 페이로드로 깔끔한 Excel 워크북을 생성하는 실행 가능한 .NET 프로젝트를 얻게 됩니다.

---

## 필요 사항

- **Aspose.Cells for .NET** (또는 Smart Markers를 지원하는 라이브러리). 예제는 버전 24.5를 사용하지만 최신 릴리스라면 모두 작동합니다.
- Visual Studio 2022 (또는 선호하는 C# IDE).
- 제어 가능한 폴더에 배치한 간단한 Excel 템플릿 파일 (`template.xlsx`).
- `Customers`라는 컬렉션을 포함하는 JSON 문자열.

이것만 있으면 됩니다—추가 서비스나 데이터베이스 연결 없이 순수 코드만으로 가능합니다.

## 단계 1: 템플릿 워크북 만들기 – Excel 템플릿 로드

먼저 **Excel 템플릿 로드**를 메모리로 수행합니다. 템플릿은 특수 플레이스홀더가 행을 반복할 위치를 처리기에 알려주는 캔버스로 생각하면 됩니다.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

// Load the template workbook (make sure the path is correct)
Workbook workbook = new Workbook(@"C:\Reports\template.xlsx");

// Grab the first worksheet – this is where our Smart Marker lives
Worksheet worksheet = workbook.Worksheets[0];
```

> **왜 중요한가:** 템플릿을 한 번만 로드하면 파일 I/O를 최소화하고 여러 보고서에 동일한 레이아웃을 재사용할 수 있습니다. 또한 Smart Marker 로직을 나머지 코드와 분리하여 관심사의 명확한 구분을 제공합니다.

## 단계 2: Smart Marker 삽입 – 동적 Excel 테이블 만들기

이제 `Customers` 컬렉션의 각 항목마다 테이블을 반복하도록 **Smart Marker**를 삽입합니다. 구문 `${Customers.RepeatWorksheet}`는 Aspose.Cells에 고객마다 전체 워크시트를 복제하도록 지시합니다.

```csharp
// Place the Smart Marker in cell A1 (top‑left corner)
worksheet.Cells[0, 0].PutValue("${Customers.RepeatWorksheet}");
```

> **팁:** 전체 워크시트가 아니라 행만 반복하면 테이블 첫 번째 행에 `${Customers.Repeat}`를 사용하세요. 워크시트 수준의 반복은 각 고객에게 별도의 탭을 제공할 때 유용합니다.

## 단계 3: SmartMarkerProcessor 준비 – Excel 보고서 자동화

마커가 설정되면 `SmartMarkerProcessor`를 생성합니다. 이 객체는 JSON과 Excel 템플릿 간의 데이터 바인딩을 조정합니다.

```csharp
// Initialize the processor with the workbook that contains the marker
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
```

프로세서는 가볍고, 원한다면 여러 JSON 페이로드에 재사용할 수 있습니다.

## 단계 4: JSON 데이터 제공 – JSON에서 Excel 채우기

여기서 마법이 일어납니다. 고객 배열을 포함하는 JSON 문자열을 제공한다. 각 고객은 `Name`, `Email`, `Total`과 같은 필드를 가질 수 있습니다.

```csharp
// Sample JSON data – in a real scenario you might read this from a file or API
string customersJson = @"
{
  ""Customers"": [
    { ""Name"": ""Acme Corp"", ""Email"": ""contact@acme.com"", ""Total"": 12500 },
    { ""Name"": ""Globex"", ""Email"": ""sales@globex.com"", ""Total"": 9800 },
    { ""Name"": ""Initech"", ""Email"": ""info@initech.com"", ""Total"": 15400 }
  ]
}";

// Apply the JSON to the processor – this populates the workbook
processor.ApplyJson(customersJson);
```

> **왜 JSON인가?** JSON은 언어에 구애받지 않으며 API, 데이터베이스, 혹은 수동 입력에서도 쉽게 생성할 수 있습니다. `ApplyJson`을 사용하면 객체를 수동으로 매핑할 필요 없이 프로세서가 복잡한 작업을 수행합니다.

## 단계 5: 결과 저장 – Excel 보고서 JSON 생성

마지막으로, 채워진 워크북을 디스크에 저장합니다. 출력 파일에는 이제 각 고객마다 별도의 워크시트가 포함되며, JSON 데이터가 채워져 있습니다.

```csharp
// Save the filled workbook – choose a path that makes sense for your app
workbook.Save(@"C:\Reports\output.xlsx");
```

### 예상 출력

- **output.xlsx**에는 `Sheet1`, `Sheet2`, `Sheet3`(또는 템플릿에서 사용하는 명명 규칙)이라는 이름의 세 개 워크시트가 생성됩니다.
- 각 시트는 단일 고객의 `Name`, `Email`, `Total` 값을 표시합니다.
- `template.xlsx`에서 설계한 레이아웃(헤더, 스타일, 수식)이 모든 생성된 시트에 그대로 유지됩니다.

## 전체 작업 예제

아래는 완전한 실행 가능한 프로그램입니다. 콘솔 앱에 복사‑붙여넣기하고 파일 경로를 조정한 뒤 **F5**를 눌러 실행하세요.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace DynamicExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the template workbook
            string templatePath = @"C:\Reports\template.xlsx";
            Workbook workbook = new Workbook(templatePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Insert the Smart Marker that repeats the worksheet per customer
            worksheet.Cells[0, 0].PutValue("${Customers.RepeatWorksheet}");

            // 3️⃣ Create the SmartMarkerProcessor
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

            // 4️⃣ JSON data containing a collection of customers
            string customersJson = @"
            {
                ""Customers"": [
                    { ""Name"": ""Acme Corp"", ""Email"": ""contact@acme.com"", ""Total"": 12500 },
                    { ""Name"": ""Globex"", ""Email"": ""sales@globex.com"", ""Total"": 9800 },
                    { ""Name"": ""Initech"", ""Email"": ""info@initech.com"", ""Total"": 15400 }
                ]
            }";

            // Apply the JSON – this populates the workbook dynamically
            processor.ApplyJson(customersJson);

            // 5️⃣ Save the generated report
            string outputPath = @"C:\Reports\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"✅ Dynamic Excel report generated at: {outputPath}");
        }
    }
}
```

프로그램을 실행하고 `output.xlsx`를 열면 **동적 Excel 테이블 만들기**가 작동하는 것을 확인할 수 있습니다—각 고객마다 설계한 대로 완전히 서식이 적용된 시트가 생성됩니다.

## 일반 질문 및 엣지 케이스

| Question | Answer |
|----------|--------|
| *JSON에 중첩 객체가 있으면 어떻게 하나요?* | Smart Markers는 JSON 계층 구조가 일치하는 한 점 표기법(`${Customers.Address.City}`)을 지원합니다. |
| *생성된 워크시트 이름을 고객 이름으로 지정할 수 있나요?* | 예—워크시트 이름 셀에 `${Customers.Name}`와 같은 마커를 추가하거나 `processor.ApplyJson(customersJson, "Customers")`와 명명 패턴을 사용하세요. |
| *10 k+ 행과 같은 대용량 데이터 세트는 어떻게 처리하나요?* | 프로세서는 데이터를 효율적으로 스트리밍하지만 메모리를 주시하세요. 성능 한계에 도달하면 보고서를 여러 파일로 나누는 것을 고려하십시오. |
| *Aspose.Cells에 라이선스가 필요합니까?* | 무료 평가판으로 테스트는 가능하지만, 라이선스 버전은 평가 워터마크를 제거하고 전체 기능을 제공합니다. |
| *이 방법을 .NET Core와 함께 사용할 수 있나요?* | 물론입니다—Aspose.Cells는 .NET 6/7/8을 지원합니다. NuGet 패키지를 참조하면 코드가 동일하게 유지됩니다. |

## 프로덕션 준비 구현을 위한 팁

- **JSON 검증**을 `ApplyJson`에 전달하기 전에 수행하세요. 형식이 잘못된 페이로드는 `JsonParseException`을 발생시킵니다.
- 짧은 시간에 많은 보고서를 생성한다면 **템플릿 캐시**를 사용하세요; 디스크에서 반복 로드하는 것은 불필요한 I/O입니다.
- 멀티스레드 웹 서비스에서 실행한다면 처리 중에 **워크북 잠금**을 걸어 경쟁 조건을 방지하세요.
- `workbook.Save` 주변에 **오류 처리**를 추가하여 권한 문제나 파일 잠금 상황을 우아하게 처리하세요.
- 템플릿에서 스타일을 맞춤화(조건부 서식, 수식)하여 생성된 시트가 추가 코드 없이도 비즈니스 로직을 유지하도록 하세요.

## 결론

이제 템플릿, Smart Markers, JSON 데이터를 활용해 **동적 Excel 테이블 만들기**를 수행하는 견고한 엔드‑투‑엔드 패턴을 갖추었습니다. **Excel 템플릿 로드**, 반복 마커 삽입, **JSON에서 Excel 채우기**를 통해 몇 줄의 C# 코드만으로 **Excel 보고서 자동화**를 구현할 수 있습니다.

다음 단계는? 동적 테이블을 참조하는 차트를 추가하거나 Aspose.Words를 사용해 동일한 JSON을 PDF로 내보내 보세요. 또한 데이터베이스 쿼리에서 **Excel 보고서 JSON 생성**을 실험해 전체 흐름을 완성할 수 있습니다.

## 관련 튜토리얼

- [Aspose.Cells for .NET을 사용하여 Excel에서 피벗 테이블 만들기](/cells/english/net/pivot-tables/create-pivot-table/)
- [Aspose.Cells for .NET을 사용하여 Excel에서 동적 라인 차트 만들기: 단계별 가이드](/cells/english/net/charts-graphs/create-line-charts-excel-aspose-cells-dotnet/)
- [Aspose.Cells for .NET을 사용하여 Excel에서 체크박스 만들기 | 데이터 검증 튜토리얼](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}