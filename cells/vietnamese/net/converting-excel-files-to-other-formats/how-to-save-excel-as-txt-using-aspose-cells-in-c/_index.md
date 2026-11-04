---
category: general
date: 2026-10-13
description: Tìm hiểu cách lưu Excel dưới dạng TXT với Aspose.Cells. Hướng dẫn này
  bao gồm xuất Excel sang TXT, ghi giá trị vào ô và đặt số chữ số có ý nghĩa chỉ trong
  vài bước.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as txt
- export excel to txt
- write value to cell
- set significant digits
- export spreadsheet as txt
language: vi
lastmod: 2026-10-13
og_description: Lưu Excel dưới dạng TXT với Aspose.Cells. Tìm hiểu cách xuất Excel
  sang TXT, ghi giá trị vào ô và đặt số chữ số có ý nghĩa chỉ trong vài dòng mã C#.
og_image_alt: Screenshot showing a workbook saved as a TXT file using save excel as
  txt
og_title: Lưu Excel thành TXT – hướng dẫn chi tiết từng bước cho các nhà phát triển
  .NET
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to save Excel as TXT with Aspose.Cells. This guide covers
    export Excel to TXT, write value to cell, and set significant digits in just a
    few steps.
  headline: How to save Excel as TXT using Aspose.Cells in C#
  type: TechArticle
- questions:
  - answer: It rounds to the nearest value based on the specified number of significant
      digits, ensuring the output is mathematically accurate to that precision.
    question: Does `SignificantDigits` round or truncate?
  - answer: 'Yes. Replace the file path with a `MemoryStream` instance: `workbook.Save(stream,
      txtOptions);`. This is handy for web APIs that need to return the TXT content
      without touching the file system.'
    question: Can I export directly to a memory stream?
  - answer: 'Use `txtOptions.ExportFormattedValues = true`. This forces Aspose.Cells
      to write the cell’s displayed text rather than the raw value. ## Conclusion
      You now know how to **save Excel as TXT** with full control over precision,
      formatting, and output location. By following the four steps—create a workbo'
    question: What if I need to keep the original formatting (e.g., dates)?
  type: FAQPage
tags:
- Excel
- TXT
- Aspose.Cells
- .NET
title: Cách lưu Excel thành TXT bằng Aspose.Cells trong C#
url: /vi/net/converting-excel-files-to-other-formats/how-to-save-excel-as-txt-using-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách lưu Excel dưới dạng TXT bằng Aspose.Cells trong C#

Nếu bạn cần **lưu Excel dưới dạng TXT** nhanh chóng, hướng dẫn này sẽ trình bày quy trình đầy đủ trong chưa đầy năm phút. Bạn sẽ thấy cách xuất Excel sang TXT, ghi giá trị vào ô, và đặt số chữ số có ý nghĩa để tệp văn bản chứa chính xác dữ liệu bạn mong muốn.

Xuất một bảng tính dưới dạng TXT hữu ích khi các hệ thống hạ nguồn chỉ chấp nhận đầu vào dạng văn bản thuần, khi bạn cần tạo nhật ký, hoặc khi muốn có bản dump tính toán có thể đọc được bởi con người. Ví dụ dưới đây hoạt động với Aspose.Cells v25.10 trở lên và chạy trên bất kỳ môi trường .NET 6+ nào.

## Các yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* Bản sao có giấy phép của **Aspose.Cells for .NET** (bản dùng thử miễn phí đủ cho việc thử nghiệm).
* .NET 6 SDK hoặc phiên bản mới hơn đã được cài đặt.
* Một IDE như Visual Studio 2022, VS Code, hoặc Rider.
* Kiến thức cơ bản về C# — không cần kinh nghiệm tự động hoá Excel nâng cao.

Bạn có thể cài đặt gói NuGet Aspose.Cells bằng:

```bash
dotnet add package Aspose.Cells
```

## Bước 1: Tạo workbook và truy cập worksheet đầu tiên (save excel as txt)

Điều đầu tiên bạn làm khi muốn **lưu Excel dưới dạng TXT** là tạo một đối tượng `Workbook`. Đối tượng này đại diện cho toàn bộ tệp Excel trong bộ nhớ.

```csharp
using Aspose.Cells;

