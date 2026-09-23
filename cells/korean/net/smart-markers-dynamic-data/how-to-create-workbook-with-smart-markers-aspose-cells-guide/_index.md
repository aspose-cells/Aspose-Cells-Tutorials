---
category: general
date: 2026-02-23
description: Aspose.Cells를 사용하여 워크북을 만들고 JSON 배열로 마커를 추가하는 방법. 마커 추가, JSON 배열 사용,
  스마트 마커를 몇 분 안에 배우세요.
draft: false
keywords:
- how to create workbook
- how to add markers
- use json array
- smart markers aspose.cells
language: ko
og_description: Aspose.Cells를 사용하여 워크북을 만들고, 마커를 추가하며, JSON 배열을 사용하는 방법. 이 단계별 가이드는
  필요한 모든 것을 보여줍니다.
og_title: 스마트 마커를 사용한 워크북 만들기 – Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel Automation
title: 스마트 마커를 사용하여 워크북 만들기 – Aspose.Cells 가이드
url: /ko/net/smart-markers-dynamic-data/how-to-create-workbook-with-smart-markers-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 스마트 마커로 워크북 만들기 – Aspose.Cells 가이드

JSON 소스에서 데이터를 자동으로 채우는 **워크북을 만드는 방법**이 궁금하셨나요? 여러분만 그런 것이 아닙니다—개발자들은 특히 Aspose.Cells를 사용할 때 배열에서 값을 가져오는 마커를 어떻게 추가하느냐에 대해 자주 질문합니다. 좋은 소식은 스마트‑마커 개념을 이해하면 꽤 간단하다는 것입니다. 이 튜토리얼에서는 워크북을 생성하고, 마커를 추가하고, JSON 배열을 사용하며, Aspose.Cells에서 스마트 마커를 구성하는 과정을 단계별로 살펴보겠습니다. 이를 통해 실시간으로 Excel 파일을 생성할 수 있습니다.

다룰 내용은 모두 포함됩니다: 워크북 초기화, `MarkerCollection` 구축, JSON 배열 전달, “ArrayAsSingle” 플래그 토글, 그리고 마커 적용까지. 최종적으로 **A**, **B**, **C** 값을 자동으로 채워 넣는 완전한 C# 프로그램을 얻게 됩니다. 외부 서비스 없이 순수 Aspose.Cells만으로 구현됩니다.

## Prerequisites

- .NET 6.0 이상 (코드는 .NET Framework 4.6+에서도 동작)
- Aspose.Cells for .NET NuGet 패키지 (`Install-Package Aspose.Cells`)
- C# 문법에 대한 기본 이해 (처음이라면 코드 스니펫에 주석이 풍부하게 포함되어 있습니다)
- Visual Studio 또는 선호하는 IDE

이미 준비가 되었다면, 바로 시작해 보세요.

## Step 1: How to Create Workbook (Initialize the Excel File)

첫 번째로 필요한 것은 빈 워크북 객체입니다. 이는 Aspose.Cells가 나중에 데이터를 채워 넣을 빈 캔버스와 같습니다.

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];    // reference to the default sheet
```

> **왜 중요한가:** `Workbook`은 모든 Excel 작업의 진입점입니다. 이 없이는 스마트 마커를 연결하거나 파일을 저장할 수 없습니다. 워크북을 먼저 생성하면 이후 단계들을 위한 깨끗한 환경을 확보할 수 있습니다.

## Step 2: How to Add Markers – Initialise a Marker Collection

스마트 마커는 `MarkerCollection` 안에 존재합니다. 이 컬렉션에서 자리표시자(마커)와 이를 대체할 데이터를 정의합니다.

```csharp
        // Step 2: Initialise a collection for smart markers
        MarkerCollection smartMarkerCollection = new MarkerCollection();
