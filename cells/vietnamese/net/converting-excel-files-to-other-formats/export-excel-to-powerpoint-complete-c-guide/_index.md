---
category: general
date: 2026-03-22
description: Tìm hiểu cách xuất Excel sang PowerPoint, thiết lập vùng in trong Excel
  và lưu Excel dưới dạng PPTX với biểu đồ có thể chỉnh sửa và các đối tượng OLE chỉ
  trong vài bước.
draft: false
keywords:
- export excel to powerpoint
- set print area excel
- save excel as pptx
- editable charts PowerPoint
- OLE objects export
language: vi
og_description: Xuất Excel sang PowerPoint nhanh chóng. Hướng dẫn này chỉ cách thiết
  lập vùng in trong Excel và lưu Excel dưới dạng PPTX với biểu đồ có thể chỉnh sửa
  và các đối tượng OLE.
og_title: Xuất Excel sang PowerPoint – Hướng dẫn C# đầy đủ
tags:
- Aspose.Cells
- C#
- Office Automation
title: Xuất Excel sang PowerPoint – Hướng dẫn C# đầy đủ
url: /vi/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Xuất Excel sang PowerPoint – Hướng dẫn C# đầy đủ

Cần **xuất Excel sang PowerPoint**? Bạn đã đến đúng nơi. Dù bạn đang tạo một bộ slide bán hàng hàng tuần hay tự động hoá quy trình báo cáo, việc chuyển một worksheet Excel thành một bộ slide PowerPoint có thể tiết kiệm hàng giờ công việc sao chép‑dán.  

Trong tutorial này chúng ta sẽ thực hành một ví dụ thực tế không chỉ **export excel to powerpoint**, mà còn chỉ cho bạn cách **set print area Excel** và **save excel as pptx** để các slide tạo ra giữ nguyên biểu đồ và đối tượng OLE có thể chỉnh sửa được. Khi hoàn thành, bạn sẽ có một chương trình C# sẵn sàng chạy, tạo ra file `.pptx` chuyên nghiệp mà không cần can thiệp thủ công.

## Những gì bạn cần

