---
category: general
date: 2026-09-27
description: Đặt vùng in trong Excel và học cách xuất ảnh PNG của các ô đã chọn. Hướng
  dẫn này cũng bao gồm việc lưu phạm vi dưới dạng hình ảnh và chèn ảnh vào bảng tính.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- how to export png
- save range as image
- add picture to worksheet
- export selected cells image
language: vi
lastmod: 2026-09-27
og_description: Đặt vùng in trong Excel và xuất PNG bằng Aspose.Cells. Thực hiện theo
  hướng dẫn từng bước này để lưu phạm vi dưới dạng hình ảnh và chèn hình vào bảng
  tính.
og_image_alt: Screenshot showing set print area excel and exported PNG file
og_title: Đặt vùng in trong Excel – xuất PNG bằng C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Set print area in Excel and learn how to export PNG images of selected
    cells. This guide also covers saving range as image and adding picture to worksheet.
  headline: How to set print area in Excel and export PNG
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Cách thiết lập vùng in trong Excel và xuất ra PNG
url: /vi/net/rendering-and-export/how-to-set-print-area-in-excel-and-export-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách đặt vùng in trong Excel và xuất PNG

Nếu bạn cần **set print area excel** trước khi tạo hình ảnh, hướng dẫn này sẽ chỉ cho bạn cách thực hiện chính xác. Bạn cũng sẽ học cách **how to export png** các tệp từ một phạm vi cụ thể, **save range as image**, và **add picture to worksheet** trong một quy trình lặp lại duy nhất.

