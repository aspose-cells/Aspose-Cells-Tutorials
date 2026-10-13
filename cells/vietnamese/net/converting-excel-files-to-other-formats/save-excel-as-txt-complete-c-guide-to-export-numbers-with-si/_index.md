---
category: general
date: 2026-02-21
description: Lưu Excel dưới dạng txt với kiểm soát chính xác số chữ số có nghĩa. Xuất
  Excel sang txt trong C# và dễ dàng thiết lập số chữ số có nghĩa.
draft: false
keywords:
- save excel as txt
- export excel to txt
- set significant digits
- save workbook as text
- export numbers to txt
language: vi
og_description: Lưu Excel dưới dạng txt nhanh chóng. Tìm hiểu cách xuất Excel sang
  txt, thiết lập số chữ số có ý nghĩa và kiểm soát đầu ra văn bản bằng C#.
og_title: Lưu Excel dưới dạng txt – Xuất các số với chữ số có ý nghĩa trong C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Lưu Excel dưới dạng txt – Hướng dẫn C# toàn diện để xuất số với chữ số đáng
  kể
url: /vi/net/converting-excel-files-to-other-formats/save-excel-as-txt-complete-c-guide-to-export-numbers-with-si/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lưu Excel dưới dạng txt – Hướng dẫn C# đầy đủ để xuất số với chữ số có nghĩa

Bạn đã bao giờ cần **save Excel as txt** nhưng lo lắng các số sẽ mất độ chính xác? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi cố gắng **export Excel to txt** và cuối cùng nhận được hoặc quá nhiều chữ số thập phân hoặc một kết quả bị làm tròn lộn xộn.  

Trong tutorial này chúng tôi sẽ chỉ cho bạn cách **export Excel to txt** một cách đơn giản trong khi **setting significant digits** để đầu ra trông chính xác như bạn mong muốn. Khi kết thúc, bạn sẽ có một đoạn mã C# sẵn sàng chạy, lưu workbook dưới dạng text, export numbers to txt, và cho phép bạn kiểm soát hoàn toàn định dạng số.

## Những gì bạn sẽ học

- Cách tạo một workbook mới và ghi dữ liệu số.
- Cách **set significant digits** đúng cách bằng `TxtSaveOptions`.
- Cách **save workbook as text** và kiểm tra kết quả.
- Xử lý các trường hợp đặc biệt (số lớn, giá trị âm, vấn đề locale).
- Mẹo nhanh để tinh chỉnh đầu ra hơn nữa (thay đổi delimiter, encoding).

### Yêu cầu trước

- .NET 6.0 hoặc mới hơn (mã cũng chạy trên .NET Framework 4.6+).
- Gói NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`).
- Hiểu biết cơ bản về cú pháp C# — không cần kiến thức sâu về Excel interop.

> **Pro tip:** Nếu bạn đang dùng Visual Studio, bật *nullable reference types* (`<Nullable>enable</Nullable>`) để phát hiện sớm các lỗi null tiềm ẩn.

---

## Bước 1: Khởi tạo Workbook và Ghi một Số

Đầu tiên, chúng ta cần một đối tượng workbook. Hãy nghĩ nó như là biểu diễn trong bộ nhớ của một file Excel.  

```csharp
using Aspose.Cells;
using System;

// Create a new workbook (starts with one worksheet by default)
var workbook = new Workbook();
var worksheet = workbook.Worksheets[0];

// Write a numeric value into cell A1 (row 0, column 0)
worksheet.Cells[0, 0].PutValue(12345.6789);
```

**Tại sao điều này quan trọng:**  
Tạo workbook bằng code tránh được chi phí của COM interop, và `PutValue` tự động phát hiện kiểu dữ liệu, đảm bảo ô được xử lý như một số — không phải chuỗi.

---

## Bước 2: Cấu hình TxtSaveOptions để Kiểm soát Significant Digits

Lớp `TxtSaveOptions` là nơi phép thuật diễn ra. Bằng cách **set `SignificantDigits`**, bạn chỉ định cho Aspose.Cells số chữ số có nghĩa cần giữ lại khi ghi file.

```csharp
// Configure text save options – keep only 4 significant digits
var txtSaveOptions = new TxtSaveOptions
{
    // 4 significant digits means 12345.6789 becomes 12350
    SignificantDigits = 4,

    // Optional: change delimiter if you need CSV‑style output
    // Delimiter = ',',

    // Optional: force UTF‑8 encoding for broader character support
    // Encoding = System.Text.Encoding.UTF8
};
```

**Tại sao bạn nên thiết lập điều này:**  
Khi bạn **export numbers to txt**, thường cần một biểu diễn ngắn gọn (ví dụ, cho các hệ thống báo cáo chỉ chấp nhận độ chính xác nhất định). Thuộc tính `SignificantDigits` đảm bảo việc làm tròn nhất quán bất kể độ dài ban đầu của số.

---

## Bước 3: Save Workbook dưới dạng Text File

Bây giờ chúng ta ghi workbook ra đĩa bằng các tùy chọn vừa định nghĩa.

```csharp
// Define the output path – adjust to your environment
string outputPath = @"C:\Temp\Numbers.txt";

// Save the workbook as a .txt file with the configured options
workbook.Save(outputPath, txtSaveOptions);

