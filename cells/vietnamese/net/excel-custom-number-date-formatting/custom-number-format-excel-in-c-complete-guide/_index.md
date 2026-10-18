---
category: general
date: 2026-03-22
description: Hướng dẫn định dạng số tùy chỉnh trong Excel, trình bày cách nhập datatable
  vào Excel, đặt màu nền cho cột, định dạng cột dưới dạng tiền tệ và lưu sổ làm việc
  dưới dạng xlsx.
draft: false
keywords:
- custom number format excel
- import datatable to excel
- set column background color
- format column as currency
- save workbook as xlsx
language: vi
og_description: Hướng dẫn định dạng số tùy chỉnh trong Excel, chỉ dẫn bạn cách nhập
  DataTable, đặt màu nền cho cột, định dạng cột dưới dạng tiền tệ và lưu sổ làm việc
  dưới dạng xlsx.
og_title: Định dạng số tùy chỉnh trong Excel bằng C# – Hướng dẫn từng bước
tags:
- C#
- Excel automation
- Aspose.Cells
- Data export
title: Định dạng số tùy chỉnh trong Excel bằng C# – Hướng dẫn đầy đủ
url: /vi/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Định dạng số tùy chỉnh trong Excel – Hướng dẫn Full‑Stack C# 

Bạn đã bao giờ tự hỏi làm thế nào để áp dụng **custom number format excel** trực tiếp từ C# chưa? Có thể bạn đã thử xuất một DataTable ra bảng tính nhưng chỉ thấy các số thuần, không có màu sắc và không có định dạng tiền tệ. Đó là một vấn đề phổ biến—đặc biệt khi bạn cần một báo cáo chuyên nghiệp cho các bên liên quan.

Trong hướng dẫn này, chúng ta sẽ giải quyết vấn đề đó cùng nhau: bạn sẽ học cách **import datatable to excel**, **set column background color**, **format column as currency**, và cuối cùng **save workbook as xlsx** với một định dạng số tùy chỉnh làm cho các con số của bạn nổi bật. Không có những tham chiếu mơ hồ, chỉ có một giải pháp hoàn chỉnh, có thể chạy ngay mà bạn có thể sao chép‑dán vào dự án của mình.

---

## Những gì bạn sẽ xây dựng

Khi kết thúc tutorial, bạn sẽ có một ứng dụng console C# tự chứa mà:

1. Lấy một `DataTable` (bạn có thể thay thế đoạn mẫu bằng truy vấn của riêng mình).  
2. Tạo một workbook Excel mới bằng Aspose.Cells (hoặc bất kỳ thư viện tương thích nào).  
3. Áp dụng phông chữ xanh, đậm cho cột đầu tiên, nền màu vàng nhạt cho cột thứ hai, và định dạng tiền tệ (`$#,##0.00`) cho cột thứ ba.  
4. Lưu file dưới tên `DataTableWithStyleArray.xlsx` vào thư mục bạn chọn.

Bạn sẽ thấy chính xác mỗi dòng mã đóng góp như thế nào vào file Excel cuối cùng, và chúng ta sẽ thảo luận vì sao những lựa chọn đó quan trọng đối với khả năng bảo trì và hiệu suất.

---

## Yêu cầu trước

- .NET 6.0 hoặc mới hơn (mã cũng hoạt động với .NET Framework 4.7+).  
- Aspose.Cells for .NET (bản dùng thử miễn phí hoặc bản có giấy phép). Cài đặt qua NuGet:

```bash
dotnet add package Aspose.Cells
```

- Kiến thức cơ bản về `DataTable` và các ứng dụng console C#.

---

## Bước 1: Lấy dữ liệu nguồn dưới dạng DataTable

Đầu tiên, chúng ta cần một số dữ liệu để xuất. Trong thực tế, bạn có thể gọi một repository hoặc chạy một truy vấn SQL. Để minh họa, chúng ta sẽ tạo một bảng đơn giản trong bộ nhớ.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetSampleData()
{
    var table = new DataTable("Sales");
    table.Columns.Add("Product", typeof(string));
    table.Columns.Add("Quantity", typeof(int));
    table.Columns.Add("Revenue", typeof(decimal));

    table.Rows.Add("Widget A", 120, 3450.75m);
    table.Rows.Add("Widget B", 85, 2190.00m);
    table.Rows.Add("Widget C", 60, 1580.40m);

    return table;
}
```

> **Tại sao điều này quan trọng:** Sử dụng `DataTable` cung cấp cho bạn một nguồn dữ liệu dạng bảng, có schema, ánh xạ sạch sẽ vào các hàng và cột của Excel. Nó cũng cho phép bạn tái sử dụng cùng một logic xuất cho bất kỳ tập dữ liệu nào mà không cần viết lại mã.

---

## Bước 2: Tạo Workbook mới và lấy Worksheet đầu tiên

Bây giờ chúng ta khởi tạo một workbook Excel. Lớp `Workbook` đại diện cho toàn bộ file; `Worksheets[0]` là sheet mặc định nơi chúng ta sẽ đưa dữ liệu vào.

```csharp
// Initialize a fresh workbook
Workbook workbook = new Workbook();

