---
category: general
date: 2026-02-15
description: cách định dạng tiền tệ nhanh chóng bằng cách đặt định dạng số cho cột
  và áp dụng định dạng số tùy chỉnh trong C#. Học cách lấy cột theo tên và thiết lập
  căn chỉnh cột trong lưới.
draft: false
keywords:
- how to format currency
- set column number format
- apply custom numeric format
- retrieve column by name
- set grid column alignment
language: vi
og_description: Cách định dạng tiền tệ trong cột lưới bằng C#. Hướng dẫn này cho thấy
  cách lấy cột theo tên, thiết lập định dạng số cho cột, áp dụng định dạng số tùy
  chỉnh và căn chỉnh cột lưới.
og_title: Cách định dạng tiền tệ trong cột Grid – Hướng dẫn đầy đủ
tags:
- C#
- GridFormatting
- UI
title: Cách định dạng tiền tệ trong cột lưới – Hướng dẫn từng bước
url: /vi/net/number-and-display-formats-in-excel/how-to-format-currency-in-a-grid-column-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cách định dạng tiền tệ trong một cột Grid – Hướng dẫn lập trình đầy đủ

Bạn đã bao giờ tự hỏi **cách định dạng tiền tệ** trong một cột grid mà không phải rối rắm không? Bạn không phải là người duy nhất. Khi bạn nhìn vào một con số đơn giản như `1234.5` và mong muốn nó hiển thị một cách kỳ diệu thành `$1,234.50`, câu trả lời thường chỉ là vài dòng cấu hình.

Trong hướng dẫn này, chúng ta sẽ **lấy cột theo tên**, **đặt định dạng số cho cột**, và **áp dụng định dạng số tùy chỉnh** phù hợp với bố cục kế toán thông thường. Đồng thời, chúng ta sẽ **đặt căn chỉnh cho cột grid** và thêm một đường viền nhẹ để giao diện trông chuyên nghiệp hơn.

> **TL;DR** – Khi kết thúc, bạn sẽ có một đoạn mã sẵn sàng chạy, biến các số thập phân thô thành các giá trị tiền tệ được định dạng đẹp mắt trong bất kỳ điều khiển kiểu `GridJs` nào.

---

## Những gì bạn cần

