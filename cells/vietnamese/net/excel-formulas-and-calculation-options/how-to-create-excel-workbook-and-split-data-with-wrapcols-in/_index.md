---
category: general
date: 2026-10-10
description: Tạo workbook Excel trong C# và sử dụng hàm WRAPCOLS để chia dữ liệu mảng
  thành các cột. Thực hiện theo hướng dẫn chi tiết từng bước với mã có thể chạy được.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- excel formula split data
- use wrapcols function
- how to use wrapcols
- split array columns
language: vi
lastmod: 2026-10-10
og_description: Tạo workbook Excel trong C# và áp dụng hàm WRAPCOLS để chia dữ liệu
  mảng thành các cột. Hướng dẫn này hiển thị toàn bộ mã và giải thích từng bước.
og_image_alt: Screenshot of an Excel sheet showing three columns filled by the WRAPCOLS
  formula
og_title: Tạo sổ làm việc Excel và chia dữ liệu bằng WRAPCOLS trong C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  headline: How to create Excel workbook and split data with WRAPCOLS in C#
  type: TechArticle
- description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  name: How to create Excel workbook and split data with WRAPCOLS in C#
  steps:
  - name: Using the function with different data types
    text: 'The `WRAPCOLS` function is not limited to numbers. You can split text values,
      dates, or mixed types:'
  - name: Variable column count at runtime
    text: 'Often the number of columns you need depends on user input. You can build
      the formula string dynamically:'
  - name: Large arrays and performance
    text: '`WRAPCOLS` can handle thousands of elements, but evaluating extremely large
      arrays in a single cell may increase calculation time. If you notice slowdown:'
  - name: Handling empty cells
    text: If the source array contains empty strings (`""`) or `NULL` values, `WRAPCOLS`
      inserts blank cells, preserving the column layout. This behavior is useful when
      you need placeholder columns for later data entry.
  - name: Using named ranges instead of literals
    text: 'For maintainability, define a named range that holds the source data, then
      reference it:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cách tạo workbook Excel và chia dữ liệu bằng WRAPCOLS trong C#
url: /vi/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-and-split-data-with-wrapcols-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách tạo workbook Excel và chia dữ liệu bằng WRAPCOLS trong C#

Nếu bạn cần **tạo workbook Excel** một cách lập trình, hướng dẫn này sẽ chỉ cho bạn cách thực hiện và cách **chia dữ liệu mảng** thành các cột bằng hàm `WRAPCOLS`. Bạn sẽ có một ví dụ hoàn chỉnh, có thể chạy được, tạo ra tệp `.xlsx` với dữ liệu được phân phối vào ba cột.

Bài học bao gồm mọi thứ bạn cần: các gói NuGet bắt buộc, từng dòng mã, lý do công thức `WRAPCOLS` hoạt động, và cách điều chỉnh giải pháp cho các kích thước mảng hoặc số cột khác nhau. Khi kết thúc, bạn sẽ có thể nhúng kỹ thuật **use wrapcols function** vào bất kỳ dự án C# nào tạo file Excel.

## Prerequisites

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có:

* .NET 6.0 SDK hoặc phiên bản mới hơn được cài đặt  
* Một IDE C# (Visual Studio, VS Code, Rider, v.v.)  
* Gói NuGet **Aspose.Cells for .NET** – thư viện cung cấp lớp `Workbook` được dùng trong các ví dụ  

Bạn không cần cài đặt Office; Aspose.Cells sẽ ghi tệp `.xlsx` trực tiếp.

## Step 1 – create Excel workbook

Nhiệm vụ đầu tiên là khởi tạo một đối tượng workbook mới và lấy tham chiếu tới worksheet đầu tiên. Bước này là nền tảng cho mọi thao tác tiếp theo.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();                // creates an empty Excel file in memory
        Worksheet ws = wb.Worksheets[0];             // the default worksheet is at index 0
