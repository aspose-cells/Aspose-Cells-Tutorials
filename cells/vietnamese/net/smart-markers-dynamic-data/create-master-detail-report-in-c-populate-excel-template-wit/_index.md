---
category: general
date: 2026-02-28
description: Tạo báo cáo master‑detail bằng C# và học cách điền dữ liệu vào mẫu Excel,
  hợp nhất dữ liệu vào Excel, và tải workbook Excel bằng C# chỉ trong vài bước.
draft: false
keywords:
- create master detail report
- populate excel template
- merge data into excel
- load excel workbook c#
- how to create master detail
language: vi
og_description: Tạo báo cáo master-detail trong C# bằng Aspose.Cells SmartMarker.
  Học cách tải workbook Excel trong C#, hợp nhất dữ liệu vào Excel và điền dữ liệu
  vào mẫu Excel.
og_title: Tạo báo cáo master‑detail trong C# – Điền dữ liệu vào mẫu Excel
tags:
- C#
- Aspose.Cells
- Excel automation
- SmartMarker
title: Tạo báo cáo master‑detail trong C# – Điền mẫu Excel bằng SmartMarker
url: /vi/net/smart-markers-dynamic-data/create-master-detail-report-in-c-populate-excel-template-wit/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo báo cáo master‑detail trong C# – Điền mẫu Excel bằng SmartMarker

Bạn đã bao giờ cần **tạo báo cáo master‑detail** trong C# nhưng không chắc làm thế nào đưa dữ liệu vào tệp Excel? Bạn không phải là người duy nhất. Trong hướng dẫn này, chúng tôi sẽ trình bày các bước chính xác để **điền mẫu Excel**, **gộp dữ liệu vào Excel**, và **tải workbook Excel C#**‑style để bạn có được một báo cáo master‑detail hoàn chỉnh, sẵn sàng phân phối.

Chúng tôi sẽ sử dụng Aspose.Cells SmartMarker, một engine mạnh mẽ hiểu các quan hệ master‑detail ngay từ đầu. Khi kết thúc tutorial, bạn sẽ có một ví dụ hoàn chỉnh, có thể chạy được mà bạn có thể chèn vào bất kỳ dự án .NET nào. Không có các lối tắt mơ hồ “xem tài liệu” — chỉ có một giải pháp tự chứa mà bạn có thể sao chép‑dán và chạy.

## Những gì bạn sẽ học

- Cách **tạo master‑detail** cấu trúc dữ liệu trong C# mà ánh xạ trực tiếp tới mẫu Excel.
- Cách chính xác để **tải workbook Excel C#** mã mở một tệp `.xlsx` chứa các thẻ SmartMarker.
- Quy trình **điền mẫu Excel** bằng cách chạy `SmartMarkerProcessor`.
- Mẹo xử lý các trường hợp đặc biệt, như thẻ bị thiếu hoặc tập dữ liệu lớn.
- Cách kiểm tra kết quả và xem báo cáo **master‑detail** cuối cùng trông như thế nào.

### Yêu cầu trước

- .NET 6.0 trở lên (mã cũng hoạt động trên .NET Framework 4.8).
- Aspose.Cells cho .NET (bạn có thể tải gói dùng thử miễn phí qua NuGet: `Install-Package Aspose.Cells`).
- Một tệp Excel cơ bản (`template.xlsx`) chứa các thẻ SmartMarker (chúng tôi sẽ hiển thị markup tối thiểu bạn cần).

Nếu bạn đã sẵn sàng, hãy bắt đầu.

## Bước 1 – Tạo nguồn dữ liệu master‑detail *(cách tạo master detail)*

Điều đầu tiên bạn cần là một đối tượng C# đại diện cho các hàng master (đơn hàng) và các hàng con (mặt hàng). SmartMarker sẽ tự động đọc cấu trúc này khi `MasterDetail` được đặt thành `true`.

```csharp
using System;

// Step 1: Build the master‑detail data object
var orderData = new
{
    // Master collection – each order is a row in the master table
    Orders = new[]
    {
        new
        {
            Id = 1,
            // Detail collection – items belonging to order 1
            Items = new[] { new { Sku = 101, Qty = 2 }, new { Sku = 102, Qty = 1 } }
        },
        new
        {
            Id = 2,
            Items = new[] { new { Sku = 202, Qty = 1 } }
        }
    }
};
```

