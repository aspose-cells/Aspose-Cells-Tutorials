---
category: general
date: 2026-03-18
description: Học cách áp dụng màu nền xen kẽ cho các hàng trong một bảng tính bằng
  C#. Bao gồm việc đặt màu nền cho hàng, thêm nền màu vàng nhạt và tô màu các hàng
  một cách xen kẽ.
draft: false
keywords:
- apply alternating row colors
- set row background color
- add light yellow background
- set alternating row shading
- color rows alternately
language: vi
og_description: Áp dụng màu nền xen kẽ cho các hàng trong C# để cải thiện khả năng
  đọc. Hướng dẫn này chỉ cách thiết lập màu nền cho hàng, thêm nền màu vàng nhạt và
  tô màu các hàng một cách xen kẽ.
og_title: Áp dụng màu nền xen kẽ cho các hàng trong C# – Hướng dẫn chi tiết
tags:
- C#
- DataTable
- Spreadsheet styling
- UI design
title: Áp dụng màu nền xen kẽ cho các hàng trong C# – Hướng dẫn từng bước
url: /vi/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Áp dụng màu nền xen kẽ cho các hàng trong C# – Hướng dẫn đầy đủ

Bạn đã bao giờ cần **áp dụng màu nền xen kẽ cho các hàng** trong một bảng dữ liệu nhưng không biết bắt đầu từ đâu? Bạn không phải là người duy nhất — hầu hết các lập trình viên đều gặp khó khăn này khi lần đầu muốn làm cho bảng trông thân thiện hơn. Tin tốt là gì? Chỉ với vài dòng C# bạn đã có thể **đặt màu nền cho hàng**, thêm **nền màu vàng nhạt**, và tạo ra một lưới gọn gàng giúp cải thiện khả năng đọc ngay lập tức.

Trong tutorial này, chúng ta sẽ đi qua toàn bộ quy trình, từ việc lấy một `DataTable` vào bộ nhớ tới việc tạo kiểu cho mỗi hàng với dải màu vàng‑trắng nhẹ. Khi kết thúc, bạn sẽ tự tin **tô màu các hàng xen kẽ**, đồng thời sẽ thấy một vài biến thể hữu ích cho các trường hợp cần màu sắc khác hoặc chủ đề động.

## Những gì bạn cần

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có sẵn các yếu tố sau:

- Một dự án .NET nhắm tới .NET 6 hoặc mới hơn (mã cũng hoạt động trên .NET Framework 4.7+).  
- Thư viện bảng tính hỗ trợ các đối tượng style – ví dụ trong tutorial dùng API chung `Workbook`/`Worksheet` tương tự như **Aspose.Cells**, **GemBox.Spreadsheet**, hoặc **ClosedXML**.  
- Một nguồn `DataTable` – có thể đến từ truy vấn cơ sở dữ liệu, nhập CSV, hoặc bất kỳ bộ sưu tập trong bộ nhớ nào.  

Không cần thêm gói NuGet nào ngoài thư viện bảng tính đã dùng. Nếu bạn dùng Aspose.Cells, không gian tên là `Aspose.Cells`; với ClosedXML là `ClosedXML.Excel`. Hãy thay đổi các lời gọi `CreateStyle` và `ImportDataTable` cho phù hợp.

## Bước 1: Lấy dữ liệu nguồn dưới dạng DataTable

Đầu tiên, hãy lấy dữ liệu bạn muốn hiển thị. Trong các ứng dụng thực tế, thường là truy vấn cơ sở dữ liệu, nhưng để minh bạch chúng ta sẽ tạo một phương thức trợ giúp tên `GetData()` trả về một `DataTable` đã được điền dữ liệu.

```csharp
// Step 1: Retrieve the source data as a DataTable
DataTable dataTable = GetData();   // Replace with your actual data retrieval logic
```

> **Tại sao điều này quan trọng:** `DataTable` xác định các hàng và cột sẽ nhận được màu nền xen kẽ. Nếu bảng rỗng, sẽ không có gì để tạo kiểu, vì vậy luôn kiểm tra `Rows.Count` > 0 trước khi tiếp tục.

### Mẹo chuyên nghiệp
Nếu bạn lấy dữ liệu từ Entity Framework, có thể dùng `DataTable.Load(reader)` sau khi thực thi một `SqlCommand`. Cách này giúp mã gọn gàng và tránh việc định nghĩa cột thủ công.

## Bước 2: Cấp phát một mảng để chứa Style cho mỗi hàng

