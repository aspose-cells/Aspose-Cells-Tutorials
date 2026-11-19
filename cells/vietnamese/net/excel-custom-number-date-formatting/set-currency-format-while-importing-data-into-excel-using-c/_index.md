---
category: general
date: 2026-11-19
description: Đặt định dạng tiền tệ trong Excel bằng C# – tìm hiểu cách thiết lập định
  dạng số và kiểu cho các cột Excel khi nhập một bảng tính Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set currency format
- how to set number format
- assign number format
- excel worksheet import
- style excel columns
language: vi
lastmod: 2026-11-19
og_description: Đặt định dạng tiền tệ trong Excel bằng C# và khám phá cách thiết lập
  định dạng số, gán định dạng số và tạo kiểu cho các cột Excel khi nhập bảng tính.
og_image_alt: Screenshot showing Excel cells formatted as currency after import
og_title: Đặt định dạng tiền tệ trong Excel bằng C# – hướng dẫn chi tiết từng bước
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  headline: Set currency format while importing data into Excel using C#
  type: TechArticle
- description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  name: Set currency format while importing data into Excel using C#
  steps:
  - name: Expected result
    text: 'When you open **FinancialReport.xlsx**, you’ll see:'
  - name: Assign number format to date columns
    text: '```csharp // Suppose column 2 contains dates and you want "dd-MMM-yyyy"
      columnStyles[2].Number = 14; // 14 = built‑in short date ```'
  - name: Use custom number formats for percentages
    text: '```csharp columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00% ```'
  - name: Styling beyond number formats
    text: 'You can also set font, background color, or alignment on the same `Style`
      object:'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
- Formatting
title: Đặt định dạng tiền tệ khi nhập dữ liệu vào Excel bằng C#
url: /vi/net/excel-custom-number-date-formatting/set-currency-format-while-importing-data-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Đặt định dạng tiền tệ khi nhập dữ liệu vào Excel bằng C#

Nếu bạn cần **đặt định dạng tiền tệ** trong một worksheet Excel, hướng dẫn này sẽ chỉ cho bạn cách **đặt định dạng số** và tạo kiểu cho các cột khi thực hiện **nhập worksheet Excel**. Bạn sẽ thấy một ví dụ hoàn chỉnh, có thể chạy được, gán định dạng số đúng cho mỗi cột của `DataTable` và nhập dữ liệu với kiểu dáng mong muốn.

Làm việc với Excel từ C# thường đòi hỏi hơn chỉ việc đổ giá trị thô—bạn còn phải kiểm soát cách hiển thị các số. Dù bạn đang tạo hoá đơn, báo cáo tài chính, hay bảng điều khiển, việc định dạng đúng tiền tệ, phần trăm hoặc ngày tháng sẽ khiến đầu ra ngay lập tức dễ đọc.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có:

* .NET 6.0 (hoặc mới hơn) đã được cài đặt.
* Tham chiếu tới **Aspose.Cells for .NET** (hoặc bất kỳ thư viện nào cung cấp lớp `Style` với thuộc tính `Number`).  
  *NuGet*: `Install-Package Aspose.Cells`.
* Kiến thức cơ bản về `DataTable` và các collection trong C#.
* Một IDE như Visual Studio 2022 hoặc VS Code.

## Bước 1: Lấy dữ liệu cần ghi vào worksheet

Đầu tiên, tạo một `DataTable` chứa dữ liệu thô mà bạn muốn xuất. Trong các dự án thực tế, dữ liệu này có thể đến từ truy vấn cơ sở dữ liệu, lời gọi API, hoặc trình phân tích CSV.

```csharp
using System.Data;

/// <summary>
/// Returns a sample DataTable with three columns:
/// Id (int), Amount (decimal), and Description (string).
/// </summary>
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Amount", typeof(decimal));
    table.Columns.Add("Description", typeof(string));

    // Sample rows
    table.Rows.Add(1, 1234.56m, "Office supplies");
    table.Rows.Add(2, 98765.43m, "Consulting fees");
    table.Rows.Add(3, 0.99m, "Miscellaneous");

    return table;
}

// Retrieve the data
DataTable dataTable = GetData();
```

> **Tại sao điều này quan trọng:** Việc nhập một `DataTable` đã được điền đầy cho phép bạn tách riêng logic lấy dữ liệu khỏi logic tạo Excel, giúp tăng khả năng kiểm thử và bảo trì.

## Bước 2: Tạo mảng kiểu – một phần tử cho mỗi cột trong DataTable

Aspose.Cells yêu cầu một `Style[]` có độ dài bằng số cột bạn dự định nhập. Mỗi phần tử có thể chứa một định dạng số cụ thể.

```csharp
// Allocate a Style object for each column
Style[] columnStyles = new Style[dataTable.Columns.Count];

// Initialize each Style instance (required before assigning properties)
for (int i = 0; i < columnStyles.Length; i++)
{
    columnStyles[i] = ws.Workbook.CreateStyle();
}
```

