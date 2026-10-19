---
category: general
date: 2026-05-23
description: Cách sử dụng markers với Aspose.Cells để thực hiện tự động đặt tên sheet
  động trong Excel. Tìm hiểu smart markers, ràng buộc dữ liệu JSON và tạo sheet trong
  vài phút.
draft: false
keywords:
- how to use markers
- dynamic sheet naming excel
- aspose.cells smart markers
language: vi
og_description: Cách sử dụng markers trong Aspose.Cells để tạo file Excel với việc
  đặt tên sheet động. Hướng dẫn chi tiết từng bước kèm ví dụ đầy đủ bằng C#.
og_title: Cách Sử Dụng Markers – Đặt Tên Bảng Động trong Excel với Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
    Excel automation. Learn smart markers, JSON data binding, and sheet creation in
    minutes.
  headline: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
  type: TechArticle
- description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
    Excel automation. Learn smart markers, JSON data binding, and sheet creation in
    minutes.
  name: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
  steps:
  - name: What Happens Under the Hood?
    text: 1. The processor reads the `Orders` array. 2. For each order it creates
      a **master sheet** (using `${Orders.MasterSheetName}`) and a **detail sheet**
      (using the `DetailSheetNewName` pattern). 3. Cell values are replaced with the
      corresponding JSON fields, so the master sheet’s first cell ends up con
  - name: What if I need more than two levels of hierarchy?
    text: You can nest markers inside the newly created detail sheets. Just place
      additional `${...}` tags in the template sheet before processing. The processor
      will cascade through each level automatically.
  - name: Can I use a DataTable instead of JSON?
    text: Absolutely. `SmartMarkerProcessor` has overloads for `DataSet`, `DataTable`,
      and even custom objects. The only change is the call to `ApplyJson` – you’d
      use `ApplyDataSet(myDataSet)` instead.
  - name: How do I control the order of sheet creation?
    text: The order follows the sequence of the source collection. If you need a custom
      sort, simply sort the JSON array (or DataTable) before passing it to the processor.
  - name: Is there a way to hide the template sheet after processing?
    text: Yes. Set `sm.Options.RemoveTemplateSheets = true;` before calling `ApplyJson`.
      The original sheet (index 0) will be removed from the final workbook.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cách sử dụng các marker trong Aspose.Cells để đặt tên sheet động trong Excel
url: /vi/net/smart-markers-dynamic-data/how-to-use-markers-in-aspose-cells-for-dynamic-sheet-naming/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sử Dụng Markers trong Aspose.Cells để Đặt Tên Sheet Động trong Excel

Bạn đã bao giờ tự hỏi **cách sử dụng markers** để biến một mẫu Excel tĩnh thành một workbook master‑detail hoàn chỉnh chưa? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi cần khả năng *dynamic sheet naming excel*, đặc biệt khi tên sheet phải phản ánh các giá trị dữ liệu đến từ JSON hoặc cơ sở dữ liệu.  

Trong tutorial này chúng ta sẽ đi qua một ví dụ C# đầy đủ, sẵn sàng chạy, cho thấy **cách sử dụng markers** với **Aspose.Cells** smart markers, ràng buộc dữ liệu JSON, và để bộ xử lý tạo các sheet có tên thay đổi ngay lập tức. Không có phần thừa, chỉ có đoạn code chính xác bạn có thể chèn vào Visual Studio và thấy kết quả ngay.

## Những Điều Bạn Sẽ Học

- Khái niệm về **smart markers** và tại sao chúng hoàn hảo cho các kịch bản master‑detail.  
- Cách nhúng các thẻ marker vào workbook để sau này được thay thế bằng tên sheet thực tế.  
- Thiết lập **dynamic sheet naming excel** bằng tùy chọn `DetailSheetNewName`.  
- Chạy `SmartMarkerProcessor` với dữ liệu JSON để tự động tạo nhiều sheet.  
- Xác minh kết quả và một vài mẹo hữu ích để tránh các lỗi thường gặp.

> **Yêu cầu trước** – Bạn cần một runtime .NET mới (≥ .NET 6 là ổn), thư viện Aspose.Cells cho .NET (bạn có thể tải bản dùng thử miễn phí từ Aspose), và kiến thức cơ bản về C#.  

---

![ví dụ cách sử dụng markers trong Aspose.Cells](example.png "ví dụ cách sử dụng markers trong Aspose.Cells")

## Cách Sử Dụng Markers để Tạo Đặt Tên Sheet Động (Bước 1)

Điều đầu tiên chúng ta cần là một workbook trống sẽ đóng vai trò là mẫu. Trong dự án thực tế bạn có thể bắt đầu từ một file `.xlsx` đã có bố cục, định dạng và các ô placeholder. Để dễ hiểu, chúng ta sẽ tạo mọi thứ bằng mã.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

