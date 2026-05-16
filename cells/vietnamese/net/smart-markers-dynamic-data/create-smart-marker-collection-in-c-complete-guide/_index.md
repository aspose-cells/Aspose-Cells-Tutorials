---
category: general
date: 2026-02-23
description: Tạo bộ sưu tập smart marker nhanh chóng và học cách định nghĩa biến giảm
  giá cho các công thức động. Ví dụ C# từng bước với mã đầy đủ.
draft: false
keywords:
- create smart marker collection
- define discount variable
- smart markers Aspose.Cells
- worksheet formulas C#
- dynamic discount calculation
language: vi
og_description: Tạo bộ sưu tập smart marker trong C# và định nghĩa biến discount cho
  các công thức Excel động. Tìm hiểu giải pháp hoàn chỉnh, có thể chạy được.
og_title: Tạo Bộ Sưu Tập Smart Marker – Hướng Dẫn C# Đầy Đủ
tags:
- C#
- Aspose.Cells
- Excel automation
title: Tạo Bộ Sưu Tập Smart Marker trong C# – Hướng Dẫn Toàn Diện
url: /vi/net/smart-markers-dynamic-data/create-smart-marker-collection-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Bộ Sưu Tập Smart Marker – Hướng Dẫn Đầy Đủ C#

Bạn đã bao giờ cần **create smart marker collection** trong một bảng tính nhưng không chắc bắt đầu từ đâu chưa? Bạn không phải là người duy nhất—nhiều nhà phát triển gặp cùng một rào cản khi họ cố gắng chèn các biến và công thức vào một worksheet Excel một cách lập trình.  

Tin tốt? Trong hướng dẫn này, chúng tôi sẽ chỉ cho bạn cách **create smart marker collection** và cũng **define discount variable** để các ô của bạn tính giảm giá ngay lập tức. Khi kết thúc, bạn sẽ có một mẫu C# sẵn sàng chạy mà bạn có thể đưa vào bất kỳ dự án Aspose.Cells nào.

## Nội Dung Hướng Dẫn Này

Chúng tôi sẽ hướng dẫn từng bước—từ việc khởi tạo `MarkerCollection` đến việc áp dụng nó trên một worksheet. Bạn sẽ thấy tại sao mỗi dòng lại quan trọng, cách xử lý các trường hợp đặc biệt như nhiều biến, và bảng tính kết quả trông như thế nào. Không cần tài liệu bên ngoài; mọi thứ bạn cần đều có ở đây.  

Yêu cầu trước là tối thiểu: một runtime .NET mới (khuyến nghị 5.0+) và thư viện Aspose.Cells cho .NET được cài đặt qua NuGet. Nếu bạn đã làm việc với C# trước đây, bạn sẽ nhanh chóng nắm bắt.

---

## Bước 1: Thiết Lập Dự Án và Thêm Aspose.Cells

### Tại sao bước này quan trọng  
Trước khi bạn có thể **create smart marker collection**, bạn cần một đối tượng workbook mà các marker sẽ nhắm tới. Aspose.Cells cung cấp các lớp `Workbook` và `Worksheet` giúp việc này trở nên dễ dàng.

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Initialize a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
```

> **Mẹo:** Nếu bạn đang sử dụng .NET Core, hãy thêm gói bằng  
> `dotnet add package Aspose.Cells` trước khi biên dịch.

### Kết quả mong đợi  
Tại thời điểm này, bạn đã có một worksheet trống (`ws`) sẵn sàng nhận các marker.

---

## Bước 2: Tạo Smart Marker Collection

### Tại sao bước này quan trọng  
`MarkerCollection` là container chứa mọi biến và marker công thức. Hãy nghĩ nó như một “túi các placeholder” mà Aspose.Cells sẽ thay thế bằng giá trị thực sau này.

```csharp
        // Step 2: Create a collection to hold smart markers
        MarkerCollection markerCollection = new MarkerCollection();
```

Bây giờ bạn đã **created smart marker collection**—nền tảng cho mọi nội dung động tiếp theo.

---

## Bước 3: Định Nghĩa Biến Discount

### Tại sao bước này quan trọng  
Định nghĩa một biến cho phép bạn tái sử dụng cùng một giá trị trong nhiều công thức. Ở đây chúng tôi **define discount variable** là `0.1` (tức 10 %). Nếu mức giảm giá thay đổi, bạn chỉ cần cập nhật một mục.

```csharp
        // Step 3: Define a variable marker for Discount (value 0.1)
        markerCollection.Add("var:Discount", "0.1");
```

> **Nếu discount là động?**  
> Bạn có thể thay thế `"0.1"` bằng bất kỳ chuỗi đại diện cho số thập phân nào, hoặc thậm chí lấy nó từ cơ sở dữ liệu trước khi thêm marker.

---

## Bước 4: Thêm Formula Marker Sử Dụng Biến

### Tại sao bước này quan trọng  
Formula markers cho phép bạn nhúng công thức Excel tham chiếu tới các biến của bạn. Trong ví dụ này, ô `A1` sẽ tính `B1 * (1 - Discount)`.

```csharp
        // Step 4: Define a formula marker that uses the Discount variable
        markerCollection.Add("A1", "=B1*(1-{{var:Discount}})");
```

Khi Aspose.Cells xử lý collection, nó sẽ thay thế `{{var:Discount}}` bằng `0.1`, tạo ra công thức cuối cùng `=B1*(1-0.1)`.

---

## Bước 5: Gắn Collection vào Worksheet

### Tại sao bước này quan trọng  
Việc gắn cho worksheet biết marker nào thuộc về nó. Nếu không có liên kết này, lời gọi `Apply` sẽ không có gì để xử lý.

```csharp
        // Step 5: Attach the marker collection to the worksheet's SmartMarkers
        ws.SmartMarkers.Add(markerCollection);
