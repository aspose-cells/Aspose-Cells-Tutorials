---
category: general
date: 2026-02-14
description: Tạo mẫu giảm giá nhanh chóng và học cách áp dụng giảm giá trong bảng
  tính, chèn dữ liệu vào mẫu, và định nghĩa tiền tố biến cho các dấu thông minh.
draft: false
keywords:
- create discount template
- apply discount in spreadsheet
- inject data into template
- define variable prefix
language: vi
og_description: Tạo mẫu giảm giá bằng C#. Học cách áp dụng giảm giá trong bảng tính,
  chèn dữ liệu vào mẫu và định nghĩa tiền tố biến cho các smart marker.
og_title: Tạo mẫu giảm giá – Hướng dẫn đầy đủ C#
tags:
- C#
- SmartMarker
- Spreadsheet Automation
title: Tạo mẫu giảm giá trong C# – Hướng dẫn từng bước
url: /vi/net/smart-markers-dynamic-data/create-discount-template-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Mẫu Giảm Giá – Hướng Dẫn Toàn Diện C#

Bạn đã bao giờ cần **tạo mẫu giảm giá** cho một báo cáo bán hàng nhưng không chắc cách đưa các con số vào bảng tính một cách tự động? Bạn không cô đơn. Trong hướng dẫn này, chúng tôi sẽ chỉ cho bạn cách **tạo mẫu giảm giá**, sau đó **áp dụng giảm giá trong các ô bảng tính**, **chèn dữ liệu vào mẫu**, và thậm chí **định nghĩa tiền tố biến** cho các smart marker—tất cả bằng mã C# sạch sẽ.

Chúng ta sẽ bắt đầu bằng cách mô tả vấn đề, rồi ngay lập tức chuyển sang một giải pháp hoạt động mà bạn có thể sao chép‑dán. Khi kết thúc, bạn sẽ có một mẫu có thể tái sử dụng cho việc tạo hoá đơn, bảng giá, hoặc bất kỳ bảng tính nào cần giảm giá động.

---

## Những Điều Bạn Sẽ Học

- Cách thiết kế một mẫu bảng tính có khả năng áp dụng giảm giá.
- Cách cấu hình `VariablePrefix` / `VariableSuffix` tùy chỉnh để các marker dễ nhận biết.
- Cách truyền một đối tượng ẩn danh (`discountData`) vào `SmartMarkerProcessor`.
- Cách công thức kết quả (`=IF(#Discount#>0, A1*(1-#Discount#), A1)`) tự động tính giá cuối cùng.
- Mẹo xử lý các trường hợp đặc biệt như hàng không giảm giá hoặc nhiều mức giảm giá.

**Yêu cầu trước** – một runtime .NET mới (≥ .NET 6), tham chiếu tới thư viện `Aspose.Cells` (hoặc tương tự) cung cấp `SmartMarkerProcessor`, và hiểu biết cơ bản về cú pháp C#. Không có gì phức tạp.

---

## Bước 1: Tạo Mẫu Giảm Giá trong Bảng Tính

Đầu tiên, mở một workbook mới (hoặc sử dụng workbook hiện có) và đặt một placeholder nơi sẽ áp dụng giảm giá. Hãy nghĩ mẫu này như một file Excel thuần với các “smart marker” mà bộ xử lý sẽ thay thế.

```csharp
using Aspose.Cells;          // SmartMarkerProcessor lives here
using System;

// Step 1: Load or create a workbook
Workbook wb = new Workbook();               // creates an empty .xlsx in memory
Worksheet ws = wb.Worksheets[0];
ws.Name = "Pricing";

// Put a header
ws.Cells["A1"].PutValue("Original Price");
ws.Cells["B1"].PutValue("Discounted Price");

// Sample data row – the formula will be injected later
ws.Cells["A2"].PutValue(100);               // original price = 100
ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";
```

**Tại sao điều này quan trọng:** Bằng cách nhúng `#Discount#` vào công thức, chúng ta cho bộ xử lý biết chính xác vị trí cần chèn giá trị giảm giá. `SmartMarkerProcessor` sẽ thay thế `#Discount#` bằng số bạn cung cấp sau này, trong khi phần còn lại của công thức vẫn giữ nguyên.

---

## Bước 2: Định Nghĩa Tiền Tố Biến cho Smart Markers

Mặc định, nhiều thư viện tìm kiếm `${Variable}` hoặc `{{Variable}}`. Trong trường hợp của chúng ta, chúng ta muốn một marker ngắn gọn, dễ đọc, vì vậy **định nghĩa tiền tố và hậu tố biến** một cách rõ ràng.

```csharp
// Step 2: Configure how markers are identified
var smartMarkerOptions = new SmartMarkerOptions
{
    VariablePrefix = "#",   // start marker
    VariableSuffix = "#"    // end marker
};
```

**Mẹo chuyên nghiệp:** Sử dụng `#` giúp các marker ngắn gọn và dễ nhận thấy trong thanh công thức của Excel. Nếu bạn cần tránh xung đột với các hàm Excel hiện có, hãy chọn một cặp khác (ví dụ `[[` và `]]`).

---

## Bước 3: Chèn Dữ Liệu vào Mẫu bằng SmartMarkerProcessor

Bây giờ chúng ta đưa giá trị giảm giá thực tế vào. Bộ xử lý sẽ quét toàn bộ worksheet, tìm mọi `#Discount#`, và thay thế bằng giá trị từ đối tượng ẩn danh mà chúng ta truyền vào.

