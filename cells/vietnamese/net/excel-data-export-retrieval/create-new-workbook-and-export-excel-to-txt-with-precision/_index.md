---
category: general
date: 2026-02-15
description: Tạo workbook mới và xuất Excel sang TXT đồng thời thiết lập độ chính
  xác số. Học cách đặt số chữ số có nghĩa và giới hạn số chữ số có nghĩa trong C#.
draft: false
keywords:
- create new workbook
- export excel to txt
- set significant digits
- limit significant digits
- set numeric precision
language: vi
og_description: Tạo sổ làm việc mới và xuất Excel sang TXT, đặt số chữ số có nghĩa
  cho độ chính xác số. Hướng dẫn C# từng bước.
og_title: Tạo Sổ làm việc mới – Xuất Excel sang TXT một cách chính xác
tags:
- C#
- Aspose.Cells
- Excel automation
title: Tạo sổ làm việc mới và xuất Excel sang TXT một cách chính xác
url: /vi/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Sổ Làm Việc Mới – Xuất Excel sang TXT với Định Dạng Số Chính Xác

Bạn đã bao giờ tự hỏi làm thế nào để **create new workbook** đối tượng trong C# và ngay lập tức ghi chúng ra một tệp văn bản thuần? Bạn không phải là người duy nhất. Trong nhiều kịch bản dữ liệu, chúng ta cần **export Excel to TXT** trong khi giữ cho các số dễ đọc, nghĩa là giới hạn số chữ số xuất hiện sau dấu thập phân.  

Trong hướng dẫn này, chúng ta sẽ đi qua toàn bộ quy trình: từ việc tạo một workbook mới, đến cấu hình việc xuất để nó **sets significant digits** (còn gọi là giới hạn chữ số có nghĩa), và cuối cùng ghi tệp ra đĩa. Khi kết thúc, bạn sẽ có một đoạn mã sẵn sàng chạy đáp ứng yêu cầu **numeric precision** của bạn—không cần thư viện bổ sung, không có phép màu.

> **Mẹo:** Nếu bạn đã sử dụng Aspose.Cells, các lớp được hiển thị bên dưới là một phần của thư viện đó. Nếu bạn đang trên nền tảng khác, các khái niệm vẫn áp dụng; chỉ cần thay đổi các lời gọi API.

---

## Những Gì Bạn Cần

- .NET 6+ (mã sẽ biên dịch trên .NET Core và .NET Framework đều được)  
- Aspose.Cells cho .NET (bản dùng thử miễn phí hoặc phiên bản có giấy phép) – cài đặt qua NuGet: `dotnet add package Aspose.Cells`  
- Bất kỳ IDE nào bạn thích (Visual Studio, Rider, VS Code)  

Chỉ vậy thôi. Không có tệp cấu hình bổ sung, không có bước ẩn nào.

---

## Bước 1: Tạo Một Workbook Mới

Điều đầu tiên là **create new workbook**. Hãy nghĩ lớp `Workbook` như một tệp Excel trống đang chờ các sheet, ô và dữ liệu.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate a fresh workbook – this is the core of create new workbook logic
        Workbook workbook = new Workbook();

        // (Optional) Add some sample data so you can see the effect of numeric precision later
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);
```

> **Tại sao điều này quan trọng:** Bằng cách bắt đầu với một workbook sạch sẽ, bạn tránh được bất kỳ định dạng ẩn nào có thể can thiệp vào cài đặt độ chính xác sau này.

---

## Bước 2: Cấu Hình Tùy Chọn Lưu Văn Bản – Đặt Significant Digits

Bây giờ chúng ta cho Aspose.Cells biết chúng ta muốn bao nhiêu **significant digits** khi ghi ra tệp `.txt`. Lớp `TxtSaveOptions` cung cấp thuộc tính `SignificantDigits` thực hiện đúng điều đó.

```csharp
        // Step 2: Prepare save options – limit numeric precision to 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            // This limits the output to 5 digits that matter, rounding the rest
            SignificantDigits = 5
        };
```

> **Giải thích:** `SignificantDigits = 5` có nghĩa là bộ xuất sẽ giữ lại năm chữ số quan trọng nhất của bất kỳ số nào, bất kể dấu thập phân nằm ở đâu. Đây là cách tiện lợi để **set numeric precision** mà không cần định dạng thủ công từng ô.

---

## Bước 3: Lưu Workbook dưới Dạng Tệp Văn Bản Thuần

Khi workbook và các tùy chọn đã sẵn sàng, cuối cùng chúng ta **export Excel to txt**. Phương thức `Save` nhận đường dẫn tệp và đối tượng tùy chọn mà chúng ta vừa cấu hình.

```csharp
        // Step 3: Write the workbook out as a TXT file using our precision settings
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        System.Console.WriteLine($"Workbook exported to {outputPath} with 5 significant digits.");
    }
}
```

Chạy chương trình sẽ tạo ra một tệp trông như sau:

```
12346
0.00012346
3.1416
```

Chú ý cách mỗi số tuân thủ quy tắc **limit significant digits** mà chúng ta đã đặt trước đó.

---

## Bước 4: Xác Minh Kết Quả (Tùy Chọn nhưng Được Khuyến Khích)

Bạn có thể dễ dàng mở `numbers.txt` đã tạo trong bất kỳ trình soạn thảo nào, nhưng có thể bạn muốn tự động hoá bước xác minh, đặc biệt trong các pipeline CI.

```csharp
        // Quick verification – read back the file and print each line
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            System.Console.WriteLine($"Line: {line}");
        }