// Step 1: Create a new workbook and get the first worksheet
Workbook wb = new Workbook();                // fresh workbook, no sheets yet
Worksheet ws = wb.Worksheets[0];             // default first sheet
```

*Why this matters*: Đối tượng `Worksheet` là nơi chúng ta sẽ đặt các thẻ **smart marker**. Hãy nghĩ các thẻ này như những placeholder nhỏ mà bộ xử lý sẽ thay thế bằng các giá trị thực tế từ JSON.  

## Chèn Thẻ Smart Marker (Bước 2)

Bây giờ chúng ta đặt các thẻ marker trực tiếp vào các ô. Cú pháp `${...}` thông báo cho Aspose.Cells “đây là một marker”. Trong ví dụ của chúng ta cần hai marker: một cho tên sheet master và một cho tên sheet detail.

```csharp
// Step 2: Insert Smart Marker tags that will be replaced with sheet names
ws.Cells[0, 0].PutValue("${Orders.MasterSheetName}");   // master sheet placeholder
ws.Cells[1, 0].PutValue("${Orders.DetailSheetName}");   // detail sheet placeholder
```

> **Pro tip** – Giữ tên marker ngắn gọn và có ý nghĩa; chúng sẽ trở thành các khóa bạn sẽ dùng trong payload JSON của mình.

## Chuẩn Bị Dữ Liệu JSON (Bước 3)

Bộ xử lý làm việc với bất kỳ nguồn dữ liệu nào có thể biểu diễn dưới dạng JSON, `DataSet`, hoặc thậm chí một đối tượng thuần. Dưới đây là một chuỗi JSON tối thiểu chứa một collection master‑detail. Lưu ý mỗi đơn hàng đều có cả `MasterSheetName` và `DetailSheetName`.

```csharp
// Step 3: Prepare the JSON data that contains the master‑detail information
string jsonOrders = @"{
    ""Orders"": [
        {
            ""OrderId"": 1,
            ""MasterSheetName"": ""Master_1"",
            ""DetailSheetName"": ""Detail_1""
        },
        {
            ""OrderId"": 2,
            ""MasterSheetName"": ""Master_2"",
            ""DetailSheetName"": ""Detail_2""
        }
    ]
}";
```

*Why JSON?* Nó nhẹ, dễ đọc, và hoạt động tốt với các API web. Bạn cũng có thể lấy dữ liệu này từ truy vấn SQL và serialize bằng `Newtonsoft.Json`.

## Khởi Tạo SmartMarkerProcessor (Bước 4)

`SmartMarkerProcessor` là engine quét workbook, tìm marker và thực hiện ràng buộc dữ liệu. Khởi tạo nó chỉ cần một dòng mã.

```csharp
// Step 4: Initialise the SmartMarkerProcessor with the workbook
SmartMarkerProcessor sm = new SmartMarkerProcessor(wb);
```

## Định Nghĩa Đặt Tên Sheet Động (Bước 5)

Đây là nơi **dynamic sheet naming excel** thực sự tỏa sáng. Bằng cách thiết lập `DetailSheetNewName`, chúng ta chỉ cho bộ xử lý tạo một sheet detail mới cho mỗi đơn hàng và đặt tên dựa trên `OrderId`. Placeholder `${OrderId}` sẽ được giải quyết từ bản ghi hiện tại trong quá trình xử lý.

```csharp
// Step 5: Define how new detail sheets should be named during processing
sm.Options.DetailSheetNewName = "Detail_${OrderId}";
```

> **Watch out** – Nếu bạn quên bao gồm cú pháp `${}`, sheet sẽ thực sự được đặt tên “Detail_${OrderId}” thay vì “Detail_1”, “Detail_2”, v.v.

## Áp Dụng JSON và Tạo Các Sheet (Bước 6)

Bây giờ để bộ xử lý thực hiện công việc nặng. Nó sẽ đọc JSON, thay thế các marker và tạo các worksheet mới khi cần.

```csharp
// Step 6: Apply the JSON data to populate the smart markers and generate sheets
sm.ApplyJson(jsonOrders);
```

### Điều Gì Xảy Ra Bên Trong?

1. Bộ xử lý đọc mảng `Orders`.  
2. Với mỗi đơn hàng, nó tạo một **master sheet** (sử dụng `${Orders.MasterSheetName}`) và một **detail sheet** (sử dụng mẫu `DetailSheetNewName`).  
3. Giá trị các ô được thay thế bằng các trường JSON tương ứng, vì vậy ô đầu tiên của master sheet sẽ chứa “Master_1”, “Master_2”, v.v.  

## Lưu và Xác Minh Kết Quả (Tùy Chọn)

Cuối cùng, ghi workbook ra đĩa. Mở file trong Excel và bạn sẽ thấy hai master sheet (`Master_1`, `Master_2`) và hai detail sheet có tên động (`Detail_1`, `Detail_2`).  

```csharp
// (Optional) Save the result to verify the output
wb.Save("output.xlsx");
```

**Expected output** – Sau khi mở `output.xlsx` bạn sẽ thấy:

- Sheet **Master_1** với ô A1 = “Master_1”.  
- Sheet **Detail_1** với ô A1 = “Detail_1”.  
- Sheet **Master_2** với ô A1 = “Master_2”.  
- Sheet **Detail_2** với ô A1 = “Detail_2”.  

Đó là vòng tuần hoàn đầy đủ của **cách sử dụng markers** để đạt được **dynamic sheet naming excel** với **Aspose.Cells smart markers**.

---

## Các Câu Hỏi Thường Gặp & Trường Hợp Cạnh

### Nếu tôi cần hơn hai cấp độ phân cấp thì sao?

Bạn có thể lồng các marker bên trong các sheet detail mới tạo. Chỉ cần đặt thêm các thẻ `${...}` trong sheet mẫu trước khi xử lý. Bộ xử lý sẽ tự động cascade qua từng cấp độ.

### Tôi có thể dùng DataTable thay cho JSON không?

Chắc chắn rồi. `SmartMarkerProcessor` có các overload cho `DataSet`, `DataTable`, và thậm chí các đối tượng tùy chỉnh. Thay đổi duy nhất là lời gọi `ApplyJson` – bạn sẽ dùng `ApplyDataSet(myDataSet)` thay thế.

### Làm sao kiểm soát thứ tự tạo sheet?

Thứ tự tuân theo chuỗi của collection nguồn. Nếu bạn cần sắp xếp tùy chỉnh, chỉ cần sắp xếp mảng JSON (hoặc DataTable) trước khi truyền vào bộ xử lý.

### Có cách nào ẩn sheet mẫu sau khi xử lý không?

Có. Đặt `sm.Options.RemoveTemplateSheets = true;` trước khi gọi `ApplyJson`. Sheet gốc (chỉ số 0) sẽ bị loại bỏ khỏi workbook cuối cùng.

---

## Ví Dụ Hoàn Chỉnh (Tất Cả Các Bước Kết Hợp)

Dưới đây là chương trình đầy đủ bạn có thể sao chép‑dán vào một dự án console C# mới. Đảm bảo bạn đã tham chiếu gói NuGet `Aspose.Cells`.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

namespace DynamicSheetNamingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook wb = new Workbook();
            Worksheet ws = wb.Worksheets[0];

            // Step 2: Insert Smart Marker tags that will be replaced with sheet names
            ws.Cells[0, 0].PutValue("${Orders.MasterSheetName}");
            ws.Cells[1, 0].PutValue("${Orders.DetailSheetName}");

            // Step 3: Prepare the JSON data that contains the master‑detail information
            string jsonOrders = @"{
                ""Orders"": [
                    {
                        ""OrderId"": 1,
                        ""MasterSheetName"": ""Master_1"",
                        ""DetailSheetName"": ""Detail_1""
                    },
                    {
                        ""OrderId"": 2,
                        ""MasterSheetName"": ""Master_2"",
                        ""DetailSheetName"": ""Detail_2""
                    }
                ]
            }";

            // Step 4: Initialise the SmartMarkerProcessor with the workbook
            SmartMarkerProcessor sm = new SmartMarkerProcessor(wb);

            // Step 5: Define how new detail sheets should be named during processing
            sm.Options.DetailSheetNewName = "Detail_${OrderId}";

            // (Optional) Remove the original template sheet after processing
            // sm.Options.RemoveTemplateSheets = true;

            // Step 6: Apply the JSON data to populate the smart markers and generate sheets
            sm.ApplyJson(jsonOrders);

            // Save the result
            wb.Save("output.xlsx");
            Console.WriteLine("Workbook generated successfully. Check output.xlsx.");
        }
    }
}
```

