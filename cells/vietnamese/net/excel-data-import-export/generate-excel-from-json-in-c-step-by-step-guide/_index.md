---
category: general
date: 2026-03-18
description: Học cách tạo Excel từ JSON bằng C#, cho phép trùng tên sheet, tạo sheet
  chi tiết và lưu workbook C# trong vài phút.
draft: false
keywords:
- generate excel from json
- allow duplicate sheet names
- how to create detail sheet
- save workbook c#
- smartmarker options
- aspnet cells integration
language: vi
og_description: Tạo file Excel từ JSON bằng C#. Hướng dẫn này chỉ cách cho phép tên
  sheet trùng lặp, tạo sheet chi tiết và lưu workbook bằng C# với Aspose.Cells.
og_title: Tạo Excel từ JSON trong C# – Hướng dẫn đầy đủ
tags:
- C#
- Excel automation
- JSON
- Aspose.Cells
title: Tạo Excel từ JSON trong C# – Hướng dẫn từng bước
url: /vi/net/excel-data-import-export/generate-excel-from-json-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Excel từ JSON trong C# – Hướng Dẫn Từng Bước

Bạn đã bao giờ cần **generate Excel from JSON** nhưng không chắc thư viện nào có thể xử lý công việc nặng? Bạn không phải là người duy nhất. Trong nhiều ứng dụng doanh nghiệp, chúng ta nhận payload dưới dạng JSON và phải đưa dữ liệu đó vào các bảng tính được định dạng đẹp mắt—như báo cáo bán hàng, dump tồn kho, hoặc log kiểm toán. Tin tốt là gì? Với engine SmartMarker của Aspose.Cells, bạn có thể biến một chuỗi JSON thành một file Excel hoàn chỉnh chỉ trong vài dòng code.

Trong tutorial này, chúng ta sẽ đi qua toàn bộ quy trình: từ chuẩn bị payload JSON, cấu hình SmartMarker để **cho phép trùng tên sheet**, tạo một **detail sheet**, và cuối cùng **lưu workbook theo kiểu C#**. Khi hoàn thành, bạn sẽ có một đoạn mã có thể tái sử dụng trong bất kỳ dự án .NET nào.

> **Tóm tắt nhanh:**  
> • Mục tiêu chính – generate Excel from JSON.  
> • Mục tiêu phụ – cho phép trùng tên sheet, tạo detail sheet, lưu workbook C#.  

## Prerequisites

Trước khi bắt đầu, hãy chắc chắn bạn đã có:

- .NET 6.0 SDK (hoặc bất kỳ phiên bản .NET gần đây nào).  
- Visual Studio 2022 hoặc VS Code với extension C#.  
- Một giấy phép hoạt động hoặc bản dùng thử miễn phí của **Aspose.Cells for .NET** (gói NuGet là `Aspose.Cells`).  
- Một file mẫu Excel (`template.xlsx`) đã chứa các thẻ SmartMarker như `&=Name` và một placeholder cho bảng chi tiết.

Nếu bất kỳ mục nào trên nghe lạ, đừng lo—cài đặt gói NuGet chỉ cần một lệnh, và mẫu có thể là một workbook đơn giản với vài ô placeholder.

## Overview of the Solution

Ở mức cao, chúng ta sẽ:

1. Định nghĩa một chuỗi JSON phản ánh dữ liệu chúng ta muốn trong sheet.  
2. Thiết lập `SmartMarkerOptions` để cho phép trùng tên sheet và một **detail sheet** có tên dự đoán được.  
3. Tải template Excel chứa các thẻ SmartMarker.  
4. Chạy bộ xử lý SmartMarker để hợp nhất dữ liệu JSON vào workbook.  
5. Lưu file cuối cùng bằng `workbook.Save(...)`.

Mỗi bước sẽ được giải thích dưới đây, kèm đầy đủ đoạn code và lý do tại sao bước đó quan trọng.

---

## Step 1 – Prepare the JSON payload you’ll merge

Điều đầu tiên bạn cần là một tài liệu JSON khớp với các thẻ SmartMarker trong template. Hãy nghĩ JSON như nguồn sự thật; mỗi key sẽ trở thành một placeholder trong file Excel.

```csharp
// Step 1: Define the JSON data that will be merged into the worksheet
string jsonData = @"{
    ""Name"": ""John"",
    ""Date"": ""2023-01-01"",
    ""Orders"": [
        { ""Item"": ""Laptop"", ""Qty"": 2, ""Price"": 1200 },
        { ""Item"": ""Mouse"",  ""Qty"": 5, ""Price"": 25 }
    ]
}";
```

