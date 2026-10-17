---
category: general
date: 2026-02-26
description: Áp dụng định dạng số trong Excel nhanh chóng và học cách định dạng cột
  thành tiền tệ, thiết lập định dạng số cho cột, và đặt màu phông chữ cho cột chỉ
  trong vài dòng C#.
draft: false
keywords:
- apply number format excel
- format column as currency
- set column number format
- format currency column
- set column font color
language: vi
og_description: Áp dụng định dạng số trong Excel bằng C# với các bước đơn giản. Học
  cách định dạng cột dưới dạng tiền tệ, thiết lập định dạng số cho cột và đặt màu
  phông chữ cho cột để tạo bảng tính chuyên nghiệp.
og_title: Áp dụng định dạng số trong Excel – Hướng dẫn toàn diện về định dạng cột
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: Áp dụng định dạng số trong Excel – Hướng dẫn từng bước để định dạng các cột
url: /vi/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# apply number format excel – Cách Định Dạng Cột Excel trong C#

Bạn đã bao giờ tự hỏi làm thế nào để **apply number format excel** khi bạn đang lặp qua một `DataTable`? Bạn không phải là người duy nhất. Hầu hết các nhà phát triển gặp khó khăn khi họ cần tiêu đề màu xanh *và* một cột định dạng tiền tệ trong cùng một thao tác nhập. Tin tốt là gì? Với vài dòng C# và các đối tượng style phù hợp, bạn có thể thực hiện mà không cần xử lý sau trên bảng tính.

Trong tutorial này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, có thể chạy được, cho thấy cách **format column as currency**, **set column number format** cho bất kỳ cột nào khác, và thậm chí **set column font color** cho tiêu đề. Khi kết thúc, bạn sẽ có một mẫu có thể tái sử dụng và chèn vào bất kỳ dự án Aspose.Cells (hoặc tương tự) nào.

## Những Điều Bạn Sẽ Học

- Cách lấy một `DataTable` và ánh xạ mỗi cột tới một `Style` cụ thể.
- Các bước chính xác để **apply number format excel** bằng cách sử dụng `Worksheet.Cells.ImportDataTable`.
- Tại sao việc tạo style trước sẽ hiệu quả hơn so với định dạng từng ô một.
- Xử lý các trường hợp biên khi bảng nguồn có nhiều cột hơn số style bạn đã định nghĩa.
- Một mẫu mã đầy đủ, sẵn sàng sao chép‑dán mà bạn có thể chạy ngay hôm nay.

> **Prerequisite:** Hướng dẫn này giả định bạn đã tham chiếu Aspose.Cells cho .NET (hoặc bất kỳ thư viện nào cung cấp các API `Workbook`, `Worksheet`, `Style`) trong dự án của mình. Nếu bạn đang dùng thư viện khác, các khái niệm vẫn áp dụng trực tiếp—chỉ cần thay thế tên kiểu.

---

## Step 1: Retrieve the Source Data as a DataTable

Trước khi thực hiện bất kỳ việc định dạng nào, bạn cần dữ liệu thô. Trong hầu hết các tình huống thực tế, dữ liệu nằm trong cơ sở dữ liệu, CSV hoặc một API. Để minh bạch, chúng ta sẽ mô phỏng một `DataTable` đơn giản với hai cột: *Product* (string) và *Price* (decimal).

```csharp
using System;
using System.Data;
using Aspose.Cells;
using System.Drawing;

public static DataTable GetData()
{
    var dt = new DataTable();
    dt.Columns.Add("Product", typeof(string));
    dt.Columns.Add("Price", typeof(decimal));

    dt.Rows.Add("Apple", 1.25m);
    dt.Rows.Add("Banana", 0.75m);
    dt.Rows.Add("Cherry", 2.10m);

    return dt;
}
```

> **Why this matters:** Việc kéo dữ liệu vào một `DataTable` cung cấp cho bạn một biểu diễn dạng bảng, trong bộ nhớ mà `ImportDataTable` có thể tiêu thụ trực tiếp, loại bỏ nhu cầu chèn ô‑bằng‑ô thủ công.

