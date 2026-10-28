---
category: general
date: 2026-10-07
description: Lưu Excel dưới dạng PPT trong C# đồng thời giữ các hộp văn bản và hình
  dạng có thể chỉnh sửa. Tìm hiểu từng bước cách chuyển đổi Excel sang PowerPoint
  bằng Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as ppt
- convert excel to powerpoint
- how to export excel
- how to keep textboxes
- convert spreadsheet to presentation
language: vi
lastmod: 2026-10-07
og_description: Lưu Excel dưới dạng PPT trong C# đồng thời giữ nguyên các hộp văn
  bản và hình dạng. Hãy theo dõi hướng dẫn đầy đủ này để chuyển Excel sang PowerPoint
  với khả năng chỉnh sửa hoàn toàn.
og_image_alt: Diagram of Excel workbook being saved as PPT with editable text boxes
og_title: Lưu Excel dưới dạng PPT – hướng dẫn chuyển đổi có thể chỉnh sửa
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Save Excel as PPT in C# while keeping text boxes and shapes editable.
    Learn step‑by‑step how to convert Excel to PowerPoint using Aspose.Cells.
  headline: How to save Excel as PPT with editable text boxes in C#
  type: TechArticle
- description: Save Excel as PPT in C# while keeping text boxes and shapes editable.
    Learn step‑by‑step how to convert Excel to PowerPoint using Aspose.Cells.
  name: How to save Excel as PPT with editable text boxes in C#
  steps:
  - name: Why each line matters
    text: 1. **Loading the workbook** – `Workbook` reads the `.xlsx` file into memory,
      giving you full access to worksheets, charts, and embedded objects. 2. **Configuring
      `PptxSaveOptions`** – Setting `ExportTextBoxesAsEditable` and `ExportShapesAsEditable`
      tells Aspose.Cells to write those objects as native
  - name: Tips for large files
    text: '- **Memory management:** Call `GC.Collect()` after the conversion if you
      process many files in a batch. - **Image quality:** Use `opts.ImageResolution
      = 300` to increase chart clarity when the source contains high‑resolution graphics.
      - **Performance:** Set `opts.CompressionLevel = CompressionLevel.'
  - name: 'Edge case: Converting a macro‑enabled workbook (`.xlsm`)'
    text: Aspose.Cells can read `.xlsm` files, but macros are **not** transferred
      to the PPTX because PowerPoint does not support VBA macros from Excel. If you
      need the macro logic, consider exporting the relevant data first, then recreating
      the macro in PowerPoint VBA manually.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel‑to‑PowerPoint
- document‑conversion
title: Cách lưu Excel thành PPT với các hộp văn bản có thể chỉnh sửa trong C#
url: /vi/net/converting-excel-files-to-other-formats/how-to-save-excel-as-ppt-with-editable-text-boxes-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách lưu Excel thành PPT với các hộp văn bản có thể chỉnh sửa trong C#

Nếu bạn cần **lưu Excel thành PPT** và giữ mọi hộp văn bản và hình dạng có thể chỉnh sửa, hướng dẫn này sẽ chỉ cho bạn cách thực hiện. Sử dụng Aspose.Cells for .NET, bạn có thể **chuyển đổi Excel sang PowerPoint** chỉ trong vài dòng mã, giữ nguyên bố cục gốc để bản trình chiếu kết quả có thể được chỉnh sửa trong PowerPoint mà không mất bất kỳ đối tượng nào.

Ngoài việc chuyển đổi, bạn sẽ học **cách xuất Excel** trong khi giữ lại các hộp văn bản, cách giữ các hộp văn bản có thể chỉnh sửa, và **cách chuyển đổi bảng tính sang bản trình chiếu** một cách hoạt động tốt cho các workbook lớn và biểu đồ phức tạp.

## Những gì bạn cần

- .NET 6.0 trở lên (mã cũng hoạt động với .NET Framework 4.6+)
- Giấy phép Aspose.Cells for .NET (bản dùng thử miễn phí dùng để đánh giá)
- Visual Studio 2022 (hoặc bất kỳ IDE nào hỗ trợ C#)
- Một tệp Excel mẫu chứa các hộp văn bản, hình dạng hoặc biểu đồ (ví dụ, `WithTextBoxes.xlsx`)

> **Mẹo chuyên nghiệp:** Nếu bạn đang sử dụng bản dùng thử miễn phí, hãy đặt `License.SetLicense("Aspose.Total.lic")` sớm trong chương trình của bạn để tránh các watermark đánh giá.

## Cách lưu Excel thành PPT trong khi giữ nguyên các hộp văn bản

Phần này trực tiếp đáp ứng từ khóa chính **save Excel as PPT**. Đoạn mã dưới đây là một ví dụ hoàn chỉnh, có thể chạy được mà bạn có thể dán vào một dự án console mới.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Presentation;

class Program
{
    static void Main()
    {
        // Step 1: Load the Excel workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/WithTextBoxes.xlsx");

        // Step 2: Configure PPTX save options to keep text boxes and shapes editable
        PptxSaveOptions saveOptions = new PptxSaveOptions
        {
            ExportTextBoxesAsEditable = true,   // how to keep textboxes editable
            ExportShapesAsEditable = true       // also keep shapes editable
        };

        // Step 3: Save the workbook as an editable PowerPoint presentation
        workbook.Save("YOUR_DIRECTORY/ExportEditable.pptx", saveOptions);

        Console.WriteLine("Excel file has been successfully saved as PPT.");
    }
}
```

