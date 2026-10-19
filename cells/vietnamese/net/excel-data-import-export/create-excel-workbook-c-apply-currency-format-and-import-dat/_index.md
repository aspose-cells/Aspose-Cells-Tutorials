---
category: general
date: 2026-03-30
description: Tạo workbook Excel bằng C# với định dạng tiền tệ. Học cách nhập DataTable,
  thêm định dạng số trong Excel và áp dụng định dạng tiền tệ cho cột trong vài phút.
draft: false
keywords:
- create excel workbook c#
- format cells currency
- import datatable to excel
- add number format excel
- apply currency format column
language: vi
og_description: Tạo workbook Excel bằng C# và ngay lập tức định dạng ô thành tiền
  tệ. Hướng dẫn từng bước này cho thấy cách nhập DataTable vào Excel và thêm định
  dạng số cho một cột.
og_title: Tạo Workbook Excel bằng C# – Hướng dẫn định dạng tiền tệ
tags:
- Aspose.Cells
- C#
- Excel automation
title: Tạo Workbook Excel bằng C# – Áp dụng định dạng tiền tệ và nhập DataTable
url: /vi/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Workbook Excel C# – Áp Dụng Định Dạng Tiền Tệ và Nhập DataTable

Ever needed to **create Excel workbook C#** that already looks like a polished report? Maybe you’re pulling sales numbers from a database and you want the price column to show as dollars without fiddling with Excel manually. Sound familiar? You’re not alone—most developers hit this snag when they first automate Excel exports.

Trong hướng dẫn này, chúng tôi sẽ đi qua một giải pháp hoàn chỉnh, sẵn sàng chạy mà **creates an Excel workbook C#**, nhập một `DataTable`, và **formats the Price column as currency**. Khi kết thúc, bạn sẽ có một tệp có tên `StyledTable.xlsx` mà bạn có thể mở và thấy các số được định dạng đẹp mắt. Không cần xử lý hậu kỳ nào thêm.

> **Bạn sẽ học được gì**
> - Cách thiết lập Aspose.Cells trong dự án .NET  
> - Cách **import datatable to excel** với một mảng style  
> - Cách **add number format excel** cho một cột cụ thể  
> - Mẹo xử lý nhiều cột hơn hoặc các locale khác nhau  

> **Yêu cầu trước**  
> - .NET 6+ (hoặc .NET Framework 4.6+) đã được cài đặt  
> - Gói NuGet Aspose.Cells cho .NET (`Install-Package Aspose.Cells`)  
> - Kiến thức cơ bản về C# và DataTables  

---

## Bước 1: Chuẩn bị DataTable (import datatable to excel)

Đầu tiên, chúng ta cần một số dữ liệu mẫu. Trong một ứng dụng thực tế, bạn có thể sẽ điền bảng này từ truy vấn DB, nhưng một ví dụ được mã hoá cứng giúp mọi thứ đơn giản hơn.

```csharp
using System.Data;

// Create a DataTable with two columns: Product (string) and Price (double)
DataTable dataTable = new DataTable();
dataTable.Columns.Add("Product", typeof(string));
dataTable.Columns.Add("Price", typeof(double));

// Add a few rows – you can add as many as you like
dataTable.Rows.Add("Apple", 1.23);
dataTable.Rows.Add("Banana", 0.78);
dataTable.Rows.Add("Cherry", 2.50);
```

*Tại sao điều này quan trọng*: `DataTable` là cầu nối giữa dữ liệu kinh doanh của bạn và tệp Excel. Aspose.Cells có thể nhập trực tiếp, giữ nguyên tên cột và kiểu dữ liệu.

---

## Bước 2: Tạo một Workbook mới (create excel workbook c#)

Bây giờ chúng ta tạo đối tượng tệp Excel thực tế. Hãy nghĩ nó như một tấm canvas trống mà bạn sẽ vẽ lên.

```csharp
using Aspose.Cells;

// Instantiate a fresh workbook – this is the core of create excel workbook c#
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0). You could also add more sheets later.
Worksheet worksheet = workbook.Worksheets[0];
```

> **Mẹo chuyên nghiệp:** Nếu bạn cần nhiều sheet, gọi `workbook.Worksheets.Add()` và đặt tên có ý nghĩa cho mỗi sheet.

