---
category: general
date: 2026-03-30
description: Tạo PowerPoint từ Excel nhanh chóng bằng Aspose.Cells và Aspose.Slides.
  Tìm hiểu cách xuất worksheet dưới dạng hình ảnh và lưu bản trình chiếu dưới dạng
  PPTX trong C#.
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export worksheet as image
- save presentation as pptx
- export excel chart as picture
language: vi
og_description: Tạo PowerPoint từ Excel trong C# với Aspose. Xuất worksheet dưới dạng
  hình ảnh, giữ các hình dạng có thể chỉnh sửa và lưu kết quả dưới dạng PPTX.
og_title: Tạo PowerPoint từ Excel – Hướng dẫn C# đầy đủ
tags:
- Aspose
- C#
- Office Automation
title: Tạo PowerPoint từ Excel – Hướng dẫn C# chi tiết từng bước
url: /vi/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PowerPoint từ Excel – Hướng dẫn C# đầy đủ

Bạn đã bao giờ cần **tạo PowerPoint từ Excel** nhưng không chắc thư viện nào có thể giữ cho biểu đồ của bạn vẫn có thể chỉnh sửa? Bạn không phải là người duy nhất. Trong nhiều kịch bản báo cáo, bạn sẽ muốn biến một bảng tính thành một bộ slide mà không mất khả năng tinh chỉnh các hộp văn bản sau này. Hướng dẫn này sẽ chỉ cho bạn cách **chuyển đổi Excel sang PowerPoint** bằng cách sử dụng Aspose.Cells và Aspose.Slides, đồng thời đề cập cách **xuất worksheet dưới dạng hình ảnh** và cuối cùng **lưu bản trình chiếu dưới dạng PPTX**.

Chúng ta sẽ đi qua từng dòng mã, giải thích *tại sao* mỗi thiết lập quan trọng, và thậm chí thảo luận cách xử lý nếu workbook của bạn chứa các biểu đồ phức tạp mà bạn muốn xuất dưới dạng hình ảnh. Khi hoàn thành, bạn sẽ có một ứng dụng console C# sẵn sàng chạy, nhận `ShapesDemo.xlsx` và tạo ra `Result.pptx` – tất cả với các hộp văn bản có thể chỉnh sửa và hình ảnh sắc nét.

## Những gì bạn cần

- .NET 6.0 hoặc phiên bản mới hơn (API cũng hoạt động với .NET Framework, nhưng .NET 6 là lựa chọn tối ưu).  
- Các gói NuGet **Aspose.Cells** và **Aspose.Slides** (giấy phép dùng thử miễn phí đủ cho việc thử nghiệm).  
- Kiến thức cơ bản về cú pháp C# – nếu bạn có thể viết `Console.WriteLine`, bạn đã sẵn sàng.  

Không cần COM interop bổ sung, không cần cài Office trên máy chủ, và không cần sao chép‑dán thủ công các hình ảnh. Mọi thứ đều được xử lý bằng mã.

---

## Tạo PowerPoint từ Excel – Tải Workbook và Đặt tùy chọn xuất

Điều đầu tiên chúng ta làm là mở file Excel và chỉ cho Aspose.Cells cách chúng ta muốn sheet được render. Đối tượng `ImageOrPrintOptions` là nơi phép thuật diễn ra: chúng ta bật `ExportShapes` và `ExportEditableTextBoxes` để bất kỳ shape nào (bao gồm biểu đồ) trở thành một phần của slide **và** vẫn có thể chỉnh sửa sau khi chuyển đổi.

```csharp
using Aspose.Cells;
using Aspose.Slides;

// 1️⃣ Load the Excel workbook
string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
Workbook workbook = new Workbook(excelPath);
Worksheet worksheet = workbook.Worksheets[0];   // Grab the first sheet

// 2️⃣ Configure image export – keep shapes editable
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    OnePagePerSheet = true,          // Export the whole sheet as one slide
    ExportShapes = true,             // Include shapes (charts, drawings)
    ExportEditableTextBoxes = true   // Make text boxes editable in PPTX
};
```

**Tại sao phải bật các flag này?**  
- `OnePagePerSheet` ngăn sheet bị chia thành nhiều slide – bạn sẽ nhận được một hình ảnh duy nhất, kích thước đầy đủ.  
- `ExportShapes` yêu cầu Aspose.Cells rasterize biểu đồ *và* các shape vector, giữ nguyên giao diện của chúng.  
- `ExportEditableTextBoxes` là “sốt bí mật” cho phép bạn double‑click vào một textbox trong PowerPoint và chỉnh sửa nội dung mà không cần mở lại Excel.

