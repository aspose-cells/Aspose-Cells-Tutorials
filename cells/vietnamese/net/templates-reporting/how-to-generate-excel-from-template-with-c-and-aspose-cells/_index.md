---
category: general
date: 2026-11-19
description: Học cách tạo Excel từ mẫu trong C# một cách nhanh chóng. Hướng dẫn này
  cũng chỉ cho bạn cách tạo báo cáo Excel bằng C# sử dụng Smart Markers.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate excel from template
- generate excel report c#
- Aspose.Cells Smart Marker
- master‑detail Excel export
- C# Excel automation
language: vi
lastmod: 2026-11-19
og_description: Tạo file Excel từ mẫu trong C# bằng Aspose.Cells. Tham khảo hướng
  dẫn này để tạo báo cáo Excel bằng C# sử dụng Smart Markers và dữ liệu master‑detail.
og_image_alt: Screenshot showing C# code that generates Excel from a template file
og_title: Tạo Excel từ mẫu trong C# – hướng dẫn chi tiết từng bước
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to generate Excel from template in C# quickly. This guide
    also shows you how to generate Excel report C# using Smart Markers.
  headline: How to generate Excel from template with C# and Aspose.Cells
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Cách tạo Excel từ mẫu bằng C# và Aspose.Cells
url: /vi/net/templates-reporting/how-to-generate-excel-from-template-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Excel từ mẫu trong C# – hướng dẫn chi tiết từng bước

Nếu bạn cần **tạo Excel từ mẫu** trong dự án .NET, bài hướng dẫn này sẽ cho bạn một giải pháp sẵn sàng chạy. Sử dụng Aspose.Cells Smart Markers, bạn có thể điền một workbook đã được thiết kế sẵn với dữ liệu master‑detail và tạo ra một báo cáo hoàn chỉnh mà không cần tự viết bất kỳ công thức Excel nào.

Bạn cũng sẽ thấy cách tiếp cận này cho phép bạn **tạo báo cáo Excel C#** cho hoá đơn, tóm tắt đơn hàng, hoặc bất kỳ tập dữ liệu phân cấp nào. Khi kết thúc hướng dẫn, bạn sẽ có một phương thức tái sử dụng để chuyển đổi tệp mẫu thành một workbook được lấp đầy đầy đủ.

## Nội dung hướng dẫn này

* Tải một mẫu `.xlsx` hiện có đã chứa các placeholder Smart Marker.  
* Chuẩn bị một đối tượng master‑detail phù hợp với cấu trúc phân cấp của mẫu.  
* Cấu hình `SmartMarkerProcessor` để tạo một sheet chi tiết riêng cho các collection lồng nhau.  
* Xử lý worksheet và lưu kết quả thành tệp mới.  

Không cần dịch vụ bên ngoài—chỉ cần thư viện Aspose.Cells cho .NET (bản dùng thử miễn phí hoặc phiên bản có giấy phép) và một dự án .NET 6+.

## Yêu cầu trước

| Yêu cầu | Lý do quan trọng |
|-------------|----------------|
| **Aspose.Cells for .NET** (gói NuGet `Aspose.Cells`) | Cung cấp `SmartMarkerProcessor` và các API thao tác Excel. |
| **.NET 6 SDK** hoặc phiên bản mới hơn | Đảm bảo các tính năng ngôn ngữ hiện đại và khả năng tương thích với phiên bản Aspose.Cells mới nhất. |
| **Một workbook mẫu** (`template.xlsx`) với Smart Markers được đặt trong worksheet đầu tiên | Smart Markers điều khiển việc ràng buộc dữ liệu; mẫu xác định bố cục, kiểu dáng và nội dung tĩnh. |
| Kiến thức cơ bản về các collection C# và kiểu ẩn danh | Nguồn dữ liệu được xây dựng dưới dạng một đối tượng ẩn danh phản ánh cấu trúc của mẫu. |

Bạn có thể tạo mẫu trong Excel bằng cách nhập `&=Orders.Id` cho cột ID đơn hàng và `&=Orders.Items.Name` cho các mục lồng nhau. Tiền tố `&=` báo cho Smart Markers thay thế ô bằng dữ liệu tại thời gian chạy.

## Bước 1: Thiết lập dự án C# và thêm Aspose.Cells

Tạo một ứng dụng console (hoặc tích hợp vào một dịch vụ hiện có) và thêm gói NuGet:

```bash
dotnet new console -n ExcelTemplateDemo
cd ExcelTemplateDemo
dotnet add package Aspose.Cells
```

> **Mẹo:** Sử dụng cờ `--version` để khóa vào một phiên bản ổn định đã biết, ví dụ, `Aspose.Cells 23.12`.

