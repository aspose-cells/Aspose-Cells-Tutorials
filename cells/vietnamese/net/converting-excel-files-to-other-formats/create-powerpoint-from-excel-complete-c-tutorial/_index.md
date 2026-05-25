---
category: general
date: 2026-02-21
description: Tạo PowerPoint từ Excel nhanh chóng. Tìm hiểu cách xuất Excel sang PowerPoint
  với văn bản và biểu đồ có thể chỉnh sửa bằng Aspose.Cells chỉ trong vài dòng C#.
draft: false
keywords:
- create powerpoint from excel
- export excel to powerpoint
- export editable text
- export excel chart powerpoint
- convert excel chart powerpoint
language: vi
og_description: Tạo PowerPoint từ Excel với văn bản và biểu đồ có thể chỉnh sửa. Tham
  khảo hướng dẫn chi tiết này để xuất Excel sang PowerPoint bằng Aspose.Cells.
og_title: Tạo PowerPoint từ Excel – Hướng dẫn C# từng bước
tags:
- C#
- Aspose.Cells
- PowerPoint
- Excel Automation
title: Tạo PowerPoint từ Excel – Hướng dẫn C# đầy đủ
url: /vi/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-complete-c-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PowerPoint từ Excel – Hướng dẫn C# đầy đủ

Bạn đã bao giờ cần **tạo PowerPoint từ Excel** nhưng không chắc API nào nên dùng? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi muốn chuyển một bảng tính giàu dữ liệu thành một bộ slide chuyên nghiệp, đặc biệt khi họ cần các hộp văn bản vẫn có thể chỉnh sửa sau khi chuyển đổi.  

Trong hướng dẫn này, chúng tôi sẽ chỉ cho bạn cách **export Excel to PowerPoint** đồng thời giữ nguyên văn bản có thể chỉnh sửa, độ chính xác của biểu đồ và bố cục — chỉ với một vài dòng C#. Khi hoàn thành, bạn sẽ có một tệp PPTX sẵn sàng sử dụng mà bạn có thể tinh chỉnh trong PowerPoint giống như bất kỳ slide nào được tạo thủ công.

## Những gì bạn sẽ học

- Cách tải một workbook Excel chứa biểu đồ và hình dạng.  
- Cách cấu hình `PresentationExportOptions` để các hộp văn bản vẫn có thể chỉnh sửa (`export editable text`).  
- Cách thực sự **export Excel chart PowerPoint** và nhận được một bộ slide sạch sẽ.  
- Một số biến thể nhỏ bạn có thể áp dụng khi cần **convert Excel chart PowerPoint** cho các thiết lập trang khác nhau hoặc nhiều worksheet.  

### Yêu cầu trước

- Môi trường phát triển .NET (Visual Studio 2022 hoặc mới hơn).  
- Aspose.Cells cho .NET (bản dùng thử miễn phí hoặc phiên bản có giấy phép).  
- Một file Excel (`ChartWithShape.xlsx`) chứa ít nhất một biểu đồ và một hình dạng mà bạn muốn giữ ở trạng thái có thể chỉnh sửa.  

Nếu bạn đã có những thứ trên, hãy bắt đầu—không có phần thừa, chỉ có giải pháp thực tế, có thể chạy được.

## Tạo PowerPoint từ Excel – Các bước thực hiện

Dưới mỗi bước chúng tôi sẽ đưa ra một đoạn mã ngắn gọn, giải thích **tại sao** chúng ta làm như vậy và chỉ ra những lỗi thường gặp. Bạn có thể sao chép‑dán toàn bộ ví dụ ở cuối trang.

### Bước 1: Tải Workbook Excel

Đầu tiên chúng ta cần đưa workbook nguồn vào bộ nhớ. Aspose.Cells đọc tệp và xây dựng một mô hình đối tượng phong phú mà chúng ta có thể thao tác.

```csharp
// Step 1: Load the Excel workbook that contains the chart and shape
Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWithShape.xlsx");

// Quick sanity check – make sure the workbook actually loaded
if (workbook.Worksheets.Count == 0)
    throw new InvalidOperationException("The workbook appears to be empty.");
```

