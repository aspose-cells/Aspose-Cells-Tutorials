---
category: general
date: 2026-11-22
description: Học cách tạo Excel từ dữ liệu JSON trong C# bằng Aspose.Cells Smart Marker.
  Hướng dẫn từng bước bao gồm thiết kế mẫu, xử lý JSON và xuất tệp.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel from json data
- Aspose.Cells
- Smart Marker
- C# Excel generation
- JSON to Excel
- Excel template
language: vi
lastmod: 2026-11-22
og_description: Tạo file Excel từ dữ liệu JSON bằng Aspose.Cells Smart Marker. Theo
  dõi hướng dẫn ngắn gọn này để tạo một workbook được định dạng đầy đủ từ một mảng
  JSON.
og_image_alt: Screenshot showing Excel workbook created from JSON data using Aspose.Cells
og_title: Tạo file Excel từ dữ liệu JSON trong C# – hướng dẫn đầy đủ Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn to create Excel from JSON data in C# using Aspose.Cells Smart
    Marker. Step‑by‑step guide covers template design, JSON handling, and file export.
  headline: How to create Excel from JSON data with Aspose.Cells and Smart Marker
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cách tạo Excel từ dữ liệu JSON bằng Aspose.Cells và Smart Marker
url: /vi/net/smart-markers-dynamic-data/how-to-create-excel-from-json-data-with-aspose-cells-and-sma/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách tạo Excel từ dữ liệu JSON bằng Aspose.Cells và Smart Marker

Nếu bạn cần **tạo Excel từ dữ liệu JSON** trong một ứng dụng .NET, hướng dẫn này sẽ cho bạn một giải pháp hoàn chỉnh, sẵn sàng cho môi trường sản xuất. Bạn sẽ thấy cách nhúng một mảng JSON vào một ô duy nhất, sử dụng tính năng **Smart Marker** của **Aspose.Cells**, và tạo ra một workbook cuối cùng mà không cần viết mã cho từng ô.

Cách tiếp cận này hoạt động với bất kỳ payload JSON nào—cho dù bạn đang xuất kết quả API, tuần tự hoá các đối tượng, hay xây dựng báo cáo. Khi kết thúc hướng dẫn, bạn sẽ có một dự án C# sẵn sàng chạy, đọc một chuỗi JSON, áp dụng nó vào **mẫu Excel**, và lưu kết quả thành một tệp mới.

## Yêu cầu trước

