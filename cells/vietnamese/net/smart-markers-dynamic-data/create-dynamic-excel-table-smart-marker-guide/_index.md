---
category: general
date: 2026-05-23
description: Tạo bảng Excel động bằng cách sử dụng mẫu và dữ liệu JSON. Tìm hiểu cách
  tải mẫu Excel, tự động hoá báo cáo Excel và nhanh chóng điền dữ liệu vào Excel từ
  JSON.
draft: false
keywords:
- create dynamic excel table
- load excel template
- automate excel report
- populate excel from json
- generate excel report json
language: vi
og_description: Tạo bảng Excel động trong vài phút bằng mẫu và JSON. Bài hướng dẫn
  này chỉ cách tải mẫu Excel, tự động hoá báo cáo Excel và điền dữ liệu Excel từ JSON.
og_title: Tạo bảng Excel động – Hướng dẫn Smart Marker
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create dynamic excel table using a template and JSON data. Learn how
    to load excel template, automate excel report, and populate excel from json quickly.
  headline: Create Dynamic Excel Table – Smart Marker Guide
  type: TechArticle
tags:
- Excel
- Smart Markers
- JSON
- .NET
title: Tạo Bảng Excel Động – Hướng Dẫn Smart Marker
url: /vi/net/smart-markers-dynamic-data/create-dynamic-excel-table-smart-marker-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Bảng Excel Động – Hướng Dẫn Smart Marker

Bạn đã bao giờ cần **tạo bảng excel động** mà tự động mở rộng cho mỗi bản ghi trong bộ dữ liệu của bạn chưa? Bạn không phải là người duy nhất. Dù bạn đang xây dựng bảng điều khiển bán hàng hàng tháng hay gói hoá đơn theo khách hàng, khả năng **điền dữ liệu excel từ json** mà không phải viết các vòng lặp vô tận có thể tiết kiệm hàng giờ.

Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn qua một giải pháp hoàn chỉnh, thực hành, cho thấy cách **tải mẫu excel**, nhúng một Smart Marker, cung cấp JSON cho nó, và cuối cùng **tự động tạo báo cáo excel**. Khi kết thúc, bạn sẽ có một dự án .NET sẵn sàng chạy, tạo ra một workbook Excel hoàn chỉnh từ một payload JSON duy nhất.

---

## Những Gì Bạn Cần

