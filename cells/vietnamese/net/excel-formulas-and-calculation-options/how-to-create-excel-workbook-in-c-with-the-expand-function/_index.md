---
category: general
date: 2026-10-04
description: Học cách tạo workbook Excel trong C# và sử dụng EXPAND, buộc tính toán
  công thức, và lưu workbook dưới dạng XLSX trong khi điền một cột bằng các số.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- how to use expand
- force formula calculation
- save workbook as xlsx
- populate column with numbers
language: vi
lastmod: 2026-10-04
og_description: Tạo workbook Excel trong C# bằng Aspose.Cells. Hướng dẫn này cho thấy
  cách sử dụng EXPAND, buộc tính toán công thức và lưu workbook dưới dạng XLSX trong
  khi điền một cột bằng các số.
og_image_alt: Screenshot of a C# program that creates an Excel workbook and applies
  the EXPAND function
og_title: Tạo workbook Excel trong C# – hướng dẫn đầy đủ với EXPAND và lưu dưới dạng
  XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to create Excel workbook in C# and use EXPAND, force formula
    calculation, and save workbook as XLSX while populating a column with numbers.
  headline: How to create Excel workbook in C# with the EXPAND function
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Automation
title: Cách tạo sổ làm việc Excel trong C# với hàm EXPAND
url: /vi/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-in-c-with-the-expand-function/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách tạo workbook Excel trong C# với hàm EXPAND

Nếu bạn cần **tạo workbook Excel** một cách lập trình, hướng dẫn này sẽ cho bạn một giải pháp hoàn chỉnh, sẵn sàng chạy. Bạn sẽ thấy cách **điền cột bằng các số**, áp dụng hàm **EXPAND** để lan truyền dữ liệu theo chiều ngang, **buộc tính toán công thức**, và cuối cùng **lưu workbook dưới dạng XLSX**.  

Bài hướng dẫn này bao gồm mọi bước bạn cần, từ khởi tạo workbook đến kiểm tra kết quả. Không cần tài liệu bên ngoài—chỉ cần sao chép mã, chạy nó, và bạn sẽ có một tệp Excel hoạt động đầy đủ.

## Yêu cầu trước

- .NET 6.0 trở lên (mã cũng hoạt động với .NET Framework 4.6+)
- Gói NuGet Aspose.Cells cho .NET (`Install-Package Aspose.Cells`)
- Kiến thức cơ bản về cú pháp C#
- Một IDE như Visual Studio hoặc VS Code

## Bước 1: Tạo workbook Excel và truy cập worksheet đầu tiên

Hành động đầu tiên là **tạo workbook Excel** và lấy tham chiếu tới worksheet mặc định của nó. Aspose.Cells tự động thêm một worksheet ở chỉ mục 0, vì vậy bạn có thể làm việc với nó ngay lập tức.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();          // create Excel workbook
        Worksheet sheet = workbook.Worksheets[0];   // first (default) worksheet
```

*Tại sao điều này quan trọng:* Khi khởi tạo `Workbook` sẽ cấp phát cấu trúc tệp nội bộ, và việc lấy `Worksheets[0]` sẽ cung cấp cho bạn một đối tượng `Worksheet` cụ thể để thao tác với các hàng, cột và ô.

## Bước 2: Điền cột bằng các số

Tiếp theo, điền một danh sách dọc trong cột A. Điều này minh họa **điền cột bằng các số** và cung cấp phạm vi nguồn cho hàm EXPAND.

```csharp
        // Step 2: Fill a vertical list of values in column A
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);
```

*Mẹo chuyên nghiệp:* Sử dụng `PutValue` cho các số nguyên, chuỗi, ngày tháng, hoặc bất kỳ kiểu dữ liệu .NET nào. Phương thức sẽ tự động xác định kiểu ô.

## Bước 3: Cách sử dụng EXPAND – lan truyền danh sách theo chiều ngang

Phần **cách sử dụng expand** là trọng tâm của bài hướng dẫn này. Hàm `EXPAND` mở rộng một phạm vi nguồn thành một hình dạng mới. Ở đây chúng ta mở rộng phạm vi dọc `A1:A3` thành một hàng duy nhất kéo dài ba cột, bắt đầu tại `B1`.

```csharp
        // Step 3: Apply the EXPAND function to spill the list horizontally starting at B1
        // The formula expands the range A1:A3 into 1 row and 3 columns (B1:D1)
        sheet.Cells["B1"].Formula = "=EXPAND(A1:A3, 1, 3)";
```

*Giải thích:*  
- Đối số đầu tiên (`A1:A3`) là phạm vi nguồn.  
- Đối số thứ hai (`1`) buộc kết quả có **1** hàng.  
- Đối số thứ ba (`3`) buộc kết quả có **3** cột.  

Khi workbook được tính lại, các ô `B1`, `C1` và `D1` sẽ chứa `1`, `2` và `3` tương ứng.

## Bước 4: Buộc tính toán công thức

Aspose.Cells không tự động đánh giá công thức sau khi bạn đặt chúng, vì vậy bạn phải **buộc tính toán công thức** trước khi lưu. Điều này đảm bảo kết quả EXPAND được ghi vào tệp.

```csharp
        // Step 4: Force calculation of all formulas in the workbook
        workbook.CalculateFormula();   // triggers calculation engine