```

> **프로 팁:** 여러 워크시트에 동일한 `MarkerCollection`을 재사용할 수 있지만, 시트당 하나씩 유지하면 디버깅이 더 쉬워집니다.

## Step 3: Use JSON Array – Add a Marker with JSON Data

이제 실제로 마커를 추가합니다. 자리표시자 `{SmartMarker}`는 제공한 JSON 배열로 대체됩니다. JSON은 문자열화된 배열이어야 하며, 예를 들어 `["A","B","C"]`와 같습니다.

```csharp
        // Step 3: Add a smart marker and provide replacement data (JSON array)
        smartMarkerCollection.Add("{SmartMarker}", "[\"A\",\"B\",\"C\"]");
```

> **설명:** `Add` 메서드는 두 개의 인수를 받습니다: 마커 텍스트와 데이터 소스. 여기서 데이터 소스는 JSON 배열이며, Aspose.Cells가 자동으로 파싱합니다. 이것이 스마트 마커와 **use json array**의 핵심입니다.

## Step 4: Configure the Marker – Treat the Array as a Single Value

기본적으로 Aspose.Cells는 JSON 배열을 개별 행으로 확장합니다. 배열 전체를 하나의 셀 값으로 취급하고 싶다면(드롭다운 목록이나 연결 문자열에 유용) `ArrayAsSingle` 플래그를 설정합니다.

```csharp
        // Step 4: Configure the marker to treat the array as a single value
        smartMarkerCollection["ArrayAsSingle"] = true;
```

> **사용 시점:** 배열을 하나의 셀에 표시하고 싶을 때(예: `"A,B,C"`), 이 플래그를 활성화합니다. 그렇지 않으면 Aspose.Cells가 각 요소를 별도의 행에 기록합니다.

## Step 5: Attach Markers to the Worksheet and Apply Them

마지막으로 마커 컬렉션을 워크시트에 바인딩하고, Aspose.Cells에게 자리표시자를 실제 데이터로 교체하도록 지시합니다.

```csharp
        // Step 5: Attach the marker collection to the worksheet and apply it
        worksheet.SmartMarkers.Add(smartMarkerCollection);
        worksheet.SmartMarkers.Apply();

        // Optional: write the placeholder into a cell so you can see the replacement
        worksheet.Cells["A1"].PutValue("{SmartMarker}");

        // Save the workbook to disk
        workbook.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook created successfully!");
    }
}
```

> **결과:** 프로그램을 실행하면 `SmartMarkerResult.xlsx` 파일의 `A1` 셀에 **A**(또는 `ArrayAsSingle`이 true인 경우 전체 배열) 값이 들어갑니다. 파일을 열어 확인해 보세요.

### Expected Output

| A |
|---|
| A |   *(`ArrayAsSingle`이 false인 경우 첫 번째 요소가 셀에 채워짐)*

`ArrayAsSingle = true`로 설정하면 셀 `A1`에 문자열 `["A","B","C"]`가 들어갑니다.

## Step 6: How to Add Markers – Advanced Scenarios (Optional)

*“마커가 하나 이상 필요하면 어떻게 할까?”* 라고 생각할 수 있습니다. 답은 간단합니다: `Add`를 다시 호출하면 됩니다.

```csharp
        smartMarkerCollection.Add("{SecondMarker}", "[{\"Name\":\"John\"},{\"Name\":\"Jane\"}]");
        // You can also control each marker individually:
        smartMarkerCollection["SecondMarker"] = false; // expand into rows
