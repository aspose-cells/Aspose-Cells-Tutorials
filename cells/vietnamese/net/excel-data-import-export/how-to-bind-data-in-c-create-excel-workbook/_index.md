---
category: general
date: 2026-03-27
description: Cách liên kết dữ liệu trong C# bằng Aspose.Cells – học cách lưu workbook
  dưới dạng XLSX, thêm biểu đồ và xuất Excel có biểu đồ trong vài phút.
draft: false
keywords:
- how to bind data
- save workbook as xlsx
- create excel workbook c#
- how to add chart
- export excel with chart
language: vi
og_description: Cách liên kết dữ liệu trong C# với Aspose.Cells. Hướng dẫn này cho
  bạn biết cách lưu workbook dưới dạng XLSX, thêm biểu đồ và xuất Excel có biểu đồ.
og_title: Cách liên kết dữ liệu trong C# – Tạo sổ làm việc Excel
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Cách ràng buộc dữ liệu trong C# – Tạo workbook Excel
url: /vi/net/excel-data-import-export/how-to-bind-data-in-c-create-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Bind Dữ liệu trong C# – Tạo Workbook Excel

Bạn đã bao giờ tự hỏi **cách bind dữ liệu** vào một biểu đồ trong C# mà không phải rối bời không? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi cần tạo file Excel một cách lập trình sao cho *trông* giống như những file họ tạo thủ công.  

Trong tutorial này chúng ta sẽ đi qua một ví dụ hoàn chỉnh, sẵn sàng chạy, tạo một workbook Excel, điền dữ liệu vào, bind dữ liệu đó vào biểu đồ Waterfall, và cuối cùng lưu file dưới dạng `.xlsx`. Khi kết thúc, bạn sẽ biết chính xác **cách save workbook as XLSX**, **cách add chart** vào worksheet, và **cách export Excel with chart** cho các báo cáo downstream.

> **Prerequisites** – Bạn cần Aspose.Cells cho .NET (bản dùng thử miễn phí vẫn hoạt động) và môi trường phát triển .NET như Visual Studio 2022. Không cần bất kỳ gói NuGet nào khác.

---

## Những Điều Hướng Dẫn Này Bao Quát

- **Create Excel workbook C#** – thiết lập một `Workbook` mới và một worksheet.  
- **How to bind data** – ánh xạ chuỗi số và nhãn danh mục của bạn tới nguồn dữ liệu của biểu đồ.  
- **How to add chart** – chèn một biểu đồ Waterfall và cấu hình tiêu đề của nó.  
- **Save workbook as XLSX** – lưu file vào đĩa để bất kỳ ai cũng có thể mở trong Excel.  
- **Export Excel with chart** – sản phẩm cuối cùng là một workbook đầy đủ chức năng mà bạn có thể chia sẻ.

Nếu bạn đã quen với cú pháp C# cơ bản, đây sẽ là một việc rất dễ dàng. Hãy bắt đầu.

---

## Bước 1: Tạo một Excel Workbook trong C#  

Đầu tiên – chúng ta cần một đối tượng workbook để làm việc. Hãy nghĩ lớp `Workbook` như một cuốn sổ trống mà bạn sẽ later fill with pages (worksheets) và nội dung.

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;