Tiếp theo, chúng ta cần một container có số phần tử bằng số hàng. Hầu hết các API bảng tính cho phép truyền một mảng style vào phương thức import, vì vậy chúng ta sẽ tạo một `Style[]` có kích thước đúng bằng số hàng.

```csharp
// Step 2: Allocate an array to hold a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];
```

> **Giải thích:** Bằng cách cấp phát trước mảng, chúng ta tránh việc tạo mới một đối tượng style ở mỗi vòng lặp, giúp cải thiện hiệu năng khi xử lý hàng ngàn dòng.

## Bước 3: Áp dụng màu nền xen kẽ (Vàng nhạt / Trắng)

Bây giờ là phần cốt lõi: **áp dụng màu nền xen kẽ cho các hàng**. Chúng ta sẽ duyệt qua từng hàng, tạo một instance style mới từ workbook, và đặt nền dựa trên chỉ số hàng. Các hàng chẵn sẽ có nền màu vàng nhạt, các hàng lẻ giữ màu trắng.

```csharp
// Step 3: Create alternating background colors (light yellow / white) for the rows
for (int rowIndex = 0; rowIndex < dataTable.Rows.Count; rowIndex++)
{
    // Create a new style instance from the workbook
    rowStyles[rowIndex] = wb.CreateStyle();

    // Apply a light yellow background to even rows, white to odd rows
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow   // add light yellow background
        : Color.White;        // set row background color to white

    rowStyles[rowIndex].Pattern = BackgroundType.Solid; // set alternating row shading
}
```

### Tại sao cách này hoạt động
- **`rowIndex % 2 == 0`** kiểm tra xem hàng có phải là chẵn hay không.  
- **`Color.LightYellow`** cung cấp một tông màu nhẹ, không gây rối mắt, rất phù hợp cho bảng dữ liệu.  
- **`BackgroundType.Solid`** đảm bảo màu nền phủ toàn bộ ô, đạt được hiệu ứng **đặt màu nền cho hàng**.  

Bạn có thể thay `Color.LightYellow` bằng bất kỳ màu nào khác (ví dụ `Color.LightCyan`) nếu muốn một giao diện khác. Logic này cũng cho phép bạn **tô màu các hàng xen kẽ** dựa trên các tiêu chí khác, chẳng hạn như cờ trạng thái.

## Bước 4: Nhập DataTable vào Worksheet với các Style đã chuẩn bị

Cuối cùng, chúng ta đưa mọi thứ vào worksheet. Hầu hết các thư viện cung cấp một overload `ImportDataTable` chấp nhận một mảng style. Tham số `true` chỉ thị API ghi tiêu đề cột, và tọa độ `0, 0` bắt đầu từ ô trên‑trái.

```csharp
// Step 4: Import the DataTable into the worksheet, applying the prepared row styles
ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

> **Kết quả:** Worksheet giờ hiển thị dữ liệu của bạn với mẫu **tô màu nền xen kẽ cho các hàng**—vàng nhạt cho các hàng chẵn, trắng cho các hàng lẻ. Người dùng có thể quét bảng mà không cần mắt di chuyển quá nhiều.

### Kết quả mong đợi
Nếu bạn mở bảng tính đã tạo, sẽ thấy dạng như sau:

| ID | Name      | Quantity |
|----|-----------|----------|
| **1** | Apple      | 50       |
| **2** | Banana     | 30       |
| **3** | Cherry     | 20       |
| **4** | Date       | 15       |

Các hàng 1, 3, 5… có **nền màu vàng nhạt**, trong khi các hàng 2, 4, 6… giữ **màu trắng**. Hàng tiêu đề (hàng 0) kế thừa style mặc định trừ khi bạn tùy chỉnh riêng.

## Các biến thể tùy chọn & Trường hợp đặc biệt

### 1. Sử dụng bảng màu khác
Nếu màu vàng nhạt không phù hợp với thương hiệu, chỉ cần thay `Color.LightYellow` bằng một `System.Drawing.Color` khác. Đối với chủ đề xanh‑xám, bạn có thể dùng:

```csharp
rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
    ? Color.FromArgb(220, 235, 247) // soft blue
    : Color.White;
