---
category: general
date: 2026-08-11
description: Xuất Excel sang TXT trong C# với hướng dẫn từng bước. Tìm hiểu cách chuyển
  đổi file xlsx sang văn bản thuần bằng Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- convert xlsx to plain text
- how to export excel worksheet as text
- export worksheet as text file
language: vi
lastmod: 2026-08-11
og_description: Xuất Excel sang txt trong C# nhanh chóng. Hướng dẫn này cho thấy cách
  chuyển đổi xlsx sang văn bản thuần, cấu hình định dạng và xử lý các bảng tính lớn.
og_image_alt: Code snippet that exports an Excel worksheet to a plain text file using
  C#
og_title: Xuất Excel sang TXT trong C# – hướng dẫn chi tiết từng bước cho nhà phát
  triển
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  headline: Export excel to txt in C# – complete programming guide
  type: TechArticle
- description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  name: Export excel to txt in C# – complete programming guide
  steps:
  - name: – load the workbook
    text: '```csharp using Aspose.Cells;'
  - name: – get the first worksheet
    text: '```csharp Worksheet sheet = workbook.Worksheets[0]; ```'
  - name: – define export options for text conversion
    text: '```csharp ExportTableOptions exportOptions = new ExportTableOptions { ExportAsString
      = true, // Export all values as text DateTimeFormat = "yyyy-MM-dd", // Desired
      date format NumberFormat = "#,##0.00" // Desired numeric format }; ```'
  - name: – export worksheet as text file
    text: '```csharp // Apply the options to the worksheet sheet.ExportTableOptions
      = exportOptions;'
  type: HowTo
tags:
- excel
- csharp
- text export
- aspose.cells
title: Xuất Excel sang TXT trong C# – hướng dẫn lập trình đầy đủ
url: /vi/net/converting-excel-files-to-other-formats/export-excel-to-txt-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Xuất excel sang txt trong C# – hướng dẫn lập trình đầy đủ

Nếu bạn cần **xuất excel sang txt** bạn có thể đạt được kết quả chỉ với vài dòng mã C#. Hướng dẫn này cho thấy cách chuyển đổi một workbook `.xlsx` thành tệp plain‑text trong khi giữ nguyên định dạng dữ liệu bạn định nghĩa.

Xuất các worksheet dưới dạng tệp văn bản là một yêu cầu phổ biến khi các hệ thống hạ nguồn chỉ chấp nhận dữ liệu có dấu phân cách hoặc khi bạn cần kiểm tra giá trị thô của các ô. Trong các phần tiếp theo, bạn sẽ học cách cấu hình định dạng ngày và số, xử lý các sheet lớn, và tránh các lỗi thường gặp.

## Yêu cầu trước khi chuyển đổi xlsx sang văn bản thuần

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* .NET 6.0 (hoặc phiên bản mới hơn) đã được cài đặt – mã nguồn nhắm tới .NET Standard 2.0, vì vậy nó cũng hoạt động với .NET Framework 4.6+.
* Giấy phép cho **Aspose.Cells** (bản dùng thử miễn phí hoạt động cho việc thử nghiệm).
* Một IDE như Visual Studio 2022 hoặc Visual Studio Code.
* Một tệp Excel có tên `input.xlsx` được đặt trong thư mục mà bạn có thể tham chiếu từ dự án của mình.

Các mục này là yêu cầu bên ngoài duy nhất; hướng dẫn không phụ thuộc vào các gói NuGet bổ sung.

## Cách xuất excel sang txt bằng Aspose.Cells

Aspose.Cells cung cấp lớp `ExportTableOptions` cho phép bạn kiểm soát cách các giá trị ô được chuyển đổi thành chuỗi. Bằng cách đặt `ExportAsString` thành `true` bạn buộc mọi ô được ghi dưới dạng văn bản, điều này rất quan trọng khi bạn muốn một đầu ra plain‑text có tính quyết định.

### Bước 1 – tải workbook

```csharp
using Aspose.Cells;

string inputPath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(inputPath);
```

