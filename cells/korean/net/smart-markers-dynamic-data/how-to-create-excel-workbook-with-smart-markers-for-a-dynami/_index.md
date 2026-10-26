---
category: general
date: 2026-10-26
description: C#에서 스마트 마커를 사용하여 엑셀 워크북을 만들고 데이터를 삽입해 동적 엑셀 보고서를 만드는 방법을 배웁니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- insert data into excel
- dynamic excel report
language: ko
lastmod: 2026-10-26
og_description: C# 스마트 마커를 사용하여 엑셀 워크북을 만들고 데이터를 삽입하세요. 이 가이드를 따라 빠르게 동적인 엑셀 보고서를
  생성하십시오.
og_image_alt: Screenshot showing a created excel workbook with populated data
og_title: 스마트 마커로 엑셀 워크북 만들기 – 단계별 가이드
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to create excel workbook and insert data into excel using
    smart markers to build a dynamic excel report in C#.
  headline: How to create excel workbook with smart markers for a dynamic excel report
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: 동적 Excel 보고서를 위한 스마트 마커가 포함된 Excel 워크북 만드는 방법
url: /ko/net/smart-markers-dynamic-data/how-to-create-excel-workbook-with-smart-markers-for-a-dynami/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 스마트 마커를 사용한 동적 Excel 보고서를 위한 Excel 워크북 생성 방법

프로그래밍 방식으로 **excel workbook**을 생성해야 한다면, 이 가이드가 정확히 어떻게 하는지 보여줍니다. 스마트 마커를 사용하면 셀 단위 코드를 작성하지 않고도 **excel에 데이터 삽입**이 가능해져 **동적 excel 보고서**를 빠르고 유지 보수하기 쉽게 생성할 수 있습니다.

워크북 초기화부터 마커 처리까지 모든 단계를 차근차근 안내하므로, 완전하고 실행 가능한 예제를 여러분의 프로젝트에 복사해 바로 사용할 수 있습니다. 외부 문서는 필요 없으며, 아래에 모든 코드와 설명이 제공됩니다.

## Prerequisites

시작하기 전에 다음이 준비되어 있는지 확인하세요:

* .NET 6.0 이상 (예제는 .NET Framework 4.7+에서도 작동합니다)
* **Aspose.Cells** 라이브러리에 대한 참조 (NuGet `Install-Package Aspose.Cells`를 통해 사용 가능)
* C# 익명 형식 및 LINQ에 대한 기본 지식
* Visual Studio 또는 VS Code와 같은 IDE

> **Pro tip:** 테스트용으로 무료 Aspose.Cells 평가 라이선스를 사용하고, 실제 운영 전에는 정식 라이선스로 교체하세요.

## Step 1: Excel 워크북 생성 및 첫 번째 워크시트 접근

첫 번째 작업은 `Workbook` 객체를 인스턴스화하는 것입니다. 이 객체는 메모리 상의 전체 Excel 파일을 나타내며 워크시트에 직접 접근할 수 있게 해줍니다.

```csharp
using Aspose.Cells;

namespace ExcelSmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new workbook – this is the core object for any Excel manipulation
            Workbook wb = new Workbook();

            // The workbook always contains at least one worksheet; we work with the first one
            Worksheet ws = wb.Worksheets[0];
```

워크북을 생성하는 것은 모든 **dynamic excel report**의 기반이 됩니다. 이 객체가 없으면 스마트 마커를 배치하거나 나중에 파일을 저장할 수 없습니다.

## Step 2: 데이터가 삽입될 위치에 스마트 마커 태그 배치

스마트 마커는 Aspose.Cells가 런타임에 데이터를 대체하는 특수 플레이스홀더입니다. `${Object.Property}` 구문을 따르며 단일 행, 테이블 또는 계층형 데이터를 나타낼 수 있습니다.

```csharp
            // Insert a smart marker for the master (header) section
            ws.Cells[0, 0].PutValue("${Orders.Master}");

            // Insert a smart marker for the detail (row) section
            ws.Cells[1, 0].PutValue("${Orders.Detail}");
```

* 셀 `[0,0]` (A1)은 헤더 행이 됩니다.
* 셀 `[1,0]` (A2)은 `Orders.Detail`에 항목이 있는 만큼 행을 확장합니다.

워크시트에 직접 마커를 배치하면 나중에 **excel에 데이터 삽입**이 자동으로 이루어져 수동 루프를 없앨 수 있습니다.

## Step 3: 스마트 마커와 일치하는 데이터 소스 준비

스마트 마커는 마커 계층 구조를 반영하는 데이터 소스가 필요합니다. 여기서는 주문 컬렉션을 포함하는 익명 객체를 사용합니다. 각 주문은 마스터 행과 상세 라인 컬렉션을 포함합니다.

```csharp
            // Build the data that matches the markers
            var data = new
            {
                Orders = GetOrders()
            };
```

아래에 표시된 `GetOrders` 메서드는 `OrderInfo` 객체 리스트를 반환합니다. 각 `OrderInfo`는 헤더용 `Master` 객체와 행용 `Detail` 리스트를 포함합니다.

```csharp
        // Sample data generator – replace with your real data source (e.g., database, API)
        static List<OrderInfo> GetOrders()
        {
            return new List<OrderInfo>
            {
                new OrderInfo
                {
                    Master = new { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today },
                    Detail = new[]
                    {
                        new { Product = "Widget A", Qty = 10, Price = 9.99 },
                        new { Product = "Widget B", Qty = 5,  Price = 19.99 }
                    }
                },
                new OrderInfo
                {
                    Master = new { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1) },
                    Detail = new[]
                    {
                        new { Product = "Gadget X", Qty = 2, Price = 99.99 },
                        new { Product = "Gadget Y", Qty = 1, Price = 149.99 }
                    }
                }
            };
        }

        // Helper class to keep master/detail together
        class OrderInfo
        {
            public object Master { get; set; }
            public object[] Detail { get; set; }
        }
```

