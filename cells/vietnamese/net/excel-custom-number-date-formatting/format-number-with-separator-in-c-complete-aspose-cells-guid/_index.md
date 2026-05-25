---
category: general
date: 2026-03-30
description: Học cách định dạng số với dấu phân cách bằng Aspose.Cells trong C#. Bao
  gồm thiết lập định dạng số tùy chỉnh, thêm dấu phân cách hàng nghìn, định dạng số
  thập phân và cách định dạng ô.
draft: false
keywords:
- format number with separator
- set custom number format
- add thousands separator
- format decimal places
- how to format cell
language: vi
og_description: Định dạng số với dấu phân cách trong C#. Hướng dẫn này chỉ cách thiết
  lập định dạng số tùy chỉnh, thêm dấu phân cách hàng nghìn, định dạng số thập phân
  và cách định dạng ô bằng Aspose.Cells.
og_title: Định dạng số với dấu phân cách trong C# – Hướng dẫn Aspose.Cells
tags:
- C#
- Aspose.Cells
- Number Formatting
title: Định dạng số với dấu phân cách trong C# – Hướng dẫn đầy đủ Aspose.Cells
url: /vi/net/excel-custom-number-date-formatting/format-number-with-separator-in-c-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Định dạng số có dấu phân cách trong C# – Hướng dẫn đầy đủ Aspose.Cells

Bạn đã bao giờ cần **format number with separator** trong một bảng tính nhưng không chắc nên gọi API nào không? Bạn không phải là người duy nhất—các nhà phát triển luôn phải vật lộn với dấu phân cách hàng nghìn, số thập phân và các mẫu tùy chỉnh khi xuất dữ liệu.  

Tin tốt: Aspose.Cells làm cho việc này trở nên dễ dàng. Trong hướng dẫn này, chúng tôi sẽ đi qua một ví dụ thực tế mà **sets a custom number format**, **adds a thousands separator**, **formats decimal places**, và cho thấy **how to format cell** output as a string. Khi hoàn thành, bạn sẽ có một đoạn mã sẵn sàng chạy mà bạn có thể chèn vào bất kỳ dự án .NET nào.

## Những gì hướng dẫn này bao gồm

* Gói NuGet chính xác bạn cần và cách cài đặt nó.  
* Mã từng bước tạo workbook, ghi giá trị số và áp dụng định dạng tùy chỉnh.  
* Tại sao `ExportTableOptions.ExportAsString` là cách ưu tiên để lấy giá trị đã định dạng.  
* Các lỗi thường gặp—như quên bật `ExportAsString` hoặc sử dụng mask định dạng sai.  
* Cách điều chỉnh mask định dạng nếu bạn cần số chữ số thập phân khác hoặc kiểu dấu phân cách khác.

Không cần liên kết tài liệu bên ngoài; mọi thứ bạn cần đều có ở đây. Hãy bắt đầu.

---

## Prerequisites

