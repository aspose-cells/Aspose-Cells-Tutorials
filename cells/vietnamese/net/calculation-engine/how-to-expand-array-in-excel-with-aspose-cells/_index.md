---
category: general
date: 2026-11-16
description: Học cách mở rộng mảng trong Excel bằng Aspose.Cells, các hàm mảng động
  và một hàm giảm lambda, sau đó ghi tệp Excel từ C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- create excel workbook
- how to use lambda
- dynamic array functions
- write excel file
language: vi
lastmod: 2026-11-16
og_description: Cách mở rộng mảng trong Excel bằng Aspose.Cells, các hàm mảng động
  và một hàm giảm lambda. Theo dõi ví dụ C# đầy đủ để ghi tệp Excel.
og_image_alt: Diagram illustrating how to expand array in an Excel worksheet
og_title: Cách mở rộng mảng trong Excel bằng Aspose.Cells – hướng dẫn từng bước
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to expand array in Excel using Aspose.Cells, dynamic array
    functions, and a lambda reducer, then write the Excel file from C#.
  headline: How to expand array in Excel with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. `EXPAND` pads missing columns with blank cells. The same works for
      rows.
    question: Can I expand to more columns than the source provides?
  - answer: '`EXPAND` will treat the source as a single row; you can still specify
      rows and columns to reshape it.'
    question: What if the source array is horizontal (`{1,2,3,4,5}`)?
  - answer: The lambda must return a value compatible with the accumulator type. For
      text concatenation you could use `LAMBDA(acc, val, acc & val)`.
    question: Does `REDUCE` work with non‑numeric data?
  - answer: Only when you need the computed values before saving. Excel will recalculate
      on open if you skip it.
    question: Do I need to call `CalculateFormula` for every change?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cách mở rộng mảng trong Excel bằng Aspose.Cells
url: /vi/net/calculation-engine/how-to-expand-array-in-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách mở rộng mảng trong Excel với Aspose.Cells

Nếu bạn cần **cách mở rộng mảng** trong một worksheet Excel từ C#, hướng dẫn này sẽ chỉ ra các bước chính xác. Bạn sẽ tạo một workbook Excel, sử dụng các hàm mảng động như `EXPAND` và `REDUCE`, áp dụng một **lambda** accumulator, và cuối cùng **ghi file Excel** ra đĩa. Cách tiếp cận này hoạt động với Aspose.Cells 23.10 trở lên và không yêu cầu cài đặt Excel thủ công.

Khi hoàn thành hướng dẫn này, bạn sẽ có một file `ExpandReduceDemo.xlsx` hoạt động đầy đủ, thể hiện sức mạnh của các công thức mảng động trong môi trường lập trình.

## Những gì bạn cần

- .NET 6.0 (hoặc bất kỳ phiên bản .NET nào được Aspose.Cells hỗ trợ)
- Gói Aspose.Cells cho .NET (`dotnet add package Aspose.Cells`)
- Trình soạn thảo mã hoặc IDE (Visual Studio, VS Code, Rider, v.v.)

Không cần bất kỳ COM interop hay cài đặt Office nào vì Aspose.Cells xử lý định dạng file nội bộ.

## Bước 1: Tạo workbook Excel

Nhiệm vụ đầu tiên là **tạo workbook excel** trong bộ nhớ. Aspose.Cells cung cấp lớp `Workbook`, đại diện cho toàn bộ file XLSX.

```csharp
using System;
using Aspose.Cells;

class ExpandReduceDemo
{
    static void Main()
    {
        // Step 1: instantiate a new workbook and get the default worksheet
        Workbook workbook = new Workbook();              // creates an empty .xlsx structure
        Worksheet sheet = workbook.Worksheets[0];        // the first (and only) sheet by default
```

> **Tại sao điều này quan trọng:** Khởi tạo một `Workbook` cung cấp cho bạn một canvas sạch sẽ. Worksheet mặc định đã được chuẩn bị sẵn, vì vậy bạn không cần phải thêm một sheet mới trừ khi muốn có nhiều sheet.

## Bước 2: Chèn một hằng số mảng dọc

Engine mảng động của Excel có thể làm việc với các hằng số mảng nguyên thủy. Chúng ta sẽ đặt mảng dọc `{1;2;3;4;5}` vào ô **A1**.

```csharp
        // Step 2: put a vertical array constant into A1
        sheet.Cells["A1"].PutValue("{1;2;3;4;5}");
```

> **Mẹo:** Dấu chấm phẩy (`;`) ngăn cách các hàng trong hằng số, trong khi dấu phẩy (`,`) sẽ ngăn cách các cột. Điều này phản ánh cú pháp của Excel.

## Bước 3: Mở rộng mảng thành ma trận

Bây giờ chúng ta trả lời câu hỏi cốt lõi – **cách mở rộng mảng** – bằng cách sử dụng hàm `EXPAND`. Công thức này mở rộng mảng một cột thành ma trận 5 hàng × 2 cột, bắt đầu tại **B1**.

```csharp
        // Step 3: use EXPAND to create a 5‑row by 2‑column matrix
        sheet.Cells["B1"].Formula = "EXPAND(A1,5,2)";
```