```

---

## Bước 6: Điền Dữ Liệu vào Worksheet và Áp Dụng Markers

### Tại sao bước này quan trọng  
Chúng ta cần ít nhất một giá trị đầu vào cho `B1` để công thức có thể tạo ra kết quả. Sau khi đặt `B1`, chúng ta gọi `Apply()` để Aspose.Cells thay thế các marker và tính toán công thức.

```csharp
        // Provide a base price in B1 (e.g., $100)
        ws.Cells["B1"].PutValue(100);

        // Step 6: Apply the smart markers to populate the worksheet cells
        ws.SmartMarkers.Apply();

        // Save the workbook to verify the outcome
        wb.Save("SmartMarkerResult.xlsx");
    }
}
```

### Kết quả mong đợi
- Ô **B1** chứa `100`.
- Ô **A1** chứa công thức `=B1*(1-0.1)`.
- Giá trị tính được trong **A1** là `90` (tức là đã áp dụng giảm giá 10 %).

Mở `SmartMarkerResult.xlsx` và bạn sẽ thấy giảm giá đã được áp dụng—không cần chỉnh sửa thủ công.

---

## Xử Lý Nhiều Biến và Các Trường Hợp Đặc Biệt

### Thêm nhiều biến
Nếu bạn cần các tham số bổ sung, chỉ cần tiếp tục gọi `Add` với tiền tố `var:`:

```csharp
markerCollection.Add("var:TaxRate", "0.07"); // 7 % tax
markerCollection.Add("B2", "=A1*(1+{{var:TaxRate}})"); // Total with tax
```

### Quy tắc đặt tên biến
- Chỉ sử dụng ký tự chữ và số cùng dấu gạch dưới.
- Đặt tiền tố `var:` để thông báo cho Aspose.Cells đây là một biến, không phải tham chiếu ô.

### Nếu một biến bị thiếu thì sao?
Aspose.Cells sẽ để nguyên placeholder, điều này giúp bạn phát hiện các vấn đề cấu hình khi gỡ lỗi.

---

## Ví Dụ Hoàn Chỉnh (Tất Cả Các Bước Kết Hợp)

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Initialize workbook and worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Create the smart marker collection
        MarkerCollection markerCollection = new MarkerCollection();

        // Define discount variable (10 % discount)
        markerCollection.Add("var:Discount", "0.1");

        // Optional: define tax variable (7 % tax)
        markerCollection.Add("var:TaxRate", "0.07");

        // Formula for discounted price in A1
        markerCollection.Add("A1", "=B1*(1-{{var:Discount}})");

        // Formula for total price with tax in B2
        markerCollection.Add("B2", "=A1*(1+{{var:TaxRate}})");

        // Attach collection to worksheet
        ws.SmartMarkers.Add(markerCollection);

        // Input base price
        ws.Cells["B1"].PutValue(100); // $100

        // Apply markers and evaluate formulas
        ws.SmartMarkers.Apply();

        // Save the file
        wb.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook saved. Check SmartMarkerResult.xlsx.");
    }
}
```

Chạy chương trình này sẽ tạo ra một bảng tính với:

| Ô | Giá trị | Giải thích |
|------|-------|-------------|
| B1   | 100   | Giá gốc |
| A1   | 90    | Áp dụng giảm giá 10 % |
| B2   | 96.3  | Giá đã giảm + thuế 7 % |

---

## Câu Hỏi Thường Gặp & Trả Lời

**Hỏi: Điều này có hoạt động với các worksheet hiện có không?**  
**Đáp:** Hoàn toàn có. Bạn có thể tải một workbook hiện có (`new Workbook("template.xlsx")`) và sau đó áp dụng cùng một marker collection cho bất kỳ sheet nào.

**Hỏi: Tôi có thể sử dụng các hàm Excel phức tạp không?**  
**Đáp:** Có. Bất kỳ hàm nào Excel hỗ trợ—`VLOOKUP`, `IF`, `SUMIFS`—có thể được đặt trong một chuỗi marker. Chỉ cần nhớ escape dấu ngoặc nhọn nếu cần.

**Hỏi: Nếu tôi cần thay đổi discount tại thời gian chạy thì sao?**  
**Đáp:** Cập nhật biến trước khi gọi `Apply()`:  
```csharp
markerCollection["var:Discount"] = newDiscount.ToString();
ws.SmartMarkers.Apply();
```

**Hỏi: Có ảnh hưởng tới hiệu năng khi có nhiều marker không?**  
**Đáp:** Việc áp dụng markers có độ phức tạp O(N) với N là số lượng markers. Đối với hàng ngàn mục, cập nhật theo batch hoặc stream workbook có thể giảm mức sử dụng bộ nhớ.

---

## Kết Luận

Bây giờ bạn đã biết cách **create smart marker collection** trong C# và **define discount variable** để thực hiện các phép tính động trong một worksheet Excel. Ví dụ đầy đủ, có thể chạy này minh họa toàn bộ quy trình—từ việc thiết lập workbook đến lưu file cuối cùng với các công thức đã được tính toán.  

Sẵn sàng cho bước tiếp theo? Hãy thử thêm định dạng có điều kiện dựa trên giá đã giảm, hoặc lấy tỷ lệ giảm giá từ một file cấu hình JSON. Khám phá những biến thể này sẽ nâng cao khả năng sử dụng smart markers của Aspose.Cells và làm cho việc tự động hóa Excel của bạn thực sự linh hoạt.

Chúc lập trình vui vẻ, và hãy thoải mái thử nghiệm—không có giới hạn gì cho những gì bạn có thể tự động hóa với smart markers!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}