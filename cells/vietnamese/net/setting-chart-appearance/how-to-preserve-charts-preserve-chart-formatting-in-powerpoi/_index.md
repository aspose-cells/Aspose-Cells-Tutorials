---
category: general
date: 2026-07-03
description: Cách bảo tồn biểu đồ đồng thời giữ định dạng biểu đồ khi sử dụng Aspose.Slides
  trong C#. Hãy làm theo hướng dẫn từng bước này.
draft: false
keywords:
- how to preserve charts
- preserve chart formatting
language: vi
og_description: Cách bảo tồn biểu đồ và định dạng biểu đồ với Aspose.Slides trong
  C#. Hướng dẫn chi tiết kèm mã nguồn.
og_title: cách bảo tồn biểu đồ – bảo lưu định dạng biểu đồ trong PowerPoint (C#)
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: how to preserve charts while keeping preserve chart formatting using
    Aspose.Slides in C#. Follow this step‑by‑step guide.
  headline: how to preserve charts – preserve chart formatting in PowerPoint C#
  type: TechArticle
- description: how to preserve charts while keeping preserve chart formatting using
    Aspose.Slides in C#. Follow this step‑by‑step guide.
  name: how to preserve charts – preserve chart formatting in PowerPoint C#
  steps:
  - name: Open `EditableCharts.pptx` in PowerPoint.
    text: Open `EditableCharts.pptx` in PowerPoint.
  - name: Click any chart → “Edit Data”.
    text: Click any chart → “Edit Data”.
  - name: The Excel‑like data sheet should appear, letting you modify series values.
    text: The Excel‑like data sheet should appear, letting you modify series values.
  type: HowTo
- questions:
  - answer: Directly no—`ExportEditableObjects` only applies to the PPTX format. Convert
      first, then export.
    question: Does this work with PowerPoint 2003 (PPT) files?
  - answer: Absolutely. The same `ExportEditableObjects` flag keeps SmartArt, tables,
      and diagrams editable.
    question: Can I preserve other objects like SmartArt?
  - answer: 'The slide size is stored in the presentation metadata and isn’t affected
      by these options. No extra code needed. --- ## Next steps – keep the momentum
      Now that you’ve nailed **how to preserve charts**, try exploring: - **preserve
      chart formatting** for specific chart types (e.g., stacked bar vs. rad'
    question: What if I need to keep the original slide size?
  type: FAQPage
tags:
- Aspose.Slides
- C#
- PowerPoint
- chart automation
title: Cách bảo tồn biểu đồ – bảo lưu định dạng biểu đồ trong PowerPoint C#
url: /vi/net/setting-chart-appearance/how-to-preserve-charts-preserve-chart-formatting-in-powerpoi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách bảo tồn biểu đồ – bảo tồn định dạng biểu đồ trong PowerPoint C#

Bạn đã bao giờ tự hỏi **cách bảo tồn biểu đồ** khi cần xuất hoặc thao tác với tệp PowerPoint một cách lập trình chưa? Có thể bạn đã thử lưu nhanh và biểu đồ biến thành hình ảnh tĩnh, làm mất khả năng chỉnh sửa mà bạn mong muốn.  

Trong hướng dẫn này, chúng tôi sẽ chỉ cho bạn **cách bảo tồn biểu đồ** **và** giữ **bảo tồn định dạng biểu đồ** nguyên vẹn bằng Aspose.Slides for .NET. Khi kết thúc, bạn sẽ có một đoạn mã C# sẵn sàng chạy, tạo ra file PPTX trong đó mọi biểu đồ vẫn là đối tượng OOXML có thể chỉnh sửa—không còn hình ảnh đã được làm phẳng nữa.

## Những gì bạn sẽ học

- Các bước chính để tải một bản trình chiếu, cấu hình tùy chọn xuất, và lưu trong khi **bảo tồn định dạng biểu đồ**.  
- Tại sao cờ `ExportEditableObjects` quan trọng và nó ngăn biểu đồ bị raster hoá như thế nào.  
- Những lỗi thường gặp (ví dụ: định dạng PPT cũ, thiếu phông chữ) và cách khắc phục nhanh.  

Không yêu cầu kinh nghiệm trước với Aspose; chỉ cần một môi trường C# cơ bản và một tệp PowerPoint mà bạn muốn giữ biểu đồ có thể chỉnh sửa.

## Yêu cầu trước

- .NET 6.0 hoặc mới hơn (mã cũng hoạt động với .NET Framework 4.7+).  
- Gói NuGet Aspose.Slides for .NET (`Install-Package Aspose.Slides.NET`).  
- Một mẫu `input.pptx` chứa ít nhất một biểu đồ.  
- Visual Studio, Rider, hoặc bất kỳ trình soạn thảo nào bạn thích.

---

## Bước 1: Cài đặt Aspose.Slides và tạo dự án console mới

Để bắt đầu, tạo một ứng dụng console mới và thêm thư viện:

```bash
dotnet new console -n PreserveChartsDemo
cd PreserveChartsDemo
dotnet add package Aspose.Slides.NET
```

> **Mẹo chuyên nghiệp:** Nếu bạn đang làm việc sau proxy công ty, thêm cờ `--no-restore` và thực hiện restore sau với cài đặt proxy của bạn.

## Bước 2: Tải bản trình chiếu nguồn – nơi đầu tiên áp dụng **cách bảo tồn biểu đồ**

Mở tệp PPTX bằng lớp `Presentation`. Đây là nơi hành trình **cách bảo tồn biểu đồ** thực sự bắt đầu.

```csharp
using Aspose.Slides;
using Aspose.Slides.Export;

namespace PreserveChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Load the source presentation
            // Replace the path with the location of your PPTX that contains charts.
            Presentation pres = new Presentation(@"YOUR_DIRECTORY\input.pptx");
```

Lưu ý chúng ta chưa chạm vào bất kỳ đối tượng biểu đồ nào—đó là ý định. Việc tải file nguyên trạng giúp chúng ta giữ cấu trúc XML gốc, điều này rất quan trọng cho **bảo tồn định dạng biểu đồ** sau này.

## Bước 3: Cấu hình tùy chọn xuất – trung tâm của **cách bảo tồn biểu đồ**

Aspose.Slides cung cấp lớp `PresentationExportOptions`. Đặt `ExportEditableObjects` thành `true` sẽ yêu cầu engine giữ biểu đồ, bảng và SmartArt dưới dạng các phần OOXML gốc thay vì làm phẳng chúng.

```csharp
            // Step 3: Configure export options to keep objects editable
            PresentationExportOptions exportOptions = new PresentationExportOptions
            {
                // This flag is the key to how to preserve charts.
                ExportEditableObjects = true
            };
```

Tại sao lại hoạt động? Khi `ExportEditableObjects` là `false` (mặc định), thư viện raster hoá các đối tượng phức tạp để tương thích, điều này phá hủy **bảo tồn định dạng biểu đồ**. Bật tùy chọn này sẽ giữ lại XML biểu đồ gốc, cho phép người dùng cuối mở PPTX và vẫn có thể chỉnh sửa dữ liệu biểu đồ.

## Bước 4: Lưu bản trình chiếu bằng các tùy chọn đã cấu hình

Bây giờ chúng ta ghi file đầu ra. Phương thức `Save` có overload nhận `SaveFormat` và `exportOptions` sẽ đảm bảo biểu đồ vẫn có thể chỉnh sửa.

```csharp
            // Step 4: Save the presentation with the configured options
            pres.Save(@"YOUR_DIRECTORY\EditableCharts.pptx", SaveFormat.Pptx, exportOptions);

            // Optional: Inform the user
            Console.WriteLine("Presentation saved with editable charts at: YOUR_DIRECTORY\\EditableCharts.pptx");
        }
    }
}
```

Chạy chương trình này sẽ tạo ra `EditableCharts.pptx`. Mở nó trong PowerPoint, chuột phải vào một biểu đồ và bạn sẽ thấy tùy chọn “Edit Data” bình thường—chứng minh rằng chúng ta đã thành công trong việc **cách bảo tồn biểu đồ** và **bảo tồn định dạng biểu đồ**.

## Bước 5: Xác minh kết quả và khắc phục các vấn đề thường gặp

### Xác minh

1. Mở `EditableCharts.pptx` trong PowerPoint.  
2. Nhấp vào bất kỳ biểu đồ nào → “Edit Data”.  
3. Bảng dữ liệu kiểu Excel sẽ xuất hiện, cho phép bạn sửa các giá trị series.

Nếu bạn chỉ thấy một hình ảnh tĩnh, hãy kiểm tra lại:

- Bạn đang dùng phiên bản mới nhất của Aspose.Slides (các bản cũ có lỗi với `ExportEditableObjects`).  
- Tệp PPTX nguồn thực sự chứa các đối tượng biểu đồ (không phải ảnh chụp của biểu đồ).  
- Không có theme tùy chỉnh hoặc thay thế phông chữ nào khiến biểu đồ được render thành hình ảnh.

### Trường hợp đặc biệt

- **Tệp PPT (binary) cũ:** Chuyển chúng sang PPTX trước (`pres.Save("temp.pptx", SaveFormat.Pptx)`) rồi mới áp dụng tùy chọn xuất.  
- **Bản trình chiếu lớn:** Tiêu thụ bộ nhớ có thể tăng đột biến; cân nhắc sử dụng mẫu `Dispose` của `Presentation` hoặc API streaming cho các file khổng lồ.  
- **Phông chữ nhúng:** Nếu môi trường đích thiếu phông chữ gốc, PowerPoint có thể fallback và render biểu đồ thành hình ảnh. Nhúng phông chữ trong tệp nguồn hoặc cung cấp chúng cùng ứng dụng của bạn.

---

## Câu hỏi thường gặp (FAQ)

**H: Điều này có hoạt động với tệp PowerPoint 2003 (PPT) không?**  
Đ: Không trực tiếp—`ExportEditableObjects` chỉ áp dụng cho định dạng PPTX. Cần chuyển đổi trước, rồi mới xuất.

**H: Tôi có thể bảo tồn các đối tượng khác như SmartArt không?**  
Đ: Chắc chắn. Cờ `ExportEditableObjects` giống nhau giữ SmartArt, bảng và sơ đồ có thể chỉnh sửa.

**H: Nếu tôi muốn giữ nguyên kích thước slide gốc thì sao?**  
Đ: Kích thước slide được lưu trong metadata của bản trình chiếu và không bị ảnh hưởng bởi các tùy chọn này. Không cần mã bổ sung.

---

## Các bước tiếp theo – duy trì đà tiến

Giờ bạn đã nắm vững **cách bảo tồn biểu đồ**, hãy thử khám phá:

- **bảo tồn định dạng biểu đồ** cho các loại biểu đồ cụ thể (ví dụ: stacked bar vs. radar).  
- Sử dụng API `Chart` để thay đổi dữ liệu một cách lập trình trước khi lưu.  
- Xuất sang các định dạng khác (PDF, HTML) trong khi vẫn giữ biểu đồ có thể chỉnh sửa trong PPTX nguồn.  

Mỗi mục trên đều dựa trên nguyên tắc chung: giữ nguyên OOXML bên trong.

---

## Kết luận

Chúng ta đã đi qua **cách bảo tồn biểu đồ** trong tệp PowerPoint bằng Aspose.Slides for .NET, và đã trình bày chi tiết các bước **bảo tồn định dạng biểu đồ** cần thiết để giữ các biểu đồ luôn có thể chỉnh sửa. Đoạn mã hoàn chỉnh ở trên đã sẵn sàng để chèn vào bất kỳ dự án C# nào, và phần giải thích cung cấp lý do *tại sao* cho mỗi dòng—để bạn không chỉ copy‑paste mà còn hiểu rõ.

Hãy thử chạy, tinh chỉnh các tùy chọn xuất, và sớm bạn sẽ tự động cập nhật bản trình chiếu mà không bao giờ mất khả năng tinh chỉnh dữ liệu biểu đồ. Chúc lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây liên quan chặt chẽ và mở rộng các kỹ thuật đã trình bày trong bài này. Mỗi tài nguyên đều bao gồm mã mẫu đầy đủ và giải thích từng bước để giúp bạn làm chủ các tính năng API khác và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [How to Convert Excel Charts to SVG Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [How to Create Charts in Excel Using Aspose.Cells for .NET&#58; A Developer's Guide](/cells/english/net/charts-graphs/create-charts-excel-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}