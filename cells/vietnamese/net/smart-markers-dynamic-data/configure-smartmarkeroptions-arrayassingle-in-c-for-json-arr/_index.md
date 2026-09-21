---
category: general
date: 2026-09-21
description: Cấu hình SmartMarkerOptions ArrayAsSingle trong C# để xuất các mảng JSON
  dưới dạng một giá trị ô duy nhất trong workbook Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- configure smartmarkeroptions arrayassingle
- Aspose.Cells smart markers
- export JSON array
- C# DataTable
- Workbook ProcessSmartMarkers
language: vi
lastmod: 2026-09-21
og_description: Cấu hình SmartMarkerOptions ArrayAsSingle trong C# để xuất các mảng
  JSON dưới dạng một giá trị ô duy nhất. Tìm hiểu giải pháp chi tiết từng bước.
og_image_alt: Screenshot of an Excel sheet showing a JSON array stored in a single
  cell after using SmartMarkerOptions
og_title: Cấu hình SmartMarkerOptions ArrayAsSingle trong C# – hướng dẫn đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Configure SmartMarkerOptions ArrayAsSingle in C# to export JSON arrays
    as a single cell value in an Excel workbook.
  headline: Configure SmartMarkerOptions ArrayAsSingle in C# for JSON arrays
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cấu hình SmartMarkerOptions ArrayAsSingle trong C# cho các mảng JSON
url: /vi/net/smart-markers-dynamic-data/configure-smartmarkeroptions-arrayassingle-in-c-for-json-arr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cấu hình SmartMarkerOptions ArrayAsSingle trong C# cho các mảng JSON

Nếu bạn cần **cấu hình SmartMarkerOptions ArrayAsSingle** khi tạo tệp Excel bằng Aspose.Cells, hướng dẫn này sẽ chỉ cho bạn cách thực hiện chính xác. Bạn sẽ thấy cách giữ nguyên một mảng JSON trong một ô thay vì phân tán các phần tử của nó ra nhiều hàng.

Làm việc với dữ liệu JSON trong bảng tính thường đồng nghĩa với việc lựa chọn giữa một dạng hiển thị phẳng và một biểu diễn gọn gàng. Trong nhiều trường hợp báo cáo—như lưu trữ danh sách thẻ hoặc một tập hợp các định danh—bạn muốn toàn bộ chuỗi JSON ở trong một ô duy nhất. Cờ **ArrayAsSingle** trong `SmartMarkerOptions` giúp thực hiện điều đó.

Trong tutorial này bạn sẽ:

* Tạo một `DataTable` chứa mảng JSON trong một cột.
* Đặt Smart Markers vào một worksheet Excel.
* **Cấu hình SmartMarkerOptions ArrayAsSingle** để mảng JSON được xử lý như một giá trị ô duy nhất.
* Xử lý các marker và lưu workbook.
* Xác minh kết quả.

> **Prerequisites** – Bạn cần thư viện Aspose.Cells cho .NET (v23.12 trở lên) và môi trường phát triển .NET (Visual Studio 2022 được khuyến nghị). Kiến thức cơ bản về C# và DataTables được giả định.

---

## Bước 1: Chuẩn bị nguồn dữ liệu với một mảng JSON

Đầu tiên, xây dựng một `DataTable` mô phỏng dữ liệu bạn sẽ nhận được từ dịch vụ hoặc cơ sở dữ liệu. Cột **Names** chứa một chuỗi đã được mã hoá JSON đại diện cho một mảng các tên.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable dataTable = new DataTable();
dataTable.Columns.Add("Id", typeof(int));
dataTable.Columns.Add("Names", typeof(string));

// Store the JSON array as a plain string
dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");
```

*Tại sao cần bước này?*  
Smart Markers đọc dữ liệu trực tiếp từ các đối tượng .NET. Bằng cách đặt mảng JSON trong một cột kiểu chuỗi, bạn giữ nguyên cú pháp JSON, sau này có thể ghi vào ô mà không bị thay đổi.

---

## Bước 2: Chèn Smart Markers vào một workbook mới

Tạo một workbook mới, chọn worksheet đầu tiên, và viết Smart Markers tham chiếu toàn bộ bảng và cột **Names** cụ thể.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Smart marker for the entire table (optional, shown for completeness)
worksheet.Cells["A1"].PutValue("&=dataTable");

// Smart marker that targets only the Names column
worksheet.Cells["A2"].PutValue("&=dataTable.Names");
```

Marker `&=dataTable.Names` nói với Aspose.Cells thay thế ô bằng giá trị của cột **Names** cho mỗi hàng trong `dataTable`. Vì chúng ta chỉ có một hàng, marker sẽ được xử lý một lần.

---

## Bước 3: **Cấu hình SmartMarkerOptions ArrayAsSingle**

Mặc định, Aspose.Cells sẽ mở rộng một chuỗi dạng mảng thành các hàng riêng biệt. Đặt `ArrayAsSingle` thành `true` sẽ ghi đè hành vi này, buộc toàn bộ chuỗi JSON ở lại trong một ô duy nhất.

```csharp
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    // Export the JSON array as a single cell value
    ArrayAsSingle = true
};
```