```

Nếu console hiển thị ba dòng trên, bạn đã **set significant digits** thành công và việc xuất hoạt động như mong đợi.

---

## Những Cạm Bẫy Thường Gặp & Cách Tránh

| Vấn đề | Nguyên nhân | Cách khắc phục |
|-------|-------------|----------------|
| Số xuất hiện quá nhiều chữ số thập phân | `SignificantDigits` để ở mặc định (0) | Đặt rõ `SignificantDigits` thành số mong muốn |
| Tệp rỗng được tạo | Workbook chưa nhận dữ liệu nào trước khi lưu | Điền dữ liệu vào các ô **trước** khi gọi `Save` |
| Đường dẫn tệp gây ra `UnauthorizedAccessException` | Cố gắng ghi vào thư mục được bảo vệ | Sử dụng thư mục bạn có quyền ghi (ví dụ, `C:\Temp` hoặc `%USERPROFILE%\Documents`) |
| Độ chính xác có vẻ sai đối với các số rất nhỏ | Đếm significant digits bao gồm các số 0 đứng đầu sau dấu thập phân | Nhớ rằng “significant” bỏ qua các số 0 đầu; 0.000123456 với 5 chữ số sẽ thành `0.00012346` |

---

## Ví Dụ Hoàn Chỉnh (Sẵn Sàng Sao Chép‑Dán)

Dưới đây là chương trình hoàn chỉnh, tự chứa. Dán vào một dự án console mới và nhấn **Run**.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // Populate with sample numbers
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);

        // 2️⃣ Set up export options – limit significant digits to 5
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 5
        };

        // 3️⃣ Export to TXT
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        Console.WriteLine($"✅ Export completed: {outputPath}");
        Console.WriteLine("🔎 Verifying content:");
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            Console.WriteLine($"   {line}");
        }
    }
}
```

**Kết quả console dự kiến**

```
✅ Export completed: C:\Temp\numbers.txt
🔎 Verifying content:
   12346
   0.00012346
   3.1416
```

Và tệp `numbers.txt` sẽ chứa ba dòng như trên.

---

## Các Bước Tiếp Theo: Vượt Qua Những Kiến Thức Cơ Bản

- **Xuất các định dạng khác** – Aspose.Cells cũng hỗ trợ CSV, HTML và PDF. Thay `TxtSaveOptions` bằng `CsvSaveOptions` hoặc `PdfSaveOptions` tùy nhu cầu.  
- **Độ chính xác động** – bạn có thể tính `SignificantDigits` tại thời gian chạy dựa trên đầu vào của người dùng hoặc tệp cấu hình.  
- **Nhiều worksheet** – lặp qua `workbook.Worksheets` và xuất mỗi worksheet ra một tệp `.txt` riêng.  
- **Địa phương hoá** – kiểm soát dấu phân cách thập phân (`.` vs `,`) qua `CultureInfo` nếu bạn cần phù hợp với cài đặt khu vực.  

Tất cả các mở rộng này vẫn dựa trên ý tưởng cốt lõi chúng ta đã đề cập: **create new workbook**, cấu hình việc xuất, và **set numeric precision** để phù hợp với yêu cầu báo cáo của bạn.

---

## Tóm Tắt

Chúng ta đã tạo một thể hiện **create new workbook** mới, điền dữ liệu vào, và minh họa cách **export Excel to TXT** trong khi **setting significant digits** để giới hạn độ chính xác đầu ra. Ví dụ đầy đủ chạy ngay mà không cần cấu hình thêm, và phần giải thích đã đề cập *tại sao* mỗi dòng được viết để bạn có thể áp dụng vào dự án của mình.

Bạn cứ thoải mái thử nghiệm—thay đổi giá trị `SignificantDigits`, thêm nhiều sheet, hoặc đổi định dạng đầu ra. Nếu gặp khó khăn, hãy xem tài liệu Aspose.Cells hoặc để lại bình luận bên dưới. Chúc lập trình vui vẻ!

---

![Ví dụ tạo workbook mới](/images/create-new-workbook.png "Ảnh chụp màn hình IDE C# với mã tạo workbook mới")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}