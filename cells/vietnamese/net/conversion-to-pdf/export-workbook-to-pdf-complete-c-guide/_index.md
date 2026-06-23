---
category: general
date: 2026-02-26
description: Xuất workbook sang PDF với phông chữ được nhúng và cũng xuất biểu đồ
  sang PowerPoint bằng C#. Học cách sao chép worksheet bảng pivot và lưu workbook
  dưới dạng PPTX.
draft: false
keywords:
- export workbook to pdf
- export charts to powerpoint
- copy pivot table worksheet
- embed fonts pdf export
- save workbook as pptx
language: vi
og_description: Xuất workbook sang PDF với phông chữ được nhúng và cũng xuất biểu
  đồ sang PowerPoint bằng C#. Thực hiện theo hướng dẫn từng bước để sao chép bảng
  pivot và lưu dưới dạng PPTX.
og_title: Xuất Workbook sang PDF – Hướng dẫn C# toàn diện
tags:
- Aspose.Cells
- Aspose.Slides
- C#
- Reporting
title: Xuất Workbook sang PDF – Hướng dẫn C# đầy đủ
url: /vi/net/conversion-to-pdf/export-workbook-to-pdf-complete-c-guide/
---

content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Xuất Workbook sang PDF – Hướng Dẫn Toàn Diện C#

Xuất workbook sang PDF là một yêu cầu phổ biến khi bạn cần chia sẻ báo cáo với các bên liên quan có thể không cài đặt Excel. Trong hướng dẫn này, chúng tôi cũng sẽ chỉ cho bạn cách **xuất biểu đồ sang PowerPoint**, sao chép **worksheet PivotTable**, và nhúng phông chữ để PDF trông giống hệt thiết kế trên màn hình của bạn.  

Bạn có bao giờ tự hỏi tại sao một số PDF lại mất bố cục gốc hoặc tại sao các slide PowerPoint lại thiếu các hình dạng không? Câu trả lời thường nằm ở việc thiếu các tùy chọn trong quá trình xuất. Khi kết thúc hướng dẫn này, bạn sẽ có một phương thức C# duy nhất, có thể tái sử dụng, xử lý tất cả những vấn đề đó—không còn phải sao chép‑dán thủ công hay điều chỉnh các cài đặt xuất nữa.

## Những Điều Bạn Sẽ Học

- Cách tạo một workbook, thêm các biểu thức Smart Marker và xử lý chúng.  
- Cách **sao chép một worksheet PivotTable** mà không làm phá vỡ nguồn dữ liệu.  
- Cách **xuất biểu đồ, hình dạng và hộp văn bản** sang một bản trình bày PowerPoint trong khi vẫn giữ chúng có thể chỉnh sửa.  
- Cách **nhúng phông chữ tiêu chuẩn** khi xuất PDF để đảm bảo hiển thị nhất quán trên bất kỳ máy nào.  
- Cách **lưu workbook dưới dạng PPTX** bằng cách sử dụng phương pháp `save workbook as pptx`.  

Tất cả những điều này hoạt động với các thư viện Aspose.Cells và Aspose.Slides .NET mới nhất (phiên bản 23.11 tại thời điểm viết). Không cần công cụ bên ngoài, không có script xử lý hậu kỳ—chỉ C# thuần.

> **Pro tip:** Nếu bạn đã sử dụng Aspose trong dự án của mình, bạn có thể chèn các đoạn mã như hiện có; nếu không, hãy thêm các gói NuGet `Aspose.Cells` và `Aspose.Slides` trước.

## Yêu Cầu Trước

- .NET 6.0 trở lên (mã cũng chạy trên .NET Framework 4.7.2).  
- Visual Studio 2022 (hoặc bất kỳ IDE nào bạn thích).  
- Aspose.Cells .NET và Aspose.Slides .NET được cài đặt qua NuGet.  
- Kiến thức cơ bản về C# và các khái niệm Excel như Smart Markers và PivotTables.

---

![Export workbook to PDF diagram](export-workbook-to-pdf.png "Export workbook to PDF workflow showing PDF and PPTX outputs")

## Xuất Workbook sang PDF – Triển Khai Từng Bước

Dưới đây là ví dụ đầy đủ, sẵn sàng chạy. Nó tạo một workbook, chèn các biểu thức Smart Marker, xử lý chúng, sao chép một vùng PivotTable, và cuối cùng lưu cả file PDF và PowerPoint.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides.Export;

