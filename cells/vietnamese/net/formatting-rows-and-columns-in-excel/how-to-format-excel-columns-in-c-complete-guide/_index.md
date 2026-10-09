---
category: general
date: 2026-06-27
description: Cách định dạng các cột Excel trong C# với màu luân phiên. Tìm hiểu cách
  tạo workbook Excel bằng C#, nhập DataTable vào Excel và xuất ra file .xlsx.
draft: false
keywords:
- how to format excel columns
- create excel workbook c#
- import datatable to excel
- apply alternating column colors
- export datatable as xlsx
language: vi
og_description: Cách định dạng các cột Excel trong C# với màu luân phiên. Hãy theo
  dõi hướng dẫn từng bước này để tạo workbook Excel bằng C#, nhập DataTable và xuất
  ra định dạng .xlsx.
og_title: Cách Định Dạng Cột Excel trong C# – Hướng Dẫn Toàn Diện
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: How to format Excel columns in C# with alternating colors. Learn to
    create Excel workbook C#, import DataTable to Excel, and export as .xlsx.
  headline: How to Format Excel Columns in C# – Complete Guide
  type: TechArticle
tags:
- C#
- Excel
- DataTable
title: Cách Định Dạng Các Cột Excel trong C# – Hướng Dẫn Toàn Diện
url: /vi/net/formatting-rows-and-columns-in-excel/how-to-format-excel-columns-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Định Dạng Cột Excel trong C# – Hướng Dẫn Đầy Đủ

Bạn đã bao giờ tự hỏi **cách định dạng cột Excel** trong C# mà không phải rối bời? Bạn không phải là người duy nhất. Dù bạn đang xuất báo cáo bán hàng hay đổ dữ liệu cơ sở dữ liệu vào bảng tính, việc làm cho các cột trông gọn gàng có thể tạo ra sự khác biệt giữa “bình thường” và “ấn tượng”.

Trong tutorial này, chúng ta sẽ đi qua một **ví dụ hoàn chỉnh, có thể chạy được** cho thấy cách **tạo workbook Excel bằng C#**, **nhập DataTable vào Excel**, và **áp dụng màu cột xen kẽ** để mỗi cột nổi bật. Khi kết thúc, bạn cũng sẽ biết cách **xuất DataTable thành file xlsx** chỉ với một dòng lệnh. Không có phần thừa, chỉ có mã thực tế bạn có thể sao chép‑dán.

> **Bạn sẽ cần**  
> - .NET 6 hoặc mới hơn (bất kỳ phiên bản gần đây nào cũng được)  
> - Gói NuGet **Aspose.Cells** (hoặc bất kỳ thư viện tương tự nào) – chúng ta sẽ dùng vì nó thuần C# và không cần cài đặt Excel.  
> - Một nguồn `DataTable` đơn giản – chúng ta sẽ tạo một bảng tạm thời để demo.

Hãy bắt đầu.

![How to format Excel columns in C# example](excel-columns.png "How to format Excel columns in C#")

## Bước 1: Tạo Excel Workbook trong C#  

Điều đầu tiên bạn phải làm là khởi tạo một workbook mới. Hãy tưởng tượng nó như mở một cuốn sổ mới để bạn sẽ ghi dữ liệu vào sau.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class ExcelDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook – this is the container for all sheets.
        Workbook workbook = new Workbook();

        // 2️⃣ Grab the first worksheet (index 0) – it’s already there.
        Worksheet worksheet = workbook.Worksheets[0];

        // The rest of the steps will fill this sheet with data and styling.
        // …
    }
}
```

**Tại sao lại quan trọng:** `Workbook` là điểm vào cho mọi thao tác Excel. Tạo nó **creates excel workbook c#** – bạn không cần bất kỳ COM interop nào, và đối tượng tồn tại hoàn toàn trong bộ nhớ cho đến khi bạn quyết định lưu lại.

> **Mẹo chuyên nghiệp:** Nếu bạn đang hướng tới môi trường server, nên chọn thư viện không phụ thuộc vào việc cài đặt Microsoft Office. Aspose.Cells, EPPlus, hoặc ClosedXML đều đáp ứng yêu cầu này.

## Bước 2: Chuẩn Bị Styles – Áp Dụng Màu Cột Xen Kẽ  

Bây giờ là phần thú vị: làm cho mỗi cột lẻ một màu khác nhau. Đánh dấu này giúp người đọc quét các bảng lớn nhanh hơn.

```csharp
// Assume we already have a DataTable called dataTable (we’ll create it later).
int columnCount = dataTable.Columns.Count;

