---
category: general
date: 2026-02-23
description: Cách tạo workbook bằng Aspose.Cells và thêm marker bằng mảng JSON. Tìm
  hiểu cách thêm marker, sử dụng mảng JSON và smart markers trong Aspose.Cells chỉ
  trong vài phút.
draft: false
keywords:
- how to create workbook
- how to add markers
- use json array
- smart markers aspose.cells
language: vi
og_description: Cách tạo workbook bằng Aspose.Cells, thêm các marker và sử dụng mảng
  JSON. Hướng dẫn chi tiết này sẽ cho bạn mọi thứ cần thiết.
og_title: Cách tạo sổ làm việc với Smart Markers – Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Cách tạo sổ làm việc với Smart Markers – Hướng dẫn Aspose.Cells
url: /vi/net/smart-markers-dynamic-data/how-to-create-workbook-with-smart-markers-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Tạo Workbook với Smart Markers – Hướng Dẫn Aspose.Cells

Bạn đã bao giờ tự hỏi **cách tạo workbook** tự động điền dữ liệu từ nguồn JSON chưa? Bạn không phải là người duy nhất—các nhà phát triển luôn hỏi cách thêm các marker để lấy giá trị từ mảng, đặc biệt khi làm việc với Aspose.Cells. Tin tốt? Khi nắm bắt được khái niệm smart‑marker, mọi thứ sẽ khá đơn giản. Trong hướng dẫn này, chúng ta sẽ đi qua việc tạo workbook, thêm marker, sử dụng một mảng JSON, và cấu hình smart markers trong Aspose.Cells để bạn có thể tạo file Excel ngay lập tức.

Chúng ta sẽ bao phủ mọi thứ bạn cần biết: khởi tạo workbook, xây dựng một `MarkerCollection`, cung cấp một mảng JSON, bật cờ “ArrayAsSingle”, và cuối cùng áp dụng các marker. Khi hoàn thành, bạn sẽ có một chương trình C# hoạt động đầy đủ, tạo ra file Excel với các giá trị **A**, **B**, và **C** được tự động điền. Không cần dịch vụ bên ngoài, chỉ cần sức mạnh của Aspose.Cells.

## Yêu Cầu Trước

- .NET 6.0 trở lên (mã cũng hoạt động với .NET Framework 4.6+)
- Gói NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`)
- Kiến thức cơ bản về cú pháp C# (nếu bạn mới bắt đầu, các đoạn mã được chú thích chi tiết)
- Visual Studio hoặc bất kỳ IDE nào bạn thích

Nếu bạn đã có những thứ này, tuyệt vời—cùng bắt đầu.

## Bước 1: Cách Tạo Workbook (Khởi Tạo Tệp Excel)

Điều đầu tiên bạn cần là một đối tượng workbook trống. Hãy nghĩ nó như một canvas trắng mà Aspose.Cells sẽ vẽ dữ liệu lên sau này.

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];    // reference to the default sheet
```

> **Tại sao điều này quan trọng:** `Workbook` là điểm vào cho mọi thao tác Excel. Nếu không có nó, bạn không thể gắn smart markers hoặc lưu tệp. Tạo workbook trước cũng đảm bảo môi trường sạch sẽ cho các bước tiếp theo.

## Bước 2: Cách Thêm Markers – Khởi Tạo Marker Collection

Smart markers tồn tại trong một `MarkerCollection`. Bộ sưu tập này là nơi bạn định nghĩa các placeholder (các marker) và dữ liệu sẽ thay thế chúng.

```csharp
        // Step 2: Initialise a collection for smart markers
        MarkerCollection smartMarkerCollection = new MarkerCollection();
```

> **Mẹo chuyên nghiệp:** Bạn có thể tái sử dụng cùng một `MarkerCollection` cho nhiều worksheet, nhưng việc giữ một bộ cho mỗi sheet sẽ giúp việc gỡ lỗi dễ dàng hơn.

## Bước 3: Sử Dụng JSON Array – Thêm Marker với Dữ Liệu JSON

