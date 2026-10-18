---
category: general
date: 2026-07-13
description: Định dạng cột ngày trong Excel khi xuất DataTable từ C#. Học cách xuất
  DataTable sang Excel bằng C# và nhập DataTable vào Excel với định dạng trong vài
  phút.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- format date column excel
- excel export datatable c#
- import datatable to excel
language: vi
lastmod: 2026-07-13
og_description: Định dạng cột ngày trong Excel một cách dễ dàng. Hướng dẫn này chỉ
  cho bạn cách xuất DataTable sang Excel bằng C# và nhập DataTable vào Excel với các
  kiểu tùy chỉnh.
og_image_alt: Screenshot showing a formatted date column in an Excel sheet generated
  from C#
og_title: Định dạng cột ngày trong Excel – Hướng dẫn xuất C# từng bước
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  headline: Format Date Column Excel – Complete C# Guide to Export DataTable
  type: TechArticle
- description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  name: Format Date Column Excel – Complete C# Guide to Export DataTable
  steps:
  - name: What if My DataTable Has More Than Three Columns?
    text: Just extend the `columnStyles` array. For any column you don’t explicitly
      style, leave the entry `null`; Excel will apply the default General format.
  - name: How to Apply a Custom Date Format (e.g., “dd‑MMM‑yyyy”)?
    text: 'Replace the built‑in number with a custom string:'
  - name: Can I Use This Approach with EPPlus or ClosedXML?
    text: 'Yes, the concept is identical: create a style object, assign it to a column,
      then load the `DataTable`. The API differs, but the **excel export datatable
      c#** pattern remains the same.'
  - name: What About Large DataSets (100k+ rows)?
    text: '`ImportDataTable` is optimized for bulk writes, but you might hit memory
      limits. In that case, consider streaming rows with `Cells.ImportDataTable` in
      chunks, or use `Worksheet.Cells["A1"].PutValue` in a loop while reusing the
      style objects.'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Export
title: Định dạng cột ngày trong Excel – Hướng dẫn C# đầy đủ để xuất DataTable
url: /vi/net/excel-custom-number-date-formatting/format-date-column-excel-complete-c-guide-to-export-datatabl/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Định dạng cột ngày trong Excel – Hướng dẫn C# đầy đủ để xuất DataTable

Bạn đã bao giờ cần **định dạng cột ngày trong Excel** khi lấy dữ liệu từ cơ sở dữ liệu, nhưng các ô vẫn hiển thị dấu thời gian thô? Bạn không phải là người duy nhất. Trong nhiều ứng dụng doanh nghiệp, việc xuất mặc định sẽ đổ giá trị `DateTime` như `2024‑03‑15 00:00:00` và không ai muốn những dữ liệu rối mắt đó.  

Tin tốt là bạn có thể kiểm soát chính xác cách hiển thị của mỗi cột ngay từ C#. Trong hướng dẫn này, chúng ta sẽ đi qua một giải pháp toàn diện **excel export datatable c#**, áp dụng kiểu ngày cho cột đầu tiên, kiểu tiền tệ cho cột thứ hai, và cuối cùng **import datatable to excel** mà không gặp khó khăn về định dạng.

Khi hoàn thành, bạn sẽ có một phương thức tái sử dụng có thể chèn vào bất kỳ dự án .NET nào, bất kể bạn đang dùng .NET 6, .NET Framework 4.8, hay phiên bản mới hơn.

---

## Những gì bạn cần

- **Aspose.Cells for .NET** (hoặc bất kỳ thư viện nào cung cấp `CreateStyle` và `ImportDataTable`). Các đoạn mã mẫu sử dụng Aspose vì API của nó sạch sẽ và được áp dụng rộng rãi.
- Một **DataTable** mà bạn đã điền dữ liệu từ SQL, CSV, hoặc bất kỳ nguồn nào khác.
- Visual Studio (hoặc IDE yêu thích của bạn).  
- .NET runtime 5.0+ (mẫu mục tiêu .NET 6, nhưng các framework cũ hơn cũng hoạt động tương tự).

Nếu bạn chưa có Aspose.Cells, hãy tải bản dùng thử miễn phí từ trang chính—không cần thẻ tín dụng.

---

## Bước 1: Lấy dữ liệu nguồn dưới dạng DataTable

Đầu tiên, bạn cần một `DataTable`. Trong các tình huống thực tế, thường lấy từ `SqlDataAdapter.Fill`, nhưng để minh bạch chúng ta sẽ mô phỏng một bảng đơn giản:

