---
category: general
date: 2026-10-07
description: Tạo các sheet chi tiết sao chép trong Excel bằng C#. Tìm hiểu cách tạo
  nhiều worksheet và xây dựng báo cáo từ các bảng trong một lần thực thi.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicated detail sheets
- how to generate multiple worksheets
- generate excel report from tables
language: vi
lastmod: 2026-10-07
og_description: Tạo các sheet chi tiết trùng lặp trong Excel bằng C#. Bài hướng dẫn
  này chỉ cách tạo nhiều worksheet và tạo báo cáo Excel đầy đủ từ các bảng.
og_image_alt: Screenshot of an Excel file that has create duplicated detail sheets
  output
og_title: Tạo các sheet chi tiết trùng lặp trong Excel – hướng dẫn C# chi tiết từng
  bước
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
title: Tạo các sheet chi tiết sao chép trong Excel bằng C#
url: /vi/net/excel-copy-worksheet/create-duplicated-detail-sheets-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo các sheet chi tiết sao chép trong Excel bằng C#

Nếu bạn cần **tạo các sheet chi tiết sao chép** trong một workbook Excel, hướng dẫn này sẽ dẫn bạn qua toàn bộ quá trình. Bạn sẽ thấy cách **tạo nhiều worksheet** từ một bộ dữ liệu master‑detail và tạo ra một báo cáo Excel hoàn chỉnh trực tiếp từ các bảng.

Việc tạo báo cáo Excel từ các bảng là một yêu cầu phổ biến cho các hệ thống thanh toán, bảng điều khiển tồn kho, hoặc bất kỳ kịch bản nào mà một bản ghi master có nhiều hàng chi tiết liên quan. Khi kết thúc tutorial này, bạn sẽ có một chương trình C# có thể chạy được, tạo ra một workbook với một sheet master và một sheet có tên duy nhất cho mỗi nhóm chi tiết.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có:

* .NET 6.0 (hoặc mới hơn) đã được cài đặt  
* Visual Studio 2022 hoặc bất kỳ IDE nào hỗ trợ C#  
* Gói NuGet **Aspose.Cells for .NET** (cung cấp `SmartMarkerProcessor`)  

Bạn có thể thêm gói này bằng lệnh sau:

```bash
dotnet add package Aspose.Cells
```

## Tổng quan về giải pháp

Giải pháp tuân theo năm bước sau:

1. **Lấy nguồn dữ liệu** chứa một bảng master và hai bảng detail.  
2. **Cấu hình Smart‑marker processor** để mỗi sheet chi tiết sao chép nhận được một tên duy nhất.  
3. **Tạo một workbook mới** và đặt một smart‑marker tham chiếu tới bảng master.  
4. **Chạy processor** để tạo sheet master và tất cả các sheet detail.  
5. **Lưu workbook** – mỗi sheet detail bây giờ có một tên riêng biệt.

Mỗi bước sẽ được giải thích chi tiết bên dưới, kèm theo mã nguồn đầy đủ và lý do.

## Bước 1: Lấy nguồn dữ liệu chứa một bảng master và hai bảng detail

Nhiệm vụ đầu tiên là xây dựng một `DataSet` mô phỏng dữ liệu bạn thường lấy từ cơ sở dữ liệu. `DataSet` phải chứa một bảng có tên **Master** và một hoặc nhiều bảng có tên **Detail**. Engine Smart‑marker sử dụng các tên bảng này để điền dữ liệu vào workbook.

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

**Tại sao điều này quan trọng:**  
*Smart‑marker* làm việc với các đối tượng `DataSet`; mỗi tên bảng trở thành một marker mà engine có thể thay thế. Bằng cách cấu trúc dữ liệu như vậy, bạn cho phép processor tự động sao chép sheet detail cho mỗi `InvoiceId` riêng biệt.

## Bước 2: Cấu hình Smart‑marker processor để mỗi sheet detail sao chép có một tên duy nhất

Khi processor gặp một marker detail, nó sẽ tạo một worksheet mới cho mỗi nhóm hàng. Mặc định, các sheet mới có cùng tên, dẫn đến xung đột tên. Thiết lập `DetailSheetNewName` cho engine biết cách đổi tên mỗi bản sao.

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

**Tại sao điều này quan trọng:**  
Nếu không có mẫu đặt tên duy nhất, workbook sẽ ném ra ngoại lệ khi processor cố gắng thêm sheet detail thứ hai. Placeholder `{0}` đảm bảo mỗi sheet nhận được một tên riêng, dự đoán được.

## Bước 3: Tạo một workbook mới và đặt một smart‑marker tham chiếu tới bảng master

Bây giờ bạn tạo một `Workbook` mới, thêm một marker trỏ tới bảng **Master**, và tùy chọn định dạng dòng tiêu đề.

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

**Tại sao điều này quan trọng:**  
Marker `{{Master}}` chỉ thị cho processor mở rộng bảng master bắt đầu tại `A1`. Các dòng tiếp theo sẽ trở thành các hàng dữ liệu cho mỗi bản ghi master. Đây là điểm khởi đầu để **generate excel report from tables**.

## Bước 4: Chạy smart‑marker processor để tạo sheet master và các sheet detail

Với nguồn dữ liệu, processor và mẫu sẵn sàng, bạn gọi `Process`. Engine mở rộng marker master, sau đó tạo một sheet detail riêng cho mỗi `InvoiceId` duy nhất.

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

**Tại sao điều này quan trọng:**  
`processor.Process` thực hiện phần công việc nặng: nó đọc các hàng master, tạo một sheet detail cho mỗi khóa duy nhất, và đổi tên các sheet đó theo mẫu đã định nghĩa ở bước trước. Kết quả là một workbook đáp ứng yêu cầu **how to generate multiple worksheets**.

## Bước 5: Lưu workbook kết quả – mỗi sheet detail bây giờ có một tên riêng biệt

Lệnh `Save` ghi file ra đĩa. Khi bạn mở workbook, bạn sẽ thấy:

* **Sheet1** – sheet master chứa các tiêu đề hoá đơn.  
* **Detail_1**, **Detail_2**, … – mỗi sheet chứa các hàng từ bảng **Detail** thuộc một hoá đơn cụ thể.

Dưới đây là một mô phỏng bố cục workbook mong đợi (hình ảnh chỉ mang tính minh họa; bạn có thể thay bằng ảnh chụp màn hình thực tế nếu muốn).

![Screenshot of an Excel file that has create duplicated detail sheets output](https://example.com/images/duplicated-detail-sheets.png)

### Kết quả mong đợi

| Tên sheet | Mô tả nội dung |
|------------|----------------------|
| **Sheet1** | Các hàng Master: InvoiceId, CustomerName, InvoiceDate |
| **Detail_1** | Các hàng Detail nơi `InvoiceId = 101` |
| **Detail_2** | Các hàng Detail nơi `InvoiceId = 102` |

Mở file `DuplicatedDetailSheets.xlsx` sẽ hiển thị đúng cấu trúc này.

## Mã nguồn đầy đủ (sẵn sàng sao chép)



## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích chi tiết từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Name Sheets Automatically – Generate Multiple Sheets in C#](/cells/english/net/smart-markers-dynamic-data/how-to-name-sheets-automatically-generate-multiple-sheets-in/)
- [How to Create Worksheets – Step‑by‑Step Guide for Dynamic Excel Generation](/cells/english/net/worksheet-operations/how-to-create-worksheets-step-by-step-guide-for-dynamic-exce/)
- [How to Generate Excel Report in C# – Full Guide Using SmartMarker](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}