*Constructor `Workbook` đọc tệp Excel vào bộ nhớ. Nếu tệp không tồn tại, một ngoại lệ sẽ được ném, vì vậy bạn có thể muốn bọc lời gọi này trong khối try‑catch cho mã sản xuất.*

### Bước 2 – lấy worksheet đầu tiên

```csharp
Worksheet sheet = workbook.Worksheets[0];
```

*Worksheets được đánh chỉ số bắt đầu từ 0, vì vậy chỉ số 0 đề cập đến tab đầu tiên. Bạn có thể thay thế chỉ số bằng tên sheet (`workbook.Worksheets["Sheet1"]`) khi cần chỉ định một tab cụ thể.*

### Bước 3 – định nghĩa các tùy chọn xuất cho việc chuyển đổi văn bản

```csharp
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,               // Export all values as text
    DateTimeFormat = "yyyy-MM-dd",       // Desired date format
    NumberFormat   = "#,##0.00"          // Desired numeric format
};
```

*`ExportAsString` đảm bảo rằng mọi ô, bất kể kiểu gốc, đều trở thành chuỗi trong tệp đầu ra. Các thuộc tính `DateTimeFormat` và `NumberFormat` cho phép bạn kiểm soát cách ngày và số hiển thị, điều này quan trọng khi bạn **chuyển đổi xlsx sang plain text** cho các hệ thống yêu cầu một mẫu cụ thể.*

### Bước 4 – xuất worksheet thành tệp văn bản

```csharp
// Apply the options to the worksheet
sheet.ExportTableOptions = exportOptions;

// Export the data to a tab‑delimited text file
string outputPath = @"YOUR_DIRECTORY\Exported.txt";
sheet.ExportDataTable(outputPath);
```

*`ExportDataTable` ghi nội dung worksheet vào một tệp plain‑text sử dụng các tùy chọn bạn cung cấp. Dấu phân cách mặc định là ký tự tab (`\t`). Nếu bạn cần dấu phân cách khác, bạn có thể sử dụng overload chấp nhận một instance `ExportTableOptions` và chỉ định `ExportTableOptions.Separator`. Tệp kết quả có thể mở bằng bất kỳ trình soạn thảo văn bản nào hoặc nhập vào cơ sở dữ liệu.*

#### Đầu ra mong đợi

Giả sử `input.xlsx` chứa:

| A            | B       | C          |
|--------------|---------|------------|
| 2023‑05‑01   | 1234.5  | Sample text|

Với các tùy chọn trên tệp `Exported.txt` sẽ chứa:

```
2023-05-01	1,234.50	Sample text
```

Mỗi cột được ngăn cách bằng một ký tự tab, ngày theo định dạng `yyyy‑MM‑dd`, và số sử dụng dấu phẩy làm dấu phân cách hàng nghìn và có hai chữ số thập phân.

## Những lỗi thường gặp khi bạn xuất worksheet thành tệp văn bản

| Vấn đề | Nguyên nhân | Cách tránh |
|-------|-------------|------------|
| Định dạng số phụ thuộc vào ngôn ngữ | Định dạng mặc định tuân theo ngôn ngữ của hệ điều hành, có thể tạo ra dấu phẩy hoặc dấu chấm không nhất quán. | Đặt rõ `NumberFormat` trong `ExportTableOptions`. |
| Các hàng hoặc cột ẩn xuất hiện trong đầu ra | Aspose.Cells xuất toàn bộ phạm vi đã sử dụng, bao gồm các hàng ẩn. | Đặt `ExportTableOptions.ExportHiddenRows = false` và `ExportHiddenColumns = false` nếu bạn muốn bỏ qua chúng. |
| Worksheet lớn gây áp lực bộ nhớ | Toàn bộ workbook được tải vào bộ nhớ trước khi xuất. | Sử dụng `Workbook.LoadOptions` với `LoadDataOnly = true` để giảm sử dụng bộ nhớ, hoặc xử lý tệp theo từng phần. |
| Các ô ngày được lưu dưới dạng văn bản trong tệp nguồn | Nếu một ô đã chứa chuỗi đã định dạng, trình xuất sẽ coi nó là văn bản và bỏ qua `DateTimeFormat`. | Đảm bảo workbook nguồn lưu ngày dưới dạng kiểu ngày Excel đúng. |

