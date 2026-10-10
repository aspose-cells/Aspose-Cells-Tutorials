---
category: general
date: 2026-10-10
description: Tạo dữ liệu smart marker và điền dữ liệu mẫu Excel bằng cách sử dụng
  smart markers của Aspose.Cells. Thực hiện theo hướng dẫn từng bước này để tự động
  hoá báo cáo Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create smart marker data
- fill excel template data
- use aspose.cells smart markers
language: vi
lastmod: 2026-10-10
og_description: Tạo dữ liệu smart marker với smart marker của Aspose.Cells và điền
  dữ liệu mẫu Excel trong vài phút. Hướng dẫn này sẽ dẫn bạn qua một ví dụ hoàn chỉnh,
  có thể chạy được.
og_image_alt: Screenshot showing the process of creating smart marker data in an Excel
  worksheet
og_title: Tạo dữ liệu smart marker và điền dữ liệu vào mẫu Excel
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create smart marker data and fill Excel template data using Aspose.Cells
    smart markers. Follow this step‑by‑step guide to automate Excel reports.
  headline: How to create smart marker data and fill Excel template data
  type: TechArticle
- description: Create smart marker data and fill Excel template data using Aspose.Cells
    smart markers. Follow this step‑by‑step guide to automate Excel reports.
  name: How to create smart marker data and fill Excel template data
  steps:
  - name: '**Loading the workbook** gives the processor a concrete file to work on.'
    text: '**Loading the workbook** gives the processor a concrete file to work on.'
  - name: '**Selecting the worksheet** ensures the processor scans the correct sheet;
      you can target any sheet by index or name.'
    text: '**Selecting the worksheet** ensures the processor scans the correct sheet;
      you can target any sheet by index or name.'
  - name: '**The data source** is an array of anonymous objects. Each property name
      (`fieldName`) must match the marker name inside `${Comment:fieldName}`.'
    text: '**The data source** is an array of anonymous objects. Each property name
      (`fieldName`) must match the marker name inside `${Comment:fieldName}`.'
  - name: '**`SmartMarkerProcessor`** is the engine that parses tags and performs
      the replacement.'
    text: '**`SmartMarkerProcessor`** is the engine that parses tags and performs
      the replacement.'
  - name: '**`Process`** performs the heavy lifting: it reads every `${...}` tag,
      looks up the matching property in the data source, and writes the value into
      the cell.'
    text: '**`Process`** performs the heavy lifting: it reads every `${...}` tag,
      looks up the matching property in the data source, and writes the value into
      the cell.'
  - name: '**Saving the workbook** writes the updated file to disk, ready for downstream
      consumption.'
    text: '**Saving the workbook** writes the updated file to disk, ready for downstream
      consumption.'
  - name: Open a new Excel workbook.
    text: Open a new Excel workbook.
  - name: 'In any cell where you want dynamic content, type a Smart Marker tag, for
      example:'
    text: 'In any cell where you want dynamic content, type a Smart Marker tag, for
      example:'
  - name: Save the file as `Template.xlsx`.
    text: Save the file as `Template.xlsx`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cách tạo dữ liệu smart marker và điền dữ liệu mẫu Excel
url: /vi/net/smart-markers-dynamic-data/how-to-create-smart-marker-data-and-fill-excel-template-data/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách tạo dữ liệu smart marker và điền dữ liệu mẫu Excel

Nếu bạn cần **tạo dữ liệu smart marker** cho một workbook Excel, smart markers của Aspose.Cells giúp việc này trở nên dễ dàng. Hướng dẫn này cho thấy cách **điền dữ liệu mẫu Excel** bằng smart markers chỉ trong vài dòng mã C#.

Bạn sẽ học cách nhúng các thẻ Smart Marker vào mẫu, cung cấp nguồn dữ liệu, chạy bộ xử lý và lưu file đã được điền. Không cần công cụ bên ngoài—chỉ cần Aspose.Cells cho .NET và một dự án C# cơ bản.

## Những gì bạn cần

- .NET 6.0 trở lên (mã cũng hoạt động với .NET Framework 4.7+)
- Aspose.Cells cho .NET (gói NuGet `Aspose.Cells`)
- Một workbook Excel chứa các thẻ Smart Marker như `${Comment:fieldName}`
- Một IDE C# (Visual Studio, Rider, hoặc VS Code)

> **Mẹo:** Giữ workbook trong cùng thư mục với dự án hoặc sử dụng đường dẫn tuyệt đối để tránh lỗi không tìm thấy file.

## Cách tạo dữ liệu smart marker với Aspose.Cells

