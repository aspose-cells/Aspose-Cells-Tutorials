---
category: general
date: 2026-06-27
description: Cách xuất Excel bằng C# — học cách chuyển Excel sang PowerPoint, tạo
  PowerPoint từ Excel và tải workbook Excel bằng C# trong vài phút.
draft: false
keywords:
- how to export excel
- convert excel to powerpoint
- create powerpoint from excel
- load excel workbook c#
- export excel chart powerpoint
language: vi
og_description: Cách xuất Excel bằng C# rất đơn giản. Hãy làm theo hướng dẫn từng
  bước này để chuyển đổi Excel sang PowerPoint, tạo PowerPoint từ Excel và tải workbook
  Excel bằng C#.
og_title: Cách xuất Excel sang PowerPoint – Hướng dẫn C# đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: How to export Excel using C#—learn to convert Excel to PowerPoint,
    create PowerPoint from Excel, and load Excel workbook C# in minutes.
  headline: How to Export Excel to PowerPoint – Complete C# Guide
  type: TechArticle
- description: How to export Excel using C#—learn to convert Excel to PowerPoint,
    create PowerPoint from Excel, and load Excel workbook C# in minutes.
  name: How to Export Excel to PowerPoint – Complete C# Guide
  steps:
  - name: '**Load Excel workbook** – We read the `.xlsx` file into memory.'
    text: '**Load Excel workbook** – We read the `.xlsx` file into memory.'
  - name: '**Convert workbook to a PowerPoint presentation** – Aspose converts each
      worksheet (or selected chart) into a slide.'
    text: '**Convert workbook to a PowerPoint presentation** – Aspose converts each
      worksheet (or selected chart) into a slide.'
  - name: '**Save the generated presentation** – The final PPTX can be opened in PowerPoint,
      edited, or sent to stakeholders.'
    text: '**Save the generated presentation** – The final PPTX can be opened in PowerPoint,
      edited, or sent to stakeholders.'
  type: HowTo
- questions:
  - answer: Yes. Use `Workbook.Worksheets["Sheet1"]` to isolate a sheet, then call
      `SaveToPresentation` on that worksheet alone.
    question: Can I export only a single worksheet instead of the whole workbook?
  - answer: Macros are not transferred to PowerPoint—only visual objects (charts,
      tables) are exported. If you need macro functionality, consider generating the
      slides first, then adding VBA manually.
    question: What about preserving macros?
  - answer: Absolutely. Aspose.Cells supports legacy formats; just change the file
      extension in `excelPath`.
    question: Does this work with `.xls` files?
  - answer: 'After creating the `Presentation` object, set: ```csharp presentation.SlideSize.Size
      = SlideSizeType.Widescreen; ```'
    question: How do I change the slide size to widescreen (16:9)?
  - answer: 'Open‑source libraries like EPPlus can read Excel, but they don’t provide
      direct Excel‑to‑PowerPoint conversion. You’d need to manually render charts
      to images and insert them, which is far more code. ## Tips & Best Practices
      - **Batch processing:** If you have dozens of workbooks, wrap the conversio'
    question: Is there a free alternative?
  type: FAQPage
tags:
- C#
- Excel
- PowerPoint
- Aspose
title: Cách xuất Excel sang PowerPoint – Hướng dẫn C# đầy đủ
url: /vi/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách xuất Excel sang PowerPoint – Hướng dẫn đầy đủ C#

Bạn đã bao giờ tự hỏi **cách xuất Excel** dữ liệu trực tiếp vào một bộ slide PowerPoint mà không mất định dạng chưa? Bạn không phải là người duy nhất. Trong nhiều quy trình báo cáo, nút thắt là việc chuyển biểu đồ và bảng từ một workbook Excel sang một bộ slide mượt mà. Tin tốt? Chỉ với vài dòng C# bạn có thể **chuyển đổi Excel sang PowerPoint**, tạo ra một tệp PPTX có thể chỉnh sửa hoàn toàn, và thậm chí giữ nguyên độ chính xác của biểu đồ.

Trong hướng dẫn này, chúng tôi sẽ hướng dẫn cách tải một workbook Excel trong C#, chuyển nội dung của nó thành một bản trình chiếu PowerPoint, và lưu kết quả. Khi kết thúc, bạn sẽ có thể **tạo PowerPoint từ Excel** một cách tự động—không cần sao chép‑dán thủ công. Không có các thao tác UI phức tạp, chỉ cần mã sạch.

> **Bạn sẽ cần**  
> * .NET 6+ (hoặc .NET Framework 4.7.2+)  
> * Các gói NuGet Aspose.Cells và Aspose.Slides (chúng thực hiện phần công việc nặng)  
> * Một tệp Excel mẫu có ít nhất một biểu đồ (chúng tôi sẽ gọi nó là `chartOle.xlsx`)  

![Diagram showing how to export Excel to PowerPoint using C#](https://example.com/images/export-excel-to-pptx.png "How to Export Excel to PowerPoint diagram")

## Cách xuất Excel sang PowerPoint với C# – Tổng quan

Trước khi bắt đầu viết mã, việc hiểu quy trình ba bước sẽ rất hữu ích:

1. **Load Excel workbook** – Chúng ta đọc tệp `.xlsx` vào bộ nhớ.  
2. **Convert workbook to a PowerPoint presentation** – Aspose chuyển mỗi worksheet (hoặc biểu đồ đã chọn) thành một slide.  
3. **Save the generated presentation** – Tệp PPTX cuối cùng có thể được mở trong PowerPoint, chỉnh sửa, hoặc gửi cho các bên liên quan.

Mỗi bước được tách riêng một cách có chủ đích để bạn có thể thay thế bằng logic tùy chỉnh sau này (ví dụ: chọn các sheet cụ thể, áp dụng giao diện slide, v.v.). Bây giờ chúng ta hãy phân tích chi tiết.

## Bước 1 – Tải Workbook Excel theo phong cách C#

Điều đầu tiên bạn phải làm là đưa tệp Excel vào ứng dụng của mình. Sử dụng Aspose.Cells, mã sẽ rất đơn giản:

```csharp
using Aspose.Cells;   // Handles Excel files
using Aspose.Slides;  // Handles PowerPoint files
using System;

