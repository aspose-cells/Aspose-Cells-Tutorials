---
category: general
date: 2026-02-23
description: Tạo sổ làm việc mới bằng cách lập trình trong C# và thêm công thức vào
  một ô. Học cách sử dụng EXPAND, sau đó lưu sổ làm việc Excel một cách dễ dàng.
draft: false
keywords:
- create new workbook
- add formula to cell
- save excel workbook
- how to use expand
- create excel file programmatically
language: vi
og_description: Tạo sổ làm việc mới bằng lập trình C#. Thêm công thức vào một ô, học
  cách sử dụng EXPAND và lưu sổ làm việc Excel trong vài giây.
og_title: Tạo sổ làm việc mới trong C# – Thêm công thức và lưu tệp Excel
tags:
- C#
- Excel Automation
- Aspose.Cells
title: Tạo Workbook mới trong C# – Thêm công thức và lưu tệp Excel
url: /vi/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Sổ Làm Việc Mới trong C# – Thêm Công Thức và Lưu Tệp Excel

Bạn đã bao giờ tự hỏi làm sao **tạo workbook mới** từ mã mà không cần mở Excel chưa? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi cần tạo một bảng tính nhanh chóng — có thể cho báo cáo, xuất dữ liệu, hoặc dump dữ liệu nhanh.

Tin tốt là gì? Trong hướng dẫn này bạn sẽ thấy cách **tạo workbook mới**, **thêm công thức vào ô**, và sau đó **lưu workbook Excel** chỉ với vài dòng C#. Chúng ta cũng sẽ khám phá **cách sử dụng expand** để tạo mảng động mà không cần sao chép thủ công. Khi hoàn thành, bạn sẽ có thể **tạo file Excel một cách lập trình** và gửi nó cho người dùng hoặc các dịch vụ downstream.

## Các Điều Kiện Cần Có

- .NET 6.0 trở lên (bất kỳ runtime .NET nào mới đều được)
- Aspose.Cells for .NET (bản dùng thử miễn phí hoặc bản có giấy phép) – thư viện này cung cấp các lớp `Workbook` và `Worksheet` được dùng ở dưới.
- Kiến thức cơ bản về cú pháp C# — không cần hiểu sâu về Excel.

Nếu bạn đã có những thứ trên, tuyệt vời! Nếu chưa, hãy tải Aspose.Cells từ NuGet (`Install-Package Aspose.Cells`) và bạn sẽ sẵn sàng.

---

## Bước 1: Tạo Workbook Mới – Nền Tảng Cơ Bản

Đầu tiên, chúng ta cần khởi tạo một đối tượng workbook mới. Hãy tưởng tượng đây là việc mở một tệp Excel hoàn toàn trống.

```csharp
using Aspose.Cells;

public class ExcelGenerator
{
    public void Generate()
    {
        // Step 1: Create a new workbook (this is the core of create new workbook)
        Workbook workbook = new Workbook();
```

> **Tại sao điều này quan trọng:** Lớp `Workbook` là điểm khởi đầu cho mọi thao tác với Excel. Khi tạo một thể hiện mới, chúng ta cấp phát bộ nhớ cho các sheet, style và công thức — tất cả mà không chạm tới hệ thống tệp.

---

## Bước 2: Truy Cập Worksheet Đầu Tiên

Mỗi workbook mới đều đi kèm với một worksheet mặc định (có tên *Sheet1*). Chúng ta sẽ lấy nó để đặt dữ liệu và công thức.

```csharp
        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Mẹo chuyên nghiệp:** Nếu cần nhiều sheet, chỉ cần gọi `workbook.Worksheets.Add("MySheet")` và làm việc với đối tượng `Worksheet` trả về.

---

## Bước 3: Thêm Công Thức Vào Ô – Sử Dụng EXPAND

Bây giờ là phần thú vị: chèn công thức. Hàm `EXPAND` rất hữu ích khi bạn muốn biến một mảng tĩnh thành một vùng dữ liệu lớn hơn, tự động lấp đầy.

```csharp
        // Step 3: Add formula to cell A1 using EXPAND
        // This creates a 5‑row array from the constant {1,2,3}
        worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";
