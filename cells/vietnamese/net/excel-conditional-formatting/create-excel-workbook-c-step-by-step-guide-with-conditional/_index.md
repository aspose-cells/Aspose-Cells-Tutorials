---
category: general
date: 2026-03-27
description: Tạo workbook Excel bằng C# với Aspose.Cells, áp dụng định dạng có điều
  kiện, nhập DataTable vào Excel và lưu workbook dưới dạng xlsx — tất cả trong một
  hướng dẫn.
draft: false
keywords:
- create excel workbook c#
- apply conditional formatting
- import datatable to excel
- save workbook as xlsx
- create excel file programmatically
language: vi
og_description: Tạo workbook Excel bằng C# sử dụng Aspose.Cells, áp dụng định dạng
  có điều kiện, nhập DataTable vào Excel và lưu workbook dưới dạng xlsx trong vài
  phút.
og_title: Tạo Workbook Excel bằng C# – Hướng Dẫn Toàn Diện với Định Dạng Có Điều Kiện
tags:
- Aspose.Cells
- C#
- Excel automation
title: Tạo Workbook Excel bằng C# – Hướng dẫn từng bước với Định dạng có điều kiện
url: /vi/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Excel Workbook C# – Hướng dẫn lập trình đầy đủ

Bạn đã bao giờ cần **create excel workbook c#** một cách nhanh chóng nhưng không biết bắt đầu từ đâu? Bạn không phải là người duy nhất—nhiều nhà phát triển gặp khó khăn này khi lần đầu tự động hoá báo cáo. Trong hướng dẫn này, chúng tôi sẽ chỉ cho bạn cách tạo excel workbook c# bằng Aspose.Cells, áp dụng định dạng có điều kiện, nhập datatable vào excel và cuối cùng lưu workbook dưới dạng xlsx.  

Bạn sẽ nhận được một ứng dụng console sẵn sàng chạy, tạo ra một tệp Excel đầy màu sắc, cùng với giải thích chi tiết từng dòng để bạn có thể tùy chỉnh cho dự án của mình. Không cần tài liệu bên ngoài; chỉ cần sao chép, dán và chạy.  

### Yêu cầu trước

- .NET 6+ (hoặc .NET Framework 4.7.2+) đã được cài đặt  
- Visual Studio 2022 hoặc bất kỳ trình soạn thảo C# nào bạn thích  
- Aspose.Cells for .NET (bạn có thể tải gói NuGet dùng thử miễn phí)  

Nếu đã có những thứ trên, hãy bắt đầu.

## Tạo Excel Workbook C# – Khởi tạo Workbook

Điều đầu tiên bạn phải làm là **create excel workbook c#** bằng cách khởi tạo lớp `Workbook`. Đối tượng này đại diện cho toàn bộ tệp Excel trong bộ nhớ.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System.Data;
using System.Drawing;

class SmartMarkerConditionalDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                // <-- creates the workbook
        Worksheet worksheet = workbook.Worksheets[0];      // first sheet (Sheet1)
```

> **Tại sao điều này quan trọng:** Lớp `Workbook` trừu tượng hoá định dạng tệp, vì vậy bạn không cần phải loay hoay với XML cấp thấp hay COM interop. Nó cũng cung cấp cho bạn quyền truy cập vào các style, table và smart markers ngay từ đầu.

## Áp dụng Định dạng có Điều kiện

Bây giờ workbook đã tồn tại, hãy **apply conditional formatting** để làm nổi bật các hàng có số lượng vượt quá 100. Định dạng có điều kiện nằm trên worksheet, không phải trên ô, giúp tái sử dụng dễ dàng.

```csharp
        // Step 4: Apply conditional formatting to highlight quantities > 100
        int cfIndex = worksheet.ConditionalFormattings.Add();               // add a new CF collection
        var conditionalFormatting = worksheet.ConditionalFormattings[cfIndex];
        var condition = conditionalFormatting.AddCondition(
            FormatConditionType.CellValue, OperatorType.Greater, "100");   // > 100

        // Define the style that will be applied when the condition is true
        condition.Style = workbook.CreateStyle();
        condition.Style.Font.Color = Color.Red;               // red font
        condition.Style.Pattern = BackgroundType.Solid;       // solid background
        condition.Style.ForegroundColor = Color.Yellow;      // yellow fill
```

> **Mẹo chuyên nghiệp:** Nếu bạn cần quy tắc phức tạp hơn (ví dụ: giữa hai giá trị), chỉ cần gọi `AddCondition` một lần nữa với `OperatorType.Between`.

## Ghi tiêu đề và Smart Markers

Trước khi chúng ta **import datatable to excel**, chúng ta cần các ô giữ chỗ—smart markers—mà thư viện sẽ thay thế bằng dữ liệu thực. Hãy nghĩ chúng như các thẻ mẫu.

```csharp
        // Step 2: Write the header row
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Quantity");
        worksheet.Cells["C1"].PutValue("Status");

        // Step 3: Define smart markers that will be replaced by data
        worksheet.Cells["A2"].PutValue("&=Products.ProductName");
        worksheet.Cells["B2"].PutValue("&=Products.Quantity");
        worksheet.Cells["C2"].PutValue("&=Products.Quantity > 100 ? \"High\" : \"Low\"");