> **Tại sao lại dùng EXPAND?** `EXPAND(source, rows, cols)` buộc phạm vi nguồn chiếm kích thước đã chỉ định, bổ sung các ô trống nếu cần. Đây là cách dễ đọc nhất để tạo một ma trận lớn hơn từ một mảng đơn.

## Bước 4: Giảm ma trận bằng một lambda accumulator

Hàm `REDUCE` lặp qua một phạm vi và tổng hợp các giá trị bằng một biểu thức **lambda**. Ở đây chúng ta cộng mỗi giá trị cột lại thành một cột duy nhất, đặt kết quả vào **D1**.

```csharp
        // Step 4: REDUCE the expanded matrix using a lambda accumulator
        sheet.Cells["D1"].Formula = "REDUCE(A1, B1:E5, LAMBDA(acc, val, acc+val))";
```

> **Cách sử dụng lambda:** `LAMBDA(acc, val, acc+val)` nhận accumulator hiện tại (`acc`) và giá trị ô tiếp theo (`val`). Nó trả về accumulator mới, thực hiện việc cộng dồn. Điều này minh họa **cách sử dụng lambda** trong công thức Excel từ mã.

## Bước 5: Tính toán công thức để hiển thị kết quả

Aspose.Cells không tự động tính toán công thức khi bạn đặt chúng. Gọi `CalculateFormula` buộc engine tính toán mọi công thức trong workbook.

```csharp
        // Step 5: recalculate all formulas so the results are materialized
        workbook.CalculateFormula();
```

> **Lưu ý:** Nếu bạn mở file đã tạo trong Excel, các giá trị sẽ đã hiển thị vì chúng đã được tính trước.

## Bước 6: Ghi file Excel ra đĩa

Cuối cùng, **ghi excel file** bằng phương thức `Save`. Chọn một thư mục mà bạn có quyền ghi.

```csharp
        // Step 6: save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\ExpandReduceDemo.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Kết quả mong đợi

| A | B | C | D |
|---|---|---|---|
| {1;2;3;4;5} | 1 |  | 15 |
|            | 2 |  |    |
|            | 3 |  |    |
|            | 4 |  |    |
|            | 5 |  |    |

- **Cột B** và **C** chứa ma trận 5 × 2 được tạo bởi `EXPAND`.
- **Ô D1** hiển thị `15`, tổng của tất cả các số, được tính bằng công thức `REDUCE` + **lambda**.

## Các câu hỏi thường gặp và trường hợp đặc biệt

- **Tôi có thể mở rộng thành nhiều cột hơn so với nguồn không?**  
  Có. `EXPAND` sẽ điền các cột thiếu bằng ô trống. Tương tự với các hàng.

- **Nếu mảng nguồn là ngang (`{1,2,3,4,5}`) thì sao?**  
  `EXPAND` sẽ coi nguồn là một hàng duy nhất; bạn vẫn có thể chỉ định số hàng và cột để thay đổi hình dạng.

- **`REDUCE` có hoạt động với dữ liệu không phải số không?**  
  Lambda phải trả về một giá trị tương thích với kiểu accumulator. Đối với việc nối chuỗi, bạn có thể dùng `LAMBDA(acc, val, acc & val)`.

- **Có cần gọi `CalculateFormula` cho mỗi thay đổi không?**  
  Chỉ cần khi bạn muốn các giá trị đã tính trước khi lưu. Excel sẽ tự tính lại khi mở nếu bạn bỏ qua bước này.

## Mẹo chuyên nghiệp

- **Hiệu năng:** Đối với workbook lớn, gọi `workbook.CalculateFormula` một lần sau khi đặt tất cả công thức, thay vì sau mỗi ô.
- **An toàn phiên bản:** `EXPAND` và `REDUCE` có sẵn trong Excel 365 và các phiên bản sau. Aspose.Cells triển khai chúng bất kể phiên bản Excel mục tiêu vì engine tính toán được tích hợp sẵn.
- **Gỡ lỗi công thức:** Dùng `sheet.Cells["B1"].Formula` để đọc lại chuỗi công thức đã đặt; điều này hữu ích khi bạn xây dựng công thức một cách động.

## Kết luận

Bây giờ bạn đã biết **cách mở rộng mảng** trong Excel bằng Aspose.Cells, tận dụng **các hàm mảng động**, áp dụng **lambda** với `REDUCE`, và **ghi excel file** từ C#. Ví dụ toàn diện này có thể được điều chỉnh cho các chuyển đổi dữ liệu phức tạp hơn, như chuyển vị ma trận, tổng lũy kế, hoặc các phép tổng hợp tùy chỉnh.

---

*Bước tiếp theo:*  
- Khám phá các hàm động khác như `FILTER`, `SORT`, và `UNIQUE`.  
- Kết hợp nhiều biểu thức `LAMBDA` để xây dựng các hàm người dùng tái sử dụng.  
- Tích hợp việc tạo workbook vào các API ASP.NET Core để tạo báo cáo ngay lập tức.

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng dựa trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã mẫu đầy đủ với các giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to create Excel workbook C# with a dynamic array formula](/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/)
- [How to expand array in Excel and populate a template](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)
- [How to Expand Array in C# with Aspose.Cells – Step‑by‑Step Guide](/cells/english/net/excel-formulas-and-calculation-options/how-to-expand-array-in-c-with-aspose-cells-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}