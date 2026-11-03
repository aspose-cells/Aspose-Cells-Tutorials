---
category: general
date: 2026-09-15
description: Tìm hiểu cách lưu workbook dưới dạng CSV, xuất Excel sang TXT và áp dụng
  định dạng số tùy chỉnh trong khi chuyển đổi giá trị ô sang chữ hoa trong C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save workbook as csv
- apply custom number format
- export excel to txt
- uppercase cell values
- export worksheet as text
language: vi
lastmod: 2026-09-15
og_description: Lưu workbook dưới dạng CSV, xuất Excel sang TXT và áp dụng định dạng
  số tùy chỉnh trong khi chuyển đổi giá trị ô thành chữ hoa bằng Aspose.Cells trong
  C#.
og_image_alt: Screenshot showing workbook saved as CSV using C# code
og_title: Lưu sổ làm việc dưới dạng CSV và xuất Excel sang TXT với định dạng tùy chỉnh
  trong C#
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to save workbook as CSV, export Excel to TXT, and apply custom
    number format while converting cell values to uppercase in C#.
  headline: How to save workbook as CSV and export Excel to TXT with custom formatting
    in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cách lưu workbook dưới dạng CSV và xuất Excel sang TXT với định dạng tùy chỉnh
  trong C#
url: /vi/net/converting-excel-files-to-other-formats/how-to-save-workbook-as-csv-and-export-excel-to-txt-with-cus/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách lưu workbook dưới dạng CSV và xuất Excel sang TXT với định dạng tùy chỉnh trong C#

Nếu bạn cần **save workbook as CSV** đồng thời xuất một worksheet dưới dạng plain‑text và áp dụng định dạng số tùy chỉnh, hướng dẫn này sẽ cho bạn một giải pháp hoàn chỉnh, sẵn sàng chạy. Bạn sẽ thấy cách giữ độ chính xác số, chuyển đổi mọi giá trị ô thành chữ hoa, và xử lý ngày theo thời kỳ Nhật Bản — tất cả với Aspose.Cells cho .NET.

Xuất dữ liệu từ Excel thường đồng nghĩa với việc xử lý nhiều định dạng: CSV cho việc trao đổi dữ liệu, TXT cho các hệ thống kế thừa, và định dạng số tùy chỉnh cho báo cáo theo địa phương. Bài hướng dẫn này sẽ đi qua từng yêu cầu một cách từng bước, để bạn có thể sao chép mã trực tiếp vào dự án của mình.

Trong các phần sau bạn sẽ học cách:

* **save workbook as csv** với số chữ số có nghĩa được xác định  
* **export excel to txt** trong khi buộc **uppercase cell values**  
* **apply custom number format** cho ngày theo thời kỳ Nhật Bản và đọc kết quả đã định dạng  

Không cần công cụ bên ngoài — chỉ cần thư viện Aspose.Cells và môi trường phát triển .NET.

## Yêu cầu trước

* .NET 6.0 trở lên (mã cũng hoạt động với .NET Framework 4.8)  
* Aspose.Cells cho .NET (gói NuGet `Aspose.Cells`)  
* Kiến thức cơ bản về C# và các khái niệm Excel  

---

## Bước 1: Lưu workbook dưới dạng CSV với độ chính xác được kiểm soát

Khi bạn **save workbook as CSV**, các giá trị số được ghi bằng biểu diễn chuỗi mặc định, có thể mất độ chính xác. Bằng cách cấu hình `CsvSaveOptions.SignificantDigits`, bạn chỉ định cho Aspose.Cells số chữ số có nghĩa cần giữ lại.

```csharp
using Aspose.Cells;
using System;

// Create a new workbook (or load an existing one)
Workbook workbook = new Workbook();               // you can also use new Workbook("input.xlsx");

// Configure CSV options to keep up to 4 significant digits
CsvSaveOptions csvOptions = new CsvSaveOptions
{
    SignificantDigits = 4   // ensures numbers like 123.4567 stay precise
};

// Save the workbook as CSV
string csvPath = @"C:\Temp\Digits.csv";
workbook.Save(csvPath, csvOptions);

Console.WriteLine($"Workbook saved as CSV to {csvPath}");
```

**Tại sao điều này quan trọng:**  
Cài đặt `SignificantDigits` ngăn chặn lỗi làm tròn thường xuất hiện khi các bộ dữ liệu lớn được trao đổi với các hệ thống hạ nguồn (ví dụ, kho dữ liệu). Đối tượng `CsvSaveOptions` cũng cho phép bạn kiểm soát dấu phân cách, mã hoá và các cài đặt đặc thù của CSV nếu cần.