| Yêu cầu | Lý do |
|-------------|--------|
| .NET 6.0 hoặc sau này | Aspose.Cells 23.10+ nhắm tới .NET Standard 2.0+, vì vậy .NET 6 là an toàn và hiện tại. |
| Visual Studio 2022 (hoặc bất kỳ IDE C# nào) | Giúp việc gỡ lỗi và quản lý gói dễ dàng. |
| Gói NuGet Aspose.Cells cho .NET | Cung cấp các lớp `Workbook`, `Worksheet`, và `ExportTableOptions` mà chúng ta sẽ sử dụng. |

Bạn có thể cài đặt gói qua Package Manager Console:

```powershell
Install-Package Aspose.Cells
```

Xong—không cần DLL bổ sung, không cần COM interop, chỉ một tham chiếu NuGet duy nhất.

## Bước 1: Khởi tạo Workbook mới (How to Format Cell)

Điều đầu tiên chúng ta làm là tạo một thể hiện `Workbook` mới. Hãy nghĩ nó như một tệp Excel trống sẵn sàng nhận dữ liệu.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is where we’ll format the cell.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Tại sao điều này quan trọng:** `Workbook` là điểm vào cho mọi thao tác trong Aspose.Cells. Bằng cách lấy worksheet đầu tiên (`Worksheets[0]`) chúng ta có một canvas sạch sẽ mà không cần đặt tên cho sheet.

## Bước 2: Ghi giá trị số vào ô mục tiêu

Tiếp theo, chúng ta đặt một số thô vào ô **A1**. Giá trị này chưa được định dạng—nó chỉ là một kiểu double.

```csharp
        // Step 2: Insert a raw numeric value.
        worksheet.Cells["A1"].PutValue(12345.6789);
```

> **Mẹo chuyên nghiệp:** Sử dụng `PutValue` thay vì `PutString` khi bạn dự định áp dụng định dạng số sau này. Điều này giữ nguyên kiểu dữ liệu gốc, cho phép các phép tính tương thích với Excel.

## Bước 3: Đặt định dạng số tùy chỉnh (Thêm dấu phân cách hàng nghìn & Định dạng chữ số thập phân)

Bây giờ là phần cốt lõi của hướng dẫn: định nghĩa mask định dạng cho Aspose.Cells biết cách hiển thị số. Mask `#,##0.00` thực hiện ba việc:

1. **`#,##0`** – thêm dấu phân cách hàng nghìn (mặc định là dấu phẩy).  
2. **`.00`** – buộc luôn có đúng hai chữ số thập phân.  

Nếu bạn cần số chữ số thập phân khác, chỉ cần thay đổi số lượng `0` sau dấu thập phân.

```csharp
        // Step 3: Configure the custom number format.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // Return the value as a formatted string.
            NumberFormat = "#,##0.00"       // Add thousands separator and fix to 2 decimals.
        };
```

> **Tại sao chúng ta dùng `ExportAsString`:** Mặc định, `ExportString` trả về giá trị thô. Đặt `ExportAsString = true` buộc API áp dụng mask `NumberFormat` trước khi chuyển sang văn bản. Điều này rất cần thiết khi bạn cần biểu diễn chuỗi chính xác cho báo cáo, payload JSON, hoặc hiển thị UI.

## Bước 4: Xuất văn bản đã định dạng (How to Format Cell)

Với các tùy chọn đã sẵn sàng, chúng ta gọi `ExportString` trên cùng một ô. Phương thức này tuân theo mask vừa định nghĩa và trả về một chuỗi đã được định dạng đẹp mắt.

```csharp
        // Step 4: Export the formatted value.
        string formattedCellText = worksheet.Cells["A1"].ExportString(exportOptions);

        // Step 5: Show the result.
        Console.WriteLine(formattedCellText); // Expected output: 12,345.68
    }
}
```

Chạy chương trình sẽ in **`12,345.68`** ra console—đúng như định dạng chúng ta yêu cầu.

> **Trường hợp đặc biệt:** Nếu số nguồn có hơn hai chữ số thập phân, mask sẽ làm tròn. Nếu bạn cần cắt bớt thay vì làm tròn, bạn phải tiền xử lý giá trị bằng `Math.Truncate` trước khi gọi `PutValue`.

## Bước 5: Điều chỉnh định dạng – Các biến thể thường gặp

### 5.1 Thay đổi độ chính xác thập phân

Muốn ba chữ số thập phân? Chỉ cần thay đổi mask:

```csharp
NumberFormat = "#,##0.000"   // → 12,345.679
```

### 5.2 Sử dụng dấu phân cách hàng nghìn khác

Một số địa phương thích dấu cách hoặc dấu chấm. Bạn có thể nhúng ký tự trực tiếp:

```csharp
NumberFormat = "# ##0.00"    // Uses a non‑breaking space as separator.
```

Hoặc dựa vào cài đặt ngôn ngữ của workbook:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("de-DE");
NumberFormat = "#.##0,00";   // German style: 12.345,68
```

### 5.3 Tiền tố hoặc Hậu tố (Tiền tệ, Phần trăm)

Thêm dấu đô la hoặc dấu phần trăm ngay trong mask:

```csharp
NumberFormat = "$#,##0.00";   // → $12,345.68
NumberFormat = "0.00%";       // → 1,234,568.00%
```

> **Lưu ý:** Mask phân biệt chữ hoa và chữ thường. `$` và `%` là ký hiệu nguyên văn; chúng không ảnh hưởng tới giá trị số gốc.

## Bước 6: Ví dụ hoàn chỉnh (Sẵn sàng sao chép‑dán)

Dưới đây là chương trình đầy đủ mà bạn có thể sao chép vào một ứng dụng console mới. Nó bao gồm tất cả các bước, chú thích và xác minh đầu ra cuối cùng.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise workbook and worksheet.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write raw numeric value to A1.
        worksheet.Cells["A1"].PutValue(12345.6789);

        // 3️⃣ Define custom format: thousands separator + two decimals.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00"
        };

        // 4️⃣ Export the formatted string.
        string result = worksheet.Cells["A1"].ExportString(exportOptions);

        // 5️⃣ Display the outcome.
        Console.WriteLine(result); // Output: 12,345.68

        // Optional: keep console open.
        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
}
```

Chạy chương trình (`dotnet run` từ terminal hoặc nhấn F5 trong Visual Studio) và bạn sẽ thấy số đã định dạng được in ra chính xác như hình.

## Câu hỏi thường gặp (FAQ)

**Q: Điều này có hoạt động với các phiên bản Excel cũ không?**  
A: Có. Mask định dạng tuân theo cú pháp định dạng số gốc của Excel, vì vậy bất kỳ phiên bản nào hiểu `#,##0.00` sẽ hiển thị cùng một chuỗi.

**Q: Nếu tôi cần định dạng một phạm vi ô thì sao?**  
A: Lặp qua phạm vi mong muốn và áp dụng cùng một `ExportTableOptions` cho mỗi ô, hoặc đặt thuộc tính `Style.Custom` trên phạm vi và sau đó gọi `ExportString` trên một ô duy nhất.

**Q: Tôi có thể xuất trực tiếp sang CSV với các định dạng này không?**  
A: Chắc chắn. Sử dụng `Workbook.Save("output.csv", SaveFormat.CSV);` sau khi đặt định dạng cho mỗi ô. Aspose.Cells tôn trọng `Style` của ô khi tạo CSV.

## Kết luận

Chúng tôi vừa trình bày cách **format number with separator** trong C# bằng Aspose.Cells, bao gồm mọi thứ từ **set custom number format** đến **add thousands separator**, **format decimal places**, và phần quan trọng **how to format cell** để xuất chuỗi. Mã hoàn toàn tự chứa, hoạt động với .NET 6+, và có thể điều chỉnh cho bất kỳ địa phương hay yêu cầu độ chính xác nào.

Tiếp theo, bạn có thể khám phá:

* Áp dụng kỹ thuật tương tự cho ngày và giờ (`NumberFormat = "dd‑MMM‑yyyy"`).  
* Tự động xuất hàng loạt khi mỗi cột cần một mask khác nhau.  
* Tích hợp các chuỗi đã định dạng vào báo cáo PDF với Aspose.Words.

Hãy thử những điều trên, và bạn sẽ nhanh chóng trở thành người được tin cậy cho việc định dạng bảng tính trong nhóm của mình. Chúc lập trình vui vẻ!  

![Ảnh chụp màn hình hiển thị số đã định dạng có dấu phân cách trong Aspose.Cells](image-placeholder.png){alt="Số đã định dạng có dấu phân cách hiển thị trong đầu ra của Aspose.Cells"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}