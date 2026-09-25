---
category: general
date: 2026-05-04
description: Tạo Excel từ mẫu và ánh xạ JSON sang Excel với việc đặt tên worksheet
  động. Học cách điền dữ liệu vào Excel từ JSON và tạo Excel bằng JSON chỉ trong vài
  phút.
draft: false
keywords:
- create excel from template
- map json to excel
- populate excel from json
- dynamic worksheet naming excel
- generate excel using json
language: vi
og_description: Tạo Excel từ mẫu nhanh chóng. Hướng dẫn này chỉ cách ánh xạ JSON sang
  Excel, điền dữ liệu Excel từ JSON, sử dụng đặt tên worksheet động và tạo Excel bằng
  JSON.
og_title: Tạo Excel từ mẫu – Hướng dẫn .NET đầy đủ
tags:
- C#
- Aspose.Cells
- SmartMarker
- JSON
title: Tạo Excel từ mẫu – Hướng dẫn chi tiết từng bước cho các nhà phát triển .NET
url: /vi/net/templates-reporting/create-excel-from-template-step-by-step-guide-for-net-develo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Excel từ Mẫu – Hướng Dẫn .NET Đầy Đủ

Bạn đã bao giờ cần **tạo Excel từ mẫu** nhưng lại gặp khó khăn khi xử lý dữ liệu JSON và tên worksheet? Bạn không phải là người duy nhất. Trong nhiều dự án báo cáo, mẫu giữ bố cục trong khi payload JSON cung cấp các giá trị thực tế, và việc làm cho chúng “giao tiếp” với nhau có thể gây đau đầu.  

Tin tốt là gì? Chỉ với vài dòng C# và engine SmartMarker của Aspose Cells, bạn có thể **điền dữ liệu Excel từ JSON**, đổi tên sheet chi tiết một cách động, và cuối cùng **tạo Excel bằng JSON** mà không cần chạm vào giao diện người dùng.  

Trong hướng dẫn này, chúng ta sẽ đi qua toàn bộ quy trình: tải mẫu, ánh xạ JSON sang Excel, cấu hình đặt tên worksheet động, và lưu workbook cuối cùng. Khi hoàn thành, bạn sẽ có một đoạn mã có thể tái sử dụng trong bất kỳ dịch vụ .NET nào. Không cần công cụ bên ngoài, chỉ cần code thuần.

---

## Những Điều Bạn Cần Có

- **Aspose.Cells for .NET** (v24.10 trở lên) – thư viện cung cấp SmartMarker.  
- Một file **template.xlsx** chứa các thẻ SmartMarker như `{Master:Name}` và `{Detail:Item}`.  
- Một file **data.json** có cấu trúc master‑detail phù hợp.  
- Visual Studio 2022 (hoặc bất kỳ IDE nào bạn thích) với mục tiêu .NET 6 trở lên.

Đó là tất cả. Nếu bạn đã có những thành phần trên, bạn đã sẵn sàng bắt đầu.

---

## Tạo Excel từ Mẫu – Tổng Quan

Ý tưởng cốt lõi rất đơn giản: coi file Excel như một *mẫu* và để SmartMarker thay thế các placeholder bằng giá trị từ JSON của bạn. Thư viện cũng cho phép bạn đổi tên worksheet chi tiết dựa trên một trường master, đó là lúc **đặt tên worksheet động trong Excel** tỏa sáng.

Dưới đây là toàn bộ mã đã sẵn sàng chạy. Bạn có thể sao chép‑dán vào một ứng dụng console và chỉnh đường dẫn tới các file của mình.

```csharp
// ------------------------------------------------------------
// Full example: create Excel from template using JSON data
// ------------------------------------------------------------
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains SmartMarker tags
            //    (e.g., {Master:Name} in the master sheet and {Detail:Item} in the detail sheet)
            string templatePath = @"C:\MyProject\Templates\template.xlsx";
            Workbook wb = new Workbook(templatePath);

            // 2️⃣ Read the JSON data that will populate the markers
            //    The JSON should match the structure expected by the template.
            string jsonPath = @"C:\MyProject\Data\data.json";
            string json = File.ReadAllText(jsonPath);

            // 3️⃣ Configure the SmartMarker processor to rename the detail sheet
            //    dynamically based on the master record’s Name field.
            //    This demonstrates dynamic worksheet naming excel.
            wb.SmartMarkerProcessor.Options.DetailSheetNewName = "Detail_{Master.Name}";

            // 4️⃣ Execute the SmartMarker processing using the JSON data.
            //    This step maps JSON to Excel and populates every marker.
            wb.SmartMarkerProcessor.Execute(json);

            // 5️⃣ Save the processed workbook – now it’s a brand‑new file.
            string outputPath = @"C:\MyProject\Output\output.xlsx";
            wb.Save(outputPath);

            Console.WriteLine("✅ Excel file generated successfully at: " + outputPath);
        }
    }
}
```

