---
category: general
date: 2026-10-26
description: Tìm hiểu cách sử dụng CultureInfo lịch Nhật trong C# khi phân tích ngày
  theo niên hiệu và chèn chúng vào bảng tính Excel bằng NPOI.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- use japanese calendar cultureinfo
- japanese era date parsing
- cultureinfo with japanese calendar
- datetime parse with cultureinfo
- npoi excel cultureinfo
language: vi
lastmod: 2026-10-26
og_description: Sử dụng CultureInfo lịch Nhật trong C# để phân tích ngày tháng thời
  đại Reiwa và ghi chúng vào bảng tính Excel. Mã hoàn chỉnh, có thể chạy được kèm
  giải thích.
og_image_alt: Screenshot of C# code parsing a Japanese era date and inserting it into
  an Excel cell
og_title: Sử dụng CultureInfo lịch Nhật trong C# – ví dụ Excel đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use Japanese calendar CultureInfo in C# when parsing era
    dates and inserting them into an Excel worksheet with NPOI.
  headline: How to use Japanese calendar CultureInfo in C# to write dates to Excel
  type: TechArticle
tags:
- C#
- CultureInfo
- Excel
- NPOI
- Internationalization
title: Cách sử dụng CultureInfo lịch Nhật trong C# để ghi ngày vào Excel
url: /vi/net/excel-custom-number-date-formatting/how-to-use-japanese-calendar-cultureinfo-in-c-to-write-dates/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách sử dụng Japanese calendar CultureInfo trong C# để ghi ngày vào Excel

Nếu bạn cần **sử dụng Japanese calendar CultureInfo** khi làm việc với ngày tháng trong C#, hướng dẫn này sẽ chỉ cho bạn cách thực hiện. Bạn sẽ học cách phân tích một chuỗi ngày có chứa tên niên hiệu Nhật Bản (ví dụ, *Reiwa 2/5/1*) và sau đó ghi `DateTime` kết quả vào ô đầu tiên của một worksheet Excel bằng thư viện NPOI.

Phân tích ngày dựa trên niên hiệu mà không có `CultureInfo` đúng sẽ gây ra `FormatException` hoặc giá trị tháng/ngày không chính xác. Bằng cách cấu hình `CultureInfo` thành Japanese calendar, bạn đảm bảo .NET runtime diễn giải niên hiệu đúng và giá trị bạn lưu vào Excel khớp với ký hiệu Nhật Bản gốc.

Trong tutorial này bạn sẽ:

* Tạo một đối tượng `CultureInfo` sử dụng Japanese calendar.
* Phân tích một chuỗi ngày theo niên hiệu Nhật Bản bằng `DateTime.Parse`.
* Chèn `DateTime` đã phân tích vào ô worksheet NPOI.
* Xem chương trình hoàn chỉnh, có thể chạy và kết quả mong đợi.

> **Prerequisites** – .NET 6.0+ (hoặc .NET Core 3.1+), gói **NPOI** NuGet, và hiểu biết cơ bản về C# và xử lý tệp Excel.

---

## Những gì bạn cần

| Mục | Lý do |
|------|--------|
| **.NET SDK** (6.0 hoặc mới hơn) | Cung cấp runtime và các thư viện cho `CultureInfo`. |
| **NPOI** (`NPOI` NuGet package) | Cho phép tạo và thao tác tệp Excel mà không cần cài Office. |
| **Visual Studio Code**, **Visual Studio**, hoặc bất kỳ IDE C# nào | Để biên dịch và chạy mẫu. |
| **Japanese era date string** (ví dụ, `"Reiwa 2/5/1"`) | Minh họa việc sử dụng Japanese calendar. |

---

## Bước 1: Cài đặt NPOI

Mở terminal trong thư mục dự án của bạn và chạy:

```bash
dotnet add package NPOI --version 2.6.1
```

Gói này cung cấp các kiểu `IWorkbook`, `ISheet`, và `ICell` sẽ được sử dụng sau này.

---

## Bước 2: Tạo một CultureInfo sử dụng Japanese calendar