```

`Workbook` đại diện cho toàn bộ file, trong khi `Worksheet` đại diện cho một sheet duy nhất. Bằng cách tạo workbook trong bộ nhớ, bạn tránh việc I/O đĩa cho đến khi lưu ra đĩa một cách có chủ ý.

## Step 2 – apply WRAPCOLS to split array columns

Bây giờ bạn sẽ đặt công thức vào ô **A1** sử dụng `WRAPCOLS`. Hàm này nhận hai đối số: mảng nguồn và số cột mà bạn muốn mảng được gói lại.

```csharp
        // Step 2: Apply the WRAPCOLS formula to split the array into 3 columns
        // The array {1,2,3,4,5,6} will be distributed as:
        // 1 2 3
        // 4 5 6
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

**Tại sao lại hoạt động:** `WRAPCOLS` lấy mảng phẳng `{1,2,3,4,5,6}` và điền vào worksheet theo hàng‑dọc, tạo ba cột cho mỗi hàng. Đối số đầu tiên có thể là bất kỳ literal mảng Excel nào, một named range, hoặc một công thức mảng động. Đối số thứ hai (`3`) cho Excel biết cần tạo bao nhiêu cột trước khi chuyển sang hàng tiếp theo.

### Using the function with different data types

Hàm `WRAPCOLS` không chỉ giới hạn ở số. Bạn có thể chia các giá trị văn bản, ngày tháng, hoặc các kiểu hỗn hợp:

```csharp
        // Example with mixed data: strings and numbers
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";
```

Khi mảng nguồn chứa chuỗi, Excel tự động coi kết quả là các ô văn bản. Tính linh hoạt này cho phép bạn **excel formula split data** cho báo cáo, dashboard, hoặc các tác vụ di chuyển dữ liệu.

## Step 3 – calculate formulas so the worksheet is populated

Công thức được lưu dưới dạng chuỗi cho đến khi bạn yêu cầu workbook tính toán chúng. Gọi `CalculateFormula` buộc Excel thực hiện tính toán và ghi kết quả vào các ô.

```csharp
        // Step 3: Calculate formulas so the worksheet is populated
        wb.CalculateFormula();   // evaluates all formulas in the workbook
```

Nếu không gọi hàm này, tệp đã lưu sẽ chỉ chứa văn bản công thức, không có giá trị đã tính. Phương thức này hoạt động trên toàn bộ workbook, vì vậy bạn có thể đặt thêm công thức ở các vị trí khác và tất cả sẽ được giải quyết chỉ bằng một lần gọi.

## Step 4 – save the workbook to see the result

Cuối cùng, ghi workbook ra đĩa. Chọn một thư mục bạn có quyền ghi, và đặt tên file rõ ràng.

```csharp
        // Step 4: Save the workbook to see the result
        string outputPath = @"output.xlsx";
        wb.Save(outputPath);      // creates output.xlsx in the application directory
    }
}
```

Khi mở `output.xlsx` trong Excel (hoặc bất kỳ trình xem tương thích nào), bạn sẽ thấy:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

Nếu bạn dùng ví dụ kiểu hỗn hợp, các hàng 3‑4 sẽ chứa văn bản và số tương ứng.

## Advanced variations and edge‑case handling

### Variable column count at runtime

Thường thì số cột bạn cần phụ thuộc vào đầu vào của người dùng. Bạn có thể xây dựng chuỗi công thức một cách động:

```csharp
int columns = 4; // could come from UI, config, etc.
string arrayLiteral = "{10,20,30,40,50,60,70,80}";
ws.Cells[5, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
```

### Large arrays and performance

`WRAPCOLS` có thể xử lý hàng ngàn phần tử, nhưng việc tính toán các mảng cực lớn trong một ô duy nhất có thể làm tăng thời gian tính toán. Nếu bạn nhận thấy chậm lại:

* Chia mảng nguồn thành các khối nhỏ hơn và ghi mỗi khối vào một ô bắt đầu riêng.  
* Sử dụng `WorkbookSettings` để bật tính toán đa luồng:

```csharp
wb.Settings.CalcMode = CalculationModeType.Automatic;
wb.Settings.EnableMultiThreadedCalc = true;
```

### Handling empty cells

