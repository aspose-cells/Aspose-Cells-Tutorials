---
category: general
date: 2026-10-10
description: Tạo báo cáo Excel bằng cách hợp nhất mẫu Excel sử dụng Smart Markers
  — thay thế các smart tag và xử lý thẻ chi tiết sheet một cách hiệu quả.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate Excel report
- merge Excel template
- detail sheet tag
- use smart markers
- replace smart tags
language: vi
lastmod: 2026-10-10
og_description: Tạo báo cáo Excel bằng Smart Markers. Tìm hiểu cách hợp nhất mẫu Excel,
  thay thế các thẻ thông minh và làm việc với thẻ chi tiết trên sheet trong một ví
  dụ C# đầy đủ.
og_image_alt: Generated Excel report after merging template with Smart Markers
og_title: Tạo báo cáo Excel bằng cách hợp nhất mẫu Excel với Smart Markers
schemas:
- author: GroupDocs
  dateModified: '2026-10-10'
  description: Generate Excel report by merging an Excel template using Smart Markers—replace
    smart tags and handle detail sheet tag efficiently.
  headline: How to generate Excel report by merging an Excel template with Smart Markers
  type: TechArticle
- description: Generate Excel report by merging an Excel template using Smart Markers—replace
    smart tags and handle detail sheet tag efficiently.
  name: How to generate Excel report by merging an Excel template with Smart Markers
  steps:
  - name: '**Load the Excel template** – The template holds the layout, formulas,
      and styling. Smart Markers are placeholders like `${MasterSheet:Orders}` that
      the processor will replace.'
    text: '**Load the Excel template** – The template holds the layout, formulas,
      and styling. Smart Markers are placeholders like `${MasterSheet:Orders}` that
      the processor will replace.'
  - name: '**Prepare the data source** – `SmartMarkerProcessor` works with any enumerable
      collection. Here we use a list of `Order` objects that contain a nested list
      of `OrderDetail` objects, which is exactly what a master‑detail report needs.'
    text: '**Prepare the data source** – `SmartMarkerProcessor` works with any enumerable
      collection. Here we use a list of `Order` objects that contain a nested list
      of `OrderDetail` objects, which is exactly what a master‑detail report needs.'
  - name: '**Create the processor** – Instantiating `SmartMarkerProcessor` is cheap;
      you can reuse it for multiple worksheets if you need to generate several reports
      in one run.'
    text: '**Create the processor** – Instantiating `SmartMarkerProcessor` is cheap;
      you can reuse it for multiple worksheets if you need to generate several reports
      in one run.'
  - name: '**Process the worksheet** – This single call does three things:'
    text: '**Process the worksheet** – This single call does three things:'
  - name: '**Save the result** – The output file (`GeneratedReport.xlsx`) is a fully‑populated
      Excel report ready for distribution.'
    text: '**Save the result** – The output file (`GeneratedReport.xlsx`) is a fully‑populated
      Excel report ready for distribution.'
  - name: Creates a new worksheet for every master row.
    text: Creates a new worksheet for every master row.
  - name: Copies the formatting from the template’s detail area.
    text: Copies the formatting from the template’s detail area.
  - name: Inserts each item from the enumerable into consecutive rows.
    text: Inserts each item from the enumerable into consecutive rows.
  - name: A **master sheet** named *Sheet1* with two rows—one for each order. Columns
      display Order ID, Customer, Order Date, and Total.
    text: A **master sheet** named *Sheet1* with two rows—one for each order. Columns
      display Order ID, Customer, Order Date, and Total.
  - name: Two **detail sheets** named `OrderDetails_1001` and `OrderDetails_1002`.
      Each sheet lists the products, quantities, and unit prices for the corresponding
      order.
    text: Two **detail sheets** named `OrderDetails_1001` and `OrderDetails_1002`.
      Each sheet lists the products, quantities, and unit prices for the corresponding
      order.
  type: HowTo
tags:
- Excel
- C#
- SmartMarkers
title: Cách tạo báo cáo Excel bằng cách hợp nhất mẫu Excel với Smart Markers
url: /vi/net/smart-markers-dynamic-data/how-to-generate-excel-report-by-merging-an-excel-template-wi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách tạo báo cáo Excel bằng cách hợp nhất mẫu Excel với Smart Markers

Nếu bạn cần **tạo báo cáo Excel** từ một workbook có thể tái sử dụng, Smart Markers cho phép bạn hợp nhất dữ liệu một cách nhanh chóng và đáng tin cậy. Bằng cách sử dụng phương pháp **hợp nhất mẫu Excel**, bạn tách riêng bố cục khỏi logic nghiệp vụ, và cùng một mẫu có thể phục vụ hàng chục báo cáo.