// Grab the first (and only) worksheet
Worksheet worksheet = workbook.Worksheets[0];
```

> **Mẹo chuyên nghiệp:** Nếu bạn cần nhiều sheet, chỉ cần gọi `workbook.Worksheets.Add("SheetName")` và lặp lại các bước định dạng cho mỗi sheet.

---

## Bước 3: Định nghĩa Style cho các cột – Font, Background và Number Format

Việc định dạng trong Aspose.Cells được thực hiện qua các đối tượng `Style`. Chúng ta sẽ xây dựng một mảng, mỗi phần tử tương ứng với một cột trong DataTable.

```csharp
// Prepare an array to hold three distinct styles
Style[] columnStyles = new Style[3];

// 1️⃣ First column – blue, bold font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = System.Drawing.Color.Blue;
columnStyles[0].Font.IsBold = true;

// 2️⃣ Second column – light‑yellow background
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
columnStyles[1].Pattern = BackgroundType.Solid;

// 3️⃣ Third column – custom currency format (custom number format excel)
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Custom = "$#,##0.00";
```

> **Tại sao lại dùng mảng style?** Việc truyền một mảng vào `ImportDataTable` cho phép bạn áp dụng một style riêng cho mỗi cột trong một lần gọi, vừa ngắn gọn vừa hiệu quả. Nó cũng đảm bảo định dạng luôn đồng bộ với thứ tự dữ liệu.

---

## Bước 4: Import DataTable đồng thời áp dụng các Style

Đây là phần cốt lõi của thao tác: chúng ta đưa `DataTable` vào worksheet, yêu cầu Aspose bao gồm hàng tiêu đề, và truyền mảng `columnStyles` của chúng ta.

```csharp
// Import data starting at cell A1 (row 0, column 0)
worksheet.Cells.ImportDataTable(
    GetSampleData(),   // source DataTable
    true,              // include column names as header
    0, 0,              // start row, start column
    columnStyles);     // apply the style array
```

> **Điều gì xảy ra phía sau?** Aspose duyệt qua từng cột, ghi tiêu đề, sau đó ghi giá trị từng hàng. Trong quá trình này nó áp dụng `Style` tương ứng từ mảng, vì vậy bạn sẽ có tiêu đề màu xanh cho “Product”, cột “Quantity” nền vàng nhạt, và cột “Revenue” được định dạng tiền tệ đẹp mắt.

---

## Bước 5: Lưu Workbook dưới dạng file XLSX

Cuối cùng, chúng ta ghi workbook ra đĩa. Phương thức `Save` tự động chọn định dạng XLSX dựa trên phần mở rộng file.

```csharp
// Choose a folder that exists on your machine
string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";

// Ensure the directory exists (optional safety check)
System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);

// Save the workbook
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

> **Mẹo:** Nếu bạn cần stream file (ví dụ cho một API web), dùng `workbook.Save(stream, SaveFormat.Xlsx)` thay vì đường dẫn file.

---

## Ví dụ hoàn chỉnh

