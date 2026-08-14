---
category: general
date: 2026-08-14
description: Xuất Excel sang PowerPoint bằng Aspose.Cells và tìm hiểu cách tính công
  thức Excel trong mã. Ví dụ C# từng bước với mã nguồn đầy đủ.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- calculate excel formulas in code
- Aspose.Cells copy pivot table
- export editable objects pptx
- dynamic array EXPAND function
- C# workbook automation
language: vi
lastmod: 2026-08-14
og_description: Xuất Excel sang PowerPoint bằng Aspose.Cells và tính toán công thức
  Excel trong code. Hãy theo dõi hướng dẫn toàn diện này để tạo các tệp PPTX có thể
  chỉnh sửa từ workbook.
og_image_alt: Screenshot showing an Excel sheet being exported to a PowerPoint slide
  with editable textboxes
og_title: Xuất Excel sang PowerPoint với Aspose.Cells – hướng dẫn C# đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  headline: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  type: TechArticle
- description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  name: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  steps:
  - name: Why this works
    text: '* **`Workbook`** loads the entire Excel file into memory, giving you full
      API access. * **`CopyRange`** with `CopyPivotTable = true` ensures the pivot
      table’s data source, cache, and layout are duplicated exactly—something older
      versions of Aspose.Cells could not do. * Adding a new worksheet (`Copy`'
  - name: Explanation
    text: '* **`WorkbookDesigner`** is a high‑level helper that prepares the workbook
      for export, handling Smart Markers, named ranges, and layout adjustments. *
      Setting `ExportEditableObjects = true` tells Aspose.Cells to translate Excel
      drawings into PowerPoint shapes rather than flattening them into images.'
  - name: Why you might use this
    text: '* **Uniform data type:** Exporting as strings avoids type‑mismatch errors
      when the consumer expects text. * **Custom formatting:** Replace `value.ToString()`
      with any custom formatter (e.g., `value.ToString("yyyy-MM-dd")` for dates).'
  - name: How the calculation engine works
    text: '* The `Formula` property stores the expression exactly as you would type
      it in Excel. * `CalculateFormula()` triggers a full workbook recalculation,
      respecting dependencies between cells. * The `EXPAND` function (available in
      Excel 365) returns a spill range based on the source cell (`B1`) and the s'
  - name: What to verify
    text: '* Open `result.xlsx` in Excel to confirm the pivot table copy, the `EXPAND`
      formula result, and any custom‑exported strings. * Open `output.pptx` in PowerPoint;
      you should see a slide that mirrors the Excel layout, and all charts/textboxes
      should be editable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
- Office 365 functions
title: Xuất Excel sang PowerPoint với Aspose.Cells – hướng dẫn lập trình đầy đủ
url: /vi/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-aspose-cells-complete-progra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Xuất Excel sang PowerPoint với Aspose.Cells – hướng dẫn lập trình đầy đủ

Nếu bạn cần **xuất Excel sang PowerPoint** một cách lập trình, hướng dẫn này sẽ chỉ cho bạn cách thực hiện với Aspose.Cells cho .NET. Bạn cũng sẽ học cách **tính toán công thức Excel trong mã**, sao chép bảng pivot mà không mất định nghĩa, và sử dụng hàm Office‑365 EXPAND mới cho các mảng động.

Trong các phần tiếp theo, chúng ta sẽ đi qua một ví dụ thực tế bằng C#, giải thích lý do mỗi dòng mã quan trọng, và đề cập đến các lỗi thường gặp để bạn có thể áp dụng giải pháp này vào dự án của mình.

## Những nội dung mà hướng dẫn này bao phủ

* Tải một workbook hiện có (`input.xlsx`)  
* Sao chép một vùng chứa bảng pivot đồng thời giữ nguyên định nghĩa của nó  
* Xuất workbook sang tệp PowerPoint (`.pptx`) với các textbox và shape có thể chỉnh sửa được  
* Xuất một vùng ô dưới dạng chuỗi bằng logic tùy chỉnh  
* Tính toán công thức Excel trong mã, bao gồm hàm Office‑365 EXPAND  
* Lưu workbook cuối cùng với mọi thay đổi đã áp dụng  

**Yêu cầu trước**  
* .NET 6.0 hoặc mới hơn (mã cũng hoạt động với .NET Framework 4.7.2+)  
* Aspose.Cells cho .NET v25.11 hoặc mới hơn (tùy chọn `CopyPivotTable` được giới thiệu trong v25.11)  
* Kiến thức cơ bản về C# và các khái niệm Excel như range, bảng pivot và công thức  

> **Mẹo chuyên nghiệp:** Cài đặt Aspose.Cells qua NuGet (`Install-Package Aspose.Cells`) để dự án luôn cập nhật các tính năng mới nhất.

## Xuất Excel sang PowerPoint với Aspose.Cells

Nhiệm vụ chính đầu tiên là chuyển đổi workbook thành một bản trình chiếu PowerPoint trong khi giữ mọi yếu tố trực quan có thể chỉnh sửa được. Điều này rất cần thiết khi bạn muốn tự động tạo slide từ báo cáo tài chính hoặc bảng điều khiển.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;      // ExportTableOptions, ExportOptions, etc.
using Aspose.Cells.Pivot;      // Pivot‑table APIs
using Aspose.Cells.Drawing;    // Shapes, textboxes, etc.

// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Step 2: Copy a range that contains a pivot table (preserves the definition)
Worksheet sourceSheet = workbook.Worksheets["Source"];
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");   // includes a pivot table
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
destinationSheet.Cells.CopyRange(sourceRange, destinationSheet.Cells, new CopyOptions
{
    CopyPivotTable = true   // new option in v25.11
});
```

### Tại sao cách này hoạt động

* **`Workbook`** tải toàn bộ tệp Excel vào bộ nhớ, cho phép bạn truy cập đầy đủ API.  
* **`CopyRange`** với `CopyPivotTable = true` đảm bảo nguồn dữ liệu, cache và bố cục của bảng pivot được sao chép chính xác—điều mà các phiên bản cũ của Aspose.Cells không thể làm được.  
* Thêm một worksheet mới (`Copy`) giúp bạn giữ nguyên sheet gốc, hữu ích cho việc theo dõi audit.

## Xuất workbook sang PowerPoint với các đối tượng có thể chỉnh sửa

Bây giờ chúng ta chuyển workbook thành tệp PowerPoint. Bằng cách bật `ExportEditableObjects`, mọi biểu đồ, shape hoặc textbox sẽ trở thành đối tượng PowerPoint gốc mà người dùng có thể chỉnh sửa trực tiếp sau khi xuất.

```csharp
// Step 3: Export the workbook to PowerPoint with editable textboxes/shapes
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.Process();   // processes Smart Markers if present
designer.ExportToPptx("YOUR_DIRECTORY/output.pptx", new ExportOptions
{
    ExportEditableObjects = true   // makes objects editable in the PPTX
});
```

### Giải thích

* **`WorkbookDesigner`** là một trợ giúp cấp cao giúp chuẩn bị workbook cho việc xuất, xử lý Smart Markers, named ranges và điều chỉnh bố cục.  
* Đặt `ExportEditableObjects = true` báo cho Aspose.Cells chuyển đổi các bản vẽ Excel thành các shape PowerPoint thay vì làm phẳng chúng thành hình ảnh. Điều này tạo ra một bộ slide **có thể chỉnh sửa hoàn toàn**.  

> **Trường hợp đặc biệt:** Nếu workbook của bạn chứa các biểu đồ phức tạp được xây dựng từ kết nối dữ liệu bên ngoài, hãy chắc chắn các kết nối đó đã được giải quyết trước khi gọi `ExportToPptx`, nếu không biểu đồ có thể hiển thị trống.

## Xuất một vùng dữ liệu dưới dạng chuỗi bằng logic tùy chỉnh

Đôi khi bạn cần giá trị chuỗi thô cho các quy trình xử lý tiếp theo (ví dụ: truyền cho bộ phân tích CSV). Lớp `ExportTableOptions` cho phép bạn kiểm soát cách mỗi ô được chuyển đổi.

```csharp
// Step 4: Export a range as strings using custom logic
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true,
    CustomExport = (cell, value) => value.ToString()   // simple conversion for each cell
};
workbook.Worksheets[0].Cells.ExportTableAsString(tableOptions, "A1:D10");
```

### Lý do bạn có thể muốn dùng cách này

* **Kiểu dữ liệu đồng nhất:** Xuất dưới dạng chuỗi tránh lỗi không khớp kiểu khi bên tiêu thụ mong đợi văn bản.  
* **Định dạng tùy chỉnh:** Thay thế `value.ToString()` bằng bất kỳ bộ định dạng tùy chỉnh nào (ví dụ: `value.ToString("yyyy-MM-dd")` cho ngày tháng).  

## Tính toán công thức Excel trong mã

Một yêu cầu phổ biến là **tính toán công thức Excel trong mã** mà không cần mở Excel. Aspose.Cells cung cấp một engine tính toán tích hợp hoạt động offline và hỗ trợ các hàm Office‑365 mới nhất, bao gồm `EXPAND`.

```csharp
// Step 5: Use the new Office‑365 EXPAND function to create a dynamic array
Worksheet firstSheet = workbook.Worksheets[0];
firstSheet.Cells["A1"].Formula = "EXPAND(B1,5,3)";   // expands array starting at B1
workbook.CalculateFormula();   // forces recalculation of the formula
```

### Cách engine tính toán hoạt động

* Thuộc tính `Formula` lưu trữ biểu thức chính xác như bạn gõ trong Excel.  
* `CalculateFormula()` kích hoạt việc tính lại toàn bộ workbook, tôn trọng các phụ thuộc giữa các ô.  
* Hàm `EXPAND` (có trong Excel 365) trả về một spill range dựa trên ô nguồn (`B1`) và số hàng (`5`) cùng số cột (`3`) được chỉ định.  

> **Mẹo:** Nếu bạn chỉ cần tính toán một phần của workbook, hãy dùng `Worksheet.CalculateFormula()` để giới hạn phạm vi và cải thiện hiệu năng.

## Lưu workbook với mọi thay đổi đã áp dụng

Cuối cùng, ghi workbook đã chỉnh sửa trở lại đĩa. Bạn có thể lưu ở bất kỳ định dạng nào được hỗ trợ (`.xlsx`, `.xls`, `.csv`, …) bằng cách thay đổi phần mở rộng tệp.

```csharp
// Step 6: Save the workbook with all changes applied
workbook.Save("YOUR_DIRECTORY/result.xlsx");
```

### Những điều cần kiểm tra

* Mở `result.xlsx` trong Excel để xác nhận việc sao chép bảng pivot, kết quả công thức `EXPAND`, và bất kỳ chuỗi xuất tùy chỉnh nào.  
* Mở `output.pptx` trong PowerPoint; bạn sẽ thấy một slide phản ánh bố cục Excel, và mọi biểu đồ/textbox đều có thể chỉnh sửa.

## Các câu hỏi thường gặp và khắc phục sự cố

| Câu hỏi | Trả lời |
|----------|--------|
| **Tôi có cần giấy phép để sử dụng Aspose.Cells không?** | Có. Bản dùng thử đủ cho việc đánh giá, nhưng giấy phép đầy đủ sẽ loại bỏ watermark và mở khóa tính năng `CopyPivotTable`. |
| **Nếu PPTX xuất ra hiển thị các shape trống thì sao?** | Kiểm tra các đối tượng vẽ trong workbook không bị ẩn (`Visible = true`) và mọi liên kết ảnh bên ngoài đã được nhúng trước khi xuất. |
| **Tôi có thể xuất nhiều worksheet thành các slide PPTX riêng biệt không?** | Sử dụng `WorkbookDesigner.ExportToPptx` trong một vòng lặp, chỉ định `ExportOptions` khác nhau cho mỗi worksheet, hoặc kết hợp chúng thành một bản trình chiếu duy nhất bằng cách thêm slide thủ công qua Aspose.Slides. |
| **`CalculateFormula` có an toàn khi chạy đa luồng không?** | Không. Thực hiện tính toán trên một luồng duy nhất hoặc sao chép workbook cho mỗi luồng để tránh điều kiện tranh chấp. |

## Kết luận

Bạn đã có một **giải pháp hoàn chỉnh, đầu‑từ‑đầu cho việc xuất Excel sang PowerPoint** bằng Aspose.Cells, và hiểu cách **tính toán công thức Excel trong mã**—bao gồm cả hàm hiện đại `EXPAND`. Hướng dẫn đã bao phủ việc tải workbook, sao chép bảng pivot, xuất sang PowerPoint có thể chỉnh sửa, xuất chuỗi tùy chỉnh, tính toán công thức, và lưu cuối cùng.

Từ đây bạn có thể:

* Mở rộng việc xuất để bao gồm nhiều slide cho mỗi worksheet (từ khóa phụ: *calculate Excel formulas in code* có thể tái sử dụng khi tạo dữ liệu biểu đồ).  
* Tích hợp Aspose.Slides để thêm hoạt ảnh hoặc bố cục master slide.  
* Thay thế delegate `CustomExport` đơn giản bằng định dạng dựa trên locale cho các dự án quốc tế.  

Hãy tự do thử nghiệm với các vùng dữ liệu khác nhau, khám phá các hàm Office‑365 khác (ví dụ: `FILTER`, `SORT`), và kết hợp quy trình này với việc gửi email tự động để có một pipeline báo cáo hoàn toàn không cần can thiệp thủ công.

---


## Bạn nên học gì tiếp theo?


Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã mẫu đầy đủ với các giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Automate Excel Data Export Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)
- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Export Excel Cells to Image Using Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}