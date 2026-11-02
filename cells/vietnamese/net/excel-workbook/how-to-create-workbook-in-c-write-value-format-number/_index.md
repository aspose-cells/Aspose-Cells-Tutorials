---
category: general
date: 2026-03-01
description: Cách tạo workbook trong C# nhanh chóng—học cách ghi giá trị vào ô, đặt
  định dạng số cho ô và định dạng số ô với các bước đơn giản.
draft: false
keywords:
- how to create workbook
- write value to cell
- format cell number
- set cell number format
- how to write cell
language: vi
og_description: Cách tạo workbook trong C#? Hướng dẫn này cho bạn biết cách ghi giá
  trị vào ô, đặt định dạng số cho ô và định dạng số ô chỉ trong vài dòng mã.
og_title: Cách tạo Workbook trong C# – Ghi giá trị và định dạng số
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Cách tạo Workbook trong C# – Ghi giá trị và định dạng số
url: /vi/net/excel-workbook/how-to-create-workbook-in-c-write-value-format-number/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách tạo Workbook trong C# – Ghi giá trị & Định dạng số

Tạo workbook trong C# là một nhiệm vụ phổ biến khi bạn cần tạo các tệp Excel một cách nhanh chóng. Trong hướng dẫn này, chúng tôi sẽ chỉ cho bạn cách ghi giá trị vào ô và định dạng số ô để bảng tính cuối cùng trông chuyên nghiệp.

Nếu bạn từng nhìn chằm chằm vào một bảng tính trống và tự hỏi tại sao các số luôn hiển thị quá nhiều chữ thập phân, bạn không phải là người duy nhất. Chúng tôi sẽ bao phủ mọi thứ từ việc khởi tạo đối tượng workbook đến việc đặt định dạng số tùy chỉnh, và sẽ đưa vào một vài mẹo cho các trường hợp đặc biệt mà bạn có thể gặp sau này.

## Những gì bạn sẽ học

- **Initialize** một thể hiện `Workbook` mới.  
- **Write value to cell** bằng phương thức `PutValue`.  
- **Set cell number format** với một đối tượng `Style`, đạt được hiển thị hai chữ số sạch sẽ.  
- Xác minh kết quả bằng cách đọc lại ô hoặc mở tệp trong Excel.  

Không cần thư viện bên ngoài nào ngoài Aspose.Cells tiêu chuẩn (hoặc bất kỳ API tương tự nào), và mã chạy trên .NET 6+ mà không cần cấu hình thêm.

---

## Cách tạo Workbook – Khởi tạo đối tượng

Đầu tiên: bạn cần một đối tượng workbook để chứa các sheet của mình. Hãy nghĩ `Workbook` như toàn bộ tệp Excel, trong khi mỗi `Worksheet` là một tab riêng.

```csharp
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

*Why this matters:* Tạo workbook sẽ cấp phát các cấu trúc nội bộ sau này sẽ chứa các hàng, cột và định dạng. Không có đối tượng này, sẽ không có nơi nào để ghi giá trị vào ô.

> **Pro tip:** Nếu bạn dự định làm việc với một tệp đã tồn tại, thay `new Workbook()` bằng `new Workbook("template.xlsx")` để tải mẫu và giữ nguyên các kiểu dáng của nó.

## Ghi giá trị vào ô

Bây giờ chúng ta đã có workbook, hãy đưa một số vào ô **A1** của worksheet đầu tiên.

```csharp
// Step 2: Access cell A1 in the first worksheet
Cell cellA1 = workbook.Worksheets[0].Cells["A1"];

// Step 3: Insert a numeric value into the cell
cellA1.PutValue(123.456789);
```

*Why we use `PutValue`*: Phương thức này tự động phát hiện kiểu dữ liệu, vì vậy bạn không cần phải ép kiểu hoặc chuyển đổi thủ công. Nó cũng tôn trọng kiểu dáng hiện có của ô, điều này hữu ích khi bạn sau này **set cell number format**.

### Kiểm tra nhanh

Nếu bạn đọc lại ô, bạn sẽ thấy giá trị thô:

```csharp
double raw = cellA1.DoubleValue; // raw == 123.456789
```

Đó là số trước khi bất kỳ định dạng nào được áp dụng.

## Đặt định dạng số cho ô

Hiển thị một double thô với nhiều chữ thập phân không phải lúc nào cũng thân thiện với người dùng. Hãy giới hạn nó ở hai chữ số có nghĩa.

```csharp
// Step 4: Apply a style that formats the number with two significant digits
cellA1.SetStyle(new Style() { Number = 2 });
```

Thuộc tính `Number` tương ứng với các ID định dạng số tích hợp sẵn của Excel. `2` có nghĩa là “Number with two decimal places”. Nếu bạn cần một định dạng khác—ví dụ tiền tệ hoặc ngày tháng—bạn sẽ dùng một ID khác hoặc một chuỗi định dạng tùy chỉnh.

### Thay thế: Chuỗi định dạng tùy chỉnh

```csharp
Style customStyle = workbook.CreateStyle();
customStyle.Custom = "#,##0.00"; // forces two decimals with thousand separator
cellA1.SetStyle(customStyle);
```

*Why choose a custom style?* Nó cho bạn toàn quyền kiểm soát, đặc biệt khi các ID tích hợp sẵn không đáp ứng các cài đặt khu vực của bạn.

## Xác minh kết quả (Tùy chọn nhưng Được khuyến nghị)

Sau khi áp dụng kiểu, bạn có thể lưu workbook và mở nó trong Excel để xác nhận giao diện.

```csharp
// Save the workbook to a file
workbook.Save("FormattedWorkbook.xlsx");

