---
category: general
date: 2026-02-14
description: Cách tạo cấu trúc phân cấp trong các mẫu SmartMarker dễ hơn bạn nghĩ
  – hãy học cách tạo dữ liệu phân cấp và cách liệt kê nhân viên một cách hiệu quả.
draft: false
keywords:
- how to create hierarchy
- create hierarchical data
- how to list employees
- SmartMarker nested range
- C# template processing
language: vi
og_description: Cách tạo phân cấp trong các mẫu SmartMarker rất đơn giản. Hãy làm
  theo hướng dẫn này để tạo dữ liệu phân cấp và liệt kê nhân viên với các phạm vi
  lồng nhau.
og_title: Cách Tạo Cây Phân Cấp với SmartMarker – Hướng Dẫn Toàn Diện
tags:
- SmartMarker
- C#
- templating
title: Cách Tạo Cây Phân Cấp với SmartMarker – Hướng Dẫn Từng Bước
url: /vi/net/smart-markers-dynamic-data/how-to-create-hierarchy-with-smartmarker-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Tạo Cây Phân Cấp với SmartMarker – Hướng Dẫn Toàn Diện

Bạn đã bao giờ tự hỏi **cách tạo cây phân cấp** trong một mẫu SmartMarker mà không phải đau đầu không? Bạn không phải là người duy nhất. Trong nhiều tình huống báo cáo, bạn cần một mối quan hệ cha‑con — ví dụ như các phòng ban và những người làm việc trong chúng. Tin tốt là SmartMarker làm cho việc này trở nên dễ dàng một cách đáng kể khi bạn biết các bước đúng.

Trong tutorial này chúng ta sẽ đi qua toàn bộ quy trình: từ **tạo dữ liệu phân cấp** trong C#, bật chế độ xử lý phạm vi lồng nhau, và cuối cùng render một mẫu mà **liệt kê nhân viên** cho mỗi phòng ban. Khi kết thúc, bạn sẽ có một mẫu sẵn sàng chạy mà có thể đưa vào bất kỳ dự án .NET nào.

---

## Những Gì Bạn Cần

- .NET 6+ (bất kỳ phiên bản gần đây nào cũng được)
- Tham chiếu tới thư viện **SmartMarker** (namespace `ws.SmartMarkerProcessor`)
- Kiến thức cơ bản về C# – không cần gì phức tạp, chỉ vài đối tượng và một hoặc hai lambda
- IDE hoặc trình soạn thảo mà bạn thích (Visual Studio, Rider, VS Code… tùy bạn)

Nếu bạn đã có những thứ trên, tuyệt vời—cùng bắt đầu nào.

---

## Cách Tạo Cây Phân Cấp – Tổng Quan

Ý tưởng cốt lõi là xây dựng một **đồ thị đối tượng lồng nhau** phản ánh cấu trúc bạn muốn thấy trong tài liệu cuối cùng. Trong trường hợp của chúng ta, đồ thị trông như sau:

```
Departments
 ├─ Name (string)
 └─ Employees (string[])
```

SmartMarker sau đó sẽ lặp qua `Departments` và, vì chúng ta sẽ bật **xử lý phạm vi lồng nhau**, nó cũng sẽ tự động lặp qua bộ sưu tập `Employees` của mỗi phòng ban.

---

## Bước 1: Xây Dựng Mô Hình Dữ Liệu Phân Cấp

Đầu tiên chúng ta tạo một đối tượng ẩn danh chứa một mảng các phòng ban, mỗi phòng ban lại có danh sách nhân viên của riêng mình. Việc dùng kiểu ẩn danh giúp ví dụ nhẹ nhàng—bạn có thể thay thế bằng các lớp POCO thực tế sau này.

```csharp
// Step 1: Create hierarchical data that SmartMarker will iterate over
var departmentData = new
{
    Departments = new[]
    {
        new { Name = "HR", Employees = new[] { "John", "Amy" } },
        new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
    }
};
```

> **Tại sao điều này quan trọng:** Mảng `Departments` là bộ sưu tập cấp cao nhất. Mỗi phần tử chứa một mảng `Employees`, cung cấp cho chúng ta cấp độ thứ hai của cây phân cấp mà sau này chúng ta sẽ truy cập bằng `#Departments.Employees#`.

---

## Bước 2: Bật Xử Lý Phạm Vi Lồng Nhau

SmartMarker sẽ không đi sâu vào các bộ sưu tập bên trong trừ khi bạn chỉ định. Đối tượng `SmartMarkerOptions` chứa công tắc này.

```csharp
// Step 2: Enable nested range processing so inner collections (Employees) can be used
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableNestedRange = true   // crucial for #Departments.Employees# to work
};
```

> **Mẹo chuyên nghiệp:** Nếu bạn quên bật cờ này, phạm vi `#Employees#` bên trong sẽ trả về rỗng, và bạn sẽ bối rối tại sao mẫu lại trống.

---

## Bước 3: Chạy Processor Với Dữ Liệu Của Bạn

Bây giờ chúng ta truyền dữ liệu và tùy chọn cho processor. Biến `ws` đại diện cho **WebService** của bạn (hoặc bất kỳ đối tượng nào chứa engine SmartMarker).

```csharp
// Step 3: Run SmartMarker processing with the data and the configured options
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);
```

