---
category: general
date: 2026-03-30
description: Tạo workbook Excel bằng C# sử dụng Aspose.Cells. Học cách áp dụng hàm
  lambda trong Excel, hàm sequence trong Excel, mở rộng mảng trong Excel và lưu workbook
  dưới dạng xlsx.
draft: false
keywords:
- create excel workbook c#
- lambda function excel
- save workbook as xlsx
- sequence function excel
- expand array excel
language: vi
og_description: Tạo nhanh workbook Excel bằng C#. Hướng dẫn này cho thấy cách sử dụng
  hàm lambda trong Excel, hàm sequence trong Excel, mở rộng mảng trong Excel và lưu
  workbook dưới dạng xlsx.
og_title: Tạo Workbook Excel bằng C# – Hướng dẫn Lambda, SEQUENCE & EXPAND
tags:
- Aspose.Cells
- C#
- Excel automation
title: Tạo Sổ làm việc Excel bằng C# – Hướng dẫn Lambda, SEQUENCE & EXPAND
url: /vi/net/formulas-functions/create-excel-workbook-c-lambda-sequence-expand-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Workbook Excel C# – Hướng dẫn Lambda, SEQUENCE & EXPAND

Bạn đã bao giờ cần **tạo workbook Excel C#** cho một báo cáo tự động, nhưng không chắc nên dùng API nào? Bạn không phải là người duy nhất—nhiều nhà phát triển gặp khó khăn tương tự khi lần đầu tiếp cận việc tạo Excel bằng mã. Trong hướng dẫn này, bạn sẽ thấy một ví dụ hoàn chỉnh, có thể chạy được, bao gồm mọi thứ từ **hàm SEQUENCE mới của Excel** đến **hàm LAMBDA mạnh mẽ của Excel**, và ngay cả cách **mở rộng mảng Excel**.  

Chúng tôi cũng sẽ chỉ cho bạn các bước chính xác để **lưu workbook dưới dạng xlsx** để bạn có thể chia sẻ file cho bất kỳ ai dùng Excel. Khi kết thúc tutorial, bạn sẽ có một đoạn mã sẵn sàng cho môi trường production mà có thể chèn vào bất kỳ dự án .NET nào. Không có liên kết “xem tài liệu” mơ hồ—chỉ có mã hoạt động ngay hôm nay.

## Những gì bạn cần

- **.NET 6.0 trở lên** – ví dụ này nhắm tới .NET 6, nhưng bất kỳ phiên bản gần đây nào cũng được.  
- **Aspose.Cells for .NET** – cài đặt qua NuGet (`Install-Package Aspose.Cells`).  
- Kiến thức cơ bản về cú pháp C# (biến, đối tượng, và biểu thức lambda).  
- Một IDE mà bạn cảm thấy thoải mái (Visual Studio, Rider, hoặc VS Code).  

Đó là tất cả. Không cần COM interop, không cần cài Office trên server—Aspose.Cells xử lý mọi thứ trong bộ nhớ.

## Tạo Workbook Excel C# – Triển khai từng bước

Dưới đây chúng tôi chia quá trình thành các bước nhỏ gọn. Mỗi bước có tiêu đề rõ ràng, một đoạn mã ngắn, và giải thích **tại sao** chúng ta làm như vậy. Bạn có thể sao chép toàn bộ khối mã ở cuối và chạy như một ứng dụng console.

### Bước 1 – Khởi tạo Workbook mới

Đầu tiên, chúng ta cần một đối tượng workbook trống đại diện cho file Excel trong bộ nhớ.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // empty workbook
Worksheet sheet = workbook.Worksheets[0];         // default first sheet
```

*Lý do quan trọng:* `Workbook` là điểm khởi đầu cho mọi thao tác Aspose.Cells. Khi lấy `Worksheet` đầu tiên, chúng ta có một “canvas” để ghi công thức, giá trị, hoặc định dạng.  

> **Mẹo:** Nếu cần nhiều sheet, chỉ cần gọi `workbook.Worksheets.Add()` và giữ tham chiếu tới mỗi sheet.

### Bước 2 – Sử dụng hàm SEQUENCE Excel để tạo dữ liệu

**Hàm sequence excel** tạo một mảng động các số mà không cần VBA. Chúng ta sẽ đặt nó vào ô `A1` và để Excel tự động mở rộng.

```csharp
// Step 2: Generate a 5‑row, 1‑column array from a SEQUENCE
sheet["A1"].Formula = "EXPAND(SEQUENCE(3),5,1)"; // 1..3 padded with blanks
```

*Lý do quan trọng:* `SEQUENCE(3)` cho ra `[1,2,3]`. Bao bọc nó bằng `EXPAND` buộc kết quả vào một vùng 5 hàng, lấp đầy các hàng còn lại bằng ô trống. Điều này đồng thời minh họa **sequence function excel** và **expand array excel**.

### Bước 3 – Tổng hợp số bằng hàm LAMBDA Excel

Bây giờ chúng ta sẽ trình diễn khả năng của **lambda function excel**. Chúng ta sẽ cộng các số 1‑5 bằng hàm `REDUCE` mới, hàm này nội bộ dựa vào một lambda.

```csharp
// Step 3: Aggregate a sequence (sum 1..5) using REDUCE/LAMBDA
sheet["B1"].Formula = "REDUCE(0, SEQUENCE(5), LAMBDA(a,b, a+b))"; // result = 15
```

*Lý do quan trọng:* `REDUCE` lặp qua mảng được tạo bởi `SEQUENCE(5)`, đưa mỗi phần tử (`b`) vào lambda cùng với bộ tích lũy (`a`). Lambda `a+b` cộng chúng lại, cho kết quả `15` ở `B1`. Đây là cách sạch sẽ, chỉ dùng công thức để thực hiện giảm tổng mà không cần vòng lặp trong C#.

### Bước 4 – Áp dụng các hàm lượng giác trực tiếp trong ô

Các hàm toán học tích hợp sẵn của Excel rất tiện cho các phép tính nhanh. Chúng ta sẽ đặt một cotangent và một hyperbolic cotangent vào các ô liền kề.

```csharp
// Step 4: Trigonometric functions directly in Excel cells
sheet["C1"].Formula = "COT(PI()/4)";   // evaluates to 1
sheet["D1"].Formula = "COTH(1)";      // hyperbolic cotangent of 1
```

*Lý do quan trọng:* Minh họa rằng bạn có thể kết hợp các hàm toán học cổ điển với các công thức mảng động mới. Không cần tính các giá trị này trong C# trừ khi bạn có lý do về hiệu năng.

### Bước 5 – Tính toán tất cả công thức

Aspose.Cells không tự động tính công thức khi bạn đặt chúng. Bạn phải yêu cầu nó thực hiện tính toán.

```csharp
// Step 5: Force calculation so that cells store the results
workbook.CalculateFormula();
```

*Lý do quan trọng:* Sau lệnh này, thuộc tính `Value` của mỗi ô chứa kết quả đã được đánh giá, sẵn sàng để lưu hoặc đọc lại.

### Bước 6 – Lưu Workbook dưới dạng Xlsx

Cuối cùng, chúng ta ghi workbook ra đĩa bằng mẫu **save workbook as xlsx**.

```csharp
// Step 6: Save the workbook to an Excel file (XLSX format)
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "NewFunctions.xlsx");

workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to: {outputPath}");
```

*Lý do quan trọng:* Phương thức `Save` tự động nhận diện phần mở rộng file. Khi dùng “.xlsx”, chúng ta đảm bảo file tương thích với các phiên bản Excel hiện đại. Đường dẫn được đặt tới desktop để dễ truy cập trong quá trình thử nghiệm.

### Ví dụ đầy đủ hoạt động

Dưới đây là chương trình hoàn chỉnh mà bạn có thể dán vào một dự án console mới. Nó bao gồm tất cả các bước ở trên, cộng với một khối kiểm tra nhỏ in các giá trị đã tính ra console.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Initialize workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // SEQUENCE + EXPAND
        sheet["A1"].Formula = "EXPAND(SEQUENCE(3),5,1)";

        // REDUCE with LAMBDA
        sheet["B1"].Formula = "REDUCE(0, SEQUENCE(5), LAMBDA(a,b, a+b))";

        // Trig functions
        sheet["C1"].Formula = "COT(PI()/4)";
        sheet["D1"].Formula = "COTH(1)";

        // Calculate formulas
        workbook.CalculateFormula();

        // Verify results (optional)
        Console.WriteLine("A1‑A5 (expanded SEQUENCE):");
        for (int i = 0; i < 5; i++)
        {
            Console.WriteLine($"  Row {i + 1}: {sheet.Cells[i, 0].Value ?? "blank"}");
        }
        Console.WriteLine($"B1 (sum 1‑5): {sheet["B1"].Value}");
        Console.WriteLine($"C1 (cot(π/4)): {sheet["C1"].Value}");
        Console.WriteLine($"D1 (coth(1)): {sheet["D1"].Value}");

        // Save workbook
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "NewFunctions.xlsx");
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

**Kết quả mong đợi trên console**

```
A1‑A5 (expanded SEQUENCE):
  Row 1: 1
  Row 2: 2
  Row 3: 3
  Row 4: blank
  Row 5: blank
B1 (sum 1‑5): 15
C1 (cot(π/4)): 1
D1 (coth(1)): 1.31303528549933
Workbook saved to: C:\Users\YourName\Desktop\NewFunctions.xlsx
```

Và khi mở *NewFunctions.xlsx* bạn sẽ thấy các số giống nhau được sắp xếp trong bốn cột đầu tiên.

![tạo workbook excel c# ảnh chụp màn hình của bảng tính kết quả](/images/create-excel-workbook-csharp.png)

## Trường hợp đặc biệt, Mẹo và Câu hỏi thường gặp

- **Nếu tôi cần nhiều hơn một sheet thì sao?**  
  Chỉ cần gọi `workbook.Worksheets.Add()` và lặp lại việc gán công thức trên mỗi đối tượng `Worksheet` mới.  

- **Có thể dùng các phiên bản Excel cũ hơn không?**  
  Các hàm mảng động (`SEQUENCE`, `EXPAND`, `REDUCE`) yêu cầu Excel 365 hoặc Excel 2021+. Nếu bạn nhắm tới các phiên bản cũ hơn, hãy dùng công thức cổ điển hoặc tính giá trị trong C# trước khi ghi vào.  

- **Lo ngại về hiệu năng?**  
  Đối với hàng ngàn dòng, việc đặt công thức trên một vùng và sau đó gọi `CalculateFormula` thường nhanh hơn so với việc lặp và gán giá trị từng ô một.  

- **Lưu vào stream thay vì file?**  
  `work

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}