// Or, for quick verification in code:
string displayed = cellA1.StringValue; // "123.46"
Console.WriteLine($"Displayed value: {displayed}");
```

Bạn sẽ thấy **123.46** trong ô A1—đúng hai chữ số thập phân, nhờ định dạng chúng ta đã đặt.

---

### Ví dụ làm việc đầy đủ

Kết hợp tất cả lại, đây là một chương trình tự chứa mà bạn có thể sao chép‑dán vào một ứng dụng console.

```csharp
using System;
using Aspose.Cells;   // Ensure you have the Aspose.Cells NuGet package

class Program
{
    static void Main()
    {
        // Initialize the workbook
        Workbook workbook = new Workbook();

        // Access the first worksheet and cell A1
        Cell cellA1 = workbook.Worksheets[0].Cells["A1"];

        // Write a numeric value
        cellA1.PutValue(123.456789);

        // Apply a two‑decimal number format
        cellA1.SetStyle(new Style() { Number = 2 });

        // Save to disk (optional)
        workbook.Save("FormattedWorkbook.xlsx");

        // Output the displayed text for verification
        Console.WriteLine($"Cell A1 shows: {cellA1.StringValue}");
    }
}
```

**Kết quả mong đợi khi bạn chạy chương trình:**

```
Cell A1 shows: 123.46
```

Mở `FormattedWorkbook.xlsx` trong Excel và bạn sẽ thấy cùng một giá trị đã được định dạng.

---

## Các biến thể phổ biến & Trường hợp đặc biệt

### 1. Các định dạng số khác nhau

| Mục tiêu | Format ID | Đoạn mã |
|------|-----------|--------------|
| Tiền tệ (hai chữ thập phân) | 5 | `cellA1.SetStyle(new Style() { Number = 5 });` |
| Phần trăm (không thập phân) | 10 | `cellA1.SetStyle(new Style() { Number = 10 });` |
| Ký hiệu khoa học | 11 | `cellA1.SetStyle(new Style() { Number = 11 });` |

Nếu không có ID tích hợp sẵn nào phù hợp, hãy quay lại sử dụng chuỗi tùy chỉnh như đã trình bày ở trên.

### 2. Dấu phân cách thập phân theo khu vực

Một số địa phương sử dụng dấu phẩy cho phần thập phân. Bạn có thể buộc định dạng nhận thức khu vực:

```csharp
Style cultureStyle = workbook.CreateStyle();
cultureStyle.Custom = "#,##0.00"; // works for most European locales
cellA1.SetStyle(cultureStyle);
```

### 3. Ghi văn bản thay vì số

Khi bạn cần **cách ghi ô** với một chuỗi, chỉ cần truyền một chuỗi vào `PutValue`:

```csharp
cellA1.PutValue("Total Revenue");
```

Không cần định dạng số, nhưng bạn vẫn có thể áp dụng kiểu font.

### 4. Dữ liệu lớn

Nếu bạn đang điền hàng ngàn dòng, việc chèn theo lô (`Cells.ImportArray`) nhanh hơn so với vòng lặp `PutValue`. Cách định dạng vẫn giữ nguyên; bạn chỉ cần áp dụng kiểu cho một phạm vi:

```csharp
Range range = workbook.Worksheets[0].Cells.CreateRange("B2:B1001");
range.ApplyStyle(new Style() { Number = 2 });
```

---

## Câu hỏi thường gặp

**Q: Điều này có hoạt động với .NET Core không?**  
A: Hoàn toàn có. Aspose.Cells hỗ trợ .NET Standard 2.0 và các phiên bản sau, vì vậy bạn có thể nhắm mục tiêu .NET 5, .NET 6 hoặc .NET 7 mà không cần thay đổi.

**Q: Nếu tôi cần nhiều hơn hai chữ số thập phân thì sao?**  
A: Thay đổi thuộc tính `Number` thành ID tích hợp sẵn phù hợp (ví dụ, `3` cho ba chữ thập phân) hoặc chỉnh sửa chuỗi định dạng tùy chỉnh (`"#,##0.000"`).

**Q: Tôi có thể áp dụng định dạng cho toàn bộ cột một lúc không?**  
A: Có. Sử dụng `Cells["A:A"]` để lấy toàn bộ cột rồi gọi `SetStyle`.

## Kết luận

Bạn giờ đã biết **cách tạo workbook** trong C#, **ghi giá trị vào ô**, và **đặt định dạng số cho ô** sao cho các số hiển thị chính xác như mong muốn. Khi nắm vững những kiến thức cơ bản này, bạn sẽ có khả năng tạo ra các báo cáo Excel, hoá đơn hoặc xuất dữ liệu chuyên nghiệp với ít công sức.

Tiếp theo, bạn có thể khám phá **định dạng số ô** cho ngày tháng, phần trăm hoặc định dạng có điều kiện—mỗi mục đều dựa trên các nguyên tắc đã đề cập. Hãy tìm hiểu tài liệu Aspose.Cells để biết thêm các tùy chọn styling sâu hơn, hoặc thử kết hợp nhiều worksheet vào một workbook duy nhất để có báo cáo phong phú hơn.

Chúc lập trình vui vẻ, và nhớ: một bảng tính được định dạng tốt chỉ là

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}