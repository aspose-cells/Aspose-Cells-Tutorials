---
category: general
date: 2026-11-16
description: Cách sao chép bảng tổng hợp từ một tệp Excel sang một workbook mới bằng
  C#. Tìm hiểu cách tải workbook, sao chép vùng dữ liệu và giữ nguyên bảng tổng hợp.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to new workbook
- load excel workbook c#
- Aspose.Cells copy pivot
- preserve pivot table C#
- Excel automation C#
language: vi
lastmod: 2026-11-16
og_description: Cách sao chép bảng tổng hợp từ một workbook hiện có sang workbook
  mới bằng C#. Theo dõi hướng dẫn đầy đủ này để tải workbook Excel, sao chép vùng
  dữ liệu và giữ nguyên bảng tổng hợp.
og_image_alt: how to copy pivot table example in C#
og_title: Cách sao chép bảng pivot sang một bảng tính mới trong C# – hướng dẫn từng
  bước
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy pivot table from one Excel file to a new workbook using
    C#. Learn to load workbook, copy range, and preserve pivot tables.
  headline: How to copy a pivot table to a new workbook in C#
  type: TechArticle
- description: How to copy pivot table from one Excel file to a new workbook using
    C#. Learn to load workbook, copy range, and preserve pivot tables.
  name: How to copy a pivot table to a new workbook in C#
  steps:
  - name: Expected output
    text: 'Running the program produces `CopyWithPivot.xlsx`. Opening the file in
      Excel shows:'
  - name: Copying multiple pivot tables
    text: If your source sheet contains several pivots, expand the `CellArea` to cover
      the union of all ranges, or repeat the copy step for each distinct area.
  - name: Preserving styles and conditional formatting
    text: '`CopyRows` copies cell styles automatically. If you need to preserve workbook‑wide
      named styles or custom number formats, call `destWorkbook.Worksheets[0].CopyStyle`
      before saving.'
  - name: Working with large workbooks
    text: For files larger than 100 MB, consider using `Workbook.LoadOptions` with
      the `MemorySetting` set to `MemorySetting.MemoryPreference` to reduce memory
      pressure.
  - name: Next steps
    text: '* Explore **Aspose.Cells** features such as refreshing pivots programmatically.
      * Combine this approach with **ExcelPackage** (EPPlus) if you need an open‑source
      alternative. * Automate copying across multiple sheets by looping through `srcWorkbook.Worksheets`.'
  type: HowTo
- questions:
  - answer: Aspose.Cells can read macro‑enabled files (`.xlsm`), but the macro code
      isn’t copied. The pivot table itself is preserved because it’s part of the worksheet
      XML.
    question: Does this work with macros or VBA‑enabled workbooks?
  - answer: The copy operation includes the cached data only. If the destination workbook
      needs to refresh from the original source, you’ll have to re‑configure the data
      connection manually.
    question: What if the pivot uses an external data source?
  - answer: 'No. A pivot table needs its cache. The most reliable way is to copy the
      rows that contain the cache, as demonstrated. You can later hide those rows
      if you don’t want them visible. ## Conclusion You now know **how to copy pivot
      table** from one Excel file to another using C#. The tutorial covered **l'
    question: Can I copy the pivot without the underlying data rows?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Cách sao chép bảng pivot vào một workbook mới trong C#
url: /vi/net/pivot-tables/how-to-copy-a-pivot-table-to-a-new-workbook-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách sao chép pivot table vào một workbook mới trong C#

Nếu bạn cần **cách sao chép pivot table** từ một tệp Excel sang một workbook mới, hướng dẫn này sẽ chỉ cho bạn các bước cụ thể. Bạn sẽ học cách **load excel workbook c#**, xác định phạm vi nguồn, và **copy range to new workbook** trong khi giữ nguyên pivot.

Sao chép một pivot table là nhu cầu phổ biến khi bạn muốn tái sử dụng mẫu báo cáo, di chuyển dữ liệu giữa các dự án, hoặc tạo một tệp nhẹ để phân phối. Đoạn mã mẫu dưới đây sử dụng Aspose.Cells, một thư viện .NET hoàn toàn quản lý mà không cần cài đặt Microsoft Office. Khi kết thúc tutorial, bạn sẽ có một chương trình chạy được tạo ra một workbook mới chứa pivot table gốc, sẵn sàng cho các xử lý hoặc chia sẻ tiếp theo.

## Yêu cầu trước

* .NET 6.0 SDK hoặc phiên bản mới hơn (ví dụ hoạt động với .NET Core và .NET Framework)
* Visual Studio 2022 hoặc bất kỳ trình chỉnh sửa C# nào bạn thích
* Giấy phép Aspose.Cells for .NET (bản dùng thử miễn phí dùng để đánh giá)
* Tệp Excel nguồn (`Source.xlsx`) chứa ít nhất một pivot table

