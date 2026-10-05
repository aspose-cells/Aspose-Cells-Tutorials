---
category: general
date: 2026-02-15
description: Tạo sổ làm việc Excel mới và học cách sử dụng EXPAND, mở rộng một dãy
  và tính cotang. Ngoài ra, xem cách lưu sổ làm việc vào tệp.
draft: false
keywords:
- create new excel workbook
- save workbook to file
- how to use expand
- how to expand sequence
- how to calculate cotangent
language: vi
og_description: Tạo sổ làm việc Excel mới bằng C#. Tìm hiểu cách sử dụng EXPAND, mở
  rộng một dãy, tính cotang và lưu sổ làm việc vào tệp.
og_title: Tạo sổ làm việc Excel mới trong C# – Hướng dẫn lập trình toàn diện
tags:
- C#
- Aspose.Cells
- Excel automation
title: Tạo sổ làm việc Excel mới trong C# – Hướng dẫn chi tiết từng bước
url: /vi/net/excel-workbook/create-new-excel-workbook-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo mới workbook Excel trong C# – Hướng dẫn lập trình đầy đủ

Bạn đã bao giờ cần **create new Excel workbook** từ mã và không chắc bắt đầu từ đâu chưa? Bạn không cô đơn; nhiều nhà phát triển gặp khó khăn này khi tự động hoá báo cáo hoặc xây dựng các pipeline dữ liệu. Trong hướng dẫn này, chúng tôi sẽ chỉ cho bạn cách tạo mới workbook Excel, viết một vài công thức thú vị, và sau đó **save workbook to file** để kiểm tra sau.  

Chúng tôi cũng sẽ đi sâu vào chi tiết của hàm `EXPAND`, trình bày **how to use expand** để biến một dãy nhỏ thành một khối lớn, giải thích **how to expand sequence** trong thực tế, và cuối cùng tiết lộ **how to calculate cotangent** trực tiếp trong Excel. Khi kết thúc, bạn sẽ có một chương trình C# có thể chạy được mà bạn có thể đưa vào bất kỳ dự án .NET nào.

## Những gì bạn cần

- **Aspose.Cells for .NET** (bản dùng thử miễn phí hoặc phiên bản có giấy phép) – thư viện cho phép chúng ta thao tác Excel mà không cần cài Office.  
- **.NET 6+** (hoặc .NET Framework 4.6+).  
- Một IDE vừa phải như Visual Studio 2022, VS Code, hoặc Rider.  

Không cần thêm bất kỳ gói NuGet nào ngoài `Aspose.Cells`. Nếu bạn chưa có, chạy:

```bash
dotnet add package Aspose.Cells
```

Xong rồi—không cần cài đặt gì thêm.

## Bước 1: Tạo mới workbook Excel

Điều đầu tiên chúng ta làm là khởi tạo một đối tượng `Workbook`. Hãy nghĩ nó như một canvas trống nơi tất cả các sheet, ô và công thức sẽ tồn tại.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];    // default sheet is named "Sheet1"
```

> **Tại sao điều này quan trọng:** Tạo workbook trong bộ nhớ có nghĩa là chúng ta không chạm vào đĩa cho đến khi chúng ta quyết định **save workbook to file** một cách rõ ràng. Điều này giữ cho thao tác nhanh và cho phép bạn thực hiện các sửa đổi tiếp theo mà không tốn chi phí I/O.

## Bước 2: Cách sử dụng EXPAND để mở rộng một dãy

`EXPAND` là một hàm Excel mới cho phép lấy một mảng nhỏ hơn và kéo dài nó đến kích thước xác định. Trong ví dụ của chúng tôi, chúng tôi bắt đầu với một dãy dọc ba hàng và biến nó thành khối 5 × 5.

```csharp
        // Step 2: Write a formula that expands a 3‑row sequence into a 5×5 block
        // The formula lives in A1 and will spill over to E5
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3),5,5)";
```

> **Giải thích:** `SEQUENCE(3)` tạo ra `{1;2;3}` (một mảng dọc). `EXPAND(...,5,5)` yêu cầu Excel lặp lại mảng đó cho đến khi lấp đầy một hình chữ nhật 5 hàng x 5 cột, bắt đầu tại A1. Kết quả là một ma trận mà mỗi cột lặp lại ba số gốc, và hai hàng cuối cùng để trống vì nguồn chỉ có ba hàng.

### Kết quả mong đợi

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 1 | 1 | 1 | 1 |
| 2 | 2 | 2 | 2 | 2 |
| 3 | 3 | 3 | 3 | 3 |
|   |   |   |   |   |
|   |   |   |   |   |

Bạn sẽ thấy cùng một mẫu lan ra toàn bộ vùng khi workbook được mở trong Excel.

## Bước 3: Cách tính cotangent trong Excel

Hầu hết mọi người đều quen thuộc với `SIN`, `COS`, và `TAN`, nhưng `COT` là một phím tắt tiện lợi cho nghịch đảo của tangent. Đây là cách lấy cotangent của 45° (bằng 1) bằng radian.

```csharp
        // Step 3: Write a formula that returns the cotangent of 45° (π/4 radians)
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";
```

> **Tại sao dùng COT?** Gọi trực tiếp `COT` tránh phép chia thêm mà bạn cần với `1/TAN(...)`, làm cho công thức rõ ràng hơn và hơi nhanh hơn cho các sheet lớn.

## Bước 4: Đánh giá tất cả công thức

Aspose.Cells không tự động tính toán công thức trừ khi bạn chỉ định. Phương thức `CalculateFormula` buộc thực hiện đánh giá đầy đủ để các giá trị kết quả được lưu trong các ô.

```csharp
        // Step 4: Evaluate all formulas so the results are stored in the cells
        workbook.CalculateFormula();
