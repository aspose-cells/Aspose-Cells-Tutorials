---
category: general
date: 2026-02-26
description: Xuất biểu đồ sang PowerPoint từ Excel bằng C#. Tìm hiểu cách chuyển đổi
  Excel sang PowerPoint, lưu Excel dưới dạng PowerPoint và giữ cho các hình dạng có
  thể chỉnh sửa.
draft: false
keywords:
- export chart to powerpoint
- convert excel to powerpoint
- save excel as powerpoint
- how to convert excel to ppt
- save workbook as pptx
language: vi
og_description: Xuất biểu đồ sang PowerPoint từ Excel bằng C#. Hướng dẫn này chỉ cách
  chuyển đổi Excel sang PowerPoint, lưu workbook dưới dạng PPTX và giữ các hình dạng
  có thể chỉnh sửa.
og_title: Xuất biểu đồ sang PowerPoint bằng C# – Hướng dẫn lập trình đầy đủ
tags:
- Aspose.Cells
- C#
- Office Automation
title: Xuất biểu đồ sang PowerPoint bằng C# – Hướng dẫn chi tiết từng bước
url: /vi/net/chart-rendering-and-conversion/export-chart-to-powerpoint-with-c-complete-step-by-step-guid/
---

**convert Excel to PowerPoint**, **save Excel as PowerPoint**, and even tweak the options for edge‑case scenarios."

Translate.

Proceed similarly for all sections.

Make sure to keep code block placeholders unchanged.

Lists: keep bullet points.

Now produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Xuất Biểu Đồ sang PowerPoint – Hướng Dẫn Lập Trình Đầy Đủ

Bạn đã bao giờ tự hỏi làm thế nào để **export chart to PowerPoint** mà không mất khả năng chỉnh sửa? Trong nhiều tình huống báo cáo, bạn cần một biểu đồ sống trong bộ slide, nhưng việc sao chép và dán thủ công thật là phiền phức. Tin tốt là bạn có thể thực hiện điều này một cách lập trình chỉ với vài dòng C#.

Trong hướng dẫn này, chúng ta sẽ đi qua toàn bộ quy trình: từ việc tải một workbook Excel chứa biểu đồ và textbox, cấu hình xuất khẩu để các textbox và shape vẫn có thể chỉnh sửa, và cuối cùng lưu kết quả thành tệp **PowerPoint**. Khi kết thúc, bạn sẽ biết cách **convert Excel to PowerPoint**, **save Excel as PowerPoint**, và thậm chí tinh chỉnh các tùy chọn cho các trường hợp đặc biệt.

## Những gì bạn cần

- **Aspose.Cells for .NET** (phiên bản 23.10 trở lên). Đây là thư viện giúp việc chuyển đổi trở nên dễ dàng.
- **.NET 6+** runtime – bất kỳ SDK mới nào cũng được.
- Một tệp Excel đơn giản (`ChartWithTextbox.xlsx`) chứa ít nhất một biểu đồ và một textbox.
- Visual Studio hoặc IDE yêu thích của bạn.

Không cần thêm bất kỳ gói NuGet nào ngoài Aspose.Cells, nhưng việc nắm vững cú pháp C# sẽ rất hữu ích.

## Export Chart to PowerPoint – Các bước thực hiện

Dưới đây chúng tôi chia giải pháp thành các bước rời rạc, dễ theo dõi. Mỗi bước bao gồm đoạn mã chính xác bạn cần, kèm theo một đoạn “tại sao” ngắn giải thích lý do.

### Bước 1: Tải Workbook Excel chứa biểu đồ

Đầu tiên chúng ta cần đưa tệp nguồn vào bộ nhớ. Sử dụng `Workbook` từ Aspose.Cells sẽ đọc toàn bộ bảng tính, bao gồm biểu đồ, hình ảnh và các đối tượng nhúng.

```csharp
using Aspose.Cells;

// Step 1: Load the Excel workbook that contains the chart with a textbox
Workbook workbook = new Workbook(@"C:\Samples\ChartWithTextbox.xlsx");

// Verify that the workbook actually contains a chart
if (workbook.Worksheets[0].Charts.Count == 0)
{
    throw new InvalidOperationException("No chart found in the first worksheet.");
}
```

*Lý do:* Nếu workbook được mở mà không chỉ định đúng đường dẫn, bạn sẽ gặp `FileNotFoundException`. Kiểm tra nhanh này ngăn bạn xuất ra một slide trống sau này.

### Bước 2: Chuẩn bị Presentation Options để giữ Shape có thể chỉnh sửa

