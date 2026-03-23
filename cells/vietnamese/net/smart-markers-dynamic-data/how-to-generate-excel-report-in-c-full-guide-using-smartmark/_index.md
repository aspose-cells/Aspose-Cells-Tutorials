---
category: general
date: 2026-03-22
description: Cách tạo báo cáo Excel trong C# với mẫu master‑detail. Học cách nhanh
  chóng điền dữ liệu vào mẫu Excel bằng C#, sử dụng SmartMarker cho các sheet lặp
  lại.
draft: false
keywords:
- how to generate excel report
- populate excel template c#
- excel smartmarker c#
- master detail excel c#
- c# excel automation
language: vi
og_description: Cách tạo báo cáo Excel trong C# bằng mẫu có thể tái sử dụng. Hướng
  dẫn chi tiết này chỉ cho bạn cách điền dữ liệu master‑detail vào mẫu Excel trong
  C#.
og_title: Cách tạo báo cáo Excel trong C# – Hướng dẫn chi tiết SmartMarker
tags:
- Excel
- C#
- SmartMarker
- Reporting
title: Cách tạo báo cáo Excel trong C# – Hướng dẫn đầy đủ sử dụng SmartMarker
url: /vi/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Tạo Báo Cáo Excel trong C# – Hướng Dẫn Toàn Diện Sử Dụng SmartMarker

Bạn đã bao giờ tự hỏi **cách tạo báo cáo Excel** trong C# mà không phải viết mã lặp lại từng ô? Bạn không phải là người duy nhất. Hầu hết các lập trình viên gặp khó khăn khi cần một báo cáo đa trang, đa sheet, phản ánh mối quan hệ master‑detail—ví dụ đơn hàng và các mục chi tiết—nhưng không muốn tự xây dựng lại từ đầu mỗi lần.

Tin tốt? Với một mẫu Excel đã chuẩn bị sẵn và engine **SmartMarker** của Aspose.Cells, bạn có thể **populate Excel template C#** chỉ trong vài dòng mã. Trong tutorial này, chúng ta sẽ đi qua một kịch bản thực tế, giải thích lý do mỗi bước quan trọng, và cung cấp một ví dụ hoàn chỉnh, có thể chạy ngay mà bạn chỉ cần copy‑paste.

> **Bạn sẽ nhận được:** một báo cáo Excel master‑detail, trong đó mỗi đơn hàng tạo ra một worksheet riêng, toàn bộ được điều khiển bằng các đối tượng C# đơn giản. Không cần vòng lặp thủ công qua các ô, không có công thức dễ vỡ—chỉ là mã sạch, dễ bảo trì.

---

## Prerequisites

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có:

- **.NET 6.0** (hoặc mới hơn) đã được cài đặt – mã nguồn nhắm tới .NET 6 nhưng cũng hoạt động trên .NET Framework 4.7+.
- Gói NuGet **Aspose.Cells for .NET** (`Install-Package Aspose.Cells`) – cung cấp các lớp `Workbook`, `SmartMarkerProcessor`, và các lớp liên quan.
- Một file Excel tên **MasterDetailTemplate.xlsx** đặt trong `YOUR_DIRECTORY`. File này cần chứa một khối SmartMarker như `{{Orders.OrderId}}` ở sheet đầu tiên và một khối lồng nhau `{{Orders.Items.Prod}}` cho các mục chi tiết.
- Kiến thức cơ bản về kiểu ẩn danh C# – chúng ta sẽ dùng chúng để mô hình hoá đơn hàng và các mục.

Nếu bất kỳ mục nào trên còn lạ, đừng lo. Chúng tôi sẽ đề cập đến các lựa chọn thay thế (ví dụ: dùng EPPlus) ở phần sau, nhưng khái niệm cốt lõi vẫn giữ nguyên.

---

## Step 1: Load the Excel Template that Holds SmartMarker Blocks

Điều đầu tiên chúng ta làm là mở file mẫu. Hãy nghĩ mẫu như một khung xương; SmartMarker sẽ sau này lấp đầy nó bằng dữ liệu thực.

```csharp
using Aspose.Cells;

// Load the template containing SmartMarker tags
var workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");
```

