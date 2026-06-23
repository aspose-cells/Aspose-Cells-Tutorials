---
category: general
date: 2026-03-18
description: Tạo sổ làm việc mới và xuất Excel sang TXT trong khi giữ độ chính xác
  số. Tìm hiểu cách lưu trang tính dưới dạng txt và chuyển đổi trang tính sang txt
  một cách hiệu quả.
draft: false
keywords:
- create new workbook
- export excel to txt
- save excel as txt
- save worksheet as txt
- convert worksheet to txt
language: vi
og_description: Tạo sổ làm việc mới và xuất Excel sang TXT một cách chính xác. Hướng
  dẫn này chỉ cách lưu worksheet dưới dạng txt và chuyển đổi worksheet sang txt bằng
  C#.
og_title: Tạo sổ làm việc mới – Hướng dẫn xuất Excel sang TXT
tags:
- Aspose.Cells
- C#
- Excel automation
title: Tạo sổ làm việc mới – Xuất Excel sang TXT với độ chính xác đầy đủ
url: /vi/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo workbook mới – Xuất Excel sang TXT với Độ chính xác đầy đủ

Bạn đã bao giờ cần **create new workbook** trong C# chỉ để ghi một số dữ liệu vào tệp văn bản thuần? Có thể bạn đang lấy báo cáo từ hệ thống cũ và công cụ downstream chỉ chấp nhận nguồn dữ liệu `.txt`. Tin tốt là gì? Bạn không cần phải hy sinh độ chính xác số, và chắc chắn không cần tự tạo chuỗi CSV.

Trong hướng dẫn này, chúng tôi sẽ đi qua toàn bộ quy trình **export excel to txt**, bao gồm mọi thứ từ khởi tạo workbook đến việc giữ lại các số 0 phía sau khi bạn **save worksheet as txt**. Khi kết thúc, bạn sẽ có một đoạn mã sẵn sàng chạy mà có thể chèn vào bất kỳ dự án .NET nào—không cần công cụ bổ sung.

## Những gì bạn cần

- **ASP.NET/ .NET 6+** (mã hoạt động trên .NET Framework 4.6+ cũng được)  
- **Aspose.Cells for .NET** – thư viện cung cấp các lớp `Workbook`, `Worksheet`, và `TxtSaveOptions`. Bạn có thể tải nó từ NuGet bằng `Install-Package Aspose.Cells`.  
- Kiến thức cơ bản về C# (nếu bạn đã quen với các câu lệnh `using`, bạn đã sẵn sàng).  

Chỉ vậy—không cần Excel interop, không có đối tượng COM, và chắc chắn không cần ghép chuỗi thủ công.  

---

## Bước 1: Khởi tạo Workbook mới (Từ khóa chính)

Điều đầu tiên bạn phải làm là **create new workbook**. Hãy nghĩ workbook như một canvas trống mà sau này bạn sẽ dán các số, văn bản hoặc công thức.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();                 // <‑‑ creates new workbook
            Worksheet worksheet = workbook.Worksheets[0];       // first sheet (index 0)
```

> **Tại sao điều này quan trọng:** Khởi tạo `Workbook` mà không tải tệp sẽ cho bạn một trang trắng. Bạn có thể sau đó thêm dữ liệu bằng chương trình, điều này hoàn hảo cho các trường hợp **convert worksheet to txt** khi bạn không có tệp `.xlsx` hiện có.

## Bước 2: Điền dữ liệu vào các ô – Giữ lại các số 0 phía sau

Một sai lầm phổ biến khi ghi số vào văn bản là mất các số 0 phía sau (`123.45000` trở thành `123.45`). Nếu các hệ thống downstream dựa vào các trường có độ rộng cố định, việc mất này có thể gây lỗi toàn bộ.

```csharp
            // Step 2: Write a numeric value that contains trailing zeros
            // PutValue respects the data type; we’ll later tell the saver to keep precision.
            worksheet.Cells[0, 0].PutValue(123.45000);
```

> **Mẹo chuyên nghiệp:** `PutValue` tự động suy ra kiểu dữ liệu. Nếu bạn cần một chuỗi trông giống số, hãy dùng `PutValue("123.45000")` thay thế.

## Bước 3: Cấu hình tùy chọn lưu TXT – Bảo tồn độ chính xác số

Đây là nơi phép thuật diễn ra. Bằng cách bật `PreserveNumericPrecision`, bạn chỉ định cho Aspose.Cells ghi giá trị chính xác mà bạn nhập, bao gồm cả các số 0 không quan trọng phía sau.

```csharp
            // Step 3: Configure TXT save options to keep the original numeric precision
            TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                PreserveNumericPrecision = true   // retain all digits, even trailing zeros
            };