> **Mẹo:** Nếu bạn đang sử dụng bản dùng thử miễn phí, hãy thiết lập giấy phép trong mã để tránh các dấu bản quyền đánh giá.

## Bước 1: Tải workbook nguồn (load excel workbook c#)

Hành động đầu tiên là mở workbook chứa pivot table. Aspose.Cells đọc tệp vào bộ nhớ, cho phép bạn truy cập đầy đủ vào các worksheet, ô và đối tượng pivot.

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Load the source workbook that contains the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY\Source.xlsx");
```

*​Tại sao điều này quan trọng*: Việc tải workbook là nền tảng cho mọi tự động hóa Excel. Nếu không có đối tượng `Workbook` hợp lệ, bạn không thể kiểm tra pivot hoặc sao chép dữ liệu của nó.

## Bước 2: Xác định vùng ô bao quanh pivot table (copy range to new workbook)

Pivot table nằm trong một khối ô hình chữ nhật. Bạn phải chỉ định khối này để thao tác sao chép biết phải di chuyển gì. Hàm tạo `CellArea` sử dụng chỉ mục bắt đầu từ 0: `StartRow, StartColumn, EndRow, EndColumn`.

```csharp
        // Define the cell range that encloses the pivot table, e.g., A1:K21
        // Row and column indexes start at 0, so A1 = (0,0)
        CellArea sourceRange = new CellArea(0, 0, 20, 10); // A1:K21
```

*​Tại sao điều này quan trọng*: Bằng cách đặt phạm vi một cách rõ ràng, bạn tránh sao chép dữ liệu không liên quan và đảm bảo cache của pivot được bao gồm. Phạm vi có thể được tính toán động nếu bạn cần xử lý các kích thước pivot khác nhau.

## Bước 3: Tạo workbook mới và lấy worksheet đầu tiên

Bây giờ tạo workbook đích sẽ nhận các hàng đã sao chép. Aspose.Cells tự động thêm một worksheet mặc định, chúng ta sẽ dùng nó làm mục tiêu.

```csharp
        // Create a new workbook that will receive the copied range
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*​Tại sao điều này quan trọng*: Bắt đầu với một workbook sạch sẽ đảm bảo chỉ có pivot table (và các hàng hỗ trợ) xuất hiện trong tệp, giữ cho đầu ra nhẹ nhàng.

## Bước 4: Sao chép các hàng từ phạm vi nguồn sang sheet đích (how to copy pivot table)

Phương thức `CopyRows` sao chép toàn bộ hàng, giữ lại công thức, định dạng và—đặc biệt—pivot table. Các tham số của phương thức là: hàng bắt đầu, hàng kết thúc, bộ sưu tập ô đích, và chỉ số hàng trong đích nơi bắt đầu sao chép (ở đây `0` để bắt đầu từ hàng đầu tiên).

```csharp
        // Copy the rows that contain the pivot table.
        // Pivot tables inside the range are preserved automatically.
        destWorksheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            destWorksheet.Cells,
            0);
```

*​Tại sao điều này quan trọng*: Sử dụng `CopyRows` thay vì sao chép từng ô riêng lẻ giúp cache của pivot vẫn được liên kết với dữ liệu đã sao chép. Aspose.Cells xử lý các cấu trúc XML bên dưới, vì vậy bạn không cần tự xây dựng lại pivot.

## Bước 5: Lưu workbook kết quả (copy range to new workbook)

Cuối cùng, ghi tệp mới ra đĩa. Workbook đích bây giờ chứa một pivot table giống hệt, hoạt động độc lập với tệp nguồn.

```csharp
        // Save the new workbook with the copied pivot table
        destWorkbook.Save(@"YOUR_DIRECTORY\CopyWithPivot.xlsx");

        // Optional: inform the user
        System.Console.WriteLine("Pivot table copied successfully!");
    }
}
```

### Kết quả mong đợi

Chạy chương trình sẽ tạo ra `CopyWithPivot.xlsx`. Mở tệp trong Excel sẽ hiển thị:

* Bố cục pivot table giống như trong `Source.xlsx`
* Tất cả các hàng dữ liệu nguồn đã nằm trong cache của pivot
* Không có tham chiếu nào tới workbook gốc (pivot hoạt động offline)

## Xử lý các biến thể phổ biến

### Sao chép nhiều pivot table

Nếu sheet nguồn của bạn chứa nhiều pivot, mở rộng `CellArea` để bao phủ hợp nhất tất cả các phạm vi, hoặc lặp lại bước sao chép cho mỗi vùng riêng biệt.

```csharp
// Example: copy two separate ranges
CellArea firstPivot = new CellArea(0, 0, 20, 10);
CellArea secondPivot = new CellArea(25, 0, 45, 10);

destWorksheet.Cells.CopyRows(firstPivot.StartRow, firstPivot.EndRow, destWorksheet.Cells, 0);
destWorksheet.Cells.CopyRows(secondPivot.StartRow, secondPivot.EndRow, destWorksheet.Cells, 21); // start after first block
```

