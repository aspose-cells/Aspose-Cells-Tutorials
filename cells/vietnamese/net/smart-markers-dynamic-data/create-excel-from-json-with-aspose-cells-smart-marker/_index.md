---
category: general
date: 2026-08-07
description: Tạo Excel từ JSON bằng Aspose.Cells Smart Marker – học cách điền dữ liệu
  vào mẫu Excel, áp dụng đặt tên sheet động và tạo nhiều trang tính.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel from json
- populate excel template
- dynamic sheet naming
- generate multiple worksheets
- aspose.cells smart marker
language: vi
lastmod: 2026-08-07
og_description: Tạo file Excel từ JSON với Aspose.Cells Smart Marker để nhanh chóng
  điền dữ liệu vào mẫu, sử dụng đặt tên sheet động và tạo nhiều worksheet.
og_image_alt: Screenshot of generated Excel workbook with multiple dynamically named
  sheets
og_title: Tạo Excel từ JSON – Hướng dẫn Aspose.Cells Smart Marker
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Create Excel from JSON using Aspose.Cells Smart Marker – learn how
    to populate an Excel template, apply dynamic sheet naming, and generate multiple
    worksheets.
  headline: Create Excel from JSON with Aspose.Cells Smart Marker
  type: TechArticle
- description: Create Excel from JSON using Aspose.Cells Smart Marker – learn how
    to populate an Excel template, apply dynamic sheet naming, and generate multiple
    worksheets.
  name: Create Excel from JSON with Aspose.Cells Smart Marker
  steps:
  - name: Define the JSON‑compatible source data
    text: '```csharp // Step 1: Define the source data that will be merged into the
      workbook var ordersData = new { Orders = new[] { new { Id = 1, Items = new[]
      { "Apple", "Banana" } }, new { Id = 2, Items = new[] { "Orange" } } } }; ```'
  - name: Prepare the workbook template and insert a Smart Marker
    text: '```csharp // Step 2: Create a new workbook and place a Smart Marker that
      references the data collection var workbook = new Workbook(); // creates an
      empty workbook workbook.Worksheets[0].Cells["A1"].PutValue("{{Orders}}"); ```'
  - name: Configure dynamic sheet naming
    text: '```csharp // Step 3: Configure how duplicated detail sheets should be named
      during processing var smartMarkerOptions = new SmartMarkerOptions { // {0} will
      be replaced by an incremental index (DetailSheet_1, DetailSheet_2, …) DetailSheetNewName
      = "DetailSheet_{0}" }; ```'
  - name: Process the template with the data and naming options
    text: '```csharp // Step 4: Process the workbook with the data and the naming
      options var smartMarkerProcessor = new SmartMarkerProcessor(workbook, smartMarkerOptions);
      smartMarkerProcessor.Process(ordersData); ```'
  - name: Save the resulting workbook
    text: '```csharp // Step 5: Save the resulting workbook – the detail sheets are
      created automatically workbook.Save("YOUR_DIRECTORY/SmartMarkerDupSheets.xlsx");
      ```'
  - name: Populate Excel template with additional fields
    text: 'If your JSON includes more properties (e.g., `CustomerName`, `TotalAmount`),
      add corresponding markers to the template:'
  - name: Generate multiple worksheets from nested collections
    text: 'You can create a second level of duplication by placing a marker inside
      the detail sheet that references a nested collection, such as `Items`:'
  - name: Custom naming with data from the record
    text: '```csharp var smartMarkerOptions = new SmartMarkerOptions { DetailSheetNewName
      = "Order_{Id}" }; ```'
  - name: Next steps
    text: '* Explore **conditional formatting** inside the detail sheet to highlight
      high‑value orders. * Replace the anonymous object with a strongly typed model
      deserialized via `System.Text.Json`. * Combine Smart Markers with **PivotTable**
      generation for advanced reporting.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Tạo Excel từ JSON bằng Aspose.Cells Smart Marker
url: /vi/net/smart-markers-dynamic-data/create-excel-from-json-with-aspose-cells-smart-marker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Excel từ JSON với Aspose.Cells Smart Marker

Nếu bạn cần **tạo Excel từ JSON**, hướng dẫn này trình bày một giải pháp hoàn chỉnh, sẵn sàng cho sản xuất. Bạn sẽ thấy cách **điền dữ liệu vào mẫu Excel**, cấu hình **đặt tên sheet động**, và **tự động tạo nhiều worksheet** bằng công cụ **Aspose.Cells Smart Marker**.

Hướng dẫn sẽ đưa bạn qua từng bước cần thiết, từ việc định nghĩa đối tượng nguồn dạng JSON tới việc lưu workbook cuối cùng. Không cần script bên ngoài, và mã chạy trên .NET 6 hoặc cao hơn.

## Những gì bạn sẽ đạt được

* Tải một đối tượng dữ liệu dạng JSON vào bộ nhớ.  
* Chèn một placeholder Smart Marker vào mẫu workbook.  
* Áp dụng mẫu đặt tên để mỗi sheet chi tiết được sao chép nhận một tên duy nhất.  
* Xử lý mẫu để tạo một worksheet riêng cho mỗi đơn hàng trong bộ sưu tập.  
* Lưu kết quả dưới dạng tệp `.xlsx` sẵn sàng cho việc tiêu thụ tiếp theo.

Yêu cầu trước: Visual Studio 2022 (hoặc bất kỳ IDE C# nào), .NET 6+, và gói NuGet **Aspose.Cells**. Ví dụ sử dụng C#; các khái niệm tương tự áp dụng cho VB.NET hoặc các ngôn ngữ .NET khác.

## Tạo Excel từ JSON – quy trình tổng thể

Các phần sau chia quy trình thành năm bước logic. Mỗi bước bao gồm mã chính xác bạn cần, giải thích lý do quan trọng và mẹo để mở rộng giải pháp.

### Bước 1: Định nghĩa dữ liệu nguồn tương thích JSON

```csharp
// Step 1: Define the source data that will be merged into the workbook
var ordersData = new
{
    Orders = new[]
    {
        new { Id = 1, Items = new[] { "Apple", "Banana" } },
        new { Id = 2, Items = new[] { "Orange" } }
    }
};
```

**Tại sao điều này quan trọng** – Đối tượng `ordersData` phản ánh cấu trúc bạn sẽ nhận được từ một API JSON thực tế. Aspose.Cells Smart Marker đọc các thuộc tính công khai, vì vậy kiểu ẩn danh hoạt động miễn là tên thuộc tính khớp với thẻ marker (`{{Orders}}`). Khi bạn sau này thay thế kiểu ẩn danh bằng đối tượng JSON đã được giải mã, không cần thay đổi mã.

### Bước 2: Chuẩn bị mẫu workbook và chèn Smart Marker

```csharp
// Step 2: Create a new workbook and place a Smart Marker that references the data collection
var workbook = new Workbook();                     // creates an empty workbook
workbook.Worksheets[0].Cells["A1"].PutValue("{{Orders}}");
```

**Tại sao điều này quan trọng** – Marker `{{Orders}}` cho trình xử lý biết lặp lại qua collection `Orders`. Đặt marker vào ô `A1` của sheet đầu tiên làm cho sheet này trở thành sheet *master*. Trình xử lý sẽ sao chép sheet này cho mỗi đơn hàng, giữ lại mọi định dạng bạn thêm sau này.

> **Mẹo:** Nếu bạn có một mẫu đã được thiết kế trước (ví dụ, có tiêu đề, công thức hoặc kiểu dáng), hãy tải nó bằng `new Workbook("Template.xlsx")` thay vì tạo một workbook trống.

### Bước 3: Cấu hình đặt tên sheet động

```csharp
// Step 3: Configure how duplicated detail sheets should be named during processing
var smartMarkerOptions = new SmartMarkerOptions
{
    // {0} will be replaced by an incremental index (DetailSheet_1, DetailSheet_2, …)
    DetailSheetNewName = "DetailSheet_{0}"
};
```

**Tại sao điều này quan trọng** – Mặc định Aspose.Cells đặt tên các sheet sao chép là `Sheet1`, `Sheet2`, v.v. Mẫu `DetailSheetNewName` chèn chỉ số tăng dần (`{0}`) để mỗi sheet nhận một tên có ý nghĩa. Bạn có thể nhúng các placeholder bổ sung (ví dụ, `{Id}`) để bao gồm dữ liệu từ bản ghi hiện tại.

> **Mẹo chuyên nghiệp:** Sử dụng `DetailSheetNewName = "Order_{Id}"` để đặt tên sheet theo định danh đơn hàng, giúp việc điều hướng dễ dàng hơn trong các workbook lớn.

### Bước 4: Xử lý mẫu với dữ liệu và tùy chọn đặt tên

```csharp
// Step 4: Process the workbook with the data and the naming options
var smartMarkerProcessor = new SmartMarkerProcessor(workbook, smartMarkerOptions);
smartMarkerProcessor.Process(ordersData);
```

**Tại sao điều này quan trọng** – `SmartMarkerProcessor` hợp nhất `ordersData` vào workbook, tạo một sheet mới cho mỗi phần tử trong `Orders`, và áp dụng mẫu đặt tên đã định nghĩa trước. Trình xử lý cũng mở rộng bất kỳ collection lồng nhau nào (ví dụ, `Items`) nếu bạn thêm các marker bổ sung bên trong sheet chi tiết.

### Bước 5: Lưu workbook kết quả

```csharp
// Step 5: Save the resulting workbook – the detail sheets are created automatically
workbook.Save("YOUR_DIRECTORY/SmartMarkerDupSheets.xlsx");
```

**Tại sao điều này quan trọng** – Phương thức `Save` ghi workbook đã được điền đầy đủ lên đĩa. Tệp hiện chứa một master sheet (có thể ẩn hoặc xóa) và một loạt các detail sheet có tên `DetailSheet_1`, `DetailSheet_2`, …, mỗi sheet chứa dữ liệu cho một đơn hàng.

#### Kết quả dự kiến

| Tên sheet        | Nội dung (đơn giản)                     |
|-------------------|------------------------------------------|
| DetailSheet_1     | Order Id = 1, Items: Apple, Banana       |
| DetailSheet_2     | Order Id = 2, Items: Orange              |

Tất cả các sheet giữ lại bất kỳ định dạng nào bạn đã áp dụng cho master sheet trước khi xử lý.

## Các biến thể nâng cao

### Điền dữ liệu vào mẫu Excel với các trường bổ sung

Nếu JSON của bạn bao gồm nhiều thuộc tính hơn (ví dụ, `CustomerName`, `TotalAmount`), hãy thêm các marker tương ứng vào mẫu:

```csharp
workbook.Worksheets[0].Cells["B1"].PutValue("{{CustomerName}}");
workbook.Worksheets[0].Cells["C1"].PutValue("{{TotalAmount}}");
```

Trình xử lý sẽ thay thế mỗi marker bằng giá trị thuộc tính tương ứng.

### Tạo nhiều worksheet từ các collection lồng nhau

Bạn có thể tạo mức sao chép thứ hai bằng cách đặt một marker bên trong detail sheet tham chiếu đến một collection lồng nhau, chẳng hạn `Items`:

```csharp
// Inside the detail sheet (e.g., cell A2)
workbook.Worksheets[0].Cells["A2"].PutValue("{{Items}}");

