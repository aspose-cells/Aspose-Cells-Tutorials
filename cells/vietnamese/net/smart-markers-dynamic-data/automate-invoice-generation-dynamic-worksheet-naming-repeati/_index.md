---
category: general
date: 2026-02-14
description: 'Tự động tạo hoá đơn với SmartMarker: học cách lặp lại các bảng tính,
  đặt tên chúng một cách động, và thành thạo việc đặt tên bảng tính động trong vài
  phút.'
draft: false
keywords:
- automate invoice generation
- how to name worksheets
- how to repeat worksheet
- dynamic worksheet naming
language: vi
og_description: Tự động tạo hóa đơn với SmartMarker. Hướng dẫn này chỉ cách lặp lại
  các bảng tính, đặt tên chúng một cách động và làm chủ việc đặt tên bảng tính động.
og_title: Tự động tạo hoá đơn – Đặt tên bảng tính động & Lặp lại
tags:
- C#
- SmartMarker
- Excel Automation
title: Tự động tạo hoá đơn – Đặt tên bảng tính động & Lặp lại trong C#
url: /vi/net/smart-markers-dynamic-data/automate-invoice-generation-dynamic-worksheet-naming-repeati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tự động tạo hoá đơn – Đặt tên Worksheet động & Lặp lại trong C#

Bạn đã bao giờ tự hỏi làm thế nào để **tự động tạo hoá đơn** mà không cần sao chép các sheet thủ công cho mỗi đơn hàng? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi họ cần một worksheet riêng cho mỗi hoá đơn nhưng cũng muốn tên sheet phản ánh số đơn hàng. Trong hướng dẫn này, chúng tôi sẽ giải quyết vấn đề đó bằng cách sử dụng `SmartMarkerProcessor` của SmartMarker và chỉ cho bạn **cách đặt tên worksheet** một cách động đồng thời bao phủ **cách lặp lại worksheet** cho mỗi bản ghi. Khi kết thúc, bạn sẽ có một mẫu C# sẵn sàng chạy tạo ra một workbook trong đó mỗi hoá đơn nằm trên một tab có tên đẹp mắt.

Chúng tôi sẽ hướng dẫn từng bước—từ việc lấy các đơn hàng từ nguồn dữ liệu đến cấu hình `SmartMarkerOptions` cho việc đặt tên worksheet động. Không cần tài liệu bên ngoài; mọi thứ bạn cần đều có ở đây. Chỉ cần một chút kiến thức nền về C# và tham chiếu tới thư viện Aspose.Cells (hoặc bất kỳ engine tương thích SmartMarker nào) là đủ.

---

## Những gì bạn sẽ xây dựng

- Lấy một tập hợp các đối tượng order.
- Cấu hình SmartMarker để **lặp lại một worksheet** cho mỗi order.
- Áp dụng **đặt tên worksheet động** bằng cách sử dụng placeholder `{OrderId}`.
- Tạo một tệp Excel trong đó mỗi tab được đặt tên `Invoice_12345`, `Invoice_67890`, v.v.
- Xác minh đầu ra bằng cách mở workbook.

## Yêu cầu trước

- .NET 6.0 hoặc mới hơn (mã có thể biên dịch với .NET 5+ cũng được).
- Aspose.Cells cho .NET (hoặc bất kỳ thư viện nào triển khai SmartMarker). Cài đặt qua NuGet:

```bash
dotnet add package Aspose.Cells
```

- Một lớp `Order` cơ bản (bạn có thể thay thế bằng DTO của riêng mình).

## Bước 1: Thiết lập dự án và mô hình