**Tại sao điều này quan trọng:**  
Tải workbook là nền tảng. Nếu đường dẫn tệp sai hoặc workbook bị hỏng, tất cả các bước `export excel to powerpoint` tiếp theo sẽ thất bại. Kiểm tra sớm sẽ cho bạn phản hồi ngay thay vì một thông báo “file not found” mơ hồ sau này.

### Bước 2: Chuẩn bị tùy chọn xuất

Aspose.Cells cung cấp cho bạn một đối tượng `PresentationExportOptions` để kiểm soát cách PPTX sẽ hiển thị. Đây là nơi bạn quyết định liệu văn bản có nên ở trạng thái có thể chỉnh sửa hay không.

```csharp
// Step 2: Create export options for PowerPoint conversion
PresentationExportOptions exportOptions = new PresentationExportOptions();

// Optional: tweak the slide size (default is 10in x 7.5in)
exportOptions.SlideSize = new SizeF(10, 7.5f);
```

**Tại sao điều này quan trọng:**  
Nếu không cấu hình `PresentationExportOptions`, thư viện sẽ sử dụng các giá trị mặc định, có thể không phù hợp với mẫu slide doanh nghiệp của bạn. Điều chỉnh kích thước slide từ đầu giúp tránh việc phải thay đổi kích thước thủ công sau này.

### Bước 3: Bật hộp văn bản có thể chỉnh sửa

Cờ đặc biệt `ExportEditableTextBoxes` nói với Aspose.Cells giữ mọi hình dạng văn bản dưới dạng hộp văn bản PowerPoint, không phải hình ảnh tĩnh.

```csharp
// Step 3: Enable editability of text boxes in the resulting presentation
exportOptions.ExportEditableTextBoxes = true;
```

**Tại sao điều này quan trọng:**  
Nếu bạn bỏ qua dòng này, PPTX tạo ra sẽ chứa văn bản được raster hoá — nghĩa là bạn không thể chỉnh sửa nhãn hay chú thích trong PowerPoint. Đặt `export editable text` là chìa khóa để có một bộ slide thực sự tái sử dụng được.

### Bước 4: Xuất Worksheet ra PPTX

Bây giờ chúng ta thực sự ghi tệp PPTX. Bạn có thể chọn bất kỳ worksheet nào; ở đây chúng tôi dùng worksheet đầu tiên (`Worksheets[0]`).

```csharp
// Step 4: Export the first worksheet's page setup to a PPTX file
workbook.Worksheets[0].PageSetup.SaveToPptx("YOUR_DIRECTORY/Result.pptx", exportOptions);
```

**Tại sao điều này quan trọng:**  
`SaveToPptx` tôn trọng thiết lập trang (lề, hướng) mà bạn đã định nghĩa trong Excel, vì vậy slide sẽ phản ánh đúng bố cục bạn đã thiết kế. Đây là cốt lõi của **export excel chart powerpoint**.

### Bước 5: Xác minh đầu ra (Tùy chọn nhưng Được khuyến nghị)

Sau khi chuyển đổi, mở tệp `Result.pptx` đã tạo trong PowerPoint và kiểm tra:

1. Biểu đồ hiển thị sắc nét và giữ nguyên các chuỗi dữ liệu.  
2. Các hộp văn bản có thể chọn và chỉnh sửa.  
3. Kích thước slide phù hợp với mong đợi của bạn.

Nếu có gì không ổn, hãy xem lại `exportOptions` — ví dụ, bạn có thể cần đặt `exportOptions.IncludePrintArea = true` để tôn trọng một vùng in được đặt tên.

```csharp
// Optional: open the PPTX automatically (requires System.Diagnostics)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/Result.pptx",
    UseShellExecute = true
});
```

### Bước 6: Các biến thể nâng cao (Xuất nhiều Sheet)

Thường bạn sẽ muốn **convert excel chart powerpoint** cho nhiều worksheet cùng lúc. Lặp qua bộ sưu tập và đặt tên duy nhất cho mỗi slide:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string outputPath = $"YOUR_DIRECTORY/Result_Sheet{i + 1}.pptx";
    workbook.Worksheets[i].PageSetup.SaveToPptx(outputPath, exportOptions);
}
```

**Mẹo chuyên nghiệp:** Nếu bạn cần tất cả các sheet trong một *PPTX* duy nhất, tạo một đối tượng `Presentation` mới, nhập mỗi slide, rồi lưu một lần. Cách này hơi phức tạp hơn nhưng giúp bạn tránh việc phải quản lý nhiều tệp.

## Ví dụ đầy đủ hoạt động

Dưới đây là toàn bộ chương trình để bạn có thể dán vào một ứng dụng console và chạy ngay lập tức.

```csharp
using System;
using System.Drawing;
using Aspose.Cells;
using Aspose.Cells.Export;