// Inside the same sheet, cell B2 will list each item
workbook.Worksheets[0].Cells["B2"].PutValue("{{Items}}");
```

Trong quá trình xử lý, Aspose.Cells tạo một hàng cho mỗi mục trong mảng `Items`, cho phép bạn tạo danh sách chi tiết cho mỗi đơn hàng.

### Đặt tên tùy chỉnh dựa trên dữ liệu từ bản ghi

```csharp
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheetNewName = "Order_{Id}"
};
```

Bây giờ các sheet được đặt tên `Order_1`, `Order_2`, phù hợp với định danh kinh doanh.

## Những lỗi thường gặp và cách tránh

| Vấn đề                              | Giải pháp |
|--------------------------------------|----------|
| Văn bản marker không khớp với tên thuộc tính (phân biệt chữ hoa‑thường) | Đảm bảo marker (`{{Orders}}`) khớp chính xác với thuộc tính, bao gồm cả chữ hoa‑thường. |
| Mẫu chứa các ô đã hợp nhất mở rộng qua vùng marker | Hủy hợp nhất các ô hoặc đặt marker vào một ô đơn, không hợp nhất để tránh thay đổi bố cục không mong muốn. |
| Các collection JSON lớn gây áp lực bộ nhớ | Xử lý dữ liệu theo lô hoặc stream JSON vào `DataTable` và sử dụng `SmartMarkerProcessor` với `DataSource`. |
| Đường dẫn tệp lưu không hợp lệ | Sử dụng `Path.Combine(Environment.CurrentDirectory, "output.xlsx")` hoặc kiểm tra quyền ghi. |

## Ví dụ hoàn chỉnh

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // 1️⃣ Define JSON‑compatible data
        var ordersData = new
        {
            Orders = new[]
            {
                new { Id = 1, Items = new[] { "Apple", "Banana" } },
                new { Id = 2, Items = new[] { "Orange" } }
            }
        };

        // 2️⃣ Create workbook and add master Smart Marker
        var workbook = new Workbook();
        workbook.Worksheets[0].Cells["A1"].PutValue("{{Orders}}");

        // 3️⃣ Set up dynamic sheet naming
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "DetailSheet_{0}"
        };

        // 4️⃣ Process template with data
        var processor = new SmartMarkerProcessor(workbook, smartMarkerOptions);
        processor.Process(ordersData);

        // 5️⃣ Save the result
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "SmartMarkerDupSheets.xlsx");
        workbook.Save(outputPath);
    }
}
```