class WaterfallDemo
{
    static void Main()
    {
        // Initialize a new workbook – this is your blank Excel file.
        Workbook workbook = new Workbook();

        // Grab the first worksheet (index 0). It’s already created for us.
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro tip:** Nếu bạn cần nhiều sheet, chỉ cần gọi `workbook.Worksheets.Add()` và giữ một tham chiếu tới mỗi `Worksheet` mới.

---

## Bước 2: Điền Dữ liệu vào Worksheet với Các Danh Mục và Giá Trị  

Bây giờ chúng ta sẽ **create excel workbook c#**‑style data. Ví dụ sử dụng một kịch bản Waterfall cổ điển: start, revenue, cost, profit, và end.  

```csharp
        // Add header labels.
        worksheet.Cells["A1"].PutValue("Category");
        worksheet.Cells["B1"].PutValue("Amount");

        // Sample data – you can replace these with your own source (database, API, etc.).
        string[] categoryLabels = { "Start", "Revenue", "Cost", "Profit", "End" };
        double[] values = { 0, 150, -70, 0, 80 };

        // Fill rows 2‑6 with the data.
        for (int i = 0; i < categoryLabels.Length; i++)
        {
            worksheet.Cells[i + 1, 0].PutValue(categoryLabels[i]); // Column A
            worksheet.Cells[i + 1, 1].PutValue(values[i]);       // Column B
        }
```

Tại sao chúng ta đặt `0` cho “Start” và “Profit”? Trong biểu đồ Waterfall những số 0 này hoạt động như *connectors* giúp luồng hình ảnh hiển thị đúng. Nếu bỏ qua chúng, biểu đồ sẽ bị gãy.

---

## Bước 3: How to Add Chart – Chèn một Waterfall Chart  

Với dữ liệu đã sẵn sàng, đã đến lúc **how to add chart**. Aspose.Cells làm việc này dễ dàng như gọi `Charts.Add`.

```csharp
        // Insert a Waterfall chart starting at row 7, column 0 and spanning to row 25, column 10.
        int chartIndex = worksheet.Charts.Add(ChartType.Waterfall, 7, 0, 25, 10);
        Chart waterfallChart = worksheet.Charts[chartIndex];

        // Give the chart a meaningful title.
        waterfallChart.Title.Text = "Quarterly Waterfall";
```

Các tọa độ `(7,0,25,10)` xác định ô trên‑trái và ô dưới‑phải của hộp bao quanh biểu đồ. Điều chỉnh chúng để phù hợp với bố cục của bạn.

---

## Bước 4: How to Bind Data – Kết Nối Series và Categories  

Đây là phần cốt lõi của tutorial: **how to bind data** vào biểu đồ. Phương thức `NSeries.Add` nhận dải giá trị Y, trong khi `CategoryData` chỉ tới nhãn trục X.

```csharp
        // Bind the numeric series (values) – the second parameter “true” tells Aspose to treat it as a series.
        waterfallChart.NSeries.Add("B2:B6", true);

        // Bind the category (X‑axis) labels.
        waterfallChart.NSeries.CategoryData = "A2:A6";
```

Lưu ý chúng ta tham chiếu cùng các ô đã điền trước đó (`A2:A6` cho categories, `B2:B6` cho amounts). Nếu bạn thay đổi bố cục dữ liệu, chỉ cần cập nhật các dải này cho phù hợp.

---

## Bước 5: Save Workbook as XLSX – Lưu File  

Cuối cùng, chúng ta **save workbook as XLSX**. Phương thức `Save` tự động chọn định dạng đúng dựa trên phần mở rộng file.

```csharp
        // Save the workbook to disk. Replace YOUR_DIRECTORY with an actual path.
        workbook.Save("YOUR_DIRECTORY/WaterfallChart.xlsx");
    }
}
```

Khi bạn mở `WaterfallChart.xlsx` trong Excel, bạn sẽ thấy một biểu đồ Waterfall được render đẹp mắt, phản ánh đúng dữ liệu chúng ta đã nhập. Đó là phần **export excel with chart** đã hoàn thành.

---

## Kết Quả Mong Đợi  

- **File Excel:** `WaterfallChart.xlsx` nằm trong thư mục bạn chỉ định.  
- **Bố cục Worksheet:** Cột A chứa các danh mục, Cột B chứa các số tiền, và biểu đồ nằm dưới bảng.  
- **Giao diện biểu đồ:** Một Waterfall chart có tiêu đề “Quarterly Waterfall” với năm cột đại diện cho Start, Revenue, Cost, Profit, và End.  

![hình ví dụ biểu đồ waterfall bind dữ liệu](waterfall_chart.png "Biểu đồ Waterfall được tạo bởi Aspose.Cells")

*Văn bản alt chứa từ khóa chính, hỗ trợ cả SEO và trích dẫn AI.*

---

## Câu Hỏi Thường Gặp & Các Trường Hợp Cạnh  

### Nếu nguồn dữ liệu của tôi là động thì sao?  
Thay thế các mảng tĩnh bằng một vòng lặp đọc từ cơ sở dữ liệu hoặc API. Miễn là bạn ghi giá trị vào cùng một dải ô, mã bind vẫn không thay đổi.

### Tôi có thể thay đổi loại biểu đồ không?  
Chắc chắn. Thay `ChartType.Waterfall` bằng `ChartType.Column`, `ChartType.Line`, v.v. Chỉ cần nhớ điều chỉnh dữ liệu series nếu biểu đồ mới yêu cầu cách sắp xếp khác.

### Làm sao để đặt màu cho biểu đồ?  
Dùng `waterfallChart.NSeries[0].Format.Fill.ForeColor = Color.Yellow;` (hoặc bất kỳ `System.Drawing.Color` nào). Điều này hữu ích khi bạn muốn cột “Profit” nổi bật hơn.

### Nếu tôi muốn export sang PDF thay vì XLSX thì sao?  
Gọi `workbook.Save("Report.pdf", SaveFormat.Pdf);`. Biểu đồ sẽ tự động được render trong PDF.

---

## Mẹo cho Mã Sẵn Sàng Sản Xuất  

- **Dispose objects** – Bao `Workbook` trong một khối `using` nếu bạn đang dùng .NET Core để giải phóng tài nguyên kịp thời.  
- **Path handling** – Dùng `Path.Combine(Environment.CurrentDirectory, "WaterfallChart.xlsx")` để tránh hard‑coding dấu phân cách.  
- **Error handling** – Bắt `Exception` quanh `Save` để sớm phát hiện các vấn đề về quyền truy cập hoặc không gian đĩa.  
- **Version check** – Aspose.Cells 23.10+ đã cải thiện hỗ trợ Waterfall; hãy chắc chắn bạn đang dùng phiên bản mới nhất để có kết quả tốt nhất.

---

## Kết Luận  

Bạn giờ đã có một ví dụ toàn diện, đầu‑tới‑cuối, minh họa **how to bind data** trong C#, **create excel workbook c#**, **how to add chart**, **save workbook as xlsx**, và **export excel with chart**. Mã nguồn đã sẵn sàng để đưa vào bất kỳ dự án .NET nào, và các khái niệm này có thể mở rộng cho tập dữ liệu lớn hơn và các loại biểu đồ khác.

Sẵn sàng cho bước tiếp theo? Hãy thử thêm nhiều series, thử nghiệm với biểu đồ stacked, hoặc tự động tạo báo cáo hàng tháng và gửi email tới các bên liên quan. Khi bạn đã nắm vững nền tảng tự động hoá Excel với Aspose.Cells, không gì là không thể.

Chúc lập trình vui vẻ, và mong các bảng tính của bạn luôn render hoàn hảo!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}