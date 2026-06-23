---
category: general
date: 2026-03-22
description: Cách sử dụng lambda trong C# để làm việc với công thức Excel. Học cách
  viết công thức vào ô, chuyển phạm vi thành mảng, hiển thị mảng trong console và
  tính cotang trong Excel.
draft: false
keywords:
- how to use lambda
- display array in console
- convert range to array
- write formula to cell
- calculate cotangent in excel
language: vi
og_description: Cách sử dụng lambda trong C# để thao tác công thức Excel, chuyển phạm
  vi thành mảng, ghi công thức vào ô, hiển thị mảng trong console và tính cotang trong
  Excel.
og_title: Cách sử dụng Lambda trong C# với công thức Excel – Từng bước
tags:
- C#
- Aspose.Cells
- Excel Automation
- Lambda Expressions
title: Cách sử dụng Lambda trong C# với công thức Excel – Hướng dẫn toàn diện
url: /vi/net/formulas-functions/how-to-use-lambda-in-c-with-excel-formulas-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sử Dụng Lambda trong C# với Công Thức Excel – Hướng Dẫn Toàn Diện

Bạn đã bao giờ tự hỏi **cách sử dụng lambda** khi tự động hóa Excel từ C# chưa? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi cần kết hợp sức mạnh của các hàm mảng động mới của Excel với khả năng `LAMBDA` của C#. Tin tốt là gì? Thực tế nó khá đơn giản một khi bạn thấy các thành phần khớp nhau.

Trong tutorial này, chúng ta sẽ đi qua **việc ghi công thức vào ô**, **chuyển dải ô thành mảng**, **hiển thị mảng trong console**, và thậm chí **tính cotang trong Excel** — đồng thời chỉ cho bạn **cách sử dụng lambda** bên trong một lời gọi `REDUCE`. Khi kết thúc, bạn sẽ có một đoạn mã có thể chạy được và có thể chèn vào bất kỳ dự án .NET nào có tham chiếu tới Aspose.Cells (hoặc thư viện tương tự).

---

## Những Điều Bạn Sẽ Học

- Cách **ghi công thức vào ô** bằng C#.
- Cách **chuyển dải ô thành mảng** bằng hàm `EXPAND`.
- Cách **hiển thị mảng trong console** sau khi tính toán.
- Cách **tính cotang trong Excel** bằng `COT` và `COTH`.
- Cú pháp chính xác để **cách sử dụng lambda** trong hàm `REDUCE` của Excel từ C#.

> **Yêu cầu trước:** Bạn cần một phiên bản .NET mới (Core 6+ hoặc .NET Framework 4.7+) và thư viện Aspose.Cells for .NET được cài đặt qua NuGet.

---

## Bước 1: Thiết Lập Workbook và Ghi Công Thức Vào Ô

Điều đầu tiên chúng ta làm là tạo một workbook mới và lấy worksheet đầu tiên. Sau đó chúng ta **ghi một công thức vào ô** – trong trường hợp này ô `A1` sẽ chứa kết quả của một lời gọi `EXPAND`.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write formula to A1 – we’ll expand B1:C2 into a 4‑by‑5 array later
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";
```

**Tại sao điều này quan trọng:** Ghi công thức trực tiếp từ mã cho phép bạn tạo ra các bảng tính phức tạp một cách tự động mà không cần mở Excel. Nó cũng chuẩn bị nền tảng cho bước tiếp theo, nơi chúng ta **chuyển dải ô thành mảng**.

---

## Bước 2: Chuyển Dải Ô Thành Mảng với EXPAND

`EXPAND` là cách của Excel để biến một dải ô nhỏ thành một ma trận lớn hơn. Khi đặt công thức ở `A1`, Excel sẽ “spill” ra một khối 4 × 5 bắt đầu từ ô đó. Từ C#, chúng ta không cần sao chép giá trị thủ công – thư viện sẽ thực hiện việc này khi chúng ta gọi `Calculate`.

```csharp
        // The EXPAND formula will spill into A1:E4 (4 rows × 5 columns)
        // No extra code needed – the workbook will handle the spill.