## Step 2: Create an Array of Styles – One per Column

Phương thức overload `ImportDataTable` mà chúng ta sẽ dùng chấp nhận một mảng các đối tượng `Style`. Mỗi phần tử tương ứng với một chỉ số cột. Nếu bạn để một phần tử là `null`, cột sẽ kế thừa style mặc định của workbook.

```csharp
// Initialize the workbook (Aspose.Cells)
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Prepare the style array based on the number of columns
DataTable dataTable = GetData();
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

> **Pro tip:** Khai báo mảng *sau* khi bạn đã có `DataTable` sẽ đảm bảo kích thước khớp chính xác, ngăn ngừa `IndexOutOfRangeException` sau này.

## Step 3: Set Column Font Color (Blue) for the First Column

Một yêu cầu phổ biến là làm nổi bật tiêu đề hoặc các cột quan trọng bằng màu phông chữ riêng. Ở đây chúng ta sẽ làm cho văn bản của cột đầu tiên màu xanh.

```csharp
// Style for the first column – blue font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = Color.Blue;
```

> **Why use a style object?** Style có thể tái sử dụng và được áp dụng hàng loạt, nhanh hơn rất nhiều so với việc lặp qua từng ô sau khi nhập. Workbook sẽ lưu cache style một lần, sau đó tái sử dụng cho mọi ô trong cột đó.

## Step 4: Format the Second Column as Currency

Các định dạng số tích hợp sẵn trong Excel được xác định bằng một chỉ số. `14` tương ứng với định dạng tiền tệ mặc định (ví dụ: `$1,234.00`). Nếu bạn cần một định dạng tùy chỉnh, bạn có thể gán một chuỗi định dạng thay thế.

```csharp
// Style for the second column – built‑in currency format (ID 14)
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].Number = 14; // 14 = built‑in currency format
```

> **Edge case:** Nếu workbook của bạn sử dụng locale mà ký hiệu tiền tệ không phải là `$`, cùng một chỉ số sẽ tự động điều chỉnh (ví dụ, `€` cho locale Đức).

## Step 5: Import the DataTable with the Defined Styles

Bây giờ chúng ta kết hợp mọi thứ lại. Phương thức `ImportDataTable` sẽ dán dữ liệu bắt đầu từ ô `A1` (hàng 0, cột 0) và áp dụng các style đã chuẩn bị.

```csharp
// Import the DataTable into the worksheet, applying the column styles
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

- Tham số thứ hai `true` thông báo cho Aspose.Cells rằng hàng đầu tiên của `DataTable` là tiêu đề cột.
- Tọa độ `0, 0` chỉ ra góc trên‑trái nơi việc nhập bắt đầu.
- `columnStyles` ánh xạ mỗi cột tới style tương ứng của nó.

## Step 6: Save the Workbook (Optional, but Handy for Verification)

Nếu bạn muốn xem kết quả trong Excel, chỉ cần lưu workbook ra đĩa. Bước này không bắt buộc cho logic định dạng, nhưng rất hữu ích để debug.

```csharp
// Save the workbook to a file
workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved as StyledReport.xlsx");
```

### Kết Quả Dự Kiến

| **Product** (phông màu xanh) | **Price** (tiền tệ) |
|------------------------------|----------------------|
| Apple                        | $1.25                |
| Banana                       | $0.75                |
| Cherry                       | $2.10                |

- Cột *Product* hiển thị màu xanh, giúp nó nổi bật.
- Cột *Price* hiển thị giá trị với ký hiệu tiền tệ mặc định và hai chữ số thập phân.

---

## Câu Hỏi Thường Gặp & Các Biến Thể

### Làm thế nào để **set column number format** cho hơn hai cột?

Chỉ cần mở rộng mảng `columnStyles`. Ví dụ, để hiển thị phần trăm ở cột thứ ba:

```csharp
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Number = 10; // 10 = built‑in percentage format
```

### Nếu tôi cần một định dạng tiền tệ *tùy chỉnh*, như “USD 1,234.00”?