> **Mẹo chuyên nghiệp:** Nếu bạn chỉ cần một hình ảnh tĩnh của biểu đồ, hãy đặt `ExportShapes = false` và sử dụng phương thức `ExportExcelChartAsPicture` sau này (xem phần cuối).

---

## Chuyển đổi Excel sang PowerPoint – Tạo hình ảnh từ Worksheet

Khi các tùy chọn đã sẵn sàng, chúng ta chuyển worksheet thành một đối tượng `System.Drawing.Image`. Lớp `WorksheetToImageConverter` thực hiện công việc nặng, áp dụng các thiết lập mà chúng ta vừa định nghĩa.

```csharp
// 3️⃣ Convert the worksheet to an image using the options above
WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
System.Drawing.Image sheetImage = converter.ConvertToImage(0, imageOptions);
```

Tham số `0` chỉ ra trang đầu tiên (chỉ có một trang vì `OnePagePerSheet`). `sheetImage` kết quả giữ nguyên DPI gốc, vì vậy slide của bạn sẽ không bị mờ ngay cả trên màn hình độ phân giải cao.

---

## Lưu bản trình chiếu dưới dạng PPTX – Chèn hình ảnh vào Slide

Bây giờ chúng ta tạo một file PowerPoint mới, thêm một slide và đặt bitmap lên đó. Aspose.Slides coi hình ảnh này như một shape *picture frame*, bạn có thể sau này thay đổi kích thước hoặc di chuyển nó giống như bất kỳ đối tượng PowerPoint gốc nào.

```csharp
// 4️⃣ Create a new PowerPoint presentation
Presentation presentation = new Presentation();
ISlide slide = presentation.Slides[0];   // The default blank slide

// Add the Excel‑derived image as a picture frame
slide.Shapes.AddPictureFrame(
    ShapeType.Rectangle,                 // Simple rectangle container
    0, 0,                                // Top‑left corner (0,0)
    sheetImage.Width,                    // Width of the picture
    sheetImage.Height,                   // Height of the picture
    sheetImage);                         // The bitmap we generated
```

> **Nếu hình ảnh lớn hơn kích thước slide thì sao?**  
> PowerPoint sẽ tự động cắt bỏ bất kỳ phần nào vượt quá kích thước slide. Một cách khắc phục nhanh là thu phóng hình ảnh trước khi chèn:

```csharp
float scale = Math.Min(presentation.SlideSize.Size.Width / (float)sheetImage.Width,
                       presentation.SlideSize.Size.Height / (float)sheetImage.Height);
int newWidth  = (int)(sheetImage.Width * scale);
int newHeight = (int)(sheetImage.Height * scale);
```

Sau đó bạn có thể truyền `newWidth` và `newHeight` vào `AddPictureFrame`.

---

## Xuất Worksheet dưới dạng Hình ảnh – Lưu file PPTX

Cuối cùng chúng ta ghi bản trình chiếu ra đĩa. Cờ `SaveFormat.Pptx` đảm bảo định dạng OpenXML hiện đại, hoạt động trên mọi phiên bản PowerPoint gần đây.

```csharp
// 5️⃣ Save the presentation as a PPTX file
string pptxPath = "YOUR_DIRECTORY/Result.pptx";
presentation.Save(pptxPath, SaveFormat.Pptx);
```

Khi bạn mở `Result.pptx` sẽ thấy một slide duy nhất trông giống hệt sheet Excel, nhưng vẫn có thể click vào bất kỳ textbox nào và chỉnh sửa nội dung trực tiếp trong PowerPoint.

---

## Xuất biểu đồ Excel dưới dạng Hình ảnh – Khi hình raster được ưu tiên

Đôi khi bạn không cần các shape có thể chỉnh sửa; một PNG chất lượng cao của biểu đồ là đủ. Aspose.Cells có thể xuất một biểu đồ cụ thể ra hình ảnh mà không cần chuyển đổi toàn bộ sheet:

```csharp
// Example: Export the first chart on the sheet as a PNG
int chartIndex = 0; // Adjust if you have multiple charts
Chart chart = worksheet.Charts[chartIndex];
ImageOrPrintOptions chartOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    OnePagePerSheet = false
};
chart.ToImage("chart.png", chartOptions);
```

Sau đó bạn có thể nhúng `chart.png` vào slide theo cách chúng ta đã chèn `sheetImage`. Cách này giảm kích thước file PPTX và hữu ích khi dữ liệu xung quanh không cần thiết trên slide.