namespace ReportExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Build the workbook and add Smart Markers
            // -------------------------------------------------
            var reportWorkbook = new Workbook();
            Worksheet dataSheet = reportWorkbook.Worksheets[0];

            // Header with a variable department name
            dataSheet.Cells["A1"].PutValue("Report for ${$dept=Department}");

            // Conditional text based on department
            dataSheet.Cells["A2"].PutValue("${if $dept == \"Sales\"}Sales Summary${else}Other Summary${/if}");

            // Table header for orders – this will be repeated for each order
            dataSheet.Cells["A5:D5"].PutValue("${Orders.Product}|${Orders.Quantity}|${Orders.Price}");

            // -------------------------------------------------
            // Step 2: Process Smart Markers and name the detail sheet
            // -------------------------------------------------
            reportWorkbook.SmartMarkerProcessor.Options.DetailSheetNewName = "Orders_${$dept}";
            reportWorkbook.SmartMarkerProcessor.Process();

            // -------------------------------------------------
            // Step 3: Copy the range that contains the pivot table
            // -------------------------------------------------
            // Assume the pivot table lives in A1:G30 on the original sheet
            Range sourceRange = dataSheet.Cells.CreateRange("A1", "G30");
            Worksheet copySheet = reportWorkbook.Worksheets.Add("Copy");
            sourceRange.Copy(copySheet.Cells["A1"]);   // Pivot table is duplicated intact

            // -------------------------------------------------
            // Step 4: Export to PowerPoint (keep charts, shapes, text boxes)
            // -------------------------------------------------
            var pptOptions = new PresentationOptions
            {
                ExportCharts = true,
                ExportShapes = true,
                ExportTextBoxes = true
            };
            string pptPath = @"C:\Temp\FinalPresentation.pptx";
            reportWorkbook.Save(pptPath, SaveFormat.Pptx, pptOptions);

            // -------------------------------------------------
            // Step 5: Export to PDF and embed standard fonts
            // -------------------------------------------------
            var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
            string pdfPath = @"C:\Temp\FinalReport.pdf";
            reportWorkbook.Save(pdfPath, pdfOptions);

            Console.WriteLine("Export completed:");
            Console.WriteLine($" • PDF saved to {pdfPath}");
            Console.WriteLine($" • PowerPoint saved to {pptPath}");
        }
    }
}
```

### Tại Sao Điều Này Hoạt Động

1. **Xử lý Smart Marker** cho phép bạn điền dữ liệu vào workbook từ bất kỳ nguồn dữ liệu nào (JSON, DataTables, v.v.) mà không cần viết vòng lặp.  
2. **DetailSheetNewName** tạo một sheet riêng cho mỗi phòng ban, cung cấp cho bạn một tab sạch sẽ, riêng biệt cho từng phòng ban.  
3. **Sao chép vùng** (`sourceRange.Copy`) nhân bản PivotTable *kèm theo* cache của nó, vì vậy sheet được sao chép hoạt động giống hệt như bản gốc.  
4. **PresentationOptions** với `ExportCharts`, `ExportShapes` và `ExportTextBoxes` chỉ định cho Aspose render các đối tượng này dưới dạng phần tử PowerPoint gốc, giữ được khả năng chỉnh sửa.  
5. **PdfSaveOptions.EmbedStandardFonts** đảm bảo PDF trông giống hệt trên các máy không cài đặt phông chữ gốc.  

Kết quả là hai tệp—`FinalReport.pdf` và `FinalPresentation.pptx`—có thể được gửi email, lưu trữ, hoặc hiển thị trong bất kỳ trình xem nào mà không mất độ chính xác.

## Xuất Biểu Đồ sang PowerPoint (Lưu Workbook dưới dạng PPTX)

Nếu báo cáo của bạn chứa biểu đồ, bạn có thể muốn chúng có thể chỉnh sửa trong PowerPoint. Lớp `PresentationOptions` là chìa khóa. Dưới đây là một đoạn mã tập trung chỉ phần xuất biểu đồ:

```csharp
// Assuming reportWorkbook already contains charts
var pptExportOptions = new PresentationOptions
{
    ExportCharts = true,      // Convert Excel charts to PowerPoint chart objects
    ExportShapes = false,    // Skip shapes if you don’t need them
    ExportTextBoxes = true   // Keep any text boxes editable
};