Thay thế thuộc tính `Number` bằng một chuỗi định dạng:

```csharp
columnStyles[1].Custom = "\"USD\" #,##0.00";
```

### Tôi có thể áp dụng **set column font color** cho một cột số mà không ảnh hưởng tới định dạng số không?

Chắc chắn rồi. Style có thể kết hợp. Bạn có thể đặt cả `Font.Color` và `Number` trên cùng một instance `Style`:

```csharp
columnStyles[3] = workbook.CreateStyle();
columnStyles[3].Font.Color = Color.Green;
columnStyles[3].Number = 2; // 2 = built‑in date format (just an example)
```

### Điều gì sẽ xảy ra nếu `DataTable` có nhiều cột hơn số style?

Bất kỳ cột nào không có style rõ ràng (`null` entry) sẽ kế thừa style mặc định của workbook. Để tránh các `null` vô tình, bạn có thể khởi tạo toàn bộ mảng bằng một style cơ bản trước:

```csharp
Style defaultStyle = workbook.CreateStyle();
defaultStyle.Font.Size = 11;
for (int i = 0; i < columnStyles.Length; i++)
    columnStyles[i] = defaultStyle;
```

Sau đó chỉ ghi đè các cột bạn quan tâm.

### Cách tiếp cận này có hoạt động với bộ dữ liệu lớn (hơn 10k dòng) không?

Có. Vì việc định dạng được áp dụng *một lần cho mỗi cột* trước khi nhập, thao tác vẫn giữ độ phức tạp O(N) theo số dòng, và mức sử dụng bộ nhớ vẫn thấp. Tránh lặp qua từng ô sau khi nhập—đó là nơi hiệu năng giảm sút.

---

## Full Working Example (Copy‑Paste Ready)

```csharp
using System;
using System.Data;
using System.Drawing;
using Aspose.Cells;

class ExcelStyler
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 3️⃣ Prepare style array (one per column)
        Style[] columnStyles = new Style[dataTable.Columns.Count];

        // 4️⃣ Style first column – blue font
        columnStyles[0] = workbook.CreateStyle();
        columnStyles[0].Font.Color = Color.Blue;

        // 5️⃣ Style second column – built‑in currency format (ID 14)
        columnStyles[1] = workbook.CreateStyle();
        columnStyles[1].Number = 14;

        // 6️⃣ (Optional) Add more styles here – e.g., percentage, custom formats

        // 7️⃣ Import the DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // 8️⃣ Save to file for verification
        workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
        Console.WriteLine("Excel file created: StyledReport.xlsx");
    }

    // Helper method to mock data
    public static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Price", typeof(decimal));

        dt.Rows.Add("Apple", 1.25m);
        dt.Rows.Add("Banana", 0.75m);
        dt.Rows.Add("Cherry", 2.10m);
        return dt;
    }
}
```

Chạy chương trình, mở `StyledReport.xlsx`, và bạn sẽ thấy kết quả **apply number format excel** ngay lập tức.

---

## Conclusion

Chúng ta vừa trình diễn một cách sạch sẽ, hiệu quả để **apply number format excel** cho một `DataTable` được nhập. Bằng cách chuẩn bị một mảng `Style[]` từ trước, bạn có thể **format column as currency**, **set column number format**, và **set column font color** trong một lần gọi—không cần xử lý sau.

Hãy tự do mở rộng mẫu: thêm định dạng có điều kiện, hợp nhất các ô cho tiêu đề, hoặc thậm chí chèn công thức. Các nguyên tắc vẫn áp dụng, giữ cho mã của bạn gọn gàng và bảng tính trông chuyên nghiệp.

---

### Điều Sắp Đến?

- Khám phá **conditional formatting** để làm nổi bật các giá trị vượt qua ngưỡng.
- Kết hợp kỹ thuật này với **pivot table generation** cho báo cáo động.
- Thử **setting column number format** cho ngày tháng, phần trăm, hoặc ký hiệu khoa học tùy chỉnh.

Bạn đã thử một biến thể nào? Hãy chia sẻ trong phần bình luận—let’s keep the

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}