Console.WriteLine($"Workbook saved as txt at: {outputPath}");
```

**Bạn sẽ thấy gì:**  
Mở `Numbers.txt` và bạn sẽ nhận được một dòng duy nhất:

```
12350
```

Số gốc `12345.6789` đã được làm tròn thành **bốn chữ số có nghĩa**, đúng như yêu cầu.

---

## Bước 4: Xác minh Kết quả (Tùy chọn nhưng Được Khuyến khích)

Kiểm thử tự động là thói quen tốt. Dưới đây là một kiểm tra nhanh bạn có thể chạy ngay sau khi lưu:

```csharp
// Read back the file to confirm the content
string fileContent = System.IO.File.ReadAllText(outputPath).Trim();

if (fileContent == "12350")
{
    Console.WriteLine("✅ Export succeeded – significant digits applied correctly.");
}
else
{
    Console.WriteLine($"⚠️ Unexpected output: {fileContent}");
}
```

Chạy khối này sẽ in ra dấu kiểm màu xanh nếu mọi thứ khớp, giúp bạn yên tâm rằng thao tác **save excel as txt** đã hoạt động như mong đợi.

---

## Các Biến thể Thông thường & Trường hợp Cạnh

### Export nhiều ô hoặc phạm vi

Nếu bạn cần **export excel to txt** cho một phạm vi lớn, chỉ cần điền thêm các ô trước khi lưu:

```csharp
worksheet.Cells[0, 1].PutValue(0.000123456);
worksheet.Cells[0, 2].PutValue(-98765.4321);
```

`TxtSaveOptions` giống nhau sẽ áp dụng quy tắc 4 chữ số cho mỗi giá trị, cho ra:

```
12350
0.0001235
-98800
```

### Thay đổi Delimiter

Một số hệ thống phía dưới yêu cầu giá trị cách nhau bằng tab. Điều chỉnh delimiter như sau:

```csharp
txtSaveOptions.Delimiter = '\t'; // Tab character
```

Bây giờ mỗi ô trong một hàng sẽ được ngăn cách bằng một tab.

### Xử lý Decimal Separator theo Locale

Nếu người dùng của bạn dùng dấu phẩy làm dấu thập phân, hãy đặt culture:

```csharp
txtSaveOptions.CultureInfo = new System.Globalization.CultureInfo("fr-FR");
```

Kết quả sẽ tuân theo locale, biến `12350` thành `12 350` (dấu cách làm dấu phân cách hàng nghìn trong tiếng Pháp).

---

## Ví dụ Hoàn chỉnh (Sẵn sàng Copy‑Paste)

```csharp
using Aspose.Cells;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and write numbers
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells[0, 0].PutValue(12345.6789);
        sheet.Cells[0, 1].PutValue(0.000123456);
        sheet.Cells[0, 2].PutValue(-98765.4321);

        // 2️⃣ Configure save options – 4 significant digits
        var txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 4,
            // Delimiter = '\t',               // Uncomment for TSV
            // Encoding = System.Text.Encoding.UTF8,
            // CultureInfo = new System.Globalization.CultureInfo("en-US")
        };

        // 3️⃣ Save to text file
        string path = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "Numbers.txt");
        workbook.Save(path, txtOptions);
        Console.WriteLine($"File saved to {path}");

        // 4️⃣ Verify result (optional)
        string result = File.ReadAllText(path).Trim();
        Console.WriteLine($"File content: {result}");
    }
}
```

**Nội dung `Numbers.txt` mong đợi (delimiter mặc định, 4 chữ số có nghĩa):**

```
12350	0.0001235	-98800
```

Tab (`\t`) xuất hiện vì chúng ta để delimiter ở mặc định (tab) trong ví dụ; bạn có thể đổi thành dấu phẩy nếu muốn CSV.

---

## Kết luận

Bây giờ bạn đã biết **cách save Excel as txt** đồng thời kiểm soát số chữ số có nghĩa. Các bước — tạo workbook, thiết lập `TxtSaveOptions.SignificantDigits`, và lưu — là tất cả những gì bạn cần để **export excel to txt** một cách đáng tin cậy.  

Từ đây bạn có thể:

- **Export numbers to txt** cho các bộ dữ liệu lớn hơn.
- Tinh chỉnh delimiter, encoding, hoặc cài đặt culture để phù hợp với bất kỳ hệ thống phía dưới nào.
- Kết hợp cách này với các tính năng khác của Aspose.Cells (styles, formulas) trước khi export.

Hãy thử, thay đổi `SignificantDigits` thành 2 hoặc 6, và xem đầu ra thay đổi như thế nào. Khả năng **save workbook as text** khiến nó trở thành công cụ hữu ích trong bất kỳ pipeline trao đổi dữ liệu nào.

---

### Các Chủ đề Liên quan Bạn Có Thể Khám phá Tiếp theo

- **Export Excel to CSV** với thứ tự cột tùy chỉnh.
- **Read txt files back into a workbook** (`Workbook.Load` với `LoadOptions`).
- **Batch processing** nhiều worksheet và hợp nhất chúng thành một file txt.
- **Performance tuning** cho các export quy mô lớn (streaming vs. in‑memory).

Nếu gặp khó khăn, hãy để lại bình luận, hoặc chia sẻ cách bạn đã tùy chỉnh export cho dự án của mình. Chúc lập trình vui vẻ!  

---  

*Image: A screenshot of the generated `Numbers.txt` file showing rounded values.*  
*Alt text: “Numbers.txt file displaying 12350, 0.0001235, and -98800 after saving Excel as txt with 4 significant digits.”*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}