> **Mẹo:** Ngay cả khi bạn chỉ cần định dạng cho một phần của các cột, bạn vẫn phải tạo một thể hiện `Style` cho mọi cột; nếu không sẽ gặp `NullReferenceException` khi nhập.

## Bước 3: Gán định dạng số cho các cột mong muốn

Các số định dạng tích hợp khác nhau tùy thư viện. Trong Aspose.Cells:

* `0` → General (số nguyên)  
* `2` → Currency (ví dụ: `$#,##0.00`)  
* `3` → Date, v.v.

Ở đây chúng ta **gán định dạng số** cho hai cột: cột đầu tiên (Id) giữ nguyên dạng số nguyên, trong khi cột thứ hai (Amount) nhận định dạng tiền tệ.

```csharp
// Column 0 → integer format (style number 0)
columnStyles[0].Number = 0;

// Column 1 → currency format (style number 2)
columnStyles[1].Number = 2;

// If you need a custom format, you can also use a format string:
// columnStyles[1].Custom = "$#,##0.00";
```

> **Cách đặt định dạng số:** Sử dụng thuộc tính `Number` là cách nhanh nhất để chọn một định dạng tích hợp. Đối với tiền tệ theo địa phương, hãy cân nhắc dùng chuỗi định dạng tùy chỉnh có ký hiệu tiền tệ phù hợp.

## Bước 4: Nhập DataTable vào worksheet, áp dụng kiểu cho các cột

Khi mảng kiểu đã sẵn sàng, tiến hành nhập dữ liệu. Phương thức `ImportDataTable` sẽ tôn trọng các kiểu bạn đã truyền vào.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];

// Import the DataTable, starting at cell A1 (row 0, column 0)
// The third argument (true) tells the method to write column headers.
ws.Cells.ImportDataTable(
    dataTable,
    /* includeColumnNames */ true,
    /* startRow */ 0,
    /* startColumn */ 0,
    columnStyles);

// Save the workbook
workbook.Save("FinancialReport.xlsx", SaveFormat.Xlsx);
```

### Kết quả mong đợi

Khi bạn mở **FinancialReport.xlsx**, sẽ thấy:

| Id | Amount      | Description      |
|----|------------|------------------|
| 1  | $1,234.56  | Văn phòng phẩm   |
| 2  | $98,765.43 | Phí tư vấn       |
| 3  | $0.99      | Khác biệt        |

*Cột **Amount** được hiển thị bằng định dạng tiền tệ mà bạn đã đặt, trong khi **Id** vẫn là số nguyên.*

## Cách đặt định dạng số cho các kịch bản bổ sung

### Gán định dạng số cho các cột ngày tháng

```csharp
// Suppose column 2 contains dates and you want "dd-MMM-yyyy"
columnStyles[2].Number = 14; // 14 = built‑in short date
```

### Sử dụng định dạng số tùy chỉnh cho phần trăm

```csharp
columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00%
```

### Định dạng ngoài định dạng số

Bạn cũng có thể đặt phông chữ, màu nền hoặc căn chỉnh trên cùng một đối tượng `Style`:

```csharp
columnStyles[1].Font.IsBold = true;
columnStyles[1].ForegroundColor = Color.LightYellow;
columnStyles[1].HorizontalAlignment = TextAlignmentType.Center;
```

> **Tại sao cách này hoạt động:** Đối tượng `Style` tổng hợp tất cả các thuộc tính hiển thị cho một ô. Khi bạn truyền mảng này vào `ImportDataTable`, mỗi ô sẽ tự động kế thừa kiểu đã định nghĩa.

## Những lỗi thường gặp và cách tránh

| Vấn đề | Triệu chứng | Cách khắc phục |
|--------|-------------|----------------|
| Quên khởi tạo mỗi `Style` | `NullReferenceException` khi nhập | Duyệt mảng và gọi `CreateStyle()` trước khi đặt thuộc tính. |
| Dùng chỉ số số tích hợp sai | Định dạng sai (ví dụ: ngày hiển thị dưới dạng số nguyên) | Tham khảo tài liệu thư viện để biết các hằng số `Number` đúng. |
| Không lưu workbook | Không có file đầu ra hoặc file rỗng | Gọi `workbook.Save(...)` sau khi quá trình nhập hoàn tất. |
| Không khớp locale với ký hiệu tiền tệ | `$` xuất hiện ngay cả trong locale không phải US | Dùng chuỗi định dạng tùy chỉnh với ký hiệu phù hợp (ví dụ, `"€#,##0.00"`). |

## Ví dụ đầy đủ, có thể chạy



## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong bài viết này. Mỗi tài nguyên đều bao gồm mã nguồn hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Create excel file c# – style cells and set currency format](/cells/english/net/excel-formatting-and-styling/create-excel-file-c-style-cells-and-set-currency-format/)
- [How to Format Excel Columns in C# – Complete Guide](/cells/english/net/formatting-rows-and-columns-in-excel/how-to-format-excel-columns-in-c-complete-guide/)
- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}