Japanese calendar là một lịch dựa trên niên hiệu. Bạn phải yêu cầu biến thể *Japanese* của locale `ja-JP` và đặt rõ ràng lịch thành `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;

// Create a CultureInfo based on Japanese locale and switch its calendar.
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

> **Why this matters** – Văn hoá mặc định `ja-JP` sử dụng Gregorian calendar. Gán lại thuộc tính `Calendar` đảm bảo các tên niên hiệu như *Reiwa* được nhận diện khi phân tích.

---

## Bước 3: Phân tích một chuỗi ngày theo niên hiệu Nhật Bản

Khi `CultureInfo` đã được cấu hình, bạn có thể an toàn phân tích một chuỗi chứa tên niên hiệu.

```csharp
// Example Japanese era date: Reiwa 2 (2020) year, May 1st.
string eraDate = "Reiwa 2/5/1";

// Parse using the Japanese CultureInfo created earlier.
DateTime reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
Console.WriteLine($"Parsed DateTime (UTC): {reiwaDate:u}");
```

**Kết quả**

```
Parsed DateTime (UTC): 2020-05-01 00:00:00Z
```

Phương thức `Parse` diễn giải *Reiwa 2* thành năm Gregorian 2020, tháng 5, ngày 1.

### Trường hợp đặc biệt: xử lý niên hiệu không hợp lệ

Nếu người dùng cung cấp một niên hiệu không được hỗ trợ (ví dụ, `"Heisei 31/4/30"` sau khi niên hiệu Heisei kết thúc), `DateTime.Parse` sẽ ném `FormatException`. Bao quanh lời gọi trong khối try‑catch để đưa ra thông báo lỗi thân thiện:

```csharp
try
{
    DateTime parsed = DateTime.Parse(input, japaneseCulture);
}
catch (FormatException)
{
    Console.Error.WriteLine($"'{input}' is not a valid Japanese era date.");
}
```

---

## Bước 4: Ghi `DateTime` đã phân tích vào worksheet Excel

Với đối tượng `DateTime` đã sẵn sàng, bạn có thể lưu nó vào một ô Excel. NPOI tự động định dạng giá trị `DateTime` thành ngày Excel.

```csharp
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;
using System.IO;

// Create a new workbook and a sheet.
IWorkbook workbook = new XSSFWorkbook();
ISheet sheet = workbook.CreateSheet("Japanese Dates");

// Write the DateTime into cell A1 (row 0, column 0).
IRow row = sheet.CreateRow(0);
ICell cell = row.CreateCell(0);
cell.SetCellValue(reiwaDate);

// Optionally apply a date style that shows the era (Excel does not have a built‑in era format,
// so we keep the Gregorian representation).
ICellStyle dateStyle = workbook.CreateCellStyle();
short dateFormatId = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
dateStyle.DataFormat = dateFormatId;
cell.CellStyle = dateStyle;