Chạy chương trình sẽ tạo một tệp Excel trên desktop chứa hai detail sheet (`DetailSheet_1` và `DetailSheet_2`). Mỗi sheet phản ánh bản ghi đơn hàng tương ứng.

## Kết luận

Bây giờ bạn đã biết cách **tạo Excel từ JSON** bằng **Aspose.Cells Smart Marker**, cách **điền dữ liệu vào mẫu Excel**, áp dụng **đặt tên sheet động**, và **tự động tạo nhiều worksheet**. Mẫu này có thể mở rộng lên hàng chục hoặc hàng nghìn bản ghi, hỗ trợ các collection lồng nhau, và tích hợp liền mạch với bất kỳ thư viện giải mã JSON .NET nào.

### Các bước tiếp theo

* Khám phá **định dạng có điều kiện** trong detail sheet để làm nổi bật các đơn hàng có giá trị cao.  
* Thay thế đối tượng ẩn danh bằng mô hình kiểu mạnh được giải mã qua `System.Text.Json`.  
* Kết hợp Smart Markers với việc tạo **PivotTable** cho báo cáo nâng cao.  

Thử nghiệm với mẫu đặt tên, thêm nhiều marker hơn, và tích hợp quy trình này vào các pipeline xuất dữ liệu hiện có của bạn. Chúc lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã đầy đủ với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Tạo báo cáo Excel động bằng Aspose.Cells .NET Smart Markers](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Điền dữ liệu vào Excel bằng Aspose.Cells và Smart Markers](/cells/english/java/cell-operations/populate-excel-aspose-cells-smart-markers/)
- [Cách tạo và hợp nhất workbook Excel bằng Aspose.Cells cho Java | Hướng dẫn đầy đủ](/cells/english/java/workbook-operations/create-merge-excel-workbooks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}