---
category: general
date: 2026-10-10
description: Học cách xử lý mẫu Excel trong C# đồng thời tự động đặt tên cho các sheet.
  Hướng dẫn chi tiết từng bước với mã SmartMarkerProcessor và các thực tiễn tốt nhất.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- process excel template
- automatically name sheets
- SmartMarkerProcessor
- Excel automation C#
- worksheet data binding
language: vi
lastmod: 2026-10-10
og_description: Xử lý mẫu Excel trong C# và tự động đặt tên cho các sheet bằng SmartMarkerProcessor.
  Tham khảo hướng dẫn chi tiết này để tạo sổ làm việc động.
og_image_alt: Screenshot showing process excel template with automatically named sheets
  in a C# application
og_title: Xử lý mẫu Excel và tự động đặt tên cho các sheet trong C# – hướng dẫn đầy
  đủ
schemas:
- author: GroupDocs
  dateModified: '2026-10-10'
  description: Learn how to process Excel template in C# while automatically name
    sheets. Step‑by‑step guide with SmartMarkerProcessor code and best practices.
  headline: How to process Excel template and automatically name sheets in C#
  type: TechArticle
- description: Learn how to process Excel template in C# while automatically name
    sheets. Step‑by‑step guide with SmartMarkerProcessor code and best practices.
  name: How to process Excel template and automatically name sheets in C#
  steps:
  - name: Large data sets
    text: 'When the data source contains hundreds of rows, the processor creates a
      separate sheet for each row by default. To keep the workbook from exploding,
      you can:'
  - name: Existing sheet name conflicts
    text: If the template already contains a sheet named `Detail`, the processor appends
      a numeric suffix to avoid collision (`Detail_0`, `Detail_1`, …). To enforce
      a custom conflict‑resolution strategy, inspect `Worksheet.Sheets` before processing
      and rename any conflicting sheets.
  - name: Non‑Excel templates
    text: The same `SmartMarkerProcessor` can process Word, PowerPoint, or PDF templates.
      The only change is the class you instantiate (`Document`, `Presentation`, etc.).
      The **process excel template** pattern stays identical, which means you can
      reuse the code with minimal adjustments.
  type: HowTo
tags:
- Excel
- C#
- SmartMarker
- Automation
title: Cách xử lý mẫu Excel và tự động đặt tên cho các sheet trong C#
url: /vi/net/templates-reporting/how-to-process-excel-template-and-automatically-name-sheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách xử lý mẫu Excel và tự động đặt tên các sheet trong C#

Nếu bạn cần **xử lý mẫu Excel** trong một ứng dụng .NET, hướng dẫn này sẽ cho bạn cách đáng tin cậy để tạo workbook và **tự động đặt tên các sheet**. Sử dụng `SmartMarkerProcessor` của GroupDocs.Parser, bạn có thể gắn dữ liệu vào mẫu, tạo các sheet chi tiết một cách động, và giữ cho workbook gọn gàng mà không cần đổi tên thủ công.

Bạn sẽ hoàn thành tutorial với một ví dụ có thể chạy được đầy đủ, đọc một mẫu, áp dụng nguồn dữ liệu, và tạo các sheet có tên `Detail`, `Detail_1`, `Detail_2`, … Tất cả các namespace cần thiết, các bước cấu hình, và những lỗi thường gặp đều được đề cập, để bạn có thể sao chép mã vào dự án của mình một cách tự tin.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* .NET 6.0 hoặc mới hơn (mã hoạt động với .NET Core và .NET Framework)
* Tham chiếu tới gói NuGet **GroupDocs.Parser** (phiên bản 23.5 hoặc mới hơn)
* Một mẫu Excel (`Template.xlsx`) chứa các thẻ SmartMarker như `{{Table}}` cho dữ liệu master‑detail
* Một mô hình dữ liệu đơn giản (ví dụ: `DataTable` hoặc danh sách các đối tượng) khớp với các thẻ trong mẫu

Nếu bất kỳ mục nào ở trên còn thiếu, hãy cài đặt gói NuGet bằng:

```bash
dotnet add package GroupDocs.Parser
```

