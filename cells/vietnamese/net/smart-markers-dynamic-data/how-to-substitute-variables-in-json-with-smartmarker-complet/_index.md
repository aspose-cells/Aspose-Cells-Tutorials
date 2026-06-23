---
category: general
date: 2026-03-29
description: Cách thay thế biến trong JSON bằng SmartMarker – học cách sử dụng biểu
  thức if, áp dụng logic điều kiện, nhân các giá trị và tạo JSON một cách dễ dàng.
draft: false
keywords:
- how to substitute variables
- use if expression
- how to apply conditional
- how to multiply values
- how to generate json
language: vi
og_description: Cách thay thế biến trong JSON bằng SmartMarker. Khám phá cách sử dụng
  biểu thức if, áp dụng logic điều kiện, nhân các giá trị và tạo JSON trong vài phút.
og_title: Cách Thay Thế Biến Trong JSON Bằng SmartMarker – Từng Bước
tags:
- C#
- SmartMarker
- JSON templating
title: Cách Thay Thế Biến Trong JSON Bằng SmartMarker – Hướng Dẫn Toàn Diện
url: /vi/net/smart-markers-dynamic-data/how-to-substitute-variables-in-json-with-smartmarker-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Thay Thế Biến Trong JSON bằng SmartMarker – Hướng Dẫn Toàn Diện

Bạn đã bao giờ tự hỏi **cách thay thế biến** bên trong một payload JSON mà không cần viết trình phân tích tùy chỉnh chưa? Bạn không phải là người duy nhất. Trong nhiều kịch bản tích hợp—như hoá đơn, công cụ định giá, hoặc tệp cấu hình động—bạn cần chèn các giá trị thời gian chạy, áp dụng các điều kiện đơn giản, và thậm chí thực hiện một phép nhân nhanh. Bài hướng dẫn này sẽ cho bạn thấy chính xác **cách thay thế biến** bằng thư viện SmartMarker, đồng thời giữ cho JSON sạch sẽ và dễ đọc.

Chúng tôi sẽ đi qua một ví dụ thực tế bao gồm **use if expression**, **how to apply conditional**, **how to multiply values**, và **how to generate json** ngay lập tức. Khi kết thúc, bạn sẽ có một đoạn mã C# sẵn sàng chạy mà bạn có thể chèn vào bất kỳ dự án .NET nào.

## Những Điều Bạn Sẽ Học

- Thiết lập `SmartMarkerOptions` để lưu trữ các biến có thể tái sử dụng.  
- Viết một mẫu JSON chứa biểu thức `if` cho logic điều kiện.  
- Nhân một giá trị với một biến trong mẫu.  
- Xử lý mẫu bằng `SmartMarkerProcessor` và nhận chuỗi JSON cuối cùng.  
- Khắc phục các vấn đề thường gặp như biến thiếu hoặc biểu thức sai định dạng.  

Không có dịch vụ bên ngoài, không có phụ thuộc nặng—chỉ cần C# thuần và gói NuGet SmartMarker.

---

## Cách Thay Thế Biến – Tổng Quan Từng Bước

Dưới đây là một hình ảnh tổng quan về quy trình. Hãy nghĩ nó như một pipeline nơi mẫu JSON thô của bạn vào từ phía trái, engine SmartMarker thực hiện phép màu, và JSON đã được render hoàn chỉnh ra phía phải.