// Create an array to hold a style per column.
Style[] columnStyles = new Style[columnCount];

for (int i = 0; i < columnCount; i++)
{
    // Each column gets its own Style object.
    columnStyles[i] = workbook.CreateStyle();

    // Alternate between blue and green fonts.
    columnStyles[i].Font.Color = (i % 2 == 0) ? Color.Blue : Color.Green;

    // Optional: make the header bold for extra clarity.
    if (i == 0) // just an example, you could set this for all headers.
        columnStyles[i].Font.IsBold = true;
}
```

**Đang xảy ra gì?**  
- `workbook.CreateStyle()` cung cấp một canvas sạch cho mỗi cột.  
- Toán tử ba ngôi `(i % 2 == 0) ? Color.Blue : Color.Green` là trái tim của **apply alternating column colors** – các cột có chỉ số chẵn sẽ thành màu xanh, các cột lẻ sẽ thành màu xanh lá.  
- Bạn có thể mở rộng khối này để đặt nền, viền, hoặc định dạng số mà không cần thay đổi phần còn lại của mã.

> **Trường hợp đặc biệt:** Nếu bảng của bạn có hơn vài chục cột, việc tạo một style cho mỗi cột có thể tiêu tốn bộ nhớ. Trong trường hợp đó, hãy tái sử dụng hai đối tượng style (blueStyle, greenStyle) và gán chúng dựa trên chỉ số cột.

## Bước 3: Xây Dựng DataTable Mẫu (hoặc dùng của bạn)  

Để có một demo tự chứa, chúng ta sẽ tạo một `DataTable` với vài dòng. Trong dự án thực tế, bạn sẽ thay `GetSampleData()` bằng logic truy xuất dữ liệu thực của mình.

```csharp
static DataTable GetSampleData()
{
    DataTable dt = new DataTable();

    // Define columns.
    dt.Columns.Add("ID", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Score", typeof(double));
    dt.Columns.Add("Date", typeof(DateTime));

    // Populate rows.
    for (int i = 1; i <= 5; i++)
    {
        dt.Rows.Add(i, $"Student {i}", 75 + i * 2, DateTime.Today.AddDays(-i));
    }

    return dt;
}
```

Bây giờ chèn đoạn này vào luồng chính:

```csharp
DataTable dataTable = GetSampleData();   // <-- import datatable to excel
```

## Bước 4: Nhập DataTable vào Worksheet với Styles  

Aspose.Cells làm cho việc nhập chỉ cần một dòng lệnh. Phiên bản overload chúng ta dùng cho phép truyền mảng style đã tạo trước.

```csharp
// 0️⃣ Row and column offsets – start at A1 (0,0).
int startRow = 0;
int startColumn = 0;

// The 'true' flag tells the method that the first row in the DataTable
// contains column headers, which will be written to the sheet.
worksheet.Cells.ImportDataTable(dataTable, true, startRow, startColumn, columnStyles);
```

**Tại sao dùng overload này?**  
- Nó tự động xử lý hàng tiêu đề, vì vậy bạn không cần tự viết tên cột.  
- Nó áp dụng mảng **columnStyles** cột‑theo‑cột, cho chúng ta màu xen kẽ mà không cần vòng lặp thêm.  
- Nhanh – toàn bộ bảng được nạp vào bộ nhớ trong một lần gọi.

## Bước 5: Lưu Workbook – Xuất DataTable thành .xlsx  

Cuối cùng, chúng ta ghi workbook ra đĩa. Đây là nơi **export datatable as xlsx** diễn ra.

```csharp
// Choose a folder that exists on your machine.
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");

// Save in the modern Office Open XML format.
workbook.Save(outputPath, SaveFormat.Xlsx);

Console.WriteLine($"Workbook saved to: {outputPath}");
```

Khi mở `output.xlsx` bạn sẽ thấy:

| **ID** | **Name**      | **Score** | **Date**    |
|--------|---------------|-----------|-------------|
| *1* (blue) | *Student 1* (green) | *77* (blue) | *2026‑06‑26* (green) |
| *2* (green) | *Student 2* (blue) | *79* (green) | *2026‑06‑25* (blue) |
| …      | …             | …         | …           |

*Phông chữ xanh và xanh lá xen kẽ theo cột, chính xác như chúng ta đã lập trình.*

## Bước 6: Những Sai Lầm Thường Gặp & Cách Tránh  

| Vấn đề | Nguyên nhân | Giải pháp |
|-------|-------------|-----------|
| **Styles không được áp dụng** | Truyền `null` hoặc mảng có độ dài không khớp vào `ImportDataTable`. | Đảm bảo `columnStyles.Length == dataTable.Columns.Count`. |
| **File bị khóa sau khi lưu** | Một tiến trình khác (ví dụ: Excel) đang mở file. | Đóng mọi trình xem trước khi chạy, hoặc lưu vào đường dẫn tạm và di chuyển file sau. |
| **Bùng nổ bộ nhớ với bảng lớn** | Tạo style cho mỗi cột khi có hàng ngàn cột. | Tái sử dụng hai style và gán dựa trên `(col % 2)`. |
| **Định dạng ngày sai** | Excel hiểu `DateTime` là số. | Đặt `columnStyles[i].Number = 14; // built‑in date format` cho các cột ngày. |

## Bước 7: Các Bước Tiếp Theo – Vượt Qua Định Dạng Đơn Giản  

Khi đã thành thạo **cách định dạng cột Excel** với phông chữ xen kẽ, bạn có thể thử:

- **Conditional formatting** – làm nổi bật các ô thỏa mãn quy tắc kinh doanh.  
- **Table objects** – chuyển phạm vi thành một Excel Table để có bộ lọc tự động.  
- **Chart generation** – trực quan hoá dữ liệu ngay trong workbook.  
- **Streaming large exports** – dùng `SaveOptions` để ghi file lớn mà không tải toàn bộ vào RAM.

Tất cả đều dựa trên các khái niệm cốt lõi chúng ta đã đề cập: tạo workbook, định dạng ô, nhập dữ liệu, và lưu.

---

### Kết Luận  

Bạn vừa học **cách định dạng cột Excel** trong C# từ đầu đến cuối: tạo workbook Excel bằng C#, áp dụng màu cột xen kẽ, nhập DataTable vào Excel, và cuối cùng xuất DataTable thành file .xlsx. Mã đầy đủ, có thể sao chép‑dán ở trên hoạt động ngay, và các giải thích đã trả lời “tại sao” cho mỗi dòng lệnh.

Hãy thoải mái thay đổi màu sắc, thêm viền, hoặc chuyển sang thư viện khác nếu muốn. Mô hình vẫn giữ nguyên, và kết quả luôn là một bảng tính sạch sẽ, chuyên nghiệp, sẵn sàng cho các bên liên quan.

Có câu hỏi hoặc muốn chia sẻ mẹo định dạng của bạn? Để lại bình luận bên dưới và cùng nhau thảo luận. Chúc bạn lập trình vui vẻ!


## Bạn Nên Học Gì Tiếp Theo?


Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã mẫu hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [How to Create and Style Excel Tables Using Aspose.Cells for .NET | Step‑By‑Step Guide](/cells/english/net/tables-structured-references/aspose-cells-net-excel-tables-styling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}