Làm việc với Excel một cách lập trình thường có nghĩa là bạn chỉ muốn một phần của các ô—ví dụ một pivot table hoặc một biểu đồ—được chuyển thành hình ảnh. Bằng cách định nghĩa vùng in trước, bạn đảm bảo rằng PNG được xuất ra chứa đúng các ô bạn mong muốn, không thừa không thiếu. Hướng dẫn này sẽ đưa bạn qua từng bước, từ việc tải workbook đến lưu tệp PNG cuối cùng, và giải thích lý do mỗi cài đặt quan trọng.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* .NET 6.0 hoặc phiên bản mới hơn đã được cài đặt  
* Visual Studio 2022 (hoặc bất kỳ IDE C# nào)  
* Gói NuGet **Aspose.Cells for .NET** (`Install-Package Aspose.Cells`)  
* Một tệp Excel (`input.xlsx`) nằm trong một thư mục đã biết  

Các yêu cầu này đảm bảo mã chạy mà không cần cấu hình bổ sung.

## Bước 1: Tải workbook mà bạn muốn làm việc với

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Load the workbook from disk
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

Lớp `Workbook` đại diện cho toàn bộ tệp Excel. Việc tải nó trước sẽ cho bạn quyền truy cập vào các worksheet, ô và các tùy chọn thiết lập trang.

## Bước 2: **Set print area excel** cho phạm vi mục tiêu

```csharp
// Define the range you want to capture
string printArea = "A1:G20";

// Apply the range as the print area on the first worksheet
workbook.Worksheets[0].PageSetup.PrintArea = printArea;
```

Việc thiết lập **print area** cho Excel (và Aspose.Cells) biết ô nào thuộc trang có thể in. Khi bạn xuất sheet dưới dạng hình ảnh, chỉ khu vực này mới được render, điều này rất cần thiết cho một **export selected cells image** sạch sẽ.

## Bước 3: Cấu hình tùy chọn xuất hình ảnh – **how to export png**

```csharp
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG ensures lossless quality
    OnePagePerSheet = true           // Export the defined print area as a single page
};
```

`ImageOrPrintOptions` kiểm soát định dạng đầu ra. Khi chọn `ImageFormat.Png`, bạn sẽ có được một hình ảnh độ phân giải cao, nền trong suốt, hoạt động tốt trong môi trường web và desktop.

## Bước 4: Tạo hình ảnh từ phạm vi đã định nghĩa và **add picture to worksheet**

```csharp
// Create a picture object from the selected range
Picture picture = workbook.Worksheets[0].Pictures.Add(
    0,                                     // top‑left row index where the picture will be placed
    0,                                     // top‑left column index where the picture will be placed
    workbook.Worksheets[0].Cells.CreateRange(printArea));
```

Phương thức `Pictures.Add` chèn một hình ảnh mới vào worksheet. Bằng cách truyền phạm vi đã tạo ở Bước 2, bạn **save range as image** trực tiếp lên sheet, hữu ích nếu sau này bạn cần tham chiếu hình ảnh này ở các phần khác của workbook.

## Bước 5: **Save the picture as an image file** – hoàn thiện quy trình **export selected cells image**

```csharp
// Save the picture to disk as a PNG file
picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);
```

Gọi `Save` sẽ ghi hình ảnh ra hệ thống tệp bằng các tùy chọn đã định nghĩa ở Bước 3. Tệp `selected_range.png` kết quả chứa chính xác các ô được xác định bởi lệnh **set print area excel**.

## Ví dụ đầy đủ, có thể chạy

```csharp
using System;
using Aspose.Cells;
using System.Drawing.Imaging;

class ExportExcelRangeAsPng
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Set print area excel
        string printArea = "A1:G20";
        workbook.Worksheets[0].PageSetup.PrintArea = printArea;

        // 3️⃣ Configure how to export png
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            OnePagePerSheet = true
        };

        // 4️⃣ Add picture to worksheet (save range as image)
        Picture picture = workbook.Worksheets[0].Pictures.Add(
            0,
            0,
            workbook.Worksheets[0].Cells.CreateRange(printArea));

        // 5️⃣ Export selected cells image
        picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);

        Console.WriteLine("PNG exported successfully to YOUR_DIRECTORY\\selected_range.png");
    }
}
```

### Kết quả mong đợi

```
PNG exported successfully to YOUR_DIRECTORY\selected_range.png
```

Và bạn sẽ tìm thấy một tệp `selected_range.png` chỉ hiển thị các ô A1 đến G20 từ `input.xlsx`.

## Những lỗi thường gặp và cách tránh

| Vấn đề | Nguyên nhân | Cách khắc phục |
|-------|-------------|----------------|
| Hình ảnh xuất ra chứa toàn bộ sheet | Không có vùng in nào được định nghĩa | Đảm bảo bạn **set print area excel** trước khi tạo hình ảnh |
| PNG bị mờ | DPI mặc định quá thấp | Đặt `imageOptions.DpiX` và `imageOptions.DpiY` thành giá trị cao hơn (ví dụ: 300) |
| Lỗi không tìm thấy tệp | Đường dẫn thư mục sai | Sử dụng `Path.Combine` hoặc kiểm tra lại thư mục tồn tại |
| Hình ảnh bị lệch | Chỉ số hàng/cột không đúng | Hai tham số đầu tiên của `Pictures.Add` là ô trên‑trái nơi hình ảnh được đặt; giữ chúng ở `0,0` để xuất sạch |

## Mẹo chuyên nghiệp: Xuất nhiều phạm vi trong một lần chạy

Nếu bạn cần **export selected cells image** cho nhiều khu vực, hãy lặp lại các Bước 2‑5 trong một vòng lặp, thay đổi `printArea` ở mỗi lần lặp. Hãy nhớ đặt tên tệp cho mỗi hình ảnh là duy nhất, nếu không lần lưu sau sẽ ghi đè lên tệp trước.

## Kết luận

Bây giờ bạn đã biết cách **set print area excel**, cấu hình **how to export png**, **save range as image**, và **add picture to worksheet** bằng Aspose.Cells. Giải pháp đầu‑cuối này cho phép bạn biến bất kỳ khối ô nào thành PNG chất lượng cao chỉ với vài dòng mã C#.

Tiếp theo, bạn có thể khám phá:

* Thêm viền hoặc watermark vào PNG đã xuất (tìm kiếm *add picture to worksheet* với kiểu dáng)  
* Xuất trực tiếp sang PDF cho báo cáo có thể in (*export selected cells image* → quy trình PDF)  
* Tự động hoá quy trình cho nhiều workbook trong một công việc batch  

Hãy thoải mái thử nghiệm với các phạm vi khác nhau, cài đặt DPI, hoặc định dạng hình ảnh để phù hợp với nhu cầu dự án của bạn. Chúc lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Set Print Area in Excel and Export to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Export Excel Print Area to HTML with Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-print-area-html-aspose-cells-java/)
- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}