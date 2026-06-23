---
category: general
date: 2026-03-22
description: Tìm hiểu cách định dạng datetime sang ISO khi trích xuất ngày từ Excel
  và hiển thị ngày ISO bằng Aspose.Cells trong C#.
draft: false
keywords:
- format datetime to iso
- extract date from excel
- display iso date
- Aspose.Cells date parsing
- Japanese era dates
language: vi
og_description: Định dạng ngày giờ sang ISO trở nên dễ dàng. Hướng dẫn này chỉ cách
  trích xuất ngày từ Excel và hiển thị ngày ở định dạng ISO bằng Aspose.Cells.
og_title: Định dạng datetime sang ISO trong C# – Hướng dẫn từng bước
tags:
- C#
- Aspose.Cells
- DateTime
- Excel
- ISO 8601
title: Định dạng datetime sang ISO trong C# – Hướng dẫn đầy đủ
url: /vi/net/number-and-display-formats-in-excel/format-datetime-to-iso-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Định dạng datetime sang iso trong C# – Hướng dẫn đầy đủ

Bạn đã bao giờ cần **định dạng datetime sang iso** nhưng nguồn dữ liệu lại nằm trong một workbook Excel? Có thể ô chứa một niên đại Nhật Bản như “令和3年5月1日” và bạn đang bối rối không biết làm sao chuyển nó thành chuỗi sạch `2021‑05‑01`. Bạn không phải là người duy nhất. Trong hướng dẫn này, chúng tôi sẽ **trích xuất ngày từ excel**, phân tích niên đại Nhật Bản, và sau đó **hiển thị ngày iso** trên console—tất cả chỉ với vài dòng C# và Aspose.Cells.

Chúng tôi sẽ hướng dẫn từng bước những gì bạn cần: gói NuGet bắt buộc, đoạn mã chính xác bạn có thể sao chép‑dán, lý do mỗi dòng quan trọng, và một vài mẹo cho các trường hợp đặc biệt. Khi kết thúc, bạn sẽ có một đoạn mã có thể tái sử dụng để định dạng datetime sang iso bất kể giá trị Excel gốc có kỳ quặc thế nào.

## Những gì bạn cần

- .NET 6.0 trở lên (mã cũng biên dịch được trên .NET Framework 4.6+)
- Visual Studio 2022 (hoặc bất kỳ trình soạn thảo nào bạn thích)
- **Aspose.Cells for .NET** gói NuGet – `Install-Package Aspose.Cells`
- Một tệp Excel (hoặc một workbook mới) chứa ngày ở định dạng niên đại Nhật Bản

Chỉ vậy thôi. Không cần thư viện bổ sung, không COM interop, chỉ một phương thức duy nhất, được tài liệu hoá đầy đủ.

## Bước 1: Tạo Workbook và Ghi ngày theo Niên đại Nhật Bản  

Đầu tiên, chúng ta cần một workbook để làm việc. Nếu bạn đã có tệp Excel, bạn có thể tải nó bằng `new Workbook("path")`. Trong ví dụ này, chúng ta sẽ tạo một workbook mới trong bộ nhớ và đưa chuỗi niên đại Nhật Bản vào ô **A1**.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date (Reiwa 3 = 2021) into A1
        sheet.Cells["A1"].PutValue("令和3年5月1日");
```

> **Lý do chúng ta làm như vậy:** Aspose.Cells xử lý giá trị ô dưới dạng chuỗi theo mặc định. Bằng cách chèn văn bản niên đại thô, chúng ta mô phỏng một kịch bản thực tế nơi khách hàng Nhật Bản nhập ngày theo lịch bản địa của họ.

## Bước 2: Bật phân tích Niên đại Nhật Bản và Trích xuất Ngày  

Aspose.Cells có thể tự động chuyển đổi chuỗi niên đại Nhật Bản thành đối tượng .NET `DateTime`—miễn là bạn bật tính năng này. Cờ `DateTimeParseOptions.EnableJapaneseEra` thực hiện công việc nặng.

```csharp
        // 3️⃣ Retrieve the cell value while enabling Japanese era parsing
        CellValue parsed = sheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

> **Mẹo chuyên nghiệp:** Nếu bạn quên tùy chọn `EnableJapaneseEra`, thư viện sẽ trả về chuỗi gốc và việc chuyển đổi tiếp theo sẽ thất bại. Luôn kiểm tra `parsed.Type` nếu bạn đang xử lý nội dung hỗn hợp.

## Bước 3: Chuyển DateTime đã phân tích sang ISO 8601  

Bây giờ chúng ta đã có một `DateTime` hợp lệ, việc chuyển nó thành chuỗi định dạng ISO rất đơn giản. Mẫu `"yyyy-MM-dd"` tuân theo phần ngày của ISO 8601, đó là định dạng hầu hết các API mong đợi.