Lõi của giải pháp là `SmartMarkerProcessor`. Nó quét một worksheet để tìm các thẻ, lấy các giá trị phù hợp từ nguồn dữ liệu và ghi kết quả trở lại sheet.

```csharp
using Aspose.Cells;
using System;

// 1️⃣ Load the workbook that contains Smart Marker tags.
Workbook workbook = new Workbook("Template.xlsx");

// 2️⃣ Get the worksheet where the tags reside.
Worksheet ws = workbook.Worksheets[0];

// 3️⃣ Prepare the data source that supplies values for the markers.
var dataSource = new[]
{
    new { fieldName = "Sample comment text generated by C#." }
};

// 4️⃣ Create a SmartMarkerProcessor instance.
SmartMarkerProcessor processor = new SmartMarkerProcessor();

// 5️⃣ Process the worksheet, replacing Smart Marker tags with data from the source.
processor.Process(ws, dataSource);

// 6️⃣ Save the populated workbook.
workbook.Save("Result.xlsx");
```

### Tại sao mỗi dòng lại quan trọng

1. **Loading the workbook** cung cấp cho bộ xử lý một file cụ thể để làm việc.  
2. **Selecting the worksheet** đảm bảo bộ xử lý quét đúng sheet; bạn có thể chỉ định bất kỳ sheet nào bằng chỉ số hoặc tên.  
3. **The data source** là một mảng các đối tượng ẩn danh. Mỗi tên thuộc tính (`fieldName`) phải khớp với tên marker trong `${Comment:fieldName}`.  
4. `SmartMarkerProcessor` là engine phân tích các thẻ và thực hiện việc thay thế.  
5. `Process` thực hiện công việc nặng: nó đọc mọi thẻ `${...}`, tra cứu thuộc tính phù hợp trong nguồn dữ liệu và ghi giá trị vào ô.  
6. **Saving the workbook** ghi file đã cập nhật lên đĩa, sẵn sàng cho các bước tiếp theo.

## Chuẩn bị mẫu Excel để **điền dữ liệu mẫu Excel**

1. Mở một workbook Excel mới.  
2. Trong bất kỳ ô nào bạn muốn nội dung động, nhập một thẻ Smart Marker, ví dụ:  

   ```
   ${Comment:fieldName}
   ```

3. Lưu file dưới tên `Template.xlsx`.  

Cú pháp thẻ tuân theo mẫu `${<CollectionName>:<PropertyName>}`. Trong ví dụ đơn giản này chúng ta bỏ qua tên collection và dựa vào collection mặc định, là nguồn dữ liệu được truyền vào `Process`.

> **Trường hợp đặc biệt:** Nếu thẻ tham chiếu tới một thuộc tính không tồn tại trong nguồn dữ liệu, Aspose.Cells sẽ để nguyên ô. Luôn kiểm tra rằng tên thuộc tính khớp chính xác, bao gồm cả phân biệt chữ hoa/thường.

## Xây dựng nguồn dữ liệu cho **sử dụng smart markers của Aspose.Cells**

Bạn có thể cung cấp bất kỳ collection nào có thể lặp—mảng, `List<T>`, `DataTable`, hoặc thậm chí các đối tượng tùy chỉnh. Bộ xử lý sẽ lặp qua collection và sao chép các hàng cho mỗi mục khi sử dụng marker dạng bảng.

```csharp
// Example with a List<T>
var comments = new List<Comment>
{
    new Comment { fieldName = "First comment." },
    new Comment { fieldName = "Second comment." }
};

processor.Process(ws, comments);
```

```csharp
public class Comment
{
    public string fieldName { get; set; }
}
```

Khi bạn cung cấp nhiều hàng, Aspose.Cells tự động mở rộng vùng mẫu để chứa tất cả các mục, rất hữu ích cho việc tạo báo cáo, hoá đơn, hoặc các bảng dữ liệu.

## Xử lý worksheet bằng **smart markers của Aspose.Cells**

`Process` có thể nhận các thiết lập tùy chọn, chẳng hạn như:

- `SmartMarkerOptions` để kiểm soát cách xử lý các ô trống.
- `DataSourceOptions` để chỉ định tên collection khác.

```csharp
SmartMarkerOptions options = new SmartMarkerOptions
{
    // Preserve empty cells as blanks instead of removing them.
    PreserveEmptyCells = true
};

processor.Process(ws, dataSource, options);
```

Các tùy chọn này cho phép bạn kiểm soát chi tiết việc **điền dữ liệu mẫu Excel**, đảm bảo kết quả đáp ứng yêu cầu định dạng của bạn.

## Lưu kết quả và kiểm tra đầu ra