Việc giải quyết các vấn đề này làm cho quá trình **cách xuất worksheet excel thành văn bản** trở nên đáng tin cậy trên các môi trường khác nhau.

## Mở rộng giải pháp – dấu phân cách tùy chỉnh và xuất dạng streaming

Nếu bạn cần một tệp giá trị phân cách bằng dấu phẩy (CSV) thay vì tệp phân cách bằng tab, hãy sửa đổi các tùy chọn:

```csharp
exportOptions.Separator = ',';
exportOptions.ExportHiddenRows = false;   // optional
exportOptions.ExportHiddenColumns = false; // optional
sheet.ExportTableOptions = exportOptions;
sheet.ExportDataTable(@"YOUR_DIRECTORY\Exported.csv");
```

Đối với các tệp lớn hơn 500 MB, việc streaming đầu ra ngăn ứng dụng tiêu thụ hết RAM:

```csharp
using (FileStream stream = new FileStream(@"YOUR_DIRECTORY\LargeExport.txt",
                                          FileMode.Create,
                                          FileAccess.Write,
                                          FileShare.None,
                                          bufferSize: 81920,
                                          useAsync: true))
{
    sheet.ExportDataTable(stream, exportOptions);
}
```

Overload chấp nhận một `Stream` ghi các hàng một cách tuần tự, rất phù hợp cho các công việc batch hoặc dịch vụ web trả về tệp văn bản trực tiếp cho client.

## Xác minh kết quả bằng chương trình

Sau khi xuất hoàn tất, bạn có thể đọc dòng đầu tiên trở lại bộ nhớ để xác nhận định dạng:

```csharp
string firstLine = File.ReadLines(outputPath).First();
Console.WriteLine($"First line: {firstLine}");
```

Chạy đoạn mã này sẽ in ra cùng một dòng như trong phần *Đầu ra mong đợi*, giúp bạn yên tâm rằng quá trình chuyển đổi đã thành công.

## Tóm tắt mã hoàn chỉnh

Kết hợp tất cả các phần lại với nhau tạo ra một chương trình tự chứa mà bạn có thể sao chép vào một ứng dụng console:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputPath  = @"YOUR_DIRECTORY\input.xlsx";
        string outputPath = @"YOUR_DIRECTORY\Exported.txt";

        // Load workbook
        Workbook workbook = new Workbook(inputPath);
        Worksheet sheet = workbook.Worksheets[0];

        // Configure export options
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            DateTimeFormat = "yyyy-MM-dd",
            NumberFormat   = "#,##0.00",
            Separator      = '\t' // tab delimiter
        };

        // Apply options and export
        sheet.ExportTableOptions = exportOptions;
        sheet.ExportDataTable(outputPath);

        // Simple verification
        string firstLine = File.ReadLines(outputPath).First();
        Console.WriteLine($"Export completed. First line: {firstLine}");
    }
}
```

Biên dịch và chạy chương trình; tệp `Exported.txt` sẽ xuất hiện trong cùng thư mục với workbook nguồn.

## Các bước tiếp theo và các chủ đề liên quan

* **Export worksheet as text file** – thử nghiệm các dấu phân cách khác nhau, các mã hoá (UTF‑8 vs. ASCII), và kiểu kết thúc dòng để đạt khả năng tương thích đa nền tảng.
* **Bulk conversion** – lặp qua `workbook.Worksheets` để tạo một tệp văn bản riêng cho mỗi tab.
* **Integration with databases** – truyền trực tiếp văn bản đã tạo vào một thao tác bulk‑insert cho SQL Server hoặc PostgreSQL.
* **

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao quát các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách Xuất Tệp Excel trong .NET Sử Dụng Aspose.Cells: Hướng Dẫn Toàn Diện](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [Cách Xuất Các Hàng Excel Có Thể Nhìn Thấy Sử Dụng Aspose.Cells cho .NET: Hướng Dẫn Từng Bước](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [Cách Xuất Biểu Đồ Excel Sang PDF Sử Dụng Aspose.Cells cho .NET: Hướng Dẫn Từng Bước](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}