```csharp
        // 4️⃣ Convert to ISO 8601 (yyyy‑MM‑dd) and display it
        string isoDate = parsed.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

Chạy chương trình sẽ in ra:

```
ISO date: 2021-05-01
```

Đó là **ngày iso hiển thị** mà bạn đang muốn.

## Ví dụ đầy đủ, có thể chạy  

Dưới đây là khối mã hoàn chỉnh bạn có thể sao chép trực tiếp vào dự án console. Không có phụ thuộc ẩn, không cần cấu hình thêm.

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

        // Write a Japanese era date into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // Retrieve the cell value with Japanese era parsing enabled
        CellValue parsedValue = worksheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);

        // Convert the DateTime to ISO 8601 format and output it
        string isoDate = parsedValue.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

> **Kết quả mong đợi:** `ISO date: 2021-05-01`

## Phân tích từng bước (Tại sao mỗi phần quan trọng)

| Bước | Điều gì xảy ra | Tại sao quan trọng |
|------|----------------|--------------------|
| **Create workbook** | Khởi tạo một container Excel trong bộ nhớ. | Cung cấp môi trường sandbox để thử nghiệm mà không cần chạm tới hệ thống tệp. |
| **PutValue** | Lưu chuỗi niên đại Nhật Bản thô vào **A1**. | Mô phỏng việc nhập dữ liệu thực tế; đảm bảo bộ phân tích thấy đúng văn bản. |
| **GetValue with `EnableJapaneseEra`** | Chuyển đổi chuỗi niên đại thành .NET `DateTime`. | Tự động xử lý chuyển đổi lịch—không cần bảng tra cứu thủ công. |
| **`ToString("yyyy-MM-dd")`** | Định dạng `DateTime` thành ISO 8601. | Đảm bảo chuỗi ngày không phụ thuộc vào ngôn ngữ, có thể sắp xếp và được chấp nhận bởi REST API, cơ sở dữ liệu, v.v. |
| **Console.WriteLine** | Hiển thị ngày ISO cuối cùng. | Xác nhận toàn bộ quy trình hoạt động từ đầu tới cuối. |

## Xử lý các biến thể phổ biến  

### 1. Vị trí ô khác  

Nếu ngày của bạn nằm ở **B2** hoặc một phạm vi có tên, chỉ cần thay `"A1"` bằng địa chỉ phù hợp:

```csharp
worksheet.Cells["B2"].PutValue("令和2年12月31日");
var value = worksheet.Cells["B2"]
    .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

### 2. Nhiều ngày trong một cột  

Khi bạn cần **trích xuất ngày từ excel** cho nhiều hàng, lặp qua phạm vi đã sử dụng:

```csharp
int lastRow = worksheet.Cells.MaxDataRow;
for (int i = 0; i <= lastRow; i++)
{
    var cell = worksheet.Cells[i, 0]; // column A
    var cv = cell.GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
    string iso = cv.DateTimeValue.ToString("yyyy-MM-dd");
    Console.WriteLine($"Row {i + 1}: {iso}");
}
```

### 3. Phương án dự phòng cho ngày không phải niên đại  

Nếu một ô đã chứa chuỗi ngày chuẩn, bộ phân tích vẫn hoạt động, nhưng bạn có thể muốn một biện pháp an toàn:

```csharp
CellValue cv = cell.GetValue(CellValueType.DateTime,
    DateTimeParseOptions.EnableJapaneseEra | DateTimeParseOptions.TryParse);
```

Cờ `TryParse` ngăn lỗi ngoại lệ và trả về giá trị gốc nếu chuyển đổi thất bại.

### 4. Thành phần thời gian  

Nếu bạn cũng cần phần thời gian, sử dụng `"yyyy-MM-ddTHH:mm:ss"`:

```csharp
string isoDateTime = parsedValue.DateTimeValue.ToString("yyyy-MM-ddTHH:mm:ss");
```

Điều này tạo ra một dấu thời gian ISO 8601 đầy đủ (`2021-05-01T00:00:00`).

## Hình ảnh minh họa  

![ví dụ định dạng datetime sang iso](image.png "Một ví dụ về định dạng datetime sang iso trong C#")

*Văn bản thay thế:* *ví dụ định dạng datetime sang iso hiển thị đầu ra console*

## Câu hỏi thường gặp  

- **Tôi có thể sử dụng điều này với tệp .xls không?**  
  Có. Aspose.Cells hỗ trợ `.xls`, `.xlsx`, `.csv`, và nhiều định dạng khác ngay từ đầu.  

- **Nếu workbook được bảo vệ bằng mật khẩu thì sao?**  
  Tải nó bằng `new Workbook("file.xlsx", new LoadOptions { Password = "secret" })`.  

- **Định dạng ISO có phụ thuộc vào ngôn ngữ không?**  
  Không. Mẫu `"yyyy-MM-dd"` không phụ thuộc vào ngôn ngữ, đảm bảo cùng một chuỗi trên mọi máy.  

- **Điều này có hoạt động trên .NET Core không?**  
  Hoàn toàn—Aspose.Cells tuân thủ .NET Standard 2.0.  

## Kết luận  

Chúng tôi đã trình bày cách **định dạng datetime sang iso** bằng cách **trích xuất ngày từ excel**, phân tích chuỗi niên đại Nhật Bản, và cuối cùng **hiển thị ngày iso** trên console. Các bước cốt lõi—tạo workbook, ghi hoặc tải văn bản niên đại, bật phân tích niên đại Nhật Bản, và định dạng với `ToString("yyyy-MM-dd")`—là tất cả những gì bạn cần cho hầu hết các trường hợp.

Tiếp theo, bạn có thể muốn:

- Ghi lại các ngày ISO vào một cột khác để xử lý tiếp theo.  
- Xuất workbook đã chuyển đổi sang CSV để nhập hàng loạt.  
- Kết hợp logic này với một web API nhận tải lên Excel và trả về ngày ISO được mã hoá JSON.  

Bạn có thể thoải mái thử nghiệm với các định dạng ngày khác nhau, múi giờ, hoặc thậm chí lịch tùy chỉnh. Tính linh hoạt của Aspose.Cells có nghĩa là bạn hiếm khi gặp phải rào cản.

Chúc lập trình vui vẻ, và mong mọi ngày của bạn đều tuân thủ chuẩn ISO một cách hoàn hảo!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}