```csharp
using System;
using System.Data;

DataTable GetSampleData()
{
    var dt = new DataTable();
    dt.Columns.Add("OrderDate", typeof(DateTime));
    dt.Columns.Add("TotalAmount", typeof(decimal));
    dt.Columns.Add("Customer", typeof(string));

    dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
    dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
    dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");

    return dt;
}
```

> **Mẹo:** Khi bạn kéo dữ liệu trực tiếp từ stored procedure, hãy chắc chắn rằng kiểu cột khớp với định dạng Excel mong muốn. Cột `datetime` sẽ là mục tiêu cho kiểu **format date column excel** của chúng ta.

---

## Bước 2: Tạo Workbook Excel và Định nghĩa Kiểu cho Các Cột

Bây giờ chúng ta tạo một workbook mới. Bí quyết **format date column excel** nằm ở việc tạo một đối tượng `Style`, đặt thuộc tính `Number` thành định dạng ngày tích hợp sẵn của Excel (mã 14), và gán kiểu này cho chỉ số cột tương ứng.

```csharp
using Aspose.Cells;

Workbook wb = new Workbook();               // creates a blank workbook
Worksheet sheet = wb.Worksheets[0];        // we’ll work with the first sheet

// Prepare a style array – one entry per DataTable column
Style[] columnStyles = new Style[dt.Columns.Count];

// Column 0 – format as a short date (e.g., 03/15/2024)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Excel built‑in date format

// Column 1 – format as currency (e.g., $1,245.67)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].Number = 2;                // Built‑in currency format

// Column 2 – no special formatting; leave null or default
columnStyles[2] = null;
```

Tại sao `Number = 14`? Excel lưu ngày dưới dạng số serial; định dạng 14 yêu cầu chương trình hiển thị các số này theo mẫu ngày ngắn của locale. Nếu bạn cần mẫu tùy chỉnh (như `dd‑MMM‑yyyy`), có thể đặt `columnStyles[0].Custom = "dd-MMM-yyyy"` thay thế.

---

## Bước 3: Nhập DataTable vào Worksheet với Các Kiểu Định dạng

Với mảng kiểu đã sẵn sàng, lời gọi nhập chỉ cần một dòng. Đây là phần cốt lõi của **excel export datatable c#** và cũng là nơi chúng ta **import datatable to excel** đồng thời giữ nguyên định dạng.

```csharp
// Import the DataTable, include column headers, start at cell A1 (row 0, column 0)
sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
```

Phiên bản `ImportDataTable` mà chúng ta dùng chấp nhận mảng kiểu, áp dụng mỗi kiểu cho cột tương ứng khi dữ liệu được ghi. Không cần vòng lặp xử lý sau—cột ngày của bạn đã được định dạng đẹp mắt.

---

## Bước 4: Lưu Workbook (hoặc Stream trực tiếp tới Browser)

Tùy theo kịch bản, bạn có thể lưu vào đĩa, một memory stream, hoặc trả về file dưới dạng HTTP response. Dưới đây là ba mẫu phổ biến:

```csharp
// 1️⃣ Save to a physical file
wb.Save("ExportedReport.xlsx");

// 2️⃣ Save to a MemoryStream (useful for ASP.NET Core)
using var ms = new MemoryStream();
wb.Save(ms, SaveFormat.Xlsx);
ms.Position = 0; // rewind for downstream consumers

// 3️⃣ Return as a file download in ASP.NET MVC
public IActionResult DownloadReport()
{
    var dt = GetSampleData();
    var wb = BuildWorkbook(dt); // encapsulate steps 2‑3 in a method
    using var ms = new MemoryStream();
    wb.Save(ms, SaveFormat.Xlsx);
    return File(ms.ToArray(), 
                "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
                "Report.xlsx");
}
```

> **Lưu ý:** Nếu bạn dùng `FileResult` trong ASP.NET Core, hãy đặt `Response.Headers["Cache-Control"] = "no-cache"` khi file được tạo động. Điều này ngăn trình duyệt trả về phiên bản cũ.

---

## Bước 5: Kiểm tra Kết quả – Sheet Excel Trông Như Thế Nào

Sau khi chạy mã, mở `ExportedReport.xlsx`. Bạn sẽ thấy:

| OrderDate (formatted) | TotalAmount (currency) | Customer |
|-----------------------|------------------------|----------|
| 03/13/2024            | $1,245.67              | Acme Corp|
| 03/14/2024            | $980.00                | Beta Ltd |
| 03/15/2024            | $1,500.25              | Gamma Inc|

Chú ý cách **format date column excel** hiển thị ngày ngắn gọn, trong khi cột tiền tệ tự động căn chỉnh theo cài đặt vùng miền của bạn. Không cần định dạng từng ô thủ công.

![format date column excel example](/images/format-date-column-excel.png)