- **.NET 6+** (bất kỳ runtime .NET nào mới đều được; mã sử dụng cú pháp C# 10)
- **Aspose.Cells for .NET** – thư viện thực hiện việc xuất. Bạn có thể tải từ NuGet (`Install-Package Aspose.Cells`).
- Một workbook Excel chứa ít nhất một biểu đồ và/hoặc một đối tượng OLE (file mẫu `ChartAndOle.xlsx` được dùng trong mã).
- Một IDE yêu thích (Visual Studio, Rider, hoặc VS Code – tùy bạn).

Đó là tất cả. Không cần COM interop, không cần cài đặt Office.  

> **Tại sao phải dùng thư viện?**  
> Office Interop tích hợp sẵn rất dễ gãy, yêu cầu cài Office trên server, và thường tạo ra hình ảnh raster khi bạn thực sự muốn các hình dạng vector có thể chỉnh sửa. Aspose.Cells thực hiện công việc nặng và giữ mọi thứ có thể chỉnh sửa trong PowerPoint.

---

## Bước 1: Tải Workbook Excel  

Đầu tiên chúng ta đưa file nguồn vào bộ nhớ. Lớp `Workbook` trừu tượng hoá toàn bộ file Excel, cho phép truy cập tới worksheets, charts và OLE objects.

```csharp
using Aspose.Cells;

try
{
    // Load the Excel file that contains the chart and OLE object.
    // Adjust the path to point to your own workbook.
    Workbook workbook = new Workbook(@"C:\MyProjects\ChartAndOle.xlsx");
}
catch (Exception ex)
{
    Console.WriteLine($"Failed to load workbook: {ex.Message}");
    return;
}
```

**Tại sao điều này quan trọng:** Việc tải workbook là nền tảng. Nếu đường dẫn sai hoặc file bị hỏng, toàn bộ pipeline sẽ không chạy. Khối `try…catch` cung cấp thông báo lỗi thân thiện thay vì crash.

---

## Bước 2: Đặt Print Area trong Excel  

Trước khi xuất, bạn thường muốn giới hạn đầu ra ở một vùng cụ thể. Đây là lúc **set print area excel** phát huy tác dụng. Bằng cách định nghĩa một print area, bạn nói với Aspose.Cells chính xác những ô (và các đối tượng liên quan) sẽ xuất hiện trên slide.

```csharp
// Assuming we want to export only the range A1:H30 on the first worksheet.
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:H30";
```

> **Mẹo chuyên nghiệp:** Nếu có nhiều worksheet, lặp lại việc gán `PrintArea` cho mỗi worksheet bạn định xuất. Nếu không đặt print area, toàn bộ sheet sẽ được xuất, làm tăng kích thước file PowerPoint.

---

## Bước 3: Cấu hình tùy chọn xuất – Giữ biểu đồ & OLE có thể chỉnh sửa  

Aspose.Cells cung cấp đối tượng `ImageOrPrintOptions` phong phú. Bằng cách bật `ExportChartObjects` và `ExportOleObjects` chúng ta bảo tồn tính vector của biểu đồ và khả năng chỉnh sửa trực tiếp của các đối tượng OLE (như tài liệu Word hoặc PDF nhúng).

```csharp
ImageOrPrintOptions pptExportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,   // We want a PPTX, not a PNG or PDF.
    ExportChartObjects = true,      // Charts stay editable in PowerPoint.
    ExportOleObjects = true         // OLE objects remain live (you can double‑click to edit).
};
```

**Điều gì xảy ra phía sau?**  
Khi `ExportChartObjects` là `true`, Aspose chuyển biểu đồ thành một shape biểu đồ PowerPoint gốc, giữ lại series, trục và định dạng. Khi `ExportOleObjects` được bật, các đối tượng nhúng được chèn dưới dạng khung OLE, vì vậy double‑click trong PowerPoint sẽ mở ứng dụng gốc (Word, Excel, …) để chỉnh sửa.

---

## Bước 4: Lưu Worksheet thành file PowerPoint có thể chỉnh sửa  

Bây giờ chúng ta gộp mọi thứ lại. Phương thức `Save` ghi file `.pptx` sử dụng các tùy chọn đã cấu hình. Kết quả là một bộ slide trong đó mỗi worksheet trở thành một slide (hoặc một loạt slide nếu print area trải qua nhiều trang).

```csharp
// Save the first worksheet as an editable PowerPoint presentation.
workbook.Save(@"C:\MyProjects\EditableChartOle.pptx", pptExportOptions);
Console.WriteLine("Export completed! Check EditableChartOle.pptx.");
```

### Kết quả mong đợi

- **Vị trí file:** `C:\MyProjects\EditableChartOle.pptx`
- **Nội dung:**  
  - Một slide hiển thị vùng `A1:H30` chính xác như trong Excel.  
  - Tất cả biểu đồ là đối tượng biểu đồ PowerPoint — click vào cột và chỉnh sửa dữ liệu.  
  - Các đối tượng OLE (ví dụ: tài liệu Word nhúng) có thể mở và chỉnh sửa trực tiếp từ slide.

Nếu bạn mở PPTX trong PowerPoint, sẽ thấy một slide sạch sẽ với các thành phần hoàn toàn có thể chỉnh sửa — không có ảnh raster.

---

## Các trường hợp đặc biệt & Biến thể  

### Nhiều Worksheet → Nhiều Slide  
Nếu bạn muốn mỗi worksheet trở thành một slide riêng, chỉ cần lặp qua `workbook.Worksheets` và gọi `Save` với `SheetToImageOptions` chỉ định chỉ số sheet cụ thể. Aspose sẽ tự động tạo một slide mới cho mỗi lần lặp.

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    ImageOrPrintOptions opts = new ImageOrPrintOptions
    {
        SaveFormat = SaveFormat.Pptx,
        ExportChartObjects = true,
        ExportOleObjects = true,
        OnePagePerSheet = true   // Ensures each sheet starts on a new slide.
    };
    workbook.Save($"Sheet{i + 1}.pptx", opts);
}
```

### Vùng lớn & Hiệu năng  
Xuất một print area khổng lồ (ví dụ: `A1:Z1000`) có thể tăng mức sử dụng bộ nhớ. Để giảm thiểu, cân nhắc:
- Chia nhỏ vùng thành các đoạn nhỏ hơn và xuất chúng thành các slide riêng.  
- Sử dụng `WorkbookSettings` để tăng `MemorySetting` nếu gặp `OutOfMemoryException`.

### Vấn đề tương thích  
PPTX được tạo hoạt động tốt với PowerPoint 2016 trở lên. Các phiên bản cũ hơn vẫn có thể mở file nhưng có thể mất một số tính năng biểu đồ nâng cao. Luôn kiểm tra trên phiên bản Office mục tiêu nếu bạn phân phối deck rộng rãi.

---

## Ví dụ hoàn chỉnh (Sẵn sàng copy‑paste)

```csharp
// ---------------------------------------------------------------
// Export Excel to PowerPoint – Complete C# Example
// ---------------------------------------------------------------

