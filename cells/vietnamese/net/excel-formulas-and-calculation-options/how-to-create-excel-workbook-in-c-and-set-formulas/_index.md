---
category: general
date: 2026-10-01
description: Tạo nhanh workbook Excel bằng C#, học cách thiết lập công thức, tính
  cotang và sử dụng hàm PI trong Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- how to calculate cot
- set formula in cell
- write formula to cell
- how to use pi function
language: vi
lastmod: 2026-10-01
og_description: Tạo sổ làm việc Excel trong C# với Aspose.Cells. Tìm hiểu cách đặt
  công thức, sử dụng hàm PI và tính cotang chỉ trong vài bước.
og_image_alt: Diagram showing an Excel workbook created in C# with a formula in cell
  A1
og_title: Tạo workbook Excel trong C# – đặt công thức và tính cot
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create Excel workbook in C# quickly, learn how to set a formula, calculate
    cotangent, and use the PI function in Aspose.Cells.
  headline: How to create Excel workbook in C# and set formulas
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cách tạo workbook Excel trong C# và đặt công thức
url: /vi/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-in-c-and-set-formulas/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách tạo workbook Excel trong C# và đặt công thức

Nếu bạn cần **tạo workbook Excel C#** bằng mã viết công thức vào một ô, hướng dẫn này sẽ chỉ cho bạn cách thực hiện. Bạn sẽ thấy cách đặt công thức trong một worksheet, sử dụng hàm PI có sẵn, và tính cotang của một góc — tất cả đều với Aspose.Cells.

Bài học bao phủ mọi thứ từ khởi tạo workbook đến việc lấy kết quả đã tính, vì vậy bạn có thể sao chép ví dụ đầy đủ vào dự án của mình mà không bỏ sót bất kỳ phần nào.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có:

* .NET 6.0 hoặc phiên bản mới hơn được cài đặt  
* Giấy phép Aspose.Cells hợp lệ (hoặc khóa đánh giá tạm thời)  
* Visual Studio 2022 hoặc bất kỳ IDE C# nào bạn ưa thích  

Không cần thêm bất kỳ gói NuGet nào ngoài `Aspose.Cells`.

## Tạo workbook Excel trong C#

Bước đầu tiên là khởi tạo một đối tượng `Workbook` mới. Đối tượng này đại diện cho toàn bộ file Excel trong bộ nhớ và cho phép bạn truy cập các worksheet của nó.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();                 // creates an empty .xlsx file
        var worksheet = workbook.Worksheets[0];        // the default first sheet

        // Continue with the rest of the steps...
```

Tạo workbook theo cách này đảm bảo file đã sẵn sàng cho bất kỳ thao tác tiếp theo nào, chẳng hạn như thêm dữ liệu, định dạng ô, hoặc viết công thức.

## Đặt công thức vào ô bằng hàm PI

Bây giờ bạn sẽ **viết công thức vào ô** A1. Công thức sử dụng hàm `PI()` để cung cấp hằng số π và hàm `COT` để tính cotang của nó.

```csharp
        // Step 2: Set a formula in cell A1 (row 0, column 0)
        // The formula calculates the cotangent of π/4, which equals 1
        worksheet.Cells[0, 0].Formula = "=COT(PI()/4)";

        // Continue with calculation...
```

*Tại sao điều này quan trọng*: `PI()` là hàm tích hợp sẵn trong Excel trả về giá trị của π. Khi chia nó cho 4 bạn sẽ có 45°, và `COT` trả về cotang của góc đó. Điều này minh họa **cách sử dụng hàm pi** trong công thức Excel từ C#.

## Cách tính cot với Aspose.Cells

Nếu bạn thắc mắc **cách tính cot** mà không cần tự chuyển đổi góc, hàm `COT` sẽ thực hiện phần việc nặng. Nó nhận một góc tính bằng radian, vì vậy bạn có thể kết hợp nó với `PI()` cho các góc phổ biến.

```csharp
        // Step 3: Recalculate the workbook so the formula is evaluated
        workbook.Calculate();

        // Step 4: Retrieve and display the calculated result
        double result = worksheet.Cells[0, 0].DoubleValue;
        Console.WriteLine($"Cotangent of PI/4 = {result}");
    }
}
```

Chạy chương trình sẽ in ra:

```
Cotangent of PI/4 = 1
```

Vì `COT(π/4)` bằng 1, đầu ra xác nhận rằng công thức đã được **đặt công thức vào ô** và tính toán đúng.

## Viết công thức vào ô – mẹo bổ sung

* **Nhiều công thức**: Bạn có thể gán công thức cho bất kỳ ô nào bằng thuộc tính `Formula` tương tự, ví dụ, `worksheet.Cells["B2"].Formula = "=SIN(PI()/2)";`.
* **Cài đặt quốc tế**: Aspose.Cells tôn trọng locale của workbook, vì vậy tên hàm vẫn giữ tiếng Anh (`PI`, `COT`) bất kể cài đặt khu vực của người dùng.
* **Hiệu năng**: Nếu cần đặt hàng ngàn công thức, hãy gom chúng lại và gọi `workbook.Calculate()` một lần ở cuối để tránh việc tính lại lặp đi lặp lại.

## Ví dụ đầy đủ có thể chạy được

Dưới đây là chương trình đầy đủ bạn có thể sao chép‑dán vào một dự án console. Nó bao gồm tất cả các câu lệnh `using` cần thiết và minh họa quy trình hoàn chỉnh từ tạo workbook đến xuất kết quả.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook and obtain the first worksheet
        var workbook = new Workbook();
        var worksheet = workbook.Worksheets[0];

        // Write a formula that uses the PI function and calculates cotangent
        worksheet.Cells[0, 0].Formula = "=COT(PI()/4)";

        // Force calculation so the formula value is materialized
        workbook.Calculate();

        // Read the calculated value and display it
        double cotValue = worksheet.Cells[0, 0].DoubleValue;
        Console.WriteLine($"Cotangent of PI/4 = {cotValue}");

        // Optional: save the workbook to verify the formula visually
        workbook.Save("CotExample.xlsx");
    }
}
```

**Kết quả mong đợi** khi bạn chạy chương trình:

```
Cotangent of PI/4 = 1
```

File `CotExample.xlsx` được tạo sẽ chứa công thức trong ô A1, cho phép bạn mở nó trong Excel và thấy cùng một kết quả.

## Kết luận

Bây giờ bạn đã biết cách **tạo workbook Excel C#** bằng mã viết công thức, sử dụng hàm `PI`, và **tính cot** với Aspose.Cells. Ví dụ bao phủ toàn bộ vòng đời: tạo workbook, **đặt công thức vào ô**, tính lại, và lấy kết quả.

Các bước tiếp theo bạn có thể khám phá:

* Áp dụng **viết công thức vào ô** cho các phép tính phức tạp hơn như mô hình tài chính.  
* Sử dụng **đặt công thức vào ô** cùng với định dạng có điều kiện để làm nổi bật kết quả.  
* Kết hợp **cách sử dụng hàm pi** với các biểu đồ lượng giác cho báo cáo khoa học.

Hãy thoải mái thử nghiệm với các góc, hàm và bố cục worksheet khác nhau. Thành thạo việc xử lý công thức trong C# mở ra cánh cửa cho các pipeline báo cáo Excel hoàn toàn tự động. Chúc bạn lập trình vui!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Calculate Cotangent in Excel with C# – Create Workbook, Use EXPAND](/cells/english/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/)
- [How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}