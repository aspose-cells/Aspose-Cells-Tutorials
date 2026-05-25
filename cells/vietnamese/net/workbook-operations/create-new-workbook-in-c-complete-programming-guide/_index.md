---
category: general
date: 2026-03-25
description: Tạo workbook mới trong C# và học cách sử dụng EXPAND, tính cotang, và
  lưu workbook vào tệp với mã từng bước.
draft: false
keywords:
- create new workbook
- save workbook to file
- how to use expand
- how to calculate cotangent
- how to save excel
language: vi
og_description: Tạo sổ làm việc mới trong C# và ngay lập tức xem cách sử dụng EXPAND,
  tính cotang và lưu sổ làm việc vào tệp.
og_title: Tạo workbook mới trong C# – Hướng dẫn lập trình toàn diện
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Tạo sổ làm việc mới trong C# – Hướng dẫn lập trình toàn diện
url: /vi/net/workbook-operations/create-new-workbook-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo workbook mới trong C# – Hướng dẫn lập trình đầy đủ

Bạn đã bao giờ cần **tạo workbook mới** trong C# nhưng không biết bắt đầu từ đâu chưa? Bạn không phải là người duy nhất. Dù bạn đang tự động hoá quy trình báo cáo hay chỉ đang thử nghiệm các công thức Excel trong mã, khả năng khởi tạo một workbook, chèn các công thức như `EXPAND` hoặc `COT`, và sau đó **lưu workbook vào tệp** là một kỹ năng cốt lõi cho bất kỳ nhà phát triển .NET nào.

Trong tutorial này chúng ta sẽ đi qua một ví dụ thực tế thực hiện đúng những việc trên: chúng ta sẽ khởi tạo một workbook mới, sử dụng hàm `EXPAND` để biến một mảng tĩnh thành cột động, tính cotangent bằng hàm `COT`, và cuối cùng **lưu workbook vào tệp** dưới dạng `.xlsx`. Khi kết thúc, bạn sẽ có một đoạn mã sẵn sàng chạy, hiểu *tại sao* mỗi lời gọi lại quan trọng, và thấy một vài biến thể hữu ích cho các trường hợp đặc biệt.

> **Pro tip:** Tất cả mã dưới đây hoạt động với phiên bản mới nhất của Aspose.Cells cho .NET (tính đến tháng 3 2026). Nếu bạn đang dùng phiên bản cũ hơn, giao diện API về cơ bản vẫn giống, nhưng hãy kiểm tra lại các import namespace.

## Những gì bạn cần

- .NET 6.0 hoặc mới hơn (mẫu này nhắm tới .NET 6, nhưng .NET 5 cũng hoạt động)  
- Aspose.Cells cho .NET được cài đặt qua NuGet (`Install-Package Aspose.Cells`)  
- Kiến thức cơ bản về C# (bạn đã có rồi)  

Đó là tất cả—không cần DLL bổ sung, không cần COM interop, và chắc chắn không cần cài đặt Excel trên máy. Sẵn sàng chưa? Hãy bắt đầu.