## Tổng quan về giải pháp

Giải pháp bao gồm ba giai đoạn logic:

1. **Tạo một thể hiện `SmartMarkerProcessor`** – đối tượng này điều khiển toàn bộ engine templating.
2. **Cấu hình bộ xử lý để tự động đặt tên các sheet chi tiết** – tùy chọn `DetailSheetNewName` xác định tên cơ sở và thư viện sẽ thêm hậu tố tăng dần.
3. **Thực thi `Process`** – phương thức đọc mẫu, hợp nhất nguồn dữ liệu, và ghi kết quả vào một workbook mới.

Mỗi giai đoạn được giải thích dưới đây, kèm theo đoạn mã chính xác mà bạn cần.

## Bước 1: Tạo một thể hiện SmartMarkerProcessor

Bộ xử lý là điểm vào cho tất cả các thao tác SmartMarker. Nó không yêu cầu bất kỳ đối số khởi tạo nào, nhưng bạn có thể truyền một đối tượng `SmartMarkerOptions` tùy chỉnh sau này nếu cần các cài đặt nâng cao.

```csharp
using GroupDocs.Parser;
using GroupDocs.Parser.Options;

// ...

// Step 1: Instantiate the processor
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

*Lý do quan trọng*: Khởi tạo bộ xử lý một lần cho mỗi thao tác giúp giảm mức sử dụng bộ nhớ và cho phép bạn tái sử dụng cùng một đối tượng cho nhiều mẫu nếu cần.

## Bước 2: Cấu hình tự động đặt tên sheet

Khi một bảng master‑detail mở rộng thành các worksheet riêng biệt, thư viện sẽ tự động tạo các sheet mới. Bằng cách thiết lập `DetailSheetNewName`, bạn kiểm soát tên cơ sở mà engine sẽ sử dụng. Thư viện sẽ thêm dấu gạch dưới và một số tăng dần cho mỗi sheet bổ sung.

```csharp
// Step 2: Define the base name for automatically created detail sheets
processor.Options.DetailSheetNewName = "Detail"; // Sheets become Detail, Detail_1, Detail_2, …
```

*Mẹo*:

* Chọn một tên cơ sở không trùng với các tên sheet đã tồn tại trong mẫu.
* Scheme đặt tên hoạt động với bất kỳ số lượng dòng chi tiết nào; thư viện sẽ ngừng thêm hậu tố khi sheet cuối cùng được tạo.
* Nếu bạn cần một mẫu đặt tên khác (ví dụ: tiền tố thay vì hậu tố), bạn có thể thao tác `processor.Options.DetailSheetNewName` trước mỗi lần gọi.

## Bước 3: Xử lý worksheet với nguồn dữ liệu

Phương thức `Process` nhận ba đối số:

* **worksheet nguồn** (`Worksheet` object) – bạn lấy nó bằng cách tải file mẫu.
* **luồng đích** – nơi workbook đã xử lý sẽ được ghi.
* **nguồn dữ liệu** – bất kỳ đối tượng nào triển khai `IDataSource` (ví dụ: `DataTable`, `IEnumerable<T>`).

Dưới đây là một ví dụ hoàn chỉnh tải `Template.xlsx`, gắn một `DataTable`, và lưu kết quả vào `Result.xlsx`.

```csharp
using System.Data;
using System.IO;
using GroupDocs.Parser;
using GroupDocs.Parser.Data;
using GroupDocs.Parser.Options;

// ...