// Create a new workbook (an empty Excel file)
Workbook workbook = new Workbook();

// Access the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

> **Tại sao điều này quan trọng:** Lớp `Workbook` là điểm khởi đầu cho mọi thao tác trên bảng tính. Bắt đầu với một workbook mới giúp bạn tránh các định dạng ẩn có thể ảnh hưởng đến đầu ra dạng văn bản thuần.

## Bước 2: Ghi một số có độ chính xác cao vào ô (write value to cell)

Bây giờ bạn cần **ghi giá trị vào ô** A1. Phương thức `PutValue` tự động phát hiện kiểu dữ liệu và lưu dưới dạng số.

```csharp
// Write a high‑precision number into cell A1
worksheet.Cells["A1"].PutValue(12345.6789012345);
```

> **Mẹo:** Nếu sau này bạn cần ghi chuỗi, ngày tháng hoặc công thức, cùng một phương thức `PutValue` vẫn hoạt động — chỉ cần truyền kiểu .NET phù hợp.

## Bước 3: Cấu hình tùy chọn xuất để giữ lại độ chính xác cần thiết (set significant digits)

Khi xuất ra tệp TXT, bạn thường muốn giới hạn số chữ số để giảm kích thước tệp hoặc đáp ứng yêu cầu của hệ thống hạ nguồn. Lớp `TxtSaveOptions` cung cấp thuộc tính `SignificantDigits` cho mục đích này.

```csharp
// Configure TXT save options to retain only 6 significant digits
TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
{
    SignificantDigits = 6   // New option in v25.10
};
```

> **Tại sao nên đặt số chữ số có ý nghĩa:** Nếu không thiết lập, Aspose.Cells sẽ ghi toàn bộ giá trị double‑precision, có thể tạo ra các chuỗi dài như `12345.6789012345`. Đặt `SignificantDigits = 6` sẽ cắt ngắn đầu ra thành `12345.7`, phù hợp với hầu hết các yêu cầu báo cáo.

## Bước 4: Xuất workbook dưới dạng tệp TXT (export excel to txt)

Cuối cùng, bạn **xuất Excel sang TXT** bằng cách gọi `Workbook.Save` với các tùy chọn đã cấu hình trước.

```csharp
// Save the workbook as a TXT file using the configured options
string outputPath = @"C:\Temp\LimitedDigits.txt";
workbook.Save(outputPath, txtSaveOptions);
```

Khi mã hoàn thành, `LimitedDigits.txt` sẽ chứa:

```
12345.7
```

> **Xác minh kết quả:** Mở tệp trong bất kỳ trình soạn thảo văn bản nào (Notepad, VS Code) để xác nhận rằng chỉ có sáu chữ số có ý nghĩa và không có dấu phẩy hoặc ký tự tab thừa.

## Ví dụ đầy đủ, có thể chạy ngay

