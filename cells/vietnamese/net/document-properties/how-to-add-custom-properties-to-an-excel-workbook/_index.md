---
category: general
date: 2026-10-01
description: Tìm hiểu cách thêm thuộc tính tùy chỉnh vào một workbook Excel bằng Aspose.Cells.
  Hướng dẫn này cũng chỉ cách thêm ID dự án và đọc các thuộc tính tùy chỉnh.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add custom properties
- how to add custom
- excel custom properties
- add project id
- read custom properties
language: vi
lastmod: 2026-10-01
og_description: Thêm các thuộc tính tùy chỉnh vào một sổ làm việc Excel bằng Aspose.Cells.
  Tham khảo hướng dẫn đầy đủ này để thêm ID dự án, thiết lập thông tin người đánh
  giá và đọc các thuộc tính tùy chỉnh một cách lập trình.
og_image_alt: Screenshot of an Excel worksheet displaying custom properties added
  via Aspose.Cells
og_title: Thêm thuộc tính tùy chỉnh vào sổ làm việc Excel – hướng dẫn từng bước
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  headline: How to add custom properties to an Excel workbook
  type: TechArticle
- description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  name: How to add custom properties to an Excel workbook
  steps:
  - name: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
    text: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
  - name: Go to **File → Info → Properties → Advanced Properties**.
    text: Go to **File → Info → Properties → Advanced Properties**.
  - name: Select the **Custom** tab.
    text: Select the **Custom** tab.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cách thêm thuộc tính tùy chỉnh vào sổ làm việc Excel
url: /vi/net/document-properties/how-to-add-custom-properties-to-an-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách thêm thuộc tính tùy chỉnh vào một workbook Excel

Nếu bạn cần **thêm thuộc tính tùy chỉnh** vào một workbook Excel, hướng dẫn này sẽ chỉ cho bạn cách thực hiện chính xác với Aspose.Cells for .NET. Bạn cũng sẽ học cách thêm ID dự án, đặt tên người xem xét, và sau đó **đọc lại các thuộc tính tùy chỉnh** từ tệp.

Làm việc với siêu dữ liệu tùy chỉnh cho phép bạn nhúng thông tin đặc thù của doanh nghiệp trực tiếp vào bảng tính, giúp dễ dàng theo dõi quyền sở hữu, phiên bản, hoặc bất kỳ ngữ cảnh nào khác mà không cần duy trì cơ sở dữ liệu riêng. Các bước dưới đây bao gồm quy trình hoàn chỉnh từ đầu đến cuối, từ việc tạo workbook đến việc lưu các thuộc tính mới.

## Yêu cầu trước

* .NET 6.0 hoặc phiên bản mới hơn được cài đặt  
* Giấy phép Aspose.Cells for .NET hợp lệ (hoặc bản dùng thử miễn phí)  
* Visual Studio 2022 (hoặc bất kỳ IDE C# nào)  

Không cần thêm bất kỳ gói NuGet nào ngoài `Aspose.Cells`.

## Bước 1: Thiết lập dự án và nhập không gian tên

Tạo một ứng dụng console mới và thêm tham chiếu Aspose.Cells:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // The rest of the code lives here
        }
    }
}
```

Không gian tên `Aspose.Cells` chứa các lớp `Workbook`, `Worksheet` và `CustomPropertyCollection` mà chúng ta sẽ sử dụng.

## Bước 2: Tải một workbook hiện có (hoặc tạo một workbook mới)

Bạn có thể bắt đầu với một tệp `.xlsb` hiện có hoặc tạo một workbook mới. Ví dụ dưới đây tải tệp có tên **Data.xlsb** nằm trong thư mục có tên `YOUR_DIRECTORY`.

```csharp
// Load the existing workbook
var workbookPath = @"YOUR_DIRECTORY\Data.xlsb";
var workbook = new Workbook(workbookPath);
```

Nếu tệp không tồn tại, thay thế mã bằng `new Workbook();` để tạo một workbook trống.

## Bước 3: Thêm thuộc tính tùy chỉnh vào worksheet đầu tiên

Hoạt động chính là **thêm thuộc tính tùy chỉnh** vào một worksheet. Aspose.Cells lưu trữ các thuộc tính tùy chỉnh trong một collection hoạt động giống như một từ điển.

```csharp
// Get the first worksheet (index 0)
var worksheet = workbook.Worksheets[0];