Dưới đây là chương trình đầy đủ mà bạn có thể dán vào một dự án console mới. Nó biên dịch và chạy ngay, tạo ra một file Excel có định dạng.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Get data
            DataTable dataTable = GetSampleData();

            // Step 2 – Create workbook & worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 3 – Prepare column styles
            Style[] columnStyles = new Style[3];

            // Font style for first column (blue, bold)
            columnStyles[0] = workbook.CreateStyle();
            columnStyles[0].Font.Color = System.Drawing.Color.Blue;
            columnStyles[0].Font.IsBold = true;

            // Background style for second column (light yellow)
            columnStyles[1] = workbook.CreateStyle();
            columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
            columnStyles[1].Pattern = BackgroundType.Solid;

            // Currency format for third column (custom number format excel)
            columnStyles[2] = workbook.CreateStyle();
            columnStyles[2].Custom = "$#,##0.00";

            // Step 4 – Import data with styles
            worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

            // Step 5 – Save as XLSX
            string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";
            System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }

        // Helper method to build a demo DataTable
        static DataTable GetSampleData()
        {
            var table = new DataTable("Sales");
            table.Columns.Add("Product", typeof(string));
            table.Columns.Add("Quantity", typeof(int));
            table.Columns.Add("Revenue", typeof(decimal));

            table.Rows.Add("Widget A", 120, 3450.75m);
            table.Rows.Add("Widget B", 85, 2190.00m);
            table.Rows.Add("Widget C", 60, 1580.40m);

            return table;
        }
    }
}
```

### Kết quả mong đợi

Khi mở `DataTableWithStyleArray.xlsx` bạn sẽ thấy:

| **Product** (blue, bold) | **Quantity** (light‑yellow) | **Revenue** (currency) |
|--------------------------|-----------------------------|------------------------|
| Widget A                 | 120                         | $3,450.75              |
| Widget B                 | 85                          | $2,190.00              |
| Widget C                 | 60                          | $1,580.40              |

**custom number format excel** mà bạn đã chỉ định (`$#,##0.00`) sẽ đảm bảo mỗi ô doanh thu hiển thị dấu đô la, dấu phân cách hàng nghìn và hai chữ số thập phân—đúng như những gì các bộ phận tài chính mong đợi.

---

## Câu hỏi thường gặp & Các trường hợp đặc biệt

### Tôi có thể dùng thư viện Excel khác không?

Chắc chắn rồi. Ý tưởng—tạo một style cho mỗi cột và áp dụng trong quá trình import—có thể chuyển sang EPPlus, ClosedXML, hoặc NPOI. Các lệnh API sẽ khác, nhưng mẫu vẫn giữ nguyên.

### Nếu DataTable của tôi có nhiều cột hơn số style đã định nghĩa thì sao?

Aspose sẽ áp dụng style mặc định cho bất kỳ cột nào không có mục tương ứng trong mảng `columnStyles`. Để tránh bất ngờ, hãy đặt kích thước mảng bằng `dataTable.Columns.Count` hoặc tạo style động trong một vòng lặp.

### Làm sao để đặt custom number format cho ngày tháng?

Chỉ cần đặt `style.Custom = "dd‑mm‑yyyy"` (hoặc bất kỳ chuỗi định dạng Excel hợp lệ nào). Cách tiếp cận dựa trên mảng cũng hoạt động cho ngày, phần trăm, hoặc ký hiệu khoa học.

### Có cách tự động điều chỉnh độ rộng cột sau khi import không?

Có—gọi `worksheet.AutoFitColumns();` sau khi import. Nó sẽ tính nhanh độ rộng dựa trên nội dung ô.

### Còn các tập dữ liệu lớn (hơn 100k dòng) thì sao?

`ImportDataTable` được tối ưu cho các thao tác bulk, nhưng bạn có thể gặp giới hạn bộ nhớ. Trong trường hợp đó, hãy cân nhắc stream từng hàng bằng `Cells[i, j].PutValue(...)` và tái sử dụng một đối tượng `Style` duy nhất để giảm tải.

---

## Mẹo chuyên nghiệp & Những lỗi thường gặp

- **Tránh hard‑code đường dẫn** trong mã production; sử dụng `Environment.GetFolderPath` hoặc cấu hình.  
- **Giải phóng workbook** nếu bạn chạy trong một service lâu dài—đặt trong khối `using` để giải phóng tài nguyên gốc.  
- **Cẩn thận với dấu phân cách phụ thuộc vào culture**. Định dạng `$#,##0.00` buộc dấu thập phân là dấu chấm bất kể locale OS, thường là điều bạn muốn cho báo cáo tài chính.  
- **Nhớ tham chiếu System.Drawing** (hoặc `System.Drawing.Common` trên .NET Core) để sử dụng các struct màu trong việc định dạng.  
- **Kiểm tra đầu ra trên các phiên bản Excel khác nhau**; các phiên bản cũ có thể diễn giải một số định dạng tùy chỉnh hơi khác nhau.

---

## Kết luận

Chúng ta đã bao quát mọi thứ bạn cần để **custom number format excel** từ C#: lấy dữ liệu từ `DataTable`, **import datatable to excel**, áp dụng **set column background color**, sử dụng **format column as currency**, và cuối cùng **save workbook as x

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}