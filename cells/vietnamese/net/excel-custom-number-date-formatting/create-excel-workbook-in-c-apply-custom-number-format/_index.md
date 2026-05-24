---
category: general
date: 2026-05-23
description: Tạo workbook Excel trong C# và học cách áp dụng định dạng số tùy chỉnh,
  thiết lập kiểu ô bằng mã, định dạng ô ở dạng khoa học, sau đó lưu workbook dưới
  dạng xlsx.
draft: false
keywords:
- create excel workbook
- apply custom number format
- format cell scientific notation
- set cell style programmatically
- save workbook to xlsx
language: vi
og_description: Tạo workbook Excel trong C# nhanh chóng. Học cách áp dụng định dạng
  số tùy chỉnh, tạo kiểu cho các ô bằng mã, định dạng ký hiệu khoa học và lưu dưới
  dạng xlsx.
og_title: Tạo Workbook Excel trong C# – Áp dụng Định dạng Số tùy chỉnh
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create excel workbook in C# and learn how to apply custom number format,
    set cell style programmatically, format cell scientific notation, then save workbook
    to xlsx.
  headline: Create Excel Workbook in C# – Apply Custom Number Format
  type: TechArticle
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Tạo Workbook Excel trong C# – Áp dụng Định dạng Số Tùy chỉnh
url: /vi/net/excel-custom-number-date-formatting/create-excel-workbook-in-c-apply-custom-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Workbook Excel trong C# – Áp Dụng Định Dạng Số Tùy Chỉnh

Tạo workbook Excel trong C# dễ hơn bạn nghĩ. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn cách áp dụng định dạng số tùy chỉnh, định dạng một ô ở dạng khoa học, thiết lập kiểu ô bằng mã, và cuối cùng lưu workbook thành file xlsx.

Nếu bạn từng nhìn vào một bảng tính trống và tự hỏi làm sao tự động hoá toàn bộ quá trình — từ việc đưa dữ liệu vào tới việc hiển thị số chính xác như mong muốn — thì tutorial này dành cho bạn. Khi hoàn thành, bạn sẽ có một file Excel hoạt động đầy đủ mà có thể mở bằng bất kỳ chương trình bảng tính nào, và bạn sẽ hiểu **tại sao** mỗi bước quan trọng, không chỉ **cách** viết mã.

## Những Điều Cần Chuẩn Bị

- **.NET 6+** (hoặc bất kỳ .NET Framework hiện đại nào hỗ trợ thư viện)  
- **Aspose.Cells for .NET** (hoặc API khác cung cấp các lớp `Workbook`, `Cell`, và `CellFormat`)  
- Một chút kinh nghiệm với C# – nếu bạn có thể viết `Console.WriteLine`, bạn đã sẵn sàng.  

Không cần file cấu hình bổ sung, không cần COM interop, và chắc chắn không cần cài đặt Excel thủ công.

---

## Tạo Excel Workbook – Khởi Tạo Đối Tượng Workbook

Điều đầu tiên chúng ta phải làm là tạo một workbook trống. Hãy nghĩ lớp `Workbook` như một canvas trắng mà bạn sẽ vẽ các hàng, cột và kiểu dáng lên.

```csharp
using Aspose.Cells;   // Make sure the Aspose.Cells namespace is referenced

// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

Chỉ vậy—một dòng và bạn đã có một file Excel mới trong bộ nhớ. Hàm khởi tạo `Workbook` tạo ra bộ sưu tập worksheet mặc định, vì vậy bạn có thể bắt đầu thêm dữ liệu ngay lập tức.

> **Mẹo chuyên nghiệp:** Nếu bạn cần nhiều sheet, có thể gọi `workbook.Worksheets.Add()` trước khi bắt đầu điền ô.

![ví dụ tạo workbook excel](image-placeholder.png "ảnh chụp màn hình tạo workbook excel")

*Văn bản thay thế ảnh: ví dụ tạo workbook excel hiển thị một sheet Excel trống trong IDE.*

## Áp Dụng Định Dạng Số Tùy Chỉnh cho Ô

Bây giờ workbook đã tồn tại, hãy đưa một số vào ô **A1** và gán cho nó định dạng tùy chỉnh. Định dạng số tùy chỉnh cho phép bạn kiểm soát cách hiển thị số — tiền tệ, phần trăm, ngày tháng, hoặc trong trường hợp này, dạng khoa học.

```csharp
// Step 2: Grab the first worksheet and the cell at A1 (row 0, column 0)
Worksheet sheet = workbook.Worksheets[0];
Cell cell = sheet.Cells[0, 0];

// Step 3: Insert a numeric value
cell.PutValue(12345.6789);

// Step 4: Retrieve the current style so we can modify its Number format
Style style = cell.GetStyle();

// Step 5: Define a custom scientific notation format with two decimal places
style.Custom = "0.00E+00";   // This is the “apply custom number format” part

// Step 6: Push the modified style back onto the cell
cell.SetStyle(style);
```

Tại sao phải lấy style trước? Bởi vì đối tượng `Cell` lưu trữ một đối tượng **Style** chứa phông chữ, viền, căn chỉnh và định dạng số, tất cả trong một chỗ. Khi chỉnh sửa thuộc tính `Custom` chúng ta nói với Excel, “hiển thị giá trị này dưới dạng khoa học với hai chữ số thập phân.”

> **Câu hỏi thường gặp:** *Tôi có thể dùng định dạng có sẵn thay vì tự tạo không?*  
> Có — đặt `style.Number = 10` để sử dụng định dạng khoa học có sẵn, nhưng chuỗi tùy chỉnh cho phép bạn kiểm soát chính xác số chữ số thập phân.

## Thiết Lập Kiểu Ô Bằng Mã (Ngoài Định Dạng Số)

Thường bạn sẽ muốn nhiều hơn chỉ định dạng số. Hãy thêm phông chữ đậm và nền xám nhạt để ô nổi bật hơn.

```csharp
// Optional: Enhance the cell appearance
style.Font.IsBold = true;
style.ForegroundColor = System.Drawing.Color.LightGray;
style.Pattern = BackgroundType.Solid;

