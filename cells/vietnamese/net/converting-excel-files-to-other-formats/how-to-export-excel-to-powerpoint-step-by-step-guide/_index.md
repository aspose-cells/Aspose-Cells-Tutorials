---
category: general
date: 2026-02-21
description: Tìm hiểu cách xuất Excel sang PowerPoint với các biểu đồ có thể chỉnh
  sửa. Chuyển đổi Excel sang PowerPoint và tạo PowerPoint từ Excel chỉ với vài dòng
  C#.
draft: false
keywords:
- how to export excel
- convert excel to powerpoint
- create powerpoint from excel
- save excel as powerpoint
- how to export charts
language: vi
og_description: Cách xuất Excel sang PowerPoint với biểu đồ có thể chỉnh sửa. Hãy
  làm theo hướng dẫn này để chuyển đổi Excel sang PowerPoint, tạo PowerPoint từ Excel
  và lưu Excel dưới dạng PowerPoint một cách dễ dàng.
og_title: Cách xuất Excel sang PowerPoint – Hướng dẫn đầy đủ
tags:
- C#
- Aspose.Cells
- PowerPoint
title: Cách xuất Excel sang PowerPoint – Hướng dẫn từng bước
url: /vi/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Xuất Excel sang PowerPoint – Hướng Dẫn Toàn Diện

Bạn đã bao giờ tự hỏi **cách xuất Excel** sang PowerPoint mà không biến các biểu đồ đẹp mắt của mình thành hình ảnh tĩnh chưa? Bạn không phải là người duy nhất. Trong nhiều quy trình báo cáo, nhu cầu **chuyển đổi Excel sang PowerPoint** xuất hiện hàng ngày, và các thủ thuật sao chép‑dán thông thường thường làm hỏng bố cục hoặc khóa dữ liệu biểu đồ.  

Trong hướng dẫn này, chúng tôi sẽ trình bày một giải pháp lập trình sạch sẽ, cho phép **tạo PowerPoint từ Excel** đồng thời giữ cho các biểu đồ vẫn có thể chỉnh sửa được. Khi kết thúc, bạn sẽ có thể **lưu Excel dưới dạng PowerPoint** chỉ bằng một lời gọi phương thức và hiểu rõ lý do mỗi dòng mã quan trọng như thế nào.

## Những Điều Bạn Sẽ Học

- Mã C# chính xác cần thiết để **xuất Excel** ra file PPTX.  
- Cách giữ cho biểu đồ có thể chỉnh sửa bằng `PresentationExportOptions`.  
- Khi nào nên ưu tiên cách này thay vì xuất thủ công hoặc dùng các công cụ chuyển đổi của bên thứ ba.  
- Các yêu cầu trước, những lỗi thường gặp, và một vài mẹo chuyên nghiệp để làm cho quy trình không có lỗi.

> **Mẹo chuyên nghiệp:** Nếu bạn đã sử dụng Aspose.Cells trong dự án, phương pháp này hầu như không gây thêm bất kỳ tải trọng nào.

### Yêu Cầu Trước

| Yêu cầu | Tại sao quan trọng |
|-------------|----------------|
| .NET 6.0 hoặc mới hơn | Runtime hiện đại, hiệu năng tốt hơn, và hỗ trợ đầy đủ cho Aspose.Cells. |
| Aspose.Cells for .NET (gói NuGet) | Cung cấp các API `Workbook`, `PresentationExportOptions`, và `SaveToPptx` mà chúng ta dựa vào. |
| Một file Excel cơ bản có ít nhất một biểu đồ | Việc xuất chỉ hoạt động khi có đối tượng biểu đồ; nếu không, file PPTX sẽ trống. |
| Visual Studio 2022 (hoặc bất kỳ IDE nào bạn thích) | Giúp việc gỡ lỗi và quản lý gói dễ dàng hơn. |

Nếu bạn đã chuẩn bị đầy đủ các mục trên, hãy bắt đầu.

## Cách Xuất Excel sang PowerPoint với Biểu Đồ Có Thể Chỉnh Sửa

Dưới đây là mẫu **đầy đủ, có thể chạy** minh họa toàn bộ quy trình. Mỗi khối mã sẽ được giải thích ngay sau đó, để bạn có thể sao chép‑dán và tùy chỉnh mà không phải mò mẫm tài liệu.