**Tại sao điều này quan trọng:**  
SmartMarker đọc cấu trúc phân cấp của JSON và tự động mở rộng các bảng cho các collection như `Orders`. Nếu cấu trúc JSON của bạn không khớp với các thẻ, quá trình merge sẽ im lặng tạo ra các hàng trống—đó là một lỗi thường gặp.

---

## Step 2 – Configure SmartMarker to allow duplicate sheet names and name the detail sheet

Mặc định Aspose.Cells không cho phép trùng tên sheet, điều này có thể gây cản trở khi bạn tạo một detail sheet cho mỗi bản ghi master. Lớp `SmartMarkerOptions` cho phép bạn nới lỏng quy tắc này và cũng chỉ định mẫu đặt tên cho các detail sheet mới tạo.

```csharp
// Step 2: Create SmartMarker options and allow duplicate base names for detail sheets
var smartMarkerOptions = new Aspose.Cells.SmartMarker.SmartMarkerOptions
{
    // When a detail sheet is generated, it will be named "Detail", "Detail (2)", etc.
    DetailSheetNewName = "Detail",

    // This flag tells the engine that duplicate sheet names are acceptable.
    // Useful when you generate multiple detail sheets from a loop.
    AllowDuplicateSheetNames = true
};
```

**Tại sao điều này quan trọng:**  
Nếu bạn lặp qua nhiều khách hàng và mỗi vòng lặp tạo một sheet mới, engine thường sẽ ném ra ngoại lệ. Đặt `AllowDuplicateSheetNames` thành `true` sẽ khiến Aspose.Cells tự động thêm hậu tố số, giữ cho quá trình diễn ra mượt mà.

---

## Step 3 – Load the Excel template that holds SmartMarker tags

Template của bạn là canvas mà SmartMarker sẽ vẽ dữ liệu lên. Nó có thể chứa bất kỳ định dạng nào—màu sắc, công thức, biểu đồ—để bạn không phải tái tạo logic đó bằng code.

```csharp
// Step 3: Load the workbook that contains SmartMarker tags
using var workbook = new Aspose.Cells.Workbook(@"C:\MyProjects\ExcelDemo\template.xlsx");
```

**Mẹo:**  
Giữ template trong một thư mục là một phần của output dự án (ví dụ, `Content\Templates`). Như vậy bạn có thể tham chiếu bằng đường dẫn tương đối và tránh việc hard‑code đường dẫn tuyệt đối.

---

## Step 4 – Run the SmartMarker processor with the JSON and options

Bây giờ phép màu xảy ra. `SmartMarkerProcessor` đọc JSON, tôn trọng các tùy chọn bạn đã đặt, và điền dữ liệu vào workbook tương ứng.

```csharp
// Step 4: Process the SmartMarker tags using the JSON data and the configured options
workbook.SmartMarkerProcessor.Process(jsonData, smartMarkerOptions);
```

**Điều gì đang diễn ra bên trong?**  
- Bộ xử lý quét mọi ô để tìm các marker như `&=Name` hoặc `&=Orders.Item`.  
- Nó thay thế các marker đơn giản bằng giá trị scalar (`Name`, `Date`).  
- Đối với các collection (`Orders`), nó tạo một detail sheet mới (đặt tên “Detail”) và điền một hàng bảng cho mỗi mục.  
- Vì chúng ta đã cho phép trùng tên sheet, nếu template đã có một sheet tên “Detail”, engine sẽ tạo “Detail (2)”.

---

## Step 5 – Save the merged workbook back to disk

Cuối cùng, ghi workbook đã được điền dữ liệu ra file. Bạn có thể chọn bất kỳ định dạng nào được Aspose.Cells hỗ trợ—XLSX, CSV, PDF, v.v. Ở đây chúng ta sẽ dùng định dạng hiện đại XLSX.

```csharp
// Step 5: Save the workbook with the merged data
workbook.Save(@"C:\MyProjects\ExcelDemo\output.xlsx");
```

**Tại sao điều này quan trọng:**  
Lưu là nơi bạn thực sự **save workbook C#** style. Nếu cần stream file về client web, bạn có thể dùng `workbook.Save(Stream, SaveFormat.Xlsx)` thay thế.

---

## Full Working Example

Kết hợp mọi thứ lại, dưới đây là một console app hoàn chỉnh, sẵn sàng chạy. Đảm bảo bạn đã cài đặt gói NuGet `Aspose.Cells` (`dotnet add package Aspose.Cells`) trước khi biên dịch.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