![Screenshot showing how to create new workbook in C#](assets/create-new-workbook.png){alt="Screenshot showing how to create new workbook in C#"}

## Bước 1: Tạo một workbook mới

Điều đầu tiên bạn phải làm là khởi tạo lớp `Workbook`. Hãy nghĩ nó như việc mở một tệp Excel trống trong bộ nhớ. Đối tượng này chứa một bộ sưu tập các worksheet, style, và mọi thứ khác mà bạn sẽ cần sau này.

```csharp
using Aspose.Cells;

class ExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();               // <-- creates an empty .xlsx structure
        Worksheet ws = workbook.Worksheets[0];            // default sheet is named "Sheet1"
```

Tại sao lại lấy ngay worksheet đầu tiên? Hầu hết các ví dụ nhanh đều làm việc với một sheet duy nhất, và accessor `Worksheets[0]` là cách nhanh nhất để lấy tham chiếu mà không cần vòng lặp. Nếu bạn cần nhiều sheet sau này, bạn có thể thêm chúng bằng `workbook.Worksheets.Add()`.

## Bước 2: Cách sử dụng EXPAND để tạo các dải động

`EXPAND` là một hàm Excel mới hơn, nhận một mảng và mở rộng nó tới kích thước chỉ định. Trong mã của chúng ta, chúng ta sẽ mở rộng mảng literal `{1,2,3}` thành **cột 5 hàng** bắt đầu tại ô `A1`. Cú pháp trong chuỗi chính xác như bạn sẽ gõ vào Excel, vì vậy bạn có thể sao chép‑dán trực tiếp vào ô sau này nếu muốn.

```csharp
        // Step 2: Apply EXPAND to turn {1,2,3} into a 5‑row vertical range
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)"; // rows=5, cols=1
```

### Điều gì đang diễn ra bên trong?

- `{1,2,3}` là một mảng literal theo chiều ngang.  
- Tham số thứ hai (`5`) yêu cầu Excel mở rộng mảng thành **5 hàng**.  
- Tham số thứ ba (`1`) buộc đầu ra thành **một cột** duy nhất.  

Nếu bạn bỏ qua tham số thứ ba, Excel sẽ cố gắng giữ nguyên hình dạng gốc, có thể cho bạn một khối 5×3 thay vì một cột đơn. Đó là một bẫy thường gặp khi bạn mới thử `EXPAND`.

#### Các biến thể bạn có thể cần

| Hình dạng mong muốn | Ví dụ công thức |
|---------------------|-----------------|
| khối 3 hàng, 2 cột | `=EXPAND({1,2,3},3,2)` |
| chỉ kéo xuống (cùng cột) | `=EXPAND({10,20},10,1)` |
| mở rộng tới số cột lớn hơn | `=EXPAND({5},5,4)` |

Bạn có thể tự do thay đổi các literal hoặc kích thước để phù hợp với logic tạo dữ liệu của mình.

## Bước 3: Cách tính cotangent bằng hàm COT

Hàm `COT` trả về cotangent của một góc được biểu diễn bằng radian. Trong ví dụ của chúng ta, chúng ta tính cotangent của 45° (π/4 radian). Kết quả, `1`, sẽ xuất hiện ở ô `B1`.

```csharp
        // Step 3: Use COT to calculate cotangent of 45 degrees (π/4 radians)
        ws.Cells["B1"].Formula = "=COT(PI()/4)"; // PI() returns π, divided by 4 = 45°
```

### Tại sao dùng COT thay vì tính toán thủ công?

Excel đã biết cách xử lý chuyển đổi lượng giác, vì vậy bạn tránh được lỗi làm tròn số thực có thể xuất hiện nếu bạn thử `1 / TAN(angle)`. Thêm nữa, công thức vẫn dễ đọc cho bất kỳ ai xem lại bảng tính sau này.

#### Trường hợp đặc biệt: góc vượt quá 0‑360°

Nếu bạn đưa vào một góc lớn hơn `2*PI()` (hoặc một góc âm), Excel sẽ tự động vòng lại, nhưng kết quả có thể gây bất ngờ. Để an toàn, bạn có thể chuẩn hoá góc trước:

```csharp
        // Normalize angle to 0‑2π range before applying COT
        ws.Cells["C1"].Formula = "=COT(MOD(PI()*3, 2*PI()))";
```

Đoạn mã này minh họa cách kết hợp `MOD` với `COT` để có các phép tính chắc chắn.

## Bước 4: Cách lưu workbook vào tệp (Excel)

Bây giờ các công thức đã sẵn sàng, bước cuối cùng là **lưu workbook vào tệp**. Bạn có thể chọn bất kỳ đường dẫn nào bạn muốn—chỉ cần đảm bảo thư mục tồn tại và bạn có quyền ghi.

```csharp
        // Step 4 (optional): Save the workbook so you can inspect the results
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "output.xlsx");

        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Thực tế lưu gì?

Khi bạn mở `output.xlsx` trong Excel, bạn sẽ thấy:

| A | B |
|---|---|
| 1 | 1 |
| 2 |   |
| 3 |   |
|   |   |
|   |   |

- Cột **A** chứa mảng đã mở rộng `{1,2,3}` tiếp theo là hai ô trống (vì chúng ta yêu cầu 5 hàng).  
- Ô **B1** hiển thị `1`, cotangent của 45°.  

Nếu bạn làm mới workbook (nhấn `F9` hoặc bật tính toán tự động), Excel sẽ đánh giá các công thức và hiển thị kết quả. Aspose.Cells cũng cung cấp phương thức `CalculateFormula` nếu bạn cần giá trị mà không mở Excel:

```csharp
        workbook.CalculateFormula();
        double cotResult = ws.Cells["B1"].DoubleValue; // should be 1.0
```

## Câu hỏi thường gặp & Những lưu ý

| Question | Answer |
|----------|--------|
| **Do I need to enable calculation manually?** | No. By default Aspose.Cells saves formulas as‑is; Excel will compute them on open. Use `workbook.CalculateFormula()` for pre‑calculation. |
| **Can I write formulas to multiple cells at once?** | Absolutely. Use `ws.Cells["D1:D5"].Formula = "=RAND()"` to fill a range with random numbers. |
| **What if my target folder doesn’t exist?** | Create it first: `Directory.CreateDirectory(Path.GetDirectoryName(outputPath));` |
| **Is `EXPAND` supported in older Excel versions?** | `EXPAND` arrived with Excel 365/2019. If you need compatibility with older files, consider using `INDEX`/`SEQUENCE` combos instead. |
| **How do I hide the formula view?** | Set `ws.Cells["A1"].FormulaHidden = true;` and protect the sheet if you don’t want users to see the underlying formula. |

## Tổng kết

Bạn giờ đã biết **cách tạo workbook mới** trong C#, tận dụng sức mạnh của hàm `EXPAND` để tạo mảng động, tính cotangent bằng `COT`, và **lưu workbook vào tệp** dưới dạng một tài liệu Excel gọn gàng. Ví dụ đầy đủ, có thể chạy được nằm trong các đoạn mã ở trên—sao chép vào một console app, nhấn `F5`, và mở `output.xlsx` để thấy kết quả.

### Tiếp theo là gì?

- **Khám phá các hàm mảng động khác** như `SEQUENCE`, `FILTER`, và `SORT`.  
- **Tự động tạo biểu đồ** với API biểu đồ phong phú của Aspose.Cells.  
- **Kết nối với các nguồn dữ liệu** (SQL, CSV) và đưa các giá trị đó vào công thức một cách lập trình.  
- **Học cách lưu Excel dưới dạng PDF** hoặc các định dạng khác—hoàn hảo cho các pipeline báo cáo.

Hãy thoải mái thử nghiệm: thay đổi giá trị mảng, điều chỉnh góc, hoặc ghi kết quả vào một sheet khác. Khi bạn kết hợp C# với engine công thức hiện đại của Excel, khả năng chỉ có trời mới giới hạn.

Chúc lập trình vui vẻ, và mong bảng tính của bạn luôn tính toán chính xác!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}