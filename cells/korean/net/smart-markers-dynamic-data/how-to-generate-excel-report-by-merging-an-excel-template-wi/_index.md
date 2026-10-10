---
category: general
date: 2026-10-10
description: 스마트 마커를 사용해 Excel 템플릿을 병합하여 Excel 보고서를 생성합니다—스마트 태그를 교체하고 상세 시트 태그를 효율적으로
  처리합니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate Excel report
- merge Excel template
- detail sheet tag
- use smart markers
- replace smart tags
language: ko
lastmod: 2026-10-10
og_description: 스마트 마커를 사용하여 Excel 보고서를 생성합니다. Excel 템플릿을 병합하고, 스마트 태그를 교체하며, 상세 시트
  태그를 활용하는 전체 C# 예제를 배워보세요.
og_image_alt: Generated Excel report after merging template with Smart Markers
og_title: 스마트 마커와 Excel 템플릿을 병합하여 Excel 보고서 생성
schemas:
- author: GroupDocs
  dateModified: '2026-10-10'
  description: Generate Excel report by merging an Excel template using Smart Markers—replace
    smart tags and handle detail sheet tag efficiently.
  headline: How to generate Excel report by merging an Excel template with Smart Markers
  type: TechArticle
- description: Generate Excel report by merging an Excel template using Smart Markers—replace
    smart tags and handle detail sheet tag efficiently.
  name: How to generate Excel report by merging an Excel template with Smart Markers
  steps:
  - name: '**Load the Excel template** – The template holds the layout, formulas,
      and styling. Smart Markers are placeholders like `${MasterSheet:Orders}` that
      the processor will replace.'
    text: '**Load the Excel template** – The template holds the layout, formulas,
      and styling. Smart Markers are placeholders like `${MasterSheet:Orders}` that
      the processor will replace.'
  - name: '**Prepare the data source** – `SmartMarkerProcessor` works with any enumerable
      collection. Here we use a list of `Order` objects that contain a nested list
      of `OrderDetail` objects, which is exactly what a master‑detail report needs.'
    text: '**Prepare the data source** – `SmartMarkerProcessor` works with any enumerable
      collection. Here we use a list of `Order` objects that contain a nested list
      of `OrderDetail` objects, which is exactly what a master‑detail report needs.'
  - name: '**Create the processor** – Instantiating `SmartMarkerProcessor` is cheap;
      you can reuse it for multiple worksheets if you need to generate several reports
      in one run.'
    text: '**Create the processor** – Instantiating `SmartMarkerProcessor` is cheap;
      you can reuse it for multiple worksheets if you need to generate several reports
      in one run.'
  - name: '**Process the worksheet** – This single call does three things:'
    text: '**Process the worksheet** – This single call does three things:'
  - name: '**Save the result** – The output file (`GeneratedReport.xlsx`) is a fully‑populated
      Excel report ready for distribution.'
    text: '**Save the result** – The output file (`GeneratedReport.xlsx`) is a fully‑populated
      Excel report ready for distribution.'
  - name: Creates a new worksheet for every master row.
    text: Creates a new worksheet for every master row.
  - name: Copies the formatting from the template’s detail area.
    text: Copies the formatting from the template’s detail area.
  - name: Inserts each item from the enumerable into consecutive rows.
    text: Inserts each item from the enumerable into consecutive rows.
  - name: A **master sheet** named *Sheet1* with two rows—one for each order. Columns
      display Order ID, Customer, Order Date, and Total.
    text: A **master sheet** named *Sheet1* with two rows—one for each order. Columns
      display Order ID, Customer, Order Date, and Total.
  - name: Two **detail sheets** named `OrderDetails_1001` and `OrderDetails_1002`.
      Each sheet lists the products, quantities, and unit prices for the corresponding
      order.
    text: Two **detail sheets** named `OrderDetails_1001` and `OrderDetails_1002`.
      Each sheet lists the products, quantities, and unit prices for the corresponding
      order.
  type: HowTo
tags:
- Excel
- C#
- SmartMarkers
title: 스마트 마커와 Excel 템플릿을 병합하여 Excel 보고서를 생성하는 방법
url: /ko/net/smart-markers-dynamic-data/how-to-generate-excel-report-by-merging-an-excel-template-wi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel 템플릿과 Smart Markers를 병합하여 Excel 보고서를 생성하는 방법

재사용 가능한 워크북에서 **Excel 보고서 생성**이 필요하다면, Smart Markers를 사용하면 데이터를 빠르고 안정적으로 병합할 수 있습니다. **Excel 템플릿 병합** 방식을 사용하면 레이아웃을 비즈니스 로직과 분리할 수 있으며, 동일한 템플릿으로 수십 개의 보고서를 만들 수 있습니다.