### Bước 1: Cài Đặt Aspose.Cells

Mở terminal trong thư mục dự án và chạy:

```bash
dotnet add package Aspose.Cells
```

Lệnh này sẽ tải phiên bản ổn định mới nhất (hiện tại là 24.9) và thêm các tham chiếu cần thiết vào file `.csproj` của bạn.

### Bước 2: Tải Workbook Excel

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;

// Step 2: Load the Excel workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

> **Tại sao điều này quan trọng:** `Workbook` là điểm vào cho mọi thao tác với Excel. Khi tải file trước, chúng ta đảm bảo rằng việc xuất tiếp theo sẽ dựa trên dữ liệu và định dạng chính xác như bạn thấy trong Excel.

### Bước 3: Cấu Hình Tùy Chọn Xuất PPTX Để Giữ Biểu Đồ Có Thể Chỉnh Sửa

```csharp
// Step 3: Configure PPTX export options to keep charts editable
PresentationExportOptions exportOptions = new PresentationExportOptions
{
    ExportEditableCharts = true   // This flag ensures charts stay editable in PowerPoint
};
```

Nếu bạn bỏ qua `ExportEditableCharts`, Aspose sẽ raster hoá các biểu đồ, biến chúng thành hình ảnh phẳng. Điều này làm mất mục đích của **cách xuất biểu đồ** ở dạng có thể chỉnh sửa.

### Bước 4: Lưu Worksheet Đầu Tiên dưới Dạng File PPTX

```csharp
// Step 4: Export the first worksheet as a PPTX file using the options
workbook.Worksheets[0].PageSetup.SaveToPptx(@"YOUR_DIRECTORY\Editable.pptx", exportOptions);
```

Phương thức `SaveToPptx` ghi một file PowerPoint trong đó mỗi ô Excel trở thành một textbox, và mỗi biểu đồ trở thành một đối tượng biểu đồ PowerPoint gốc. Bạn có thể mở `Editable.pptx` trong PowerPoint và nhấp đúp vào bất kỳ biểu đồ nào để chỉnh sửa chuỗi dữ liệu, trục, hoặc kiểu dáng.

### Bước 5: Kiểm Tra Kết Quả

1. Mở `Editable.pptx` trong Microsoft PowerPoint.  
2. Tìm slide tương ứng với worksheet đã xuất.  
3. Nhấp vào một biểu đồ → chọn **Edit Data** → bạn sẽ thấy lưới dữ liệu dạng Excel.

Nếu biểu đồ vẫn là hình ảnh, hãy kiểm tra lại rằng `ExportEditableCharts` được đặt thành `true` và worksheet nguồn thực sự chứa một đối tượng biểu đồ.

![Sơ đồ mô tả luồng từ Excel sang PowerPoint – cách xuất excel](/images/excel-to-pptx-flow.png "ví dụ cách xuất excel")

## Chuyển Đổi Excel sang PowerPoint – Những Rủi Ro Thường Gặp và Mẹo

Ngay cả khi có mã đúng, các nhà phát triển đôi khi vẫn gặp khó khăn. Dưới đây là những vấn đề phổ biến nhất và cách tránh chúng.

| Vấn đề | Giải thích | Cách khắc phục |
|-------|-------------|-----|
| **Không có biểu đồ nào xuất hiện** | Workbook có thể không có đối tượng biểu đồ, hoặc chúng bị ẩn. | Đảm bảo biểu đồ hiển thị và không nằm trên sheet ẩn. |
| **Biểu đồ trở thành hình ảnh** | `ExportEditableCharts` để mặc định `false`. | Đặt rõ `ExportEditableCharts = true` như trong Bước 3. |
| **Lỗi đường dẫn file** | Sử dụng đường dẫn tương đối mà không có `Path.Combine` thích hợp. | Nên dùng `Path.Combine(Environment.CurrentDirectory, "input.xlsx")`. |
| **File lớn gây OutOfMemory** | Xuất workbook có hàng nghìn dòng và nhiều biểu đồ tiêu tốn nhiều bộ nhớ. | Sử dụng `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;` trước khi tải. |
| **Phiên bản không tương thích** | Dùng phiên bản Aspose.Cells cũ không có `PresentationExportOptions`. | Nâng cấp lên gói NuGet mới nhất. |

