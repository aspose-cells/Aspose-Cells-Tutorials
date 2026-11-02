---
category: general
date: 2026-09-21
description: C#에서 SmartMarkerOptions의 ArrayAsSingle 옵션을 설정하여 JSON 배열을 Excel 워크북의 단일
  셀 값으로 내보냅니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- configure smartmarkeroptions arrayassingle
- Aspose.Cells smart markers
- export JSON array
- C# DataTable
- Workbook ProcessSmartMarkers
language: ko
lastmod: 2026-09-21
og_description: C#에서 SmartMarkerOptions ArrayAsSingle을 구성하여 JSON 배열을 단일 셀 값으로 내보냅니다.
  전체 단계별 솔루션을 확인하세요.
og_image_alt: Screenshot of an Excel sheet showing a JSON array stored in a single
  cell after using SmartMarkerOptions
og_title: C#에서 SmartMarkerOptions ArrayAsSingle 구성 – 전체 가이드
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Configure SmartMarkerOptions ArrayAsSingle in C# to export JSON arrays
    as a single cell value in an Excel workbook.
  headline: Configure SmartMarkerOptions ArrayAsSingle in C# for JSON arrays
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: C#에서 JSON 배열을 위한 SmartMarkerOptions ArrayAsSingle 설정
url: /ko/net/smart-markers-dynamic-data/configure-smartmarkeroptions-arrayassingle-in-c-for-json-arr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 JSON 배열을 위한 SmartMarkerOptions ArrayAsSingle 구성

Aspose.Cells를 사용하여 Excel 파일을 생성할 때 **SmartMarkerOptions ArrayAsSingle**을 구성해야 하는 경우, 이 가이드는 정확히 어떻게 수행하는지 보여줍니다. JSON 배열을 여러 행에 퍼뜨리는 대신 하나의 셀에 그대로 유지하는 방법을 확인할 수 있습니다.

스프레드시트에서 JSON 데이터를 다룰 때는 평탄화된 보기와 압축된 표현 사이에서 선택해야 하는 경우가 많습니다. 태그 목록이나 식별자 집합을 저장하는 많은 보고 시나리오에서 전체 JSON 문자열을 단일 셀에 유지하고 싶습니다. `SmartMarkerOptions`의 **ArrayAsSingle** 플래그가 이를 가능하게 합니다.

이 튜토리얼에서 여러분은:

* JSON 배열을 열에 보관하는 `DataTable`을 생성합니다.
* Excel 워크시트에 Smart Markers를 배치합니다.
* JSON 배열이 단일 셀 값으로 처리되도록 **SmartMarkerOptions ArrayAsSingle**을 **구성**합니다.
* 마커를 처리하고 워크북을 저장합니다.
* 결과를 검증합니다.

> **Prerequisites** – Aspose.Cells for .NET 라이브러리(v23.12 이상)와 .NET 개발 환경(Visual Studio 2022 권장)이 필요합니다. C# 및 DataTable에 대한 기본 지식이 전제됩니다.

---

## Step 1: Prepare the data source with a JSON array

먼저, 서비스나 데이터베이스에서 받을 데이터를 모방하는 `DataTable`을 만듭니다. **Names** 열에는 이름 배열을 나타내는 JSON‑인코딩 문자열이 들어 있습니다.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable dataTable = new DataTable();
dataTable.Columns.Add("Id", typeof(int));
dataTable.Columns.Add("Names", typeof(string));

// Store the JSON array as a plain string
dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");
```

*Why this step?*  
Smart Markers는 .NET 객체에서 직접 데이터를 읽습니다. JSON 배열을 문자열 열에 배치하면 정확한 JSON 구문을 보존할 수 있으며, 이후 셀에 변경 없이 기록됩니다.

---

## Step 2: Insert Smart Markers into a new workbook

새 워크북을 만들고 첫 번째 워크시트를 선택한 뒤, 전체 테이블과 특정 **Names** 열을 참조하는 Smart Markers를 작성합니다.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Smart marker for the entire table (optional, shown for completeness)
worksheet.Cells["A1"].PutValue("&=dataTable");

// Smart marker that targets only the Names column
worksheet.Cells["A2"].PutValue("&=dataTable.Names");
```

마커 `&=dataTable.Names`는 Aspose.Cells에 `dataTable`의 **Names** 열 값을 셀에 대체하도록 지시합니다. 행이 하나뿐이므로 마커는 한 번만 처리됩니다.

---

## Step 3: **Configure SmartMarkerOptions ArrayAsSingle**

기본적으로 Aspose.Cells는 배열과 같은 문자열을 별도의 행으로 확장합니다. `ArrayAsSingle`을 `true`로 설정하면 이 동작을 무시하고 전체 JSON 문자열을 단일 셀에 유지합니다.

```csharp
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    // Export the JSON array as a single cell value
    ArrayAsSingle = true
};
```

*Why enable `ArrayAsSingle`?*  
`ArrayAsSingle`이 `false`이면 엔진은 `["Alice","Bob"]`을 두 개의 별도 값으로 해석하여 인접한 행에 기록합니다. `true`로 설정하면 문자열을 원자값으로 취급하게 되며, 이는 Excel 내부에서 JSON 형식을 보존하는 데 필수적입니다.