namespace ExcelFromJsonDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Define the JSON payload
            string jsonData = @"{
                ""Name"": ""John"",
                ""Date"": ""2023-01-01"",
                ""Orders"": [
                    { ""Item"": ""Laptop"", ""Qty"": 2, ""Price"": 1200 },
                    { ""Item"": ""Mouse"",  ""Qty"": 5, ""Price"": 25 }
                ]
            }";

            // 2️⃣ Configure SmartMarker options – allow duplicate sheet names & set detail sheet name
            var smartMarkerOptions = new SmartMarkerOptions
            {
                DetailSheetNewName = "Detail",
                AllowDuplicateSheetNames = true
            };

            // 3️⃣ Load the template workbook (ensure the path is correct)
            var workbookPath = @"C:\MyProjects\ExcelDemo\template.xlsx";
            using var workbook = new Workbook(workbookPath);

            // 4️⃣ Merge JSON data into the workbook
            workbook.SmartMarkerProcessor.Process(jsonData, smartMarkerOptions);

            // 5️⃣ Save the result
            var outputPath = @"C:\MyProjects\ExcelDemo\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"✅ Excel file generated successfully at: {outputPath}");
        }
    }
}
```

### Kết Quả Mong Đợi

- **Sheet 1** (sheet master) sẽ hiển thị “John” trong ô `Name` và “2023‑01‑01` trong ô `Date`.  
- Một sheet **Detail** mới sẽ xuất hiện, chứa bảng với hai hàng: một cho đơn hàng Laptop và một cho đơn hàng Mouse.  
- Nếu template đã có một sheet tên “Detail”, sheet mới sẽ được đặt tên “Detail (2)”, nhờ cờ `AllowDuplicateSheetNames`.

![Kết quả Excel hiển thị sheet chính với tên và ngày, cộng với sheet Chi Tiết chứa các dòng đơn hàng](excel-output.png "kết quả tạo excel từ json")

*Văn bản thay thế hình ảnh:* **tạo excel từ json – ví dụ sổ làm việc với sheet chính và chi tiết**

---

## Common Questions & Edge Cases

### Nếu JSON của tôi chứa các collection lồng nhau thì sao?

SmartMarker có thể xử lý các mảng lồng nhau, nhưng bạn sẽ cần thêm các detail sheet hoặc sử dụng các marker phân cấp. Ví dụ, `&=Orders.SubItems.Product` sẽ tự động tạo một sheet cấp ba.

### Làm thế nào để tùy chỉnh mẫu đặt tên cho các sheet trùng?

Thay vì một `DetailSheetNewName` tĩnh, bạn có thể gán một callback qua `smartMarkerOptions.DetailSheetNameGenerator`. Điều này cho phép bạn chèn timestamp hoặc ID duy nhất vào tên sheet.

```csharp
smartMarkerOptions.DetailSheetNameGenerator = (baseName, index) =>
    $"{baseName}_{DateTime.Now:yyyyMMdd}_{index}";
```

### Tôi có thể tạo CSV thay vì XLSX không?

Chắc chắn rồi. Thay thế lời gọi `Save` cuối cùng bằng:

```csharp
workbook.Save(outputPath, SaveFormat.Csv);
```

Phần còn lại của pipeline vẫn giữ nguyên.

### Điều này có hoạt động trong ASP.NET Core không?

Có. Đoạn code giống hệt có thể chạy trong một action controller. Chỉ cần stream workbook về response:

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
ms.Position = 0;
return File(ms, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "report.xlsx");
```

---

## Pro Tips & Pitfalls

- **Mẹo chuyên gia:** Giữ các thẻ SmartMarker trong một sheet “Template” riêng. Như vậy bạn có thể bảo vệ sheet khỏi các chỉnh sửa vô tình trong khi vẫn cho phép processor đọc nó.  
- **Cảnh báo:** Các key JSON chứa dấu cách hoặc ký tự đặc biệt. Aspose.Cells yêu cầu các identifier hợp lệ của JavaScript; hãy đổi tên chúng hoặc dùng thuộc tính `JsonProperty` nếu bạn đang deserialize từ POCO.  
- **Mẹo hiệu năng:** Nếu bạn xử lý hàng ngàn dòng, đặt `smartMarkerOptions.EnableCache = true` để tái sử dụng các marker đã biên dịch.  
- **Kiểm tra phiên bản:** Code trên nhắm tới Aspose.Cells 23.9+. Các phiên bản cũ hơn có thể không hỗ trợ `AllowDuplicateSheetNames`.

---

## Conclusion

Bạn đã có một công thức hoàn chỉnh, đầu‑từ‑đầu để **generate Excel from JSON** trong C#. Bằng cách cấu hình `SmartMarkerOptions` chúng ta đã minh họa cách **cho phép trùng tên sheet**, kiểm soát việc đặt tên **detail sheet**, và cuối cùng **save workbook C#** style. Cách tiếp cận này hoàn toàn tự chứa—không cần dịch vụ bên ngoài, chỉ một gói NuGet duy nhất.

Bước tiếp theo? Hãy thử thay thế nguồn JSON bằng một API thực tế

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}