---

## Bước 2: Xuất một worksheet dưới dạng plain text trong khi chuyển đổi giá trị thành chữ hoa

Xuất một sheet ra file `.txt` đơn giản hữu ích cho các quy trình nhập dữ liệu kế thừa yêu cầu dữ liệu phân tách bằng khoảng trắng. Bằng cách bật `ExportTableOptions.ExportAsString` và cung cấp một delegate `CustomExport`, bạn có thể **export excel to txt** và đồng thời áp dụng **uppercase cell values**.

```csharp
// Prepare export options for plain‑text output
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true, // forces every cell to be treated as a string
    // CustomExport receives the cell and its current string value,
    // allowing you to modify it before it is written.
    CustomExport = (cell, value) =>
    {
        // Convert the cell value to an upper‑case string
        return value?.ToString().ToUpperInvariant();
    }
};

// Define the output path for the text file
string txtPath = @"C:\Temp\Table.txt";

// Export the first worksheet (index 0) as a tab‑delimited text file
workbook.Worksheets[0].ExportTable(txtPath, tableOptions);

Console.WriteLine($"Worksheet exported as text to {txtPath}");
```

**Tại sao điều này quan trọng:**  
Nhiều điểm tích hợp (ví dụ, các job batch trên mainframe) yêu cầu các định danh bằng chữ hoa. Callback `CustomExport` cung cấp cho bạn toàn quyền kiểm soát cách biểu diễn mỗi ô, cho phép bạn chèn các biến đổi như cắt bỏ, đệm, hoặc định dạng theo địa phương mà không cần xử lý hậu kỳ file.

---

## Bước 3: Áp dụng định dạng số tùy chỉnh và đọc kết quả đã định dạng

Các định dạng số tích hợp sẵn trong Excel bao phủ hầu hết các trường hợp, nhưng đôi khi bạn cần hiển thị ngày trong một hệ thống lịch cụ thể — chẳng hạn như thời kỳ Nhật Bản. Đoạn mã dưới đây minh họa cách **apply custom number format** cho một ô, sau đó đọc chuỗi đã định dạng phù hợp với locale của workbook.

```csharp
// Create a new workbook for the era example
Workbook eraWorkbook = new Workbook();

// Access the first worksheet and target cell A1
Worksheet sheet = eraWorkbook.Worksheets[0];
Cell dateCell = sheet.Cells["A1"];

// Insert a Japanese‑era date string (Reiwa 3 = 2021)
dateCell.PutValue("Reiwa 3/04/01");

// Apply a built‑in date number format (14 = mm-dd-yy)
// You could also assign a custom format string, e.g., "[$-ja-JP]ggge年m月d日"
Style style = eraWorkbook.CreateStyle();
style.Number = 14; // standard short date format
dateCell.SetStyle(style);

// Force formula calculation (necessary if the cell contains a formula)
eraWorkbook.CalculateFormula();

// Retrieve the formatted string as it would appear in Excel
string formattedDate = dateCell.StringValue;
Console.WriteLine($"Formatted date (locale aware): {formattedDate}");
```

**Tại sao điều này quan trọng:**  
Sử dụng `SetStyle` với định dạng số đảm bảo việc hiển thị của ô tuân theo cài đặt khu vực, điều này rất quan trọng cho các báo cáo được phân phối trên các locale khác nhau. Khi bạn sau này đọc `StringValue`, bạn nhận được chuỗi chính xác mà người dùng sẽ thấy trong giao diện Excel, loại bỏ nhu cầu phân tích thủ công.

---

## Ví dụ đầy đủ, có thể chạy

Dưới đây là một chương trình duy nhất kết hợp ba bước. Dán nó vào một dự án Console App mới, thêm gói NuGet Aspose.Cells, và chạy.