> **Kết quả mong đợi:**  
> - Sheet master sẽ hiển thị tên từ `Master.Name`.  
> - Sheet detail sẽ được đổi tên thành một chuỗi như `Detail_JohnDoe`.  
> - Tất cả các hàng `{Detail:Item}` sẽ được lấp đầy bằng mảng items từ JSON.

---

## Ánh Xạ JSON sang Excel – Tải Dữ Liệu

Trước khi engine SmartMarker thực hiện phép màu, JSON phải **đúng định dạng** và phản ánh đúng cấu trúc phân cấp được dùng trong mẫu. Một JSON master‑detail điển hình trông như sau:

```json
{
  "Master": {
    "Name": "John Doe",
    "Date": "2026-05-04"
  },
  "Detail": [
    { "Item": "Widget A", "Qty": 10, "Price": 2.5 },
    { "Item": "Widget B", "Qty": 5,  "Price": 5.0 }
  ]
}
```

**Tại sao lại quan trọng:**  
- Các khóa `Master` và `Detail` tương ứng trực tiếp với các thẻ `{Master:…}` và `{Detail:…}`.  
- Nếu cấu trúc JSON khác, SmartMarker sẽ không tìm thấy khớp, và các ô sẽ để trống.  

**Mẹo:** Kiểm tra JSON của bạn bằng một công cụ validator trực tuyến hoặc dùng `System.Text.Json.JsonDocument.Parse(json)` để phát hiện lỗi cú pháp sớm.

---

## Điền Dữ Liệu Excel từ JSON – Cấu Hình SmartMarker

SmartMarker hoạt động bằng cách quét workbook để tìm thẻ, sau đó chèn dữ liệu. Bước **populate excel from json** thực chất là lời gọi `Execute` mà chúng ta đã thấy, nhưng có một vài tùy chọn tùy chọn đáng chú ý:

| Setting | What it does | When to use it |
|---------|--------------|----------------|
| `Options.CaseSensitive` | Xử lý tên thẻ phân biệt chữ hoa/thường. | Khi mẫu của bạn trộn lẫn các kiểu chữ và bạn cần khớp chính xác. |
| `Options.RemoveEmptyRows` | Xóa các hàng không nhận được dữ liệu. | Để giữ sheet cuối cùng gọn gàng khi một số mục detail là tùy chọn. |
| `Options.EnableHyperlink` | Cho phép các hyperlink trong JSON trở thành có thể nhấp. | Khi bạn cần các URL có thể click trong báo cáo. |

Bạn có thể xâu chuỗi chúng như sau:

```csharp
wb.SmartMarkerProcessor.Options.CaseSensitive = true;
wb.SmartMarkerProcessor.Options.RemoveEmptyRows = true;
```

---

## Đặt Tên Worksheet Động trong Excel – Cấu Hình Tên Sheet Detail

Một trong những yêu cầu khó khăn mà nhiều dự án gặp phải là **đặt tên worksheet động trong Excel**. Thay vì một sheet “Detail” tĩnh, bạn có thể muốn mỗi báo cáo mang tên khách hàng hoặc số đơn hàng.

Dòng lệnh:

```csharp
wb.SmartMarkerProcessor.Options.DetailSheetNewName = "Detail_{Master.Name}";
```

thực hiện đúng như vậy. Placeholder `{Master.Name}` được thay thế *sau* khi JSON được xử lý, vì vậy tên sheet mới sẽ thành `Detail_JohnDoe`.  