이 튜토리얼에서는 **detail sheet tag**를 정의하고, **smart markers**를 사용하여 마스터‑디테일 데이터를 채우며, 최종 파일에서 **smart tags를 교체**하는 방법을 보여줍니다. 몇 초 만에 전문적인 Excel 보고서를 생성하는 완전한 실행 가능한 C# 프로그램을 얻을 수 있습니다.

## 필요 사항

- .NET 6.0 이상 (코드는 .NET Framework 4.7+에서도 작동합니다)
- Visual Studio 2022 또는 기타 C# IDE
- `GroupDocs.Viewer` / `Aspose.Cells` (또는 `SmartMarkerProcessor`를 제공하는 라이브러리) NuGet 패키지
- Smart Marker 태그가 포함된 Excel 템플릿 파일 (`ReportTemplate.xlsx`)

> **Pro tip:** 템플릿을 프로젝트의 `Resources` 폴더에 두고, *Copy to Output Directory* 속성을 *Copy if newer* 로 설정하면 런타임에 코드가 템플릿을 찾을 수 있습니다.

## Smart Markers를 사용한 단계별 Excel 보고서 생성

아래는 전체 소스 파일 `Program.cs`입니다. 각 영역은 다음 섹션에서 설명합니다.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.Cells;               // SmartMarkerProcessor lives in this namespace
using Aspose.Cells.Tables;        // For master‑detail handling

