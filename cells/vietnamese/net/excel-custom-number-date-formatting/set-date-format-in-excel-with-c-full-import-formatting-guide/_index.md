---
category: general
date: 2026-06-17
description: Đặt định dạng ngày trong Excel bằng C# và đồng thời thiết lập nền ô,
  áp dụng màu chữ, và tô màu cột Excel khi nhập. Học từng bước.
draft: false
keywords:
- set date format
- set cell background
- apply foreground color
- color excel column
- excel import formatting
language: vi
og_description: Đặt định dạng ngày trong Excel bằng C# đồng thời thiết lập nền ô,
  áp dụng màu chữ và tô màu cột Excel khi nhập. Hướng dẫn đầy đủ.
og_title: Đặt định dạng ngày trong Excel bằng C# – Hướng dẫn đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  headline: Set date format in Excel with C# – Full Import Formatting Guide
  type: TechArticle
- description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  name: Set date format in Excel with C# – Full Import Formatting Guide
  steps:
  - name: 2.1 Set Date Format for the First Column
    text: The first column (`OrderDate`) should display as “MM/dd/yyyy”. Aspose uses
      the built‑in number format index 14 for the short date, but you can also supply
      a custom format string if you prefer.
  - name: 2.2 Set Cell Background for the Second Column
    text: Let’s give the `CustomerName` column a light blue background. This is where
      **set cell background** comes into play.
  - name: 2.3 Apply Foreground (Text) Color – Optional Extra
    text: 'If you also want the text itself to be a contrasting color, you can tweak
      the same style:'
  - name: 3.1 Save the Workbook
    text: '```csharp // Save to a file – change path as needed wb.Save("FormattedReport.xlsx",
      SaveFormat.Xlsx); Console.WriteLine("Excel file created with date format and
      colors."); ```'
  - name: What if I have more than two columns?
    text: Just expand the `columnStyles` array and assign a `Style` to each index
      you care about. Unassigned indexes will fall back to the default style, which
      is perfectly fine.
  - name: How do I format a column as currency?
    text: '```csharp columnStyles[3] = wb.CreateStyle(); columnStyles[3].Number =
      164; // Built‑in currency format (e.g., $#,##0.00) ```'
  - name: Can I change the header row style separately?
    text: 'Yes. After the import, you can grab the first row and apply a distinct
      style:'
  - name: What if the DataTable contains null dates?
    text: 'Aspose will leave those cells blank. If you prefer a placeholder like “N/A”,
      you can preprocess the table:'
  type: HowTo
tags:
- excel
- csharp
- aspnet
- data-import
title: Đặt định dạng ngày trong Excel bằng C# – Hướng dẫn đầy đủ về định dạng nhập
url: /vi/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Đặt định dạng ngày trong Excel bằng C# – Hướng dẫn Định dạng Nhập toàn diện

Bạn đã bao giờ cần **đặt định dạng ngày** trong một bảng Excel được tạo từ mã C#, nhưng đồng thời muốn cột có nền hoặc màu chữ tùy chỉnh? Bạn không phải là người duy nhất. Trong nhiều kịch bản báo cáo, bạn lấy một `DataTable` từ cơ sở dữ liệu, chèn nó vào một worksheet, và sau đó phải vội vàng để làm cho ngày tháng hiển thị đúng và các cột nổi bật với màu sắc phù hợp.  

Trong hướng dẫn này, chúng ta sẽ đi qua một giải pháp sạch sẽ, từ đầu đến cuối, bao gồm **đặt định dạng ngày**, **đặt nền ô**, **áp dụng màu chữ**, và thậm chí **tô màu một cột Excel** khi nhập dữ liệu. Khi kết thúc, bạn sẽ có một mẫu có thể tái sử dụng để xử lý **định dạng nhập Excel** mà không cần thử‑và‑sai thường gặp.

> **Bạn sẽ cần**  
> * .NET 6+ (or .NET Framework 4.7+)  
> * Aspose.Cells for .NET (free trial works for testing)  
> * A `DataTable` source – any ADO.NET query will do  
> * Visual Studio or your favorite IDE  

Hãy bắt đầu.

---

## Tổng quan về Giải pháp

Chúng ta sẽ chia vấn đề thành ba phần logic:

1. **Lấy dữ liệu nguồn** – một `DataTable` với các hàng bạn muốn xuất.  
2. **Tạo kiểu cho từng cột** – một kiểu cho cột ngày, một kiểu cho cột văn bản, và bất kỳ kiểu bổ sung nào bạn muốn.  
3. **Nhập bảng với các kiểu** – sử dụng `Worksheet.Cells.ImportDataTable` để mỗi cột kế thừa kiểu bạn đã chuẩn bị.

Tại sao lại chọn cách này? Vì Aspose.Cells cho phép bạn gắn một mảng `Style` trực tiếp vào lời gọi `ImportDataTable`, nghĩa là bạn không cần một lần xử lý thứ hai để áp dụng lại định dạng. Nó nhanh hơn, ít lỗi hơn và giữ cho mã của bạn gọn gàng.

---

## Bước 1: Lấy Dữ liệu để Xuất

Đầu tiên – bạn cần một `DataTable`. Trong một dự án thực tế, bạn có thể gọi stored procedure hoặc dùng Entity Framework để điền dữ liệu, nhưng để minh họa chúng ta sẽ mô phỏng một bảng đơn giản với một cột ngày và một cột văn bản.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("OrderDate", typeof(DateTime));
    table.Columns.Add("CustomerName", typeof(string));

    // Sample rows – replace with your DB call
    table.Rows.Add(DateTime.Today.AddDays(-2), "Acme Corp");
    table.Rows.Add(DateTime.Today.AddDays(-1), "Globex Inc");
    table.Rows.Add(DateTime.Today, "Soylent Co");

    return table;
}
```

> **Mẹo chuyên nghiệp:** Nếu nguồn dữ liệu của bạn sử dụng ngày nullable, hãy chắc chắn rằng kiểu cột là `typeof(DateTime?)` – Aspose vẫn sẽ tôn trọng định dạng bạn gán sau này.

## Bước 2: Chuẩn bị Mảng Các Kiểu – Một cho Mỗi Cột

Bây giờ chúng ta tạo một `Style[]` có độ dài bằng số cột trong `DataTable`. Mỗi phần tử sẽ chứa định dạng cho cột tương ứng.

```csharp
// Create a new workbook and get the first worksheet
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Pull the data
DataTable dataTable = GetData();

