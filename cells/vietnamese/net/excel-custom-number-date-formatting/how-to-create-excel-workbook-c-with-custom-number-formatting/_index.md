---
category: general
date: 2026-10-01
description: Tìm hiểu cách tạo workbook Excel bằng C#, áp dụng định dạng số tùy chỉnh,
  thiết lập số thập phân cho ô và lưu workbook dưới dạng XLSX trong hướng dẫn chi
  tiết từng bước.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- apply custom number format
- how to format numbers excel
- set cell decimal places
- save workbook as xlsx
language: vi
lastmod: 2026-10-01
og_description: Tạo workbook Excel bằng C# với định dạng số tùy chỉnh, thiết lập số
  chữ số thập phân cho ô, và lưu workbook dưới dạng XLSX. Tham khảo hướng dẫn đầy
  đủ này để có đầu ra số chính xác.
og_image_alt: Screenshot of an Excel sheet showing numbers rounded to four significant
  digits
og_title: Tạo workbook Excel bằng C# – định dạng số tùy chỉnh & xuất XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  headline: How to create Excel workbook C# with custom number formatting
  type: TechArticle
- description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  name: How to create Excel workbook C# with custom number formatting
  steps:
  - name: Run the program (`dotnet run`).
    text: Run the program (`dotnet run`).
  - name: Open `SigDigits.xlsx`.
    text: Open `SigDigits.xlsx`.
  - name: Confirm that **A1** reads `123.5`.
    text: Confirm that **A1** reads `123.5`.
  - name: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
    text: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Cách tạo workbook Excel bằng C# với định dạng số tùy chỉnh
url: /vi/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-c-with-custom-number-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách tạo workbook Excel bằng C# với định dạng số tùy chỉnh

Nếu bạn cần **tạo workbook Excel bằng C#** mà hiển thị số chính xác như mong muốn, hướng dẫn này sẽ chỉ cho bạn cách thực hiện trong vài bước rõ ràng. Bạn sẽ học cách áp dụng định dạng số tùy chỉnh, thiết lập số chữ số thập phân cho ô, và cuối cùng **lưu workbook dưới dạng xlsx** để sử dụng tiếp.