---

## Bước 3: Định nghĩa Style Tiền Tệ (format cells currency)

Aspose.Cells cho phép bạn tạo một đối tượng `Style` mô tả cách các ô sẽ hiển thị. Đối với tiền tệ, chúng ta sử dụng ID định dạng số tích hợp sẵn 164 (`"$#,##0.00"`).

```csharp
// Create a new style object for the price column
Style priceStyle = workbook.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format "$#,##0.00"
```

*Tại sao không chỉ đặt chuỗi định dạng?* Sử dụng ID tích hợp sẵn đảm bảo tính tương thích giữa các phiên bản Excel và tránh các vấn đề đặc thù của locale.

---

## Bước 4: Xây dựng Mảng Style (apply currency format column)

Khi nhập một `DataTable`, bạn có thể truyền một mảng các đối tượng `Style` — một cho mỗi cột. `null` có nghĩa là “sử dụng style mặc định”. Ở đây chúng ta áp dụng `priceStyle` chỉ cho cột thứ hai.

```csharp
// Column 0 (Product) gets the default style, Column 1 (Price) gets the currency style
Style[] columnStyles = { null, priceStyle };
```

Nếu sau này bạn thêm nhiều cột hơn, chỉ cần mở rộng mảng tương ứng. Độ dài của `columnStyles` phải khớp với số cột bạn đang nhập, nếu không Aspose sẽ ném ra một ngoại lệ.

---

## Bước 5: Nhập DataTable với Style (import datatable to excel)

Bây giờ phép màu xảy ra — `DataTable` của chúng ta được đưa vào worksheet, và cột giá ngay lập tức hiển thị dưới dạng tiền tệ.

```csharp
// Parameters:
//  - dataTable: source data
//  - true: include column headers
//  - startRow: 0 (top of sheet)
//  - startColumn: 0 (first column)
//  - columnStyles: style array defined above
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

*Nếu bạn có nhiều hơn hai cột thì sao?* Chỉ cần mở rộng `columnStyles` để mỗi cột nhận được style phù hợp (hoặc `null` cho mặc định). Đây là cách sạch nhất để **add number format excel** một cách chọn lọc.

---

## Bước 6: Lưu Workbook (create excel workbook c#)

Cuối cùng, chúng ta ghi tệp ra đĩa. Chọn bất kỳ thư mục nào bạn có quyền ghi.

```csharp
// Save the workbook as an XLSX file
workbook.Save("YOUR_DIRECTORY/StyledTable.xlsx");
```

Mở `StyledTable.xlsx` trong Excel và bạn sẽ thấy:

| Product | Price |
|---------|-------|
| Apple   | $1.23 |
| Banana  | $0.78 |
| Cherry  | $2.50 |

Cột **Price** đã được định dạng là tiền tệ — không cần bước nào thêm.

---

## Các Trường Hợp Đặc Biệt & Biến Thể

### Nhiều Cột, Định Dạng Khác

Nếu bạn cần **format cells currency** cho nhiều cột (ví dụ: Cost, Tax, Total), tạo một `Style` riêng cho mỗi cột và điền `columnStyles` cho phù hợp:

```csharp
Style costStyle = workbook.CreateStyle();
costStyle.Number = 164; // currency

Style taxStyle = workbook.CreateStyle();
taxStyle.Number = 164;

// Assuming columns: Product, Cost, Tax, Total
Style[] styles = { null, costStyle, taxStyle, priceStyle };
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, styles);
```

### Tiền Tệ Đặc Thù Theo Locale

Đối với Euro hoặc Bảng Anh, sử dụng các ID tích hợp khác (ví dụ, 165 cho `€#,##0.00`). Hoặc, đặt một chuỗi định dạng tùy chỉnh:

```csharp
priceStyle.Custom = "€#,##0.00";
```

### Tập Dữ Liệu Lớn

Aspose.Cells có thể xử lý hàng triệu dòng, nhưng việc tiêu thụ bộ nhớ tăng lên với các đối tượng style. Hãy tái sử dụng một thể hiện `Style` duy nhất cho tất cả các cột tiền tệ để giảm footprint.

### Thiếu Style