// Re‑apply the enriched style
cell.SetStyle(style);
```

Chú ý chúng ta tái sử dụng cùng một đối tượng `style` đã chỉnh sửa trước đó. Đó là ưu điểm của **set cell style programmatically** — bạn chỉ lấy style một lần, sửa các thuộc tính cần thiết, và ghi lại. Không cần tạo lại đối tượng hay mất định dạng số đã thiết lập.

## Định Dạng Ô Dạng Khoa Học (Xử Lý Trường Hợp Cạnh)

Nếu bạn làm việc với các số rất lớn hoặc rất nhỏ, dạng khoa học là cứu cánh. Định dạng tùy chỉnh chúng ta dùng (`0.00E+00`) đảm bảo có hai chữ số sau dấu thập phân và luôn có dấu cộng cho số mũ. Dưới đây là một kiểm tra nhanh:

```csharp
// Verify the format by inserting another extreme value
Cell extraCell = sheet.Cells[1, 0]; // B2
extraCell.PutValue(0.00001234);
extraCell.SetStyle(style); // Reuse the same style with scientific notation
```

Khi mở file kết quả, ô B2 sẽ hiển thị `1.23E-05`, xác nhận **format cell scientific notation** hoạt động cho cả số lớn và nhỏ.

## Lưu Workbook thành XLSX

Mọi công việc thú vị sẽ dừng lại khi bạn thực sự ghi file ra đĩa. Phương thức `Save` thực hiện công việc nặng, chuyển đổi biểu diễn trong bộ nhớ thành một gói `.xlsx` hợp lệ.

```csharp
// Step 7: Persist the workbook
string outputPath = @"C:\Temp\CustomFormatted.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
```

Dòng này hoàn thành mục tiêu **save workbook to xlsx**. Nếu thư mục không tồn tại, `Save` sẽ ném ngoại lệ — vì vậy hãy chắc chắn thư mục đã được tạo trước hoặc bao bọc lời gọi trong khối try/catch.

```csharp
try
{
    workbook.Save(outputPath, SaveFormat.Xlsx);
    Console.WriteLine($"Workbook saved successfully to {outputPath}");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
}
```

Bây giờ bạn đã có một file Excel sẵn sàng chia sẻ với số khoa học được định dạng đẹp, kiểu chữ đậm, và nền xám nhạt.

## Ví Dụ Hoàn Chỉnh

Dưới đây là chương trình đầy đủ, sẵn sàng copy‑paste, kết nối mọi phần lại với nhau. Nó biên dịch như một console app, nhưng bạn có thể đưa logic này vào bất kỳ dự án C# nào.

```csharp
using System;
using Aspose.Cells;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Access the first worksheet and target cell A1
        Worksheet sheet = workbook.Worksheets[0];
        Cell cell = sheet.Cells[0, 0];

        // 3️⃣ Insert a numeric value
        cell.PutValue(12345.6789);

        // 4️⃣ Retrieve and customize the cell style
        Style style = cell.GetStyle();
        style.Custom = "0.00E+00";               // apply custom number format (scientific)
        style.Font.IsBold = true;               // set cell style programmatically
        style.ForegroundColor = Color.LightGray;
        style.Pattern = BackgroundType.Solid;

        // 5️⃣ Apply the style back to the cell
        cell.SetStyle(style);

        // 6️⃣ Add another example to prove scientific notation works for tiny numbers
        Cell tinyCell = sheet.Cells[1, 0]; // B2
        tinyCell.PutValue(0.00001234);
        tinyCell.SetStyle(style);

        // 7️⃣ Save the workbook to an XLSX file
        string outputPath = @"C:\Temp\CustomFormatted.xlsx";
        try
        {
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved successfully to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
        }
    }
}
```

**Kết quả mong đợi:** Mở `CustomFormatted.xlsx` và bạn sẽ thấy:

| A1               | B2            |
|------------------|---------------|
| 1.23E+04         | 1.23E-05      |

Cả hai ô đều in đậm, có nền xám nhạt, và hiển thị số ở dạng khoa học với hai chữ số thập phân.

---

## Tổng Kết

Chúng ta vừa **create excel workbook** từ đầu, **apply custom number format**, **format cell scientific notation**, **set cell style programmatically**, và **save workbook to xlsx** — tất cả chỉ trong vài dòng C#. Cách tiếp cận này có thể mở rộng: chỉ cần lặp qua các hàng, sao chép đối tượng `style`, và bạn sẽ có một báo cáo đầy đủ kiểu trong vài giây.

### Tiếp Theo?

- **Định dạng động:** Thay đổi định dạng dựa trên độ lớn của giá trị (ví dụ: tiền tệ vs. phần trăm).  
- **Nhiều sheet:** Dùng `workbook.Worksheets.Add("Summary")` để xây dựng dashboard.  
- **Styling nâng cao:** Viền, định dạng có điều kiện, và xác thực dữ liệu


## Các Tutorial Liên Quan

- [Cách Tạo và Lưu Workbook Excel dưới dạng ODS bằng Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Tạo và Lưu Workbook Excel Aspose Cells Dotnet](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)
- [Tạo và Lưu Workbook Excel PDF Aspnet Aspose Cells](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}