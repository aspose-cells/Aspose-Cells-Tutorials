---
category: general
date: 2026-02-21
description: Lặp lại dữ liệu trong Excel nhanh chóng bằng SmartMarker—tìm hiểu cách
  điền mẫu Excel và lặp lại các hàng một cách dễ dàng.
draft: false
keywords:
- repeat data in excel
- populate excel template
- how to repeat rows
- repeat rows in excel
- populate excel from data
language: vi
og_description: Lặp lại dữ liệu trong Excel bằng SmartMarker. Tìm hiểu cách điền mẫu
  Excel, lặp lại các hàng và tự động hoá bảng tính của bạn.
og_title: Lặp dữ liệu trong Excel – Điền mẫu bằng SmartMarker
tags:
- excel
- csharp
- smartmarker
- automation
title: Lặp dữ liệu trong Excel – Điền mẫu bằng SmartMarker
url: /vi/net/smart-markers-dynamic-data/repeat-data-in-excel-populate-template-with-smartmarker/
---

answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lặp dữ liệu trong Excel – Đổ dữ liệu vào mẫu bằng SmartMarker

Bạn đã bao giờ cần **lặp dữ liệu trong Excel** nhưng không biết cách tránh việc sao chép‑dán thủ công? Bạn không phải là người duy nhất. Trong nhiều trường hợp báo cáo, bạn có một danh sách các mục cần mở rộng thành các hàng một cách tự động, và làm việc này bằng tay là công thức cho lỗi.

Điều quan trọng là—sử dụng **SmartMarkerProcessor** từ thư viện **GemBox.Spreadsheet** cho phép bạn **đổ một mẫu Excel** chỉ bằng một dòng C# và các hàng sẽ được lặp lại cho mỗi mục trong bộ sưu tập của bạn. Trong hướng dẫn này, chúng tôi sẽ đi qua các bước cụ thể, trình bày toàn bộ mã, và giải thích lý do mỗi phần quan trọng, để bạn có thể tự tin lặp các hàng trong Excel mà không gặp khó khăn.

## Những gì bạn sẽ học

* Cách định nghĩa cấu trúc dữ liệu điều khiển hoạt động lặp.  
* Cách gắn một `SmartMarkerProcessor` vào workbook chứa một sheet mẫu ẩn.  
* Cách marker `${Repeat:Item}` mở rộng thành nhiều hàng tự động.  
* Mẹo xử lý các trường hợp đặc biệt như bộ sưu tập rỗng hoặc định dạng tùy chỉnh.  

Khi kết thúc tutorial này, bạn sẽ có thể **đổ dữ liệu vào Excel** theo cách mở rộng, dễ bảo trì, và hoạt động với bất kỳ dự án .NET nào.

---

## Điều kiện tiên quyết