**Tại sao điều này quan trọng:**  
SmartMarker tìm một thuộc tính có tên `Orders` (master) và sau đó đối với mỗi đơn hàng nó tìm một collection có tên `Items`. Bằng cách khớp các tên này, bạn tự động có được một **báo cáo master‑detail** mà không cần viết bất kỳ vòng lặp nào.

> **Mẹo chuyên nghiệp:** Giữ tên thuộc tính ngắn gọn và có ý nghĩa; chúng sẽ trở thành các placeholder trong mẫu Excel của bạn.

## Bước 2 – Cấu hình tùy chọn SmartMarker cho xử lý master‑detail

Thông báo cho engine rằng bạn đang làm việc với một kịch bản master‑detail và cung cấp tên của sheet chi tiết sẽ nhận các hàng con.

```csharp
using Aspose.Cells;

// Step 2: Set up SmartMarker options
SmartMarkerOptions options = new SmartMarkerOptions
{
    // Enables master‑detail processing
    MasterDetail = true,
    // The sheet in the template that holds the detail rows
    DetailSheetName = "OrderDetail"
};
```

**Tại sao điều này quan trọng:**  
Nếu bạn bỏ qua `MasterDetail = true`, SmartMarker sẽ xem dữ liệu như một danh sách phẳng và các hàng chi tiết sẽ không bao giờ xuất hiện. `DetailSheetName` phải khớp với tên sheet bạn tạo trong mẫu (phân biệt chữ hoa/thường).

## Bước 3 – Tải workbook Excel theo kiểu C#

Bây giờ chúng ta mở mẫu chứa các thẻ SmartMarker. Đây là bước **tải workbook Excel C#** mà nhiều nhà phát triển gặp khó khăn vì họ quên sử dụng đúng đường dẫn tệp hoặc không giải phóng workbook đúng cách.

```csharp
using System.IO;

// Step 3: Load the workbook that holds the SmartMarker tags
string templatePath = Path.Combine(Environment.CurrentDirectory, "template.xlsx");
Workbook workbook = new Workbook(templatePath);
```

**Tại sao điều này quan trọng:**  
Aspose.Cells đọc toàn bộ workbook vào bộ nhớ, vì vậy tệp có thể nằm trên đĩa, nhúng như một resource, hoặc thậm chí được stream từ một dịch vụ web. Chỉ cần chắc chắn đường dẫn trỏ tới một tệp `.xlsx` hợp lệ chứa các thẻ chúng ta sẽ thảo luận tiếp theo.

## Bước 4 – Chèn thẻ SmartMarker vào mẫu (điền mẫu Excel)

Nếu bạn mở `template.xlsx` ngay bây giờ, bạn sẽ thấy hai sheet:

- **Orders** – sheet master với một hàng như `&=Orders.Id`.
- **OrderDetail** – sheet detail với các hàng như `&=Items.Sku` và `&=Items.Qty`.

Dưới đây là một view tối thiểu của markup:

| Sheet | Cell A1 | Cell B1 |
|-------|---------|---------|
| Orders | `&=Orders.Id` | *(trống)* |
| OrderDetail | `&=Items.Sku` | `&=Items.Qty` |

Bạn không cần viết bất kỳ mã nào cho các thẻ — chúng tồn tại trong tệp Excel. Bước **điền mẫu Excel** chỉ đơn giản là gọi bộ xử lý:

```csharp
// Step 4: Run SmartMarker to merge data into Excel
new SmartMarkerProcessor().Process(workbook, orderData, options);
```

**Tại sao điều này quan trọng:**  
Bộ xử lý quét mọi sheet, thay thế các placeholder `&=` bằng giá trị thực, và mở rộng các hàng cho mỗi bản ghi master và detail. Vì `MasterDetail` được bật, nó tự động tạo một hàng mới cho mỗi mục dưới đơn hàng tương ứng.

## Bước 5 – Lưu báo cáo master‑detail

Cuối cùng, ghi workbook đã được điền vào đĩa. Đây là lúc bạn có một **báo cáo master‑detail** sẵn sàng chia sẻ.

