---
category: general
date: 2026-06-30
description: Tạo sparkline dạng đường trong Excel bằng C# nhanh chóng. Tìm hiểu cách
  thêm sparkline, tạo workbook Excel bằng C#, và thêm sparkline vào ô trong vài bước.
draft: false
keywords:
- create line sparkline
- how to add sparkline
- add line sparkline
- create excel workbook c#
- add sparkline to cell
language: vi
og_description: Tạo sparkline dạng đường trong Excel bằng C#. Hướng dẫn này chỉ cách
  thêm sparkline, tạo workbook Excel bằng C# và nhúng sparkline vào một ô.
og_title: Tạo sparkline dạng đường trong Excel bằng C# – Hướng dẫn từng bước
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create line sparkline in Excel with C# quickly. Learn how to add sparkline,
    create Excel workbook C#, and add sparkline to cell in a few steps.
  headline: Create line sparkline in Excel with C# – Complete Programming Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Tạo sparkline dạng đường trong Excel bằng C# – Hướng dẫn lập trình toàn diện
url: /vi/net/charts/create-line-sparkline-in-excel-with-c-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo line sparkline trong Excel bằng C# – Hướng dẫn lập trình toàn diện

Bạn đã bao giờ tự hỏi làm thế nào để **tạo line sparkline** trong một tệp Excel bằng C# chưa? Bạn không phải là người duy nhất—các nhà phát triển thường hỏi, “làm sao thêm sparkline vào báo cáo mà không mở Excel thủ công?” Tin tốt là với một vài dòng mã, bạn có thể tạo một line sparkline mượt mà ngay trong workbook, không cần giao diện người dùng.

Trong hướng dẫn này, chúng ta sẽ đi qua mọi thứ bạn cần biết: từ các kiến thức cơ bản **create Excel workbook C#**, qua việc điền dữ liệu, đến các bước chính xác để **add line sparkline** và **add sparkline to cell**. Khi kết thúc, bạn sẽ có một tệp *.xlsx* sẵn sàng sử dụng, hiển thị xu hướng bán hàng hàng tháng trong một cái nhìn. Không có phần thừa, chỉ có giải pháp thực tế, có thể chạy ngay.

---

## Những gì bạn sẽ xây dựng

- Một workbook Excel mới tên *KPI_Sparklines.xlsx*  
- Một worksheet có tên **KPI** chứa các số bán hàng mẫu  
- Một **line sparkline** đặt trong ô **D2** tham chiếu tới dải dữ liệu **B2:B13**  
- Định dạng cơ bản (màu sắc, độ dày đường) để sparkline nổi bật  

Điều kiện tiên quyết? Chỉ cần .NET SDK (3.1+ hoặc .NET 6) và thư viện miễn phí Aspose.Cells for .NET (có sẵn qua NuGet). Nếu bạn chưa từng dùng Aspose.Cells, hãy nghĩ tới nó như một engine Excel mạnh mẽ mà bạn có thể gọi từ mã—không cần COM interop, không cần cài đặt Excel.

---