* .NET 6.0 trở lên (mã sử dụng các tính năng hiện đại của C#).  
* Gói NuGet **GemBox.Spreadsheet** (phiên bản miễn phí hỗ trợ tới 150 hàng).  
* Một file mẫu Excel cơ bản (`Template.xlsx`) với một sheet ẩn có tên `HiddenTemplate`.  
* Kiến thức cơ bản về đối tượng C# và LINQ là hữu ích nhưng không bắt buộc.

---

## Bước 1 – Định nghĩa cấu trúc dữ liệu lặp

Đầu tiên, bạn cần một nguồn dữ liệu mà engine SmartMarker có thể duyệt qua. Trong hầu hết các ứng dụng thực tế, dữ liệu này sẽ đến từ cơ sở dữ liệu, API, hoặc file CSV. Để minh họa, chúng ta sẽ dùng một kiểu ẩn danh với một thuộc tính duy nhất tên `Item` chứa một mảng các chuỗi.

```csharp
// Step 1: Define the data that will be repeated in the template
var repeatData = new { Item = new[] { "A", "B", "C" } };
```

> **Tại sao điều này quan trọng:** Marker `${Repeat:Item}` trong mẫu Excel tìm kiếm một thuộc tính có tên `Item`. Nếu bạn đổi tên thuộc tính, hãy cập nhật marker cho phù hợp. Sự liên kết chặt chẽ này đảm bảo mẫu luôn đồng bộ với mã, giúp **đổ mẫu Excel** mà không phải đoán tên cột.

### Các biến thể phổ biến

* **Đối tượng phức tạp:** Thay vì một mảng chuỗi đơn giản, bạn có thể cung cấp danh sách các đối tượng (`new[] { new { Name = "A", Qty = 10 } }`). Marker sẽ lặp các hàng và bạn có thể tham chiếu `${Item.Name}` và `${Item.Qty}` trong sheet.  
* **Bộ sưu tập rỗng:** Nếu `Item` rỗng, SmartMarker sẽ tự động loại bỏ khối lặp, để lại mẫu không thay đổi—rất hữu ích cho các phần tùy chọn.

---

## Bước 2 – Tạo SmartMarkerProcessor cho sheet mẫu ẩn

Tiếp theo, tải workbook và khởi tạo một `SmartMarkerProcessor`. Chỉ định nó tới workbook chứa sheet mẫu ẩn; SmartMarker sẽ sao chép sheet đó sang một sheet hiển thị và mở rộng các marker lặp.

```csharp
using GemBox.Spreadsheet;

// Load the workbook that holds the hidden template sheet.
var wb = ExcelFile.Load("Template.xlsx");

// Step 2: Create a SmartMarkerProcessor for the workbook that holds the hidden template sheet
var processor = new SmartMarkerProcessor(wb);
```

> **Mẹo chuyên nghiệp:** Nếu bạn có nhiều mẫu trong cùng một file, bạn có thể chỉ định tên sheet nguồn khi gọi `processor.Process`. Điều này hữu ích khi bạn cần **lặp các hàng trong Excel** cho các phần báo cáo khác nhau.

### Xử lý các trường hợp đặc biệt

* **Thiếu sheet mẫu:** Bao quanh quá trình tải bằng try/catch và ghi log lỗi rõ ràng—điều này ngăn việc thất bại im lặng khi đường dẫn file sai.  
* **Bộ dữ liệu lớn:** Đối với hàng ngàn dòng, cân nhắc stream kết quả ra file (`processor.Save`) thay vì giữ toàn bộ trong bộ nhớ.

---

## Bước 3 – Áp dụng dữ liệu và mở rộng marker `${Repeat:Item}`

Bây giờ là dòng lệnh “ma thuật” thực sự lặp các hàng. Gửi đối tượng bạn tạo ở Bước 1 cho `processor.Process`. SmartMarker sẽ tìm mọi marker `${Repeat:Item}`, sao chép hàng cho mỗi phần tử, và thay thế các placeholder bằng giá trị thực.

```csharp
// Step 3: Apply the data to the template, expanding the ${Repeat:Item} marker
processor.Process(repeatData);

// Save the resulting workbook.
wb.Save("Result.xlsx");
```

### Kết quả mong đợi

Khi mở `Result.xlsx`, sheet mẫu ẩn đã được sao chép sang một sheet hiển thị mới (mặc định tên `Sheet1`). Hàng chứa `${Repeat:Item}` bây giờ xuất hiện ba lần, với các ô hiển thị **A**, **B**, và **C** tương ứng.

| Item |
|------|
| A    |
| B    |
| C    |

Nếu bạn thêm các cột như `${Item.Price}`, chúng sẽ được tự động điền từ nguồn dữ liệu.

---

## Cách lặp các hàng trong Excel mà không dùng SmartMarker (so sánh nhanh)

| Cách tiếp cận          | Độ phức tạp mã | Bảo trì | Hiệu năng |
|------------------------|----------------|---------|-----------|
| Sao chép‑dán thủ công  | Cao            | Thấp    | Kém       |
| Macro VBA              | Trung bình     | Trung bình | Tốt   |
| **SmartMarkerProcessor**| Thấp           | Cao     | Xuất sắc  |

Như bạn thấy, việc sử dụng SmartMarker để **lặp dữ liệu trong Excel** mang lại sự tách biệt sạch sẽ nhất giữa thiết kế mẫu và logic nghiệp vụ. Nó cũng không phụ thuộc ngôn ngữ—các khái niệm tương tự tồn tại trong Java, Python và các thư viện JavaScript.

---

## Mẹo nâng cao & các lỗi thường gặp

### 1. Định dạng các hàng được lặp

SmartMarker sao chép toàn bộ hàng—bao gồm kiểu ô, viền, và định dạng có điều kiện. Nếu bạn cần kiểu khác cho hàng đầu hoặc cuối, hãy thêm các marker như `${If:Item.IsFirst}` và sử dụng công thức có điều kiện trong Excel.

### 2. Xử lý bộ dữ liệu lớn

Khi làm việc với > 10 000 hàng, tắt tính toán tự động của Excel trước khi xử lý:

```csharp
wb.WorkbookOptions = new WorkbookOptions { RecalculateAllFormulas = false };
```

Bật lại sau khi lưu để duy trì hiệu suất nhanh chóng.

### 3. Đổ dữ liệu Excel từ cơ sở dữ liệu thực

```csharp
var orders = dbContext.Orders
    .Where(o => o.Date >= start && o.Date <= end)
    .Select(o => new { o.OrderId, o.CustomerName, o.Total })
    .ToArray();

processor.Process(new { Order = orders });
```

Sau đó dùng `${Repeat:Order}` trong mẫu để liệt kê mọi đơn hàng. Mẫu này cho thấy cách dễ dàng **đổ dữ liệu vào Excel** trực tiếp từ Entity Framework.

### 4. Sử dụng nhiều khối lặp

Bạn có thể có nhiều marker `${Repeat:...}` trên cùng một sheet hoặc các sheet khác nhau. SmartMarker xử lý chúng tuần tự, vì vậy thứ tự chỉ quan trọng nếu một khối phụ thuộc vào kết quả của khối khác.

---

## Ví dụ hoàn chỉnh có thể chạy được

Dưới đây là một ứng dụng console tự chứa, bạn có thể dán vào Visual Studio và chạy ngay. Nó minh họa cả ba bước cùng với việc lưu file.

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License free version (up to 150 rows). For production use, set your license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Define the data to repeat.
        var repeatData = new { Item = new[] { "A", "B", "C" } };

        // 2️⃣ Load the template workbook (ensure Template.xlsx exists next to the exe).
        var wb = ExcelFile.Load("Template.xlsx");

        // Create processor bound to the workbook.
        var processor = new SmartMarkerProcessor(wb);

        // 3️⃣ Process the data – this expands the ${Repeat:Item} marker.
        processor.Process(repeatData);

        // Save the populated workbook.
        wb.Save("Result.xlsx");

        Console.WriteLine("Excel file generated successfully – check Result.xlsx");
    }
}
```

**Kết quả mong đợi:** `Result.xlsx` chứa một sheet trong đó hàng có `${Repeat:Item}` xuất hiện ba lần, hiển thị A, B và C. Không cần điều chỉnh thủ công nào.

---

## Kết luận

Bạn đã biết cách **lặp dữ liệu trong Excel** một cách hiệu quả bằng cách tận dụng SmartMarkerProcessor. Bằng cách định nghĩa một đối tượng dữ liệu đơn giản, tải workbook mẫu, và gọi `Process`, bạn có thể **đổ mẫu Excel**, **lặp các hàng trong Excel**, và nói chung **

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}