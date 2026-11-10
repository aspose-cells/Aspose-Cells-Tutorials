---
category: general
date: 2026-09-15
description: Tìm hiểu cách nhúng phông chữ vào SVG và xuất biểu đồ Excel sang PowerPoint,
  bao gồm chuyển đổi XLSX sang SVG và chuyển đổi XLSX sang PPTX với các ví dụ mã đầy
  đủ.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in SVG
- export excel chart to powerpoint
- convert xlsx to svg
- convert xlsx to pptx
- save workbook as svg
language: vi
lastmod: 2026-09-15
og_description: Nhúng phông chữ vào SVG và xuất biểu đồ Excel sang PowerPoint với
  mã C# hướng dẫn từng bước. Chuyển đổi XLSX sang SVG và XLSX sang PPTX nhanh chóng
  và đáng tin cậy.
og_image_alt: Screenshot showing an Excel chart exported to PowerPoint with embedded
  fonts in the resulting SVG file
og_title: Nhúng phông chữ trong SVG và xuất biểu đồ Excel sang PowerPoint – hướng
  dẫn đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  headline: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  type: TechArticle
- description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  name: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  steps:
  - name: Open `EditableChart.pptx` in PowerPoint.
    text: Open `EditableChart.pptx` in PowerPoint.
  - name: Locate the slide containing the chart.
    text: Locate the slide containing the chart.
  - name: Choose **Chart Tools → Design → Edit Data**.
    text: Choose **Chart Tools → Design → Edit Data**.
  - name: Confirm that the Excel‑style data grid appears and that you can change values.
    text: Confirm that the Excel‑style data grid appears and that you can change values.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cách nhúng phông chữ vào SVG khi chuyển đổi tệp Excel sang SVG và PowerPoint
url: /vi/net/converting-excel-files-to-other-formats/how-to-embed-fonts-in-svg-when-converting-excel-files-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách nhúng phông chữ vào SVG khi chuyển đổi tệp Excel sang SVG và PowerPoint  

Nếu bạn cần **nhúng phông chữ vào SVG** khi chuyển đổi một workbook Excel, hướng dẫn này sẽ chỉ cho bạn cách thực hiện chính xác. Bạn cũng sẽ học cách **xuất biểu đồ Excel sang PowerPoint**, và cách **chuyển đổi XLSX sang SVG** và **chuyển đổi XLSX sang PPTX** với biểu đồ có thể chỉnh sửa.  

Làm việc với dữ liệu Excel một cách lập trình thường đồng nghĩa với việc bạn phải di chuyển cùng một nội dung trực quan giữa các định dạng tệp khác nhau. Việc tự tay tạo lại biểu đồ trong PowerPoint hoặc áp dụng lại phông chữ trong SVG rất dễ gây lỗi và tốn thời gian. Khi kết thúc tutorial này, bạn sẽ có một đoạn mã C# duy nhất, có thể tái sử dụng, giúp:

* Lưu workbook dưới dạng tệp SVG với phông chữ được nhúng và các bộ chọn biến thể phông chữ.  
* Xuất cùng một workbook sang tệp PPTX, trong đó biểu đồ vẫn có thể chỉnh sửa.  

Yêu cầu duy nhất là một phiên bản mới của **Aspose.Cells for .NET** (2024‑x trở lên) và môi trường phát triển .NET như Visual Studio 2022.

---

## Những gì bạn sẽ cần  

* .NET 6.0 trở lên (đoạn mã cũng hoạt động trên .NET Framework 4.8).  
* Gói NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`).  
* Một tệp Excel (`input.xlsx`) chứa ít nhất một biểu đồ.  
* Quyền ghi vào thư mục đầu ra.  

---

## Nhúng phông chữ vào SVG khi chuyển đổi XLSX sang SVG  

Việc nhúng phông chữ đảm bảo SVG hiển thị đúng trên bất kỳ thiết bị nào, ngay cả khi hệ thống đích không có các kiểu chữ gốc. Lớp `SvgSaveOptions` cung cấp hai cờ cho phép thực hiện điều này: `EmbedFonts` và `FontVariationSelectors`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Load the workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// OPTIONAL: Use WRAPCOLS to reshape data before export (demonstrates a formula)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)"; // 2 columns per wrap
sheet.Calculate(); // Force calculation so the formula result appears

// Configure SVG options to embed fonts
SvgSaveOptions svgOptions = new SvgSaveOptions
{
    EmbedFonts = true,                // embed fonts in the SVG
    FontVariationSelectors = true    // include variation selectors for better Unicode handling
};

// Save the workbook as an SVG file
string svgPath = @"YOUR_DIRECTORY\WithFonts.svg";
workbook.Save(svgPath, svgOptions);
```