// Save the workbook to a file.
using (FileStream fs = new FileStream("JapaneseEraDate.xlsx", FileMode.Create, FileAccess.Write))
{
    workbook.Write(fs);
}
Console.WriteLine("Excel file 'JapaneseEraDate.xlsx' created successfully.");
```

**Result** – Khi mở *JapaneseEraDate.xlsx* sẽ hiển thị ngày **2020‑05‑01** ở ô A1.

### Tại sao lại dùng NPOI?

*Works on any platform* (Windows, Linux, macOS) và **không** yêu cầu Microsoft Office. Điều này làm cho giải pháp phù hợp cho các pipeline CI, container Docker, hoặc xử lý phía server.

---

## Bước 5: Chương trình đầy đủ, có thể chạy

Kết hợp mọi thứ lại, dưới đây là một ứng dụng console hoàn chỉnh minh họa toàn bộ quy trình:

```csharp
// File: Program.cs
using System;
using System.Globalization;
using System.IO;
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure CultureInfo for the Japanese calendar.
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // 2️⃣ Parse a Japanese era date string.
        string eraDate = "Reiwa 2/5/1";
        DateTime reiwaDate;
        try
        {
            reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
            Console.WriteLine($"Parsed DateTime: {reiwaDate:u}");
        }
        catch (FormatException)
        {
            Console.Error.WriteLine($"'{eraDate}' is not a valid Japanese era date.");
            return;
        }

        // 3️⃣ Create an Excel workbook and write the date.
        IWorkbook workbook = new XSSFWorkbook();
        ISheet sheet = workbook.CreateSheet("Japanese Dates");
        IRow row = sheet.CreateRow(0);
        ICell cell = row.CreateCell(0);
        cell.SetCellValue(reiwaDate);

        // Apply a simple Gregorian date format.
        ICellStyle style = workbook.CreateCellStyle();
        short fmt = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
        style.DataFormat = fmt;
        cell.CellStyle = style;

        // 4️⃣ Save the workbook.
        const string fileName = "JapaneseEraDate.xlsx";
        using (FileStream fs = new FileStream(fileName, FileMode.Create, FileAccess.Write))
        {
            workbook.Write(fs);
        }

        Console.WriteLine($"Excel file '{fileName}' created successfully.");
    }
}
```

**Cách chạy**

```bash
dotnet run
```

Sau khi thực thi, bạn sẽ tìm thấy `JapaneseEraDate.xlsx` trong thư mục dự án với ngày đã được phân tích chính xác.

---

## Các lỗi thường gặp và mẹo thực hành tốt

| Lỗi thường gặp | Cách khắc phục / Khuyến nghị |
|----------------|------------------------------|
| Quên đặt `japaneseCulture.DateTimeFormat.Calendar` | Luôn gán một instance của `JapaneseCalendar`; nếu không, tên niên hiệu sẽ không được nhận diện. |
| Dùng `DateTime.TryParse` mà không truyền `CultureInfo` tùy chỉnh | Truyền cùng `japaneseCulture` cho `TryParse` để duy trì hành vi nhất quán. |
| Mong Excel hiển thị tên niên hiệu | Định dạng ngày tích hợp của Excel chỉ hỗ trợ Gregorian. Nếu cần hiển thị niên hiệu, lưu chuỗi gốc vào cột riêng hoặc tạo định dạng văn bản tùy chỉnh. |
| Không giải phóng `FileStream` | Sử dụng khối `using` (như trong ví dụ) để đảm bảo handle tệp được giải phóng kịp thời. |
| Trộn các đối tượng `CultureInfo` giữa các luồng | `CultureInfo` an toàn với luồng cho các thao tác chỉ đọc, nhưng tránh thay đổi thuộc tính `Calendar` sau khi đã thiết lập. |

---

## Kết luận

Bạn đã biết cách **sử dụng Japanese calendar CultureInfo** trong C# để phân tích chính xác ngày theo niên hiệu Nhật Bản và ghi `DateTime` kết quả vào worksheet Excel bằng NPOI. Ví dụ đầy đủ bao gồm cấu hình, phân tích, xử lý lỗi và xuất ra Excel, cung cấp nền tảng vững chắc cho bất kỳ kịch bản báo cáo quốc tế hoá hoặc trao đổi dữ liệu nào.

Tiếp theo, bạn có thể khám phá:

* **Định dạng ngày bằng văn bản tùy chỉnh** để giữ lại tên niên hiệu trong Excel.
* **Đọc ngày từ Excel** bằng `cell.DateCellValue` đồng thời tôn trọng Japanese calendar.
* **Áp dụng kỹ thuật tương tự** cho các lịch dựa trên niên hiệu khác (ví dụ, Thai Buddhist calendar) bằng cách thay `JapaneseCalendar` bằng lớp `Calendar` phù hợp.

Hãy thoải mái thử nghiệm với các chuỗi niên hiệu khác, bộ dữ liệu lớn hơn, hoặc tích hợp logic này vào API ASP.NET Core tạo báo cáo Excel động. Chúc bạn lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã nguồn đầy đủ và giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Tạo Workbook Excel với ngày theo Japanese Calendar – Hướng dẫn đầy đủ](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-japanese-calendar-dates-full-guid/)
- [Phân tích ngày theo Japanese Era trong Excel – Hướng dẫn đầy đủ cho nhà phát triển C#](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [Cách tạo workbook Excel và phân tích ngày Nhật trong C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}