// Step 1: Load the Excel workbook
string excelPath = @"YOUR_DIRECTORY\chartOle.xlsx";

if (!System.IO.File.Exists(excelPath))
{
    throw new FileNotFoundException($"Excel file not found at {excelPath}");
}

// The Workbook class reads the .xlsx file into memory
Workbook workbook = new Workbook(excelPath);
```

**Tại sao điều này quan trọng:**  
`Workbook` trừu tượng hoá toàn bộ bảng tính, cho phép bạn truy cập vào các worksheet, ô, và—đặc biệt—các biểu đồ nhúng. Nếu bạn bỏ qua việc kiểm tra tồn tại, sau này sẽ nhận được một `FileNotFoundException` mơ hồ, gây khó khăn trong việc gỡ lỗi ở môi trường production.

**Mẹo chuyên nghiệp:** Nếu bạn chỉ cần một sheet cụ thể, bạn có thể truyền một đối tượng `LoadOptions` để giới hạn việc sử dụng bộ nhớ:

```csharp
LoadOptions options = new LoadOptions(LoadFormat.Xlsx) { LoadDataOnly = true };
Workbook workbook = new Workbook(excelPath, options);
```

Cải tiến nhỏ này sẽ tăng tốc đáng kể cho các workbook lớn.

## Bước 2 – Chuyển đổi Excel sang PowerPoint (Xuất biểu đồ Excel sang PowerPoint)

Bây giờ là phần kỳ diệu: chuyển workbook thành một tệp PPTX. Aspose.Slides cung cấp một phương thức duy nhất thực hiện công việc nặng:

```csharp
// Step 2: Convert the workbook to a PowerPoint presentation (PPTX format)
Presentation presentation = workbook.SaveToPresentation(ExportToPresentationFormat.Pptx);
```

**Điều gì đang diễn ra bên trong?**  
`SaveToPresentation` lặp qua mỗi worksheet, trích xuất các đối tượng biểu đồ, và tạo một slide cho mỗi biểu đồ. Phương thức này giữ nguyên kiểu dáng biểu đồ gốc, vì vậy màu sắc, phông chữ và nhãn dữ liệu vẫn được giữ nguyên. Nếu workbook của bạn chứa các bảng thuần, chúng sẽ được hiển thị dưới dạng hộp văn bản trên slide.

**Trường hợp đặc biệt – nhiều biểu đồ:**  
Nếu một worksheet có hơn một biểu đồ, Aspose sẽ xếp chúng theo chiều dọc trên cùng một slide. Để giữ chúng trên các slide riêng biệt, bạn có thể lặp qua các biểu đồ một cách thủ công:

```csharp
Presentation presentation = new Presentation();