*Tại sao bật `ArrayAsSingle`?*  
Khi `ArrayAsSingle` là `false`, engine sẽ hiểu `["Alice","Bob"]` là hai giá trị riêng biệt và ghi chúng vào các hàng liền kề. Đặt thành `true` sẽ coi chuỗi này là một giá trị nguyên tử, điều cần thiết để bảo toàn định dạng JSON trong Excel.

---

## Bước 4: Xử lý Smart Markers với các tùy chọn đã cấu hình

Bây giờ chạy engine Smart Marker, truyền đối tượng tùy chọn mà bạn vừa cấu hình.

```csharp
// Process smart markers using the custom options
workbook.ProcessSmartMarkers(smartMarkerOptions);
```

Trong quá trình xử lý, Aspose.Cells đọc `dataTable`, áp dụng các marker và tôn trọng cờ `ArrayAsSingle`, để nguyên mảng JSON không bị thay đổi.

---

## Bước 5: Lưu workbook và xác minh kết quả

Cuối cùng, ghi workbook ra đĩa. Mở tệp đã tạo trong Excel hoặc bất kỳ trình xem bảng tính nào để xác nhận ô **A2** chứa đúng chuỗi JSON.

```csharp
// Save the resulting workbook
string outputPath = @"C:\Temp\SmartMarkerJson.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### Kết quả mong đợi

| A   |
|-----|
| **["Alice","Bob"]** |

Ô **A2** hiển thị mảng JSON dưới dạng một giá trị văn bản duy nhất, giống như đã lưu trong `DataTable`. Không có hàng phụ nào được tạo ra.

---

## Các biến thể phổ biến và xử lý trường hợp đặc biệt

| Tình huống | Cách thích ứng |
|-----------|----------------|
| **Nhiều hàng với các mảng JSON** | Cài đặt `ArrayAsSingle` vẫn hoạt động; mỗi mảng JSON của hàng sẽ ở trong ô riêng của nó. |
| **Cấu trúc JSON khác nhau (đối tượng, mảng lồng nhau)** | Miễn là JSON ở dạng chuỗi, `ArrayAsSingle` sẽ giữ nguyên. Đối với các đối tượng phức tạp bạn có thể cần escape dấu ngoặc kép. |
| **Sử dụng nguồn dữ liệu khác (ví dụ List\<T\>)** | Thay thế `DataTable` bằng bất kỳ collection nào có thể lặp; cú pháp marker (`&=myList.Property`) vẫn giữ nguyên. |
| **Xuất ra CSV thay vì XLSX** | `ArrayAsSingle` vẫn áp dụng, nhưng nhớ rằng CSV không giữ định dạng ô; bạn có thể cần bao quanh JSON bằng dấu ngoặc kép. |

**Mẹo:** Luôn đặt `ArrayAsSingle` *trước* khi gọi `ProcessSmartMarkers`. Thay đổi cờ sau khi xử lý sẽ không ảnh hưởng tới các ô đã được tạo.

---

## Ví dụ đầy đủ, có thể chạy được

Dưới đây là chương trình hoàn chỉnh bạn có thể sao chép‑dán vào một ứng dụng console. Nó bao gồm tất cả các `using` directive và chú thích để dễ hiểu.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the data source with a JSON array
            DataTable dataTable = new DataTable();
            dataTable.Columns.Add("Id", typeof(int));
            dataTable.Columns.Add("Names", typeof(string));
            dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");

            // 2️⃣ Build a workbook and place smart markers
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Cells["A1"].PutValue("&=dataTable");          // whole table (optional)
            worksheet.Cells["A2"].PutValue("&=dataTable.Names");   // Names column

            // 3️⃣ Configure SmartMarkerOptions to treat arrays as single values
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 4️⃣ Process the markers with the custom options
            workbook.ProcessSmartMarkers(options);

            // 5️⃣ Save the file
            string path = @"C:\Temp\SmartMarkerJson.xlsx";
            workbook.Save(path);
            Console.WriteLine($"Workbook saved to {path}");
        }
    }
}
```

Chạy chương trình, mở `SmartMarkerJson.xlsx`, và bạn sẽ thấy mảng JSON được giữ nguyên trong ô **A2**.

---

## Kết luận

Bạn đã biết cách **cấu hình SmartMarkerOptions ArrayAsSingle** trong C# để giữ một mảng JSON làm giá trị ô duy nhất khi sử dụng smart markers của Aspose.Cells. Các bước—chuẩn bị `DataTable`, chèn marker, thiết lập cờ `ArrayAsSingle`, xử lý và lưu—tạo thành một mẫu lặp lại mà bạn có thể áp dụng cho bất kỳ kịch bản nào cần biểu diễn JSON gọn gàng trong Excel.

Tiếp theo, bạn có thể khám phá:

* **Smart markers của Aspose.Cells** để lặp qua các collection.
* Xuất **đối tượng JSON lồng nhau** bằng cách tùy chỉnh định dạng ô.
* Kết hợp **định dạng có điều kiện** với smart markers để tạo báo cáo phong phú hơn.

Hãy thử nghiệm với các cấu trúc dữ liệu khác nhau và chia sẻ những phát hiện của bạn. Chúc lập trình vui vẻ!

## Bạn Nên Học Gì Tiếp Theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã mẫu đầy đủ với các giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Create Excel Workbook from JSON – Complete Aspose.Cells Guide](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Create Configure Excel Workbook Aspose Cells Net](/cells/hindi/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Create Configure Excel Workbook Aspose Cells Net](/cells/german/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}