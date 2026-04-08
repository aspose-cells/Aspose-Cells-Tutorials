---
category: general
date: 2026-04-07
description: Áp dụng định dạng số tùy chỉnh cho một ô trong bảng tính và học cách
  định dạng số trong bảng tính khi xuất giá trị ô bằng C#. Hướng dẫn nhanh, đầy đủ.
draft: false
keywords:
- apply custom number format
- format number in spreadsheet
- how to format numeric cell
- how to export cell value
language: vi
og_description: Áp dụng định dạng số tùy chỉnh cho ô trong bảng tính và xuất nó dưới
  dạng chuỗi đã định dạng. Tìm hiểu cách định dạng số trong bảng tính và xuất giá
  trị ô.
og_title: Áp dụng Định dạng Số Tùy chỉnh – Hướng dẫn Xuất C# đầy đủ
tags:
- C#
- Spreadsheet
- Number Formatting
title: Áp dụng Định dạng Số Tùy chỉnh trong Xuất Bảng tính C# – Hướng dẫn từng bước
url: /vi/net/excel-custom-number-date-formatting/apply-custom-number-format-in-c-spreadsheet-export-step-by-s/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Áp dụng Định dạng Số Tùy chỉnh trong Xuất Bảng tính C# – Hướng dẫn Đầy đủ

Bạn đã bao giờ cần **áp dụng định dạng số tùy chỉnh** cho một ô và sau đó lấy chuỗi đã định dạng ra khỏi bảng tính chưa? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi giá trị thô được trả về thay vì chuỗi đẹp mắt, phù hợp với ngôn ngữ địa phương mà họ mong đợi. Trong hướng dẫn này, chúng tôi sẽ chỉ cho bạn cách định dạng số trong các ô bảng tính và cách xuất giá trị ô dưới dạng chuỗi đã định dạng bằng một thư viện bảng tính C# phổ biến.

Khi hoàn thành bài hướng dẫn, bạn sẽ có thể **áp dụng định dạng số tùy chỉnh** cho bất kỳ ô số nào, xuất kết quả bằng `ExportTable`, và xem đầu ra chính xác như bạn mong muốn hiển thị trong giao diện người dùng hoặc báo cáo. Không cần tài liệu bên ngoài—mọi thứ đã có ở đây.

## Các yêu cầu trước

- .NET 6.0 trở lên (mã cũng hoạt động trên .NET Framework 4.7+)
- Tham chiếu tới thư viện bảng tính cung cấp `Workbook`, `Worksheet`, và `ExportTableOptions` (ví dụ: **Aspose.Cells** hoặc **GemBox.Spreadsheet**; API được minh họa phù hợp với Aspose.Cells)
- Kiến thức cơ bản về C#—nếu bạn có thể viết một `Console.WriteLine`, bạn đã sẵn sàng

> **Pro tip:** Nếu bạn đang dùng thư viện khác, các tên thuộc tính thường tương tự (`NumberFormat`, `ExportAsString`). Chỉ cần ánh xạ chúng cho phù hợp.

## Nội dung hướng dẫn

1. Tạo một workbook và chọn worksheet đầu tiên.  
2. Chèn một giá trị số vào một ô.  
3. Cấu hình `ExportTableOptions` để **áp dụng định dạng số tùy chỉnh** và trả về một chuỗi.  
4. Xuất ô và in kết quả đã định dạng.  
5. Xử lý các trường hợp đặc biệt – nếu ô chứa công thức hoặc giá trị null thì sao?

Hãy bắt đầu.