Dưới đây là một ứng dụng console tự chứa mà bạn có thể sao chép, dán và chạy ngay lập tức.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Write a high‑precision number to cell A1
            worksheet.Cells["A1"].PutValue(12345.6789012345);

            // 3️⃣ Set up TXT save options with 6 significant digits
            TxtSaveOptions txtOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                SignificantDigits = 6
            };

            // 4️⃣ Save as TXT
            string path = @"C:\Temp\LimitedDigits.txt";
            workbook.Save(path, txtOptions);

            Console.WriteLine($"Workbook exported to TXT at: {path}");
        }
    }
}
```

**Giải thích từng khối**

| Khối | Mục đích |
|-------|---------|
| `using Aspose.Cells;` | Nhập không gian tên Aspose.Cells cần thiết cho `Workbook`, `Worksheet`, và `TxtSaveOptions`. |
| `Workbook workbook = new Workbook();` | Khởi tạo một workbook Excel rỗng trong bộ nhớ. |
| `worksheet.Cells["A1"].PutValue(...);` | **write value to cell** A1 với một số double‑precision. |
| `TxtSaveOptions` | Cấu hình hành vi **set significant digits** cho việc xuất TXT. |
| `workbook.Save(..., txtOptions);` | Thực hiện thao tác **export excel to txt**, tạo tệp văn bản thuần. |

## Các trường hợp đặc biệt và mẹo bổ sung

| Tình huống | Cách xử lý |
|----------|---------------|
| **Worksheet lớn** (nhiều hàng/cột) | Sử dụng `txtOptions.Encoding = Encoding.UTF8` nếu cần hỗ trợ Unicode, và cân nhắc stream tệp bằng `Workbook.Save(Stream, txtOptions)` để tránh tiêu thụ bộ nhớ cao. |
| **Dấu phân cách tùy chỉnh** (giá trị phân tách bằng dấu phẩy) | `TxtSaveOptions` cũng cung cấp `Separator` — đặt thành `','` để tạo đầu ra kiểu CSV trong khi vẫn dùng định dạng TXT. |
| **Bảo toàn công thức** | Đặt `txtOptions.ExportFormulas = true` để ghi văn bản công thức thay vì giá trị đã tính. |
| **Dấu thập phân theo địa phương** | Điều chỉnh `txtOptions.DecimalSeparator` thành `','` cho các khu vực châu Âu. |
| **Nhiều worksheet** | Duyệt `workbook.Worksheets` và gọi `Save` cho mỗi worksheet, thêm tên worksheet vào tên tệp. |

## Các câu hỏi thường gặp

**Hỏi: `SignificantDigits` làm tròn hay cắt ngắn?**  
Đáp: Nó làm tròn tới giá trị gần nhất dựa trên số chữ số có ý nghĩa đã chỉ định, đảm bảo đầu ra chính xác về mặt toán học ở mức độ đó.

**Hỏi: Tôi có thể xuất trực tiếp tới một memory stream không?**  
Đáp: Có. Thay thế đường dẫn tệp bằng một thể hiện `MemoryStream`: `workbook.Save(stream, txtOptions);`. Điều này hữu ích cho các API web cần trả về nội dung TXT mà không ghi vào hệ thống tệp.

**Hỏi: Nếu tôi muốn giữ nguyên định dạng gốc (ví dụ: ngày tháng) thì sao?**  
Đáp: Sử dụng `txtOptions.ExportFormattedValues = true`. Điều này buộc Aspose.Cells ghi lại văn bản hiển thị của ô thay vì giá trị thô.

## Kết luận

Bây giờ bạn đã biết cách **lưu Excel dưới dạng TXT** với kiểm soát đầy đủ về độ chính xác, định dạng và vị trí xuất. Bằng cách thực hiện bốn bước — tạo workbook, **write value to cell**, **set significant digits**, và **export Excel to TXT** — bạn có thể tích hợp xuất văn bản thuần vào bất kỳ ứng dụng .NET nào.

Tiếp theo, hãy khám phá các chủ đề liên quan như **xuất bảng tính dưới dạng TXT với dấu phân cách tùy chỉnh**, **chuyển đổi Excel sang CSV**, hoặc **sử dụng Aspose.Cells để tạo báo cáo JSON**. Mỗi chủ đề đều dựa trên các khái niệm cốt lõi đã được trình bày ở đây, cung cấp cho bạn một bộ công cụ linh hoạt cho việc trao đổi dữ liệu giữa các nền tảng.

Chúc bạn lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được minh họa trong bài viết này. Mỗi tài nguyên bao gồm mã mẫu đầy đủ và giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Lưu Excel dưới dạng Văn bản – Hướng dẫn C# đầy đủ để xuất Excel sang TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Tạo Workbook mới và xuất Excel sang TXT với độ chính xác](/cells/english/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/)
- [Tạo workbook mới – Xuất Excel sang TXT với Độ chính xác đầy đủ](/cells/english/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}