![Sơ đồ cho thấy cách thay thế biến trong JSON](https://example.com/images/smartmarker-flow.png "Cách thay thế biến trong JSON")

*Văn bản thay thế ảnh: Sơ đồ cho thấy cách thay thế biến trong JSON.*

---

## Bước 1: Cài Đặt và Nhập SmartMarker

Trước khi bắt đầu, hãy chắc chắn rằng gói SmartMarker đã được tham chiếu trong dự án của bạn. Nếu bạn đang sử dụng .NET CLI, chạy:

```bash
dotnet add package SmartMarker
```

Sau đó, thêm các chỉ thị `using` cần thiết ở đầu tệp C# của bạn:

```csharp
using SmartMarker;
using SmartMarker.Models;
using System;
```

> **Mẹo chuyên nghiệp:** Phiên bản mới nhất (tính đến tháng 3 2026) là 2.4.1. Nó hỗ trợ .NET 6 trở lên, nhưng cũng hoạt động tốt với .NET Framework 4.7.

---

## Bước 2: Tạo SmartMarker Options và Định Nghĩa Các Biến

Bây giờ chúng ta sẽ tạo một thể hiện của `SmartMarkerOptions` để chứa bất kỳ biến nào chúng ta muốn tái sử dụng trong mẫu. Đây là nơi chúng ta trả lời câu hỏi **cách thay thế biến**—các biến đóng vai trò là chỗ giữ mà SmartMarker sẽ thay thế sau.

```csharp
// Step 2: Create SmartMarker options to hold variables used in the template
var smartMarkerOptions = new SmartMarkerOptions();

// Define a variable (Rate) that we’ll reference later in the JSON expression
smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission rate
```

Tại sao lưu trữ tỷ lệ trong `Variables` thay vì mã cứng? Bởi vì bạn có thể lấy số này từ cơ sở dữ liệu, tệp cấu hình, hoặc đầu vào của người dùng. Giữ nó trong options giúp mẫu có thể tái sử dụng và dễ kiểm thử.

---

## Bước 3: Viết Mẫu JSON với Biểu Thức `if`

Đây là nơi từ khóa **use if expression** tỏa sáng. SmartMarker cho phép bạn nhúng logic điều kiện trực tiếp trong chuỗi JSON. Cú pháp trông giống như một tên thuộc tính, nhưng SmartMarker xử lý nó như một chỉ thị.

```csharp
// Step 3: Prepare the JSON data with a conditional field that uses the variable
string jsonTemplate = @"{
    ""Amount"": 1000,
    ""if(Amount>500)"": ""${Amount * Rate}""
}";
```

Chú ý tới khóa `if(Amount>500)`. SmartMarker đánh giá biểu thức `Amount>500`; nếu đúng, giá trị tương ứng (`${Amount * Rate}`) sẽ được chèn vào đầu ra. Cú pháp `${...}` là *công cụ thay thế biến* — ở đây chúng ta **cách nhân giá trị** (`Amount * Rate`) trước khi chèn kết quả.

---

## Bước 4: Xử Lý Mẫu và Lấy JSON Cuối Cùng

Với các options và mẫu đã sẵn sàng, chúng ta chuyển mọi thứ cho bộ xử lý. Phương thức `ProcessJson` phân tích mẫu, áp dụng điều kiện, thực hiện phép nhân, và trả về một chuỗi JSON sạch sẽ.

```csharp
// Step 4: Process the JSON with SmartMarker, applying the variable substitution
string resultJson = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(resultJson);
```

Chạy đoạn mã sẽ in ra:

```json
{
  "Amount": 1000,
  "Result": "80"
}
```

**Điều gì đã xảy ra?**  
- `Amount` là 1000, thỏa mãn `Amount>500`.  
- SmartMarker đánh giá `${Amount * Rate}` → `1000 * 0.08 = 80`.  
- Khóa điều kiện gốc (`if(Amount>500)`) được thay thế bằng một tên thuộc tính sạch (`Result`). Mặc định SmartMarker sử dụng `"Result"` nhưng bạn có thể tùy chỉnh (xem phần sau).

Nếu bạn thay đổi `Amount` thành `400`, kết quả sẽ là:

```json
{
  "Amount": 400
}
```

Khối điều kiện biến mất vì biểu thức được đánh giá là `false`. Đó là bản chất của **cách áp dụng điều kiện** trong JSON.

---

## Bước 5: Tùy Chỉnh Tên Thuộc Tính Đầu Ra (Tùy Chọn)

Đôi khi bạn không muốn khóa chung chung `"Result"`. SmartMarker cho phép bạn chỉ định tên tùy chỉnh bằng tùy chọn `RenameIfExpression`:

```csharp
smartMarkerOptions.RenameIfExpression = "Discount";
string customResult = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(customResult);
```

Kết quả:

```json
{
  "Amount": 1000,
  "Discount": "80"
}
```

Bây giờ giá trị điều kiện được lưu dưới một tên thuộc tính có ý nghĩa hơn—hoàn hảo cho các dịch vụ hạ nguồn cần một trường cụ thể.

---

## Những Cạm Bẫy Thường Gặp và Cách Tránh

| Vấn đề | Nguyên nhân | Cách khắc phục |
|-------|----------------|-----|
| Biến không tồn tại | Bạn tham chiếu một biến không có trong `smartMarkerOptions.Variables`. | Kiểm tra lại chính tả và đảm bảo biến đã được thêm trước khi xử lý. |
| Cú pháp `if` không hợp lệ | Thiếu dấu ngoặc hoặc toán tử sai (`>`, `<`, `==`). | Tuân theo đúng mẫu `if(<expression>)`; SmartMarker chỉ hỗ trợ các so sánh số đơn giản. |
| JSON bị lỗi cấu trúc | Vô tình để lại dấu phẩy thừa sau khối điều kiện. | Để SmartMarker xử lý việc loại bỏ; giữ mẫu gốc đúng cú pháp. |
| Định dạng số không mong muốn | Kết quả xuất hiện dưới dạng chuỗi `"80"` thay vì số. | Ép kiểu hoặc phân tích sau, hoặc sử dụng `${(Amount * Rate):N0}` để định dạng số. |

---

## Ví Dụ Hoàn Chỉnh (Sẵn Sàng Sao Chép‑Dán)

Dưới đây là chương trình đầy đủ mà bạn có thể biên dịch và chạy. Nó minh họa **cách tạo json** với các biến động, điều kiện và phép tính—tất cả trong chưa tới 30 dòng.

```csharp
using System;
using SmartMarker;
using SmartMarker.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Create SmartMarker options and define a reusable variable
        var smartMarkerOptions = new SmartMarkerOptions();
        smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission
        smartMarkerOptions.RenameIfExpression = "Discount"; // optional custom name

        // 2️⃣ JSON template with an if expression and multiplication
        string jsonTemplate = @"{
            ""Amount"": 1000,
            ""if(Amount>500)"": ""${Amount * Rate}""
        }";

        // 3️⃣ Process the template
        string output = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);

        // 4️⃣ Show the result
        Console.WriteLine("Generated JSON:");
        Console.WriteLine(output);
    }
}
```

**Kết quả mong đợi trên console**

```
Generated JSON:
{
  "Amount": 1000,
  "Discount": "80"
}
```

Bạn có thể thay đổi `Amount` để kiểm tra nhánh điều kiện, hoặc điều chỉnh `Rate` để xem các phép tính chiết khấu khác nhau.

---

## Mở Rộng Mẫu – Thêm Các Kịch Bản “Cách”

- **Cách thay thế biến** từ tệp cấu hình: Tải một `Dictionary<string, object>` từ `appsettings.json` và đưa vào `smartMarkerOptions.Variables`.  
- **Cách sử dụng if expression** cho nhiều điều kiện: Nối chúng như `"if(Amount>500 && CustomerType=='VIP')"`—SmartMarker hỗ trợ logic AND/OR.  
- **Cách áp dụng định dạng có điều kiện**: Sử dụng `${Amount:0.00}` trong biểu thức để kiểm soát số thập phân.  
- **Cách nhân các giá trị** với phép tính phức tạp hơn: `${(Amount - Discount) * TaxRate}` hoạt động tương tự.  
- **Cách tạo json** cho các đối tượng lồng nhau: Đặt khối điều kiện bên trong một đối tượng JSON khác, và SmartMarker sẽ giữ nguyên cấu trúc cây.

---

## Kết Luận

Chúng tôi đã trình bày **cách thay thế biến** trong JSON bằng SmartMarker, minh họa **use if expression** để chèn điều kiện, giải thích **cách áp dụng điều kiện** logic, cho thấy **cách nhân các giá trị** trong mẫu, và cuối cùng trình bày **cách tạo json** sẵn sàng cho việc tiêu thụ ở phía hạ nguồn. Cách tiếp cận này nhẹ, không cần engine templating bên ngoài, và tích hợp gọn gàng vào bất kỳ codebase C# nào.

Hãy thử nghiệm—điều chỉnh các biến, thêm nhiều điều kiện, hoặc đóng gói toàn bộ trong một lớp trợ giúp để tái sử dụng trong toàn bộ giải pháp của bạn. Khi bạn cần tạo JSON động nhanh chóng, SmartMarker là một lựa chọn vững chắc, sẵn sàng cho môi trường production.

**Các bước tiếp theo**

- Tìm hiểu sâu hơn các tính năng nâng cao của SmartMarker như vòng lặp (`foreach`) và hàm tùy chỉnh.  
- Kết hợp kỹ thuật này với các endpoint ASP.NET Core để cung cấp API JSON động.  
- Khám phá các thư viện templating khác (ví dụ, Handlebars.NET) để so sánh, đặc biệt nếu bạn cần cú pháp phong phú hơn.

Có câu hỏi hoặc một trường hợp sử dụng cụ thể mà bạn đang gặp khó khăn? Để lại bình luận bên dưới, và chúng ta sẽ cùng giải quyết. Chúc lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}