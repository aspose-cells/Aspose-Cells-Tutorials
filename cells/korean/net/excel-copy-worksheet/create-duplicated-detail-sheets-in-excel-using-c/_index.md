---
category: general
date: 2026-10-07
description: C#를 사용하여 Excel에서 중복된 상세 시트를 생성합니다. 한 번의 실행으로 여러 워크시트를 만들고 테이블에서 보고서를
  작성하는 방법을 배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicated detail sheets
- how to generate multiple worksheets
- generate excel report from tables
language: ko
lastmod: 2026-10-07
og_description: C#를 사용하여 Excel에서 중복된 상세 시트를 생성합니다. 이 튜토리얼에서는 여러 워크시트를 만들고 테이블에서 전체
  Excel 보고서를 만드는 방법을 보여줍니다.
og_image_alt: Screenshot of an Excel file that has create duplicated detail sheets
  output
og_title: Excel에서 중복 상세 시트 만들기 – 단계별 C# 가이드
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create duplicated detail sheets in Excel using C#. Learn how to generate
    multiple worksheets and build a report from tables in a single run.
  headline: Create duplicated detail sheets in Excel using C#
  type: TechArticle
- description: Create duplicated detail sheets in Excel using C#. Learn how to generate
    multiple worksheets and build a report from tables in a single run.
  name: Create duplicated detail sheets in Excel using C#
  steps:
  - name: '**Obtain the data source** that contains a master table and two detail
      tables.'
    text: '**Obtain the data source** that contains a master table and two detail
      tables.'
  - name: '**Configure the Smart‑marker processor** so each duplicated detail sheet
      receives a unique name.'
    text: '**Configure the Smart‑marker processor** so each duplicated detail sheet
      receives a unique name.'
  - name: '**Create a new workbook** and place a smart‑marker that references the
      master table.'
    text: '**Create a new workbook** and place a smart‑marker that references the
      master table.'
  - name: '**Run the processor** to generate the master sheet and all detail sheets.'
    text: '**Run the processor** to generate the master sheet and all detail sheets.'
  - name: '**Save the workbook** – each detail sheet now has a distinct name.'
    text: '**Save the workbook** – each detail sheet now has a distinct name.'
  type: HowTo
tags:
- C#
- Excel automation
- Aspose.Cells
title: C#를 사용하여 Excel에서 중복 상세 시트 만들기
url: /ko/net/excel-copy-worksheet/create-duplicated-detail-sheets-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#를 사용하여 Excel에서 중복 상세 시트 만들기

Excel 통합 문서에서 **중복 상세 시트**를 만들어야 하는 경우, 이 가이드는 전체 과정을 단계별로 안내합니다. **여러 워크시트**를 마스터‑디테일 데이터 세트에서 생성하고 테이블에서 직접 깔끔한 Excel 보고서를 만드는 방법을 확인할 수 있습니다.

테이블에서 Excel 보고서를 생성하는 것은 청구 시스템, 재고 대시보드 또는 마스터 레코드에 여러 관련 상세 행이 있는 모든 시나리오에서 흔히 요구됩니다. 이 튜토리얼을 마치면 마스터 시트와 각 상세 그룹마다 고유한 이름을 가진 시트를 포함하는 실행 가능한 C# 프로그램을 얻게 됩니다.

## 필수 조건

* .NET 6.0 (또는 이후 버전) 설치  
* Visual Studio 2022 또는 C# 호환 IDE  
* **Aspose.Cells for .NET** NuGet 패키지 (`SmartMarkerProcessor` 제공)  

다음 명령으로 패키지를 추가할 수 있습니다:

```bash
dotnet add package Aspose.Cells
```

## 솔루션 개요

솔루션은 다음 다섯 단계로 구성됩니다:

1. **데이터 소스 확보** – 마스터 테이블과 두 개의 상세 테이블을 포함합니다.  
2. **Smart‑marker 프로세서 구성** – 각 중복 상세 시트에 고유한 이름을 부여합니다.  
3. **새 워크북 생성** – 마스터 테이블을 참조하는 스마트‑마커를 배치합니다.  
4. **프로세서 실행** – 마스터 시트와 모든 상세 시트를 생성합니다.  
5. **워크북 저장** – 이제 각 상세 시트가 고유한 이름을 갖습니다.  

각 단계는 아래에서 자세히 설명되며, 전체 코드와 설명이 포함됩니다.

## 단계 1: 마스터 테이블과 두 개의 상세 테이블을 포함하는 데이터 소스 확보

첫 번째 작업은 일반적으로 데이터베이스에서 가져오는 데이터를 모방하는 `DataSet`을 만드는 것입니다. `DataSet`에는 **Master**라는 이름의 테이블과 하나 이상의 **Detail**이라는 이름의 테이블이 포함되어야 합니다. Smart‑marker 엔진은 이러한 테이블 이름을 사용해 워크북을 채웁니다.