Aspose.Cells cho phép bạn quyết định liệu các textbox, shape và thậm chí biểu đồ có **editable** sau khi xuất hay không. Đặt `ExportTextBoxes` và `ExportShapes` thành `true` sẽ giữ các đối tượng này dưới dạng phần tử PowerPoint gốc thay vì biến chúng thành hình ảnh tĩnh.

```csharp
using Aspose.Cells.Drawing;

// Step 2: Set up presentation options to keep textboxes and shapes editable in the output
PresentationOptions presentationOptions = new PresentationOptions
{
    ExportTextBoxes = true, // Preserve editable textboxes
    ExportShapes    = true  // Preserve shapes such as the chart itself
};
```

*Lý do:* Nếu để các flag này ở giá trị mặc định (`false`), slide kết quả sẽ chỉ chứa một bitmap của biểu đồ, khiến bạn không thể chỉnh sửa series hay thay đổi chú thích sau này. Bật cả hai tùy chọn sẽ cho bạn một biểu đồ PowerPoint thực sự, hoạt động giống như khi bạn tự vẽ.

### Bước 3: Chuyển đổi Excel sang PowerPoint và lưu tệp

Bây giờ chúng ta gọi phương thức `Save`, truyền enum `SaveFormat.Pptx` và các tùy chọn vừa cấu hình. Thư viện sẽ tự động dịch đối tượng biểu đồ Excel thành một shape biểu đồ PowerPoint.

```csharp
// Step 3: Save the workbook as a PowerPoint presentation using the configured options
workbook.Save(@"C:\Samples\Result.pptx", SaveFormat.Pptx, presentationOptions);
```

*Lý do:* Lệnh `Save` thực hiện toàn bộ công việc nặng – ánh xạ series Excel sang series PowerPoint, giữ định dạng trục, và sao chép các textbox liên kết. Sau khi dòng này chạy, bạn sẽ có một tệp `.pptx` hoàn toàn có thể chỉnh sửa, sẵn sàng mở trong Microsoft PowerPoint.

### Xác minh kết quả

Mở `Result.pptx` trong PowerPoint. Bạn sẽ thấy một slide chứa:

- Biểu đồ gốc, vẫn liên kết với dữ liệu (bạn có thể double‑click để chỉnh sửa series).
- Bất kỳ textbox nào có trong sheet Excel, giờ trở thành textbox gốc của PowerPoint.
- Bố cục slide được tự động chọn (thường là một slide trống).

Nếu thấy thiếu bất kỳ thành phần nào, hãy kiểm tra lại workbook nguồn có thực sự chứa các đối tượng hiển thị và `ExportTextBoxes` / `ExportShapes` đã được đặt thành `true`.

### Convert Excel to PowerPoint: Xử lý nhiều Worksheet

Thường một workbook có hơn một sheet, mỗi sheet có biểu đồ riêng. Mặc định Aspose.Cells sẽ xuất **tất cả** biểu đồ từ **tất cả** worksheet thành các slide riêng biệt. Nếu bạn chỉ cần một phần, có thể lọc chúng trước khi lưu:

```csharp
// Example: Export only charts from the first worksheet
Worksheet firstSheet = workbook.Worksheets[0];
foreach (Chart chart in firstSheet.Charts)
{
    chart.IsVisible = true; // Ensure visibility
}

// Hide charts from other sheets
for (int i = 1; i < workbook.Worksheets.Count; i++)
{
    foreach (Chart chart in workbook.Worksheets[i].Charts)
    {
        chart.IsVisible = false;
    }
}
```

*Mẹo:* Đặt `chart.IsVisible = false` rẻ hơn việc xóa hoàn toàn biểu đồ, và cho phép bạn bật/tắt việc đưa vào mà không phải sửa đổi tệp nguồn.

### Save Excel as PowerPoint – Tùy chỉnh kích thước slide

PowerPoint mặc định có kích thước slide 10‑inch x 5.63‑inch. Nếu biểu đồ của bạn bị chật, bạn có thể thay đổi kích thước slide qua đối tượng `PresentationOptions`:

```csharp
presentationOptions.SlideSize = new SizeF(13.33f, 7.5f); // 16:9 widescreen
```

Bây giờ biểu đồ được xuất sẽ có không gian thoáng hơn, và các textbox sẽ giữ nguyên bố cục gốc.

### Cách Convert Excel to PPT: Xử lý các đối tượng ẩn

Các hàng, cột hoặc shape ẩn đôi khi vẫn lọt vào quá trình xuất. Để loại bỏ chúng, chạy một bước dọn dẹp nhanh trước khi lưu:

```csharp
// Remove hidden rows/columns that might affect chart layout
foreach (Worksheet sheet in workbook.Worksheets)
{
    sheet.Cells.HideRows = false;
    sheet.Cells.HideColumns = false;
}
```