### Bảo tồn kiểu dáng và định dạng có điều kiện

`CopyRows` tự động sao chép kiểu dáng ô. Nếu bạn cần bảo tồn các kiểu đặt tên trên toàn workbook hoặc định dạng số tùy chỉnh, hãy gọi `destWorkbook.Worksheets[0].CopyStyle` trước khi lưu.

### Làm việc với workbook lớn

Đối với các tệp lớn hơn 100 MB, hãy cân nhắc sử dụng `Workbook.LoadOptions` với `MemorySetting` được đặt thành `MemorySetting.MemoryPreference` để giảm áp lực bộ nhớ.

```csharp
LoadOptions loadOptions = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook largeSrc = new Workbook(@"bigfile.xlsx", loadOptions);
```

## Mã nguồn đầy đủ (sẵn sàng chạy)

Dưới đây là chương trình hoàn chỉnh, bao gồm các chỉ thị `using` và chú thích. Sao chép nó vào một dự án console mới và thay thế `YOUR_DIRECTORY` bằng đường dẫn thư mục thực tế.

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the source workbook (load excel workbook c#)
        // -------------------------------------------------
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY\Source.xlsx");

        // -------------------------------------------------
        // Step 2: Define the area that contains the pivot table
        // -------------------------------------------------
        // Adjust the indices if your pivot occupies a different range.
        CellArea sourceRange = new CellArea(0, 0, 20, 10); // A1:K21

        // -------------------------------------------------
        // Step 3: Create the destination workbook
        // -------------------------------------------------
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // -------------------------------------------------
        // Step 4: Copy rows (how to copy pivot table)
        // -------------------------------------------------
        destWorksheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            destWorksheet.Cells,
            0);

        // -------------------------------------------------
        // Step 5: Save the new file (copy range to new workbook)
        // -------------------------------------------------
        destWorkbook.Save(@"YOUR_DIRECTORY\CopyWithPivot.xlsx");

        Console.WriteLine("Pivot table copied successfully!");
    }
}
```

Chạy chương trình (`dotnet run` hoặc `Ctrl+F5` trong Visual Studio). Sau khi thực thi, mở `CopyWithPivot.xlsx` để xác nhận pivot hoạt động giống hệt như bản gốc.

## Câu hỏi thường gặp

**Q: Điều này có hoạt động với các workbook có macro hoặc VBA‑enabled không?**  
A: Aspose.Cells có thể đọc các tệp có macro (`.xlsm`), nhưng mã macro sẽ không được sao chép. Pivot table vẫn được bảo tồn vì nó là một phần của XML worksheet.

**Q: Nếu pivot sử dụng nguồn dữ liệu bên ngoài thì sao?**  
A: Hoạt động sao chép chỉ bao gồm dữ liệu đã được cache. Nếu workbook đích cần làm mới từ nguồn gốc, bạn sẽ phải cấu hình lại kết nối dữ liệu theo cách thủ công.

**Q: Tôi có thể sao chép pivot mà không sao chép các hàng dữ liệu nền không?**  
A: Không. Pivot table cần cache của nó. Cách đáng tin cậy nhất là sao chép các hàng chứa cache, như đã minh họa. Bạn có thể ẩn các hàng này sau khi sao chép nếu không muốn chúng hiển thị.

## Kết luận

Bạn giờ đã biết **cách sao chép pivot table** từ một tệp Excel sang tệp khác bằng C#. Tutorial đã đề cập đến **load excel workbook c#**, xác định **copy range to new workbook**, và sử dụng phương thức `CopyRows` của Aspose.Cells để giữ nguyên pivot. Với ví dụ hoàn chỉnh, có thể tích hợp mẫu này vào các pipeline báo cáo, công cụ xuất tự động, hoặc bất kỳ kịch bản nào mà pivot cần di chuyển giữa các workbook.

### Các bước tiếp theo

* Khám phá các tính năng của **Aspose.Cells** như làm mới pivot một cách lập trình.  
* Kết hợp cách tiếp cận này với **ExcelPackage** (EPPlus) nếu bạn cần một giải pháp mã nguồn mở.  
* Tự động sao chép qua nhiều sheet bằng cách lặp qua `srcWorkbook.Worksheets`.  

Hãy tự do thử nghiệm với các phạm vi khác nhau, thêm kiểu dáng tùy chỉnh, hoặc nhúng logic này vào một dịch vụ xử lý dữ liệu lớn hơn. Chúc bạn lập trình vui!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã đầy đủ với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Tạo Workbook mới trong C# – Sao chép Pivot Table](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)
- [Cách sao chép pivot table trong Excel với C# và Aspose.Cells](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/)
- [Sao chép pivot table vào workbook mới, xuất shape sang PowerPoint](/cells/english/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}