![Create line sparkline in Excel using C#](https://example.com/images/create-line-sparkline.png "Create line sparkline in Excel with C#")

*Image alt text: create line sparkline in Excel using C# code example*

---

## Bước 1: **Create Excel workbook C#** – Thiết lập tệp và worksheet

Đầu tiên, chúng ta cần một đối tượng workbook và một worksheet nơi dữ liệu sẽ được lưu. Đây là nền tảng cho mọi tự động hoá Excel, dù bạn sau này **add line sparkline** hay viết công thức.

```csharp
using Aspose.Cells;
using System.Drawing;

// Initialize a new workbook
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0) and give it a meaningful name
Worksheet worksheet = workbook.Worksheets[0];
worksheet.Name = "KPI";   // “KPI” will hold our key performance indicators
```

> **Tại sao điều này quan trọng:** Lớp `Workbook` đại diện cho toàn bộ tệp, trong khi `Worksheet` là canvas cho các hàng, cột và cuối cùng là sparkline của chúng ta. Đặt tên sheet sớm giúp tệp gọn gàng và tự mô tả.

---

## Bước 2: Điền dữ liệu – Dải nguồn cho sparkline

Một sparkline cần dữ liệu để vẽ. Hãy mô phỏng 12 tháng doanh số bán hàng. Bạn có thể lấy dữ liệu này từ cơ sở dữ liệu, nhưng để minh bạch chúng ta sẽ tạo chúng ngay trong mã.

```csharp
// Fill column B (index 1) with monthly sales numbers
for (int month = 0; month < 12; month++)
{
    // Example pattern: start at 5,000 and increase by 750 each month
    worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
}
```

> **Mẹo:** `PutValue` tự động phát hiện kiểu dữ liệu, vì vậy bạn không cần ép kiểu sang `double` hay `int`. Nếu cần định dạng ô (tiền tệ, dấu phân cách hàng nghìn), bạn có thể áp dụng đối tượng `Style` sau này.

---

## Bước 3: **Create line sparkline** – Thêm sparkline vào ô cụ thể

Bây giờ là phần chính: **line sparkline**. Aspose.Cells nhóm các sparkline, vì vậy chúng ta đầu tiên tạo một `SparklineGroup` loại `Line`, rồi chỉ định vị trí hiển thị.

```csharp
// Add a new SparklineGroup of type Line
int groupIndex = worksheet.SparklineGroups.Add(SparklineType.Line);
SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIndex];

// Add a sparkline that lives in D2 (row 1, column 3) and reads data from B2:B13
// Parameters: firstRow, firstColumn, lastRow, lastColumn, firstDataRow, lastDataRow
sparklineGroup.Add(1, 3, 1, 3, 1, 12);   // D2 ↔ B2:B13
```

> **Cách hoạt động:**  
> - `firstRow/firstColumn` và `lastRow/lastColumn` xác định *ô mục tiêu* (nơi sparkline xuất hiện).  
> - `firstDataRow/lastDataRow` chỉ tới dải nguồn.  
> Vì chúng ta đang dùng **line sparkline**, hình ảnh sẽ là một đường mỏng đơn giản phản ánh xu hướng của các số.

### Tùy chọn: **How to add sparkline** với kiểu dáng tùy chỉnh

Nếu muốn sparkline nổi bật hơn, hãy điều chỉnh một vài thuộc tính:

```csharp
sparklineGroup.LineWeight = 1.0;               // Thickness of the line
sparklineGroup.SeriesColor = Color.DarkBlue;  // Color of the sparkline line
sparklineGroup.ShowMarkers = true;             // Show data markers (optional)
sparklineGroup.MarkerColor = Color.OrangeRed;  // Marker color
```

> **Tại sao cần style?** Một đường xanh đậm trên nền trắng dễ nhìn, trong khi các marker cung cấp gợi ý nhanh về các điểm dữ liệu cá nhân—rất hữu ích cho các buổi thuyết trình.

---

## Bước 4: Lưu workbook – Xác minh kết quả

Sau khi sparkline đã sẵn sàng, chúng ta chỉ cần ghi tệp ra đĩa. Chọn một thư mục bạn có quyền ghi; ví dụ sử dụng một đường dẫn placeholder mà bạn cần thay thế.

```csharp
// Save the workbook as an .xlsx file
string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
workbook.Save(outputPath);
```

> **Xác minh:** Mở tệp đã tạo trong Excel (hoặc bất kỳ trình xem nào hỗ trợ .xlsx). Bạn sẽ thấy một **line sparkline** trong ô **D2** phản ánh các số bán hàng tăng dần ở cột **B**. Di chuột lên sparkline sẽ hiển thị tooltip với các giá trị nền.

---

## Bước 5: Những lỗi thường gặp khi **add sparkline to cell**

Ngay cả ví dụ đơn giản cũng có thể gây bối rối cho người mới. Dưới đây là một số điều cần chú ý:

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| Wrong cell coordinates | Sparkline target uses zero‑based column index but one‑based row index. | Remember `Cells[row, column]` where `row` is zero‑based, `column` is zero‑based as well. In `SparklineGroup.Add`, rows and columns are **1‑based**. |
| No data displayed | Source range is empty or contains non‑numeric values. | Ensure the range (e.g., `B2:B13`) holds numbers. Use `PutValue` with numeric types. |
| Sparkline disappears after saving | Library version mismatch or missing license. | Use the latest Aspose.Cells package and provide a valid license if you’re beyond the evaluation limits. |
| Formatting not applied | Style changes made before adding the sparkline. | Set styling **after** you create the group, as shown above. |

---

## Toàn bộ mã nguồn – Sao chép‑dán một lần

Dưới đây là chương trình hoàn chỉnh, sẵn sàng chạy. Dán vào một dự án console mới, thêm gói NuGet Aspose.Cells, và nhấn **F5**.

```csharp
using Aspose.Cells;
using System.Drawing;

namespace SparklineDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create Excel workbook C#
            // -------------------------------------------------
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "KPI";

            // -------------------------------------------------
            // Step 2: Populate monthly sales data (B2:B13)
            // -------------------------------------------------
            for (int month = 0; month < 12; month++)
            {
                worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
            }

            // -------------------------------------------------
            // Step 3: Create line sparkline and add it to D2
            // -------------------------------------------------
            int groupIdx = worksheet.SparklineGroups.Add(SparklineType.Line);
            SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIdx];
            sparklineGroup.Add(1, 3, 1, 3, 1, 12); // D2 ↔ B2:B13

            // -------------------------------------------------
            // Step 4: Optional formatting (how to add sparkline with style)
            // -------------------------------------------------
            sparklineGroup.LineWeight = 1.0;
            sparklineGroup.SeriesColor = Color.DarkBlue;
            sparklineGroup.ShowMarkers = true;
            sparklineGroup.MarkerColor = Color.OrangeRed;

            // -------------------------------------------------
            // Step 5: Save the workbook
            // -------------------------------------------------
            string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
            workbook.Save(outputPath);

            System.Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Kết quả mong đợi:** Khi mở *KPI_Sparklines.xlsx*, cột **B** liệt kê mười hai số (5,000 → 13,250) và ô **D2** chứa một line sparkline màu xanh đậm mượt mà, tăng dần. Các marker xuất hiện dưới dạng các chấm màu cam‑đỏ nếu bạn đã bật `ShowMarkers`.

---

## Tiếp theo? Mở rộng kỹ năng Sparkline của bạn

Sau khi đã thành thạo **create line sparkline** với Aspose.Cells, hãy khám phá các chủ đề liên quan sau:

- **Add column sparkline** – lý tưởng để hiển thị dữ liệu chồng.  
- **Create multi‑sparkline groups** trên cùng một sheet để so sánh bên nhau.  
- **Export to PDF** trong khi giữ nguyên sparkline (Aspose.Cells hỗ trợ chuyển PDF).  
- **Dynamic data sources** – lấy dữ liệu bán hàng thực tế từ cơ sở dữ liệu SQL thay vì giá trị cứng.  

Mỗi mục này dựa trên các khái niệm cốt lõi: **create Excel workbook C#**, điền dữ liệu, và **add sparkline to cell** theo kiểu mong muốn.

---

### TL;DR

Chúng tôi đã trình bày cách **create line sparkline** trong một workbook Excel bằng C#. Các bước—*tạo workbook, điền dữ liệu, thêm sparkline, định dạng, và lưu*—đều được gói gọn trong một chương trình tự chứa. Bạn có thể tùy chỉnh màu sắc, độ dày đường, hoặc dải nguồn để phù hợp với nhu cầu báo cáo của mình.

Có cách làm nào khác muốn chia sẻ? Để lại bình luận bên dưới, và chúc bạn lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với hướng dẫn chi tiết từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Excel Automation: Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Excel Automation Create Workbook Add Listbox Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Excel Automation Create Workbook Add Listbox Aspose Cells](/cells/french/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}