string pptFile = @"C:\Temp\ChartsOnly.pptx";
reportWorkbook.Save(pptFile, SaveFormat.Pptx, pptExportOptions);
```

**What happens under the hood?** Aspose chuyển đổi mỗi biểu đồ Excel thành một biểu đồ PowerPoint gốc, giữ lại các series, tiêu đề trục và định dạng. Điều này tốt hơn nhiều so với việc xuất biểu đồ dưới dạng hình ảnh tĩnh, vì khán giả của bạn có thể điều chỉnh các điểm dữ liệu sau này.

## Sao Chép Worksheet PivotTable mà Không Mất Dữ Liệu

PivotTable thường là phần khó nhất trong quá trình xuất vì chúng dựa vào một cache ẩn. Phương thức `Copy` đơn giản hoạt động vì Aspose sao chép cả vùng hiển thị **và** đối tượng cache nền.

```csharp
// Copy the whole sheet (including pivot table) to a new workbook
Workbook clone = new Workbook();
reportWorkbook.Worksheets[0].CopyTo(clone.Worksheets[0]);
clone.Save(@"C:\Temp\PivotCopy.xlsx", SaveFormat.Xlsx);
```

> **Note:** Nếu bạn chỉ cần PivotTable trên một sheet mới trong cùng workbook, cách tiếp cận `sourceRange.Copy` ở trên nhẹ hơn và tránh tạo một workbook mới hoàn toàn.

## Nhúng Phông Chữ cho Xuất PDF – Tại Sao Điều Này Quan Trọng

Khi bạn mở một PDF trên máy không có phông chữ gốc, văn bản có thể bị dịch chuyển, ngắt dòng thay đổi, hoặc ký tự biến mất. Thiết lập `EmbedStandardFonts = true` cho Aspose nhúng các phông chữ phổ biến nhất (Arial, Times New Roman, v.v.) trực tiếp vào luồng PDF.  

Nếu bạn sử dụng phông chữ tùy chỉnh, chuyển sang `PdfSaveOptions.FontEmbeddingMode = FontEmbeddingMode.EmbedAll`. Dưới đây là một ví dụ:

```csharp
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    FontEmbeddingMode = FontEmbeddingMode.EmbedAll   // For custom fonts
};
reportWorkbook.Save(@"C:\Temp\CustomFontReport.pdf", pdfOpts);
```

Bây giờ mọi người nhận sẽ thấy cùng một bố cục bạn thiết kế—không có bất ngờ.

## Tổng Kết Ví Dụ Hoạt Động Đầy Đủ

Kết hợp mọi thứ lại, chương trình hoàn chỉnh (được hiển thị ở trên) thực hiện các bước sau:

1. **Tạo** một workbook với các placeholder Smart Marker.  
2. **Xử lý** các marker, tạo một sheet chi tiết có tên theo phòng ban.  
3. **Sao chép** một vùng chứa PivotTable sang một worksheet mới, giữ nguyên chức năng của nó.  
4. **Xuất** workbook sang PowerPoint, giữ các biểu đồ, hình dạng và hộp văn bản có thể chỉnh sửa.  
5. **Xuất** cùng một workbook sang PDF đồng thời nhúng phông chữ tiêu chuẩn để hiển thị đáng tin cậy.  

Chạy chương trình, mở các tệp đã tạo, và bạn sẽ thấy:

- **PDF**: Bảng rõ nét, phông chữ được nhúng, và cùng phong cách trực quan như nguồn Excel.  
- **PowerPoint**: Biểu đồ có thể chỉnh sửa mà bạn có thể chuột phải → *Edit Data* trong PowerPoint, và các hình dạng vẫn hoàn toàn có thể thao tác.

---

## Câu Hỏi Thường Gặp (FAQ)

**Q: Điều này có hoạt động với .NET Core không?**  
Có—Aspose.Cells và Aspose.Slides là đa nền tảng. Chỉ cần nhắm mục tiêu .NET 6 trở lên và cùng một đoạn mã sẽ chạy trên Windows, Linux hoặc macOS.

**Q: Nếu tôi chỉ cần xuất một phần của các sheet thì sao?**  
Sử dụng `Workbook.Save` với `SaveOptions` cho phép bạn chỉ định `SheetNames`. Ví dụ: `new PresentationOptions { SheetNames = new[] { "Copy" } }`.

**Q: Tôi có thể mã hoá PDF không?**  
Chắc chắn. Đặt `PdfSaveOptions.EncryptionDetails` với mật khẩu trước khi gọi `Save`.

**Q: PivotTable của tôi sử dụng nguồn dữ liệu bên ngoài—việc sao chép có làm mất liên kết không?**  
Hoạt động sao chép bao gồm cache, không bao gồm kết nối bên ngoài. Pivot sẽ vẫn hoạt động offline, nhưng sẽ không làm mới dữ liệu từ nguồn gốc. Nếu bạn cần làm mới trực tiếp, hãy xuất dữ liệu nguồn cùng với workbook.

## Các Bước Tiếp Theo & Chủ Đề Liên Quan

- **Dynamic Data Sources** – Tìm hiểu cách cung cấp JSON hoặc DataTable vào Smart Markers cho báo cáo thời gian thực.  
- **Advanced PDF Styling** – Explore `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}