*Alt ảnh: format date column excel – một ảnh chụp màn hình của sheet Excel với cột ngày được định dạng đúng.*

---

## Câu hỏi Thường gặp & Các Trường hợp Cạnh

### DataTable của tôi có hơn ba cột thì sao?

Chỉ cần mở rộng mảng `columnStyles`. Đối với bất kỳ cột nào bạn không định dạng rõ ràng, để giá trị `null`; Excel sẽ áp dụng định dạng General mặc định.

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 10; // Percent format, for example
```

### Làm sao áp dụng Định dạng Ngày Tùy chỉnh (ví dụ “dd‑MMM‑yyyy”)?

Thay thế số tích hợp bằng chuỗi tùy chỉnh:

```csharp
columnStyles[0].Custom = "dd-MMM-yyyy";
```

### Tôi có thể dùng cách này với EPPlus hoặc ClosedXML không?

Có, khái niệm vẫn giống nhau: tạo một đối tượng style, gán cho cột, rồi tải `DataTable`. API có thể khác, nhưng mẫu **excel export datatable c#** vẫn giữ nguyên.

### Còn các DataSet lớn (hơn 100k dòng) thì sao?

`ImportDataTable` được tối ưu cho ghi bulk, nhưng bạn có thể gặp giới hạn bộ nhớ. Trong trường hợp đó, hãy cân nhắc stream các hàng bằng `Cells.ImportDataTable` theo từng khối, hoặc dùng `Worksheet.Cells["A1"].PutValue` trong vòng lặp đồng thời tái sử dụng các đối tượng style.

---

## Ví dụ Hoàn chỉnh (Tất cả các Bước trong Một Phương thức)

Dưới đây là một phương thức tự chứa mà bạn có thể sao chép‑dán vào bất kỳ console app hoặc controller ASP.NET nào. Nó minh họa toàn bộ quy trình—from lấy dữ liệu tới xuất Excel có định dạng.

```csharp
using System;
using System.Data;
using System.IO;
using Aspose.Cells;

public class ExcelExporter
{
    // Entry point for demonstration
    public static void Main()
    {
        DataTable dt = GetSampleData();
        Workbook wb = BuildWorkbook(dt);
        wb.Save("StyledExport.xlsx");
        Console.WriteLine("Excel file created – check StyledExport.xlsx");
    }

    // Generates the sample DataTable (Step 1)
    private static DataTable GetSampleData()
    {
        var dt = new DataTable();
        dt.Columns.Add("OrderDate", typeof(DateTime));
        dt.Columns.Add("TotalAmount", typeof(decimal));
        dt.Columns.Add("Customer", typeof(string));

        dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
        dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
        dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");
        return dt;
    }

    // Builds the workbook with styled columns (Steps 2‑3)
    private static Workbook BuildWorkbook(DataTable dt)
    {
        var wb = new Workbook();
        var sheet = wb.Worksheets[0];

        // Allocate style array
        Style[] columnStyles = new Style[dt.Columns.Count];

        // Format column 0 as short date
        columnStyles[0] = wb.CreateStyle();
        columnStyles[0].Number = 14; // short date

        // Format column 1 as currency
        columnStyles[1] = wb.CreateStyle();
        columnStyles[1].Number = 2; // currency

        // No style for column 2 (Customer name)
        columnStyles[2] = null;

        // Import with headers, start at A1
        sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
        return wb;
    }
}
```

Chạy chương trình, mở `StyledExport.xlsx`, và bạn sẽ thấy **format date column excel** được áp dụng hoàn hảo.

---

## Tóm tắt & Các Bước Tiếp Theo

Chúng ta vừa tìm hiểu cách **format date column excel** khi thực hiện **excel export datatable c#**, và cách **import datatable to excel** với định dạng từng cột trong một lời gọi duy nhất. Những điểm chính:

1. Tạo một `Style` cho mỗi cột cần định dạng.  
2. Dùng `Number = 14` cho ngày, `Number = 2` cho tiền tệ, hoặc bất kỳ định dạng tùy chỉnh nào bạn cần.  
3. Truyền mảng style vào `ImportDataTable`—thư viện sẽ làm phần còn lại.

Bạn có thể khám phá tiếp:

- **Conditional formatting** để làm nổi bật các ngày quá hạn.  
- **


## Bạn Nên Học Gì Tiếp Theo?


Các hướng dẫn sau đây liên quan chặt chẽ đến các kỹ thuật đã trình bày trong bài viết này. Mỗi tài nguyên đều bao gồm mã nguồn đầy đủ và giải thích chi tiết từng bước, giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Export Excel Data to DataTable Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/import-export/export-excel-data-datatatable-aspose-cells-net/)
- [Export HTML Strings from Excel to DataTable using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}