```csharp
// Step 5: Save the populated workbook
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
workbook.Save(outputPath);

// Optional: open the file automatically (Windows only)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = outputPath,
    UseShellExecute = true
});
```

**Kết quả mong đợi:**  

- Sheet **Orders** hiển thị hai hàng: `1` và `2` (ID đơn hàng).  
- Sheet **OrderDetail** hiển thị ba hàng:  
  - SKU 101 Qty 2  
  - SKU 102 Qty 1  
  - SKU 202 Qty 1  

Đó là một **báo cáo master‑detail** hoàn chỉnh mà bạn có thể gửi email, in ấn, hoặc đưa vào hệ thống khác.

## Các trường hợp đặc biệt & câu hỏi thường gặp

### Nếu mẫu thiếu thẻ thì sao?

SmartMarker sẽ im lặng bỏ qua các thẻ không biết, nhưng bạn sẽ nhận được các ô trống. Hãy kiểm tra lại chính tả thẻ và đảm bảo tên thuộc tính trong đối tượng C# của bạn khớp chính xác.

### Nó xử lý tập dữ liệu lớn như thế nào?

Bộ xử lý stream các hàng, vì vậy ngay cả hàng nghìn bản ghi detail cũng không làm tràn bộ nhớ. Tuy nhiên, đối với các tệp cực lớn, bạn có thể muốn tăng `MemorySetting` trong `LoadOptions`.

```csharp
var loadOptions = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook largeWorkbook = new Workbook(templatePath, loadOptions);
```

### Tôi có thể dùng tên sheet khác cho master không?

Được — chỉ cần đổi tên sheet trong mẫu và điều chỉnh `DetailSheetName` nếu bạn có sheet detail. Tên sheet master được suy ra từ placeholder (`&=Orders.Id`).

### Nếu tôi cần thêm một hàng tổng cộng thì sao?

Thêm một công thức Excel thông thường vào mẫu (ví dụ, `=SUM(B2:B{#})`). SmartMarker sẽ giữ lại công thức sau khi chèn dữ liệu.

## Ví dụ đầy đủ có thể chạy được

Dưới đây là chương trình hoàn chỉnh mà bạn có thể sao chép‑dán vào một ứng dụng console. Nó bao gồm tất cả các chỉ thị `using`, mô hình dữ liệu, tùy chọn và xử lý tệp.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace MasterDetailReportDemo
{
    class Program
    {
        static void Main()
        {
            // ---------- Step 1: Create master‑detail data ----------
            var orderData = new
            {
                Orders = new[]
                {
                    new
                    {
                        Id = 1,
                        Items = new[]
                        {
                            new { Sku = 101, Qty = 2 },
                            new { Sku = 102, Qty = 1 }
                        }
                    },
                    new
                    {
                        Id = 2,
                        Items = new[]
                        {
                            new { Sku = 202, Qty = 1 }
                        }
                    }
                }
            };

            // ---------- Step 2: SmartMarker options ----------
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                MasterDetail = true,
                DetailSheetName = "OrderDetail"
            };

            // ---------- Step 3: Load the template ----------
            string templatePath = Path.Combine(Environment.CurrentDirectory, "template.xlsx");
            Workbook workbook = new Workbook(templatePath);

            // ---------- Step 4: Process the template ----------
            new SmartMarkerProcessor().Process(workbook, orderData, options);

            // ---------- Step 5: Save the result ----------
            string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
            workbook.Save(outputPath);

            Console.WriteLine($"Master detail report generated at: {outputPath}");
        }
    }
}
```

Chạy chương trình, mở `output.xlsx`, và bạn sẽ thấy dữ liệu master‑detail được điền đẹp mắt.

## Tham chiếu hình ảnh

![Ảnh chụp màn hình kết quả báo cáo master‑detail](https://example.com/images/master-detail-report.png "Ví dụ báo cáo master‑detail")

*Hình ảnh hiển thị sheet Orders với các ID 1 và 2, và sheet OrderDetail với ba hàng SKU‑Qty.*

## Kết luận

Bạn giờ đã biết **cách tạo báo cáo master‑detail** trong C# bằng Aspose.Cells SmartMarker, từ việc xây dựng nguồn dữ liệu đến **tải workbook Excel C#**, **điền mẫu Excel**, và cuối cùng

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}