// Allocate the style array
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

### 2.1 Đặt Định dạng Ngày cho Cột Đầu Tiên

Cột đầu tiên (`OrderDate`) nên hiển thị dưới dạng “MM/dd/yyyy”. Aspose sử dụng chỉ số định dạng số tích hợp 14 cho ngày ngắn, nhưng bạn cũng có thể cung cấp một chuỗi định dạng tùy chỉnh nếu muốn.

```csharp
// Style for the date column (index 0)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Built‑in short date format
// Or a custom pattern:
// columnStyles[0].Custom = "mm/dd/yyyy";
```

**Tại sao điều này quan trọng:** Excel lưu trữ ngày dưới dạng số serial. Bằng cách gán một định dạng số, bạn nói với Excel hiển thị những số serial đó dưới dạng ngày mà con người có thể đọc được thay vì các số thô.

### 2.2 Đặt Nền Ô cho Cột Thứ Hai

Hãy cho cột `CustomerName` một nền màu xanh nhạt. Đây là nơi **set cell background** phát huy tác dụng.

```csharp
// Style for the text column (index 1)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightBlue;
columnStyles[1].Pattern = BackgroundType.Solid; // Needed to show the color
```

> **Lưu ý:** Nếu không đặt `Pattern` thành `Solid`, màu nền sẽ không hiển thị vì mẫu mặc định là “None”.

### 2.3 Áp dụng Màu Chữ (Foreground) – Thêm Tùy Chọn

Nếu bạn cũng muốn chữ có màu tương phản, bạn có thể chỉnh sửa cùng một kiểu:

```csharp
columnStyles[1].Font.Color = System.Drawing.Color.DarkBlue; // apply foreground color
```

Điều này đáp ứng yêu cầu **apply foreground color** trong khi vẫn giữ nguyên nền của cột.

## Bước 3: Nhập DataTable với Các Kiểu Đã Định Nghĩa

Với các kiểu đã sẵn sàng, bước cuối cùng chỉ là một dòng lệnh để nhập dữ liệu và áp dụng các kiểu theo cột.

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// includeColumnNames = true to add a header row
ws.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**Cách nó hoạt động:** Aspose đọc mảng `columnStyles` và ánh xạ mỗi `Style` tới chỉ số cột tương ứng. Hàng tiêu đề sẽ kế thừa kiểu mặc định trừ khi bạn cung cấp một kiểu riêng cho hàng 0.

