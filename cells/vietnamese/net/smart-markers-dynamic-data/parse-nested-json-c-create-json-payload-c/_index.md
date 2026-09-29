---
category: general
date: 2026-02-15
description: Phân tích JSON lồng nhau trong C# bằng SmartMarkers và học cách tạo payload
  JSON C# cho các đơn hàng phức tạp. Hướng dẫn chi tiết từng bước kèm mã nguồn đầy
  đủ và giải thích.
draft: false
keywords:
- parse nested json c#
- create json payload c#
language: vi
og_description: Phân tích JSON lồng nhau trong C# ngay lập tức. Học cách tạo payload
  JSON trong C# và xử lý nó bằng SmartMarkers trong một ví dụ đầy đủ, có thể chạy
  được.
og_title: Phân tích JSON lồng nhau C# – Tạo payload JSON C#
tags:
- json
- csharp
- smartmarkers
title: Phân tích JSON lồng nhau C# – Tạo payload JSON C#
url: /vi/net/smart-markers-dynamic-data/parse-nested-json-c-create-json-payload-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Phân tích JSON lồng nhau C# – Tạo Payload JSON C#  

Bạn đã bao giờ cần **parse nested JSON C#** nhưng không chắc bắt đầu từ đâu chưa? Bạn không đơn độc—nhiều nhà phát triển gặp khó khăn khi dữ liệu của họ chứa mảng bên trong đối tượng. Tin tốt là chỉ với vài dòng code, bạn có thể vừa **create JSON payload C#** vừa để SmartMarkers duyệt qua cấu trúc lồng nhau cho bạn.  

Trong tutorial này chúng ta sẽ xây dựng một chuỗi JSON mô tả các đơn hàng với các mục dòng, bật bộ xử lý SmartMarkers để hiểu các phạm vi lồng nhau, và cuối cùng xác minh rằng dữ liệu đã được phân tích đúng. Khi kết thúc, bạn sẽ có một chương trình tự chứa, sẵn sàng sao chép‑dán mà bạn có thể điều chỉnh cho bất kỳ JSON phân cấp nào bạn gặp.

## Những gì bạn cần  

- .NET 6 hoặc mới hơn (code cũng biên dịch được với .NET Core 3.1)  
- Tham chiếu tới thư viện SmartMarkers (hoặc bất kỳ bộ xử lý nào tương tự hỗ trợ nested ranges)  
- Kiến thức cơ bản về C#—không có gì phức tạp, chỉ các câu lệnh `using` thông thường và một phương thức `Main`  

Đó là tất cả. Không cần thêm gói NuGet nào ngoài thư viện marker, và không có dịch vụ bên ngoài.

## Bước 1: Tạo JSON Payload C# – Xây dựng dữ liệu  

Đầu tiên chúng ta tạo chuỗi JSON chứa một mảng các đơn hàng, mỗi đơn hàng có mảng `Lines` riêng. Hãy nghĩ nó như một ảnh chụp nhanh của hệ thống quản lý đơn hàng mini.

```csharp
using System;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // STEP 1 – Define the JSON payload with nested arrays
            // -------------------------------------------------
            string ordersJson = @"{
                ""Orders"": [
                    {
                        ""Id"": 1,
                        ""Lines"": [
                            { ""Prod"": ""A"" },
                            { ""Prod"": ""B"" }
                        ]
                    },
                    {
                        ""Id"": 2,
                        ""Lines"": [
                            { ""Prod"": ""C"" }
                        ]
                    }
                ]
            }";

            // The rest of the steps follow…
```

Tại sao lại xây dựng payload dưới dạng chuỗi verbatim? Nó giữ nguyên các ngắt dòng và cho phép bạn nhìn thấy cấu trúc ngay lập tức—rất hữu ích khi debug JSON lồng nhau.  

> **Pro tip:** Nếu JSON của bạn đến từ cơ sở dữ liệu hoặc API, bạn có thể thay thế literal bằng `File.ReadAllText` hoặc một yêu cầu web—không có gì trong tutorial này phụ thuộc vào nguồn dữ liệu.

## Bước 2: Bật Nested Ranges với SmartMarkerOptions  

SmartMarkers cần một chút gợi ý để hiểu rằng một mảng có thể chứa một mảng khác. Đó là công dụng của `EnableNestedRanges`.

```csharp
            // -------------------------------------------------
            // STEP 2 – Configure SmartMarker options for nesting
            // -------------------------------------------------
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                EnableNestedRanges = true   // <-- crucial for Orders → Lines
            };
```

Cài đặt `EnableNestedRanges` thành `true` báo cho bộ xử lý coi mỗi collection `Lines` là một sub‑range của phạm vi `Orders` cha. Nếu không bật cờ này, vòng lặp bên trong sẽ bị bỏ qua và bạn chỉ thấy các đối tượng cấp trên.

## Bước 3: Xử lý JSON với SmartMarkersProcessor  