class Program
{
    static void Main()
    {
        // 1️⃣ Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWithShape.xlsx");
        if (workbook.Worksheets.Count == 0)
        {
            Console.WriteLine("Workbook is empty – aborting.");
            return;
        }

        // 2️⃣ Set up export options
        PresentationExportOptions exportOptions = new PresentationExportOptions
        {
            SlideSize = new SizeF(10, 7.5f),          // optional custom size
            ExportEditableTextBoxes = true           // <‑‑ keep text boxes editable
        };

        // 3️⃣ Export first worksheet
        string outputPath = "YOUR_DIRECTORY/Result.pptx";
        workbook.Worksheets[0].PageSetup.SaveToPptx(outputPath, exportOptions);
        Console.WriteLine($"PowerPoint created at: {outputPath}");

        // 4️⃣ Open the result automatically (Windows only)
        try
        {
            System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
            {
                FileName = outputPath,
                UseShellExecute = true
            });
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Could not open PPTX automatically: {ex.Message}");
        }
    }
}
```

**Kết quả mong đợi:**  
Khi mở `Result.pptx`, bạn sẽ thấy một slide phản chiếu bố cục của worksheet Excel. Bất kỳ biểu đồ nào bạn đặt trong Excel sẽ xuất hiện dưới dạng biểu đồ PowerPoint gốc, và chú thích bạn thêm dưới dạng shape sẽ trở thành một hộp văn bản hoàn toàn có thể chỉnh sửa.

## Câu hỏi thường gặp & Trường hợp đặc biệt

- **Liệu điều này có hoạt động với workbook có macro (`.xlsm`)?**  
  Có. Aspose.Cells đọc macro nhưng không thực thi chúng. Quá trình chuyển đổi sẽ bỏ qua VBA, vì vậy bạn vẫn nhận được nội dung hình ảnh.

- **Nếu worksheet của tôi chứa nhiều biểu đồ thì sao?**  
  Tất cả các biểu đồ hiển thị sẽ được chuyển sang cùng một slide. Nếu bạn muốn mỗi biểu đồ trên một slide riêng, hãy tách worksheet hoặc sử dụng vòng lặp được mô tả ở Bước 6.

- **Tôi có thể giữ lại các theme PowerPoint tùy chỉnh không?**  
  Không trực tiếp trong quá trình xuất. Sau khi chuyển đổi, bạn có thể áp dụng theme trong PowerPoint hoặc lập trình bằng Aspose.Slides.

- **Có cách nào để chỉ xuất một phạm vi đã chọn không?**  
  Đặt một vùng in có tên trong Excel (`Page Layout → Print Area`) và bật `exportOptions.IncludePrintArea = true`.

## Kết luận

Bạn giờ đã biết cách **tạo PowerPoint từ Excel** bằng Aspose.Cells, với khả năng kiểm soát toàn diện văn bản có thể chỉnh sửa, độ chính xác của biểu đồ và kích thước slide. Đoạn mã ngắn chúng tôi chia sẻ xử lý kịch bản phổ biến nhất, và các mẹo bổ sung mang lại sự linh hoạt khi bạn cần **export excel to powerpoint** cho nhiều sheet hoặc bố cục tùy chỉnh.  

Sẵn sàng cho thử thách tiếp theo? Hãy thử kết hợp cách này với **Aspose.Slides** để lập trình thêm chuyển động, ghi chú người thuyết trình, hoặc thậm chí nhúng các slide đã tạo vào một bản trình bày lớn hơn. Hoặc thử nghiệm chuyển đổi toàn bộ workbook thành một bộ slide đa slide — hoàn hảo cho các pipeline báo cáo tự động.

Có câu hỏi, hoặc đã khám phá ra một cách tinh chỉnh thông minh? Để lại bình luận bên dưới, và chúc bạn lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}