Nếu mảng nguồn chứa chuỗi rỗng (`""`) hoặc giá trị `NULL`, `WRAPCOLS` sẽ chèn các ô trống, giữ nguyên bố cục cột. Hành vi này hữu ích khi bạn cần các cột placeholder cho việc nhập dữ liệu sau này.

### Using named ranges instead of literals

Để dễ bảo trì, hãy định nghĩa một named range chứa dữ liệu nguồn, sau đó tham chiếu tới nó:

```csharp
ws.Cells["D1:D6"].PutValue(new object[] { 11, 12, 13, 14, 15, 16 });
ws.Cells["E1"].Formula = "=WRAPCOLS(D1:D6,3)";
```

Bây giờ công thức sẽ đọc dữ liệu từ chính worksheet, cho phép **how to use wrapcols** trong các kịch bản báo cáo động.

## Common pitfalls and pro tips

* **Không bỏ qua đối số thứ hai.** `WRAPCOLS(array)` mà không chỉ định số cột sẽ trả về một cột duy nhất, làm mất mục đích chia dữ liệu.  
* **Tránh trộn các chiều của mảng.** Mảng nguồn phải là một chiều; cung cấp mảng hai chiều (ví dụ `{ {1,2},{3,4} }`) sẽ gây lỗi `#VALUE!`.  
* **Lưu sau khi tính toán.** Nếu bạn gọi `wb.Save` trước `CalculateFormula`, tệp sẽ chỉ chứa văn bản công thức.  
* **Kiểm tra quyền truy cập file.** Khi chạy trong môi trường bị hạn chế (ví dụ ASP.NET), đảm bảo danh tính tiến trình có thể ghi vào thư mục đích.

## Full working example

Dưới đây là chương trình hoàn chỉnh bạn có thể sao chép, dán và chạy. Nó bao gồm tất cả các import, xử lý lỗi, và chú thích.

```csharp
using System;
using Aspose.Cells;

class ExcelWrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Split a numeric array into 3 columns
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";

        // Split a mixed array (text + numbers) into 3 columns, starting at row 3
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";

        // Dynamically build a formula with a variable column count
        int columnCount = 4;
        string sourceArray = "{10,20,30,40,50,60,70,80}";
        ws.Cells[5, 0].Formula = $"=WRAPCOLS({sourceArray},{columnCount})";

        // Evaluate all formulas
        wb.CalculateFormula();

        // Save the workbook
        string outputPath = "output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Chạy chương trình sẽ tạo `output.xlsx` với ba vùng riêng biệt minh họa **excel formula split data** bằng hàm `WRAPCOLS`.

## Conclusion

Bây giờ bạn đã biết cách **tạo workbook Excel** trong C# và cách **sử dụng hàm wrapcols** để **chia các cột mảng** một cách hiệu quả. Các bước chính—khởi tạo `Workbook`, chèn công thức `WRAPCOLS`, tính toán, và lưu—tạo thành một mẫu có thể tái sử dụng cho bất kỳ tác vụ tự động nào yêu cầu phân phối dữ liệu qua các cột.

Từ đây bạn có thể:

* Kết hợp `WRAPCOLS` với các hàm mảng động khác như `FILTER` hoặc `SORT`.  
* Xuất các bộ dữ liệu lớn từ cơ sở dữ liệu và để Excel tự động sắp xếp bố cục.  
* Xây dựng báo cáo do người dùng điều khiển, trong đó số cột được chọn qua một điều khiển UI.

Hãy thử nghiệm với các nguồn mảng, số cột và công thức bổ sung khác nhau để mở rộng nền tảng này. Chúc bạn lập trình vui vẻ!

## What Should You Learn Next?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên đều bao gồm mã nguồn đầy đủ và các giải thích chi tiết từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách sử dụng WRAPCOLS trong C# – Tạo Excel Workbook với các hàm Wrap](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Tạo Excel Workbook – Chuyển Mảng thành Ma trận với WRAPCOLS](/cells/english/net/calculation-engine/create-excel-workbook-convert-array-to-matrix-with-wrapcols/)
- [Tạo Excel Workbook C# – Hướng dẫn từng bước](/cells/english/net/excel-workbook/create-excel-workbook-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}