```csharp
// Step 3: Prepare the data that will be injected
var discountData = new { Discount = 0.10, Total = 100 };

// Run the processor – it mutates the workbook in‑place
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);
```

Sau lệnh này, công thức trong `B2` sẽ trở thành:

```
=IF(0.1>0, A2*(1-0.1), A2)
```

Khi workbook tính toán, `B2` hiển thị **90**, tức là đã áp dụng giảm giá 10 % cho giá gốc 100.

**Tại sao nó hoạt động:** `StartSmartMarkerProcessing` duyệt qua mọi ô, tìm token `#Discount#`, và thay thế bằng giá trị số. Vì token nằm trong một câu lệnh `IF`, bảng tính vẫn xử lý được trường hợp giảm giá bằng 0.

---

## Bước 4: Áp Dụng Giảm Giá trong Bảng Tính – Kiểm Tra Kết Quả

Hãy kích hoạt tính toán và in giá cuối cùng ra console. Bước này chứng minh quy trình **áp dụng giảm giá trong bảng tính** đã thành công.

```csharp
// Step 4: Force calculation and read the result
wb.CalculateFormula();                     // ensures all formulas are up‑to‑date
double discountedPrice = ws.Cells["B2"].DoubleValue;

Console.WriteLine($"Original: {ws.Cells["A2"].DoubleValue}");
Console.WriteLine($"Discounted (10%): {discountedPrice}");
```

**Kết quả mong đợi**

```
Original: 100
Discounted (10%): 90
```

Nếu bạn thay `discountData.Discount` thành `0.25` và chạy lại bộ xử lý, kết quả sẽ tự động phản ánh giảm giá 25 %—không cần thêm mã nào.

---

## Bước 5: Xử Lý Các Trường Hợp Đặc Biệt & Nhiều Giảm Giá

### Hàng Không Giảm Giá

Đôi khi một sản phẩm không được giảm giá. Để công thức luôn ổn định, `IF` bạn đã đặt ở trên đã bao phủ trường hợp này: khi `#Discount#` bằng `0`, giá gốc sẽ được giữ nguyên.

```csharp
var noDiscountData = new { Discount = 0.0 };
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(noDiscountData, smartMarkerOptions);
wb.CalculateFormula();
Console.WriteLine($"No discount applied: {ws.Cells["B2"].DoubleValue}");
```

### Nhiều Cột Giảm Giá

Nếu bạn cần các mức giảm giá riêng cho từng hàng, hãy tạo marker riêng cho mỗi hàng, ví dụ `#Discount1#`, `#Discount2#`, và truyền một collection:

```csharp
var multiDiscountData = new[]
{
    new { Discount = 0.05 },   // row 2
    new { Discount = 0.15 }    // row 3
};

ws.SmartMarkerProcessor.StartSmartMarkerProcessing(multiDiscountData, smartMarkerOptions);
```

Bộ xử lý sẽ khớp các marker theo thứ tự, vì vậy mỗi hàng sẽ nhận được giá trị đúng.

---

## Ví Dụ Hoàn Chỉnh

Dưới đây là chương trình đầy đủ, sẵn sàng sao chép, bao gồm mọi bước ở trên. Lưu lại dưới tên `Program.cs`, thêm tham chiếu tới `Aspose.Cells`, và chạy.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook & template
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Pricing";
        ws.Cells["A1"].PutValue("Original Price");
        ws.Cells["B1"].PutValue("Discounted Price");
        ws.Cells["A2"].PutValue(100);
        ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";

        // 2️⃣ Define marker delimiters
        var smartMarkerOptions = new SmartMarkerOptions
        {
            VariablePrefix = "#",
            VariableSuffix = "#"
        };

        // 3️⃣ Inject a 10 % discount
        var discountData = new { Discount = 0.10 };
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);

        // 4️⃣ Calculate and display result
        wb.CalculateFormula();
        double original = ws.Cells["A2"].DoubleValue;
        double discounted = ws.Cells["B2"].DoubleValue;

        Console.WriteLine($"Original: {original}");
        Console.WriteLine($"Discounted (10%): {discounted}");

        // Optional: Save the workbook to verify manually
        wb.Save("DiscountedPricing.xlsx");
    }
}
```

Chạy chương trình sẽ in ra các số mong đợi và tạo ra file `DiscountedPricing.xlsx` mà bạn có thể mở trong Excel để xem công thức đã được giải quyết.

---

## Kết Luận

Bây giờ bạn đã biết cách **tạo mẫu giảm giá**, **áp dụng giảm giá trong bảng tính**, **chèn dữ liệu vào mẫu**, và **định nghĩa tiền tố biến** cho smart markers—tất cả chỉ với một vài dòng C# ngắn gọn. Mẫu này có thể mở rộng—chỉ cần thay đổi đối tượng ẩn danh hoặc truyền một collection để cập nhật hàng loạt, và cùng một mẫu sẽ xử lý mọi kịch bản giảm giá bạn đưa ra.

Sẵn sàng lên cấp độ tiếp theo? Hãy thử:

- Thêm tính toán thuế song hành với giảm giá.
- Lấy phần trăm giảm giá từ cơ sở dữ liệu thay vì hard‑code.
- Sử dụng conditional formatting để làm nổi bật các hàng có mức giảm cao.

Những mở rộng này giữ nguyên ý tưởng cốt lõi trong khi tăng tính hữu dụng của mẫu giảm giá.

Có câu hỏi hoặc muốn chia sẻ trường hợp sử dụng thú vị? Để lại bình luận bên dưới, và chúc bạn lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}