Bây giờ chúng ta thực sự thêm một marker. Placeholder `{SmartMarker}` sẽ được thay thế bằng mảng JSON mà chúng ta cung cấp. JSON phải là một mảng đã được chuyển thành chuỗi, ví dụ `["A","B","C"]`.

```csharp
        // Step 3: Add a smart marker and provide replacement data (JSON array)
        smartMarkerCollection.Add("{SmartMarker}", "[\"A\",\"B\",\"C\"]");
```

> **Giải thích:** Phương thức `Add` nhận hai đối số: văn bản marker và nguồn dữ liệu. Ở đây nguồn dữ liệu là một mảng JSON, Aspose.Cells sẽ tự động phân tích. Đây là phần cốt lõi của **use json array** với smart markers.

## Bước 4: Cấu Hình Marker – Xử Lý Mảng Như Một Giá Trị Đơn

Mặc định, Aspose.Cells sẽ mở rộng một mảng JSON thành các hàng riêng biệt. Nếu bạn muốn toàn bộ mảng được coi là một giá trị ô duy nhất (hữu ích cho danh sách thả xuống hoặc chuỗi nối), hãy bật cờ `ArrayAsSingle`.

```csharp
        // Step 4: Configure the marker to treat the array as a single value
        smartMarkerCollection["ArrayAsSingle"] = true;
```

> **Khi nào nên dùng:** Nếu bạn muốn mảng xuất hiện trong một ô (ví dụ `"A,B,C"`), bật cờ này. Nếu không, Aspose.Cells sẽ ghi mỗi phần tử vào một hàng riêng.

## Bước 5: Gắn Markers vào Worksheet và Áp Dụng Chúng

Cuối cùng, liên kết bộ sưu tập marker với worksheet và yêu cầu Aspose.Cells thay thế các placeholder bằng dữ liệu thực tế.

```csharp
        // Step 5: Attach the marker collection to the worksheet and apply it
        worksheet.SmartMarkers.Add(smartMarkerCollection);
        worksheet.SmartMarkers.Apply();

        // Optional: write the placeholder into a cell so you can see the replacement
        worksheet.Cells["A1"].PutValue("{SmartMarker}");

        // Save the workbook to disk
        workbook.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook created successfully!");
    }
}
```

> **Kết quả:** Sau khi chạy chương trình, `SmartMarkerResult.xlsx` chứa giá trị **A** (hoặc toàn bộ mảng nếu `ArrayAsSingle` là true) ở ô `A1`. Mở tệp để kiểm tra.

### Kết Quả Mong Đợi

| A |
|---|
| A |   *(nếu `ArrayAsSingle` là false, phần tử đầu tiên sẽ lấp đầy ô)*

Nếu bạn đặt `ArrayAsSingle = true`, ô `A1` sẽ chứa chuỗi `["A","B","C"]`.

## Bước 6: Cách Thêm Markers – Kịch Bản Nâng Cao (Tùy Chọn)

Bạn có thể tự hỏi, *nếu cần nhiều hơn một marker thì sao?* Câu trả lời rất đơn giản: chỉ cần gọi `Add` lại lần nữa.

```csharp
        smartMarkerCollection.Add("{SecondMarker}", "[{\"Name\":\"John\"},{\"Name\":\"Jane\"}]");
        // You can also control each marker individually:
        smartMarkerCollection["SecondMarker"] = false; // expand into rows
```

> **Tại sao điều này hoạt động:** Mỗi marker hoạt động độc lập, vì vậy bạn có thể kết hợp “array as single” và “expand into rows” trong cùng một worksheet. Sự linh hoạt này là đặc trưng của **smart markers aspose.cells**.

## Những Sai Lầm Thường Gặp & Cách Tránh

