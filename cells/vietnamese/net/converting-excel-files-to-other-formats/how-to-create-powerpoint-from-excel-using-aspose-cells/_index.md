---
category: general
date: 2026-09-18
description: Tạo PowerPoint từ Excel bằng Aspose.Cells – sao chép bảng pivot, xuất
  các vùng dữ liệu và lưu dưới dạng PPTX chỉ trong vài dòng mã C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create powerpoint from excel
- how to copy pivot table
- copy range between workbooks
- how to export excel to pptx
- save workbook as pptx
language: vi
lastmod: 2026-09-18
og_description: Tạo PowerPoint từ Excel nhanh chóng. Tìm hiểu cách sao chép bảng pivot,
  xuất phạm vi và lưu workbook dưới dạng PPTX bằng Aspose.Cells.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel data
og_title: Tạo PowerPoint từ Excel bằng Aspose.Cells – hướng dẫn từng bước
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  headline: How to create PowerPoint from Excel using Aspose.Cells
  type: TechArticle
- description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  name: How to create PowerPoint from Excel using Aspose.Cells
  steps:
  - name: Load the source workbook and define the range
    text: You must load the workbook that holds the source data and the pivot table.
      Selecting a precise range ensures that only the needed cells are transferred,
      which keeps the resulting slide lightweight.
  - name: Prepare the destination workbook
    text: Aspose.Cells treats a PowerPoint slide as a workbook when you save it in
      PPTX format. Creating a fresh workbook gives you a clean canvas for the copied
      range.
  - name: Copy the range while preserving the pivot table
    text: The `CopyRange` method accepts a `PasteOptions` object. Setting `CopyPivotTables
      = true` tells Aspose.Cells to keep the pivot table structure intact, not just
      the rendered values.
  - name: Save the workbook as a PowerPoint file
    text: Finally, export the workbook to PPTX format. The `SaveFormat.Pptx` flag
      tells Aspose.Cells to write the worksheet as a PowerPoint slide.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel to PowerPoint
title: Cách tạo PowerPoint từ Excel bằng Aspose.Cells
url: /vi/net/converting-excel-files-to-other-formats/how-to-create-powerpoint-from-excel-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách tạo PowerPoint từ Excel bằng Aspose.Cells

Nếu bạn cần tạo PowerPoint từ Excel, hướng dẫn này sẽ cho bạn một giải pháp ngắn gọn, từ đầu đến cuối. Bạn sẽ thấy cách sao chép bảng pivot, xuất một phạm vi đã chọn, và lưu kết quả dưới dạng tệp PPTX chỉ với vài dòng C#.

Việc tạo bộ slide trực tiếp từ dữ liệu bảng tính loại bỏ bước sao chép‑dán thủ công làm chậm quy trình báo cáo. Bài học bao gồm mọi thứ bạn cần, từ thiết lập dự án đến tệp PPTX cuối cùng, và hoạt động với phiên bản mới nhất của Aspose.Cells cho .NET.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* **Aspose.Cells for .NET** (phiên bản 23.12 trở lên). Cài đặt qua NuGet: `Install-Package Aspose.Cells`.
* Môi trường phát triển **.NET 6+** (Visual Studio 2022 hoặc VS Code đều được).
* Một workbook Excel (`Source.xlsx`) chứa dữ liệu và bảng pivot bạn muốn tái sử dụng.
* Quyền ghi vào thư mục đầu ra.

Không cần thư viện bên thứ ba nào khác.

## Tạo PowerPoint từ Excel – từng bước

Quá trình bao gồm bốn bước logic tương ứng trực tiếp với ví dụ mã bạn sẽ thấy phía sau.

### Bước 1: Tải workbook nguồn và xác định phạm vi

Bạn phải tải workbook chứa dữ liệu nguồn và bảng pivot. Việc chọn một phạm vi chính xác đảm bảo chỉ các ô cần thiết được chuyển, giúp slide kết quả nhẹ hơn.

```csharp
using Aspose.Cells;
using System;

// Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// Select the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that contains the pivot table and surrounding data
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");
```

**Tại sao điều này quan trọng:**  
`CreateRange` tạo một đối tượng `Range` có thể sao chép nguyên khối. Bằng cách giới hạn phạm vi ở `A1:G20`, bạn tránh việc kéo các ô không liên quan, điều có thể làm tăng kích thước tệp PowerPoint.

### Bước 2: Chuẩn bị workbook đích

Aspose.Cells coi một slide PowerPoint như một workbook khi bạn lưu ở định dạng PPTX. Tạo một workbook mới sẽ cho bạn một canvas sạch cho phạm vi đã sao chép.

```csharp
// Create a new empty workbook that will become the PowerPoint slide
Workbook destinationWorkbook = new Workbook();

// Use the first worksheet of the new workbook
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
```

**Mẹo:** Nếu bạn cần nhiều slide, có thể thêm các worksheet bổ sung và sau đó lưu mỗi worksheet dưới dạng tệp PPTX riêng.

### Bước 3: Sao chép phạm vi đồng thời giữ nguyên bảng pivot

