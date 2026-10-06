---
category: general
date: 2026-03-01
description: Nhập dữ liệu có định dạng vào Excel bằng C#. Tìm hiểu cách nhập DataTable
  vào Excel và thêm màu nền cho các ô chỉ trong vài bước.
draft: false
keywords:
- import data with formatting
- how to import datatable into excel
- add background color to excel cells
language: vi
og_description: Nhập dữ liệu có định dạng vào Excel bằng C#. Hướng dẫn từng bước cho
  thấy cách nhập DataTable và thêm màu nền cho các ô.
og_title: Nhập dữ liệu có định dạng vào Excel – Hướng dẫn C#
tags:
- C#
- Excel
- DataTable
- Formatting
title: Nhập dữ liệu có định dạng vào Excel bằng C#
url: /vi/net/excel-data-import-export/import-data-with-formatting-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nhập Dữ liệu có Định dạng vào Excel bằng C#

Bạn đã bao giờ **nhập dữ liệu có định dạng** vào một workbook Excel nhưng lại chỉ nhận được một sheet đơn giản, nhàm chán? Bạn không phải là người duy nhất. Hầu hết các nhà phát triển gặp phải vấn đề này khi phát hiện rằng việc nhập mặc định sẽ xóa hết màu sắc và kiểu dáng mà họ đã tỉ mỉ thiết lập trong dữ liệu nguồn.

Trong hướng dẫn này, chúng ta sẽ đi qua một giải pháp hoàn chỉnh, sẵn sàng chạy ngay **nhập một DataTable vào Excel** và **thêm màu nền cho các ô Excel** đồng thời. Không cần xử lý hậu kỳ—bảng tính của bạn sẽ trông chính xác như mong muốn ngay từ đầu.

## Những gì bạn sẽ học

- Cách lấy dữ liệu vào một `DataTable`.
- Cách định nghĩa một mảng các đối tượng `Style` chứa màu nền.
- Cách gọi `ImportDataTable` với các style đó để việc nhập giữ nguyên định dạng.
- Một ví dụ đầy đủ, có thể chạy ngay mà bạn có thể sao chép vào một console app và thấy kết quả ngay lập tức.
- Các mẹo, lưu ý và biến thể cho các dự án thực tế.

### Yêu cầu trước

- .NET 6.0 hoặc mới hơn (mã cũng hoạt động với .NET Framework 4.6+).
- Thư viện **GemBox.Spreadsheet** (phiên bản miễn phí đã đủ cho demo).
- Kiến thức cơ bản về C# và Excel.

Nếu bạn thắc mắc *tại sao lại chọn GemBox?* vì nó cung cấp một phương thức một dòng `ImportDataTable` chấp nhận mảng style—đúng những gì chúng ta cần để **nhập dữ liệu có định dạng** mà không phải viết vòng lặp.

---

## Bước 1: Thiết lập dự án và thêm GemBox.Spreadsheet

Để bắt đầu, tạo một console app mới:

```bash
dotnet new console -n ExcelImportDemo
cd ExcelImportDemo
dotnet add package GemBox.Spreadsheet
```

> **Mẹo chuyên nghiệp:** Phiên bản miễn phí giới hạn số ô trong mỗi worksheet ở 150 k ô, đã đủ cho các demo. Nếu bạn vượt quá giới hạn, hãy nâng cấp hoặc chuyển sang EPPlus, nhưng API sẽ hơi khác một chút.

## Bước 2: Lấy dữ liệu nguồn dưới dạng `DataTable`

Điều đầu tiên chúng ta cần là một `DataTable` mô phỏng dữ liệu bạn thường lấy từ cơ sở dữ liệu. Dưới đây là một helper nhỏ tạo nó trong bộ nhớ:

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register the free license (remove for paid version).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve the source data as a DataTable.
        DataTable dataTable = GetSampleData();

        // Remaining steps will follow...
    }

    /// <summary>
    /// Generates a sample DataTable with three columns and five rows.
    /// In a real app you’d replace this with a DB call.
    /// </summary>
    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

**Tại sao điều này quan trọng:** Bằng cách tách việc lấy dữ liệu ra thành một phương thức riêng, bạn có thể thay thế bất kỳ nguồn nào—SQL, CSV, dịch vụ web—mà không ảnh hưởng đến logic nhập. Điều này giữ cho mã sạch sẽ và làm cho tutorial **cách nhập datatable vào excel** có thể tái sử dụng.

## Bước 3: Định nghĩa các Style bạn muốn áp dụng

Bây giờ là phần thú vị: chúng ta sẽ tạo một mảng các đối tượng `Style`, mỗi cái có một `ForegroundColor` riêng. GemBox cho phép bạn đặt `BackgroundPatternColor` (màu nền ô) và `ForegroundColor` (màu chữ). Trong demo này, chúng ta sẽ tô màu khác nhau cho hai cột đầu tiên.

```csharp
        // 2️⃣ Define the styles to apply to the imported cells.
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // Column 0 – Light blue fill
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Column 1 – Light green fill
            // No style for column 2 – it will keep the default look.
        };
```