Nếu `columnStyles` ngắn hơn số cột, Aspose sẽ áp dụng style mặc định cho các cột còn lại. Điều này hữu ích khi bạn chỉ quan tâm đến một vài cột.

---

## Ví Dụ Hoàn Chỉnh (Tất Cả Các Bước Kết Hợp)

Dưới đây là chương trình hoàn chỉnh bạn có thể sao chép‑dán vào một ứng dụng console. Nó bao gồm tất cả các phần chúng ta đã thảo luận, cộng thêm một vài chú thích hữu ích.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Build sample DataTable (import datatable to excel)
        // -------------------------------------------------
        DataTable dataTable = new DataTable();
        dataTable.Columns.Add("Product", typeof(string));
        dataTable.Columns.Add("Price", typeof(double));
        dataTable.Rows.Add("Apple", 1.23);
        dataTable.Rows.Add("Banana", 0.78);
        dataTable.Rows.Add("Cherry", 2.50);
        // You can add as many rows as you like here.

        // -------------------------------------------------
        // Step 2: Create a new workbook (create excel workbook c#)
        // -------------------------------------------------
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // -------------------------------------------------
        // Step 3: Define a currency style (format cells currency)
        // -------------------------------------------------
        Style priceStyle = workbook.CreateStyle();
        priceStyle.Number = 164; // "$#,##0.00" – built‑in currency format

        // -------------------------------------------------
        // Step 4: Build the style array (apply currency format column)
        // -------------------------------------------------
        // First column gets default style (null), second column uses priceStyle.
        Style[] columnStyles = { null, priceStyle };

        // -------------------------------------------------
        // Step 5: Import the DataTable with the style array
        // -------------------------------------------------
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // -------------------------------------------------
        // Step 6: Save the workbook to disk
        // -------------------------------------------------
        string outputPath = @"YOUR_DIRECTORY\StyledTable.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Kết quả mong đợi:** Khi mở `StyledTable.xlsx` sẽ hiển thị cột `Price` với dấu đô la và hai chữ số thập phân, chính xác như hướng dẫn `format cells currency` yêu cầu.

---

## Câu Hỏi Thường Gặp

**Q: Điều này có hoạt động với .NET Core không?**  
A: Hoàn toàn có. Aspose.Cells tuân thủ .NET‑standard, vì vậy bạn có thể nhắm tới .NET 5, .NET 6 hoặc các phiên bản sau mà không cần thay đổi.

**Q: Nếu DataTable của tôi có 10 cột nhưng tôi chỉ muốn định dạng cột 5 thì sao?**  
A: Tạo một `Style[]` độ dài 10, điền các vị trí 0‑4 và 6‑9 bằng `null`, và đặt style tùy chỉnh của bạn ở chỉ mục 4 (đánh số từ 0). Aspose sẽ tôn trọng mỗi mục nhập.

**Q: Tôi có thể ẩn hàng tiêu đề không?**  
A: Sau khi nhập, đặt `worksheet.Cells.Rows[0].Hidden = true;` hoặc đơn giản truyền `false` cho tham số `includeColumnNames` trong `ImportDataTable`.

---

## Kết Luận

Chúng ta vừa **created an Excel workbook C#**, nhập một `DataTable`, và **applied a currency format column** bằng Aspose.Cells. Các bước chính — chuẩn bị dữ liệu, định nghĩa style, xây dựng mảng style, nhập bằng `ImportDataTable`, và lưu — bao phủ phần cốt lõi của hầu hết các tác vụ tự động hóa Excel.

Từ đây bạn có thể khám phá:
- **add number format excel** cho ngày tháng hoặc phần trăm  
- Xuất nhiều worksheet trong một tệp duy nhất  
- Sử dụng **format cells currency** với ký hiệu đặc thù theo locale  
- Tự động tạo biểu đồ dựa trên cùng một dữ liệu  

Hãy thử những điều trên, và bạn sẽ nhanh chóng trở thành người được mọi người nhờ tới cho báo cáo Excel trong đội. Có cách tiếp cận nào bạn muốn chia sẻ? Để lại bình luận bên dưới — chúc lập trình vui!

![ảnh chụp màn hình tạo workbook Excel C#](image.png "tạo workbook excel c#")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}