Làm việc với dữ liệu số thường đòi hỏi cân bằng giữa độ chính xác và khả năng đọc. Khi kết thúc tutorial này, bạn sẽ có một mẫu có thể tái sử dụng để giới hạn số chữ số hiển thị theo một số lượng chữ số có nghĩa nhất định, đồng thời giữ nguyên giá trị gốc trong tệp. Không cần script bên ngoài—chỉ cần C# và thư viện Aspose.Cells.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* .NET 6.0 SDK hoặc phiên bản mới hơn đã được cài đặt  
* Visual Studio 2022 (hoặc bất kỳ IDE C# nào)  
* Gói NuGet **Aspose.Cells for .NET** (`Install-Package Aspose.Cells`) – thư viện này cung cấp các lớp `Workbook`, `Worksheet` và `ExportTableOptions` được sử dụng trong các ví dụ.  

Các yêu cầu này là tối thiểu; cùng một đoạn mã hoạt động trên .NET Core, .NET Framework và thậm chí trong Azure Functions.

## Bước 1: Tạo workbook Excel C# – khởi tạo tệp

Hoạt động đầu tiên là khởi tạo một đối tượng `Workbook` mới. Đối tượng này đại diện cho toàn bộ tệp Excel trong bộ nhớ và tự động chứa một worksheet mặc định.

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();               // creates an empty .xlsx container
            Worksheet sheet = workbook.Worksheets[0];         // reference to the default sheet
```

**Tại sao điều này quan trọng:**  
Việc tạo workbook ngay từ đầu giúp bạn có một canvas sạch sẽ. Worksheet mặc định (`Worksheets[0]`) đã sẵn sàng để nhập dữ liệu, vì vậy bạn không cần phải thêm sheet mới trừ khi kịch bản của bạn yêu cầu nhiều tab.

## Bước 2: Ghi một giá trị số vào ô

Bây giờ đặt một số mẫu vào ô **A1**. Giá trị chúng ta dùng (`123.456789`) có nhiều chữ số thập phân hơn so với số chúng ta muốn hiển thị cuối cùng, giúp chúng ta minh họa việc làm tròn sau này.

```csharp
            // Step 2: Write a numeric value to cell A1
            sheet.Cells[0, 0].PutValue(123.456789); // row 0, column 0 = A1
```

**Mẹo:** `PutValue` tự động phát hiện kiểu dữ liệu, vì vậy bạn không cần phải chuyển số sang chuỗi.

## Bước 3: Áp dụng định dạng số tùy chỉnh – giới hạn số thập phân hiển thị

Để kiểm soát cách Excel hiển thị số, chúng ta tạo một `Style` với **định dạng số tùy chỉnh**. Mẫu `"0.######"` chỉ ra cho Excel hiển thị tối đa sáu chữ số thập phân nhưng bỏ qua các số 0 thừa ở cuối.

```csharp
            // Step 3: Define a custom number format (up to 6 decimal places) and apply it
            Style customStyle = workbook.CreateStyle();
            customStyle.Custom = "0.######";               // up to 6 decimals, no trailing zeros
            sheet.Cells[0, 0].SetStyle(customStyle);
```

**Cách hoạt động:**  
Chuỗi định dạng tuân theo cú pháp định dạng tùy chỉnh của Excel. `0` buộc phải có một chữ số, trong khi `#` chỉ hiển thị chữ số nếu nó có ý nghĩa. Khi kết hợp chúng, bạn có được một cách hiển thị linh hoạt nhưng vẫn giữ nguyên độ chính xác gốc.

## Bước 4: Thiết lập số chữ số thập phân cho ô – sử dụng ExportTableOptions

Nếu bạn cần **thiết lập số chữ số thập phân cho ô** khi xuất dữ liệu (ví dụ, khi chuyển đổi sang DataTable), Aspose.Cells cho phép bạn chỉ định số **chữ số có nghĩa**. Bước này đảm bảo CSV hoặc DataTable được xuất ra tuân theo cùng quy tắc làm tròn mà bạn đã áp dụng trong workbook.

```csharp
            // Step 4: Configure export options to limit the output to 4 significant digits
            ExportTableOptions exportOptions = new ExportTableOptions();
            exportOptions.SignificantDigits = 4;           // round to 4 significant figures
```

**Tại sao sử dụng `SignificantDigits`?**  
Khác với việc cố định số chữ số thập phân, chữ số có nghĩa giữ nguyên quy mô của số trong khi giới hạn độ chính xác, điều mà các nhà phân tích thường mong đợi khi tóm tắt dữ liệu.

## Bước 5: Xuất dữ liệu worksheet và **lưu workbook dưới dạng xlsx**

Cuối cùng, xuất dữ liệu (nếu bạn cần một DataTable) và lưu workbook vào đĩa. Lệnh `ExportDataTable` tuân theo `ExportTableOptions` mà chúng ta đã cấu hình, và `workbook.Save` ghi ra một tệp XLSX tiêu chuẩn.

```csharp
            // Step 5: Export the worksheet data using the configured options and save the workbook
            sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
            workbook.Save("SigDigits.xlsx");               // saves to the application’s working folder
        }
    }
}
```

**Kết quả mong đợi:**  
Khi bạn mở *SigDigits.xlsx* trong Excel, ô **A1** hiển thị `123.5`. Giá trị gốc vẫn là `123.456789`, nhưng số hiển thị tuân theo quy tắc 4 chữ số có nghĩa. Nếu bạn xuất sheet sang DataTable, giá trị trong bảng cũng sẽ được làm tròn thành `123.5`.

---

## Áp dụng định dạng số tùy chỉnh cho các ô bổ sung

Nếu bạn cần định dạng một phạm vi thay vì một ô duy nhất, hãy tái sử dụng đối tượng `Style`:

```csharp
// Apply the same custom style to B2:C5
Range range = sheet.Cells.CreateRange("B2:C5");
range.ApplyStyle(customStyle, new StyleFlag { NumberFormat = true });
```

**Pro tip:** Việc tái sử dụng một đối tượng style giảm tải bộ nhớ và đảm bảo định dạng nhất quán trên toàn sheet.

## Cách định dạng số trong Excel bằng C# – các biến thể phổ biến

| Tình huống | Chuỗi định dạng | Kết quả |
|-----------|----------------|--------|
| Hai chữ số thập phân cố định | `"0.00"` | `123.46` |
| Tiền tệ (Mỹ) | `"$#,##0.00"` | `$123.46` |
| Phần trăm với một chữ số thập phân | `"0.0%"` | `12,346.0%` |
| Ký hiệu khoa học | `"0.00E+00"` | `1.23E+02` |

Chọn mẫu phù hợp với yêu cầu báo cáo của bạn. Tất cả các mẫu đều tương thích với thuộc tính `Style.Custom` đã được trình bày ở trên.

## Thiết lập số chữ số thập phân cho ô một cách động dựa trên đầu vào của người dùng

Đôi khi độ chính xác cần thiết không được biết trước khi biên dịch. Bạn có thể xây dựng chuỗi định dạng tại thời gian chạy:

```csharp
int decimals = 3; // could come from a UI textbox
string format = "0." + new string('#', decimals);
customStyle.Custom = format;
sheet.Cells["A2"].PutValue(987.654321);
sheet.Cells["A2"].SetStyle(customStyle);
```

**Trường hợp đặc biệt:** Nếu `decimals` bằng không, định dạng sẽ trở thành `"0"` (hiển thị nguyên). Luôn xác thực đầu vào của người dùng để tránh chuỗi định dạng sai cấu trúc.

## Lưu workbook dưới dạng XLSX – các thực hành tốt nhất

* **Sử dụng đường dẫn tuyệt đối** khi ghi vào một thư mục đã biết (`Path.Combine(Environment.CurrentDirectory, "output.xlsx")`).  
* **Giải phóng** đối tượng `Workbook` nếu bạn bọc nó trong câu lệnh `using` để giải phóng tài nguyên không quản lý kịp thời:

```csharp
using (Workbook wb = new Workbook())
{
    // ...populate workbook...
    wb.Save(Path.Combine(@"C:\Exports", "Report.xlsx"));
}
```

* **Tương thích phiên bản:** Aspose.Cells ghi các tệp tương thích với Excel 2010‑2023, vì vậy người dùng downstream sẽ không gặp vấn đề về định dạng.

---

## Ví dụ hoàn chỉnh hoạt động

Dưới đây là chương trình đầy đủ mà bạn có thể sao chép, dán và chạy ngay lập tức. Nó bao gồm tất cả các chỉ thị `using` cần thiết, chú thích và xử lý lỗi.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // 1️⃣ Create workbook and get the first worksheet
                Workbook workbook = new Workbook();
                Worksheet sheet = workbook.Worksheets[0];

                // 2️⃣ Write a high‑precision number to A1
                sheet.Cells[0, 0].PutValue(123.456789);

                // 3️⃣ Apply a custom number format (up to 6 decimals)
                Style customStyle = workbook.CreateStyle();
                customStyle.Custom = "0.######";
                sheet.Cells[0, 0].SetStyle(customStyle);

                // 4️⃣ Configure export options for 4 significant digits
                ExportTableOptions exportOptions = new ExportTableOptions
                {
                    SignificantDigits = 4
                };

                // 5️⃣ Export data (optional) and save the workbook as XLSX
                sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
                string outputPath = Path.Combine(Environment.CurrentDirectory, "SigDigits.xlsx");
                workbook.Save(outputPath);

                Console.WriteLine($"Workbook saved successfully at: {outputPath}");
                Console.WriteLine("Cell A1 displays: " + sheet.Cells["A1"].StringValue);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error creating workbook: {ex.Message}");
            }
        }
    }
}
```

**Các bước xác minh**

1. Chạy chương trình (`dotnet run`).  
2. Mở `SigDigits.xlsx`.  
3. Xác nhận rằng **A1** hiển thị `123.5`.  
4. Nếu bạn mở XML của tệp (`.xlsx` là một archive zip), bạn sẽ thấy định dạng tùy chỉnh `"0.######"` được lưu trong thuộc tính `s` của phần tử `<c>`.

---

## Kết luận

Trong tutorial này, bạn đã học cách **tạo workbook Excel bằng C#**, **áp dụng định dạng số tùy chỉnh**, **thiết lập số chữ số thập phân cho ô**, và **lưu workbook dưới dạng xlsx** bằng Aspose.Cells. Giải pháp này minh họa cả việc định dạng trực quan trong Excel và làm tròn khi xuất dữ liệu qua `ExportTableOptions`.  

Từ đây, bạn có thể:

* Mở rộng cách tiếp cận cho toàn bộ phạm vi hoặc bảng.  
* Kết hợp nhiều style (phông chữ, viền) với `StyleFlag`.  
* Tự động tạo báo cáo bằng cách lặp qua các nguồn dữ liệu và áp dụng cùng một logic định dạng.  

Hãy thoải mái thử nghiệm các chuỗi định dạng, số chữ số thập phân hoặc tùy chọn xuất khác nhau để phù hợp với nhu cầu báo cáo cụ thể của bạn. Chúc bạn lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Create Excel Workbook C# – Step‑by‑Step Guide with Conditional Formatting](/cells/english/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/)
- [Create Excel Workbook C# – Add Comment & Save as XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}