Phương thức `CopyRange` nhận một đối tượng `PasteOptions`. Đặt `CopyPivotTables = true` sẽ yêu cầu Aspose.Cells giữ nguyên cấu trúc bảng pivot, không chỉ giá trị đã hiển thị.

```csharp
// Copy the defined range, preserving the pivot table definition
destinationSheet.Cells.CopyRange(
    sourceRange,
    new PasteOptions { CopyPivotTables = true });
```

**Cách hoạt động:**  
Khi `CopyPivotTables` được bật, sheet đích sẽ nhận cả dữ liệu nguồn và cache của pivot. Điều này có nghĩa là bảng pivot vẫn hoạt động đầy đủ và có thể làm mới lại nếu dữ liệu nguồn thay đổi.

### Bước 4: Lưu workbook dưới dạng tệp PowerPoint

Cuối cùng, xuất workbook ra định dạng PPTX. Cờ `SaveFormat.Pptx` chỉ cho Aspose.Cells ghi worksheet dưới dạng một slide PowerPoint.

```csharp
// Save the destination workbook as a PowerPoint presentation
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);
```

**Kết quả:**  
`CopyWithPivot.pptx` mở trong Microsoft PowerPoint (hoặc bất kỳ trình xem tương thích nào) với một slide duy nhất hiển thị phạm vi đã sao chép, bao gồm cả bảng pivot sống động có thể tương tác trong PowerPoint.

## Ví dụ đầy đủ có thể chạy

Dưới đây là chương trình hoàn chỉnh mà bạn có thể dán vào một dự án console mới và chạy ngay lập tức.

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook and select the range containing the pivot table
            Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
            Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
            Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

            // 2️⃣ Create a fresh workbook that will become the PowerPoint slide
            Workbook destinationWorkbook = new Workbook();
            Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

            // 3️⃣ Copy the range, preserving the pivot table definition
            destinationSheet.Cells.CopyRange(
                sourceRange,
                new PasteOptions { CopyPivotTables = true });

            // 4️⃣ Export the workbook as a PPTX file
            destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);

            Console.WriteLine("PowerPoint file created successfully.");
        }
    }
}
```

**Kết quả mong đợi:**  
Chạy chương trình sẽ in ra “PowerPoint file created successfully.” và tạo một tệp có tên `CopyWithPivot.pptx`. Mở tệp trong PowerPoint sẽ hiển thị một slide duy nhất, trong đó phạm vi Excel đã sao chép xuất hiện chính xác như trong worksheet nguồn, kèm theo một bảng pivot hoạt động có thể làm mới từ bên trong PowerPoint.

## Các biến thể phổ biến và trường hợp đặc biệt

| Tình huống | Cần thay đổi gì |
|-----------|----------------|
| **Nhiều bảng pivot** | Định nghĩa các đối tượng `Range` riêng cho mỗi bảng và gọi `CopyRange` cho từng cái, hoặc sao chép toàn bộ sheet nếu chúng dùng cùng nguồn dữ liệu. |
| **Bộ dữ liệu lớn** | Mở rộng phạm vi (ví dụ, `"A1:Z5000"`). Xem xét bật `PasteOptions.CompressData = true` để giảm kích thước PPTX. |
| **Bố cục slide khác nhau** | Sau khi lưu dưới dạng PPTX, mở tệp trong PowerPoint và áp dụng bố cục hoặc theme tùy chỉnh; dữ liệu vẫn có thể chỉnh sửa. |
| **Lưu vào stream** | Sử dụng `destinationWorkbook.Save(stream, SaveFormat.Pptx)` khi bạn cần trả về PPTX qua một API web. |
| **Giữ định dạng ô** | Đặt `PasteOptions.PasteType = PasteType.All` để giữ phông chữ, màu sắc và viền. |

**Mẹo chuyên nghiệp:** Luôn kiểm tra xem thư mục đích có tồn tại trước khi gọi `Save`. Nếu thư mục không tồn tại, `Save` sẽ ném ra `DirectoryNotFoundException`.

## Kết luận

Bây giờ bạn đã biết cách tạo PowerPoint từ Excel, sao chép bảng pivot, và xuất kết quả dưới dạng tệp PPTX bằng Aspose.Cells. Các bước — tải workbook nguồn, xác định phạm vi, sao chép với `CopyPivotTables`, và lưu dưới dạng PPTX — bao quát toàn bộ quy trình một cách đáng tin cậy, sẵn sàng cho môi trường sản xuất.

Tiếp theo, hãy khám phá **cách xuất Excel sang PPTX** cho nhiều worksheet, hoặc tìm hiểu **cách sao chép phạm vi giữa các workbook** khi bạn cần hợp nhất dữ liệu từ nhiều nguồn trước khi tạo bộ slide. Cả hai chủ đề đều dựa trên cùng một API và có thể kết hợp để tự động hoá các pipeline báo cáo phức tạp.

Chúc lập trình vui vẻ, và tận hưởng việc biến bảng tính của bạn thành các bản trình bày chuyên nghiệp!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, dựa trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [How to Create and Save Excel Files with Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}