---

## Những lỗi thường gặp & Cách tránh

| Vấn đề | Nguyên nhân | Giải pháp |
|-------|------------|-----------|
| **Văn bản bị mờ** | Xuất ở DPI thấp (mặc định 96). | Đặt `imageOptions.Dpi = 300;` trước khi chuyển đổi. |
| **Shape biến mất** | `ExportShapes` để `false`. | Đảm bảo `ExportShapes = true` khi bạn cần đồ họa có thể chỉnh sửa. |
| **Kích thước slide không khớp** | Hình ảnh lớn hơn kích thước slide. | Thu phóng hình ảnh (xem đoạn mã) hoặc thay đổi kích thước slide qua `presentation.SlideSize`. |
| **Lỗi giấy phép** | Sử dụng phiên bản dùng thử mà chưa kích hoạt đúng. | Gọi `License license = new License(); license.SetLicense("Aspose.Total.lic");` ngay trong `Main`. |

---

## Ví dụ hoàn chỉnh (Sẵn sàng sao chép‑dán)

Dưới đây là toàn bộ chương trình, sẵn sàng đưa vào một dự án console mới. Thay `YOUR_DIRECTORY` bằng thư mục chứa file Excel của bạn.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;
using System.Drawing;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the Excel workbook
            // -----------------------------------------------------------------
            string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
            Workbook workbook = new Workbook(excelPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -----------------------------------------------------------------
            // 2️⃣ Set up export options – keep shapes editable
            // -----------------------------------------------------------------
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                OnePagePerSheet = true,
                ExportShapes = true,
                ExportEditableTextBoxes = true,
                Dpi = 300                 // High‑resolution output
            };

            // -----------------------------------------------------------------
            // 3️⃣ Convert worksheet to an image
            // -----------------------------------------------------------------
            WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
            Image sheetImage = converter.ConvertToImage(0, imageOptions);

            // -----------------------------------------------------------------
            // 4️⃣ Create PowerPoint and add the image as a slide
            // -----------------------------------------------------------------
            Presentation presentation = new Presentation();
            ISlide slide = presentation.Slides[0];
            slide.Shapes.AddPictureFrame(
                ShapeType.Rectangle,
                0, 0,
                sheetImage.Width,
                sheetImage.Height,
                sheetImage);

            // -----------------------------------------------------------------
            // 5️⃣ Save the PPTX file
            // -----------------------------------------------------------------
            string pptxPath = "YOUR_DIRECTORY/Result.pptx";
            presentation.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine("✅ PowerPoint created successfully at: " + pptxPath);
        }
    }
}
```

**Kết quả mong đợi:**  
Khi chạy chương trình sẽ in ra `✅ PowerPoint created successfully at: YOUR_DIRECTORY/Result.pptx`. Mở file PPTX sẽ thấy một slide duy nhất phản ánh đúng sheet Excel gốc, với các hộp văn bản có thể chỉnh sửa.

---

## Tổng kết & Các bước tiếp theo

Bạn đã biết cách **tạo PowerPoint từ Excel** bằng các API mạnh mẽ của Aspose, cách **xuất worksheet dưới dạng hình ảnh**, và cách **lưu bản trình chiếu dưới dạng PPTX** đồng thời giữ được khả năng chỉnh sửa. Mẫu này cũng áp dụng cho workbook đa sheet — chỉ cần lặp qua `workbook.Worksheets` và thêm một slide mới cho mỗi sheet.

**Bạn có thể khám phá tiếp gì?**  

- **Chuyển đổi hàng loạt:** Duyệt qua một thư mục chứa các file Excel và tạo một bộ slide cho mỗi file.  
- **Bố cục động:** Sử dụng `slide.LayoutSlide` để áp dụng các mẫu PowerPoint đã thiết kế sẵn.  
- **Xuất chỉ biểu đồ:** Kết hợp đoạn mã “Export Excel chart as picture” với các placeholder trên slide để có bộ deck gọn hơn.  
- **Tùy chỉnh nâng cao:** Áp dụng nền slide tùy chỉnh, chuyển động, hoặc animation qua Aspose.Slides.

Hãy thoải mái thử nghiệm — thay đổi DPI, đổi `ShapeType.Ellipse` thành một picture frame dạng vòng tròn, hoặc thậm chí nhúng nhiều hình ảnh vào một slide. Bầu trời là giới hạn khi bạn có quyền kiểm soát lập trình

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}