foreach (Worksheet sheet in workbook.Worksheets)
{
    foreach (Chart chart in sheet.Charts)
    {
        // Export each chart as an individual slide
        ISlide slide = presentation.Slides.AddEmptySlide(presentation.SlideSize.Size);
        chart.ExportToSlide(presentation, slide);
    }
}
```

Đoạn mã này cung cấp cho bạn kiểm soát chi tiết—hoàn hảo cho một bộ slide chuyên nghiệp.

## Bước 3 – Lưu bản trình chiếu đã tạo (Tạo PowerPoint từ Excel)

Bước cuối cùng là lưu tệp PPTX vào đĩa. Thật đơn giản như sau:

```csharp
// Step 3: Save the generated presentation to a file
string pptxPath = @"YOUR_DIRECTORY\editable.pptx";
presentation.Save(pptxPath, Aspose.Slides.Export.SaveFormat.Pptx);

Console.WriteLine($"Presentation saved successfully to {pptxPath}");
```

**Tại sao bạn nên kiểm tra đầu ra:**  
Sau khi lưu, mở `editable.pptx` trong PowerPoint. Bạn sẽ thấy một slide cho mỗi biểu đồ, mỗi slide đều có thể chỉnh sửa hoàn toàn (bạn có thể thay đổi màu sắc, di chuyển đối tượng, v.v.). Nếu một biểu đồ trông không đúng, hãy kiểm tra lại rằng biểu đồ Excel gốc sử dụng phông chữ tiêu chuẩn—một số phông chữ tùy chỉnh có thể không được nhúng đúng cách.

**Cạm bẫy thường gặp:**  
Lưu vào một thư mục chia sẻ mạng mà không có quyền thích hợp sẽ gây ra `UnauthorizedAccessException`. Đảm bảo tài khoản đang chạy có quyền ghi vào `YOUR_DIRECTORY`.

## Ví dụ hoàn chỉnh – Tất cả các bước cùng nhau

Dưới đây là chương trình hoàn chỉnh, sẵn sàng chạy. Dán nó vào một dự án Console App mới, khôi phục các gói NuGet, và nhấn **F5**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Paths – adjust to your environment
            string excelPath = @"YOUR_DIRECTORY\chartOle.xlsx";
            string pptxPath = @"YOUR_DIRECTORY\editable.pptx";

            // -------------------------------------------------
            // Step 1: Load the Excel workbook (load excel workbook c#)
            // -------------------------------------------------
            if (!System.IO.File.Exists(excelPath))
            {
                Console.WriteLine($"Error: File not found -> {excelPath}");
                return;
            }

            Workbook workbook = new Workbook(excelPath);
            Console.WriteLine("Excel workbook loaded successfully.");

            // -------------------------------------------------
            // Step 2: Convert Excel to PowerPoint (export excel chart powerpoint)
            // -------------------------------------------------
            Presentation presentation = workbook.SaveToPresentation(ExportToPresentationFormat.Pptx);
            Console.WriteLine("Workbook converted to PowerPoint.");

            // -------------------------------------------------
            // Step 3: Save the generated presentation (create powerpoint from excel)
            // -------------------------------------------------
            presentation.Save(pptxPath, Aspose.Slides.Export.SaveFormat.Pptx);
            Console.WriteLine($"Presentation saved at: {pptxPath}");
        }
    }
}
```

**Kết quả mong đợi (console):**

