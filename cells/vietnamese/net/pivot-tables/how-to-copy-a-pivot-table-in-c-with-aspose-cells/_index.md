---
category: general
date: 2026-09-27
description: Tìm hiểu cách sao chép bảng pivot trong C# bằng Aspose.Cells. Bao gồm
  sao chép các hàng có định dạng, sao chép bảng pivot sang sheet khác và xuất bảng
  pivot ra một workbook mới.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy rows with formatting
- copy pivot table to another sheet
- how to copy excel rows
- export pivot table to new workbook
language: vi
lastmod: 2026-09-27
og_description: Cách sao chép bảng tổng hợp trong C# bằng Aspose.Cells. Tham khảo
  hướng dẫn chi tiết từng bước để sao chép các hàng kèm định dạng, di chuyển bảng
  tổng hợp sang sheet khác và xuất nó ra một workbook mới.
og_image_alt: Excel sheet showing a copied pivot table after using Aspose.Cells
og_title: Cách sao chép bảng tổng hợp trong C# – hướng dẫn đầy đủ Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to copy a pivot table in C# using Aspose.Cells. Includes
    copy rows with formatting, copy pivot table to another sheet, and export pivot
    table to a new workbook.
  headline: How to copy a pivot table in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot table
title: Cách sao chép bảng tổng hợp trong C# bằng Aspose.Cells
url: /vi/net/pivot-tables/how-to-copy-a-pivot-table-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách sao chép Pivot Table trong C# với Aspose.Cells

Nếu bạn cần **sao chép một pivot table** từ một worksheet sang worksheet khác, việc học **cách sao chép pivot table** trong C# với Aspose.Cells có thể giúp bạn tiết kiệm hàng giờ công việc thủ công. Cách tiếp cận này cũng cho phép bạn **sao chép các hàng với định dạng**, giữ nguyên pivot cache, và thậm chí **xuất pivot table ra một workbook mới** khi bạn cần một tệp độc lập.

Hướng dẫn này sẽ đưa bạn qua toàn bộ quy trình:

* tạo một workbook,  
* sao chép phạm vi pivot‑table trong khi giữ nguyên định dạng,  
* đặt dữ liệu đã sao chép vào một sheet mới, và  
* lưu kết quả dưới dạng một tệp riêng.

Bạn sẽ thấy tại sao phương thức tích hợp sẵn `CopyRows` là cách đáng tin cậy nhất để **sao chép pivot table sang sheet khác**, và sẽ nhận được các mẹo để xử lý các trường hợp đặc biệt như hàng ẩn hoặc nguồn dữ liệu bên ngoài.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