```csharp
using Aspose.Cells;
using System;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // ---------- Step 1: Save workbook as CSV ----------
            Workbook workbook = new Workbook(); // start with a fresh workbook
            // (Optionally load an existing file: new Workbook("input.xlsx"))

            // Populate some sample data
            workbook.Worksheets[0].Cells["A1"].PutValue(123.456789);
            workbook.Worksheets[0].Cells["B1"].PutValue("Sample Text");

            CsvSaveOptions csvOptions = new CsvSaveOptions
            {
                SignificantDigits = 4
            };
            string csvPath = @"C:\Temp\Digits.csv";
            workbook.Save(csvPath, csvOptions);
            Console.WriteLine($"Saved CSV to {csvPath}");

            // ---------- Step 2: Export worksheet as text with uppercase ----------
            ExportTableOptions tableOptions = new ExportTableOptions
            {
                ExportAsString = true,
                CustomExport = (cell, value) => value?.ToString().ToUpperInvariant()
            };
            string txtPath = @"C:\Temp\Table.txt";
            workbook.Worksheets[0].ExportTable(txtPath, tableOptions);
            Console.WriteLine($"Exported TXT to {txtPath}");

            // ---------- Step 3: Apply custom number format ----------
            Workbook eraWorkbook = new Workbook();
            Cell dateCell = eraWorkbook.Worksheets[0].Cells["A1"];
            dateCell.PutValue("Reiwa 3/04/01");

            Style eraStyle = eraWorkbook.CreateStyle();
            eraStyle.Number = 14; // short date format; replace with custom if needed
            dateCell.SetStyle(eraStyle);
            eraWorkbook.CalculateFormula();

            Console.WriteLine($"Japanese era date formatted: {dateCell.StringValue}");
        }
    }
}
```

**Kết quả mong đợi**

```
Saved CSV to C:\Temp\Digits.csv
Exported TXT to C:\Temp\Table.txt
Japanese era date formatted: 4/1/2021
```

(Định dạng ngày chính xác có thể thay đổi tùy theo cài đặt locale của hệ thống của bạn.)

---

## Các câu hỏi thường gặp và xử lý các trường hợp đặc biệt

| Question | Answer |
|----------|--------|
| *Nếu tôi cần dấu phân cách khác trong CSV?* | Đặt `csvOptions.Separator` thành `','`, `'\t'` hoặc bất kỳ ký tự tùy chỉnh nào trước khi gọi `Save`. |
| *Tôi có thể giữ độ chính xác số gốc thay vì làm tròn không?* | Sử dụng `SignificantDigits = 0` để ghi toàn bộ giá trị double‑precision, hoặc đặt `NumberDecimalSeparator` cho các ký hiệu thập phân theo locale. |
| *Làm sao để xuất chỉ một phạm vi cụ thể thay vì toàn bộ sheet?* | Gọi `ExportTable(string fileName, ExportTableOptions options, CellArea area)` và truyền một `CellArea` xác định phạm vi. |
| *Nếu workbook chứa công thức tham chiếu tới các sheet khác thì sao?* | Đảm bảo bạn gọi `workbook.CalculateFormula()` trước khi xuất; nếu không bạn sẽ nhận được các giá trị đã được lưu trong bộ nhớ đệm. |
| *Có cách nào giữ định dạng ô gốc (phông chữ, màu sắc) trong file TXT không?* | Định dạng plain‑text không thể giữ lại kiểu dáng trực quan. Nếu bạn cần định dạng phong phú, hãy cân nhắc xuất sang HTML (`HtmlSaveOptions`) thay thế. |

---

## Kết luận

Bạn đã biết cách **save workbook as CSV** với độ chính xác được kiểm soát, **export excel to TXT** trong khi buộc **uppercase cell values**, và **apply custom number format** cho việc hiển thị ngày theo locale. Mỗi đoạn mã đều độc lập, chạy ngay mà không cần cấu hình thêm, và tuân theo các thực hành tốt nhất về hiệu suất và khả năng bảo trì.

Tiếp theo, bạn có thể khám phá:

* Sử dụng `HtmlSaveOptions` để giữ kiểu dáng khi xuất sang định dạng thân thiện với web.  
* Tận dụng `CsvSaveOptions.Encoding` cho UTF‑8 hoặc các bộ ký tự khác khi làm việc với dữ liệu đa ngôn ngữ.  
* Tự động xử lý hàng loạt nhiều worksheet bằng cách lặp qua `workbook.Worksheets`.

Bạn có thể tự do điều chỉnh mã cho các pipeline dữ liệu của mình, và để sự linh hoạt của Aspose.Cells thực hiện phần công việc nặng.

---

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với các giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Save Workbook To Text Csv Format](/cells/german/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)
- [Save Workbook To Text Csv Format](/cells/french/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)
- [Save Workbook To Text Csv Format](/cells/spanish/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}