### Tại sao mỗi dòng lại quan trọng

1. **Tải workbook** – `Workbook` đọc tệp `.xlsx` vào bộ nhớ, cho phép bạn truy cập đầy đủ vào các worksheet, biểu đồ và các đối tượng nhúng.
2. **Cấu hình `PptxSaveOptions`** – Thiết lập `ExportTextBoxesAsEditable` và `ExportShapesAsEditable` cho Aspose.Cells ghi các đối tượng này dưới dạng hình dạng PowerPoint gốc thay vì hình ảnh đã phẳng. Đây là chìa khóa để **giữ các hộp văn bản** có thể chỉnh sửa sau khi chuyển đổi.
3. **Lưu dưới dạng PPTX** – Phương thức `Save` cùng với đối tượng `PptxSaveOptions` thực hiện thao tác **chuyển đổi Excel sang PowerPoint** thực tế. Tệp đầu ra (`ExportEditable.pptx`) có thể mở trong Microsoft PowerPoint và chỉnh sửa như bất kỳ bản trình chiếu gốc nào.

> **Lưu ý:** Đầu ra giữ nguyên độ rộng cột, chiều cao hàng và định dạng ô, vì vậy bố cục hình ảnh vẫn giống hệt với sheet Excel nguồn.

![Ảnh chụp màn hình đầu ra console xác nhận chuyển đổi thành công](/images/save-excel-as-ppt-console.png "Đầu ra console sau khi lưu Excel thành PPT")

*Văn bản thay thế ảnh: Cửa sổ console hiển thị “Excel file has been successfully saved as PPT.”*

## Chuyển đổi Excel sang PowerPoint – xử lý workbook lớn

Khi bạn **chuyển đổi bảng tính sang bản trình chiếu** có nhiều worksheet, bạn có thể muốn mỗi sheet trở thành một slide riêng. Aspose.Cells thực hiện việc này tự động, nhưng bạn có thể tinh chỉnh hành vi:

```csharp
// Create save options with a custom slide layout
PptxSaveOptions opts = new PptxSaveOptions
{
    ExportTextBoxesAsEditable = true,
    ExportShapesAsEditable = true,
    // Each worksheet becomes a new slide (default behavior)
    // You can also set opts.OnePagePerSheet = false to merge sheets
};
workbook.Save("LargeExport.pptx", opts);
```

### Mẹo cho tệp lớn

- **Quản lý bộ nhớ:** Gọi `GC.Collect()` sau khi chuyển đổi nếu bạn xử lý nhiều tệp trong một batch.
- **Chất lượng hình ảnh:** Sử dụng `opts.ImageResolution = 300` để tăng độ rõ của biểu đồ khi nguồn chứa đồ họa độ phân giải cao.
- **Hiệu suất:** Đặt `opts.CompressionLevel = CompressionLevel.Maximum` để giảm kích thước tệp PPTX mà không ảnh hưởng đến khả năng chỉnh sửa.

## Cách xuất Excel trong khi giữ nguyên công thức và biểu đồ

Nếu workbook của bạn chứa công thức, chúng sẽ được tính trong quá trình chuyển đổi và các giá trị kết quả sẽ xuất hiện trên các slide. Các công thức gốc **không** được chuyển vì PowerPoint không hỗ trợ công thức Excel một cách nguyên bản. Tuy nhiên, bạn có thể giữ workbook nguồn được liên kết với bản trình chiếu:

```csharp
PptxSaveOptions linkedOpts = new PptxSaveOptions
{
    ExportTextBoxesAsEditable = true,
    ExportShapesAsEditable = true,
    // Keep a link to the original Excel file for future updates
    LinkToSource = true
};
workbook.Save("LinkedExport.pptx", linkedOpts);
```

Khi người dùng mở PPTX trong PowerPoint, một thông báo sẽ xuất hiện hỏi có cập nhật dữ liệu liên kết hay không. Điều này đáp ứng yêu cầu **cách xuất Excel** đồng thời vẫn cho phép chỉnh sửa sau này.

## Các lỗi thường gặp và cách giữ các hộp văn bản nguyên vẹn

