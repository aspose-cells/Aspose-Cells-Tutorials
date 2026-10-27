---
category: general
date: 2026-02-15
description: Cách sao chép phông chữ và áp dụng kiểu ô trong C# với một ví dụ đơn
  giản. Tìm hiểu cách lấy kiểu ô và sử dụng định dạng ô để đặt kích thước phông chữ
  cho textbox.
draft: false
keywords:
- how to copy font
- apply cell style
- get cell style
- use cell formatting
- set textbox font size
language: vi
og_description: Cách sao chép phông chữ từ ô trong bảng tính và áp dụng kiểu ô cho
  TextBox. Hướng dẫn này chỉ cách lấy kiểu ô, sử dụng định dạng ô và đặt kích thước
  phông chữ cho textbox.
og_title: cách sao chép phông chữ từ ô Excel – Hướng dẫn C# đầy đủ
tags:
- C#
- EPPlus
- UI‑grid
- Excel‑interop
title: Cách sao chép phông chữ từ ô Excel sang TextBox – Hướng dẫn từng bước
url: /vi/net/working-with-fonts-in-excel/how-to-copy-font-from-an-excel-cell-to-a-textbox-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách sao chép phông chữ từ ô Excel sang TextBox – Hướng dẫn C# đầy đủ

Bạn đã bao giờ cần **sao chép phông chữ** từ một ô trong bảng tính và làm cho TextBox trong giao diện người dùng trông hoàn toàn giống hệt không? Bạn không phải là người duy nhất. Trong nhiều công cụ báo cáo hoặc bảng điều khiển tùy chỉnh, bạn sẽ phải lấy dữ liệu từ Excel và sau đó cố gắng giữ nguyên độ chính xác về hình ảnh—font family, size và colour—của ô.

Tin tốt là chỉ với vài dòng C# bạn có thể **lấy style của ô**, đọc các thuộc tính phông chữ, và **áp dụng style của ô** cho bất kỳ điều khiển textbox nào. Trong tutorial này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, có thể chạy được, cho thấy cách **sử dụng định dạng ô** và thậm chí **đặt kích thước phông chữ cho textbox** một cách lập trình.

---

## Những gì bạn sẽ học

- Cách lấy đối tượng `TextBox` từ một thành phần lưới (`gridJs` trong mẫu của chúng tôi)
- Cách đọc font family, size và colour từ một ô Excel cụ thể (`B2`)
- Cách sao chép các thuộc tính phông chữ đó sang textbox để UI phản chiếu bảng tính
- Những cạm bẫy thường gặp (ví dụ: chuyển đổi màu) và một vài **mẹo chuyên nghiệp** để mã của bạn luôn ổn định
- Một đoạn mã sẵn sàng chạy mà bạn có thể chèn vào một console app hoặc dự án WinForms

**Yêu cầu trước**  
Bạn cần có:

1. .NET 6+ (hoặc .NET Framework 4.8) đã được cài đặt  
2. Gói NuGet EPPlus (để xử lý Excel)  
3. Một điều khiển lưới cung cấp một dictionary `TextBoxes` (ví dụ sử dụng `gridJs` hư cấu, nhưng ý tưởng này áp dụng cho bất kỳ thư viện UI nào)

Bây giờ, hãy bắt tay vào thực hành.

---

## Bước 1: Thiết lập dự án và tải Worksheet

Đầu tiên, tạo một dự án console hoặc WinForms mới và thêm EPPlus:

```bash
dotnet add package EPPlus --version 6.*
```

Sau đó, tải workbook và lấy ô mà bạn muốn sao chép style.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System.Drawing;

// ...

// Load the Excel file (make sure the file exists at the given path)
var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
using var package = new ExcelPackage(fileInfo);
ExcelWorksheet ws = package.Workbook.Worksheets["Sheet1"]; // adjust sheet name if needed

// Retrieve the style of cell B2
ExcelStyle cellStyle = ws.Cells["B2"].Style;
```

**Tại sao điều này quan trọng:** EPPlus cho phép bạn truy cập trực tiếp vào đối tượng `Style`, trong đó chứa sub‑object `Font`. Từ đó bạn có thể đọc `Name`, `Size` và `Color`. Đây là phần cốt lõi của thao tác **lấy style của ô**.

---

## Bước 2: Lấy TextBox mục tiêu từ Grid của bạn

Giả sử lưới UI (`gridJs`) của bạn lưu các textbox trong một dictionary được khóa bằng tên cột, bạn có thể lấy textbox mong muốn như sau:

```csharp
// Fake grid class for illustration – replace with your actual grid component
var gridJs = new MyGrid(); // MyGrid is a placeholder for your UI control