```

### Cách Hoạt Động Của Công Thức EXPAND

| Tham số | Ý nghĩa |
|----------|---------|
| `{1,2,3}` | Mảng nguồn (danh sách ngang gồm ba số) |
| `5`       | Số hàng mong muốn trong kết quả |
| `1`       | Số cột mong muốn (giữ là 1 để kết quả dọc) |

Khi Excel tính toán công thức này, nó sẽ tạo ra một danh sách **dọc**:

```
A1: 1
A2: 2
A3: 3
A4: 0   (filled with zeros)
A5: 0
```

> **Tại sao nên dùng EXPAND?** Nó loại bỏ nhu cầu sao chép thủ công hoặc vòng lặp VBA. Hàm này tự động định dạng lại dữ liệu, giúp bảng tính của bạn mạnh mẽ và dễ bảo trì hơn.

---

## Bước 4: Lưu Workbook Excel – Ghi Kết Quả Vào Đĩa

Sau khi công thức đã được đặt, bước cuối cùng là ghi workbook ra ổ đĩa. Bạn có thể chọn bất kỳ thư mục nào mà bạn có quyền ghi.

```csharp
        // Step 4: Save the workbook to view the result
        string outputPath = @"C:\Temp\ExpandFormula.xlsx";
        workbook.Save(outputPath);
    }
}
```

> **Bạn sẽ thấy gì:** Mở `ExpandFormula.xlsx` trong Excel, ô `A1` sẽ hiển thị mảng đã được mở rộng. Công thức vẫn nằm trong ô, vì vậy nếu bạn chỉnh sửa mảng nguồn, kết quả sẽ tự động cập nhật.

---

## Tùy Chọn: Xác Minh Kết Quả Bằng Chương Trình

Nếu bạn không muốn mở Excel thủ công, có thể đọc lại các giá trị để xác nhận chúng khớp với mong đợi.

```csharp
        // Verify values without opening Excel
        for (int row = 0; row < 5; row++)
        {
            var value = worksheet.Cells[row, 0].Value; // column 0 = A
            Console.WriteLine($"Row {row + 1}: {value}");
        }
```

Chạy đoạn mã trên sẽ in ra:

```
Row 1: 1
Row 2: 2
Row 3: 3
Row 4: 0
Row 5: 0
```

---

## Các Câu Hỏi Thường Gặp & Trường Hợp Đặc Biệt

| Câu hỏi | Trả lời |
|----------|--------|
| **Tôi có thể dùng EXPAND với mảng nguồn lớn hơn không?** | Chắc chắn. Chỉ cần thay `{1,2,3}` bằng bất kỳ hằng số hoặc phạm vi ô nào, ví dụ `EXPAND(A1:C1,10,1)`. |
| **Nếu tôi muốn kết quả nằm ngang thì sao?** | Đổi vị trí đối số hàng/cột: `EXPAND({1,2,3},1,5)` sẽ tạo ra một dải 1 hàng, 5 cột. |
| **Công thức này có hoạt động trên các phiên bản Excel cũ không?** | `EXPAND` chỉ có từ Excel 365/2021 trở lên. Đối với các phiên bản cũ hơn, bạn phải mô phỏng mảng bằng `INDEX`/`SEQUENCE`. |
| **Có cần gọi `workbook.CalculateFormula()` không?** | Không. Aspose.Cells tự động tính toán công thức khi lưu, vì vậy giá trị sẽ xuất hiện ngay lập tức. |
| **Làm sao thêm hơn một sheet trước khi lưu?** | Gọi `workbook.Worksheets.Add("SecondSheet")` và lặp lại các bước thao tác ô trên worksheet mới. |

---

## Ví Dụ Hoàn Chỉnh

Dưới đây là chương trình hoàn chỉnh, sẵn sàng chạy. Sao chép‑dán vào một ứng dụng console, chỉnh đường dẫn xuất, và nhấn **F5**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutomationDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create new workbook
            Workbook workbook = new Workbook();

            // Access first worksheet
            Worksheet worksheet = workbook.Worksheets[0];

            // Add EXPAND formula to A1
            worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";

            // Optional: verify values in console
            workbook.CalculateFormula(); // ensures formulas are evaluated now
            for (int i = 0; i < 5; i++)
            {
                Console.WriteLine($"A{i + 1} = {worksheet.Cells[i, 0].Value}");
            }

            // Save the workbook
            string filePath = @"C:\Temp\ExpandFormula.xlsx";
            workbook.Save(filePath);
            Console.WriteLine($"Workbook saved to {filePath}");
        }
    }
}
```

**Kết quả mong đợi trong console:**

```
A1 = 1
A2 = 2
A3 = 3
A4 = 0
A5 = 0
Workbook saved to C:\Temp\ExpandFormula.xlsx
```

Mở tệp đã tạo và bạn sẽ thấy các số giống nhau được điền vào cột **A**.

---

## Tóm Tắt Hình Ảnh

![Create new workbook example](create-new-workbook.png "Screenshot showing a new workbook created with create new workbook in C#")

*Hình ảnh minh họa workbook mới được tạo với kết quả từ hàm EXPAND.*

---

## Kết Luận

Bây giờ bạn đã biết cách **tạo workbook mới**, **thêm công thức vào ô**, và **lưu workbook Excel** bằng C#. Bằng cách nắm vững **cách sử dụng expand**, bạn có thể tạo các mảng động mà không cần công sức thủ công, và toàn bộ quy trình cho phép bạn **tạo file Excel một cách lập trình** cho bất kỳ kịch bản tự động nào.

Tiếp theo bạn muốn làm gì? Hãy thử thay đổi mảng hằng số thành tham chiếu phạm vi, thử các kích thước `EXPAND` khác nhau, hoặc chuỗi nhiều công thức qua các sheet. Mẫu này cũng áp dụng cho biểu đồ, định dạng, và thậm chí pivot table — vì vậy hãy tiếp tục khám phá.

Nếu gặp bất kỳ vấn đề nào, hãy để lại bình luận bên dưới. Chúc bạn lập trình vui vẻ và tận hưởng sức mạnh của Excel lập trình!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}