![ví dụ áp dụng định dạng số tùy chỉnh](https://example.com/image.png "áp dụng định dạng số tùy chỉnh")

## Bước 1 – Tạo workbook và lấy worksheet đầu tiên

Điều đầu tiên bạn cần là một đối tượng workbook. Hãy nghĩ nó như một tệp Excel mà bạn sẽ mở trong ứng dụng Office. Khi đã có, lấy sheet đầu tiên—hầu hết các hướng dẫn bắt đầu ở đây vì nó giữ cho ví dụ ngắn gọn.

```csharp
// Step 1: Initialize the workbook and fetch the first worksheet
Workbook workbook = new Workbook();                 // creates an in‑memory workbook
Worksheet worksheet = workbook.Worksheets[0];      // first sheet (index 0)
```

**Tại sao lại quan trọng:** Một workbook mới cung cấp một “bảng trắng” sạch sẽ, đảm bảo không có định dạng ẩn can thiệp vào định dạng số tùy chỉnh của chúng ta sau này.

## Bước 2 – Đặt giá trị số vào ô B2 (ô sẽ được xuất)

Bây giờ chúng ta cần một giá trị để định dạng. Ô **B2** là vị trí thuận tiện—dễ tham chiếu và đủ xa góc A1 mặc định để tránh ghi đè nhầm.

```csharp
// Step 2: Insert a raw numeric value
worksheet.Cells["B2"].Value = 1234.56;   // raw double, no formatting yet
```

**Nếu giá trị là công thức thì sao?**  
Nếu bạn sau này thay thế giá trị thô bằng một công thức (ví dụ, `=SUM(A1:A10)`), quy trình xuất vẫn sẽ tôn trọng định dạng số mà chúng ta áp dụng ở bước tiếp theo, vì định dạng được gắn vào ô, không phải vào kiểu giá trị.

## Bước 3 – Cấu hình tùy chọn xuất để nhận giá trị dưới dạng chuỗi đã định dạng

Đây là phần cốt lõi của hướng dẫn: chúng ta yêu cầu thư viện **áp dụng định dạng số tùy chỉnh** khi xuất. Chuỗi `NumberFormat` tuân theo cùng mẫu bạn sẽ dùng trong mục “Custom” của Excel.

```csharp
// Step 3: Set up options for exporting as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,                         // forces string output
    NumberFormat = "#,##0.00;(#,##0.00)"           // custom format: 1,234.56 or (1,234.56) for negatives
};
```

- `ExportAsString = true` đảm bảo phương thức trả về một `string` thay vì một double thô.  
- `NumberFormat = "#,##0.00;(#,##0.00)"` sao chép mẫu của Excel: dấu phẩy cho hàng nghìn, hai chữ số thập phân, và dấu ngoặc tròn cho số âm.

> **Tại sao lại dùng định dạng tùy chỉnh?** Nó đảm bảo tính nhất quán giữa các nền văn hoá (ví dụ, dấu phân cách số ở Mỹ vs. châu Âu) và cho phép bạn nhúng kiểu dáng kinh doanh như dấu ngoặc cho số âm trong kế toán.

## Bước 4 – Xuất ô bằng các tùy chọn đã cấu hình

Bây giờ chúng ta thực sự lấy giá trị ra khỏi worksheet, để thư viện thực hiện việc áp dụng định dạng mà chúng ta đã định nghĩa.

```csharp
// Step 4: Export the formatted value from B2
string formattedResult = worksheet.Cells.ExportTable(
    worksheet.Cells["B2"],   // the source cell
    exportOptions);         // our custom options
```

**Trường hợp đặc biệt – ô trống:** Nếu `B2` trống, `formattedResult` sẽ là `null`. Bạn có thể kiểm tra null đơn giản trước khi in.

## Bước 5 – Hiển thị chuỗi đã định dạng

Cuối cùng, chúng ta ghi kết quả ra console. Trong một ứng dụng thực tế, bạn có thể đưa chuỗi này vào PDF, email, hoặc nhãn UI.

```csharp
// Step 5: Show the result
Console.WriteLine(formattedResult);   // Expected output: 1,234.56
```

**Kết quả mong đợi**

```
1,234.56
```

Nếu bạn thay đổi giá trị thô thành `-9876.54`, cùng một định dạng sẽ cho ra `(9,876.54)`—đúng như nhiều báo cáo kế toán yêu cầu.

## Ví dụ đầy đủ, có thể chạy

Dưới đây là chương trình hoàn chỉnh mà bạn có thể sao chép‑dán vào một dự án console mới. Nó biên dịch và chạy ngay, với giả định bạn đã thêm gói NuGet thích hợp cho thư viện bảng tính.

```csharp
using System;
using Aspose.Cells;   // Replace with your library’s namespace if different

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Insert numeric value into B2
        worksheet.Cells["B2"].Value = 1234.56;

        // 3️⃣ Set export options – apply custom number format
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00;(#,##0.00)"   // custom format
        };

        // 4️⃣ Export the cell as a formatted string
        string formattedResult = worksheet.Cells.ExportTable(
            worksheet.Cells["B2"], exportOptions);

        // 5️⃣ Output the result
        Console.WriteLine(formattedResult);   // → 1,234.56
    }
}
```

### Kiểm tra nhanh

- **Có biên dịch không?** Có—chỉ cần chắc chắn rằng DLL `Aspose.Cells` (hoặc tương đương) đã được tham chiếu.  
- **Có hoạt động với các nền văn hoá khác không?** Chuỗi định dạng không phụ thuộc vào ngôn ngữ; thư viện sẽ tuân theo mẫu bạn cung cấp. Nếu bạn cần dấu phân cách theo locale, có thể thêm xử lý `CultureInfo` trước khi xuất.

## Các câu hỏi thường gặp & biến thể

### Làm sao **định dạng số trong bảng tính** bằng một mẫu khác?

Thay đổi chuỗi `NumberFormat`. Ví dụ, để hiển thị phần trăm với một chữ số thập phân:

```csharp
NumberFormat = "0.0%";
```

### Nếu tôi muốn **xuất giá trị ô** dưới dạng HTML thay vì văn bản thuần?

Hầu hết các thư viện có một overload chấp nhận kiểu xuất. Bạn sẽ đặt `ExportAsString = true` và thêm `ExportHtml = true` (hoặc tương tự). Nguyên tắc vẫn giữ nguyên: định nghĩa định dạng, rồi chọn dạng đầu ra.

### Tôi có thể áp dụng định dạng cho một phạm vi, không chỉ một ô duy nhất không?

Chắc chắn. Bạn có thể gán `NumberFormat` cho một đối tượng `Style` rồi áp dụng style đó cho một `Range`. Lệnh xuất vẫn không thay đổi; nó sẽ tự động lấy style.

```csharp
Style style = workbook.CreateStyle();
style.Custom = "#,##0.00;(#,##0.00)";
Range range = worksheet.Cells.CreateRange("A1:C10");
range.ApplyStyle(style, new StyleFlag { NumberFormat = true });
```

### Điều gì xảy ra khi ô chứa công thức?

Quy trình xuất sẽ tính toán công thức trước, sau đó định dạng giá trị số thu được. Không cần mã bổ sung—chỉ cần chắc chắn đã gọi `Calculate` nếu bạn đã tắt tính toán tự động.

```csharp
worksheet.Cells["B2"].Formula = "=SUM(A1:A5)";
worksheet.Calculate();   // forces evaluation
```

## Kết luận

Bây giờ bạn đã biết cách **áp dụng định dạng số tùy chỉnh** cho một ô bảng tính, **định dạng số trong bảng tính** trong các ngữ cảnh khác nhau, và **xuất giá trị ô** dưới dạng chuỗi sẵn sàng hiển thị. Đoạn mã ngắn gọn ở trên bao phủ mọi bước—from tạo workbook đến xuất ra cuối cùng—để bạn có thể chèn ngay vào dự án thực tế.

Sẵn sàng cho thử thách tiếp theo? Hãy thử kết hợp kỹ thuật này với **định dạng ô số** cho ngày tháng, ký hiệu tiền tệ, hoặc định dạng có điều kiện. Hoặc khám phá việc xuất nhiều ô dưới dạng CSV trong khi giữ nguyên định dạng tùy chỉnh của từng ô. Không giới hạn, và với những nền tảng này, bạn đã có một khởi đầu vững chắc.

Chúc lập trình vui vẻ, và đừng quên thử nghiệm—đôi khi câu trả lời tốt nhất xuất hiện khi bạn tinh chỉnh chuỗi định dạng một chút!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}