// Load the Excel template into a Worksheet object
using (FileStream templateStream = File.OpenRead("Template.xlsx"))
{
    // Create a Worksheet instance from the template
    Worksheet ws = new Worksheet(templateStream);

    // Prepare a simple DataTable as the data source
    DataTable dt = new DataTable("Employees");
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Department", typeof(string));
    dt.Columns.Add("Salary", typeof(decimal));

    // Populate the table with sample rows
    dt.Rows.Add("Alice", "Engineering", 95000);
    dt.Rows.Add("Bob", "Marketing", 72000);
    dt.Rows.Add("Charlie", "Sales", 68000);

    // Wrap the DataTable in a DataSource object required by SmartMarker
    IDataSource dataSource = new DataTableSource(dt);

    // Step 1 and Step 2 have already been performed earlier
    // Now process the worksheet
    using (MemoryStream resultStream = new MemoryStream())
    {
        processor.Process(ws, dataSource, resultStream);

        // Write the processed workbook to a physical file
        File.WriteAllBytes("Result.xlsx", resultStream.ToArray());
    }
}
```

*Giải thích các dòng quan trọng*:

* `new Worksheet(templateStream)` đọc file Excel và tạo một biểu diễn trong bộ nhớ mà SmartMarker có thể thao tác.
* `DataTableSource` triển khai `IDataSource`, cho phép bộ xử lý duyệt các dòng và thay thế các thẻ như `{{Employees.Name}}`.
* `processor.Process(ws, dataSource, resultStream)` hợp nhất dữ liệu và ghi workbook cuối cùng vào `resultStream`. Phương thức tự động tạo các sheet chi tiết có tên `Detail`, `Detail_1`, … nhờ tùy chọn đã thiết lập ở Bước 2.
* Sau khi xử lý, kết quả được lưu dưới dạng `Result.xlsx`. Mở file trong Excel để xác nhận rằng ba sheet chi tiết tồn tại, mỗi sheet chứa các dòng từ bảng `Employees`.

## Xác minh đầu ra

Mở `Result.xlsx` và kiểm tra các mục sau:

| Tên sheet | Nội dung dự kiến |
|------------|------------------|
| Detail | Dòng tiêu đề (`Name`, `Department`, `Salary`) và dòng dữ liệu đầu tiên (`Alice`) |
| Detail_1 | Dòng dữ liệu thứ hai (`Bob`) |
| Detail_2 | Dòng dữ liệu thứ ba (`Charlie`) |

Nếu các sheet xuất hiện với tên cơ sở đúng và hậu tố tăng dần, quy trình **process excel template** đã thành công và tính năng **automatically name sheets** hoạt động như mong đợi.

## Xử lý các trường hợp đặc biệt

### Bộ dữ liệu lớn

Khi nguồn dữ liệu chứa hàng trăm dòng, bộ xử lý sẽ tạo một sheet riêng cho mỗi dòng theo mặc định. Để tránh workbook trở nên quá lớn, bạn có thể:

* **Nhóm các dòng**: chỉnh sửa mẫu để sử dụng một thẻ bảng lặp lại trong cùng một sheet thay vì tạo sheet mới cho mỗi dòng.
* **Giới hạn việc tạo sheet**: đặt `processor.Options.MaxDetailSheets` thành một số hợp lý (ví dụ: 50) và xử lý phần dư thủ công.

```csharp
processor.Options.MaxDetailSheets = 50; // Prevent more than 50 auto‑generated sheets
```

### Xung đột tên sheet hiện có

Nếu mẫu đã chứa một sheet có tên `Detail`, bộ xử lý sẽ thêm hậu tố số để tránh trùng lặp (`Detail_0`, `Detail_1`, …). Để áp dụng chiến lược giải quyết xung đột tùy chỉnh, hãy kiểm tra `Worksheet.Sheets` trước khi xử lý và đổi tên bất kỳ sheet nào bị trùng.

```csharp
foreach (var sheet in ws.Sheets)
{
    if (sheet.Name.Equals("Detail", StringComparison.OrdinalIgnoreCase))
    {
        sheet.Name = "BaseDetail";
    }
}
```

### Mẫu không phải Excel

Cùng một `SmartMarkerProcessor` có thể xử lý các mẫu Word, PowerPoint hoặc PDF. Điều duy nhất thay đổi là lớp bạn khởi tạo (`Document`, `Presentation`, …). Mẫu **process excel template** vẫn giống hệt, nghĩa là bạn có thể tái sử dụng mã với tối thiểu điều chỉnh.

## Mẹo chuyên nghiệp cho môi trường production

* **Tái sử dụng bộ xử lý**: Tạo một singleton `SmartMarkerProcessor` nếu bạn xử lý nhiều mẫu trong một dịch vụ web. Điều này giảm chi phí cấp phát.
* **Dùng stream thay cho file**: Trong các kịch bản tải cao, giữ cả mẫu và kết quả trong memory stream để tránh I/O đĩa.
* **Giải phóng tài nguyên**: Tất cả các instance `Worksheet`, `FileStream`, và `MemoryStream` đều triển khai `IDisposable`. Sử dụng khối `using` như trong ví dụ để đảm bảo giải phóng đúng cách.
* **Ghi log**: Bật `processor.Options.Logging` để thu thập thông tin xử lý chi tiết, giúp chẩn đoán lỗi mẫu nhanh hơn.

## Ví dụ hoàn chỉnh có thể chạy được

Dưới đây là toàn bộ chương trình được biên dịch thành một file duy nhất. Sao chép nó vào một dự án console và chạy; workbook kết quả sẽ xuất hiện trong thư mục dự án.

```csharp
using System;
using System.Data;
using System.IO;
using GroupDocs.Parser;
using GroupDocs.Parser.Data;
using GroupDocs.Parser.Options;