| Vấn đề | Nguyên Nhân | Giải Pháp |
|-------|------------|-----------|
| Marker không được thay thế | Văn bản placeholder thiếu hoặc có lỗi chính tả | Đảm bảo ô chứa đúng chuỗi marker (`{SmartMarker}`) |
| JSON không được phân tích | Cú pháp JSON không hợp lệ (thiếu dấu ngoặc kép) | Sử dụng công cụ kiểm tra JSON hoặc escape dấu ngoặc kép kép trong chuỗi C# |
| Mảng mở rộng không mong muốn | `ArrayAsSingle` để mặc định `false` | Đặt `["ArrayAsSingle"] = true` cho marker cụ thể |
| Workbook lưu trống | `Apply()` chưa được gọi trước `Save()` | Luôn gọi `worksheet.SmartMarkers.Apply()` trước khi lưu |

## Ví Dụ Hoàn Chỉnh (Sẵn Sàng Sao Chép)

Dưới đây là chương trình đầy đủ mà bạn có thể đưa vào một console app. Không cần file bổ sung nào.

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Initialise a collection for smart markers
        MarkerCollection smartMarkerCollection = new MarkerCollection();

        // Add a smart marker and provide replacement data (JSON array)
        smartMarkerCollection.Add("{SmartMarker}", "[\"A\",\"B\",\"C\"]");

        // Configure the marker to treat the array as a single value
        smartMarkerCollection["ArrayAsSingle"] = true;

        // Attach the marker collection to the worksheet and apply it
        worksheet.SmartMarkers.Add(smartMarkerCollection);
        worksheet.SmartMarkers.Apply();

        // Place the marker in a cell so we can see the replacement
        worksheet.Cells["A1"].PutValue("{SmartMarker}");

        // Save the workbook
        workbook.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook created successfully!");
    }
}
```

Chạy chương trình, mở `SmartMarkerResult.xlsx`, và bạn sẽ thấy mảng JSON (hoặc phần tử đầu tiên) được đặt gọn gàng ở ô **A1**.

## Các Bước Tiếp Theo: Mở Rộng Giải Pháp

Bây giờ bạn đã biết **cách tạo workbook**, **cách thêm markers**, và **cách sử dụng json array** với Aspose.Cells, hãy cân nhắc các ý tưởng tiếp theo:

1. **Nhiều Worksheet** – Lặp qua danh sách worksheets và gắn các MarkerCollection khác nhau cho mỗi sheet.
2. **JSON Động** – Lấy JSON từ một API web (`HttpClient`) và truyền trực tiếp vào `smartMarkerCollection.Add`.
3. **Định Dạng Đầu Ra** – Sau khi áp dụng markers, định dạng các ô (phông chữ, màu sắc) để báo cáo trông chuyên nghiệp hơn.
4. **Định Dạng Xuất** – Lưu workbook dưới dạng PDF, CSV, hoặc HTML bằng cách thay đổi `workbook.Save("file.pdf")`.

Mỗi chủ đề này đều liên quan tới **smart markers aspose.cells**, vì vậy bạn sẽ mở rộng các khái niệm cốt lõi mà vừa học.

## Kết Luận

Chúng ta đã đi qua **cách tạo workbook** từ đầu, **cách thêm markers**, và **cách sử dụng json array** với smart markers của Aspose.Cells. Ví dụ đầy đủ, có thể chạy ngay, minh họa toàn bộ quy trình, từ khởi tạo `Workbook` đến lưu file cuối cùng. Bằng cách bật hoặc tắt cờ `ArrayAsSingle`, bạn có thể kiểm soát chi tiết cách dữ liệu JSON hiển thị trong Excel, giúp giải pháp linh hoạt cho nhiều kịch bản báo cáo.

Hãy thử chạy mã, thay đổi JSON, và thử nghiệm thêm các marker. Khi bạn thành thạo những khối xây dựng này, việc tạo báo cáo Excel phức tạp sẽ trở nên dễ dàng. Có câu hỏi hoặc muốn chia sẻ một trường hợp sử dụng thú vị? Để lại bình luận bên dưới—chúc bạn lập trình vui vẻ! 

![Sơ đồ mô tả cách tạo workbook với smart markers trong Aspose.Cells](https://example.com/images/create-workbook-smart-markers.png "cách tạo workbook với Aspose.Cells smart markers")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}