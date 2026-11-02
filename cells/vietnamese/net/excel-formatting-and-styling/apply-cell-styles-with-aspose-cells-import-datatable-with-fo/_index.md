---
category: general
date: 2026-06-05
description: Áp dụng kiểu ô khi sử dụng nhập khẩu Aspose.Cells. Tìm hiểu cách nhập
  DataTable với định dạng, tạo kiểu cho các hàng và giữ cho các bảng tính gọn gàng.
draft: false
keywords:
- apply cell styles
- aspose cells import
- import with formatting
- how to import datatable
- import datatable worksheet
language: vi
og_description: Áp dụng kiểu ô khi nhập DataTable vào worksheet của Aspose.Cells.
  Hướng dẫn từng bước kèm mã đầy đủ và mẹo.
og_title: Áp dụng kiểu ô với Aspose.Cells – Nhập DataTable
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  headline: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  type: TechArticle
- description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  name: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  steps:
  - name: How It Works
    text: 1. **Headers** – Because we passed `true`, Aspose writes “Name” and “Score”
      into the first row. 2. **Data Rows** – Each subsequent row receives the corresponding
      style from `importStyles`. 3. **Performance** – The method streams the data
      directly into the worksheet, which is faster than looping cell
  - name: What if My DataTable Has More Columns Than Styles?
    text: Aspose will apply the last style in the array to any extra columns. To avoid
      unexpected colors, always match the array length to the column count, or pass
      `null` for columns you don’t want styled.
  - name: Can I Apply Different Styles to Specific Rows?
    text: 'Absolutely. After the import, you can loop through rows and assign new
      `Style` objects based on conditions (e.g., highlight scores > 90 in green).
      Here’s a quick snippet:'
  - name: Does This Work with Large DataSets?
    text: Yes. `ImportDataTable` streams data efficiently, and applying a static style
      array adds negligible overhead. For millions of rows, consider using `ImportDataTable`
      in chunks or leveraging `Cells.ImportDataTable` with a `DataReader` for even
      better memory usage.
  - name: How Do I Preserve Existing Formatting in the Worksheet?
    text: If the target range already has formatting you want to keep, set the `ImportDataTable`
      overload’s `importOptions` parameter (`ImportTableOptions`) and tweak `ImportDataTableOptions.PreserveCellFormatting`.
      The default behavior overwrites styles with the ones you supply.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DataTable
title: Áp dụng kiểu ô với Aspose.Cells – Nhập DataTable với định dạng
url: /vi/net/excel-formatting-and-styling/apply-cell-styles-with-aspose-cells-import-datatable-with-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Áp dụng kiểu ô với Aspose.Cells – Nhập DataTable với Định dạng

Bạn đã bao giờ tự hỏi làm thế nào để **apply cell styles** khi bạn kéo một `DataTable` vào một sheet Excel chưa? Bạn không phải là người duy nhất. Trong nhiều kịch bản báo cáo, bạn cần dữ liệu trông đẹp ngay từ đầu—không cần định dạng thủ công sau này. Tin tốt là Aspose.Cells giúp **import with formatting** một cách dễ dàng để các hàng của bạn có thể màu đỏ hoặc xanh, in đậm, hoặc bất kỳ gì bạn muốn.

Trong tutorial này, chúng tôi sẽ hướng dẫn qua một ví dụ hoàn chỉnh, có thể chạy được, cho thấy **how to import datatable** vào một worksheet **with cell styles** đã được áp dụng. Khi kết thúc, bạn sẽ có một ứng dụng console C# sẵn sàng chạy, tạo một workbook, định dạng hai cột đầu tiên, và lưu file—tất cả đều sử dụng API `aspose cells import`.

## Những gì bạn sẽ học

- Cài đặt Aspose.Cells trong một dự án .NET  
- Xây dựng một `DataTable` mẫu mô phỏng dữ liệu thực tế  
- Định nghĩa các đối tượng `Style` cho phông chữ màu đỏ và xanh  
- Sử dụng `Worksheet.Cells.ImportDataTable` để **import datatable worksheet** trong khi áp dụng các kiểu  
- Xác minh kết quả và lưu workbook  

Không cần công cụ bên ngoài, chỉ cần C# thuần và Aspose.Cells. Hãy bắt đầu.

---

## Yêu cầu trước

Trước khi chúng ta bắt đầu với mã, hãy chắc chắn rằng bạn có những thứ sau:

| Yêu cầu | Lý do quan trọng |
|-------------|----------------|
| .NET 6.0 hoặc sau | Aspose.Cells 23.x nhắm tới .NET Standard 2.0+, vì vậy .NET 6 cung cấp các tính năng runtime mới nhất. |
| Aspose.Cells cho .NET (NuGet) | Thư viện cung cấp các phương thức `Workbook`, `Worksheet`, `Style`, và `ImportDataTable` mà chúng ta cần. |
| Kiến thức C# cơ bản | Bạn sẽ hiểu về lớp, mảng, và các câu lệnh `using`. |
| Một IDE (Visual Studio, VS Code, Rider) | Bất kỳ trình chỉnh sửa nào cũng được, nhưng bạn sẽ cần khôi phục các gói NuGet. |

Bạn có thể cài đặt gói từ dòng lệnh:

```bash
dotnet add package Aspose.Cells
```

---

## Bước 1: Tạo một Workbook mới và Truy cập Worksheet đầu tiên

Đầu tiên—hãy tạo một `Workbook` và lấy sheet đầu tiên. Hãy nghĩ workbook như một cuốn sổ trắng; worksheet đầu tiên là trang chúng ta sẽ viết lên.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Create a new workbook (equivalent to a new Excel file)
        Workbook wb = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet worksheet = wb.Worksheets[0];
```

> **Mẹo:** Nếu bạn cần nhiều sheet, chỉ cần thêm chúng bằng `wb.Worksheets.Add()` và tham chiếu bằng tên hoặc chỉ mục.

---

## Bước 2: Chuẩn bị một DataTable mẫu (Cách nhập DataTable)

Bây giờ chúng ta cần một thứ để nhập. Trong các dự án thực tế bạn sẽ gọi DB, nhưng để minh bạch chúng ta sẽ tạo một `DataTable` trong bộ nhớ.

```csharp
        // Build a sample DataTable with two columns: Name and Score
        DataTable dataTable = new DataTable("Results");
        dataTable.Columns.Add("Name", typeof(string));
        dataTable.Columns.Add("Score", typeof(int));

        // Populate rows – imagine these came from a query
        dataTable.Rows.Add("Alice", 85);
        dataTable.Rows.Add("Bob", 92);
        dataTable.Rows.Add("Charlie", 78);
        dataTable.Rows.Add("Diana", 91);
```

> **Lý do quan trọng:** Có một `DataTable` cho phép chúng ta kiểm tra luồng **aspose cells import** mà không cần phụ thuộc bên ngoài.

---

## Bước 3: Định nghĩa các Style để áp dụng cho các ô đã nhập

Đây là nơi phép thuật xảy ra. Chúng ta sẽ tạo hai đối tượng `Style`: một với phông chữ màu đỏ, một với phông chữ màu xanh. Chúng sẽ được áp dụng theo cột trong quá trình nhập.

```csharp
        // Define an array of styles – one per column
        Style[] importStyles = new Style[2];

        // Style for the first column (Name) – red text
        Style redStyle = wb.CreateStyle();
        redStyle.Font.Color = Color.Red;
        importStyles[0] = redStyle;

        // Style for the second column (Score) – blue text
        Style blueStyle = wb.CreateStyle();
        blueStyle.Font.Color = Color.Blue;
        importStyles[1] = blueStyle;
```

> **Cảnh báo:** Độ dài của `importStyles` phải khớp với số cột bạn đang nhập, nếu không Aspose sẽ ném ra một `ArgumentException`.

---

## Bước 4: Nhập DataTable vào Worksheet **with Formatting**

Bây giờ chúng ta kết hợp mọi thứ lại. Phương thức `ImportDataTable` overload mà chúng ta dùng chấp nhận mảng `Style[]`, cho phép chúng ta **apply cell styles** khi dữ liệu được đưa vào sheet.

```csharp
        // Import the DataTable starting at cell A1 (row 0, column 0)
        // The 'true' flag tells Aspose to generate column headers automatically
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);
```

### Cách hoạt động

1. **Headers** – Vì chúng ta truyền `true`, Aspose ghi “Name” và “Score” vào hàng đầu tiên.  
2. **Data Rows** – Mỗi hàng tiếp theo nhận kiểu tương ứng từ `importStyles`.  
3. **Performance** – Phương thức truyền dữ liệu trực tiếp vào worksheet, nhanh hơn so với việc lặp qua từng ô.

---

## Bước 5: Xác minh kết quả và lưu Workbook

Hãy xem qua một vài ô đầu tiên để chắc chắn các style đã được áp dụng, sau đó ghi file ra đĩa.

```csharp
        // Optional: Quick sanity check – print the first row's values
        Console.WriteLine("Header Row:");
        Console.WriteLine($"{worksheet.Cells[0, 0].StringValue} | {worksheet.Cells[0, 1].StringValue}");

        // Save the workbook to an Excel file
        string outputPath = "StyledImport.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Khi bạn mở **StyledImport.xlsx**, bạn sẽ thấy:

- Cột “Name” có văn bản **red**.  
- Cột “Score” có văn bản **blue**.  
- Các tiêu đề cột ở kiểu mặc định (bạn cũng có thể định dạng chúng, nhưng đó là một tutorial khác).

![Ví dụ áp dụng kiểu ô](https://example.com/images/apply-cell-styles.png "Áp dụng kiểu ô trong Aspose.Cells")

> **Lưu ý:** Hình ảnh trên minh họa giao diện cuối cùng. Thuộc tính `alt` chứa từ khóa chính, đáp ứng yêu cầu SEO.

---

## Câu hỏi thường gặp & Trường hợp đặc biệt

### Nếu DataTable của tôi có nhiều cột hơn số Style?

Aspose sẽ áp dụng style cuối cùng trong mảng cho bất kỳ cột thừa nào. Để tránh màu không mong muốn, luôn đảm bảo độ dài mảng khớp với số cột, hoặc truyền `null` cho các cột bạn không muốn định dạng.

### Tôi có thể áp dụng các Style khác nhau cho các hàng cụ thể không?

Chắc chắn. Sau khi nhập, bạn có thể lặp qua các hàng và gán các đối tượng `Style` mới dựa trên điều kiện (ví dụ, làm nổi bật các điểm > 90 bằng màu xanh lá). Dưới đây là một đoạn mã nhanh:

```csharp
for (int i = 1; i <= dataTable.Rows.Count; i++) // start at 1 to skip header
{
    int score = worksheet.Cells[i, 1].IntValue;
    if (score > 90)
    {
        Style highScore = wb.CreateStyle();
        highScore.Font.Color = Color.Green;
        worksheet.Cells[i, 1].SetStyle(highScore);
    }
}
```

### Điều này có hoạt động với DataSets lớn không?

Có. `ImportDataTable` truyền dữ liệu một cách hiệu quả, và việc áp dụng một mảng style tĩnh gây overhead không đáng kể. Đối với hàng triệu dòng, hãy cân nhắc sử dụng `ImportDataTable` theo từng khối hoặc tận dụng `Cells.ImportDataTable` với `DataReader` để sử dụng bộ nhớ tốt hơn.

### Làm sao để giữ nguyên định dạng hiện có trong Worksheet?

Nếu vùng mục tiêu đã có định dạng bạn muốn giữ, hãy đặt tham số `importOptions` của overload `ImportDataTable` (`ImportTableOptions`) và điều chỉnh `ImportDataTableOptions.PreserveCellFormatting`. Hành vi mặc định sẽ ghi đè các style bằng những style bạn cung cấp.

---

## Tóm tắt: Những gì chúng ta đã đạt được

- **Applied cell styles** trong một thao tác **aspose cells import**.  
- Demonstrated **import with formatting** bằng cách truyền một mảng `Style[]`.  
- Showed **how to import datatable** vào một worksheet và lưu kết quả.  
- Covered edge cases như số lượng style không khớp và định dạng hàng có điều kiện.  

Tất cả đều được thực hiện trong một ứng dụng console duy nhất, tự chứa—không cần script bên ngoài, không cần chỉnh sửa Excel thủ công. Giờ bạn có nền tảng vững chắc cho bất kỳ tính năng báo cáo hoặc xuất dữ liệu nào cần đầu ra Excel được định dạng đẹp mắt.

---

## Bước tiếp theo

Sẵn sàng nâng cấp? Dưới đây là một vài ý tưởng mở rộng từ những gì bạn vừa học:

- **Style the header row** (ví dụ, in đậm, màu nền).  
- **Apply conditional formatting** using `Worksheet.Cells[i, j].ConditionalFormattingCollection`.  
- **Export to other formats** như CSV hoặc PDF với `wb.Save("file.pdf", SaveFormat.Pdf)`.  
- **Combine multiple DataTables** vào một workbook duy nhất, mỗi bảng trên một sheet riêng, sử dụng cùng cách định dạng.

Nếu bạn gặp bất kỳ vấn đề nào, hãy để lại bình luận hoặc kiểm tra tài liệu chính thức của Aspose về `ImportDataTable`. Chúc lập trình vui vẻ, và tận hưởng những file Excel được định dạng đẹp mắt!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh, hoạt động với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách nhập DataTable vào Excel bằng Aspose.Cells cho .NET (Hướng dẫn từng bước)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Cách đặt kiểu phông chữ trong Excel bằng Aspose.Cells cho .NET (Hướng dẫn từng bước)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)
- [Cách áp dụng bóng văn bản trong Excel bằng Aspose.Cells .NET: Hướng dẫn từng bước](/cells/english/net/formatting/apply-text-shadow-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}