```

> **Tại sao smart markers?** Chúng cho phép bạn giữ bố cục Excel tách biệt khỏi mã. Bạn thiết kế sheet một lần, sau đó chỉ cần cung cấp một `DataTable` và thư viện sẽ tự động thực hiện phần còn lại.

## Nhập DataTable vào Excel

Đây là phần cốt lõi của **import datatable to excel**. Chúng ta tạo một `DataTable` phản ánh các trường smart marker và truyền nó cho `ImportDataTable`.

```csharp
        // Step 5: Build a simple DataTable that matches the smart marker fields
        DataTable products = new DataTable();
        products.Columns.Add("ProductName");
        products.Columns.Add("Quantity", typeof(int));
        products.Rows.Add("Apple", 120);
        products.Rows.Add("Banana", 80);
        products.Rows.Add("Cherry", 150);

        // Step 6: Populate the worksheet with the DataTable via smart markers
        worksheet.Cells.ImportDataTable(products, true, "A2");
```

> **Trường hợp đặc biệt:** Nếu bảng của bạn có nhiều cột hơn cần thiết, chỉ cần bỏ qua các cột thừa trong smart markers; chúng sẽ bị bỏ qua.

## Lưu Workbook dưới dạng XLSX

Cuối cùng, chúng ta **save workbook as xlsx** vào đĩa. Phương thức `Save` tự động xác định định dạng dựa trên phần mở rộng tệp.

```csharp
        // Step 7: Save the result to an Excel file
        workbook.Save("SmartMarkersConditional.xlsx");   // <-- saves as .xlsx
    }
}
```

Đó là toàn bộ chương trình. Khi bạn chạy, sẽ xuất hiện một tệp có tên `SmartMarkersConditional.xlsx` trong thư mục output.

### Kết quả mong đợi

| Sản phẩm | Số lượng | Trạng thái |
|----------|----------|------------|
| Apple    | 120      | Cao        |
| Banana   | 80       | Thấp       |
| Cherry   | 150      | Cao        |

Các hàng có **Quantity > 100** (Apple và Cherry) sẽ có văn bản màu đỏ trên nền vàng nhờ định dạng có điều kiện chúng ta đã thêm ở trên.

## Tạo tệp Excel bằng chương trình – Danh sách mã nguồn đầy đủ

Dưới đây là toàn bộ mã nguồn sẵn sàng sao chép. Nó chứa mọi phần chúng ta đã thảo luận, cộng thêm một vài chú thích để rõ ràng hơn.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System.Data;
using System.Drawing;

class SmartMarkerConditionalDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write header cells
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Quantity");
        worksheet.Cells["C1"].PutValue("Status");

        // 3️⃣ Insert smart markers – placeholders for our data
        worksheet.Cells["A2"].PutValue("&=Products.ProductName");
        worksheet.Cells["B2"].PutValue("&=Products.Quantity");
        worksheet.Cells["C2"].PutValue("&=Products.Quantity > 100 ? \"High\" : \"Low\"");

        // 4️⃣ Apply conditional formatting (highlight >100)
        int cfIdx = worksheet.ConditionalFormattings.Add();
        var cf = worksheet.ConditionalFormattings[cfIdx];
        var cond = cf.AddCondition(FormatConditionType.CellValue, OperatorType.Greater, "100");
        cond.Style = workbook.CreateStyle();
        cond.Style.Font.Color = Color.Red;
        cond.Style.Pattern = BackgroundType.Solid;
        cond.Style.ForegroundColor = Color.Yellow;

        // 5️⃣ Build a DataTable that matches the markers
        DataTable products = new DataTable();
        products.Columns.Add("ProductName");
        products.Columns.Add("Quantity", typeof(int));
        products.Rows.Add("Apple", 120);
        products.Rows.Add("Banana", 80);
        products.Rows.Add("Cherry", 150);

        // 6️⃣ Import the DataTable – this replaces the smart markers
        worksheet.Cells.ImportDataTable(products, true, "A2");

        // 7️⃣ Save the workbook – this will create an .xlsx file
        workbook.Save("SmartMarkersConditional.xlsx");
    }
}
```

> **Mẹo:** Nếu bạn cần tạo nhiều sheet, chỉ cần lặp lại các bước 2‑6 trên một đối tượng `Worksheet` mới được lấy bằng `workbook.Worksheets.Add()`.

## Tại sao nên sử dụng Aspose.Cells cho tự động hóa Excel C#?

- **Hiệu năng:** Hoạt động hoàn toàn trong bộ nhớ, không cần COM interop, vì vậy nhanh ngay cả với bộ dữ liệu lớn.  
- **Tính năng phong phú:** Hỗ trợ smart markers, định dạng có điều kiện, biểu đồ, pivot table và nhiều hơn nữa.  
- **Đa nền tảng:** Hoạt động trên Windows, Linux và macOS với .NET Core/5/6+.  

Nếu bạn gặp khó khăn với một tính năng nào đó—ví dụ, thêm biểu đồ hoặc bảo vệ sheet—chỉ cần tìm “asp​ose.cells add chart c#” và bạn sẽ tìm thấy mẫu tương tự.

## Các bước tiếp theo & Chủ đề liên quan

- **Xuất ra PDF:** Sau khi bạn **create excel workbook c#**, có thể ngay lập tức xuất ra PDF bằng `workbook.Save("output.pdf")`.  
- **Đọc các tệp Excel hiện có:** Sử dụng `new Workbook("ExistingFile.xlsx")` để chỉnh sửa một mẫu.  
- **Nhập hàng loạt:** Đối với dữ liệu khổng lồ, cân nhắc dùng `ImportArray` hoặc `ImportDataTable` kết hợp `ImportOptions` để tăng tốc.  

Hãy thoải mái thử nghiệm các quy tắc điều kiện, màu sắc khác nhau, hoặc thậm chí thêm một hàng tổng bằng công thức. Không có giới hạn khi bạn **create excel file programmatically**.

---

*Bạn đã sẵn sàng thử chưa? Lấy mã, chạy và mở `SmartMarkersConditional.xlsx` đã tạo. Nếu gặp bất kỳ vấn đề nào, hãy để lại bình luận bên dưới—chúc bạn lập trình vui!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}