Đầu tiên, tạo một ứng dụng console mới và định nghĩa mô hình dữ liệu đại diện cho một order.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    // Simple POCO representing an order – replace fields as needed
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }
    }

    class Program
    {
        static void Main()
        {
            // Retrieve orders (in real life this could be a DB call)
            var orders = GetOrders();

            // The rest of the tutorial continues here...
        }

        // Mock method – in production pull from EF Core, Dapper, etc.
        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

> **Mẹo:** Giữ mô hình nhẹ cho bản demo; bạn luôn có thể bổ sung nó sau này với các mục hàng, chi tiết thuế, v.v.

## Bước 2: Chuẩn bị mẫu Excel

SmartMarker hoạt động dựa trên một workbook mẫu. Tạo một tệp có tên `InvoiceTemplate.xlsx` với một worksheet duy nhất tên `InvoiceTemplate`. Trong ô **A1** đặt một placeholder SmartMarker như:

```
{{OrderId}} – {{Customer}} – {{Date}} – ${{Total}}
```

Bạn có thể định dạng các ô theo cách bạn muốn—đầu đề in đậm, định dạng tiền tệ, v.v. Lưu tệp trong thư mục gốc của dự án.

> **Tại sao cần mẫu?** Nó tách biệt bố cục khỏi mã, cho phép nhà thiết kế chỉnh sửa giao diện mà không ảnh hưởng đến logic.

## Bước 3: Cấu hình SmartMarker Options – Lặp lại & Đặt tên Worksheet

Bây giờ chúng ta sẽ chỉ cho SmartMarker *lặp lại* worksheet mẫu cho mỗi order và đặt tên cho mỗi bản sao sao cho bao gồm ID của order. Đây là cốt lõi của **đặt tên worksheet động**.

```csharp
// Inside Main() after retrieving orders
// Load the template workbook
Workbook wb = new Workbook("InvoiceTemplate.xlsx");

// Set up SmartMarker options
var smartMarkerOptions = new SmartMarkerOptions
{
    // Instructs SmartMarker to create a new worksheet per data item
    RepeatWorksheet = true,

    // Naming pattern – {OrderId} will be replaced with the actual value
    RepeatWorksheetName = "Invoice_{OrderId}"
};

// Run the processor
wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

// Save the result
string outputPath = "GeneratedInvoices.xlsx";
wb.Save(outputPath);

Console.WriteLine($"✅ Invoices generated: {outputPath}");
```

### Cách hoạt động

- **`RepeatWorksheet = true`** cho engine biết sao chép sheet nguồn cho mỗi phần tử trong tập hợp `orders`. Điều này đáp ứng yêu cầu **cách lặp lại worksheet**.
- **`RepeatWorksheetName = "Invoice_{OrderId}"`** là một chuỗi mẫu trong đó `{OrderId}` là placeholder mà SmartMarker thay thế bằng ID của order hiện tại. Đó là câu trả lời cho **cách đặt tên worksheet** và **đặt tên worksheet động**.
- Bộ xử lý sẽ hợp nhất các trường của mỗi order (`{{OrderId}}`, `{{Customer}}`, v.v.) vào sheet đã sao chép, tạo ra một hoá đơn đã được điền đầy đủ.

## Bước 4: Chạy ứng dụng và xác minh đầu ra

Biên dịch và chạy ứng dụng console:

```bash
dotnet run
```

Bạn sẽ thấy thông báo thành công trong console. Mở `GeneratedInvoices.xlsx` và bạn sẽ thấy ba tab:

- **Invoice_1001**
- **Invoice_1002**
- **Invoice_1003**

Mỗi sheet chứa dữ liệu order đã được thay thế vào các placeholder. Bố cục bạn thiết kế trong mẫu được giữ nguyên, chứng minh rằng **tự động tạo hoá đơn** hoạt động từ đầu đến cuối.

### Ảnh chụp màn hình dự kiến (văn bản thay thế cho SEO)

![ví dụ tự động tạo hoá đơn hiển thị ba worksheet được đặt tên động](/images/invoice-automation.png)

> *Văn bản thay thế cho ảnh bao gồm từ khóa chính để đáp ứng SEO.*

## Bước 5: Các trường hợp góc cạnh & Biến thể phổ biến

### Nếu OrderId chứa ký tự không hợp lệ thì sao?

Tên sheet Excel không được chứa `\ / ? * [ ] :`. Nếu ID của bạn có thể bao gồm những ký tự này, hãy làm sạch chúng:

```csharp
RepeatWorksheetName = "Invoice_{SanitizedOrderId}"
```

Thêm một thuộc tính tính toán vào `Order`:

```csharp
public string SanitizedOrderId => OrderId.ToString().Replace("/", "-").Replace("\\", "-");
```

### Cần giữ lại sheet mẫu gốc?

Đặt `smartMarkerOptions.RemoveTemplate = false;` (mặc định là `true`). Điều này để nguyên `InvoiceTemplate` không bị thay đổi, dùng làm tham chiếu.

### Muốn nhóm hoá đơn theo khách hàng?

Bạn có thể lồng **repeat groups**. Đầu tiên lặp lại theo khách hàng, sau đó lặp lại các order trong mỗi worksheet của khách hàng. Cú pháp sẽ hơi phức tạp hơn, nhưng nguyên tắc vẫn giữ nguyên—sử dụng `RepeatWorksheet` và một mẫu đặt tên phản ánh cấu trúc phân cấp.

## Ví dụ hoàn chỉnh (Tất cả mã trong một nơi)

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }

        // Helper for safe sheet names
        public string SanitizedOrderId => OrderId.ToString();
    }

    class Program
    {
        static void Main()
        {
            var orders = GetOrders();

            // Load template
            Workbook wb = new Workbook("InvoiceTemplate.xlsx");

            // Configure SmartMarker for repeating and naming worksheets
            var smartMarkerOptions = new SmartMarkerOptions
            {
                RepeatWorksheet = true,
                RepeatWorksheetName = "Invoice_{OrderId}" // dynamic worksheet naming
                // RemoveTemplate = true; // default behavior
            };

            // Process the data
            wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

            // Save the final workbook
            string outputPath = "GeneratedInvoices.xlsx";
            wb.Save(outputPath);

            Console.WriteLine($"✅ Invoices generated: {outputPath}");
        }

        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

Sao chép‑dán đoạn này vào `Program.cs`, đặt `InvoiceTemplate.xlsx` bên cạnh nó, và bạn đã sẵn sàng.

## Câu hỏi thường gặp

**Q: Phương pháp này có hoạt động với bộ dữ liệu lớn (hàng ngàn hoá đơn) không?**  
A: Có. SmartMarker truyền dữ liệu một cách hiệu quả, nhưng bạn cần chú ý đến việc sử dụng bộ nhớ. Nếu gặp giới hạn, hãy cân nhắc xử lý theo lô và ghi mỗi lô vào một workbook riêng.

**Q: Tôi có thể tự động thêm logo vào mỗi hoá đơn không?**  
A: Chắc chắn. Đặt hình logo trên sheet mẫu. Vì sheet được sao chép, logo sẽ xuất hiện trên mỗi hoá đơn được tạo mà không cần mã bổ sung.

**Q: Nếu tôi cần bảo vệ các worksheet thì sao?**  
A: Sau khi xử lý, duyệt qua `wb.Worksheets` và gọi `ws.Protect(Password, ProtectionType.All)`.

## Kết luận

Chúng ta vừa **tự động tạo hoá đơn** bằng cách tận dụng tính năng lặp lại worksheet của SmartMarker và một mẫu đặt tên thông minh. Hướng dẫn đã bao phủ **cách đặt tên worksheet**, trình bày **cách lặp lại worksheet** cho mỗi order, và giới thiệu **đặt tên worksheet động** giúp workbook của bạn gọn gàng và dễ tìm kiếm.

Từ việc lấy dữ liệu, thiết lập mẫu, cấu hình `SmartMarkerOptions`, đến xử lý các trường hợp góc cạnh, bạn giờ đã có một giải pháp hoàn chỉnh, có thể chạy ngay. Tiếp theo, hãy thử thêm bảng chi tiết hàng, áp dụng định dạng có điều kiện, hoặc xuất cùng dữ liệu sang PDF để có một quy trình thanh toán hoàn toàn tự động.

Sẵn sàng nâng cấp? Khám phá các chủ đề liên quan như “xuất Excel hàng loạt với Aspose.Cells”, “chuyển đổi worksheet sang PDF”, hoặc “gửi hoá đơn đã tạo qua email trực tiếp từ C#”. Không gì là không thể—chúc bạn lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}