class ExcelTemplateProcessor
{
    static void Main()
    {
        // 1️⃣ Create the processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 2️⃣ Set automatic sheet naming
        processor.Options.DetailSheetNewName = "Detail";

        // Load the template
        using (FileStream templateStream = File.OpenRead("Template.xlsx"))
        {
            Worksheet ws = new Worksheet(templateStream);

            // Build a sample data source
            DataTable dt = new DataTable("Employees");
            dt.Columns.Add("Name", typeof(string));
            dt.Columns.Add("Department", typeof(string));
            dt.Columns.Add("Salary", typeof(decimal));
            dt.Rows.Add("Alice", "Engineering", 95000);
            dt.Rows.Add("Bob", "Marketing", 72000);
            dt.Rows.Add("Charlie", "Sales", 68000);
            IDataSource dataSource = new DataTableSource(dt);

            // 3️⃣ Process the worksheet
            using (MemoryStream resultStream = new MemoryStream())
            {
                processor.Process(ws, dataSource, resultStream);
                File.WriteAllBytes("Result.xlsx", resultStream.ToArray());
            }
        }

        Console.WriteLine("Processing complete. Check Result.xlsx.");
    }
}
```

Khi chạy chương trình sẽ in “Processing complete. Check Result.xlsx.” và tạo một file Excel minh họa quy trình **process excel template** với **automatically name sheets**.

## Kết luận

Bạn đã biết cách **process Excel template** trong C# đồng thời cho phép thư viện **automatically name sheets** dựa trên một tên cơ sở tùy chỉnh. Tutorial đã bao gồm việc tạo bộ xử lý, cấu hình tùy chọn, gắn dữ liệu và các bước xác minh, cùng với xử lý các trường hợp đặc biệt và mẹo production. Áp dụng cùng một mẫu cho các dự án lớn hơn, tích hợp vào API web, hoặc mở rộng sang các định dạng Office khác.

**Các bước tiếp theo** bạn có thể khám phá:

* Sử dụng `processor.Options.DetailSheetNewName` với giá trị động (ví dụ: bao gồm ngày tháng hoặc ID người dùng).
* Kết hợp nhiều nguồn dữ liệu để tạo cấu trúc master‑detail trên nhiều worksheet.
* Thử nghiệm việc định dạng các thẻ SmartMarker để kiểm soát phông chữ, màu sắc và định dạng số trực tiếp từ mẫu.

Chúc bạn lập trình vui vẻ và tận hưởng việc tự động hoá Excel một cách mượt mà!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã mẫu đầy đủ với các giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Create Excel from Template – Step‑by‑Step Guide for .NET Developers](/cells/english/net/templates-reporting/create-excel-from-template-step-by-step-guide-for-net-develo/)
- [How to Merge and Rename Excel Sheets Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/worksheet-management/merge-rename-excel-sheets-aspose-cells-net/)
- [How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide](/cells/english/net/smart-markers-dynamic-data/how-to-link-sheets-in-excel-with-smartmarker-step-by-step-gu/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}