## Bước 2: Định nghĩa nguồn dữ liệu master‑detail

Nguồn dữ liệu phải phản ánh cấu trúc phân cấp được sử dụng trong mẫu. Trong ví dụ này, chúng ta có các đơn hàng (master) mỗi đơn hàng chứa một collection các mục (detail).

```csharp
using System;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // Step 2: Create the data source with master‑detail information
            var orderData = new
            {
                Orders = new[]
                {
                    new
                    {
                        Id = 1,
                        Items = new[]
                        {
                            new { Name = "A" },
                            new { Name = "B" }
                        }
                    },
                    new
                    {
                        Id = 2,
                        Items = new[]
                        {
                            new { Name = "C" }
                        }
                    }
                }
            };
```

**Tại sao cách này hoạt động:**  
*Kiểu ẩn danh* cho phép bạn xây dựng một biểu diễn nhanh trong bộ nhớ mà không cần định nghĩa các lớp POCO rõ ràng. Mỗi `Order` có một `Id` và một mảng `Items`, phù hợp với các marker `&=Orders.Id` và `&=Orders.Items.Name` trong mẫu.

## Bước 3: Tải mẫu Excel có chứa Smart Markers

```csharp
            // Step 3: Load the Excel template that contains Smart Markers
            string templatePath = @"YOUR_DIRECTORY\template.xlsx";
            Workbook workbook = new Workbook(templatePath);
```

**Giải thích:**  
`Workbook` đọc tệp `.xlsx` vào bộ nhớ. Mẫu nên đã có cú pháp Smart Marker (`&=Orders.Id`, `&=Orders.Items.Name`, v.v.) đặt ở vị trí bạn muốn dữ liệu xuất hiện.

## Bước 4: Lấy worksheet nơi Smart Markers được đặt

```csharp
            // Step 4: Get the worksheet where the Smart Markers are placed
            Worksheet worksheet = workbook.Worksheets[0];   // first sheet (index 0)
```

**Tại sao là sheet đầu tiên?**  
Hầu hết các mẫu giữ bảng master trên sheet đầu tiên, nhưng bạn có thể tham chiếu bất kỳ sheet nào bằng tên (`workbook.Worksheets["SheetName"]`) nếu thiết kế của bạn khác.

## Bước 5: Cấu hình SmartMarker processor

`SmartMarkerProcessor` thực hiện các công việc nặng. Bằng cách đặt `DetailSheetNewName` chúng ta chỉ đạo Aspose.Cells tạo một sheet mới cho mỗi collection lồng nhau.

```csharp
            // Step 5: Set up the SmartMarker processor and configure options
            SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
            smartMarkerProcessor.Options.DetailSheetNewName = "OrderDetails";
```

**Điều này làm gì:**  
Khi processor gặp một collection bên trong một collection (mảng `Items`), nó tạo một worksheet mới có tên `OrderDetails` và điền các hàng liên quan. Điều này giữ cho sheet master gọn gàng và phản ánh bố cục báo cáo master‑detail điển hình.

## Bước 6: Xử lý worksheet bằng nguồn dữ liệu

```csharp
            // Step 6: Process the worksheet using the data source
            smartMarkerProcessor.Process(worksheet, orderData);
```

Phương thức `Process` thay thế mọi Smart Marker bằng giá trị tương ứng từ `orderData`. Nó cũng mở rộng các hàng khi cần, vì vậy bạn không phải dự trữ không gian trong mẫu.

## Bước 7: Lưu workbook đã được lấp đầy

```csharp
            // Step 7: Save the populated workbook
            string outputPath = @"YOUR_DIRECTORY\masterDetail.xlsx";
            workbook.Save(outputPath);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Kết quả:**  
- `masterDetail.xlsx` chứa một sheet master với các ID đơn hàng.  
- Một sheet mới `OrderDetails` chứa tên các mục cho mỗi đơn hàng.  
- Tất cả định dạng (phông chữ, viền, độ rộng cột) từ mẫu được giữ nguyên.

Bạn có thể mở tệp trong Excel để xác nhận dữ liệu khớp với đối tượng nguồn.

## Mã nguồn đầy đủ (sẵn sàng sao chép‑dán)

```csharp
using System;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create the data source with master‑detail information
            var orderData = new
            {
                Orders = new[]
                {
                    new
                    {
                        Id = 1,
                        Items = new[]
                        {
                            new { Name = "A" },
                            new { Name = "B" }
                        }
                    },
                    new
                    {
                        Id = 2,
                        Items = new[]
                        {
                            new { Name = "C" }
                        }
                    }
                }
            };

            // Step 2: Load the Excel template that contains Smart Markers
            string templatePath = @"YOUR_DIRECTORY\template.xlsx";
            Workbook workbook = new Workbook(templatePath);

            // Step 3: Get the worksheet where the Smart Markers are placed
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 4: Set up the SmartMarker processor and configure options
            SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
            smartMarkerProcessor.Options.DetailSheetNewName = "OrderDetails";

            // Step 5: Process the worksheet using the data source
            smartMarkerProcessor.Process(worksheet, orderData);

            // Step 6: Save the populated workbook
            string outputPath = @"YOUR_DIRECTORY\masterDetail.xlsx";
            workbook.Save(outputPath);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Kết quả mong đợi trong Excel**

