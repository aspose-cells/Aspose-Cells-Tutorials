---
category: general
date: 2026-02-14
description: Tạo đối tượng dữ liệu master trong C# và tạo bảng chi tiết một cách dễ
  dàng. Học quy trình SmartMarker đầy đủ với các ví dụ mã thực tế.
draft: false
keywords:
- create master data object
- generate detail sheet
- smartmarker processing
- worksheet automation
- c# data binding
language: vi
og_description: Tạo đối tượng dữ liệu master trong C# và tạo bảng chi tiết bằng SmartMarker.
  Tham khảo hướng dẫn chi tiết của chúng tôi để có giải pháp sẵn sàng chạy.
og_title: Tạo Đối Tượng Dữ Liệu Chủ – Hướng Dẫn Toàn Diện
tags:
- C#
- SmartMarker
- Excel Automation
title: Tạo Đối tượng Dữ liệu Chủ – Hướng dẫn Từng bước để Tạo Bảng Chi tiết
url: /vi/net/smart-markers-dynamic-data/create-master-data-object-step-by-step-guide-to-generate-det/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Đối Tượng Dữ Liệu Master – Hướng Dẫn Toàn Diện

Bạn đã bao giờ cần **tạo đối tượng dữ liệu master** cho một bảng tính Excel nhưng không chắc cách kết nối nó với một sheet chi tiết SmartMarker? Bạn không phải là người duy nhất. Trong nhiều kịch bản báo cáo, đối tượng master điều khiển một sheet chi tiết động, và việc thiết lập đúng có thể giống như lắp ráp một câu đố mà không có hình ảnh mẫu.  

Trong hướng dẫn này, chúng ta sẽ đi qua toàn bộ quy trình — xây dựng đối tượng dữ liệu master, cấu hình các tùy chọn SmartMarker để **tạo sheet chi tiết**, và cuối cùng kích hoạt bộ xử lý. Khi hoàn thành, bạn sẽ có một đoạn mã có thể chạy được để dán vào bất kỳ dự án .NET nào sử dụng thư viện GrapeCity Documents for Excel (GcExcel).

## Những Gì Bạn Cần Chuẩn Bị

- .NET 6+ (hoặc .NET Framework 4.7.2) với tham chiếu tới `GcExcel.dll`
- Kiến thức cơ bản về C# (biến, kiểu ẩn danh, khởi tạo đối tượng)
- Một workbook Excel đã chứa các thẻ SmartMarker như `{{OrderId}}` và một bảng cho các mục hàng
- Visual Studio, Rider, hoặc bất kỳ trình soạn thảo nào bạn thích

Đó là tất cả — không cần thêm gói NuGet nào ngoài bản phân phối cốt lõi của GcExcel.

## Bước 1: Tạo Đối Tượng Dữ Liệu Master

Điều đầu tiên bạn phải làm là **tạo đối tượng dữ liệu master** sao cho phản ánh cấu trúc mà các thẻ SmartMarker mong đợi. Hãy nghĩ nó như một mô hình báo cáo nhỏ trong bộ nhớ.

```csharp
// Step 1: Build the master data object that feeds the SmartMarkers.
// It contains an OrderId and a collection of line items.
var orderData = new
{
    OrderId = 1,
    Items = new[]
    {
        new { Product = "A", Quantity = 2 },
        new { Product = "B", Quantity = 5 }
    }
};
```

Tại sao lại dùng kiểu ẩn danh ở đây? Vì nó cho phép bạn định nghĩa một container nhẹ mà không cần khai báo một lớp đầy đủ — rất phù hợp cho các demo nhanh hoặc khi cấu trúc dữ liệu không có khả năng thay đổi. Nếu sau này bạn cần một mô hình có thể tái sử dụng, chỉ cần thay `var` bằng một POCO thích hợp.

> **Mẹo chuyên nghiệp:** Giữ tên thuộc tính (`OrderId`, `Product`, `Quantity`) giống hệt các placeholder trong worksheet của bạn; SmartMarker sẽ so khớp chúng mà không phân biệt chữ hoa/chữ thường.

## Bước 2: Cấu Hình Tùy Chọn SmartMarker Để Tạo Sheet Chi Tiết

Bây giờ chúng ta thông báo cho SmartMarker rằng muốn một worksheet riêng cho bảng mục hàng. Đây là nơi từ khóa **generate detail sheet** phát huy tác dụng.

```csharp
// Step 2: Set up SmartMarker options.
// Enabling DetailSheet creates a new sheet for each master record.
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheet = true,
    // The new sheet will be named using the OrderId value.
    DetailSheetNewName = "Order_{OrderId}"
};
```

Mẫu `DetailSheetNewName` sử dụng các placeholder trong dấu ngoặc nhọn sẽ được thay thế tại thời gian chạy. Trong ví dụ của chúng ta, sheet sẽ được đặt tên là `Order_1`. Nếu bạn lặp lại nhiều đơn hàng, mỗi đơn sẽ có một tab riêng — đúng như những gì các kế toán thường mong đợi.

## Bước 3: Chạy Bộ Xử Lý SmartMarker

Khi dữ liệu và tùy chọn đã sẵn sàng, bước cuối cùng là gọi bộ xử lý trên worksheet mục tiêu.

```csharp
// Step 3: Execute SmartMarker processing on the worksheet.
// 'worksheet' is an IWorksheet instance that points to the template sheet.
worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);
```