```

**Cách sử dụng lambda:** Chưa tới lúc này, nhưng hãy chờ nhé. Đầu tiên chúng ta cần dữ liệu trong sheet, sau đó sẽ giảm chúng bằng một lambda.

---

## Bước 3: Sử Dụng LAMBDA Bên Trong REDUCE – Trọng Tâm của “Cách Sử Dụng Lambda”

Excel 365 đã giới thiệu `REDUCE`, nhận vào **giá trị khởi tạo**, **dải ô**, và một **LAMBDA** chỉ định cách kết hợp mỗi phần tử. Từ C# chúng ta chỉ cần gán chuỗi công thức; lambda tồn tại bên trong công thức Excel, không phải trong mã C#.

```csharp
        // Reduce the spilled array by summing all its values.
        // This demonstrates how to use lambda inside REDUCE.
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";
```

**Giải thích:**  
- `0` là giá trị khởi tạo của bộ tích lũy (`acc`).  
- `A1:D4` là dải ô chúng ta muốn xử lý (bốn cột đầu tiên của spill).  
- `LAMBDA(acc, x, acc + x)` chỉ cho Excel cộng mỗi ô (`x`) vào bộ tích lũy.  

Đó là bản chất của **cách sử dụng lambda** để tổng hợp trong ngữ cảnh bảng tính.

---

## Bước 4: Tính Cotang trong Excel – Từ Độ Đo Sang Hyperbolic

Nếu bạn cần kết quả lượng giác, các hàm `COT` và `COTH` của Excel rất tiện lợi. Chúng ta sẽ đặt chúng ở `G1` và `G2` tương ứng.

```csharp
        // Demonstrate trigonometric functions – cotangent and hyperbolic cotangent
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected result: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";      // Hyperbolic cotangent of 1
```

**Tại sao hữu ích:** Biết **cách tính cotang trong Excel** có thể giúp bạn tránh việc viết mã toán học tùy chỉnh, đặc biệt khi workbook sẽ được chia sẻ với những người không phải lập trình viên.

---

## Bước 5: Buộc Tính Toán và Lấy Mảng Đã Mở Rộng

Bây giờ chúng ta yêu cầu workbook tính toán mọi công thức, sau đó lấy mảng đã spill ra từ `A1`. Đây là nơi chúng ta **hiển thị mảng trong console**.

```csharp
        // Force calculation of all formulas
        workbook.Calculate();

        // Retrieve the spilled array from A1 as a 2‑D object
        var expanded = worksheet.Cells["A1"].Value;

        // Pretty‑print the 2‑D array to the console
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show the result of the REDUCE lambda
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**Bạn sẽ thấy:**  
- Một ma trận 4 × 5 được định dạng đẹp, in ra từng dòng.  
- Tổng được tính bởi lambda `REDUCE`.  
- Hai giá trị cotang.

Điều này hoàn thiện quy trình từ **ghi công thức vào ô** cho tới **hiển thị mảng trong console**.

---

## Ví Dụ Hoàn Chỉnh (Sẵn Sàng Sao Chép‑Dán)

Dưới đây là toàn bộ chương trình bạn có thể đưa vào một ứng dụng console. Nhớ thêm package `Aspose.Cells` qua NuGet trước (`dotnet add package Aspose.Cells`).

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Write EXPAND formula (convert range to array)
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";

        // Step 3: Use REDUCE with LAMBDA (how to use lambda)
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";

        // Step 4: Calculate cotangent values (calculate cotangent in excel)
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";

        // Step 5: Force calculation
        workbook.Calculate();

        // Step 6: Retrieve and display the expanded array (display array in console)
        var expanded = worksheet.Cells["A1"].Value;
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show REDUCE result
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**Kết quả console dự kiến (giá trị sẽ thay đổi tùy vào nội dung mặc định của B1:C2, mặc định là 0):**

```
Expanded array from A1 (4×5):
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0

Sum of A1:D4 (via REDUCE lambda): 0
Cotangent of π/4: 1
Hyperbolic cotangent of 1: 1.31303528549933
```

Bạn có thể tự do điền `B1:C2` với các số của mình trước khi chạy – ma trận sẽ phản ánh các giá trị đó.

---

## Mẹo Chuyên Gia & Những Cạm Bẫy Thường Gặp

- **Mẹo:** Nếu bạn muốn dải spill bắt đầu ở vị trí khác, chỉ cần thay đổi ô đích (`A1`). Hàm `EXPAND` sẽ tuân theo anchor mới.
- **Cẩn thận:** Các ô trống trong dải nguồn sẽ trở thành `0` trong mảng spill, có thể ảnh hưởng tới tổng `REDUCE` của bạn.
- **Trường hợp đặc biệt:** Khi workbook chứa các công thức phụ thuộc vào hàm volatile (ví dụ `NOW()`), hãy gọi `workbook.Calculate()` sau khi đặt tất cả công thức để đảm bảo mọi thứ được cập nhật.
- **Lưu ý hiệu năng:** Đối với các spill lớn, cân nhắc giới hạn kích thước trong lời gọi `EXPAND`; nếu không, bạn có thể cấp phát quá nhiều bộ nhớ.
- **Tương thích:** The `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}