Sau khi xử lý, bạn có thể lưu workbook ở bất kỳ định dạng nào được Aspose.Cells hỗ trợ, như XLSX, CSV, hoặc PDF.

```csharp
workbook.Save("Result.pdf", SaveFormat.Pdf);
```

Mở `Result.xlsx` (hoặc `Result.pdf`) để kiểm tra rằng placeholder `${Comment:fieldName}` đã được thay thế bằng **Sample comment text generated by C#**. Nếu ô vẫn hiển thị thẻ gốc, hãy kiểm tra lại tên thuộc tính trong nguồn dữ liệu.

## Những lỗi thường gặp và cách tránh

| Vấn đề | Nguyên nhân | Cách khắc phục |
|-------|-------------|----------------|
| Thẻ không được thay thế | Tên thuộc tính không khớp (ví dụ, `fieldname` so với `fieldName`) | Đảm bảo khớp chính xác phân biệt chữ hoa/thường |
| Các hàng không được sao chép | Nguồn dữ liệu chỉ chứa một đối tượng trong khi mẫu yêu cầu một bảng | Cung cấp một collection có nhiều mục |
| Workbook gặp lỗi khi lưu | Sử dụng phiên bản Aspose.Cells đã lỗi thời | Nâng cấp lên gói NuGet mới nhất |
| Mất định dạng | Bộ xử lý ghi đè kiểu ô | Giữ nguyên kiểu bằng `SmartMarkerOptions.PreserveCellFormatting = true` |

## Ví dụ hoạt động đầy đủ

Dưới đây là một chương trình tự chứa mà bạn có thể sao chép, dán và chạy.

```csharp
using Aspose.Cells;
using System;
using System.Collections.Generic;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // Load the template that contains the Smart Marker tag ${Comment:fieldName}
            Workbook workbook = new Workbook("Template.xlsx");
            Worksheet ws = workbook.Worksheets[0];

            // Create a list of data objects – each object maps to the marker property.
            var data = new List<Comment>
            {
                new Comment { fieldName = "First generated comment." },
                new Comment { fieldName = "Second generated comment." },
                new Comment { fieldName = "Third generated comment." }
            };

            // Initialise the processor and run it.
            SmartMarkerProcessor processor = new SmartMarkerProcessor();
            processor.Process(ws, data);

            // Save the populated workbook.
            workbook.Save("Result.xlsx");
            Console.WriteLine("Smart marker processing complete. Check Result.xlsx.");
        }
    }

    public class Comment
    {
        public string fieldName { get; set; }
    }
}
```

**Kết quả mong đợi:** Trong `Result.xlsx`, ô ban đầu chứa `${Comment:fieldName}` sẽ mở rộng thành ba hàng, mỗi hàng được điền bằng văn bản bình luận tương ứng từ danh sách `data`.

## Kết luận

Bây giờ bạn đã biết cách **tạo dữ liệu smart marker**, **điền dữ liệu mẫu Excel**, và **sử dụng smart markers của Aspose.Cells** để tự động tạo báo cáo Excel. Quy trình chỉ gồm ba bước: nhúng các thẻ Smart Marker, cung cấp nguồn dữ liệu phù hợp, và gọi `SmartMarkerProcessor.Process`. Từ đây bạn có thể khám phá các kịch bản nâng cao hơn như collection lồng nhau, định dạng có điều kiện, hoặc xuất ra PDF.

### Các bước tiếp theo

- Thử nghiệm **smart markers kiểu bảng** để tự động tạo các bảng nhiều hàng.  
- Kết hợp smart markers với **định dạng có điều kiện** để làm nổi bật các hàng đáp ứng tiêu chí nhất định.  
- Xem tài liệu Aspose.Cells về **các tùy chọn Smart Marker** để tối ưu hiệu năng.

Chúc lập trình vui vẻ, và tận hưởng thời gian tiết kiệm nhờ tự động hoá quy trình Excel của bạn!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên đều có các ví dụ mã hoàn chỉnh kèm giải thích chi tiết từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Tự động hoá workbook Excel với Aspose.Cells .NET: Sử dụng Smart Markers để xử lý dữ liệu hiệu quả](/cells/english/net/automation-batch-processing/automate-excel-aspose-cells-workbook-smart-markers/)
- [Thành thạo Smart Markers & tích hợp DataTable của Aspose.Cells .NET để quản lý dữ liệu hiệu quả trong Excel](/cells/english/net/import-export/aspose-cells-net-smart-markers-data-table-integration/)
- [Kết hợp dữ liệu Excel trong C# – Hướng dẫn Smart Marker toàn diện](/cells/english/net/smart-markers-dynamic-data/excel-data-merging-in-c-complete-smart-marker-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}