**Tại sao cách này hoạt động:**  
* `EmbedFonts = true` sao chép các tệp phông chữ vào phần `<defs>` của SVG, loại bỏ phụ thuộc bên ngoài.  
* `FontVariationSelectors = true` thêm các bộ chọn cần thiết cho các phông chữ hỗ trợ tính năng OpenType, bảo tồn các biến thể glyph như ligature.  

**Kết quả mong đợi:** Mở `WithFonts.svg` trong bất kỳ trình duyệt hiện đại nào; văn bản trong biểu đồ hoặc ô sẽ hiển thị đúng kiểu chữ đã dùng trong Excel, ngay cả trên máy không cài đặt phông chữ đó.

---

## Xuất biểu đồ Excel sang PowerPoint với biểu đồ có thể chỉnh sửa  

Khi bạn cần nhúng một biểu đồ vào slide PowerPoint nhưng vẫn muốn người nhận có thể chỉnh sửa dữ liệu biểu đồ, `PptxSaveOptions` của Aspose.Cells cung cấp cờ `ExportEditableChart`.

```csharp
// Configure PPTX options to keep charts editable after export
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableChart = true   // allow chart editing in PowerPoint
};

// Save the same workbook as a PPTX file
string pptxPath = @"YOUR_DIRECTORY\EditableChart.pptx";
workbook.Save(pptxPath, pptxOptions);
```

**Tại sao điều này quan trọng:**  
Đặt `ExportEditableChart` thành `true` sẽ lưu biểu đồ dưới dạng đối tượng chart XML của Office Open XML thay vì hình ảnh tĩnh. Khi mở `EditableChart.pptx` trong PowerPoint, bạn có thể chuột phải vào biểu đồ → **Edit Data** và sửa các series như một biểu đồ PowerPoint gốc.

**Các bước xác minh:**  

1. Mở `EditableChart.pptx` trong PowerPoint.  
2. Tìm slide chứa biểu đồ.  
3. Chọn **Chart Tools → Design → Edit Data**.  
4. Xác nhận rằng lưới dữ liệu kiểu Excel xuất hiện và bạn có thể thay đổi giá trị.

---

## Chuyển đổi XLSX sang SVG – tóm tắt quy trình đầy đủ  

Dưới đây là phiên bản ngắn gọn kết hợp việc tải, tùy chọn thao tác dữ liệu, và lưu dưới dạng SVG. Dùng đoạn này khi bạn chỉ cần đầu ra SVG.

```csharp
public void ConvertXlsxToSvg(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Example: apply a formula to demonstrate cell calculations
    Worksheet ws = wb.Worksheets[0];
    ws.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
    ws.Calculate();

    SvgSaveOptions opts = new SvgSaveOptions
    {
        EmbedFonts = true,
        FontVariationSelectors = true
    };

    wb.Save(outputPath, opts);
}
```

Gọi phương thức như sau:

```csharp
ConvertXlsxToSvg(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.svg");
```

**Mẹo trường hợp đặc biệt:** Nếu workbook của bạn chứa các phông chữ tùy chỉnh chưa được cài đặt trên server, hãy nhúng chúng thủ công trước khi gọi `Save`. Sử dụng `FontInfoCollection` để thêm các tệp phông chữ vào `SvgSaveOptions` qua thuộc tính `CustomFonts` (có trong các phiên bản Aspose.Cells mới hơn).

---

## Chuyển đổi XLSX sang PPTX – bảo toàn khả năng chỉnh sửa biểu đồ  

Phương thức trợ giúp dưới đây minh họa đường dẫn **convert XLSX to PPTX** đồng thời đảm bảo biểu đồ vẫn có thể chỉnh sửa.

```csharp
public void ConvertXlsxToPptx(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Ensure any chart you want to keep editable is on the first worksheet
    // (Aspose.Cells exports only the first worksheet by default for PPTX)
    PptxSaveOptions opts = new PptxSaveOptions
    {
        ExportEditableChart = true
    };

    wb.Save(outputPath, opts);
}
```

Cách dùng:

```csharp
ConvertXlsxToPptx(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.pptx");
```