// Step 1: Retrieve the "Notes" text box from the grid
var notesTextBox = gridJs.TextBoxes["Notes"];
```

Nếu bạn đang dùng WinForms, `notesTextBox` có thể là một điều khiển `TextBox`; với WPF có thể là một phần tử `TextBox`, và với lưới dựa trên web có thể là một đối tượng JavaScript interop. Điểm quan trọng là bạn đã có một tham chiếu có thể thao tác.

---

## Bước 3: Chuyển Font Family

Bây giờ chúng ta đã có cả style nguồn và điều khiển đích, sao chép font family.

```csharp
// Apply the cell's font family to the text box
notesTextBox.FontFamily = cellStyle.Font.Name;
```

**Mẹo chuyên nghiệp:** Không phải tất cả các framework UI đều cung cấp thuộc tính `FontFamily` nhận một chuỗi thuần. Trong WinForms bạn sẽ đặt `notesTextBox.Font = new Font(cellStyle.Font.Name, notesTextBox.Font.Size);`. Hãy điều chỉnh cho phù hợp.

---

## Bước 4: Chuyển Font Size

Kích thước phông chữ được lưu dưới dạng `float` trong EPPlus. Áp dụng trực tiếp:

```csharp
// Apply the cell's font size to the text box
notesTextBox.FontSize = cellStyle.Font.Size;
```

Nếu điều khiển của bạn sử dụng đơn vị point (hầu hết đều vậy), bạn có thể gán giá trị mà không cần chuyển đổi. Đối với các lưới dựa trên CSS, bạn có thể cần nối thêm `"pt"`.

---

## Bước 5: Chuyển Font Colour

Chuyển đổi màu là phần khó nhất vì EPPlus lưu màu dưới dạng số nguyên ARGB, trong khi nhiều framework UI mong đợi một `System.Drawing.Color` hoặc một chuỗi hex CSS.

```csharp
// Apply the cell's font colour to the text box
// EPPlus stores colour as a System.Drawing.Color when using .Color property
var excelColor = cellStyle.Font.Color?.GetColor();

// Fallback to black if the cell has no explicit colour
var safeColor = excelColor ?? Color.Black;

// Convert to the format your UI expects (example for WinForms)
notesTextBox.FontColor = safeColor;
```

> **Tại sao cách này hoạt động:** `GetColor()` giải quyết các màu dựa trên theme và trả về một `System.Drawing.Color` cụ thể. Nếu ô sử dụng màu mặc định (không có thiết lập rõ ràng), chúng ta sẽ mặc định là màu đen để tránh lỗi tham chiếu null.

---

## Ví dụ Hoạt động Đầy đủ

Kết hợp tất cả lại, đây là một console app tối thiểu đọc file Excel, trích xuất phông chữ từ **B2**, và áp dụng nó cho một textbox mô phỏng.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System;
using System.Collections.Generic;
using System.Drawing;

namespace FontCopyDemo
{
    // Mock grid control – replace with your real UI component
    public class MyGrid
    {
        public Dictionary<string, TextBoxMock> TextBoxes { get; } = new()
        {
            { "Notes", new TextBoxMock() }
        };
    }

    // Simple text box representation for demonstration
    public class TextBoxMock
    {
        public string FontFamily { get; set; }
        public float FontSize { get; set; }
        public Color FontColor { get; set; }

        public override string ToString()
        {
            return $"FontFamily: {FontFamily}, FontSize: {FontSize}, FontColor: {FontColor.Name}";
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Load Excel worksheet
            var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
            using var package = new ExcelPackage(fileInfo);
            var ws = package.Workbook.Worksheets["Sheet1"];
            var cellStyle = ws.Cells["B2"].Style;

            // 2️⃣ Grab the target TextBox from the grid
            var gridJs = new MyGrid();
            var notesTextBox = gridJs.TextBoxes["Notes"];

            // 3️⃣ Apply font family
            notesTextBox.FontFamily = cellStyle.Font.Name;

            // 4️⃣ Apply font size
            notesTextBox.FontSize = cellStyle.Font.Size;

            // 5️⃣ Apply font colour (with safety net)
            var excelColor = cellStyle.Font.Color?.GetColor();
            notesTextBox.FontColor = excelColor ?? Color.Black;

            // Output the result for verification
            Console.WriteLine("TextBox after copying font:");
            Console.WriteLine(notesTextBox);
        }
    }
}
```

**Kết quả mong đợi (giả sử B2 sử dụng Arial, 12 pt, màu xanh):**