// Add a numeric ProjectId property
worksheet.CustomProperties.Add("ProjectId", 12345);

// Add a string Reviewer property
worksheet.CustomProperties.Add("Reviewer", "John Doe");

// Optional: add a DateTime property for the creation timestamp
worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);
```

Lý do chúng ta sử dụng `CustomProperties.Add` thay vì `CustomProperties["Name"] = value` là vì phương thức `Add` tạo mục nếu nó chưa tồn tại và đảm bảo kiểu dữ liệu đúng được lưu. Cách tiếp cận này ngăn ngừa việc không khớp kiểu dữ liệu gây lỗi thời gian chạy khi đọc các giá trị sau này.

## Bước 4: Lưu workbook với các thuộc tính mới

Sau khi bạn đã chèn siêu dữ liệu, lưu các thay đổi vào một tệp mới để tệp gốc không bị thay đổi.

```csharp
// Save the workbook with the custom properties
var outputPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Tại thời điểm này, tệp Excel chứa siêu dữ liệu tùy chỉnh mà bạn đã định nghĩa. Bạn có thể xác minh các thuộc tính bằng các bước trong phần tiếp theo.

## Bước 5: Đọc thuộc tính tùy chỉnh từ một workbook

Đọc **thuộc tính tùy chỉnh của excel** tuân theo cùng mẫu collection. Đoạn mã này minh họa cách lấy lại các giá trị mà chúng ta vừa lưu.

```csharp
// Load the workbook that contains custom properties
var loadedWorkbook = new Workbook(outputPath);
var loadedWorksheet = loadedWorkbook.Worksheets[0];
var props = loadedWorksheet.CustomProperties;

// Retrieve each property safely
int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

Console.WriteLine($"ProjectId: {projectId}");
Console.WriteLine($"Reviewer: {reviewer}");
Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
```

`CustomPropertyCollection` indexer trả về một đối tượng `CustomProperty`; truy cập thuộc tính `Value` của nó sẽ cho bạn dữ liệu đã lưu ở kiểu gốc. Kiểm tra `null` trước khi ép kiểu tránh `NullReferenceException` nếu một thuộc tính bị thiếu.

### Đầu ra console dự kiến

```
ProjectId: 12345
Reviewer: John Doe
CreatedOn (UTC): 2026-10-01 12:34:56Z
```

Dấu thời gian sẽ phản ánh chính xác thời điểm bạn gọi `Add` ở bước 3.

## Mẹo chuyên nghiệp: Cập nhật thuộc tính tùy chỉnh hiện có

Nếu bạn cần **thêm thông tin tùy chỉnh** sau này (ví dụ, thay đổi người xem xét), hãy sử dụng setter của `CustomPropertyCollection`:

```csharp
// Change the reviewer name
if (props["Reviewer"] != null)
{
    props["Reviewer"].Value = "Jane Smith";
}
else
{
    // Property does not exist; add it
    props.Add("Reviewer", "Jane Smith");
}
```

Mẫu này đảm bảo rằng thuộc tính sẽ được cập nhật hoặc tạo mới, hữu ích trong các quy trình lặp lại như tạo báo cáo tự động.

## Bước 6: Xác minh các thuộc tính trong Excel (tùy chọn)

Bạn cũng có thể xem các thuộc tính tùy chỉnh trực tiếp trong Excel:

1. Mở tệp `DataWithProps.xlsb` đã lưu trong Microsoft Excel.  
2. Chọn **File → Info → Properties → Advanced Properties**.  
3. Chọn tab **Custom**.  

Bạn sẽ thấy các mục `ProjectId`, `Reviewer` và `CreatedOn` được liệt kê cùng với các giá trị tương ứng.

## Ví dụ hoạt động đầy đủ