namespace ExcelReportDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the Excel template that contains Smart Marker tags
            string templatePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "ReportTemplate.xlsx");
            Workbook workbook = new Workbook(templatePath);
            Worksheet ws = workbook.Worksheets[0];   // assume the first sheet is the master sheet

            // 2️⃣ Prepare the data source – a list of orders, each with order lines
            List<Order> ordersData = GetSampleOrders();

            // 3️⃣ Create a SmartMarkerProcessor instance
            SmartMarkerProcessor processor = new SmartMarkerProcessor();

            // 4️⃣ Process the worksheet, merging the template with the data source
            // This replaces all ${...} tags with real values and expands the detail sheet tag.
            processor.Process(ws, ordersData);

            // 5️⃣ Save the merged workbook as the final report
            string outputPath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "GeneratedReport.xlsx");
            workbook.Save(outputPath, SaveFormat.Xlsx);

            Console.WriteLine($"Report generated successfully: {outputPath}");
        }

        // Sample data generator – in a real project you would pull from a database or service
        private static List<Order> GetSampleOrders()
        {
            return new List<Order>
            {
                new Order
                {
                    OrderId = 1001,
                    Customer = "Acme Corp",
                    OrderDate = new DateTime(2024, 9, 15),
                    Total = 1250.75,
                    Details = new List<OrderDetail>
                    {
                        new OrderDetail { Product = "Widget A", Quantity = 10, UnitPrice = 25.00 },
                        new OrderDetail { Product = "Widget B", Quantity = 5,  UnitPrice = 75.00 }
                    }
                },
                new Order
                {
                    OrderId = 1002,
                    Customer = "Beta Ltd.",
                    OrderDate = new DateTime(2024, 9, 16),
                    Total = 980.00,
                    Details = new List<OrderDetail>
                    {
                        new OrderDetail { Product = "Gadget X", Quantity = 8, UnitPrice = 80.00 },
                        new OrderDetail { Product = "Gadget Y", Quantity = 4, UnitPrice = 50.00 }
                    }
                }
            };
        }
    }

    // Simple POCO classes that represent master‑detail data
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime OrderDate { get; set; }
        public double Total { get; set; }
        public List<OrderDetail> Details { get; set; }
    }

    public class OrderDetail
    {
        public string Product { get; set; }
        public int Quantity { get; set; }
        public double UnitPrice { get; set; }
    }
}
```

### 각 부분이 중요한 이유

1. **Excel 템플릿 로드** – 템플릿은 레이아웃, 수식 및 스타일을 포함합니다. Smart Markers는 `${MasterSheet:Orders}`와 같은 자리표시자로, 프로세서가 이를 교체합니다.
2. **데이터 소스 준비** – `SmartMarkerProcessor`는 모든 열거 가능한 컬렉션과 함께 사용할 수 있습니다. 여기서는 `Order` 객체 리스트를 사용하며, 각 객체는 중첩된 `OrderDetail` 리스트를 포함합니다. 이는 마스터‑디테일 보고서에 정확히 필요한 구조입니다.
3. **프로세서 생성** – `SmartMarkerProcessor` 인스턴스를 만드는 비용이 적으며, 한 번에 여러 워크시트를 생성해야 할 경우 재사용할 수 있습니다.
4. **워크시트 처리** – 이 한 번의 호출로 세 가지 작업을 수행합니다:
   - `${MasterSheet:Orders}`와 같은 **smart tags 교체**를 실제 필드 값으로 바꿉니다.
   - **detail sheet tag 확장** (`${DetailSheetNewName:OrderDetails}`)을 사용해 각 마스터 행마다 새로운 워크시트를 생성합니다.
   - 템플릿의 **서식 복사**를 수행하여 생성된 행에 디자인을 유지합니다.
5. **결과 저장** – 출력 파일 (`GeneratedReport.xlsx`)은 배포 준비가 된 완전한 Excel 보고서입니다.

## 데이터 소스와 Excel 템플릿 병합

**merge Excel template** 기법의 핵심은 Smart Marker 구문입니다. `ReportTemplate.xlsx`에 다음과 같은 태그를 배치합니다:

| 셀 | 값 |
|------|-------|
| A1   | `${MasterSheet:Orders.OrderId}` |
| B1   | `${MasterSheet:Orders.Customer}` |
| C1   | `${MasterSheet:Orders.OrderDate:MM/dd/yyyy}` |
| D1   | `${MasterSheet:Orders.Total}` |
| A5   | `${DetailSheetNewName:OrderDetails}` |
| A6   | `${DetailSheet:OrderDetails.Product}` |
| B6   | `${DetailSheet:OrderDetails.Quantity}` |
| C6   | `${DetailSheet:OrderDetails.UnitPrice}` |

- `${MasterSheet:Orders}`는 프로세서에게 데이터 소스에서 `Orders` 컬렉션을 읽도록 지시합니다.
- `${DetailSheetNewName:OrderDetails}`는 마스터 행의 이름을 따서 새로운 워크시트를 생성하는 **detail sheet tag**를 만듭니다 (예: `OrderDetails_1001`).
- `${DetailSheet:OrderDetails.*}`는 각 디테일 행을 채웁니다.

`processor.Process(ws, ordersData)`가 실행되면, 라이브러리는 `ordersData`의 값으로 **smart tags를 자동으로 교체**하고 각 주문마다 detail sheet를 복제합니다.

## Detail sheet tag 구문

**detail sheet tag**는 `${DetailSheetNewName:TagName}` 패턴을 따릅니다. `TagName`은 `IEnumerable`을 반환하는 속성과 일치해야 합니다 (우리 경우 `Order.Details`). 프로세서는 다음을 수행합니다:

1. 각 마스터 행마다 새로운 워크시트를 생성합니다.
2. 템플릿의 디테일 영역에서 서식을 복사합니다.
3. 열거형의 각 항목을 연속 행에 삽입합니다.

각 마스터 행마다 동일한 이름의 detail sheet를 유지해야 하는 경우(예: 모든 디테일을 하나의 시트에 포함), `${DetailSheetNewName:OrderDetails}`를 `${DetailSheet:OrderDetails}`로 교체합니다. 앞의 방식은 각 주문마다 별도의 탭을 갖는 **Excel 보고서 생성** 시나리오에 유용합니다.

## 스마트 마커를 사용하여 스마트 태그 교체

Smart Markers는 단순한 자리표시자를 넘어섭니다. 다음을 지원합니다:

- **포맷 문자열** (`:MM/dd/yyyy` 예시)로 날짜나 숫자 표시 형식을 제어합니다.
- **조건부 섹션** (`${if:Orders.Total > 1000}`)을 사용해 데이터에 따라 행을 숨깁니다.
- **컬렉션 반복**을 태그만으로 구현하여 별도의 코드를 작성하지 않아도 됩니다.

프로세서가 이러한 기능을 내부적으로 처리하기 때문에, 사용자 정의 루프나 셀별 할당 코드를 작성하지 않고도 템플릿에서 **smart tags를 교체**할 수 있습니다. 이는 버그를 줄이고 템플릿을 유지보수하기 쉽게 합니다.

## 기대 출력

프로그램을 실행한 후 `GeneratedReport.xlsx`를 열면 다음과 같은 내용이 표시됩니다:

1. 두 개의 행을 가진 *Sheet1*이라는 **마스터 시트**가 있으며, 각 행은 주문 하나에 해당합니다. 열에는 Order ID, Customer, Order Date, Total이 표시됩니다.
2. `OrderDetails_1001` 및 `OrderDetails_1002`라는 두 개의 **detail 시트**가 있습니다. 각 시트는 해당 주문의 제품, 수량, 단가를 나열합니다.
3. `ReportTemplate.xlsx`에서 원본 서식(글꼴, 색상, 테두리)이 모두 유지됩니다.

![Generated Excel report after merging template with Smart Markers](generated-report.png "Generated Excel report after merging template

## 다음에 배워야 할 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 리소스는 단계별 설명과 함께 완전한 코드 예제를 제공하여 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색할 수 있도록 돕습니다.

- [Aspose Cells Smart Markers: Excel 템플릿 로드 및 템플릿에서 Excel 생성](/cells/english/java/templates-reporting/aspose-cells-smart-markers-load-excel-template-generate-exce/)
- [Aspose.Cells .NET Smart Markers를 사용하여 동적 Excel 보고서 생성](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Aspose Cells Smart Markers: C# 모델에서 Excel 생성](/cells/english/net/smart-markers-dynamic-data/aspose-cells-smart-markers-generate-excel-from-model-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}