```
TextBox after copying font:
FontFamily: Arial, FontSize: 12, FontColor: Blue
```

Chạy chương trình, mở UI của bạn, và bạn sẽ thấy textbox “Notes” giờ đã phản chiếu đúng phong cách phông chữ của ô **B2**. Không cần tinh chỉnh thủ công.

---

## Các Câu Hỏi Thường Gặp & Trường Hợp Đặc Biệt

### Nếu ô sử dụng màu theme thay vì giá trị RGB cụ thể thì sao?

`GetColor()` của EPPlus tự động giải quyết màu theme thành một `System.Drawing.Color` cụ thể. Tuy nhiên, nếu bạn dùng thư viện cũ hơn chỉ trả về chỉ số theme, bạn sẽ phải tự ánh xạ chỉ số đó tới bảng màu.

### Tôi có thể sao chép các thuộc tính style khác (ví dụ: bold, italic) không?

Chắc chắn rồi. Đối tượng `ExcelStyle.Font` còn cung cấp `Bold`, `Italic`, `Underline`, và `Strike`. Chỉ cần gán các thuộc tính tương ứng cho điều khiển UI của bạn:

```csharp
notesTextBox.FontBold = cellStyle.Font.Bold;
notesTextBox.FontItalic = cellStyle.Font.Italic;
```

### Nếu điều khiển grid không có thuộc tính `FontColor` thì sao?

Hầu hết các framework UI hiện đại đều có, nhưng nếu của bạn chỉ chấp nhận một chuỗi CSS, hãy chuyển `Color` sang dạng hex:

```csharp
string hex = $"#{notesTextBox.FontColor.R:X2}{notesTextBox.FontColor.G:X2}{notesTextBox.FontColor.B:X2}";
notesTextBox.Style["color"] = hex; // for web‑based grids
```

### Làm sao xử lý nhiều ô cùng một lúc?

Lặp qua phạm vi mong muốn, lấy style của mỗi ô, và áp dụng cho textbox tương ứng. Hãy nhớ cache các đối tượng style nếu bạn xử lý nhiều hàng để tránh giảm hiệu năng.

---

## Mẹo Chuyên Nghiệp & Những Cạm Bẫy Thường Gặp

- **Cache ExcelPackage** – mở và đóng file cho mỗi ô là rất tốn kém. Tải workbook một lần, sau đó tái sử dụng đối tượng `ExcelWorksheet`.
- **Cẩn thận với màu null** – ô kế thừa màu mặc định sẽ trả về `null`. Luôn cung cấp giá trị dự phòng (đen hoặc màu mặc định của điều khiển).
- **Lưu ý DPI scaling** – nếu bạn nhắm tới màn hình DPI cao, kích thước phông chữ có thể hiển thị hơi lớn hơn. Điều chỉnh bằng `Graphics.DpiX` nếu cần.
- **An toàn đa luồng** – EPPlus không thread‑safe. Nếu bạn xử lý nhiều sheet song song, hãy tạo một `ExcelPackage` riêng cho mỗi thread.

---

## Kết Luận

Bây giờ bạn đã biết **cách sao chép phông chữ** từ một ô Excel và **áp dụng style của ô** cho bất kỳ điều khiển textbox nào bằng C#. Bằng cách lấy `Style` của ô, trích xuất các thuộc tính `Font`, và gán chúng cho phần tử UI, bạn duy trì được tính nhất quán về hình ảnh mà không cần sao chép thủ công.

Giải pháp hoàn chỉnh—tải workbook, lấy style ô, và đặt font family, size, colour cho textbox—đã bao phủ phần cốt lõi của **sử dụng định dạng ô** và minh họa cách **đặt kích thước phông chữ cho textbox** một cách chính xác.

Tiếp theo, hãy thử mở rộng ví dụ để sao chép màu nền, viền, hoặc thậm chí toàn bộ nội dung ô. Nếu bạn đang làm việc với thư viện data‑grid hỗ trợ render ô phong phú, giờ bạn có thể cung cấp cho nó cùng một thông tin style mà bạn đã lấy từ Excel, giúp UI và báo cáo luôn đồng bộ hoàn hảo.

Có câu hỏi nào thêm? Hãy để lại bình luận hoặc khám phá các chủ đề liên quan như “ràng buộc Excel‑to‑UI động” và “chuyển đổi màu theme‑aware”. Chúc bạn lập trình vui vẻ!

---

![cách sao chép phông chữ ví dụ](placeholder-image.jpg "cách sao chép phông chữ từ ô Excel sang TextBox")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}