| Yêu cầu | Lý do quan trọng |
|-------------|----------------|
| .NET 6.0 hoặc mới hơn | Aspose.Cells hỗ trợ .NET 6+ và mang lại hiệu năng tốt nhất. |
| Visual Studio 2022 (hoặc bất kỳ IDE C# nào) | Bạn cần một trình soạn thảo có thể khôi phục các gói NuGet. |
| Aspose.Cells for .NET (gói NuGet `Aspose.Cells`) | Thư viện này cung cấp API `CopyRows` được sử dụng trong ví dụ. |
| Tệp Excel nguồn (`source.xlsx`) chứa một pivot table trong phạm vi `A1:G20` | Mã sẽ sao chép phạm vi cụ thể này; hãy điều chỉnh phạm vi nếu pivot table của bạn lớn hơn. |

Cài đặt thư viện bằng NuGet CLI hoặc Package Manager Console:

```bash
dotnet add package Aspose.Cells
```

## Bước 1: Tải workbook chứa pivot table

Dòng đầu tiên tạo một đối tượng `Workbook` đại diện cho toàn bộ tệp Excel. Việc tải tệp một lần cho phép bạn đọc/ghi vào mọi worksheet.

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Tại sao bước này quan trọng** – Nếu không tải workbook, bất kỳ lời gọi `CopyRows` nào tiếp theo cũng không thể tham chiếu đến dữ liệu nguồn hoặc pivot cache.

## Bước 2: Chuẩn bị worksheet nguồn và đích

Bạn cần một sheet đích để chứa pivot table đã sao chép. Đoạn mã dưới đây lấy worksheet đầu tiên (nơi pivot table gốc nằm) và thêm một sheet mới có tên **Copy**.

```csharp
// Get the source worksheet (index 0 = first sheet)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a new worksheet that will receive the copied rows
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
```

> **Mẹo chuyên nghiệp:** Nếu sheet đích đã tồn tại, hãy gọi `Worksheets.RemoveAt(index)` trước để tránh trùng tên.

## Bước 3: Xác định vùng ô bao quanh pivot table

Đối tượng `CellArea` mô tả ô trái‑trên và ô phải‑dưới của phạm vi bạn muốn di chuyển. Trong ví dụ này pivot table chiếm `A1:G20`. Điều chỉnh tọa độ cho các bảng lớn hơn.

```csharp
// Define the range that includes the pivot table (A1:G20)
CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");
```

## Bước 4: Sao chép các hàng với định dạng và giữ nguyên pivot cache

Phương thức `CopyRows` sao chép **các hàng** từ sheet nguồn sang sheet đích. Khi truyền `CopyOptions.CopyAll` bạn đảm bảo rằng giá trị, định dạng, biểu đồ và các đối tượng nhúng—tất cả đều là một phần của pivot table—được chuyển sang.

```csharp
// Copy the rows from the source area to the destination sheet
sourceSheet.CopyRows(
    sourceArea.StartRow,          // start row in the source sheet
    destinationSheet,            // target worksheet
    0,                            // start row in the destination sheet
    sourceArea.RowCount,          // number of rows to copy
    CopyOptions.CopyAll);        // copy everything (values, formats, objects, etc.)
```

### Tại sao `CopyRows` hoạt động tốt hơn `Copy` đối với pivot table

* `CopyRows` tôn trọng pivot cache nội bộ, vì vậy pivot table đã sao chép vẫn hoạt động được.
* Nó giữ nguyên **sao chép các hàng với định dạng** chính xác như trong sheet gốc.
* Không giống như một lệnh `Copy` đơn giản của một phạm vi, nó còn di chuyển các hàng ẩn và bất kỳ slicer nào liên quan.

## Bước 5: Lưu workbook với pivot table đã sao chép

Cuối cùng, ghi workbook đã chỉnh sửa ra đĩa. Tệp mới chứa sheet gốc cộng với một sheet **Copy** chứa bản sao hoàn chỉnh của pivot table gốc.

```csharp
// Save the workbook to a new file
workbook.Save(@"YOUR_DIRECTORY\pivot_copied.xlsx");
```

### Kết quả mong đợi

Khi bạn mở `pivot_copied.xlsx`:

* Sheet **Sheet1** vẫn chứa dữ liệu và pivot table gốc.
* Sheet **Copy** hiển thị một pivot table giống hệt với cùng bố cục, bộ lọc và định dạng.
* Tất cả công thức và kết nối dữ liệu vẫn nguyên vẹn vì pivot cache đã được sao chép cùng với các hàng.

## Cách sao chép pivot table sang sheet khác trong cùng một workbook

Nếu bạn chỉ cần pivot table ở một sheet hiện có khác (ví dụ, “Report”), hãy thay thế bước tạo sheet đích bằng việc tham chiếu tới sheet mục tiêu:

```csharp
Worksheet destinationSheet = workbook.Worksheets["Report"]; // existing sheet
sourceSheet.CopyRows(sourceArea.StartRow, destinationSheet, 0,
                     sourceArea.RowCount, CopyOptions.CopyAll);
```

Đoạn mã này minh họa **sao chép pivot table sang sheet khác** mà không cần tạo worksheet mới.

## Xuất pivot table ra workbook mới

Đôi khi bạn muốn pivot table ở một tệp hoàn toàn riêng biệt. Sau khi sao chép, bạn có thể xóa tất cả các worksheet ngoại trừ worksheet chứa pivot table đã sao chép và sau đó lưu:

```csharp
// Keep only the copied sheet
for (int i = workbook.Worksheets.Count - 1; i >= 0; i--)
{
    if (workbook.Worksheets[i].Name != "Copy")
        workbook.Worksheets.RemoveAt(i);
}

// Save as a new workbook containing only the pivot table
workbook.Save(@"YOUR_DIRECTORY\pivot_only.xlsx");
```

Bây giờ `pivot_only.xlsx` chứa một sheet duy nhất với pivot table đã được nhân bản, đáp ứng yêu cầu **xuất pivot table ra workbook mới**.

## Cách sao chép các hàng Excel mà không mất định dạng

Lệnh `CopyRows` tương tự hoạt động cho bất kỳ phạm vi nào, không chỉ pivot table. Nếu bạn cần **sao chép các hàng Excel** bao gồm định dạng có điều kiện, xác thực dữ liệu hoặc ô đã ghép, hãy sử dụng cùng một phương pháp:

```csharp
// Example: copy rows 30‑40 from Sheet1 to Sheet2
sourceSheet.CopyRows(29, // zero‑based index for row 30
                     workbook.Worksheets["Sheet2"],
                     0,
                     11, // rows 30‑40 = 11 rows
                     CopyOptions.CopyAll);
```

Vì `CopyOptions.CopyAll` chuyển mọi thứ, các hàng đích sẽ trông hoàn toàn giống như các hàng nguồn.

## Các rủi ro thường gặp và cách khắc phục

| Rủi ro | Triệu chứng | Cách khắc phục |
|---------|---------|-----|
| Phạm vi nguồn không bao gồm toàn bộ pivot table | Pivot table đã sao chép bị cắt ngắn. | Kiểm tra `CellArea` bao phủ tất cả các hàng/cột của pivot table. |
| Worksheet đích đã chứa dữ liệu | Các hàng bị ghi đè gây mất dữ liệu. | Chọn một sheet mới hoặc bắt đầu sao chép ở chỉ số hàng cao hơn. |
| Pivot table sử dụng nguồn dữ liệu bên ngoài | Bản sao mất kết nối. | Sau khi sao chép, gọi `pivotTable.RefreshData()` để thiết lập lại liên kết. |
| Các hàng ẩn bị bỏ qua | Một số hàng biến mất trong bản sao. | `CopyRows` tự động sao chép các hàng ẩn; đảm bảo bạn không sử dụng `CopyOptions.CopyValuesOnly`. |

## Ví dụ đầy đủ, có thể chạy

Dưới đây là một chương trình tự chứa mà bạn có thể dán vào một dự án console mới. Nó minh họa mọi bước đã thảo luận ở trên.

```csharp
using System;
using Aspose.Cells;

namespace PivotTableCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains the pivot table
            string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2️⃣ Get source and destination worksheets
            Worksheet sourceSheet = workbook.Worksheets[0]; // first sheet
            Worksheet destinationSheet = workbook.Worksheets.Add("Copy");

            // 3️⃣ Define the cell area that holds the pivot table (A1:G20)
            CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");

            // 4️⃣ Copy rows with formatting and keep the pivot cache
            sourceSheet.CopyRows(
                sourceArea.StartRow,      // start row index (0‑based)
                destinationSheet,        // target sheet
                0,                        // start row in destination
                sourceArea.RowCount,      // number of rows to copy
                CopyOptions.CopyAll);    // copy everything

            // 5️⃣ Save the workbook with the copied pivot table
            string destPath = @"YOUR_DIRECTORY\pivot_copied.xlsx";
            workbook.Save(destPath);

            Console.WriteLine("Pivot table copied successfully to " + destPath);
        }
    }
}
```

**Chạy chương trình** sẽ tạo `pivot_copied.xlsx` với một bản sao của pivot table gốc trên một sheet mới có tên **Copy**.

## Kết luận

Bạn giờ đã biết **cách sao chép một pivot table** trong C# bằng cách

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copy Pivot Table in C# – Complete Step‑by‑Step Guide](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [How to copy range with pivot tables in C# – Complete Guide](/cells/english/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}