```

*Tại sao bạn cần điều này:* Nếu không gọi `CalculateFormula`, tệp đã lưu sẽ chứa chuỗi công thức thô, và Excel sẽ chỉ tính lại khi tệp được mở. Đối với các quy trình tự động, bạn thường muốn các giá trị được ghi ngay lập tức.

## Bước 5: Lưu workbook dưới dạng XLSX

Bây giờ workbook đã được chuẩn bị đầy đủ, **lưu workbook dưới dạng XLSX** tới vị trí bạn chọn. Phần mở rộng tệp xác định định dạng đầu ra; `.xlsx` tạo một workbook Office Open XML.

```csharp
        // Step 5: Save the workbook to a file
        string outputPath = @"C:\Temp\ExpandFunction.xlsx";
        workbook.Save(outputPath);   // save workbook as XLSX
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

*Mẹo:* Nếu bạn cần định dạng khác (CSV, PDF, v.v.), chỉ cần thay đổi phần mở rộng tệp hoặc sử dụng `workbook.Save(outputPath, SaveFormat.Xls)` cho các phiên bản Excel cũ hơn.

## Ví dụ đầy đủ, có thể chạy

Kết hợp tất cả các phần lại với nhau sẽ cho bạn một chương trình tự chứa, **tạo workbook Excel**, điền một cột, sử dụng **EXPAND**, buộc tính toán, và **lưu workbook dưới dạng XLSX**.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1. Create Excel workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2. Populate column with numbers
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // 3. How to use EXPAND – spill horizontally
        sheet.Cells["B1"].Formula = "=EXPAND(A1:A3, 1, 3)";

        // 4. Force formula calculation
        workbook.CalculateFormula();

        // 5. Save workbook as XLSX
        string path = @"C:\Temp\ExpandFunction.xlsx";
        workbook.Save(path);
        System.Console.WriteLine($"Workbook saved to {path}");
    }
}
```

### Kết quả mong đợi

Sau khi chạy chương trình, mở `ExpandFunction.xlsx` trong Excel. Bạn sẽ thấy:

| A | B | C | D |
|---|---|---|---|
| 1 | 1 | 2 | 3 |
| 2 |   |   |   |
| 3 |   |   |   |

Các giá trị `1`, `2`, `3` trong các ô `B1:D1` xác nhận rằng hàm **EXPAND** đã hoạt động và bước **buộc tính toán công thức** đã ghi thành công các kết quả.

## Các biến thể phổ biến và trường hợp đặc biệt

| Kịch bản | Điều chỉnh |
|----------|------------|
| **Phạm vi nguồn động** | Sử dụng `=EXPAND(A1:INDEX(A:A, COUNTA(A:A)), 1, 0)` để mở rộng số hàng đã được điền. |
| **Kích thước đầu ra khác nhau** | Thay đổi đối số thứ hai và thứ ba của `EXPAND` để kiểm soát số hàng và cột. |
| **Nhiều worksheet** | Lặp qua `workbook.Worksheets` và áp dụng cùng logic cho mỗi sheet. |
| **Bộ dữ liệu lớn** | Gọi `workbook.CalculateFormula()` một lần sau khi đã đặt tất cả công thức để tránh tính lại lặp lại. |
| **Lưu vào memory stream** | Thay thế `workbook.Save(path)` bằng `workbook.Save(stream, SaveFormat.Xlsx)` khi bạn cần tệp trong phản hồi API web. |

## Danh sách kiểm tra khắc phục sự cố

- **Công thức không mở rộng:** Kiểm tra rằng `CalculateFormula()` được gọi *sau* khi đặt công thức.  
- **Không tìm thấy tệp khi lưu:** Đảm bảo thư mục đích tồn tại và tiến trình có quyền ghi.  
- **Kiểu dữ liệu không đúng:** Sử dụng `PutValue` cho số; đối với ngày tháng, dùng `PutValue(DateTime.Now)` hoặc `PutDateTime`.  
- **Không khớp phiên bản:** Hàm EXPAND yêu cầu engine tính toán tương thích Excel 365; Aspose.Cells 23.9+ hỗ trợ.

## Kết luận

Bây giờ bạn đã biết cách **tạo workbook Excel** trong C#, **điền cột bằng các số**, áp dụng hàm **EXPAND**, **buộc tính toán công thức**, và **lưu workbook dưới dạng XLSX**. Ví dụ toàn diện này có thể được điều chỉnh cho báo cáo, chuyển đổi dữ liệu, hoặc bất kỳ kịch bản tự động nào cần đầu ra Excel động.

### Các bước tiếp theo

- Khám phá các hàm mảng động khác như `FILTER`, `SORT`, và `UNIQUE`.  
- Tích hợp việc tạo workbook vào một API ASP.NET Core để cung cấp tệp Excel theo yêu cầu.  
- Thay thế các số được mã hoá cứng bằng dữ liệu đọc từ cơ sở dữ liệu hoặc tệp CSV cho báo cáo thực tế.

Bạn có thể tự do thử nghiệm với các phạm vi, tên sheet và định dạng đầu ra khác nhau. Chúc lập trình vui vẻ!

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên đều có các ví dụ mã hoàn chỉnh, hoạt động với các giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách tính Cotangent trong Excel với C# – Tạo Workbook, Sử dụng EXPAND,](/cells/english/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/)
- [Cách sử dụng WRAPCOLS trong C# – Tạo Workbook Excel với các hàm Wrap](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Cách tạo và lưu Workbook Excel dưới dạng ODS bằng Aspose.Cells cho .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}