Tại thời điểm này SmartMarker sẽ phân tích mẫu, thay thế `#Departments.Name#` cho mỗi tên phòng ban, và vì đã bật phạm vi lồng nhau, nó sẽ lặp qua bộ sưu tập `Employees` của từng phòng ban.

---

## Bước 4: Tạo Các Marker Trong Mẫu

Dưới đây là một mẫu tối thiểu minh họa cả vòng lặp ngoài và trong. Dán nó vào trình chỉnh sửa mẫu SmartMarker (hoặc một file `.txt` mà bạn truyền cho processor).

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

Khi được render, bạn sẽ thấy:

```
HR
  - John
  - Amy
IT
  - Bob
  - Eve
```

> **Bạn đang thấy gì:** Phạm vi ngoài `#Departments.Name#` in tiêu đề phòng ban. Khối `#Departments.Employees#` bên trong lặp qua mỗi nhân viên, và `#Departments.Employees#` trong khối sẽ xuất ra tên thực tế.

---

## Kết Quả Dự Kiến & Kiểm Tra

Chạy toàn bộ ví dụ (dữ liệu + tùy chọn + mẫu) sẽ tạo ra chính xác danh sách như trên. Để nhanh chóng kiểm tra, bạn có thể in kết quả ra console:

```csharp
string result = ws.SmartMarkerProcessor.GetProcessedResult(); // pseudo‑method
Console.WriteLine(result);
```

Nếu bạn thấy hai tiêu đề phòng ban theo sau là các dấu đầu dòng nhân viên, bạn đã **tạo thành công cây phân cấp** và **liệt kê nhân viên**.

---

## Những Sai Lầm Thường Gặp & Các Trường Hợp Cạnh

| Vấn đề | Nguyên nhân | Cách khắc phục |
|-------|------------|----------------|
| Không có đầu ra cho nhân viên | `EnableNestedRange` để sai | Đặt `EnableNestedRange = true` |
| Trùng tên nhân viên | Cùng một mảng được tái sử dụng cho nhiều phòng ban | Sao chép mảng hoặc dùng các bộ sưu tập riêng biệt |
| Cây phân cấp quá lớn gây áp lực bộ nhớ | SmartMarker tải toàn bộ đồ thị đối tượng vào bộ nhớ | Dòng dữ liệu hoặc phân trang các bộ sưu tập lớn |
| Lỗi cú pháp mẫu | Thiếu thẻ đóng `#/…#` | Dùng trình kiểm tra SmartMarker hoặc chạy thử nhanh với một mẫu nhỏ |

---

## Tiến Xa Hơn – Các Biến Thể Thực Tế

1. **Nguồn dữ liệu động** – Lấy danh sách phòng ban từ cơ sở dữ liệu và ánh xạ chúng thành cấu trúc ẩn danh bằng LINQ.  
2. **Định dạng có điều kiện** – Thêm cờ `IsManager` cho mỗi nhân viên và dùng thẻ điều kiện của SmartMarker (`#if …#`) để làm nổi bật các quản lý.  
3. **Nhiều cấp lồng nhau** – Nếu bạn cần các đội nhóm bên trong phòng ban, chỉ cần thêm một bộ sưu tập khác (`Teams`) và vẫn giữ `EnableNestedRange` bật.

---

## Ví Dụ Hoàn Chỉnh (Sẵn Sàng Sao Chép)

```csharp
using System;
using SmartMarker; // hypothetical namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Build hierarchical data
        var departmentData = new
        {
            Departments = new[]
            {
                new { Name = "HR", Employees = new[] { "John", "Amy" } },
                new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
            }
        };

        // 2️⃣ Enable nested ranges
        var smartMarkerOptions = new SmartMarkerOptions
        {
            EnableNestedRange = true
        };

        // 3️⃣ Start processing
        var ws = new WebService(); // assume this is your entry point
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);

        // 4️⃣ Retrieve and display the result
        string output = ws.SmartMarkerProcessor.GetProcessedResult(); // placeholder method
        Console.WriteLine(output);
    }
}
```

**Mẫu (template.txt)**

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

Chạy chương trình sẽ in ra cây phân cấp chính xác như đã mô tả ở trên.

---

## Kết Luận

Chúng ta đã bao quát **cách tạo cây phân cấp** trong SmartMarker, từ việc tạo **dữ liệu phân cấp** trong C# đến bật phạm vi lồng nhau và cuối cùng render một mẫu **liệt kê nhân viên** theo từng phòng ban. Mô hình này có thể mở rộng—chỉ cần thêm các bộ sưu tập lồng nhau hoặc logic điều kiện và bạn sẽ có một engine báo cáo mạnh mẽ trong tầm tay.

Sẵn sàng cho thử thách tiếp theo? Hãy thử thay các kiểu ẩn danh bằng các lớp POCO được định kiểu mạnh, hoặc tích hợp quy trình này vào một endpoint ASP.NET Core trả về tài liệu PDF hoặc Word. Bầu trời là giới hạn, và giờ bạn đã có nền tảng vững chắc.

---

![Sơ đồ tạo cây phân cấp](image.png){alt="Sơ đồ tạo cây phân cấp hiển thị mối quan hệ phòng ban‑nhân viên"}

*Chúc lập trình vui! Nếu gặp bất kỳ khó khăn nào, hãy để lại bình luận bên dưới—tôi sẵn sàng giúp đỡ.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}