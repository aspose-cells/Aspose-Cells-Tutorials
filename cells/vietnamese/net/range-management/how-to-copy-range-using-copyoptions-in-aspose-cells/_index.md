---
category: general
date: 2026-11-19
description: Tìm hiểu cách sao chép vùng dữ liệu bằng CopyOptions trong Aspose.Cells,
  giữ nguyên định dạng và bảng pivot khi sao chép một vùng Excel có định dạng.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range using copyoptions
- copy excel range with formatting
- Aspose.Cells copy range
- preserve pivot tables Aspose
- Excel automation C#
language: vi
lastmod: 2026-11-19
og_description: Sao chép phạm vi bằng CopyOptions trong Aspose.Cells cho phép bạn
  sao chép dữ liệu Excel với đầy đủ định dạng và bảng pivot được giữ nguyên, giúp
  thao tác sổ làm việc một cách đáng tin cậy.
og_image_alt: Screenshot of C# code that copies an Excel range using Aspose.Cells
  CopyOptions
og_title: Sao chép phạm vi bằng CopyOptions trong Aspose.Cells – hướng dẫn từng bước
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  headline: How to copy range using CopyOptions in Aspose.Cells
  type: TechArticle
- description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  name: How to copy range using CopyOptions in Aspose.Cells
  steps:
  - name: Why `CopyOptions` matters
    text: '* **Performance** – The library performs a single internal operation rather
      than copying cells one‑by‑one. * **Accuracy** – All visual aspects (fonts, colors,
      borders) survive the move, which eliminates visual drift in generated reports.
      * **Reliability** – Pivot tables remain functional because the'
  - name: What if the destination area overlaps the source?
    text: 'Aspose.Cells throws an `ArgumentException`. To avoid this, calculate a
      destination that does not intersect the source, or copy to a different worksheet:'
  - name: How to copy between different workbooks?
    text: 'Create a second `Workbook` instance for the target file and use the same
      `CopyOptions` object:'
  - name: Does `CopyOptions` also copy merged cells?
    text: Yes. The `CopyStyle` flag includes merged‑cell information. If you need
      finer control, set `options.CopyMergedCells = true` (available in newer versions).
  - name: What about large ranges (thousands of rows)?
    text: The operation is memory‑efficient, but you may want to increase the `WorkbookSettings`
      `MemorySetting` to `MemorySetting.MemoryPreference` for very large files.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cách sao chép phạm vi bằng CopyOptions trong Aspose.Cells
url: /vi/net/range-management/how-to-copy-range-using-copyoptions-in-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách sao chép phạm vi bằng CopyOptions trong Aspose.Cells

Nếu bạn cần **sao chép phạm vi bằng CopyOptions** trong Aspose.Cells, hướng dẫn này cho bạn biết chính xác cách sao chép một khối ô trong khi giữ nguyên mọi định dạng và các pivot tables được nhúng. Nhiều nhà phát triển gặp khó khăn trong việc bảo tồn kiểu khi di chuyển dữ liệu giữa các worksheet, và lớp `CopyOptions` giải quyết vấn đề này mà không cần các bước thủ công bổ sung.

Trong tutorial này bạn sẽ học:

* Xác định các khu vực nguồn và đích trong một workbook Excel.  
* Sử dụng `CopyOptions` để giữ lại định dạng ô, độ rộng cột và các pivot tables.  
* Lưu kết quả vào một tệp mới sẵn sàng cho quá trình xử lý tiếp theo.

Ví dụ này hoạt động với bất kỳ tệp `.xlsx` nào và chỉ yêu cầu thư viện Aspose.Cells cho .NET.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* .NET 6.0 hoặc phiên bản mới hơn đã được cài đặt.  
* Giấy phép Aspose.Cells cho .NET hợp lệ (hoặc khóa dùng thử miễn phí).  
* Visual Studio 2022 hoặc bất kỳ IDE C# nào bạn thích.  

Không cần thêm bất kỳ gói NuGet nào ngoài `Aspose.Cells`.

## Bước 1: Thiết lập dự án và nhập namespace

Tạo một ứng dụng console mới và thêm tham chiếu Aspose.Cells:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Your code will go here
        }
    }
}
```

Lệnh `using Aspose.Cells;` cho phép bạn truy cập vào `Workbook`, `CellArea` và `CopyOptions`.

## Bước 2: Tải workbook bạn muốn chỉnh sửa

```csharp
// Step 2: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

`Workbook` đại diện cho toàn bộ tệp Excel. Thay thế `YOUR_DIRECTORY` bằng thư mục chứa tệp nguồn của bạn.

## Bước 3: Xác định các phạm vi nguồn và đích

```csharp
// Step 3: Define the source range (A1:H30)
CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");

// Step 3b: Define the destination range (A35:H64)
CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");
```

`CellArea.CreateCellArea` tạo một vùng hình chữ nhật dựa trên địa chỉ ô trên‑trái và dưới‑phải. Bạn có thể điều chỉnh tọa độ để phù hợp với kích thước khối cần sao chép.

## Bước 4: Sao chép phạm vi trong khi giữ nguyên định dạng và pivot tables

```csharp
// Step 4: Copy the range using CopyOptions
CopyOptions options = new CopyOptions
{
    // Preserve all cell styles, number formats, and column widths
    CopyStyle = true,
    // Keep formulas unchanged (they will still reference the original sheet)
    CopyFormula = true,
    // Preserve any pivot tables that intersect the copied area
    CopyPivotTables = true,
    // Retain data validation and conditional formatting
    CopyDataValidation = true,
    CopyConditionalFormatting = true
};

workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
```