**Tại sao điều này quan trọng:** Bằng cách tách bố cục (mẫu) ra khỏi dữ liệu (các đối tượng C#), bạn làm hài lòng cả designer và developer. Designer có thể chỉnh sửa phông chữ, màu sắc, hoặc công thức mà không cần chạm vào mã.

---

## Step 2: Build the Master‑Detail Data Source

Tiếp theo, chúng ta tạo dữ liệu sẽ được đưa vào mẫu. Đối với một báo cáo đơn hàng tiêu chuẩn, bạn sẽ có một tập hợp các đơn hàng, mỗi đơn hàng lại chứa một tập hợp các mục.

```csharp
// Master‑detail data: a list of orders, each with a list of items
var masterDetailData = new
{
    Orders = new[]
    {
        new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Prod = "A", Qty = 2 },
                new { Prod = "B", Qty = 1 }
            }
        },
        new
        {
            OrderId = 2,
            Items = new[]
            {
                new { Prod = "C", Qty = 5 }
            }
        }
    }
};
```

> **Pro tip:** Sử dụng các lớp strongly‑typed thay cho kiểu ẩn danh nếu bạn cần tái sử dụng chúng trong nhiều báo cáo. Cách dùng kiểu ẩn danh giúp ví dụ ngắn gọn hơn.

**Tại sao điều này quan trọng:** SmartMarker hoạt động bằng cách khớp tên thuộc tính (`Orders`, `OrderId`, `Items`, `Prod`, `Qty`) với các placeholder trong mẫu. Cấu trúc phân cấp phải hoàn toàn khớp, nếu không engine sẽ bỏ qua các phần tương ứng.

---

## Step 3: Tell SmartMarker to Create a New Sheet for Every Master Record

Mặc định SmartMarker ghi tất cả các hàng vào một sheet duy nhất. Chúng ta muốn mỗi đơn hàng nằm trên một worksheet riêng, thuận tiện cho việc in hoặc gửi PDF từng đơn hàng sau này.

```csharp
// Enable a separate sheet for each master (order) record
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableRepeatingSheet = true // each Order gets its own sheet
};
```

**Tại sao điều này quan trọng:** `EnableRepeatingSheet` loại bỏ nhu cầu sao chép sheet thủ công. Engine sẽ sao chép sheet gốc, chèn dữ liệu đơn hàng, và tự động đổi tên sheet (thường dựa trên giá trị của cột đầu tiên).

---

## Step 4: Process the Template with Your Data

Bây giờ chúng ta gắn mọi thứ lại với nhau. `SmartMarkerProcessor` sẽ duyệt qua workbook, thay thế các thẻ, và tạo các sheet mới theo chỉ dẫn.

```csharp
// Apply the data to the workbook
workbook.Worksheets[0].SmartMarkerProcessor.Process(masterDetailData, smartMarkerOptions);
```

**Tại sao điều này quan trọng:** Dòng lệnh duy nhất này thực hiện toàn bộ công việc nặng—phân tích mẫu, lặp qua các collection, và xử lý các bảng lồng nhau. Đây là trái tim của **populate Excel template C#** mà không cần vòng lặp thủ công.

---

## Step 5: Save the Finished Report

Cuối cùng, ghi workbook đã được điền dữ liệu ra đĩa. Bạn cũng có thể stream trực tiếp tới phản hồi HTTP cho các ứng dụng web.

```csharp
// Save the generated report
workbook.Save("YOUR_DIRECTORY/MasterDetailResult.xlsx");
```

**Tại sao điều này quan trọng:** Lưu thành file cho bạn một sản phẩm thực tế có thể mở trong Excel, chia sẻ với các bên liên quan, hoặc đưa vào các quy trình downstream như chuyển sang PDF.

---

## Full Working Example (Copy‑Paste Ready)

Dưới đây là chương trình hoàn chỉnh, bao gồm các `using` directive và phương thức `Main`. Đặt nó vào một console app, chỉnh sửa đường dẫn file, và chạy.

```csharp
using System;
using Aspose.Cells;

namespace ExcelReportDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the template
            var workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");

            // 2️⃣ Build master‑detail data
            var masterDetailData = new
            {
                Orders = new[]
                {
                    new
                    {
                        OrderId = 1,
                        Items = new[]
                        {
                            new { Prod = "A", Qty = 2 },
                            new { Prod = "B", Qty = 1 }
                        }
                    },
                    new
                    {
                        OrderId = 2,
                        Items = new[]
                        {
                            new { Prod = "C", Qty = 5 }
                        }
                    }
                }
            };

            // 3️⃣ Enable a new sheet per order
            var smartMarkerOptions = new SmartMarkerOptions
            {
                EnableRepeatingSheet = true
            };

            // 4️⃣ Process the template with data
            workbook.Worksheets[0].SmartMarkerProcessor.Process(masterDetailData, smartMarkerOptions);

            // 5️⃣ Save the result
            workbook.Save("YOUR_DIRECTORY/MasterDetailResult.xlsx");

            Console.WriteLine("Excel report generated successfully!");
        }
    }
}
```

### Expected Output

Khi bạn mở `MasterDetailResult.xlsx` sẽ thấy:

- **Sheet “Order_1”** – chứa header của Order 1 và hai dòng cho sản phẩm A và B.
- **Sheet “Order_2”** – chứa header của Order 2 và một dòng cho sản phẩm C.
- Tất cả công thức, định dạng, và biểu đồ từ mẫu gốc được giữ nguyên.

![Báo cáo Excel với các sheet riêng cho từng đơn hàng – ví dụ workbook đã được điền dữ liệu](/images/excel-report-example.png "Báo cáo Excel đã tạo với dữ liệu master‑detail")

*Văn bản thay thế ảnh: báo cáo Excel đã tạo với các sheet riêng cho từng đơn hàng, minh họa cách generate Excel report using C# and SmartMarker.*

---

## Common Questions & Edge Cases

### What if I need a static sheet (e.g., a summary) alongside the repeating sheets?

Đặt `EnableRepeatingSheet = true` **chỉ** trên worksheet chứa khối master. Các sheet khác sẽ không bị thay đổi, vì vậy bạn có thể giữ một trang tổng hợp trong mẫu gốc.

### Can I use a DataTable instead of anonymous objects?

Chắc chắn rồi. SmartMarker hoạt động với bất kỳ đối tượng nào thực thi `IEnumerable`. Chỉ cần thay thế kiểu ẩn danh bằng một `DataTable` và đảm bảo tên cột khớp với các thẻ.

```csharp
DataTable ordersTable = GetOrdersFromDatabase();
var data = new { Orders = ordersTable };
```

### How do I change the naming convention of the generated sheets?

Triển khai giao diện `ISmartMarkerSheetNaming` tùy chỉnh (hoặc thao tác với `workbook.Worksheets` sau khi xử lý). Hầu hết các developer chỉ đổi tên sheet dựa trên giá trị của một ô:

```csharp
foreach (var sheet in workbook.Worksheets)
{
    sheet.Name = $"Order_{sheet.Cells["A1"].StringValue}";
}
```

### What if my template uses a different placeholder syntax?

SmartMarker cho phép tùy chỉnh delimiter qua `SmartMarkerOptions`. Ví dụ, để dùng `<< >>` thay cho `{{ }}`:

```csharp
smartMarkerOptions.StartTag = "<<";
smartMarkerOptions.EndTag = ">>";
```

---

## Tips for Scaling This Approach

- **Cache mẫu** trong bộ nhớ nếu bạn tạo nhiều báo cáo cho mỗi yêu cầu; việc tải từ đĩa mỗi lần sẽ làm tăng độ trễ.
- **Kết hợp với chuyển đổi PDF** (`workbook.Save("report.pdf", SaveFormat.Pdf)`) để tạo ra đầu ra thân thiện với email.
- **Tham số hoá đường dẫn file** bằng các file cấu hình hoặc biến môi trường để giải pháp dễ di chuyển giữa dev, test, và prod.
- **Kiểm thử đơn vị lớp dữ liệu** riêng biệt; SmartMarker tự nó là deterministic, vì vậy bạn chỉ cần xác nhận dữ liệu đưa vào khớp với schema mong đợi.

---

## Conclusion

Chúng ta đã bao quát **cách generate Excel report** trong C# từ đầu đến cuối, từ việc tải mẫu SmartMarker tới việc lưu workbook đa sheet phản ánh mối quan hệ master‑detail. Bằng cách **populate Excel template C#** chỉ với vài dòng mã, bạn tránh được logic lặp lại từng ô và cho phép designer tự do thiết kế giao diện cuối cùng.

Tiếp theo, bạn có thể khám phá:

- Sử dụng **populate Excel template C#** với các biểu đồ tự động cập nhật theo sheet.
- Tích hợp **excel smartmarker c#** với ASP.NET Core để stream báo cáo trực tiếp tới trình duyệt.
- Tự động hoá quy trình **c# excel automation** lấy dữ liệu từ API hoặc cơ sở dữ liệu.

Hãy thử, tùy chỉnh mẫu, và xem nhanh chóng bạn có thể biến dữ liệu thô thành một báo cáo Excel chuyên nghiệp. Có câu hỏi hoặc trường hợp sử dụng thú vị? Để lại bình luận bên dưới—chúc bạn coding vui! 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}