```
Excel workbook loaded successfully.
Workbook converted to PowerPoint.
Presentation saved at: YOUR_DIRECTORY\editable.pptx
```

Mở `editable.pptx` và bạn sẽ thấy một slide cho mỗi biểu đồ, sẵn sàng để chỉnh sửa thêm.

## Câu hỏi thường gặp (FAQs)

**Hỏi: Tôi có thể xuất chỉ một worksheet duy nhất thay vì toàn bộ workbook không?**  
Đáp: Có. Sử dụng `Workbook.Worksheets["Sheet1"]` để cô lập một sheet, sau đó gọi `SaveToPresentation` chỉ trên worksheet đó.

**Hỏi: Còn việc giữ lại macro thì sao?**  
Đáp: Macro không được chuyển sang PowerPoint—chỉ các đối tượng trực quan (biểu đồ, bảng) được xuất. Nếu bạn cần chức năng macro, hãy cân nhắc tạo slide trước, sau đó thêm VBA một cách thủ công.

**Hỏi: Điều này có hoạt động với tệp `.xls` không?**  
Đáp: Hoàn toàn có. Aspose.Cells hỗ trợ các định dạng cũ; chỉ cần thay đổi phần mở rộng tệp trong `excelPath`.

**Hỏi: Làm sao để thay đổi kích thước slide thành dạng màn hình rộng (16:9)?**  
Đáp: Sau khi tạo đối tượng `Presentation`, đặt:

```csharp
presentation.SlideSize.Size = SlideSizeType.Widescreen;
```

**Hỏi: Có giải pháp miễn phí nào không?**  
Đáp: Các thư viện mã nguồn mở như EPPlus có thể đọc Excel, nhưng chúng không cung cấp chuyển đổi trực tiếp từ Excel sang PowerPoint. Bạn sẽ phải tự vẽ biểu đồ thành hình ảnh và chèn chúng, điều này đòi hỏi nhiều mã hơn rất nhiều.

## Mẹo & Thực hành tốt nhất

- **Xử lý hàng loạt:** Nếu bạn có hàng chục workbook, hãy bao bọc quá trình chuyển đổi trong một vòng lặp `Parallel.ForEach`—chỉ cần cẩn thận với các đối tượng Aspose không an toàn với đa luồng.  
- **Quản lý bộ nhớ:** Gọi `presentation.Dispose()` và `workbook.Dispose()` khi làm việc với tệp lớn để giải phóng tài nguyên gốc kịp thời.  
- **Định dạng slide:** Sau khi chuyển đổi, bạn có thể áp dụng một giao diện master slide bằng `presentation.SlideMaster` để tất cả các slide có giao diện đồng nhất.  
- **Kiểm thử:** Tự động hoá một unit test đơn giản tải một workbook đã biết, thực hiện chuyển đổi, và xác nhận rằng PPTX kết quả chứa số slide mong đợi.

## Kết luận

Chúng tôi vừa trình bày **cách xuất dữ liệu Excel** vào một bộ slide PowerPoint bằng C#. Bằng cách tải workbook, chuyển đổi nó bằng Aspose, và lưu PPTX, bạn giờ đã có một cách lặp lại, lập trình để **chuyển đổi Excel sang PowerPoint**, **tạo PowerPoint từ Excel**, và **tải workbook Excel theo phong cách C#** mà không cần công sức thủ công. Mã nguồn độc lập, hoạt động với bất kỳ runtime .NET hiện đại nào, và có thể mở rộng để phù hợp với các quy trình báo cáo phức tạp.

Sẵn sàng cho thử thách tiếp theo? Hãy thử nhúng nhiều biểu đồ vào mỗi slide, áp dụng bố cục slide tùy chỉnh, hoặc thậm chí tự động tạo ghi chú cho người thuyết trình. Không có giới hạn khi bạn kết hợp tự động hoá Excel với việc tạo PowerPoint.

Có câu hỏi hoặc trường hợp sử dụng thú vị? Hãy để lại bình luận bên dưới, và chúc bạn lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên đều có các ví dụ mã hoàn chỉnh, kèm theo giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [How to Export Excel to HTML with Grid Lines Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/export-excel-to-html-grid-lines-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}