**Câu hỏi thường gặp:** *Nếu workbook của tôi có nhiều worksheet chứa biểu đồ thì sao?*  
**Trả lời:** Aspose.Cells mặc định xuất worksheet đầu tiên. Để bao gồm các sheet khác, hãy lặp qua `workbook.Worksheets`, sao chép mỗi biểu đồ vào một slide mới, và lưu từng slide riêng biệt bằng các đối tượng `Presentation` từ Aspose.Slides. Kịch bản nâng cao này nằm ngoài luồng “lưu workbook dưới dạng SVG” và “xuất biểu đồ Excel sang PowerPoint” cơ bản, nhưng các cờ cốt lõi vẫn giữ nguyên.

---

## Mẹo thực tiễn và những cạm bẫy  

* **Hiệu năng:** Nhúng phông chữ làm tăng kích thước tệp SVG. Nếu kích thước là mối quan tâm, đặt `EmbedFonts = false` và dựa vào các phông chữ web‑safe.  
* **Giấy phép phông chữ:** Đảm bảo bạn có quyền nhúng các phông chữ đang dùng; một số phông chữ thương mại hạn chế việc nhúng.  
* **Tương thích biểu đồ:** Các biểu đồ có thể chỉnh sửa được lưu dưới dạng phần `chart.xml` bên trong PPTX. Các biểu đồ rất phức tạp (ví dụ: 3‑D hoặc combo) có thể mất một số kiểu khi chỉnh sửa trong PowerPoint. Hãy kiểm tra các loại biểu đồ phổ biến mà bạn cần.  
* **Không khớp phiên bản:** Cờ `ExportEditableChart` yêu cầu Aspose.Cells 20.10 trở lên. Sử dụng phiên bản cũ hơn sẽ tự động chuyển sang hình ảnh raster mà không báo lỗi.  
* **An toàn đa luồng:** Các đối tượng Workbook không an toàn khi dùng đa luồng. Tạo một thể hiện `Workbook` mới cho mỗi yêu cầu trong kịch bản dịch vụ web.  

---

## Ví dụ toàn diện từ đầu đến cuối  

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class ExcelExportDemo
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputFile = @"YOUR_DIRECTORY\input.xlsx";
        string svgFile   = @"YOUR_DIRECTORY\WithFonts.svg";
        string pptxFile  = @"YOUR_DIRECTORY\EditableChart.pptx";

        // 1. Load workbook
        Workbook workbook = new Workbook(inputFile);

        // 2. Optional: reshape data using WRAPCOLS
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
        sheet.Calculate();

        // 3. Save as SVG with embedded fonts
        SvgSaveOptions svgOpts = new SvgSaveOptions
        {
            EmbedFonts = true,
            FontVariationSelectors = true
        };
        workbook.Save(svgFile, svgOpts);
        Console.WriteLine($"SVG saved with embedded fonts to: {svgFile}");

        // 4. Save as PPTX with editable chart
        PptxSaveOptions pptxOpts = new PptxSaveOptions
        {
            ExportEditableChart = true
        };
        workbook.Save(pptxFile, pptxOpts);
        Console.WriteLine($"PPTX saved with editable chart to: {pptxFile}");
    }
}
```

Chạy chương trình này sẽ tạo ra hai tệp:

* **WithFonts.svg** – một SVG hiển thị chính xác như trong Excel, bao gồm cả phông chữ.  
* **EditableChart.pptx** – một bản trình chiếu PowerPoint trong đó biểu đồ có thể chỉnh sửa trực tiếp.

---

## Kết luận  

Bây giờ bạn đã biết cách **nhúng phông chữ vào SVG** khi **chuyển đổi XLSX sang SVG**, và cách **xuất biểu đồ Excel sang PowerPoint** đồng thời giữ cho biểu đồ có thể chỉnh sửa. Đoạn mã trên cũng cho thấy cách sạch sẽ để **lưu workbook dưới dạng SVG** và **chuyển đổi XLSX sang PPTX** với ít nỗ lực.  

Từ đây bạn có thể khám phá các chủ đề tiếp theo như:

* Thêm phông chữ tùy chỉnh bằng mã (`svgOptions.CustomFonts`).  
* Xử lý hàng loạt nhiều workbook trong một dịch vụ nền.  
* Sử dụng Aspose.Slides để tạo các tệp PPTX đa slide kết hợp nhiều biểu đồ Excel.  

Thử nghiệm các tùy chọn, điều chỉnh các đoạn mã cho dự án của bạn, và tận hưởng việc chuyển đổi Excel‑to‑SVG/PPTX đáng tin cậy mà không cần xử lý thủ công. Chúc bạn lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã đầy đủ với hướng dẫn từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Convert Excel Charts to SVG Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/german/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/french/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}