```csharp
using System.Data;

/// <summary>
/// Returns a DataSet with a master table and two detail tables.
/// In a real application you would fill these tables from a database.
/// </summary>
static DataSet GetReportDataSet()
{
    var ds = new DataSet();

    // Master table – one row per invoice
    var master = new DataTable("Master");
    master.Columns.Add("InvoiceId", typeof(int));
    master.Columns.Add("CustomerName", typeof(string));
    master.Columns.Add("InvoiceDate", typeof(DateTime));
    master.Rows.Add(101, "Acme Corp", new DateTime(2024, 12, 01));
    master.Rows.Add(102, "Beta Ltd.", new DateTime(2024, 12, 03));
    ds.Tables.Add(master);

    // Detail table – multiple rows per invoice
    var detail = new DataTable("Detail");
    detail.Columns.Add("InvoiceId", typeof(int));
    detail.Columns.Add("Product", typeof(string));
    detail.Columns.Add("Quantity", typeof(int));
    detail.Columns.Add("Price", typeof(decimal));

    // Detail rows for Invoice 101
    detail.Rows.Add(101, "Widget A", 5, 9.99m);
    detail.Rows.Add(101, "Widget B", 2, 19.95m);

    // Detail rows for Invoice 102
    detail.Rows.Add(102, "Gadget X", 1, 99.00m);
    detail.Rows.Add(102, "Gadget Y", 3, 49.50m);
    ds.Tables.Add(detail);

    return ds;
}
```

**왜 중요한가:**  
*Smart‑marker*는 `DataSet` 객체와 함께 작동하며, 각 테이블 이름은 엔진이 교체할 수 있는 마커가 됩니다. 이렇게 데이터를 구조화하면 프로세서가 각 고유 `InvoiceId`에 대해 상세 시트를 자동으로 복제하도록 할 수 있습니다.

## 단계 2: Smart‑marker 프로세서를 구성하여 각 중복 상세 시트에 고유한 이름 부여

프로세서가 상세 마커를 만나면 각 행 그룹마다 새로운 워크시트를 생성합니다. 기본적으로 새 시트는 동일한 이름을 공유하므로 이름 충돌이 발생합니다. `DetailSheetNewName`을 설정하면 엔진에 각 복사본의 이름을 지정하는 방법을 알려줍니다.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