구조가 잘 잡힌 데이터 소스를 제공하면 **dynamic excel report**가 주문 수에 관계없이 올바르게 확장됩니다.

## Step 4: 스마트 마커를 처리하여 워크시트 채우기

이제 워크북에 마커가 포함되고 데이터 소스가 준비되었으므로 `ProcessSmartMarkers`를 호출합니다. Aspose.Cells는 워크시트를 스캔하고 각 마커를 적절한 값으로 교체하며, 컬렉션에 대해 행을 자동으로 확장합니다.

```csharp
            // Populate the worksheet by processing the smart markers
            wb.ProcessSmartMarkers(data);
```

처리 중:

* `${Orders.Master}`는 마스터 필드(`OrderId`, `Customer`, `Date`)를 포함하는 단일 행으로 변환됩니다.
* `${Orders.Detail}`은 상세 항목마다 하나씩 행을 확장하여 열 정렬을 유지합니다.

## Step 5: 워크북 저장 및 출력 확인

마지막으로 워크북을 실제 파일로 기록합니다. 결과 파일을 Excel 호환 프로그램에서 열어 데이터가 올바르게 삽입되었는지 확인할 수 있습니다.

```csharp
            // Save the populated workbook to disk
            string outputPath = "DynamicReport.xlsx";
            wb.Save(outputPath, SaveFormat.Xlsx);

            System.Console.WriteLine($"Report generated: {outputPath}");
        }
    }
}
```

**Expected output:** `DynamicReport.xlsx`를 열면 각 주문에 대한 헤더 행과 그에 따른 상세 행이 표시됩니다. 행 수는 `Detail` 컬렉션 크기에 따라 자동으로 조정되며, 이것이 **dynamic excel report**의 핵심입니다.

![스마트 마커로 생성된 Excel 워크북](excel-workbook.png)

*Image alt text:* *스마트 마커로 생성된 Excel 워크북*

## Common variations and edge cases

| Scenario | What to change | Why it matters |
|----------|----------------|----------------|
| **Different sheet layout** | 스마트 마커를 다른 시트(`wb.Worksheets[1]`)로 이동 | 템플릿을 데이터 시트와 분리하여 관리할 수 있습니다 |
| **Nested collections** | `${Orders.SubOrders.Detail}`을 사용하고 `OrderInfo`에 `SubOrders` 속성을 추가 | 다중 레벨 마스터/디테일 보고서를 지원합니다 |
| **Large data sets** | 삽입된 데이터에 의존하는 수식이 있다면 처리 후 `wb.CalculateFormula()` 호출 | 계산된 필드가 최신 상태를 유지합니다 |
| **Custom formatting** | 처리 전에 `ws.Cells`에 스타일 객체 적용(예: `Style style = wb.CreateStyle();`) | 생성된 행 전체에 일관된 모양을 보장합니다 |
| **Memory‑constrained environments** | 스트림과 함께 `WorkbookFactory.Create` 사용 후 객체를 즉시 `Dispose` | 서비스에서 다수의 보고서를 생성할 때 메모리 누수를 방지합니다 |

## Best practices for inserting data into excel with smart markers

* **템플릿을 깔끔하게 유지:** 필요한 마커만 배치하세요; 여분의 셀은 예상치 못한 데이터 배치를 초래할 수 있습니다.
* **속성 이름을 정확히 일치시킴:** 스마트 마커는 대소문자를 구분합니다. 오타가 있으면 오류 없이 빈 셀이 됩니다.
* **동일 데이터 객체 재사용:** 동일 소스로 여러 시트를 생성해야 할 경우, 같은 `data` 인스턴스로 `ProcessSmartMarkers`를 반복 호출하세요.
* **처리 전 데이터 검증:** 데이터 소스 내부에 널 참조가 있으면 빈 셀이 생성됩니다. `?.` 연산자나 기본값으로 방어하세요.

## Conclusion

이제 **excel workbook**을 **생성**하고, 스마트 마커를 사용해 **excel에 데이터 삽입**하며, 데이터에 따라 자동으로 확장되는 **dynamic excel report**를 만들 수 있습니다. 완전한 코드 예제를 C# 프로젝트에 복사해 자신의 데이터 구조에 맞게 조정하고, 추가 포맷팅이나 계산을 확장할 수 있습니다.

### Next steps

* 수식과 차트를 활용해 **excel에 데이터 삽입**을 탐색하고 보고서를 풍부하게 만들기
* 이 방식을 **dynamic excel report** 생성과 결합해 다중 워크시트(예: 고객당 한 시트) 만들기
* ASP.NET Core API에 통합해 필요 시 보고서를 제공하기

행복한 코딩 되시고, Aspose.Cells와 함께 유연한 Excel 자동화를 즐기세요!

## What Should You Learn Next?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 리소스는 완전한 작동 코드 예제와 단계별 설명을 포함해 추가 API 기능을 마스터하고 프로젝트에 적용할 수 있는 다양한 구현 방식을 탐색하도록 돕습니다.

- [Create Excel workbook programmatically using Smart Markers](/cells/english/net/smart-markers-dynamic-data/create-excel-workbook-programmatically-using-smart-markers/)
- [Create Excel Workbook C# – Full Guide to Inserting Arrays into Cells](/cells/english/net/smart-markers-dynamic-data/create-excel-workbook-c-full-guide-to-inserting-arrays-into/)
- [Create Excel Workbook and Write Data in C# – Full Step‑by‑Step Guide](/cells/english/net/excel-workbook/create-excel-workbook-and-write-data-in-c-full-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}