Dưới đây là chương trình hoàn chỉnh, tự chứa, kết hợp tất cả các đoạn mã trước. Sao chép nó vào `Program.cs` và chạy; console sẽ hiển thị các giá trị đã lấy.

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // Paths (adjust to your environment)
            var sourcePath = @"YOUR_DIRECTORY\Data.xlsb";
            var resultPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";

            // Load or create workbook
            var workbook = new Workbook(sourcePath);
            var worksheet = workbook.Worksheets[0];

            // Add custom properties
            worksheet.CustomProperties.Add("ProjectId", 12345);
            worksheet.CustomProperties.Add("Reviewer", "John Doe");
            worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);

            // Save the workbook
            workbook.Save(resultPath);
            Console.WriteLine($"Saved workbook with custom properties to {resultPath}");

            // Load the saved workbook to read properties
            var loadedWorkbook = new Workbook(resultPath);
            var loadedWorksheet = loadedWorkbook.Worksheets[0];
            var props = loadedWorksheet.CustomProperties;

            // Read properties
            int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
            string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
            DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

            Console.WriteLine($"ProjectId: {projectId}");
            Console.WriteLine($"Reviewer: {reviewer}");
            Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
        }
    }
}
```

Chạy chương trình này sẽ tạo ra đầu ra console như đã hiển thị trước và tạo tệp `DataWithProps.xlsb` chứa siêu dữ liệu được nhúng.

## Các câu hỏi thường gặp và trường hợp đặc biệt

| Question | Answer |
|---|---|
| **Có thể lưu các kiểu không nguyên thủy không?** | Aspose.Cells hỗ trợ `string`, `int`, `double`, `DateTime` và `bool`. Đối với các đối tượng phức tạp, hãy tuần tự hoá chúng thành JSON hoặc XML trước và lưu dưới dạng chuỗi. |
| **Nếu workbook được bảo vệ bằng mật khẩu thì sao?** | Mở workbook bằng mật khẩu (`new Workbook(path, password)`) trước khi truy cập `CustomProperties`. Các thuộc tính vẫn có thể truy cập được sau khi giải mã. |
| **Các thuộc tính tùy chỉnh có tồn tại sau khi chuyển đổi định dạng không?** | Khi lưu sang định dạng khác (ví dụ, `.xlsx`), Aspose.Cells giữ lại các thuộc tính tùy chỉnh miễn là định dạng đích hỗ trợ chúng. |
| **Cách xóa một thuộc tính tùy chỉnh?** | Sử dụng `worksheet.CustomProperties.Remove("PropertyName");`. Điều này sẽ xóa mục khỏi collection. |

## Các bước tiếp theo

Bây giờ bạn đã biết **cách thêm thuộc tính tùy chỉnh**, bạn có thể khám phá các chủ đề liên quan như:

* **excel custom properties** cho việc quản lý phiên bản tài liệu  
* **read custom properties** từ nhiều worksheet trong một workbook  
* Sử dụng **Aspose.Cells** để tạo pivot table tham chiếu siêu dữ liệu tùy chỉnh  
* Xuất workbook ra PDF trong khi giữ lại các thuộc tính tùy chỉnh  

Thử nghiệm với các kiểu dữ liệu khác nhau, kết hợp thuộc tính tùy chỉnh với bình luận ô, hoặc tích hợp siêu dữ liệu vào hệ thống quản lý tài liệu lớn hơn.

---

**Sẵn sàng tự động hoá báo cáo Excel của bạn?** Thêm mã trên vào dự án của bạn, điều chỉnh tên thuộc tính cho phù hợp với nhu cầu kinh doanh, và bạn sẽ có một bảng tính tự mô tả sẵn sàng cho quá trình xử lý tiếp theo.

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với các giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Tạo Workbook Excel – Thêm Thuộc Tính Tùy Chỉnh và Lưu dưới dạng XLSB](/cells/english/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/)
- [Cách Truy Cập Thuộc Tính Tài Liệu Tùy Chỉnh trong Excel bằng Aspose.Cells cho .NET](/cells/english/net/workbook-operations/access-custom-excel-properties-aspose-cells-net/)
- [Làm Chủ Thuộc Tính Tùy Chỉnh trong Excel bằng Aspose.Cells .NET cho Quản Lý Dữ Liệu Nâng Cao](/cells/english/net/data-manipulation/excel-custom-properties-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}