/// <summary>
/// Configures the SmartMarkerProcessor to rename duplicated detail sheets.
/// The placeholder {0} is replaced with a sequential number (1, 2, …).
/// </summary>
static SmartMarkerProcessor ConfigureProcessor()
{
    var processor = new SmartMarkerProcessor();

    // The pattern "Detail_{0}" becomes Detail_1, Detail_2, …
    processor.Options.DetailSheetNewName = "Detail_{0}";

    // Optional: keep the original sheet as a template (if you have one)
    processor.Options.KeepTemplateSheet = false;

    return processor;
}
```

**왜 중요한가:**  
고유한 이름 패턴이 없으면 프로세서가 두 번째 상세 시트를 추가하려 할 때 워크북이 예외를 발생시킵니다. 자리표시자 `{0}`는 각 시트가 구별 가능하고 예측 가능한 이름을 받도록 보장합니다.

## 단계 3: 새 워크북을 만들고 마스터 테이블을 참조하는 스마트‑마커 배치

이제 새 `Workbook`을 만들고 **Master** 테이블을 가리키는 마커를 추가하며, 필요에 따라 헤더 행을 서식 지정합니다.

```csharp
/// <summary>
/// Creates a workbook with a single cell that contains the master smart‑marker.
/// </summary>
static Workbook CreateTemplateWorkbook()
{
    var workbook = new Workbook();
    var sheet = workbook.Worksheets[0];

    // Put the master smart‑marker in cell A1.
    // The double braces {{ }} tell SmartMarker to replace the content with the Master table.
    sheet.Cells["A1"].PutValue("{{Master}}");

    // Optional: add a header row for visual clarity.
    sheet.Cells["A2"].PutValue("Invoice ID");
    sheet.Cells["B2"].PutValue("Customer");
    sheet.Cells["C2"].PutValue("Date");
    sheet.Cells["A2:C2"].Style.Font.IsBold = true;

    return workbook;
}
```

**왜 중요한가:**  
마커 `{{Master}}`는 프로세서에게 마스터 테이블을 `A1`부터 확장하도록 지시합니다. 이후 행들은 각 마스터 레코드의 데이터 행이 됩니다. 이것이 **테이블에서 Excel 보고서 생성**의 시작점입니다.

## 단계 4: 스마트‑마커 프로세서를 실행하여 마스터 시트와 상세 시트 생성

데이터 소스, 프로세서 및 템플릿이 준비되면 `Process`를 호출합니다. 엔진은 마스터 마커를 확장한 뒤, 각 고유 `InvoiceId`마다 별도의 상세 시트를 생성합니다.

```csharp
static void GenerateReport()
{
    // 1️⃣ Obtain data
    DataSet reportData = GetReportDataSet();

    // 2️⃣ Configure processor
    SmartMarkerProcessor processor = ConfigureProcessor();

    // 3️⃣ Create template workbook
    Workbook workbook = CreateTemplateWorkbook();

    // 4️⃣ Process the smart‑markers – this creates the master sheet and duplicated detail sheets
    processor.Process(workbook, reportData);

    // 5️⃣ Save the file
    string outputPath = Path.Combine(
        Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
        "DuplicatedDetailSheets.xlsx");
    workbook.Save(outputPath);

    Console.WriteLine($"Report generated successfully: {outputPath}");
}
```

**왜 중요한가:**  
`processor.Process`는 핵심 작업을 수행합니다: 마스터 행을 읽고, 각 고유 키마다 상세 시트를 만들며, 앞서 정의한 패턴에 따라 시트 이름을 바꿉니다. 결과적으로 **여러 워크시트 생성 방법** 요구 사항을 충족하는 워크북이 만들어집니다.

## 단계 5: 결과 워크북 저장 – 이제 각 상세 시트가 고유한 이름을 가짐

`Save` 호출은 파일을 디스크에 기록합니다. 워크북을 열면 다음과 같이 표시됩니다:

* **Sheet1** – 인보이스 헤더를 포함하는 마스터 시트.  
* **Detail_1**, **Detail_2**, … – 각 시트는 특정 인보이스에 해당하는 **Detail** 테이블의 행을 포함합니다.

다음은 예상 워크북 레이아웃의 모형(이미지는 예시이며, 필요에 따라 실제 스크린샷으로 교체할 수 있습니다)입니다.

![중복 상세 시트 생성 결과를 보여주는 Excel 파일 스크린샷](https://example.com/images/duplicated-detail-sheets.png)

### 예상 출력

| 시트 이름 | 내용 설명 |
|------------|----------------------|
| **Sheet1** | 마스터 행: InvoiceId, CustomerName, InvoiceDate |
| **Detail_1** | `InvoiceId = 101`인 상세 행 |
| **Detail_2** | `InvoiceId = 102`인 상세 행 |

`DuplicatedDetailSheets.xlsx`를 열면 정확히 이 구조가 표시됩니다.

## 전체 소스 코드 (복사 준비 완료)

```csharp
using System;
using System.Data;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace ExcelDetailSheetsDemo
{
    class Program
    {
        static void Main()
        {
            GenerateReport();
        }

        // ------------------------------------------------------------
        // Step 1 – data source
        // ------------------------------------------------------------
        static DataSet GetReportDataSet()
        {
            var ds = new DataSet();

            var master = new DataTable("Master");
            master.Columns.Add("InvoiceId", typeof(int));
            master.Columns.Add("CustomerName", typeof(string));
            master.Columns.Add("InvoiceDate", typeof(DateTime));
            master.Rows.Add(101, "Acme Corp", new DateTime(2024, 12, 01));
            master.Rows.Add(102, "Beta Ltd.", new DateTime(2024, 12, 03));
            ds.Tables.Add(master);

            var detail = new DataTable("Detail");
            detail.Columns.Add("InvoiceId", typeof(int));
            detail.Columns.Add("Product", typeof(string));
            detail.Columns.Add("Quantity", typeof(int));
            detail.Columns.Add("Price", typeof(decimal));
            detail.Rows.Add(101, "Widget A", 5, 9.99m);
            detail.Rows.Add(101, "Widget B", 2, 19.95m);
            detail.Rows.Add(102, "Gadget X", 1, 99.00m);
            detail.Rows.Add(102, "Gadget Y", 3, 49.50m);
            ds.Tables.Add(detail);

            return ds;
        }

        // ------------------------------------------------------------
        // Step 2 – processor configuration
        // ------------------------------------------------------------
        static SmartMarkerProcessor ConfigureProcessor()
        {
            var processor = new SmartMarkerProcessor();
            processor.Options.DetailSheetNewName = "Detail_{0}";
            processor.Options.KeepTemplate


## 다음에 배울 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료에는 전체 작동 코드 예제와 단계별 설명이 포함되어 있어 추가 API 기능을 마스터하고 자체 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [시트 자동 이름 지정 방법 – C#에서 여러 시트 생성](/cells/english/net/smart-markers-dynamic-data/how-to-name-sheets-automatically-generate-multiple-sheets-in/)
- [워크시트 만들기 – 동적 Excel 생성 단계별 가이드](/cells/english/net/worksheet-operations/how-to-create-worksheets-step-by-step-guide-for-dynamic-exce/)
- [C#에서 Excel 보고서 생성 – SmartMarker 사용 전체 가이드](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}