Hướng dẫn này sẽ chỉ cho bạn cách định nghĩa **thẻ sheet chi tiết**, **sử dụng smart markers** để điền dữ liệu master‑detail, và **thay thế smart tags** trong file cuối cùng. Bạn sẽ nhận được một chương trình C# hoàn chỉnh, có thể chạy được, tạo ra báo cáo Excel chuyên nghiệp trong vài giây.

## Những gì bạn cần

- .NET 6.0 trở lên (mã cũng hoạt động với .NET Framework 4.7+)
- Visual Studio 2022 hoặc bất kỳ IDE C# nào
- Gói NuGet `GroupDocs.Viewer` / `Aspose.Cells` (hoặc bất kỳ thư viện nào cung cấp `SmartMarkerProcessor`)
- Một file mẫu Excel (`ReportTemplate.xlsx`) chứa các thẻ Smart Marker được mô tả bên dưới

> **Mẹo chuyên nghiệp:** Đặt mẫu trong thư mục `Resources` của dự án và đặt thuộc tính *Copy to Output Directory* thành *Copy if newer* để mã có thể tìm thấy nó khi chạy.

## Tạo báo cáo Excel: từng bước với Smart Markers

Dưới đây là file nguồn đầy đủ `Program.cs`. Mỗi vùng được giải thích trong các phần tiếp theo.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.Cells;               // SmartMarkerProcessor lives in this namespace
using Aspose.Cells.Tables;        // For master‑detail handling

