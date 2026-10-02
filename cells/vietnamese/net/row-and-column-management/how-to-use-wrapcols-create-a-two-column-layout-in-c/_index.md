---
category: general
date: 2026-02-15
description: Cách sử dụng WRAPCOLS để tạo bố cục hai cột, thêm công thức và tạo mảng
  chuỗi trong các bảng tính C# – hướng dẫn từng bước.
draft: false
keywords:
- how to use wrapcols
- create two column layout
- how to add formula
- how to create columns
- generate sequence array
language: vi
og_description: Cách sử dụng WRAPCOLS để xây dựng bố cục hai cột, thêm công thức và
  tạo mảng dãy trong bảng tính C# – hướng dẫn đầy đủ.
og_title: 'Cách sử dụng WRAPCOLS: Bố cục hai cột trong C#'
tags:
- CSharp
- ExcelAutomation
- WorksheetFormula
title: 'Cách sử dụng WRAPCOLS: Tạo bố cục hai cột trong C#'
url: /vi/net/row-and-column-management/how-to-use-wrapcols-create-a-two-column-layout-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sử Dụng WRAPCOLS: Tạo Bố Cục Hai Cột trong C#

Bạn đã bao giờ tự hỏi **cách sử dụng WRAPCOLS** khi cần một giao diện hai cột nhanh chóng trong một bảng tính kiểu Excel? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi cố gắng chia một danh sách đã tạo thành các cột gọn gàng mà không phải viết vòng lặp cho mỗi ô. Tin tốt là gì? Với hàm `WRAPCOLS` bạn có thể đặt một công thức duy nhất vào `A1` và để Excel (hoặc một engine tương thích) thực hiện công việc nặng.

Trong hướng dẫn này, chúng tôi sẽ hướng dẫn **cách thêm công thức** tạo **bố cục hai cột**, cho bạn thấy **cách tạo cột** một cách động, và thậm chí **tạo mảng chuỗi** giá trị ngay lập tức. Khi kết thúc, bạn sẽ có một đoạn mã C# có thể chạy được hoàn chỉnh mà bạn có thể dán vào dự án, chạy và thấy một khối hai cột gọn gàng xuất hiện ngay lập tức.

## Những Điều Bạn Sẽ Học

- Mục đích của `WRAPCOLS` và lý do nó là một lựa chọn thay thế tốt hơn so với việc lặp thủ công.  
- Cách **thêm công thức** vào một ô trong worksheet bằng C#.  
- Cách tạo mảng chuỗi với `SEQUENCE` và đưa nó vào `WRAPCOLS`.  
- Mẹo để tính lại sheet sao cho công thức được giải quyết ngay lập tức.  
- Xử lý các trường hợp biên (ví dụ: worksheet trống, số cột tùy chỉnh).

Không cần thư viện bên ngoài nào ngoài một gói xử lý Excel tiêu chuẩn – chúng tôi sẽ sử dụng **ClosedXML** vì API đơn giản của nó, nhưng các khái niệm cũng áp dụng cho EPPlus, SpreadsheetGear, hoặc thậm chí Google Sheets qua API của nó.

---

## Yêu Cầu Trước

- .NET 6.0 hoặc mới hơn (mã sẽ biên dịch trên .NET Core và .NET Framework).  
- Tham chiếu tới **ClosedXML** (`dotnet add package ClosedXML`).  
- Kiến thức cơ bản về C# – bạn nên quen với các câu lệnh `using` và khởi tạo đối tượng.

Nếu bạn đã có một workbook mở, bạn có thể bỏ qua phần tạo tệp và chuyển thẳng tới phần công thức.

---

## Bước 1: Thiết Lập Worksheet (Cách Tạo Cột)

Đầu tiên chúng ta cần một đối tượng `Worksheet` để làm việc. Trong ClosedXML bạn lấy nó từ một `XLWorkbook`. Đoạn mã dưới đây tạo một workbook mới, thêm một sheet có tên *Demo*, và lấy một tham chiếu tên `worksheet` để dễ hiểu.

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // Create a fresh workbook and add a worksheet named "Demo"
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");

            // Rename for clarity – this is the worksheet we’ll manipulate
            var worksheet = ws;   // <-- same object, just a clearer name

            // --------------------------------------------------------------
            // Next step: write the WRAPCOLS formula
            // --------------------------------------------------------------
```

> **Tại sao đổi tên?**  
> Giữ tên biến ngắn (`worksheet`) làm cho mã sau này dễ đọc hơn, đặc biệt khi bạn chuỗi nhiều thao tác. Nó cũng phản ánh phong cách đặt tên mà bạn sẽ thấy trong hầu hết tài liệu, giảm tải nhận thức.

---

## Bước 2: Viết Công Thức (Cách Thêm Công Thức + Tạo Mảng Chuỗi)

Bây giờ là dòng mã ma thuật. Chúng ta sẽ đặt một công thức vào ô **A1** thực hiện hai việc:

1. **Tạo một mảng chuỗi** gồm sáu số (`SEQUENCE(6)` → 1,2,3,4,5,6).  
2. **Gói các số đó thành hai cột** (`WRAPCOLS(..., 2)`).

```csharp
            // Write the WRAPCOLS formula into A1
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // --------------------------------------------------------------
            // Finally, force the engine to evaluate the formula
            // --------------------------------------------------------------