---

## Step 4: Process the Smart Markers with the configured options

이제 방금 구성한 옵션 객체를 전달하여 Smart Marker 엔진을 실행합니다.

```csharp
// Process smart markers using the custom options
workbook.ProcessSmartMarkers(smartMarkerOptions);
```

처리 중에 Aspose.Cells는 `dataTable`을 읽고 마커를 적용하며 `ArrayAsSingle` 플래그를 준수하여 JSON 배열을 그대로 둡니다.

---

## Step 5: Save the workbook and verify the result

마지막으로 워크북을 디스크에 저장합니다. 생성된 파일을 Excel 또는 기타 스프레드시트 뷰어에서 열어 **A2** 셀에 정확한 JSON 문자열이 들어 있는지 확인합니다.

```csharp
// Save the resulting workbook
string outputPath = @"C:\Temp\SmartMarkerJson.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### Expected output

| A   |
|-----|
| **["Alice","Bob"]** |

셀 **A2**에 JSON 배열이 단일 텍스트 값으로 표시되며, `DataTable`에 저장된 그대로입니다. 추가 행이 생성되지 않습니다.

---

## Common variations and edge‑case handling

| Situation | How to adapt |
|-----------|--------------|
| **Multiple rows with JSON arrays** | 동일한 `ArrayAsSingle` 설정이 작동하며, 각 행의 JSON 배열이 각각의 셀에 유지됩니다. |
| **Different JSON structures (objects, nested arrays)** | JSON이 문자열인 한 `ArrayAsSingle`은 그대로 보존합니다. 복잡한 객체의 경우 따옴표를 이스케이프해야 할 수 있습니다. |
| **Using a different data source (e.g., List\<T\>)** | `DataTable`을任意의 열거 가능한 컬렉션으로 교체하면 됩니다; 마커 구문(`&=myList.Property`)은 동일하게 유지됩니다. |
| **Exporting to CSV instead of XLSX** | `ArrayAsSingle`은 여전히 적용되지만, CSV는 셀 서식을 보존하지 않으므로 JSON을 따옴표로 감싸야 할 수 있습니다. |

**Pro tip:** `ProcessSmartMarkers`를 호출하기 **전에** 항상 `ArrayAsSingle`을 설정하세요. 처리 후에 플래그를 변경해도 이미 생성된 셀에는 영향을 주지 않습니다.

---

## Full, runnable example

아래는 콘솔 애플리케이션에 복사‑붙여넣기 할 수 있는 완전한 프로그램 예제입니다. 모든 `using` 지시문과 설명 주석이 포함되어 있습니다.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the data source with a JSON array
            DataTable dataTable = new DataTable();
            dataTable.Columns.Add("Id", typeof(int));
            dataTable.Columns.Add("Names", typeof(string));
            dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");

            // 2️⃣ Build a workbook and place smart markers
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Cells["A1"].PutValue("&=dataTable");          // whole table (optional)
            worksheet.Cells["A2"].PutValue("&=dataTable.Names");   // Names column

            // 3️⃣ Configure SmartMarkerOptions to treat arrays as single values
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 4️⃣ Process the markers with the custom options
            workbook.ProcessSmartMarkers(options);

            // 5️⃣ Save the file
            string path = @"C:\Temp\SmartMarkerJson.xlsx";
            workbook.Save(path);
            Console.WriteLine($"Workbook saved to {path}");
        }
    }
}
```

프로그램을 실행하고 `SmartMarkerJson.xlsx` 파일을 열면 셀 **A2**에 JSON 배열이 보존된 것을 확인할 수 있습니다.

---

## Conclusion

이제 C#에서 **SmartMarkerOptions ArrayAsSingle**을 **구성**하여 Aspose.Cells 스마트 마커를 사용할 때 JSON 배열을 단일 셀 값으로 유지하는 방법을 알게 되었습니다. `DataTable` 준비, 마커 삽입, `ArrayAsSingle` 플래그 설정, 처리 및 저장 단계는 Excel 내부에서 압축된 JSON 표현이 필요한 모든 시나리오에 적용할 수 있는 반복 가능한 패턴을 형성합니다.

다음 단계로 탐색해 볼 내용:

* 컬렉션 반복을 위한 **Aspose.Cells smart markers**  
* 셀 서식을 커스터마이징하여 **중첩 JSON 객체** 내보내기  
* 보다 풍부한 보고서를 위한 **조건부 서식**과 스마트 마커 결합

다양한 데이터 구조를 실험해 보고 결과를 공유하세요. 즐거운 코딩 되세요!

## What Should You Learn Next?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하여 밀접하게 연관된 주제를 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 포함하고 있어 추가 API 기능을 마스터하고 프로젝트에 적용할 수 있는 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [JSON에서 Excel 워크북 만들기 – 완전한 Aspose.Cells 가이드](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Aspose Cells Net으로 Excel 워크북 만들기 및 구성](/cells/hindi/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Aspose Cells Net으로 Excel 워크북 만들기 및 구성](/cells/german/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}