namespace ExcelReportDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the Excel template that contains Smart Marker tags
            string templatePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "ReportTemplate.xlsx");
            Workbook workbook = new Workbook(templatePath);
            Worksheet ws = workbook.Worksheets[0];   // assume the first sheet is the master sheet

            // 2️⃣ Prepare the data source – a list of orders, each with order lines
            List<Order> ordersData = GetSampleOrders();

            // 3️⃣ Create a SmartMarkerProcessor instance
            SmartMarkerProcessor processor = new SmartMarkerProcessor();

            // 4️⃣ Process the worksheet, merging the template with the data source
            // This replaces all ${...} tags with real values and expands the detail sheet tag.
            processor.Process(ws, ordersData);

            // 5️⃣ Save the merged workbook as the final report
            string outputPath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "GeneratedReport.xlsx");
            workbook.Save(outputPath, SaveFormat.Xlsx);

            Console.WriteLine($"Report generated successfully: {outputPath}");
        }

        // Sample data generator – in a real project you would pull from a database or service
        private static List<Order> GetSampleOrders()
        {
            return new List<Order>
            {
                new Order
                {
                    OrderId = 1001,
                    Customer = "Acme Corp",
                    OrderDate = new DateTime(2024, 9, 15),
                    Total = 1250.75,
                    Details = new List<OrderDetail>
                    {
                        new OrderDetail { Product = "Widget A", Quantity = 10, UnitPrice = 25.00 },
                        new OrderDetail { Product = "Widget B", Quantity = 5,  UnitPrice = 75.00 }
                    }
                },
                new Order
                {
                    OrderId = 1002,
                    Customer = "Beta Ltd.",
                    OrderDate = new DateTime(2024, 9, 16),
                    Total = 980.00,
                    Details = new List<OrderDetail>
                    {
                        new OrderDetail { Product = "Gadget X", Quantity = 8, UnitPrice = 80.00 },
                        new OrderDetail { Product = "Gadget Y", Quantity = 4, UnitPrice = 50.00 }
                    }
                }
            };
        }
    }

    // Simple POCO classes that represent master‑detail data
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime OrderDate { get; set; }
        public double Total { get; set; }
        public List<OrderDetail> Details { get; set; }
    }

    public class OrderDetail
    {
        public string Product { get; set; }
        public int Quantity { get; set; }
        public double UnitPrice { get; set; }
    }
}
```

### Tại sao mỗi phần lại quan trọng

1. **Tải mẫu Excel** – Mẫu chứa bố cục, công thức và định dạng. Smart Markers là các placeholder như `${MasterSheet:Orders}` mà bộ xử lý sẽ thay thế.

2. **Chuẩn bị nguồn dữ liệu** – `SmartMarkerProcessor` làm việc với bất kỳ collection nào có thể lặp. Ở đây chúng ta dùng danh sách các đối tượng `Order` chứa một danh sách lồng nhau các đối tượng `OrderDetail`, chính là cấu trúc cần cho báo cáo master‑detail.

3. **Tạo bộ xử lý** – Khởi tạo `SmartMarkerProcessor` rất nhẹ; bạn có thể tái sử dụng nó cho nhiều worksheet nếu cần tạo nhiều báo cáo trong một lần chạy.

4. **Xử lý worksheet** – Lệnh duy nhất này thực hiện ba việc:
   - **Thay thế smart tags** như `${MasterSheet:Orders}` bằng giá trị thực tế của trường.
   - **Mở rộng thẻ sheet chi tiết** (`${DetailSheetNewName:OrderDetails}`) thành một worksheet mới cho mỗi dòng master.
   - **Sao chép định dạng** từ mẫu sang các dòng được tạo, giữ nguyên thiết kế của bạn.

5. **Lưu kết quả** – File đầu ra (`GeneratedReport.xlsx`) là một báo cáo Excel đã được điền đầy đủ, sẵn sàng để phân phối.

## Hợp nhất mẫu Excel với nguồn dữ liệu

Cốt lõi của kỹ thuật **hợp nhất mẫu Excel** là cú pháp Smart Marker. Trong `ReportTemplate.xlsx` bạn sẽ đặt các thẻ như:

| Ô   | Giá trị |
|------|---------|
| A1   | `${MasterSheet:Orders.OrderId}` |
| B1   | `${MasterSheet:Orders.Customer}` |
| C1   | `${MasterSheet:Orders.OrderDate:MM/dd/yyyy}` |
| D1   | `${MasterSheet:Orders.Total}` |
| A5   | `${DetailSheetNewName:OrderDetails}` |
| A6   | `${DetailSheet:OrderDetails.Product}` |
| B6   | `${DetailSheet:OrderDetails.Quantity}` |
| C6   | `${DetailSheet:OrderDetails.UnitPrice}` |

- `${MasterSheet:Orders}` yêu cầu bộ xử lý đọc collection `Orders` từ nguồn dữ liệu.
- `${DetailSheetNewName:OrderDetails}` tạo một **thẻ sheet chi tiết** sinh ra một worksheet mới có tên dựa trên dòng master (ví dụ, `OrderDetails_1001`).
- `${DetailSheet:OrderDetails.*}` điền mỗi dòng chi tiết.

Khi `processor.Process(ws, ordersData)` được gọi, thư viện tự động **thay thế smart tags** bằng các giá trị từ `ordersData` và sao chép sheet chi tiết cho mỗi đơn hàng.

## Cú pháp thẻ sheet chi tiết

Một **thẻ sheet chi tiết** tuân theo mẫu `${DetailSheetNewName:TagName}`. `TagName` phải khớp với một thuộc tính trả về `IEnumerable` (trong ví dụ của chúng ta là `Order.Details`). Bộ xử lý:

1. Tạo một worksheet mới cho mỗi dòng master.
2. Sao chép định dạng từ khu vực chi tiết của mẫu.
3. Chèn từng mục trong enumerable vào các dòng liên tiếp.

Nếu bạn muốn sheet chi tiết giữ cùng một tên cho mọi dòng master (ví dụ, một sheet duy nhất chứa tất cả chi tiết), thay `${DetailSheetNewName:OrderDetails}` bằng `${DetailSheet:OrderDetails}`. Cách này hữu ích cho các kịch bản **tạo báo cáo Excel** nơi mỗi đơn hàng có một tab riêng.

## Sử dụng smart markers để thay thế smart tags

Smart Markers không chỉ là các placeholder đơn giản. Chúng hỗ trợ:

- **Chuỗi định dạng** (`:MM/dd/yyyy` trong ví dụ) để kiểm soát cách hiển thị ngày hoặc số.
- **Các phần có điều kiện** (`${if:Orders.Total > 1000}`) để ẩn dòng dựa trên dữ liệu.
- **Vòng lặp** qua các collection mà không cần viết mã ngoài thẻ.

Vì bộ xử lý thực hiện các tính năng này nội bộ, bạn **thay thế smart tags** trong mẫu mà không cần viết vòng lặp tùy chỉnh hay gán ô‑theo‑ô. Điều này giảm lỗi và giúp mẫu dễ bảo trì hơn.

## Kết quả mong đợi

Sau khi chạy chương trình, mở `GeneratedReport.xlsx`. Bạn sẽ thấy:

1. Một **sheet master** tên *Sheet1* với hai dòng — mỗi dòng cho một đơn hàng. Các cột hiển thị Order ID, Customer, Order Date và Total.
2. Hai **sheet chi tiết** tên `OrderDetails_1001` và `OrderDetails_1002`. Mỗi sheet liệt kê các sản phẩm, số lượng và đơn giá tương ứng với đơn hàng đó.
3. Tất cả định dạng gốc (phông chữ, màu sắc, viền) được giữ nguyên từ `ReportTemplate.xlsx`.

![Generated Excel report after merging template with Smart Markers](generated-report.png "Generated Excel report after merging template


## Bạn nên học gì tiếp theo?


Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã mẫu đầy đủ với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Aspose Cells Smart Markers: Load Excel Template & Generate Excel from Template](/cells/english/java/templates-reporting/aspose-cells-smart-markers-load-excel-template-generate-exce/)
- [Generate Dynamic Excel Reports Using Aspose.Cells .NET Smart Markers](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Aspose Cells Smart Markers: Generate Excel from Model in C#](/cells/english/net/smart-markers-dynamic-data/aspose-cells-smart-markers-generate-excel-from-model-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}