```

> **Điều gì đang xảy ra?**  
> `SEQUENCE(6)` tạo một mảng dọc `{1;2;3;4;5;6}`. `WRAPCOLS` sau đó lấy mảng đó và “gói” nó thành số cột đã chỉ định — trong trường hợp này là **2**. Kết quả là một khối 3‑hàng × 2‑cột trông như sau:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

Nếu bạn thay đổi đối số thứ hai thành **3**, bạn sẽ có một bố cục ba cột thay vì hai. Đó là cốt lõi của **cách tạo cột** một cách động mà không cần vòng lặp thủ công.

---

## Bước 3: Tính Lại Worksheet (Đảm Bảo Công Thức Được Đánh Giá)

ClosedXML sẽ không tự động tính toán công thức khi bạn viết chúng. Bạn cần gọi `Calculate()` trên workbook (hoặc trên worksheet cụ thể) để buộc đánh giá.

```csharp
            // Recalculate so the formula is evaluated immediately
            worksheet.Calculate();

            // Optional: save the workbook to inspect the result
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

> **Mẹo chuyên nghiệp:** Nếu bạn làm việc với các workbook lớn, chỉ gọi `Calculate()` trên các sheet thực sự đã thay đổi. Điều này tiết kiệm bộ nhớ và tăng tốc xử lý.

Khi bạn mở `WrapColsDemo.xlsx` bạn sẽ thấy bố cục hai cột được điền gọn gàng trong **A1:B3**. Không cần mã bổ sung để lặp qua các hàng hoặc cột – `WRAPCOLS` đã xử lý mọi thứ.

---

## Bước 4: Xác Nhận Kết Quả (Điều Gì Mong Đợi)

Sau khi chạy chương trình, mở tệp đã tạo. Bạn sẽ thấy:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

Nếu các số xuất hiện theo chiều dọc (tức là tất cả trong cột A), hãy kiểm tra lại rằng bạn đã gọi `worksheet.Calculate()` **sau** khi đặt công thức. Một số engine cũng cần `workbook.Calculate()`; đoạn mã trên hoạt động với bộ đánh giá tích hợp của ClosedXML.

---

## Các Biến Thể Thông Thường & Trường Hợp Đặc Biệt

### Thay Đổi Số Cột

Để **tạo bố cục hai cột** với số hàng khác, chỉ cần điều chỉnh kích thước `SEQUENCE` hoặc đối số thứ hai của `WRAPCOLS`:

```csharp
worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(12), 3)";
```

Điều này tạo ra một khối 4‑hàng × 3‑cột (12 số được chia thành ba cột).

### Sử Dụng Số Cột Động

Nếu số cột của bạn đến từ một biến, chèn nó bằng string interpolation:

```csharp
int colCount = 4;
worksheet.Cell("A1").FormulaA1 = $"=WRAPCOLS(SEQUENCE(8), {colCount})";
```

Bây giờ bạn đã **cách thêm công thức** có thể thích nghi tại thời gian chạy.

### Worksheet Trống

Nếu worksheet trống, `Calculate()` vẫn hoạt động – công thức sẽ điền các ô bắt đầu từ A1. Tuy nhiên, nếu bạn sau đó xóa các hàng/cột giao nhau với vùng đầu ra, bạn có thể thấy lỗi `#REF!`. Để tránh điều này, hãy xóa vùng mục tiêu trước:

```csharp
worksheet.Range("A1:Z100").Clear(); // wipes any leftovers
```

### Tính Tương Thích

`WRAPCOLS` và `SEQUENCE` là một phần của các hàm **Dynamic Array** của Excel, được giới thiệu trong Office 365. Nếu bạn nhắm tới các phiên bản Excel cũ hơn, các hàm này sẽ không tồn tại và bạn sẽ cần một vòng lặp thủ công. Bộ đánh giá của ClosedXML mô phỏng hành vi mới nhất của Excel, vì vậy nó an toàn cho môi trường hiện đại.

---

## Ví Dụ Hoàn Chỉnh (Sẵn Sàng Sao Chép‑Dán)

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook & worksheet
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");
            var worksheet = ws;   // clearer name

            // 2️⃣ Write WRAPCOLS formula that generates a sequence array
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // 3️⃣ Force calculation so the formula resolves immediately
            worksheet.Calculate();

            // 4️⃣ Save the file (optional, but handy for verification)
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

**Kết quả mong đợi:** Mở *WrapColsDemo.xlsx* sẽ hiển thị một bố cục hai cột gọn gàng với các số 1‑6 được sắp xếp như đã mô tả ở trên.

## Kết Luận

Chúng tôi đã trình bày **cách sử dụng WRAPCOLS** để **tạo bố cục hai cột**, minh họa **cách thêm công thức** một cách lập trình, và thấy cách `SEQUENCE` cho phép bạn **tạo mảng chuỗi** mà không cần vòng lặp. Bằng cách tận dụng các hàm dynamic array của Excel từ C#, bạn có thể giữ mã ngắn gọn, dễ đọc và dễ bảo trì.

Tiếp theo, bạn có thể khám phá:

- **Tạo số hàng động** với `ROWS` hoặc `COUNTA`.  
- **Định dạng đầu ra** (đường viền, định dạng số) bằng API styling của ClosedXML.  
- **Xuất ra CSV** sau khi bố cục được xây dựng, cho các quy trình xử lý tiếp theo.

Hãy thử ngay, điều chỉnh số cột, và xem bạn có thể tạo mẫu nhanh chóng các bảng tính phức tạp như thế nào. Chúc lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}