```

### 2. Tô nền động dựa trên dữ liệu
Đôi khi bạn muốn làm nổi bật các hàng thỏa mãn một điều kiện (ví dụ: tồn kho thấp). Kết hợp kiểm tra modulo với một kiểm tra tùy chỉnh:

```csharp
int quantity = Convert.ToInt32(dataTable.Rows[rowIndex]["Quantity"]);
if (quantity < 20)
{
    rowStyles[rowIndex].ForegroundColor = Color.Salmon; // urgent low‑stock color
}
else
{
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow
        : Color.White;
}
```

### 3. Áp dụng Style chỉ cho một số cột
Nếu bạn chỉ cần **đặt màu nền cho hàng** trên một số cột nhất định, hãy tạo một style riêng cho mỗi cột và gán nó sau khi import bằng API phạm vi ô của worksheet.

```csharp
// Example for column B only
var colBStyle = wb.CreateStyle();
colBStyle.ForegroundColor = Color.LightYellow;
colBStyle.Pattern = BackgroundType.Solid;

// Apply after import
ws.Cells[$"B2:B{dataTable.Rows.Count + 1}"].SetStyle(colBStyle);
```

### 4. Mẹo hiệu năng cho bảng lớn
Khi làm việc với > 10.000 hàng, hãy cân nhắc tái sử dụng một đối tượng style duy nhất cho mỗi màu thay vì tạo mới cho mỗi hàng. Mảng sẽ chỉ chứa các tham chiếu tới hai style chia sẻ, giảm đáng kể việc sử dụng bộ nhớ.

```csharp
Style yellowStyle = wb.CreateStyle();
yellowStyle.ForegroundColor = Color.LightYellow;
yellowStyle.Pattern = BackgroundType.Solid;

Style whiteStyle = wb.CreateStyle();
whiteStyle.ForegroundColor = Color.White;
whiteStyle.Pattern = BackgroundType.Solid;

for (int i = 0; i < dataTable.Rows.Count; i++)
    rowStyles[i] = (i % 2 == 0) ? yellowStyle : whiteStyle;
```

## Ví dụ hoàn chỉnh

Dưới đây là một chương trình tự chứa bạn có thể dán vào một console app. Nó sử dụng API giả `Workbook`/`Worksheet`; hãy thay thế các kiểu này bằng những kiểu từ thư viện bạn đang dùng.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using YourSpreadsheetLib;     // Replace with actual namespace

class Program
{
    static void Main()
    {
        // Initialize workbook & worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Step 1: Retrieve data
        DataTable dataTable = GetData();

        // Step 2: Allocate style array
        Style[] rowStyles = new Style[dataTable.Rows.Count];

        // Step 3: Apply alternating row colors
        for (int i = 0; i < dataTable.Rows.Count; i++)
        {
            rowStyles[i] = wb.CreateStyle();
            rowStyles[i].ForegroundColor = (i % 2 == 0)
                ? Color.LightYellow   // add light yellow background
                : Color.White;        // set row background color
            rowStyles[i].Pattern = BackgroundType.Solid; // set alternating row shading
        }

        // Step 4: Import with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // Save to file
        wb.Save("AlternatingRows.xlsx");
        Console.WriteLine("Workbook saved with alternating row colors.");
    }

    // Sample data generator
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Quantity", typeof(int));

        dt.Rows.Add(1, "Apple", 50);
        dt.Rows.Add(2, "Banana", 30);
        dt.Rows.Add(3, "Cherry", 20);
        dt.Rows.Add(4, "Date", 15);
        dt.Rows.Add(5, "Elderberry", 5);
        return dt;
    }
}
```

**Kết quả:** Một tệp có tên `AlternatingRows.xlsx` trong đó mỗi hàng xen kẽ giữa nền màu vàng nhạt và trắng, giúp bảng dễ nhìn hơn.

## Câu hỏi thường gặp

**Hỏi: Phương pháp này có hoạt động với định dạng có điều kiện kiểu Excel không?**  
Đáp: Có. Nếu thư viện của bạn hỗ trợ quy tắc có điều kiện, bạn có thể chuyển cùng một logic thành một quy tắc kiểm tra `MOD(ROW(),2)=0`. Phương pháp dựa trên mã được trình bày ở đây lại di động hơn đối với các thư viện không có tính năng định dạng có điều kiện tích hợp.

**Hỏi: Nếu tôi cần **tô màu các hàng xen kẽ** trong một bảng PDF thay vì bảng Excel thì sao?**  
Đáp: Hầu hết các trình tạo bảng PDF (ví dụ iTextSharp, PdfSharp) cho phép bạn đặt `BackgroundColor` cho mỗi hàng. Công thức modulo tương tự vẫn áp dụng—

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}