- **Aspose.Cells for .NET** (hoặc bất kỳ thư viện nào hỗ trợ Smart Markers). Ví dụ sử dụng phiên bản 24.5, nhưng bất kỳ bản phát hành gần đây nào cũng hoạt động.
- Visual Studio 2022 (hoặc IDE C# yêu thích của bạn).
- Một tệp mẫu Excel đơn giản (`template.xlsx`) đặt trong thư mục bạn kiểm soát.
- Một chuỗi JSON chứa một collection có tên `Customers`.

Chỉ vậy—không cần dịch vụ bổ sung, không cần kết nối cơ sở dữ liệu, chỉ cần mã thuần.

---

## Bước 1: Tạo Workbook Mẫu – Tải Mẫu Excel

Điều đầu tiên chúng ta làm là **tải mẫu excel** vào bộ nhớ. Hãy nghĩ mẫu như một canvas nơi một placeholder đặc biệt cho trình xử lý biết nơi cần lặp lại các hàng.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

// Load the template workbook (make sure the path is correct)
Workbook workbook = new Workbook(@"C:\Reports\template.xlsx");

// Grab the first worksheet – this is where our Smart Marker lives
Worksheet worksheet = workbook.Worksheets[0];
```

> **Tại sao điều này quan trọng:** Tải mẫu một lần giúp giảm tối đa I/O file và cho phép bạn tái sử dụng cùng một bố cục cho nhiều báo cáo. Nó cũng tách biệt logic Smart Marker khỏi phần còn lại của mã, tạo ra một sự tách biệt rõ ràng giữa các mối quan tâm.

---

## Bước 2: Chèn Smart Marker – Tạo Bảng Excel Động

Bây giờ chúng ta nhúng một **Smart Marker** sẽ lặp lại một bảng cho mỗi mục trong collection `Customers`. Cú pháp `${Customers.RepeatWorksheet}` cho Aspose.Cells biết sao chép toàn bộ worksheet cho mỗi khách hàng.

```csharp
// Place the Smart Marker in cell A1 (top‑left corner)
worksheet.Cells[0, 0].PutValue("${Customers.RepeatWorksheet}");
```

> **Mẹo chuyên nghiệp:** Nếu bạn chỉ cần lặp lại các hàng thay vì toàn bộ worksheet, hãy sử dụng `${Customers.Repeat}` trên hàng đầu tiên của bảng. Việc lặp lại ở mức worksheet rất hữu ích khi mỗi khách hàng có một tab riêng.

---

## Bước 3: Chuẩn Bị SmartMarkerProcessor – Tự Động Tạo Báo Cáo Excel

Với marker đã được đặt, chúng ta tạo một `SmartMarkerProcessor`. Đối tượng này điều phối việc ràng buộc dữ liệu giữa JSON và mẫu Excel.

```csharp
// Initialize the processor with the workbook that contains the marker
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
```

Processor này nhẹ, bạn có thể tái sử dụng nó cho nhiều payload JSON nếu muốn.

---

## Bước 4: Cung Cấp Dữ Liệu JSON – Đổ Dữ Liệu Vào Excel Từ JSON

Đây là nơi phép màu xảy ra. Chúng ta cung cấp một chuỗi JSON chứa một mảng các khách hàng. Mỗi khách hàng có thể có các trường như `Name`, `Email`, và `Total`.

```csharp
// Sample JSON data – in a real scenario you might read this from a file or API
string customersJson = @"
{
  ""Customers"": [
    { ""Name"": ""Acme Corp"", ""Email"": ""contact@acme.com"", ""Total"": 12500 },
    { ""Name"": ""Globex"", ""Email"": ""sales@globex.com"", ""Total"": 9800 },
    { ""Name"": ""Initech"", ""Email"": ""info@initech.com"", ""Total"": 15400 }
  ]
}";

// Apply the JSON to the processor – this populates the workbook
processor.ApplyJson(customersJson);
```

> **Tại sao lại là JSON?** JSON không phụ thuộc ngôn ngữ và dễ tạo ra từ API, cơ sở dữ liệu, hoặc thậm chí nhập liệu thủ công. Sử dụng `ApplyJson` có nghĩa là bạn không cần phải ánh xạ các đối tượng một cách thủ công; processor sẽ thực hiện phần công việc nặng.

---

## Bước 5: Lưu Kết Quả – Tạo Báo Cáo Excel JSON

Cuối cùng, chúng ta ghi workbook đã được điền dữ liệu ra đĩa. Tệp đầu ra bây giờ chứa một worksheet riêng cho mỗi khách hàng, mỗi worksheet được lấp đầy dữ liệu từ JSON của chúng ta.

```csharp
// Save the filled workbook – choose a path that makes sense for your app
workbook.Save(@"C:\Reports\output.xlsx");
```

### Kết Quả Dự Kiến

- **output.xlsx** sẽ có ba worksheet có tên `Sheet1`, `Sheet2`, `Sheet3` (hoặc bất kỳ quy ước đặt tên nào mà mẫu của bạn sử dụng).
- Mỗi sheet sẽ hiển thị các giá trị `Name`, `Email`, và `Total` cho một khách hàng duy nhất.
- Bố cục bạn thiết kế trong `template.xlsx` (tiêu đề, kiểu dáng, công thức) sẽ được giữ nguyên trên tất cả các sheet được tạo.

---

## Ví Dụ Hoàn Chỉnh Hoạt Động

Dưới đây là chương trình hoàn chỉnh, sẵn sàng chạy. Sao chép‑dán nó vào một ứng dụng console, điều chỉnh các đường dẫn tệp, và nhấn **F5**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace DynamicExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the template workbook
            string templatePath = @"C:\Reports\template.xlsx";
            Workbook workbook = new Workbook(templatePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Insert the Smart Marker that repeats the worksheet per customer
            worksheet.Cells[0, 0].PutValue("${Customers.RepeatWorksheet}");

            // 3️⃣ Create the SmartMarkerProcessor
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

            // 4️⃣ JSON data containing a collection of customers
            string customersJson = @"
            {
                ""Customers"": [
                    { ""Name"": ""Acme Corp"", ""Email"": ""contact@acme.com"", ""Total"": 12500 },
                    { ""Name"": ""Globex"", ""Email"": ""sales@globex.com"", ""Total"": 9800 },
                    { ""Name"": ""Initech"", ""Email"": ""info@initech.com"", ""Total"": 15400 }
                ]
            }";

            // Apply the JSON – this populates the workbook dynamically
            processor.ApplyJson(customersJson);

            // 5️⃣ Save the generated report
            string outputPath = @"C:\Reports\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"✅ Dynamic Excel report generated at: {outputPath}");
        }
    }
}
```

Chạy chương trình, mở `output.xlsx`, và bạn sẽ thấy một **tạo bảng excel động** đang hoạt động—mỗi khách hàng có một sheet riêng, được định dạng đầy đủ như bạn đã thiết kế.

---

## Câu Hỏi Thường Gặp & Trường Hợp Cạnh

| Question | Answer |
|----------|--------|
| *Nếu JSON của tôi có các đối tượng lồng nhau thì sao?* | Smart Markers hỗ trợ ký hiệu dấu chấm (`${Customers.Address.City}`) miễn là cấu trúc JSON phù hợp. |
| *Tôi có thể đặt tên các worksheet được tạo theo tên khách hàng không?* | Có—thêm một marker như `${Customers.Name}` vào ô tên worksheet hoặc sử dụng `processor.ApplyJson(customersJson, "Customers")` với mẫu đặt tên. |
| *Còn dữ liệu lớn (hơn 10 k dòng) thì sao?* | Processor truyền dữ liệu một cách hiệu quả, nhưng cần chú ý tới bộ nhớ. Xem xét chia báo cáo thành nhiều tệp nếu gặp giới hạn hiệu năng. |
| *Tôi có cần giấy phép cho Aspose.Cells không?* | Bản đánh giá miễn phí hoạt động cho việc thử nghiệm, nhưng phiên bản có giấy phép sẽ loại bỏ watermark đánh giá và cung cấp đầy đủ tính năng. |
| *Tôi có thể sử dụng cách này với .NET Core không?* | Chắc chắn—Aspose.Cells hỗ trợ .NET 6/7/8. Chỉ cần tham chiếu gói NuGet và mã vẫn giữ nguyên. |

---

## Mẹo cho Triển Khai Sẵn Sàng Sản Xuất

- **Validate JSON** trước khi cung cấp cho `ApplyJson`. Một payload không hợp lệ sẽ gây ra `JsonParseException`.
- **Cache the template** nếu bạn tạo nhiều báo cáo trong thời gian ngắn; việc tải liên tục từ đĩa là I/O không cần thiết.
- **Lock the workbook** trong quá trình xử lý nếu bạn chạy trong dịch vụ web đa luồng để tránh race condition.
- **Add error handling** quanh `workbook.Save` để xử lý một cách nhẹ nhàng các vấn đề quyền truy cập hoặc tệp bị khóa.
- **Customize styling** trong mẫu (định dạng có điều kiện, công thức) để các sheet được tạo giữ lại logic nghiệp vụ mà không cần mã bổ sung.

---

## Kết Luận

Bây giờ bạn đã có một mẫu vững chắc, từ đầu đến cuối cho cách **tạo bảng excel động** bằng cách sử dụng mẫu, Smart Markers và dữ liệu JSON. Bằng cách **tải mẫu excel**, chèn marker lặp lại, và **điền dữ liệu excel từ json**, bạn có thể **tự động tạo báo cáo excel** chỉ với vài dòng C#.

Bước tiếp theo? Hãy thử thêm biểu đồ tham chiếu các bảng động, hoặc xuất cùng JSON ra PDF bằng Aspose.Words. Bạn cũng có thể thử nghiệm **tạo báo cáo excel json** từ truy vấn cơ sở dữ liệu để hoàn thiện quy trình.

## Hướng Dẫn Liên Quan

- [Tạo Pivot Table trong Excel bằng Aspose.Cells cho .NET](/cells/english/net/pivot-tables/create-pivot-table/)
- [Tạo Biểu Đồ Đường Động trong Excel bằng Aspose.Cells cho .NET&#58; Hướng Dẫn Từng Bước](/cells/english/net/charts-graphs/create-line-charts-excel-aspose-cells-dotnet/)
- [Cách Tạo Checkbox trong Excel sử dụng Aspose.Cells cho .NET | Hướng Dẫn Xác Thực Dữ Liệu](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}