**Giải thích:**  
- Các đối tượng `Style` là các container nhẹ; bạn không cần tạo một đối tượng mới cho mỗi ô.  
- Bằng cách sắp xếp thứ tự của mảng sao cho khớp với thứ tự cột, GemBox sẽ tự động áp dụng style tương ứng trong quá trình nhập.  
- Đây là chìa khóa để **nhập dữ liệu có định dạng**—định dạng đi cùng dữ liệu, không phải sau khi nhập.

## Bước 4: Nhập `DataTable` vào Worksheet với các Style

Khi dữ liệu và style đã sẵn sàng, chúng ta có thể tạo một workbook, chọn worksheet đầu tiên, và gọi `ImportDataTable`. Chữ ký của phương thức như sau:

```csharp
public void ImportDataTable(
    DataTable dataTable,
    bool includeColumnNames,
    int startRow,
    int startColumn,
    Style[] columnStyles = null);
```

Đây là cách chúng ta sử dụng nó:

```csharp
        // 3️⃣ Create a new workbook and import the DataTable.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        // Import, include column headers, start at A1 (0,0), apply our styles.
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the file to disk.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Excel file 'Report.xlsx' created with formatted data.");
```

**Điều gì đang diễn ra phía sau?**  
- `true` báo cho GemBox ghi tên các cột vào hàng đầu tiên.  
- `0, 0` đặt vị trí nhập tại ô A1.  
- `importStyles` liên kết mỗi cột với màu mà chúng ta đã định nghĩa trước đó.  

Khi bạn mở *Report.xlsx*, bạn sẽ thấy cột **ID** được tô nền xanh nhạt, cột **Name** được tô nền xanh lá nhạt, và cột **Score** không thay đổi. Đó là **nhập dữ liệu có định dạng** chỉ với một lời gọi.

## Bước 5: Kiểm tra kết quả (Kết quả mong đợi)

Mở file `Report.xlsx` vừa tạo. Bạn sẽ thấy một bảng như sau:

| ID (xanh nhạt) | Name (xanh lá nhạt) | Score |
|----------------|----------------------|-------|
| 1              | Alice                | 93.5 |
| 2              | Bob                  | 78.0 |
| 3              | Charlie              | 85.2 |
| 4              | Diana                | 91.3 |
| 5              | Ethan                | 67.8 |

- Các ô của cột **ID** có nền màu xanh nhạt.  
- Các ô của cột **Name** có nền màu xanh lá nhạt.  
- Cột **Score** giữ nền trắng mặc định.

Cảm giác trực quan này giúp báo cáo dễ dàng quét nhanh—một chi tiết nhỏ có thể cải thiện trải nghiệm người dùng đáng kể.

![Excel sheet showing import data with formatting – ID column light blue, Name column light green](excel-screenshot.png "import data with formatting example")

*Văn bản thay thế hình ảnh bao gồm từ khóa chính cho SEO.*

---

## Câu hỏi thường gặp & Trường hợp đặc biệt

### Có thể áp dụng nhiều hơn chỉ màu nền không?

Chắc chắn rồi. `Style` cho phép bạn đặt phông chữ, viền, định dạng số, và thậm chí định dạng có điều kiện. Ví dụ, để làm cho các điểm trên 90 trở nên in đậm và màu đỏ:

```csharp
Style highScoreStyle = new Style()
{
    FontColor = Color.Red,
    FontBold = true
};
worksheet.Cells["C2:C6"].ConditionalFormatting.Add(
    ConditionalFormattingCondition.GreaterThan, "90", highScoreStyle);
```

### Nếu DataTable của tôi có nhiều cột hơn số style đã định nghĩa thì sao?

GemBox sẽ chỉ áp dụng style cho những cột có mục tương ứng trong mảng. Các cột thừa sẽ sử dụng style mặc định—không có lỗi nào phát sinh.

### Điều này có hoạt động với tập dữ liệu lớn không?

Có, nhưng hãy chú ý tới giới hạn ô của phiên bản miễn phí (150 k ô). Đối với các báo cáo khổng lồ, hãy cân nhắc mua giấy phép trả phí hoặc truyền dữ liệu từng hàng một bằng `worksheet.Cells[row, col].Value = …`—tuy nhiên bạn sẽ mất đi tiện lợi của một dòng lệnh.

### Làm sao để nhập dữ liệu có định dạng từ một mẫu Excel có sẵn?

Bạn có thể tải workbook mẫu trước:

```csharp
var template = ExcelFile.Load("Template.xlsx");
var targetSheet = template.Worksheets[0];
targetSheet.Cells.ImportDataTable(dataTable, true, 5, 2, importStyles);
template.Save("FilledReport.xlsx");
```

Cách này cho phép bạn giữ lại logo tiêu đề, chân trang và bất kỳ style nào đã tồn tại, đồng thời **nhập dữ liệu có định dạng** cho phần dữ liệu động.

---

## Ví dụ Hoàn chỉnh (Sẵn sàng sao chép)

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register free license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Get the source data.
        DataTable dataTable = GetSampleData();

        // 2️⃣ Define column styles (background colors).
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // ID column
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Name column
            // Score column gets default style.
        };

        // 3️⃣ Create workbook and import with styles.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the result.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Report.xlsx created – import data with formatting complete.");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

Chạy chương trình (`dotnet run`) và mở file *Report.xlsx* để thấy màu sắc được áp dụng ngay lập tức.

---

## Kết luận

Bạn đã có một giải pháp vững chắc, cuối cùng

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}