| Triệu chứng | Nguyên nhân | Cách khắc phục |
|------------|-------------|----------------|
| Hộp văn bản xuất hiện dưới dạng hình ảnh | `ExportTextBoxesAsEditable` để ở giá trị mặc định `false` | Đặt `ExportTextBoxesAsEditable = true` |
| Không thể di chuyển hình dạng trong PowerPoint | `ExportShapesAsEditable` chưa được bật | Bật `ExportShapesAsEditable = true` |
| Thiếu chú giải biểu đồ | Biểu đồ sử dụng theme tùy chỉnh không được bộ chuyển đổi hỗ trợ | Áp dụng theme tiêu chuẩn trước khi chuyển đổi |
| Bản trình chiếu trống | Đường dẫn workbook không đúng hoặc tệp bị khóa | Kiểm tra lại đường dẫn và đảm bảo tệp không được mở ở nơi khác |

### Trường hợp đặc biệt: Chuyển đổi workbook có macro (`.xlsm`)

Aspose.Cells có thể đọc tệp `.xlsm`, nhưng macro **không** được chuyển sang PPTX vì PowerPoint không hỗ trợ macro VBA từ Excel. Nếu bạn cần logic macro, hãy cân nhắc xuất dữ liệu liên quan trước, sau đó tự tạo lại macro trong VBA của PowerPoint.

## Xác minh đầu ra – chuyển đổi bảng tính sang bản trình chiếu đúng

Sau khi chạy mã, mở `ExportEditable.pptx` trong PowerPoint:

1. **Chọn một hộp văn bản** – bạn sẽ thấy các tay cầm thay đổi kích thước thông thường, xác nhận đối tượng có thể chỉnh sửa.
2. **Nhấp chuột phải vào một hình dạng** – menu ngữ cảnh sẽ hiển thị các tùy chọn hình dạng PowerPoint (đổ màu, đường viền, v.v.).
3. **Kiểm tra thứ tự slide** – mỗi worksheet nên tương ứng với một slide, giữ nguyên thứ tự tab gốc.

Nếu bất kỳ đối tượng nào không thể chỉnh sửa, hãy kiểm tra lại các cờ trong `PptxSaveOptions`. Các giá trị mặc định (`false`) khiến bộ chuyển đổi raster hoá các đối tượng, vì vậy việc đặt chúng thành `true` là cần thiết cho yêu cầu **giữ các hộp văn bản** có thể chỉnh sửa.

## Các thực tiễn tốt nhất cho môi trường sản xuất

- **Cấp giấy phép sớm:** `License license = new License(); license.SetLicense("Aspose.Total.lic");`
- **Xử lý ngoại lệ:** Bao bọc quá trình chuyển đổi trong khối `try/catch` để phát hiện lỗi truy cập tệp.
- **Ghi log:** Ghi lại đường dẫn nguồn và đích cùng với thời gian để tạo nhật ký kiểm tra.
- **Kiểm thử đơn vị:** Sử dụng một workbook nhỏ với các đối tượng đã biết để xác nhận rằng PPTX kết quả chứa số lượng hình dạng chỉnh sửa mong muốn.

```csharp
try
{
    // Conversion code from earlier sections
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Conversion failed: {ex.Message}");
    // Optionally rethrow or handle according to your error policy
}
```

## Kết luận

Bạn đã có một giải pháp hoàn chỉnh, sẵn sàng cho môi trường sản xuất để **lưu Excel thành PPT** trong khi giữ nguyên các hộp văn bản, hình dạng và bố cục tổng thể. Bằng cách cấu hình `PptxSaveOptions` bạn kiểm soát **cách giữ các hộp văn bản** có thể chỉnh sửa, cho phép chỉnh sửa liền mạch trong PowerPoint sau khi chuyển đổi. Cùng với đó, bạn có thể **chuyển đổi Excel sang PowerPoint**, **xuất dữ liệu Excel**, và **chuyển đổi bảng tính sang bản trình chiếu** cho bất kỳ workbook nào, dù lớn hay phức tạp.

Tiếp theo, hãy khám phá các chủ đề liên quan như **xuất biểu đồ Excel dưới dạng hình ảnh độ phân giải cao**, **chuyển đổi hàng loạt nhiều workbook**, hoặc **nhúng PPTX đã tạo vào ứng dụng web**. Mỗi chủ đề này dựa trên những nguyên tắc cơ bản đã trình bày ở đây và mở rộng sức mạnh của Aspose.Cells trong các kịch bản tự động hoá tài liệu thực tế. Chúc bạn lập trình vui vẻ!

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên đều có mã mẫu hoàn chỉnh và giải thích chi tiết từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách Chuyển Đổi Excel sang PowerPoint Sử Dụng Aspose.Cells cho .NET: Hướng Dẫn Toàn Diện](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Cách Thêm và Truy Cập Hộp Văn Bản trong Excel bằng Aspose.Cells .NET | Hướng Dẫn Từng Bước](/cells/english/net/images-shapes/aspose-cells-net-add-text-boxes-excel/)
- [Cách Chuyển Đổi Các Sheet Excel thành Hình Ảnh Sử Dụng Aspose.Cells .NET (Hướng Dẫn Từng Bước)](/cells/english/net/workbook-operations/convert-excel-sheets-images-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}