Bây giờ chúng ta truyền chuỗi JSON và các tùy chọn cho bộ xử lý. Lệnh gọi là đồng bộ và không trả về gì—SmartMarkers ghi kết quả vào ngữ cảnh nội bộ, bạn có thể lấy ra sau này.

```csharp
            // -------------------------------------------------
            // STEP 3 – Run the processor on the JSON payload
            // -------------------------------------------------
            ws.SmartMarkersProcessor.Process(ordersJson, options);
```

Nếu bạn đang dùng thư viện khác, thay thế `ws.SmartMarkersProcessor.Process` bằng tên phương thức phù hợp; nguyên tắc vẫn giống—truyền JSON và cấu hình cho phép xử lý lồng nhau.

## Bước 4: Xác minh kết quả đã phân tích  

Sau khi xử lý, bạn thường muốn xác nhận rằng mọi đơn hàng và các mục dòng của chúng đã được duyệt. Dưới đây là cách đơn giản để in dữ liệu ra console bằng một phương thức giả định `GetProcessedData` (thay bằng accessor thực tế của thư viện bạn dùng).

```csharp
            // -------------------------------------------------
            // STEP 4 – Output the parsed structure (demo purpose)
            // -------------------------------------------------
            var result = ws.SmartMarkersProcessor.GetProcessedData(); // pseudo‑code
            Console.WriteLine("=== Parsed Orders ===");
            foreach (var order in result.Orders)
            {
                Console.WriteLine($"Order Id: {order.Id}");
                foreach (var line in order.Lines)
                {
                    Console.WriteLine($"  - Product: {line.Prod}");
                }
            }
        }
    }
}
```

**Expected console output**

```
=== Parsed Orders ===
Order Id: 1
  - Product: A
  - Product: B
Order Id: 2
  - Product: C
```

Nhìn thấy cấu trúc phân cấp được tái tạo xác nhận rằng **parse nested json c#** đã hoạt động như mong đợi.

## Bước 5: Các trường hợp biên và lỗi thường gặp  

### Bộ sưu tập rỗng  
Nếu một đơn hàng không có `Lines`, bộ xử lý vẫn sẽ tạo một phạm vi rỗng. Đảm bảo mã downstream của bạn có thể xử lý danh sách rỗng mà không ném `NullReferenceException`.

### Cấu trúc lồng sâu  
`EnableNestedRanges` hoạt động cho mức lồng hai cấp ngay từ đầu. Đối với ba cấp trở lên, bạn có thể cần đặt `MaxNestedDepth` (nếu thư viện cung cấp) hoặc gọi đệ quy bộ xử lý trên mỗi sub‑object.

### Ký tự đặc biệt  
Các chuỗi JSON chứa dấu ngoặc kép, dấu gạch ngược, hoặc Unicode cần được escape đúng cách. Sử dụng chuỗi verbatim (`@""`) như chúng tôi đã làm giúp tránh hầu hết vấn đề, nhưng nếu bạn tạo JSON một cách lập trình, hãy để `System.Text.Json.JsonSerializer` thực hiện việc escape cho bạn.

### Hiệu năng  
Phân tích các payload lớn (megabyte) có thể tốn nhiều bộ nhớ. Hãy cân nhắc stream JSON bằng `Utf8JsonReader` và đưa các khối dữ liệu vào bộ xử lý nếu gặp nút thắt hiệu năng.

## Tổng quan hình ảnh  

![Diagram illustrating how parse nested json c# flows through SmartMarkers processing](parse-nested-json-csharp-diagram.png "parse nested json c# diagram")

Hình ảnh cho thấy hành trình từ JSON thô → SmartMarkerOptions → Processor → Mô hình đối tượng đã phân tích.

## Tóm tắt  

Chúng ta đã đi qua một ví dụ đầy đủ về **parse nested json c#**, từ **create json payload c#** đến việc xác minh dữ liệu lồng nhau sau khi xử lý. Những điểm chính cần ghi nhớ là:

1. Xây dựng một chuỗi JSON có cấu trúc tốt phản ánh các đối tượng miền của bạn.  
2. Bật `EnableNestedRanges` (hoặc tương đương) để parser tôn trọng các mảng bên trong.  
3. Chạy bộ xử lý và kiểm tra kết quả để đảm bảo mọi cấp độ đều được duyệt.  

## Bước tiếp theo?  

- **Dynamic payloads:** Thay thế chuỗi cứng bằng các đối tượng được serialize qua `System.Text.Json`.  
- **Custom markers:** Mở rộng SmartMarkers với các thẻ của riêng bạn để chèn các trường tính toán vào mỗi mục dòng.  
- **Error handling:** Bao quanh lệnh `Process` bằng try/catch và ghi log chi tiết `SmartMarkerException` để khắc phục sự cố.  

Hãy thoải mái thử nghiệm—thay mảng `Orders` bằng khách hàng, hoá đơn, hoặc bất kỳ dữ liệu phân cấp nào bạn cần **parse nested json c#**. Mẫu này vẫn giữ nguyên.

Chúc lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}