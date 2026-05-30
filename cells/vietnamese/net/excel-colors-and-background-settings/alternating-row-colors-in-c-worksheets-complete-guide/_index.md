---
category: general
date: 2026-05-30
description: Học cách thêm màu nền xen kẽ cho các hàng trong bảng tính C#, đặt nền
  ô bằng mẫu tô đầy đặc, và tùy chỉnh kiểu ô bảng tính một cách dễ dàng.
draft: false
keywords:
- alternating row colors
- set cell background
- solid fill pattern
- add background color
- worksheet cell style
language: vi
og_description: Tô màu xen kẽ các hàng trong bảng tính C# trở nên dễ dàng. Học cách
  đặt nền ô, sử dụng mẫu tô đầy đặc, và làm chủ kiểu ô trong bảng tính.
og_title: Màu nền xen kẽ cho các hàng trong bảng tính C# – Hướng dẫn toàn diện
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  headline: Alternating Row Colors in C# Worksheets – Complete Guide
  type: TechArticle
- description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  name: Alternating Row Colors in C# Worksheets – Complete Guide
  steps:
  - name: Why Use a **Solid Fill Pattern**?
    text: The `Pattern` property tells the engine how to render the color. A `Solid`
      fill guarantees that the entire cell background is painted, eliminating any
      faint gridlines that might otherwise show through. This is the most common way
      to **set cell background** when you want a clean look.
  - name: Change the Colors
    text: 'If your brand uses different hues, just replace `Color.LightYellow` and
      `Color.LightCyan` with any `System.Drawing.Color` you prefer. For example:'
  - name: Use a Different **Background Type**
    text: While `BackgroundType.Solid` is the most common, you can experiment with
      `BackgroundType.Gray125`, `BackgroundType.Horizontal`, or any pattern that the
      library supports. This changes the visual texture while still **adding background
      color**.
  - name: Apply a **Worksheet Cell Style** to Specific Columns
    text: 'Sometimes you only want the alternating effect on data columns, leaving
      the first column (e.g., IDs) untouched. Create a separate style for that column
      and assign it after the import:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: Màu nền xen kẽ cho các hàng trong bảng tính C# – Hướng dẫn toàn diện
url: /vi/net/excel-colors-and-background-settings/alternating-row-colors-in-c-worksheets-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Màu Hàng Xen Kẽ trong Bảng Tính C# – Hướng Dẫn Toàn Diện

Bạn đã bao giờ tự hỏi làm thế nào để làm cho file Excel xuất ra trông chuyên nghiệp hơn bằng cách sử dụng **màu hàng xen kẽ** chưa? Bạn không phải là người duy nhất—các nhà phát triển luôn hỏi cách *thêm màu nền* cho các hàng mà không phải viết hàng triệu dòng mã.  

Trong tutorial này, chúng ta sẽ đi qua một cách đơn giản để **đặt nền cho ô** trên mỗi hàng, áp dụng **mẫu tô đầy đặc** và kiểm soát **kiểu ô bảng tính** sao cho kết quả vừa dễ đọc vừa bắt mắt.

## Những Điều Bạn Sẽ Học

- Lấy dữ liệu vào một `DataTable` (hoặc bất kỳ nguồn dữ liệu dạng bảng nào).  
- Xây dựng một mảng các đối tượng `Style` xen kẽ giữa hai màu.  
- Nhập `DataTable` vào bảng tính đồng thời áp dụng các kiểu này.  
- Kiểm tra kết quả và điều chỉnh màu hoặc mẫu nếu cần.  

Không cần công cụ bên ngoài nào ngoài môi trường .NET và một thư viện bảng tính (chúng ta sẽ dùng **Aspose.Cells** trong các ví dụ). Khi hoàn thành, bạn sẽ có một phương thức tái sử dụng được, có thể đưa vào bất kỳ quy trình báo cáo nào.

---

## Bước 1: Lấy Dữ Liệu Nguồn dưới dạng `DataTable`

Đầu tiên—không có dữ liệu thì không có gì để định dạng. Dưới đây là một helper nhỏ tạo một `DataTable` với vài dòng mẫu. Trong dự án thực tế, bạn sẽ thay thế phần này bằng lời gọi cơ sở dữ liệu hoặc bộ phân tích CSV.

```csharp
using System;
using System.Data;

static DataTable GetData()
{
    // Create a simple table with three columns
    DataTable table = new DataTable("Report");
    table.Columns.Add("ID", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with dummy rows
    for (int i = 1; i <= 10; i++)
    {
        table.Rows.Add(i, $"Item {i}", Math.Round(new Random().NextDouble() * 100, 2));
    }

    return table;
}
```

> **Tại sao điều này quan trọng:** Khi dữ liệu ở dạng `DataTable`, công cụ bảng tính có thể *nhập* nó trong một lần gọi, tự động giữ lại tên cột và kiểu dữ liệu.

## Bước 2: Tạo Các Kiểu **Màu Hàng Xen Kẽ**

Bây giờ chúng ta sẽ tạo một mảng các đối tượng `Style`—một cho mỗi hàng—để các hàng chẵn có màu vàng nhạt, còn các hàng lẻ có màu xanh cyan nhẹ. Đây là phần cốt lõi của kỹ thuật **màu hàng xen kẽ**.

```csharp
using Aspose.Cells;
using System.Drawing;

// Assume workbook and worksheet are already instantiated
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Retrieve data
DataTable dataTable = GetData();

// Prepare an array of styles – one for each row in the table
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style for the current row
    rowStyles[i] = workbook.CreateStyle();

    // **Add background color**: LightYellow for even rows, LightCyan for odd rows
    rowStyles[i].ForegroundColor = (i % 2 == 0)
        ? Color.LightYellow
        : Color.LightCyan;

    // **Set cell background** using a **solid fill pattern**
    rowStyles[i].Pattern = BackgroundType.Solid;

    // Optional: you could also set font color, borders, etc., here
}
```