- .NET 6.0 hoặc mới hơn (mã cũng hoạt động với .NET Framework 4.6+)
- Visual Studio 2022 (hoặc bất kỳ IDE nào hỗ trợ C#)
- Gói NuGet **Aspose.Cells for .NET** (phiên bản 23.10 hoặc mới hơn)
- Một tệp mẫu Excel đơn giản chứa thẻ Smart Marker `<%=Fruits:ArrayAsSingle%>` trong ô mục tiêu

> **Mẹo chuyên nghiệp:** Đặt mẫu trong một thư mục mà ứng dụng của bạn có thể truy cập tại thời gian chạy (ví dụ, `Resources` hoặc một đường dẫn có thể cấu hình).  

## Bước 1: Chuẩn bị payload JSON

Đầu tiên, định nghĩa mảng JSON mà bạn muốn chèn vào worksheet. Trong ví dụ này chúng ta sử dụng một danh sách các tên trái cây.

```csharp
// Step 1 – JSON array that will be placed in a single cell
string fruitsJson = "[\"Apple\",\"Banana\",\"Cherry\"]";
```

Chuỗi JSON có thể được tạo động (ví dụ, `JsonSerializer.Serialize(myList)`) hoặc đọc từ nguồn bên ngoài như một REST API. Điểm quan trọng là chuỗi phải là một mảng JSON hợp lệ vì **Smart Marker** mong đợi một biểu diễn JSON khi sử dụng tùy chọn `ArrayAsSingle`.

## Bước 2: Xây dựng nguồn dữ liệu Smart Marker

Engine Smart Marker của Aspose.Cells làm việc với bất kỳ đối tượng .NET nào. Chúng ta tạo một đối tượng ẩn danh chứa chuỗi JSON dưới một thuộc tính có tên `Fruits`. Tên thuộc tính phải khớp với tên marker được dùng trong mẫu.

```csharp
// Step 2 – Anonymous object serving as the Smart Marker data source
var dataSource = new
{
    Fruits = fruitsJson   // Property name "Fruits" matches the marker <%=Fruits...%>
};
```

> **Tại sao lại dùng đối tượng ẩn danh?** Nó cho phép bạn truyền một container dữ liệu nhẹ mà không cần định nghĩa lớp riêng, giúp tăng tốc quá trình thử nghiệm. Đối với dự án lớn hơn, bạn có thể thay thế bằng một DTO có kiểu mạnh.

## Bước 3: Thiết kế mẫu Excel với placeholder Smart Marker

Tạo một tệp Excel (`SmartMarkerTemplate.xlsx`) chứa placeholder nơi JSON sẽ xuất hiện. Đặt marker sau vào ô mong muốn (ví dụ, **A1**):

```
<%=Fruits:ArrayAsSingle%>
```

- `Fruits` – khớp với tên thuộc tính trong nguồn dữ liệu.
- `ArrayAsSingle` – yêu cầu Smart Marker ghi toàn bộ mảng JSON dưới dạng một chuỗi duy nhất, giữ nguyên dấu ngoặc và dấu ngoặc kép.

![Excel template with Smart Marker placeholder](excel-template.png){alt="Mẫu Excel chứa <%=Fruits:ArrayAsSingle%> để tạo Excel từ dữ liệu JSON"}

## Bước 4: Tải workbook và khởi tạo bộ xử lý Smart Marker

Bây giờ tải tệp mẫu vào một thể hiện `Aspose.Cells.Workbook` và tạo một `SmartMarkerProcessor` sẽ thực hiện việc thay thế.

```csharp
// Step 4 – Load the template workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/SmartMarkerTemplate.xlsx");

// Initialise the Smart Marker processor with the loaded workbook
SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor(workbook);
```

Tải workbook một lần và tái sử dụng cùng một thể hiện `SmartMarkerProcessor` sẽ hiệu quả hơn so với việc tạo bộ xử lý mới cho mỗi ô.

## Bước 5: Áp dụng nguồn dữ liệu để thay thế marker

Phương thức `ApplyTemplate` sẽ quét toàn bộ workbook để tìm các marker và thay thế chúng bằng giá trị từ đối tượng đã cung cấp.

```csharp
// Step 5 – Replace the Smart Marker with the JSON content
smartMarkerProcessor.ApplyTemplate(dataSource);
```

Vì chúng ta đã dùng `ArrayAsSingle`, ô hiện tại chứa chuỗi JSON thô:

```
["Apple","Banana","Cherry"]
```

Nếu bạn cần định dạng khác (ví dụ, danh sách phân tách bằng dấu phẩy), có thể dùng `ArrayAsCommaSeparated` thay cho `ArrayAsSingle`.

## Bước 6: Lưu workbook đã xử lý

Cuối cùng, ghi workbook đã chỉnh sửa ra một tệp mới. Bạn có thể chọn bất kỳ định dạng nào được hỗ trợ (`.xlsx`, `.xls`, `.csv`, …).

```csharp
// Step 6 – Save the workbook with the JSON inserted
workbook.Save("YOUR_DIRECTORY/JsonExported.xlsx");
```

Tệp `JsonExported.xlsx` kết quả có thể được mở trong Excel, Google Sheets, hoặc bất kỳ trình xem tương thích nào, và sẽ hiển thị mảng JSON đúng như đã chèn.

## Ví dụ hoàn chỉnh

Kết hợp tất cả các phần lại sẽ cho bạn một chương trình console tự chứa:

```csharp
using Aspose.Cells;

class SmartMarkerJsonDemo
{
    static void Main()
    {
        // 1️⃣ Define the JSON array
        string fruitsJson = "[\"Apple\",\"Banana\",\"Cherry\"]";

        // 2️⃣ Create the data source object
        var dataSource = new
        {
            Fruits = fruitsJson
        };

        // 3️⃣ Load the Excel template that contains <%=Fruits:ArrayAsSingle%>
        Workbook workbook = new Workbook("YOUR_DIRECTORY/SmartMarkerTemplate.xlsx");

        // 4️⃣ Initialise the Smart Marker processor
        SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor(workbook);

        // 5️⃣ Apply the data source – the marker is replaced with the JSON string
        smartMarkerProcessor.ApplyTemplate(dataSource);

        // 6️⃣ Save the result
        workbook.Save("YOUR_DIRECTORY/JsonExported.xlsx");
    }
}
```

### Kết quả mong đợi

| A                                   |
|-------------------------------------|
| `["Apple","Banana","Cherry"]`       |

JSON sẽ xuất hiện chính xác dưới dạng chuỗi trong ô **A1** của `JsonExported.xlsx`.

## Xử lý các biến thể và trường hợp đặc biệt thường gặp

| Tình huống                                 | Điều chỉnh đề xuất |
|-------------------------------------------|--------------------|
| **JSON lớn** (từ điển lồng nhau) | Sử dụng `ArrayAsJson` để nhúng toàn bộ cấu trúc đối tượng, hoặc ánh xạ JSON vào một mô hình có kiểu mạnh và dùng các marker lồng nhau (`<%=Parent.Child%>`). |
| **Nhiều mảng JSON** trong các ô khác nhau | Thêm các thuộc tính bổ sung vào đối tượng ẩn danh (ví dụ, `Vegetables = vegJson`) và các marker tương ứng (`<%=Vegetables:ArrayAsSingle%>`). |
| **Cần tách mảng thành các hàng** | Thay `ArrayAsSingle` bằng `Array` – Smart Marker sẽ tạo một hàng mới cho mỗi phần tử. |
| **Mẫu được lưu dưới dạng tài nguyên nhúng** | Tải workbook từ stream: `Assembly.GetExecutingAssembly().GetManifestResourceStream("Namespace.Template.xlsx")`. |
| **Chạy trong ASP.NET Core** | Dùng `IWebHostEnvironment.ContentRootPath` để xây dựng đường dẫn đầy đủ tới mẫu và các tệp đầu ra. |

## Các lưu ý về hiệu năng

- **Tái sử dụng đối tượng `Workbook`** khi xử lý nhiều bản ghi trong một lô; tạo bộ xử lý một lần cho mỗi workbook.
- **Vô hiệu hoá tính toán** (`workbook.CalculateFormula = false`) nếu mẫu chứa các công thức nặng mà không cần thiết cho bước chèn JSON.
- **Lưu dưới dạng stream** (`workbook.Save(stream, SaveFormat.Xlsx)`) giảm tải I/O khi gửi tệp trực tiếp tới phản hồi client.

## Kết luận

Bây giờ bạn đã biết cách **tạo Excel từ dữ liệu JSON** trong C# bằng **Aspose.Cells** và tính năng **Smart Marker**. Hướng dẫn đã bao quát việc chuẩn bị JSON, tạo nguồn dữ liệu, thiết kế mẫu, xử lý marker, và lưu tệp—tất cả trong một chương trình có thể chạy ngay.

Từ đây bạn có thể:

- Mở rộng mẫu với các thẻ **Smart Marker** bổ sung để tạo báo cáo phong phú hơn.
- Chuyển sang `Array` hoặc `ArrayAsJson` để xuất JSON dưới dạng các hàng hoặc cấu trúc lồng nhau.
- Kết hợp kỹ thuật này với các thư viện tạo Excel C# như EPPlus hoặc ClosedXML nếu bạn cần một giải pháp miễn phí.

Chúc lập trình vui vẻ, và tận hưởng việc biến JSON thành các workbook Excel chuyên nghiệp!


## Bạn nên học gì tiếp theo?


Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh cùng giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Import JSON Data into Excel Using Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Aspose Cells GridJs tutorial – Export Excel data to JSON with lazy loading](/cells/english/python/import-and-export/aspose-cells-gridjs-tutorial-export-excel-data-to-json-with/)
- [Crear Excel a partir de JSON con Smart Marker de Aspose.Cells](/cells/spanish/net/smart-markers-dynamic-data/create-excel-from-json-with-aspose-cells-smart-marker/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}