- Một dự án .NET (bất kỳ phiên bản nào hỗ trợ C# 8.0+ – Visual Studio 2022 hoạt động tốt).  
- Một thành phần grid cung cấp bộ sưu tập `Columns` (ví dụ sử dụng lớp giả `GridJs`, nhưng các khái niệm này cũng áp dụng cho grid của DevExpress, Telerik, hoặc Syncfusion).  
- Kiến thức cơ bản về cú pháp C# – không cần các thủ thuật nâng cao.

Nếu bạn đã có những thứ trên, tuyệt vời. Nếu chưa, chỉ cần tạo một ứng dụng console; grid có thể được mô phỏng để minh họa.

---

## Triển khai từng bước

Dưới mỗi bước, bạn sẽ thấy một khối mã ngắn gọn, một giải thích ngắn về **lý do** dòng mã quan trọng, và một mẹo để tránh các lỗi thường gặp.

### ## Bước 1 – Lấy cột “Amount” theo tên

```csharp
// Step 1: Retrieve the "Amount" column from the grid
var amountColumn = gridJs.Columns["Amount"];
if (amountColumn == null)
{
    throw new InvalidOperationException("Column 'Amount' does not exist. Verify the column name or check the grid's schema.");
}
```

**Lý do quan trọng:**  
Hầu hết các API của grid cung cấp các cột thông qua một chỉ mục kiểu từ điển. Lấy cột bằng tên tiêu đề của nó (`"Amount"`) cho phép bạn thao tác giao diện mà không cần chạm vào nguồn dữ liệu gốc.

**Mẹo chuyên nghiệp:** Luôn kiểm tra giá trị trả về có phải `null` không – một lỗi đánh máy trong tên cột hoặc thay đổi schema động có thể gây ra `NullReferenceException` khi chạy.

---

### ## Bước 2 – Đặt định dạng số cho cột bằng mask tiền tệ tùy chỉnh

```csharp
// Step 2: Apply a custom numeric format for currency values
amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";
```

**Lý do quan trọng:**  
Chuỗi định dạng tuân theo quy tắc định dạng kế toán của Excel:

- `_(* #,##0.00_)` → Số dương, căn phải với một khoảng trống đầu cho ký hiệu tiền tệ.  
- `_(* (#,##0.00)` → Số âm được bao trong dấu ngoặc.  
- `_(* \"-\"??_)` → Giá trị zero hiển thị dưới dạng dấu gạch ngang.  
- `_(@_)` → Giá trị văn bản giữ nguyên.

Sử dụng **apply custom numeric format** cho phép bạn kiểm soát hoàn toàn dấu phân cách hàng nghìn, số chữ số thập phân, và vị trí của ký hiệu tiền tệ.

**Trường hợp đặc biệt:** Nếu ứng dụng của bạn cần hỗ trợ một locale khác (ví dụ Euro thay vì USD), thay khoảng trống đầu bằng ký hiệu phù hợp hoặc sử dụng định dạng dựa trên `CultureInfo` trong nguồn dữ liệu.

---

### ## Bước 3 – Căn chỉnh nội dung cột sang phải để dễ đọc

```csharp
// Step 3: Align the column contents to the right for better readability
amountColumn.Alignment = GridAlignment.Right;
```

**Lý do quan trọng:**  
Giá trị tiền tệ dễ dàng quét khi chúng được căn trên dấu phân cách thập phân. Đặt **set grid column alignment** thành `Right` giống như cách các bảng tính hiển thị dữ liệu tài chính.

**Cảnh báo:** Một số grid sẽ bỏ qua căn chỉnh trên các ô chứa template tùy chỉnh. Nếu bạn nhận thấy căn chỉnh không hoạt động, hãy kiểm tra lại xem cột có đang sử dụng renderer ô tùy chỉnh không.

---

### ## Bước 4 – Thêm một đường viền xám mỏng quanh các ô của cột

```csharp
// Step 4: Add a thin gray border around the column cells
amountColumn.Border = new GridBorder
{
    Color = Color.Gray,
    Style = BorderLineStyle.Thin
};
```

**Lý do quan trọng:**  
Một đường viền nhẹ giúp tách biệt cột “Amount” khỏi các cột lân cận, đặc biệt khi grid có màu nền hàng xen kẽ. Đây là tín hiệu trực quan cho thấy dữ liệu đại diện cho một con số tài chính riêng biệt.

**Mẹo:** Nếu bạn cần đường viền dày hơn cho mục đích in ấn, tăng `BorderLineStyle` lên `Medium` hoặc thay đổi `Color` thành `Color.Black`.

---

## Ví dụ hoàn chỉnh

Dưới đây là toàn bộ đoạn mã mà bạn có thể chèn vào dự án WinForms hoặc WPF sử dụng điều khiển kiểu `GridJs`. Ví dụ cũng in các giá trị đã định dạng ra console để bạn có thể kiểm tra kết quả mà không cần UI.

```csharp
using System;
using System.Drawing;   // For Color
using GridLibrary;      // Hypothetical namespace for GridJs

namespace GridCurrencyDemo
{
    class Program
    {
        static void Main()
        {
            // Create a mock grid and add a sample column
            var gridJs = new GridJs();
            gridJs.Columns.Add(new GridColumn
            {
                Name = "Amount",
                Header = "Amount",
                DataType = typeof(decimal)
            });

            // Populate some sample data
            gridJs.Rows.Add(new { Amount = 1234.5m });
            gridJs.Rows.Add(new { Amount = -567.89m });
            gridJs.Rows.Add(new { Amount = 0m });

            // ---- Formatting steps ------------------------------------------------
            // 1️⃣ Retrieve the "Amount" column
            var amountColumn = gridJs.Columns["Amount"]
                ?? throw new InvalidOperationException("Column 'Amount' not found.");

            // 2️⃣ Apply custom numeric format for currency
            amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";

            // 3️⃣ Right‑align the values
            amountColumn.Alignment = GridAlignment.Right;

            // 4️⃣ Add a thin gray border
            amountColumn.Border = new GridBorder
            {
                Color = Color.Gray,
                Style = BorderLineStyle.Thin
            };
            // -----------------------------------------------------------------------

            // Render the grid (in a real UI you would call gridJs.Render() or similar)
            Console.WriteLine("Formatted Currency Grid:");
            foreach (var row in gridJs.Rows)
            {
                var rawValue = (decimal)row.Amount;
                // The grid library would automatically apply NumberFormat when displaying.
                // For console demo we mimic the formatting:
                string formatted = rawValue.ToString("#,##0.00", System.Globalization.CultureInfo.InvariantCulture);
                if (rawValue < 0)
                    formatted = $"({formatted.TrimStart('-')})";
                else if (rawValue == 0)
                    formatted = "-";

                Console.WriteLine($"| {formatted,15} |");
            }

            // Keep console open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Kết quả mong đợi trên console**

```
Formatted Currency Grid:
|        1,234.50 |
|       (567.89) |
|               - |
```

Chú ý cách số dương được căn phải, số âm hiển thị trong ngoặc, và số zero hiển thị dấu gạch ngang – chính xác như chuỗi định dạng tùy chỉnh quy định.

---

## Câu hỏi thường gặp & Trường hợp đặc biệt

| Câu hỏi | Trả lời |
|----------|--------|
| *Nếu grid sử dụng một culture khác (ví dụ € thay vì $) thì sao?* | Thay khoảng trống đầu trong chuỗi định dạng bằng ký hiệu mong muốn hoặc để nguồn dữ liệu xuất ra chuỗi đã định dạng sẵn bằng `CultureInfo.CurrentCulture`. |
| *Có thể tái sử dụng cùng một định dạng cho nhiều cột không?* | Hoàn toàn có thể. Lưu chuỗi định dạng trong một hằng (`const string CurrencyMask = "...";`) và gán nó ở bất kỳ cột nào cần tiền tệ. |
| *Nếu cột chứa giá trị kiểu string thì sẽ ra sao?* | Chuỗi định dạng chỉ ảnh hưởng tới các kiểu số. Các chuỗi sẽ được truyền qua không thay đổi, vì vậy phần cuối của mask (`_(@_)`) tồn tại để bảo toàn nội dung không phải số. |
| *Có ảnh hưởng tới hiệu năng không?* | Rất nhỏ. Định dạng được áp dụng khi render, không phải khi truy xuất dữ liệu. Trừ khi bạn render hàng ngàn dòng mỗi khung, bạn sẽ không cảm nhận được chậm trễ. |
| *Làm sao để làm đường viền dày hơn cho báo cáo in?* | Thay `BorderLineStyle.Thin` bằng `BorderLineStyle.Medium` hoặc `BorderLineStyle.Thick`. Một số thư viện còn cho phép chỉ định độ rộng pixel trực tiếp. |

---

## Kết luận

Chúng ta đã đi qua **cách định dạng tiền tệ** trong một cột grid từ đầu đến cuối: lấy cột theo tên, đặt định dạng số cho cột, áp dụng định dạng số tùy chỉnh, căn chỉnh các ô, và thêm một đường viền tinh tế. Ví dụ hoàn chỉnh chạy ngay và hiển thị kết quả trực quan như mong đợi.

Nếu bạn muốn tiến xa hơn, hãy thử:

- **Văn hoá động** – chuyển đổi chuỗi định dạng dựa trên locale của người dùng.  
- **Conditional

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}