**Trường hợp biên:** Nếu tên chứa các ký tự không hợp lệ trong tên sheet (`:`, `\`, `/`, `?`, `*`, `[`, `]`), Aspose sẽ tự động làm sạch chúng, nhưng bạn cũng có thể tiền xử lý chuỗi trong JSON nếu cần định dạng cụ thể.

---

## Tạo Excel Bằng JSON – Thực Thi và Lưu

Hai dòng cuối cùng của mã (`Execute` và `Save`) là nơi phép màu **generate excel using json** diễn ra. Bên trong, Aspose phân tích JSON thành bảng dữ liệu, duyệt qua mẫu, và ghi file đầu ra.

Nếu bạn cần tạo nhiều workbook trong một vòng lặp (ví dụ, một cho mỗi khách hàng), chỉ cần di chuyển việc khởi tạo `Workbook` vào trong vòng lặp và thay đổi tên file đầu ra cho phù hợp:

```csharp
foreach (var customerJson in customers)
{
    Workbook wb = new Workbook(templatePath);
    wb.SmartMarkerProcessor.Options.DetailSheetNewName = $"Detail_{customerJson.Master.Name}";
    wb.SmartMarkerProcessor.Execute(customerJson);
    wb.Save($@"C:\Reports\Report_{customerJson.Master.Name}.xlsx");
}
```

Mẫu này thường xuất hiện trong các dịch vụ báo cáo hàng loạt.

---

## Những Sai Lầm Thường Gặp & Mẹo Chuyên Nghiệp

- **Thiếu thẻ:** Nếu một ô vẫn hiển thị `{Master:Name}`, thẻ chưa được nhận diện. Kiểm tra lại chính tả và đảm bảo thẻ nằm trong ô, không phải trong comment.  
- **Payload JSON lớn:** Đối với tập dữ liệu khổng lồ, cân nhắc streaming JSON hoặc dùng `DataTable` thay vì chuỗi thô để giảm áp lực bộ nhớ.  
- **An toàn đa luồng:** Các instance `Workbook` không thread‑safe. Tạo một instance mới cho mỗi luồng nếu bạn chạy các job song song.  
- **Khóa file:** Đảm bảo mẫu không mở trong Excel khi code của bạn chạy; nếu không sẽ gặp `IOException`.

> **Mẹo pro:** Giữ một bản sao của mẫu gốc trong thư mục chỉ‑đọc. Điều này ngăn ngừa việc ghi đè vô tình trong quá trình debug.

---

## Tóm Tắt Ví Dụ Hoàn Chỉnh

Dưới đây là toàn bộ chương trình một lần nữa, lần này kèm các chú thích nội tuyến cho mọi dòng không hiển nhiên:

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // Path to the Excel template that contains SmartMarker tags.
            string templatePath = @"C:\MyProject\Templates\template.xlsx";

            // Load the workbook – this is the "create excel from template" step.
            Workbook wb = new Workbook(templatePath);

            // Read JSON data that maps directly to the template's tags.
            string jsonPath = @"C:\MyProject\Data\data.json";
            string json = File.ReadAllText(jsonPath);

            // OPTIONAL: tweak SmartMarker behavior (case‑sensitivity, empty rows, etc.).
            wb.SmartMarkerProcessor.Options.CaseSensitive = false;
            wb.SmartMarkerProcessor.Options.RemoveEmptyRows = true;

            // Set up dynamic worksheet naming based on the master record's Name field.
            wb.SmartMarkerProcessor.Options.DetailSheetNewName = "Detail_{Master.Name}";

            // Run the SmartMarker engine – this is where we "populate excel from json".
            wb.SmartMarkerProcessor.Execute(json);

            // Save the newly generated workbook – the final "generate excel using json" step.
            string outputPath = @"C:\MyProject\Output\output.xlsx";
            wb.Save(outputPath);

            Console.WriteLine("✅ Workbook created at: " + outputPath);
        }
    }
}
```

Chạy ứng dụng console này sẽ tạo ra `output.xlsx` với sheet detail đã được đổi tên và tất cả dữ liệu đã được điền.

---

## Các Bước Tiếp Theo & Chủ Đề Liên Quan

- **Xuất ra PDF:** Sau khi tạo workbook, bạn có thể gọi `wb.Save("report.pdf", SaveFormat.Pdf);` để xuất bản PDF.  
- **Điền dữ liệu biểu đồ:** SmartMarker cũng hỗ trợ nguồn dữ liệu cho chart; chỉ cần bind mảng JSON vào phạm vi series của chart.  
- **Định dạng có điều kiện:** Sử dụng các quy tắc có sẵn trong Excel template; chúng sẽ được giữ lại sau khi SmartMarker thay thế.  
- **Tối ưu hiệu năng:** Đối với kịch bản khối lượng lớn, tái sử dụng một instance `Workbook` duy nhất với `Clone` để tránh I/O file lặp lại.

Hãy thử nghiệm với các cấu trúc JSON khác nhau, mẫu đổi tên, hoặc thậm chí kết hợp nhiều mẫu trong một lần chạy. Tính linh hoạt của **create excel from template** với Aspose.Cells cho phép bạn áp dụng giải pháp này cho hoá đơn, dashboard, hoặc bất kỳ nhu cầu báo cáo nào.

---

## Tóm Tắt Hình Ảnh

![Quy trình tạo Excel từ mẫu hiển thị JSON → SmartMarker → Đặt tên sheet động](/images/create-excel-from-template-workflow.png "Sơ đồ quy trình tạo Excel từ mẫu")

*(Văn bản thay thế bao gồm từ khóa chính cho SEO)*

---

### Kết Luận

Chúng ta đã bao quát mọi thứ cần thiết để **tạo Excel từ mẫu**, **ánh xạ JSON sang Excel**, **điền Excel từ JSON**, sử dụng **đặt tên worksheet động trong Excel**, và cuối cùng **tạo Excel bằng JSON**. Mã đã đầy đủ, giải thích cho bạn *tại sao* mỗi dòng quan trọng, và bạn hiện có nền tảng vững chắc để xây dựng các pipeline báo cáo lớn hơn.

Bạn có ý tưởng nào muốn thực hiện? Hãy để lại bình luận bên dưới, chúng mình sẽ cùng nhau giải quyết. Chúc bạn lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}