Trong nền, SmartMarker sẽ quét worksheet để tìm các thẻ, chèn giá trị `orderData`, và vì `DetailSheet` được đặt là `true`, nó sẽ sao chép mẫu vào một sheet mới có tên `Order_1`. Tất cả các mục hàng sẽ xuất hiện trong khu vực chi tiết, giữ nguyên mọi định dạng bạn đã áp dụng trong mẫu.

### Ví Dụ Hoàn Chỉnh Hoạt Động

Dưới đây là một chương trình console tự chứa, mở một workbook mẫu (`Template.xlsx`), thực hiện ba bước, và lưu kết quả thành `Result.xlsx`. Bạn có thể sao chép‑dán đoạn này vào một dự án console mới và nhấn **F5**.

```csharp
using System;
using GrapeCity.Documents.Excel;

class Program
{
    static void Main()
    {
        // Load the Excel template that contains SmartMarker tags.
        var workbook = new Workbook();
        workbook.Open("Template.xlsx");

        // -------------------------------------------------
        // Step 1: Create the master data object.
        // -------------------------------------------------
        var orderData = new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Product = "A", Quantity = 2 },
                new { Product = "B", Quantity = 5 }
            }
        };

        // -------------------------------------------------
        // Step 2: Configure SmartMarker options to generate detail sheet.
        // -------------------------------------------------
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheet = true,
            DetailSheetNewName = "Order_{OrderId}"
        };

        // -------------------------------------------------
        // Step 3: Process the worksheet.
        // -------------------------------------------------
        // Assume the first sheet holds the master template.
        var worksheet = workbook.Worksheets[0];
        worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);

        // Save the populated workbook.
        workbook.Save("Result.xlsx");
        Console.WriteLine("Done! Check Result.xlsx – a new sheet named Order_1 should exist.");
    }
}
```

#### Kết Quả Dự Kiến

- **Result.xlsx** chứa một sheet có tên `Order_1`.
- Ô `A1` (hoặc bất kỳ ô nào bạn đặt `{{OrderId}}`) hiện hiển thị `1`.
- Một bảng bắt đầu tại khối SmartMarker liệt kê hai dòng:
  | Product | Quantity |
  |---------|----------|
  | A       | 2        |
  | B       | 5        |

Nếu bạn mở file, sẽ thấy định dạng từ mẫu được giữ nguyên — viền, phông chữ, định dạng có điều kiện — tất cả vẫn nguyên vẹn.

## Các Câu Hỏi Thường Gặp & Trường Hợp Đặc Biệt

### Nếu tôi có nhiều đơn hàng thì sao?

Bao bọc đối tượng master trong một collection và để SmartMarker tự động lặp lại:

```csharp
var orders = new[]
{
    new {
        OrderId = 1,
        Items = new[] { new { Product = "A", Quantity = 2 } }
    },
    new {
        OrderId = 2,
        Items = new[] { new { Product = "C", Quantity = 3 } }
    }
};

worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);
```

Mỗi đơn hàng sẽ sinh ra một sheet riêng (`Order_1`, `Order_2`, …). Bộ xử lý sẽ xem mảng bên ngoài như là collection master.

### Làm sao kiểm soát vị trí của sheet?

Đặt `smartMarkerOptions.DetailSheetInsertIndex = 2;` để đặt sheet mới sau tab thứ hai, hoặc dùng `DetailSheetInsertAfter = "Summary"` để chèn sau một sheet có tên cụ thể.

### Có thể tắt việc tạo sheet chi tiết cho một lần chạy nhất định không?

Chỉ cần chuyển `DetailSheet = false;`. Khi đó SmartMarker sẽ ghi các mục hàng vào cùng sheet chứa các thẻ master.

### Còn dữ liệu lớn thì sao?

SmartMarker truyền dữ liệu một cách hiệu quả, nhưng nếu bạn vượt quá vài trăm ngàn hàng, có thể gặp giới hạn 1.048.576 hàng của Excel. Trong trường hợp đó, hãy chia dữ liệu thành nhiều bản ghi master hoặc cân nhắc xuất ra CSV.

## Tổng Quan Trực Quan

![Sơ đồ minh họa cách tạo đối tượng dữ liệu master và tạo sheet chi tiết bằng SmartMarker](/images/smartmarker-flow.png)

*Hình minh họa cho thấy luồng từ đối tượng master C# → tùy chọn SmartMarker → xử lý worksheet → sheet chi tiết mới.*

## Kết Luận

Bây giờ bạn đã biết cách **tạo đối tượng dữ liệu master** trong C# và cấu hình SmartMarker để **tự động tạo sheet chi tiết**. Mô hình ba bước — dữ liệu, tùy chọn, bộ xử lý — bao phủ phần lớn các kịch bản tự động hoá Excel với GcExcel.  

Từ đây, bạn có thể khám phá:

- Thêm dữ liệu header/footer cho mỗi sheet chi tiết
- Sử dụng định dạng có điều kiện dựa trên trạng thái đơn hàng
- Xuất workbook đã tạo ra thành PDF bằng `workbook.SaveAsPdf(...)`

Hãy tự do thử nghiệm, phá vỡ và sau đó ghép lại. Đó là cách nhanh nhất để thành thạo tự động hoá worksheet. Chúc bạn lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}