Chạy chương trình, mở `output.xlsx`, và bạn sẽ thấy các sheet động chính xác như mô tả ở trên.

---

## Kết Luận

Chúng ta vừa mới khám phá **cách sử dụng markers** trong Aspose.Cells để biến một workbook đơn giản thành giải pháp master‑detail với **dynamic sheet naming excel**. Những điểm chính cần ghi nhớ:

1. Đặt các marker `${...}` ở nơi bạn muốn dữ liệu xuất hiện.  
2. Cung cấp JSON (hoặc bất kỳ nguồn dữ liệu hỗ trợ nào) cho `SmartMarkerProcessor`.  
3. Sử dụng `DetailSheetNewName` để cho phép bộ xử lý đặt tên sheet mới một cách tự động.  

Từ đây bạn có thể khám phá các kịch bản nâng cao hơn—thêm bảng, định dạng ô, hoặc thậm chí nhúng biểu đồ—tất cả đều được điều khiển

## Các Tutorial Liên Quan

- [Cách Triển Khai Aspose.Cells Smart Markers trong C# cho Báo Cáo Excel Động](/cells/english/net/automation-batch-processing/implement-aspose-cells-smart-markers-with-csharp/)
- [Tạo Báo Cáo Excel Động Sử Dụng Aspose.Cells .NET Smart Markers](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Thành Thạo Aspose.Cells .NET: Triển Khai Smart Markers và Nhãn Tùy Chỉnh cho Báo Cáo Excel Động](/cells/english/net/advanced-features/aspose-cells-net-smart-markers-custom-labels/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}