### Tại sao lại dùng **Mẫu Tô Đầy Đặc**?

Thuộc tính `Pattern` cho công cụ biết cách vẽ màu. Một mẫu `Solid` đảm bảo toàn bộ nền ô được tô, loại bỏ các đường lưới mờ có thể hiện ra. Đây là cách phổ biến nhất để **đặt nền cho ô** khi bạn muốn một giao diện sạch sẽ.

## Bước 3: Nhập `DataTable` với Các Kiểu Đã Chuẩn Bị

Khi mảng kiểu đã sẵn sàng, lời gọi nhập chỉ còn một dòng. Aspose.Cells sẽ tự động áp dụng kiểu tương ứng cho mỗi hàng.

```csharp
// Import the DataTable into the worksheet, applying the prepared styles
worksheet.Cells.ImportDataTable(
    dataTable,                     // source
    true,                          // include column names
    0,                             // start row (0‑based)
    0,                             // start column (0‑based)
    rowStyles);                    // array of styles
```

> **Điều gì xảy ra phía sau?**  
> Thư viện duyệt qua từng hàng, sao chép giá trị vào các ô, rồi áp dụng `Style` phù hợp từ `rowStyles`. Vì chúng ta đã định nghĩa **mẫu tô đầy đặc**, mỗi ô trong một hàng sẽ thừa hưởng cùng một màu nền, mang lại hiệu ứng **màu hàng xen kẽ** hoàn hảo.

## Bước 4: Lưu Workbook và Kiểm Tra Kết Quả

Một lần lưu nhanh sẽ cho phép bạn mở file trong Excel (hoặc bất kỳ trình xem tương thích nào) và quan sát hiệu ứng.

```csharp
// Save to disk – you can change the format to .xlsx, .xls, .csv, etc.
workbook.Save("AlternatingRowsReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved. Open 'AlternatingRowsReport.xlsx' to see the result.");
```

Khi mở file, các hàng 1, 3, 5… sẽ có màu vàng nhạt, trong khi các hàng 2, 4, 6… sẽ có màu cyan nhẹ. Phần tiêu đề cột vẫn giữ màu trắng, làm nổi bật dữ liệu.

![Worksheet showing alternating row colors](/images/alternating-row-colors.png "Screenshot of worksheet with alternating row colors")

*Văn bản thay thế hình ảnh:* **alternating row colors** screenshot of a worksheet where each row’s background alternates between light yellow and light cyan.

## Bước 5: Tùy Chỉnh Thêm (Tùy Chọn)

### Thay Đổi Màu Sắc

Nếu thương hiệu của bạn dùng các tông màu khác, chỉ cần thay `Color.LightYellow` và `Color.LightCyan` bằng bất kỳ `System.Drawing.Color` nào bạn muốn. Ví dụ:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.FromArgb(255, 235, 205) // Peach
                                            : Color.FromArgb(205, 235, 255); // Soft blue
```

### Sử Dụng Kiểu **Nền** Khác

Mặc dù `BackgroundType.Solid` là phổ biến nhất, bạn có thể thử nghiệm `BackgroundType.Gray125`, `BackgroundType.Horizontal`, hoặc bất kỳ mẫu nào mà thư viện hỗ trợ. Điều này sẽ thay đổi kết cấu hình ảnh trong khi vẫn **thêm màu nền**.

### Áp Dụng **Kiểu Ô Bảng Tính** cho Các Cột Cụ Thể

Đôi khi bạn chỉ muốn hiệu ứng xen kẽ trên các cột dữ liệu, để cột đầu tiên (ví dụ: ID) không bị ảnh hưởng. Tạo một kiểu riêng cho cột đó và gán sau khi nhập:

```csharp
Style idStyle = workbook.CreateStyle();
idStyle.ForegroundColor = Color.White;
idStyle.Pattern = BackgroundType.Solid;

// Apply to the first column (A)
for (int row = 0; row < dataTable.Rows.Count + 1; row++) // +1 for header
{
    worksheet.Cells[row, 0].SetStyle(idStyle);
}
```

---

## Kết Luận

Bạn đã có một giải pháp hoàn chỉnh, tái sử dụng được cho **màu hàng xen kẽ** trong bảng tính C#. Bằng cách xây dựng một mảng các đối tượng `Style`, **đặt nền cho ô** với **mẫu tô đầy đặc**, và nhập `DataTable` trong một lần gọi, bạn có thể tạo ra các báo cáo chuyên nghiệp với ít mã nhất.  

Từ đây, bạn có thể:

- **Thêm màu nền** cho các hàng tiêu đề để nhấn mạnh hơn.  
- Kết hợp kỹ thuật này với định dạng có điều kiện để tạo các gợi ý trực quan động.  
- Khám phá các thuộc tính **kiểu ô bảng tính** khác như phông chữ, viền, hoặc định dạng số.

Hãy thử áp dụng trong quy trình xuất dữ liệu tiếp theo—người dùng của bạn sẽ cảm ơn vì những bảng tính sạch sẽ, dễ đọc hơn. Chúc lập trình vui!

## Bạn Nên Học Gì Tiếp Theo?

- [Set Row Height in Worksheet with Aspose.Cells for .NET](/cells/english/net/size-and-spacing-customization/setting-height-of-all-rows-in-worksheet/)
- [Convert Excel Cell Names to Row and Column Indices Using Aspose.Cells for .NET](/cells/english/net/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-dotnet/)
- [Set Worksheet Tab Colors in Excel Using Aspose.Cells .NET - A Comprehensive Guide](/cells/english/net/worksheet-management/set-worksheet-tab-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}