```

> **왜 동작하는가:** 각 마커는 독립적으로 작동하므로 같은 워크시트 내에서 “배열을 단일값으로”와 “행으로 확장”을 혼합해서 사용할 수 있습니다. 이 유연성이 **smart markers aspose.cells**의 특징입니다.

## Common Pitfalls & How to Avoid Them

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| 마커가 교체되지 않음 | 자리표시자 텍스트 누락 또는 오타 | 셀에 정확한 마커 문자열(`{SmartMarker}`)이 있는지 확인 |
| JSON 파싱 실패 | 잘못된 JSON 구문(따옴표 누락) | JSON 검증기를 사용하거나 C# 문자열에서 따옴표를 이중 이스케이프 |
| 배열이 예상치 않게 확장됨 | `ArrayAsSingle`이 기본값 `false` 그대로 | 특정 마커에 대해 `["ArrayAsSingle"] = true` 설정 |
| 워크북이 빈 채로 저장됨 | `Apply()`를 `Save()` 전에 호출하지 않음 | `worksheet.SmartMarkers.Apply()`를 저장 전에 항상 호출 |

## Full Working Example (Copy‑Paste Ready)

아래는 콘솔 앱에 바로 붙여넣을 수 있는 전체 프로그램입니다. 추가 파일은 필요하지 않습니다.

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Initialise a collection for smart markers
        MarkerCollection smartMarkerCollection = new MarkerCollection();

        // Add a smart marker and provide replacement data (JSON array)
        smartMarkerCollection.Add("{SmartMarker}", "[\"A\",\"B\",\"C\"]");

        // Configure the marker to treat the array as a single value
        smartMarkerCollection["ArrayAsSingle"] = true;

        // Attach the marker collection to the worksheet and apply it
        worksheet.SmartMarkers.Add(smartMarkerCollection);
        worksheet.SmartMarkers.Apply();

        // Place the marker in a cell so we can see the replacement
        worksheet.Cells["A1"].PutValue("{SmartMarker}");

        // Save the workbook
        workbook.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook created successfully!");
    }
}
```

프로그램을 실행하고 `SmartMarkerResult.xlsx`를 열면 JSON 배열(또는 첫 번째 요소)이 셀 **A1**에 깔끔하게 배치된 것을 확인할 수 있습니다.

## Next Steps: Extending the Solution

이제 **워크북을 만드는 방법**, **마커를 추가하는 방법**, 그리고 Aspose.Cells와 함께 **json 배열을 사용하는 방법**을 알게 되었으니, 다음과 같은 확장 아이디어를 고려해 보세요:

1. **다중 워크시트** – 워크시트 리스트를 순회하면서 각 시트에 다른 마커 컬렉션을 연결합니다.
2. **동적 JSON** – 웹 API(`HttpClient`)에서 JSON을 가져와 `smartMarkerCollection.Add`에 직접 전달합니다.
3. **출력 스타일링** – 마커 적용 후 셀 서식(폰트, 색상)을 지정해 보고서를 더욱 깔끔하게 만듭니다.
4. **다양한 내보내기 형식** – `workbook.Save("file.pdf")`와 같이 저장 형식을 PDF, CSV, HTML 등으로 변경합니다.

이 모든 주제는 **smart markers aspose.cells**와 직결되므로, 방금 배운 핵심 개념을 그대로 활용할 수 있습니다.

## Conclusion

우리는 **워크북을 만드는 방법**, **마커를 추가하는 방법**, 그리고 Aspose.Cells 스마트 마커와 함께 **json 배열을 사용하는 방법**을 처음부터 끝까지 살펴보았습니다. 전체 실행 가능한 예제는 `Workbook` 초기화부터 최종 파일 저장까지 전체 흐름을 보여줍니다. `ArrayAsSingle` 플래그를 토글하면 JSON 데이터가 Excel에 표시되는 방식을 세밀하게 제어할 수 있어 다양한 보고 시나리오에 적용하기 쉽습니다.

코드를 직접 실행해 보고, JSON을 변형하고, 추가 마커를 실험해 보세요. 이 빌딩 블록을 마스터하면 복잡한 Excel 보고서를 손쉽게 생성할 수 있습니다. 질문이 있거나 멋진 사용 사례를 공유하고 싶다면 아래에 댓글을 남겨 주세요—행복한 코딩 되세요! 

![스마트 마커로 워크북을 만드는 방법을 보여주는 다이어그램](https://example.com/images/create-workbook-smart-markers.png "스마트 마커로 Aspose.Cells 워크북 만들기")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}