using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook.
            string excelPath = @"C:\MyProjects\ChartAndOle.xlsx";
            Workbook workbook;
            try
            {
                workbook = new Workbook(excelPath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error loading Excel file: {ex.Message}");
                return;
            }

            // 2️⃣ Set the print area (set print area excel).
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:H30";

            // 3️⃣ Configure export options – keep charts & OLE objects editable.
            ImageOrPrintOptions pptExportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportChartObjects = true,
                ExportOleObjects = true
            };

            // 4️⃣ Save as PPTX (save excel as pptx).
            string pptxPath = @"C:\MyProjects\EditableChartOle.pptx";
            try
            {
                workbook.Save(pptxPath, pptExportOptions);
                Console.WriteLine($"Success! PPTX created at: {pptxPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Failed to save PPTX: {ex.Message}");
            }
        }
    }
}
```

> **Mẹo:** Thay các đường dẫn cứng bằng giá trị cấu hình hoặc đối số dòng lệnh để công cụ linh hoạt hơn.

---

## Câu hỏi thường gặp  

**Hỏi:** Tôi có thể xuất chỉ một biểu đồ mà không cần các ô xung quanh không?  
**Đáp:** Có. Chỉ bật `ExportChartObjects` và đặt print area cho phạm vi bao quanh biểu đồ. Biểu đồ sẽ xuất hiện ở giữa slide.

**Hỏi:** Nếu workbook của tôi chứa macro thì sao?  
**Đáp:** Aspose.Cells bỏ qua macro VBA khi xuất. Nếu bạn cần chức năng macro trong PowerPoint, sẽ phải tái tạo bằng VBA PowerPoint hoặc add‑in.

**Hỏi:** Điều này có hoạt động trên Linux/macOS không?  
**Đáp:** Hoàn toàn có. Aspose.Cells là thư viện .NET thuần; miễn là có runtime .NET, mã chạy đa nền tảng.

---

## Kết luận  

Bạn vừa học cách **export Excel to PowerPoint** đồng thời **set print area excel** và **save excel as pptx** với các biểu đồ và đối tượng OLE có thể chỉnh sửa hoàn toàn. Các bước chính là tải workbook, định nghĩa print area, cấu hình `ImageOrPrintOptions`, và cuối cùng lưu PPTX.  

Từ đây bạn có thể khám phá:
- Xuất nhiều worksheet vào một deck duy nhất.  
- Thêm tiêu đề slide hoặc ghi chú tùy chỉnh bằng code.  
- Chuyển PPTX sang PDF để phân phối (dùng `SaveFormat.Pdf`).  

Hãy chạy thử code, điều chỉnh print area, và xem dữ liệu Excel của bạn hiện ra trong PowerPoint một cách tự động — không cần sao chép‑dán thủ công. Nếu gặp khó khăn, hãy tham khảo tài liệu Aspose.Cells hoặc để lại bình luận bên dưới. Chúc lập trình vui!  

![Diagram showing export excel to powerpoint workflow](/images/export-excel-to-powerpoint.png "export excel to powerpoint workflow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}