```

> **Mẹo:** Nếu bạn có nhiều công thức tốn kém, bạn có thể truyền một đối tượng `CalculationOptions` để tinh chỉnh hiệu năng (ví dụ, bật đa luồng).

## Bước 5: Lưu workbook vào tệp

Bây giờ mọi thứ đã sẵn sàng, cuối cùng chúng ta **save workbook to file**. Chọn một thư mục bạn có quyền ghi, và đặt tên tệp có ý nghĩa.

```csharp
        // Step 5: Save the workbook to a file for inspection
        string outputPath = @"C:\Temp\output.xlsx";
        workbook.Save(outputPath);
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

> **Điều gì xảy ra trên đĩa?** Lệnh `Save` ghi một gói `.xlsx` hoàn chỉnh, bao gồm cả mảng đã mở rộng từ `EXPAND` và giá trị cotangent đã tính. Mở tệp trong Excel và bạn sẽ thấy khối 5 × 5 bắt đầu tại A1 và số `1` ở B1.

![Kết quả Excel hiển thị dãy mở rộng và giá trị cotangent](excel-output.png "ví dụ đầu ra tạo mới workbook Excel")

*Văn bản thay thế hình ảnh: ví dụ đầu ra tạo mới workbook Excel*

### Kiểm tra nhanh

1. Mở `output.xlsx`.  
2. Kiểm tra rằng các ô **A1:E5** chứa mẫu 1‑2‑3 lặp lại.  
3. Nhìn vào **B1** – nó nên hiển thị `1`.  

Nếu mọi thứ khớp, chúc mừng—bạn đã tự động hoá Excel thành công!

## Cách mở rộng dãy trong các kịch bản khác

Mặc dù ví dụ trên sử dụng `SEQUENCE(3)` tĩnh, bạn có thể dễ dàng thay thế nó bằng một phạm vi động hoặc công thức khác:

```csharp
// Expand a dynamic range from D1:D10 to a 4×4 block
worksheet.Cells["F1"].Formula = "=EXPAND(D1:D10,4,4)";
```

**Khi nào nên dùng?**  
- Tạo bảng placeholder cho các mẫu.  
- Nhanh chóng sao chép một hàng tiêu đề qua nhiều cột.  
- Xây dựng lưới heat‑map mà không cần sao chép‑dán thủ công.

## Những cạm bẫy thường gặp và cách tránh

| Cạm bẫy | Tại sao xảy ra | Cách khắc phục |
|---------|----------------|----------------|
| `#VALUE!` after `EXPAND` | Mảng nguồn không phải là một phạm vi hợp lệ (ví dụ, chứa lỗi) | Làm sạch dữ liệu nguồn hoặc bọc nó trong `IFERROR`. |
| Cotangent returns `#DIV/0!` for 0° | `COT(0)` về mặt toán học là vô hạn | Bảo vệ bằng `IF(PI()/4=0,0,COT(...))`. |
| Workbook not saved | Đường dẫn không hợp lệ hoặc thiếu quyền ghi | Sử dụng `Path.GetFullPath` và xác minh thư mục tồn tại. |
| Formulas not calculated | `CalculateFormula` bị bỏ qua | Luôn gọi nó trước `Save`. |

## Bonus: Thêm kiểu dáng (tùy chọn)

Nếu bạn muốn kết quả trông đẹp hơn, bạn có thể áp dụng một kiểu đơn giản sau khi tính toán:

```csharp
        // Apply a light gray background to the expanded block
        Style style = workbook.CreateStyle();
        style.Pattern = BackgroundType.Solid;
        style.ForegroundColor = System.Drawing.Color.LightGray;
        StyleFlag flag = new StyleFlag { CellShading = true };
        worksheet.Cells.CreateRange("A1:E5").ApplyStyle(style, flag);
```

Đoạn mã này là tùy chọn, nhưng nó minh họa cách bạn có thể kết hợp logic **create new Excel workbook** với định dạng trong một lần thực thi.

## Tóm tắt

Chúng tôi đã đi qua toàn bộ quy trình:

1. **Create new Excel workbook** với Aspose.Cells.  
2. Sử dụng **how to use expand** để biến một `SEQUENCE` nhỏ thành ma trận 5 × 5.  
3. Hiển thị **how to calculate cotangent** trực tiếp trong một ô.  
4. Buộc tính toán bằng `CalculateFormula`.  
5. **Save workbook to file** và xác minh kết quả.

Tất cả những điều này đều tự chứa, chạy trên bất kỳ môi trường .NET hiện đại nào, và chỉ yêu cầu một gói NuGet.

## Tiếp theo là gì?

- **Dynamic data sources:** Lấy dữ liệu từ cơ sở dữ liệu và đưa vào `EXPAND`.  
- **Multiple worksheets:** Lặp qua một tập hợp các sheet để tạo một cuốn báo cáo đầy đủ.  
- **Advanced formulas:** Khám phá `LET`, `LAMBDA`, hoặc logic điều kiện dựa trên mảng cho các bảng tính thông minh hơn.  

Hãy thoải mái thử nghiệm—đổi đối số `SEQUENCE`, thử các góc độ khác cho `COT`, hoặc kết hợp tạo biểu đồ. Không giới hạn gì khi bạn có thể **create new Excel workbook** một cách lập trình.

---

*Chúc lập trình vui! Nếu bạn gặp bất kỳ khó khăn nào, hãy để lại bình luận bên dưới hoặc nhắn tin cho tôi trên Twitter @YourHandle. Tôi sẽ rất sẵn lòng giúp đỡ.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}