### 3.1 Lưu Workbook

```csharp
// Save to a file – change path as needed
wb.Save("FormattedReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Excel file created with date format and colors.");
```

Chạy chương trình, mở *FormattedReport.xlsx*, và bạn sẽ thấy:

- **OrderDate** column displayed as dates (e.g., `06/15/2026`). → **cột OrderDate** hiển thị dưới dạng ngày (ví dụ `06/15/2026`).  
- **CustomerName** column with a light‑blue fill and dark‑blue text. → **cột CustomerName** có nền màu xanh nhạt và chữ màu xanh đậm.  

Đó là toàn bộ quy trình **excel import formatting** trong chưa tới 30 dòng C#.

## Tóm tắt Bước‑bước (với Lý do)

| Bước | Bạn làm gì | Tại sao quan trọng |
|------|------------|--------------------|
| **Lấy dữ liệu** | Gọi `GetData()` để điền dữ liệu vào một `DataTable`. | Cung cấp nguồn dữ liệu có cấu trúc mà Aspose có thể nạp trực tiếp. |
| **Tạo mảng kiểu** | Khởi tạo `Style[]` có độ dài bằng số cột. | Cho phép định dạng từng cột trong một lần gọi import. |
| **Đặt định dạng ngày** | `columnStyles[0].Number = 14;` | Đảm bảo ngày hiển thị đúng trong Excel. |
| **Đặt màu nền** | `ForegroundColor = LightBlue; Pattern = Solid;` | Làm nổi bật cột, đáp ứng yêu cầu **set cell background**. |
| **Áp dụng màu chữ** | `Font.Color = DarkBlue;` | Cải thiện khả năng đọc và đáp ứng yêu cầu **apply foreground color**. |
| **Nhập với các kiểu** | `ImportDataTable(..., columnStyles);` | Nhập một lần duy nhất, tôn trọng mọi định dạng. |
| **Lưu workbook** | `wb.Save(...);` | Lưu kết quả để người dùng tiếp theo sử dụng. |

## Xử lý Các Trường hợp Cạnh và Câu hỏi Thường gặp

### Nếu tôi có nhiều hơn hai cột thì sao?

Chỉ cần mở rộng mảng `columnStyles` và gán một `Style` cho mỗi chỉ số bạn quan tâm. Các chỉ số chưa gán sẽ sử dụng kiểu mặc định, điều này hoàn toàn ổn.

```csharp
columnStyles[2] = wb.CreateStyle();
columnStyles[2].Number = 0; // General format for numeric columns
```

### Làm sao để định dạng một cột dưới dạng tiền tệ?

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 164; // Built‑in currency format (e.g., $#,##0.00)
```

### Tôi có thể thay đổi kiểu hàng tiêu đề riêng biệt không?

Có. Sau khi nhập, bạn có thể lấy hàng đầu tiên và áp dụng một kiểu riêng:

```csharp
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = System.Drawing.Color.Gold;
headerStyle.Pattern = BackgroundType.Solid;

ws.Cells.Rows[0].ApplyStyle(headerStyle, new StyleFlag { All = true });
```

### Nếu DataTable chứa ngày null thì sao?

Aspose sẽ để các ô đó trống. Nếu bạn muốn hiển thị một placeholder như “N/A”, bạn có thể tiền xử lý bảng:

```csharp
foreach (DataRow row in dataTable.Rows)
{
    if (row.IsNull("OrderDate"))
        row["OrderDate"] = DateTime.MinValue; // or any sentinel
}
```

Sau đó điều chỉnh kiểu để hiển thị định dạng tùy chỉnh cho giá trị sentinel “N/A”.

## Ví dụ Hoàn chỉnh

Dưới đây là chương trình đầy đủ, sẵn sàng sao chép‑dán. Chạy nó như một ứng dụng console, và bạn sẽ nhận được một file Excel được định dạng đẹp mắt.



## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Đặt màu chữ trong các ô Excel bằng Aspose.Cells cho .NET](/cells/english/net/formatting/setting-font-color/)
- [Đặt màu chữ trong Excel .NET với Aspose.Cells](/cells/english/net/formatting/set-font-color-net-excel-aspose-cells/)
- [Đặt độ rộng cột Excel tính bằng pixel bằng Aspose.Cells cho .NET | Hướng dẫn Từng bước](/cells/english/net/formatting/set-excel-column-width-pixels-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}