```

> **Tại sao bật tùy chọn này?** Khi bạn **save excel as txt**, hành vi mặc định sẽ cắt bỏ các chữ số thập phân không cần thiết. Đặt `PreserveNumericPrecision = true` đảm bảo đầu ra phản ánh giá trị hiển thị của ô, điều này quan trọng đối với báo cáo tài chính hoặc dữ liệu khoa học.

## Bước 4: Lưu Worksheet dưới dạng TXT – Xuất cuối cùng

Bây giờ chúng ta thực sự **save worksheet as txt**. Bạn có thể chỉ định đường dẫn bất kỳ nơi nào bạn có quyền ghi; ví dụ sử dụng thư mục tương đối có tên `output`.

```csharp
            // Step 4: Save the worksheet as a TXT file using the configured options
            string outputPath = "output/num-preserve.txt";
            worksheet.Save(outputPath, txtSaveOptions);

            Console.WriteLine($"File saved to {outputPath}");
        }
    }
}
```

> **Kết quả mong đợi** (`num-preserve.txt`):

```
123.45000
```

Chú ý các số 0 phía sau vẫn giữ nguyên—đúng như yêu cầu của bạn.

## Bước 5: Xác minh kết quả – Kiểm tra nhanh

Sau khi chương trình chạy, mở `num-preserve.txt` bằng bất kỳ trình soạn thảo văn bản nào. Bạn sẽ thấy dòng duy nhất `123.45000`. Nếu bạn thấy `123.45` thay vào đó, hãy kiểm tra lại rằng `PreserveNumericPrecision` đã được đặt thành `true` và bạn đang sử dụng phiên bản mới của Aspose.Cells (v23.10+).

## Các biến thể thường gặp & Trường hợp đặc biệt

### Xuất nhiều ô hoặc phạm vi

Nếu bạn cần **export excel to txt** cho toàn bộ một phạm vi, chỉ cần điền thêm các ô trước khi lưu:

```csharp
worksheet.Cells["A1"].PutValue(100);
worksheet.Cells["A2"].PutValue(200.500);
worksheet.Cells["A3"].PutValue(300.00);
```

Mặc định, Aspose sẽ ghi mỗi ô trên một dòng mới. Bạn cũng có thể thay đổi ký tự phân tách (tab, dấu phẩy) qua `txtSaveOptions.Separator`.

### Chuyển Worksheet sang TXT với các mã hoá khác nhau

Đôi khi các hệ thống downstream yêu cầu UTF‑8 BOM hoặc ASCII. Điều chỉnh mã hoá như sau:

```csharp
txtSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

### Xử lý Workbook lớn

Khi làm việc với các sheet khổng lồ (hàng trăm ngàn), hãy cân nhắc truyền dữ liệu đầu ra theo luồng:

```csharp
txtSaveOptions.EnableCache = true; // writes data in chunks to reduce memory footprint
```

## Mẹo chuyên nghiệp & Những lưu ý

- **Đừng quên tạo thư mục output** trước khi gọi `Save`, nếu không bạn sẽ nhận được `DirectoryNotFoundException`.  
- **Cẩn thận với dấu phân cách thập phân theo locale**. Nếu môi trường của bạn dùng dấu phẩy (`1,23`), đặt `txtSaveOptions.DecimalSeparator = '.'` để buộc sử dụng dấu chấm.  
- **Tương thích phiên bản**: Cờ `PreserveNumericPrecision` được giới thiệu trong Aspose.Cells 20.6. Nếu bạn đang dùng phiên bản cũ hơn, cờ này sẽ không tồn tại và bạn cần định dạng ô thành văn bản trước khi lưu.

![Ví dụ tạo workbook mới](excel-to-txt.png "Tạo workbook mới")

*Văn bản thay thế hình ảnh: "Tạo workbook mới và xuất Excel sang TXT với độ chính xác số được bảo tồn"*

## Tóm tắt – Những gì chúng ta đã đề cập

- **Create new workbook** sử dụng Aspose.Cells.  
- Điền một ô với số có chứa các số 0 phía sau.  
- Đặt `TxtSaveOptions.PreserveNumericPrecision = true` để **save excel as txt** mà không mất độ chính xác.  
- Ghi tệp ra đĩa, xác minh đầu ra khớp với giá trị gốc.  

Đó là toàn bộ quy trình **convert worksheet to txt** trong dưới 50 dòng C#.

## Các bước tiếp theo & Chủ đề liên quan

Bây giờ bạn có thể **export excel to txt** với độ chính xác hoàn hảo, bạn có thể muốn khám phá:

- **Exporting to CSV** với các dấu phân tách tùy chỉnh (`TxtSaveOptions.Separator`).  
- **Saving as other plain‑text formats** như TSV (`SaveFormat.TabDelimited`).  
- **Batch processing** nhiều workbook trong một thư mục bằng `Directory.GetFiles`.  
- **Integrating with Azure Functions** để chuyển đổi theo yêu cầu trên đám mây.  

Mỗi mục đều dựa trên mẫu `Workbook` → `Worksheet` → `TxtSaveOptions` giống nhau, vì vậy bạn sẽ cảm thấy quen thuộc.

### Suy nghĩ cuối cùng

Nếu bạn đã theo dõi, bây giờ bạn biết chính xác cách **create new workbook**, điền dữ liệu và **save worksheet as txt** trong khi giữ lại mọi chữ số thập phân mà bạn quan tâm. Đó là một đoạn mã ngắn, nhưng nó giải quyết một vấn đề thường gặp khi các pipeline cũ yêu cầu đầu vào dạng văn bản thuần.

Hãy thử nghiệm, điều chỉnh các tùy chọn, và để dữ liệu chảy đúng như bạn mong muốn. Chúc lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}