| **Đơn hàng** (master sheet) |
|---|
| Id |
| 1 |
| 2 |

*OrderDetails* sheet:

| **Mặt hàng** |
|---|
| Tên |
| A |
| B |
| C |

Các hàng được tự động thêm để khớp với số lượng mục cho mỗi đơn hàng.

## Các biến thể phổ biến và trường hợp đặc biệt

| Tình huống | Cách điều chỉnh mã |
|-----------|-----------------------|
| **Nhiều cấp chi tiết** (ví dụ, Orders → Items → SubItems) | Thêm một thuộc tính collection khác (`SubItems`) và đặt `DetailSheetNewName` thành một giá trị khác cho mỗi cấp. Aspose.Cells sẽ tự động tạo các sheet bổ sung. |
| **Đặt tên sheet tùy chỉnh cho mỗi bản ghi master** | Sử dụng `smartMarkerProcessor.Options.DetailSheetNameFromData = true;` và bao gồm trường `SheetName` trong collection master. |
| **Bộ dữ liệu lớn (hơn 10 000 hàng)** | Gọi `workbook.Settings.MemorySetting = MemorySetting.MemoryOptimized;` trước khi tải mẫu để giảm tiêu thụ bộ nhớ. |
| **Mẫu không có sheet chi tiết** (báo cáo phẳng) | Bỏ qua `DetailSheetNewName`; processor sẽ ghi dữ liệu lồng nhau trực tiếp vào sheet master, mở rộng các hàng khi cần. |
| **Chạy trong ASP.NET Core** | Thay thế `Console.WriteLine` bằng logging (`ILogger`) và sử dụng `Path.Combine` để xác định vị trí tệp tương đối với `wwwroot`. |

## Mẹo để tạo Excel đáng tin cậy

* **Giữ placeholder ở một hàng riêng** – Smart Markers mở rộng các hàng dưới marker; đặt chúng ở hàng tiêu đề sẽ giữ nguyên định dạng.  
* **Tránh gộp ô trong vùng dữ liệu** – Các ô đã gộp có thể gây dịch chuyển hàng không mong muốn khi mở rộng.  
* **Kiểm tra với bộ dữ liệu tối thiểu** trước; khi bố cục hoạt động, mở rộng lên dữ liệu thực.  
* **Khóa phiên bản** – Ghi lại phiên bản Aspose.Cells bạn đã sử dụng (`Aspose.Cells 23.12`) để tránh các thay đổi gây lỗi khi nâng cấp.  

## Kết luận

Bây giờ bạn đã biết cách **tạo Excel từ mẫu** trong C# bằng Aspose.Cells Smart Markers, và bạn có thể dễ dàng mở rộng cùng mẫu để **tạo báo cáo Excel C#** cho bất kỳ kịch bản master‑detail nào. Cách tiếp cận này tách biệt bố cục (mẫu) khỏi dữ liệu (đối tượng C#), cung cấp cho bạn một engine báo cáo có thể bảo trì và tái sử dụng.

Tiếp theo, khám phá các chủ đề liên quan sau:

* **Định dạng ô bằng lập trình** – học cách áp dụng conditional formatting sau khi dữ liệu đã được điền.  
* **Xuất ra PDF** – Aspose.Cells có thể chuyển đổi workbook đã tạo sang PDF chỉ với một lệnh.  
* **Tích hợp với ASP.NET Core** – truyền trực tiếp tệp đã tạo tới trình duyệt mà không cần ghi ra đĩa.

Hãy chạy thử mã, chỉnh sửa mẫu để phù hợp với thương hiệu của bạn, và để các báo cáo Excel được tạo trở thành một phần cốt lõi của ứng dụng .NET của bạn. Chúc lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các bài hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách tạo báo cáo Excel bằng cách hợp nhất mẫu Excel với Smart Markers](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-by-merging-an-excel-template-wi/)
- [Cách tạo báo cáo Excel trong C# – Hướng dẫn đầy đủ sử dụng SmartMarker](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/)
- [Aspose Cells Smart Markers: Tạo Excel từ Model trong C#](/cells/english/net/smart-markers-dynamic-data/aspose-cells-smart-markers-generate-excel-from-model-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}