Bước này không phải lúc nào cũng cần, nhưng nó ngăn các khoảng trống bất ngờ trong bộ slide cuối cùng.

### Save Workbook as PPTX – Ví dụ đầy đủ

Kết hợp mọi thứ lại, đây là một chương trình console sẵn sàng chạy, minh họa toàn bộ quy trình:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing; // For SizeF

class ExportChartDemo
{
    static void Main()
    {
        // Load workbook (Step 1)
        string sourcePath = @"C:\Samples\ChartWithTextbox.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // Verify chart existence
        if (workbook.Worksheets[0].Charts.Count == 0)
        {
            Console.WriteLine("No chart found. Exiting.");
            return;
        }

        // Configure presentation options (Step 2)
        PresentationOptions options = new PresentationOptions
        {
            ExportTextBoxes = true,
            ExportShapes    = true,
            SlideSize       = new SizeF(13.33f, 7.5f) // optional widescreen
        };

        // Optional: export only first worksheet charts
        for (int i = 1; i < workbook.Worksheets.Count; i++)
        {
            foreach (Chart c in workbook.Worksheets[i].Charts)
                c.IsVisible = false;
        }

        // Save as PowerPoint (Step 3)
        string targetPath = @"C:\Samples\Result.pptx";
        workbook.Save(targetPath, SaveFormat.Pptx, options);

        Console.WriteLine($"Export complete! File saved to {targetPath}");
    }
}
```

Chạy chương trình này sẽ tạo `Result.pptx` với biểu đồ và textbox có thể chỉnh sửa, chính xác như khi bạn **save workbook as pptx** thủ công.

![Export chart to PowerPoint example](/images/export-chart-to-powerpoint.png "Export chart to PowerPoint – editable slide")

## Câu hỏi thường gặp & Trường hợp đặc biệt

**Nếu tệp Excel chứa biểu đồ có nguồn dữ liệu ngoại vi liên kết thì sao?**  
Aspose.Cells sao chép *giá trị dữ liệu hiện tại* vào biểu đồ PowerPoint. Nó **không** giữ liên kết ngoại vi, vì PowerPoint không thể tham chiếu kết nối dữ liệu Excel theo cùng cách. Nếu bạn cần cập nhật trực tiếp, hãy cân nhắc nhúng tệp Excel gốc vào PPTX dưới dạng OLE object.

**Có thể xuất biểu đồ sử dụng theme tùy chỉnh không?**  
Có. Thư viện cố gắng ánh xạ màu theme Excel sang các slot theme của PowerPoint. Đối với palette rất tùy chỉnh, bạn có thể cần điều chỉnh màu sau khi xuất bằng API của PowerPoint (ví dụ: Aspose.Slides).

**Có giới hạn về số lượng biểu đồ không?**  
Thực tế không – Aspose.Cells stream dữ liệu, vì vậy ngay cả workbook có hàng chục biểu đồ cũng có thể xuất, dù kích thước PPTX sẽ tăng tuyến tính.

**Có cần giấy phép cho Aspose.Cells không?**  
Bản đánh giá miễn phí hoạt động, nhưng sẽ thêm watermark vào slide đầu tiên. Đối với môi trường sản xuất, hãy mua giấy phép để loại bỏ watermark và mở khóa hiệu năng đầy đủ.

## Tóm tắt

Chúng ta đã tìm hiểu cách **export chart to PowerPoint** bằng C#, trình bày mã chính xác để tải workbook Excel, cấu hình `PresentationOptions` giữ textbox và shape có thể chỉnh sửa, và cuối cùng lưu kết quả thành `.pptx`. Bạn cũng đã học cách **convert Excel to PowerPoint**, **save Excel as PowerPoint**, và trả lời câu hỏi “**how to convert Excel to ppt**” bằng một ví dụ chạy được đầy đủ.

## Bước tiếp theo?

- **Save workbook as PPTX** với nhiều slide: lặp qua từng worksheet và gọi `Save` với `PresentationOptions` cho mỗi sheet.
- Khám phá **Aspose.Slides** nếu bạn cần chỉnh sửa PPTX đã tạo thêm (thêm transition, speaker notes, v.v.).
- Thử xuất **pivot chart** hoặc **3‑D chart** – các tùy chọn tương tự áp dụng, nhưng có thể cần tinh chỉnh định dạng trục sau khi xuất.

Nếu gặp bất kỳ khó khăn nào, hãy để lại bình luận bên dưới hoặc tham khảo tài liệu chính thức của Aspose.Cells để biết các thay đổi API mới nhất. Chúc bạn lập trình vui vẻ và tận hưởng việc biến các biểu đồ Excel thành slide PowerPoint chuyên nghiệp chỉ với vài dòng C#!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}