Đối tượng `CopyOptions` cho Aspose.Cells biết chính xác những gì cần giữ lại. Đặt `CopyPivotTables = true` là chìa khóa để **sao chép phạm vi bằng CopyOptions** khi nguồn của bạn bao gồm các pivot tables. Các cờ khác đảm bảo rằng **sao chép phạm vi excel với định dạng** được thực hiện tự động—không cần mã bổ sung để áp dụng lại kiểu sau khi sao chép.

### Tại sao `CopyOptions` lại quan trọng

* **Performance** – Thư viện thực hiện một thao tác nội bộ duy nhất thay vì sao chép từng ô một.  
* **Accuracy** – Tất cả các khía cạnh trực quan (phông chữ, màu sắc, viền) vẫn được giữ lại, loại bỏ sự lệch về hình ảnh trong các báo cáo được tạo.  
* **Reliability** – Các pivot tables vẫn hoạt động vì bộ nhớ đệm và tham chiếu nguồn của chúng được sao chép.

## Bước 5: Lưu workbook đã chỉnh sửa

```csharp
// Step 5: Save the workbook with the copied range
workbook.Save("YOUR_DIRECTORY/output.xlsx");
Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
```

Sau khi gọi `Save`, tệp `output.xlsx` chứa dữ liệu gốc cộng với khối đã sao chép tại vị trí đích, đầy đủ định dạng và pivot tables.

## Mã nguồn đầy đủ để tham khảo

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Load the source workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // Define source and destination ranges
            CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");
            CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");

            // Configure copy options to preserve everything
            CopyOptions options = new CopyOptions
            {
                CopyStyle = true,
                CopyFormula = true,
                CopyPivotTables = true,
                CopyDataValidation = true,
                CopyConditionalFormatting = true
            };

            // Perform the copy operation
            workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);

            // Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");
            Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
        }
    }
}
```

Running this program prints:

```
Range copied successfully. Output saved to output.xlsx
```

Mở `output.xlsx` trong Excel – bạn sẽ thấy khối A1:H30 được sao chép tại A35:H64, với mọi màu ô, viền, định dạng số và bất kỳ pivot tables nào vẫn nguyên vẹn.

## Các câu hỏi thường gặp và xử lý trường hợp biên

### Nếu vùng đích trùng lặp với nguồn thì sao?

Aspose.Cells sẽ ném ra một `ArgumentException`. Để tránh điều này, tính toán một vị trí đích không giao nhau với nguồn, hoặc sao chép sang một worksheet khác:

```csharp
Worksheet destSheet = workbook.Worksheets.Add("CopySheet");
destSheet.Cells.CopyRange(sourceRange, CellArea.CreateCellArea("A1", "H30"), options);
```

### Cách sao chép giữa các workbook khác nhau?

Tạo một thể hiện `Workbook` thứ hai cho tệp đích và sử dụng cùng một đối tượng `CopyOptions`:

```csharp
Workbook target = new Workbook();
target.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
target.Save("target.xlsx");
```

### `CopyOptions` có sao chép các ô đã hợp nhất không?

Có. Cờ `CopyStyle` bao gồm thông tin về các ô đã hợp nhất. Nếu bạn cần kiểm soát chi tiết hơn, đặt `options.CopyMergedCells = true` (có sẵn trong các phiên bản mới hơn).

### Còn các phạm vi lớn (hàng nghìn) thì sao?

Thao tác này tiết kiệm bộ nhớ, nhưng bạn có thể muốn tăng `WorkbookSettings` `MemorySetting` lên `MemorySetting.MemoryPreference` cho các tệp rất lớn.

## Mẹo chuyên nghiệp

* **Tái sử dụng cùng một `CopyOptions`** cho nhiều thao tác sao chép – nó giảm tải cấp phát đối tượng.  
* **Xác thực các phạm vi** trước khi sao chép: `if (!CellArea.IsValid(sourceRange) || !CellArea.IsValid(destinationRange))` giúp phát hiện sớm các lỗi do nhập sai.  
* **Tắt tính toán** (`workbook.Settings.CalcMode = CalculationMode.Manual`) khi sao chép các bộ dữ liệu lớn để tăng tốc quá trình, sau đó gọi `workbook.CalculateFormula()` sau khi sao chép nếu bạn cần kết quả cập nhật.

## Kết luận

Bây giờ bạn đã biết cách **sao chép phạm vi bằng CopyOptions** trong Aspose.Cells, đạt được việc **sao chép phạm vi excel với định dạng** đầy đủ trong khi giữ nguyên các pivot tables và các tính năng nâng cao khác. Cách tiếp cận này loại bỏ việc áp dụng lại kiểu thủ công và đảm bảo tự động hoá Excel của bạn luôn mạnh mẽ và dễ bảo trì.

Next steps you might explore:

* Sử dụng `CopyOptions` để sao chép toàn bộ worksheet.  
* Kết hợp thao tác sao chép với `WorksheetCollection.AddCopy` để tạo báo cáo dựa trên mẫu.  
* Tích hợp mã vào một API ASP.NET Core để cung cấp chuyển đổi Excel ngay lập tức.

Bạn có thể tự do thử nghiệm với các tọa độ nguồn/đích khác nhau, và chia sẻ kết quả của mình trong phần bình luận!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Sao chép dữ liệu phạm vi Excel Aspose Cells .NET](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Sao chép dữ liệu phạm vi Excel Aspose Cells .NET](/cells/french/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Sao chép dữ liệu phạm vi Excel Aspose Cells .NET](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}