### Bonus: Xuất Nhiều Worksheet

Nếu bạn cần **tạo PowerPoint từ Excel** cho hơn một sheet, hãy lặp qua collection:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string pptxPath = $@"YOUR_DIRECTORY\Sheet{i + 1}.pptx";
    workbook.Worksheets[i].PageSetup.SaveToPptx(pptxPath, exportOptions);
}
```

Mỗi worksheet sẽ tạo ra một file PPTX riêng, vẫn giữ được khả năng chỉnh sửa biểu đồ.

## Lưu Excel dưới Dạng PowerPoint – Các Tình Huống Nâng Cao

### Nhúng Hình Ảnh Cùng Biểu Đồ

Đôi khi báo cáo kết hợp biểu đồ và logo công ty. Aspose xử lý hình ảnh giống như bất kỳ shape nào khác, vì vậy chúng sẽ tự động xuất hiện trong PPTX. Nếu muốn kiểm soát thứ tự, hãy điều chỉnh Z‑index qua thuộc tính `Shape` trước khi xuất.

### Bố Cục Slide Tùy Chỉnh

PowerPoint hỗ trợ master slides. Trong khi `SaveToPptx` tạo một bố cục mặc định, bạn có thể áp dụng template master sau này:

```csharp
using Aspose.Slides;

// Load the generated PPTX
Presentation pres = new Presentation(@"YOUR_DIRECTORY\Editable.pptx");

// Apply a master template (must be a .pptx file)
pres.Masters.AddFromFile(@"TEMPLATES\CorporateTemplate.pptx");

// Save the final version
pres.Save(@"YOUR_DIRECTORY\FinalPresentation.pptx", SaveFormat.Pptx);
```

Bước này cho phép bạn **chuyển đổi Excel sang PowerPoint** đồng thời giữ nguyên thương hiệu công ty.

### Xử Lý Các Loại Biểu Đồ Khác Nhau

Hầu hết các loại biểu đồ phổ biến (Bar, Column, Line, Pie) xuất ra hoàn hảo. Tuy nhiên, **cách xuất biểu đồ** như Radar hoặc Stock có thể cần thêm việc định dạng sau khi nhập. Trong những trường hợp đó, bạn có thể:

1. Xuất như mô tả.  
2. Mở file PPTX bằng Aspose.Slides.  
3. Điều chỉnh thuộc tính biểu đồ (ví dụ, `Chart.Type = ChartType.Radar`).

## Tổng Kết & Các Bước Tiếp Theo

Chúng ta đã bao quát mọi thứ cần biết về **cách xuất Excel** sang bộ PowerPoint đồng thời giữ cho biểu đồ có thể chỉnh sửa. Các bước cốt lõi—cài đặt Aspose.Cells, tải workbook, cấu hình `PresentationExportOptions`, và gọi `SaveToPptx`—chỉ mất vài dòng C# nhưng thay thế hoàn toàn quy trình thủ công.

### Những Gì Bạn Nên Thử Tiếp Theo

- **Chuyển đổi Excel sang PowerPoint** cho toàn bộ workbook bằng ví dụ vòng lặp.  
- Thử **tạo PowerPoint từ Excel** cho các dashboard động cập nhật hàng đêm.  
- Kết hợp xuất này với **Aspose.Slides** để áp dụng master slide tùy chỉnh và tự động hoá branding.  
- Khám phá phương thức `ExportAllSheetsAsPptx` nếu bạn muốn một file PPTX duy nhất chứa nhiều worksheet.

Hãy tự do thay đổi đường dẫn, điều chỉnh tùy chọn xuất, hoặc nhúng logic này vào một dịch vụ báo cáo lớn hơn. Giới hạn duy nhất là sự sáng tạo của bạn với các biểu đồ dữ liệu.

---

*Chúc lập trình vui vẻ! Nếu gặp bất kỳ khó khăn nào khi **lưu Excel dưới dạng PowerPoint**, hãy để lại bình luận bên dưới hoặc kiểm tra tài liệu Aspose.Cells để cập nhật mới nhất.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}