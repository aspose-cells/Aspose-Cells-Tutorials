---
category: general
date: 2026-11-19
description: Cách lặp lại bảng tính khi điền dữ liệu mảng vào Excel. Học cách tạo
  nhiều bảng tính và điền dữ liệu vào bảng tính từ danh sách trong vài bước.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to repeat worksheet
- populate excel with array
- generate multiple worksheets
- populate worksheet from list
language: vi
lastmod: 2026-11-19
og_description: Cách lặp lại bảng tính bằng SmartMarkerProcessor. Hãy làm theo hướng
  dẫn này để điền dữ liệu mảng vào Excel, tạo nhiều bảng tính và điền dữ liệu vào
  bảng tính từ danh sách.
og_image_alt: Screenshot showing repeated worksheets in an Excel workbook after processing
og_title: Cách lặp lại bảng tính trong Excel – hướng dẫn từng bước
schemas:
- author: GroupDocs
  dateModified: '2026-11-19'
  description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  headline: How to repeat worksheet in Excel with SmartMarkerProcessor
  type: TechArticle
- description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  name: How to repeat worksheet in Excel with SmartMarkerProcessor
  steps:
  - name: Expected output
    text: 'When you open the resulting workbook, you should see:'
  - name: Empty or null arrays
    text: 'If `Dept` is null or empty, the processor will not create any additional
      worksheets. To avoid a completely blank workbook, you can add a guard:'
  - name: Custom worksheet names
    text: 'The default naming scheme may not suit every reporting requirement. After
      processing, rename each sheet using a loop:'
  - name: Populating additional columns
    text: 'If you need to **populate excel with array** values beyond a single marker,
      extend the data object:'
  type: HowTo
tags:
- Excel automation
- SmartMarkerProcessor
- .NET
title: Cách lặp lại worksheet trong Excel bằng SmartMarkerProcessor
url: /vi/net/smart-markers-dynamic-data/how-to-repeat-worksheet-in-excel-with-smartmarkerprocessor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách lặp lại worksheet trong Excel với SmartMarkerProcessor

Nếu bạn cần **how to repeat worksheet** khi tạo báo cáo Excel, hướng dẫn này sẽ cho bạn một giải pháp hoàn chỉnh, có thể chạy được. Khi kết thúc tutorial, bạn sẽ có thể **populate Excel with array** dữ liệu, **generate multiple worksheets**, và **populate worksheet from list** bằng thư viện SmartMarkerProcessor.

Lặp lại một worksheet là yêu cầu phổ biến khi mỗi phòng ban, khu vực, hoặc thời kỳ cần một tab riêng. Ví dụ dưới đây trình bày các bước chính xác, giải thích lý do mỗi cài đặt quan trọng, và bao gồm các trường hợp đặc biệt như danh sách rỗng hoặc đặt tên tùy chỉnh.

## Yêu cầu trước

- .NET 6.0 hoặc phiên bản mới hơn đã được cài đặt
- Tham chiếu tới gói NuGet **GroupDocs.Viewer** (hoặc tương đương) chứa `SmartMarkerProcessor`
- Một workbook mẫu Excel (`.xlsx`) với một marker như `${repeat:Dept}` được đặt trong một hàng bạn muốn lặp lại
- Kiến thức cơ bản về C# và LINQ (tùy chọn nhưng hữu ích)

Không cần thêm bất kỳ thư viện bên thứ ba nào.

## Bước 1: Tạo instance SmartMarkerProcessor

Bộ xử lý điều phối việc thay thế marker và sao chép worksheet. Khởi tạo nó mà không truyền đối số sẽ sử dụng các tùy chọn mặc định.

```csharp
// Step 1: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

Tạo bộ xử lý sớm cho phép bạn cấu hình các tùy chọn toàn cục trước khi bất kỳ dữ liệu nào được áp dụng. Đây là nền tảng cho **how to repeat worksheet** một cách chính xác.

## Bước 2: Bật tính năng lặp lại worksheet

Mặc định, bộ xử lý chỉ thay thế các marker trên sheet hiện tại. Đặt `RepeatWorksheet` thành `true` sẽ yêu cầu engine sao chép toàn bộ worksheet cho mỗi mục trong bộ dữ liệu.

```csharp
// Step 2: Enable worksheet repetition for the ${repeat:Dept} marker
processor.Options.RepeatWorksheet = true;
```

Bật tùy chọn này là chìa khóa để **generate multiple worksheets**—bộ xử lý sẽ tạo một tab mới cho mỗi phần tử trong mảng `Dept` và giữ nguyên định dạng gốc.

## Bước 3: Chuẩn bị nguồn dữ liệu dưới dạng mảng hoặc danh sách

SmartMarkerProcessor làm việc với bất kỳ enumerable nào, nhưng sử dụng mảng giúp ý định rõ ràng hơn khi bạn muốn **populate worksheet from list**. Ở đây chúng ta tạo một đối tượng ẩn danh chứa thuộc tính `Dept` là một mảng string.

```csharp
// Step 3: Prepare the data source with a list of departments
var data = new { Dept = new[] { "HR", "IT", "Finance" } };
```

Nếu bạn đã có một `List<string>` bạn có thể truyền trực tiếp; bộ xử lý sẽ xử lý nó tương tự. Điều quan trọng là tên thuộc tính (`Dept`) phải khớp với marker `${repeat:Dept}` trong mẫu.

## Bước 4: Tải worksheet mẫu

Giả sử bạn có một `ExcelPackage` (từ EPPlus) hoặc một đối tượng `Workbook`, lấy worksheet bạn muốn lặp lại. Biến `ws` đại diện cho sheet đó.

```csharp
// Example using EPPlus to load the template workbook
using var package = new OfficeOpenXml.ExcelPackage(new FileInfo("Template.xlsx"));
var ws = package.Workbook.Worksheets[0]; // first worksheet
```

Nếu bạn thích một thư viện khác (ví dụ, ClosedXML), nguyên tắc vẫn giống nhau: lấy một đối tượng worksheet thực hiện giao diện yêu cầu.

## Bước 5: Xử lý worksheet với dữ liệu

Bây giờ áp dụng dữ liệu vào mẫu. Bộ xử lý sao chép worksheet cho mỗi phòng ban, thay thế marker `${repeat:Dept}` bằng tên phòng ban thực tế, và giữ nguyên phần còn lại của sheet.

```csharp
// Step 5: Apply the data to the template worksheet (ws)
processor.Process(ws, data);
```

Sau khi `Process` hoàn thành, `ws` trở thành worksheet đầu tiên trong số nhiều worksheet—một cho mỗi phòng ban. Tên sheet gốc được giữ nguyên, trong khi các bản sao nhận hậu tố tăng dần (ví dụ, “Sheet1 (1)”, “Sheet1 (2)”). Bạn có thể đổi tên chúng sau nếu cần một scheme đặt tên tùy chỉnh.

### Kết quả mong đợi

Khi bạn mở workbook kết quả, bạn sẽ thấy:

- **Sheet1** – mẫu gốc (thường để trống hoặc dùng làm master)
- **Sheet1 (1)** – được điền dữ liệu “HR”
- **Sheet1 (2)** – được điền dữ liệu “IT”
- **Sheet1 (3)** – được điền dữ liệu “Finance”

Mỗi sheet có cùng bố cục nhưng tên phòng ban được thay thế tại vị trí `${repeat:Dept}` xuất hiện.

## Xử lý các trường hợp đặc biệt

### Mảng rỗng hoặc null

Nếu `Dept` là null hoặc rỗng, bộ xử lý sẽ không tạo thêm worksheet nào. Để tránh một workbook hoàn toàn trống, bạn có thể thêm một guard:

```csharp
if (data.Dept != null && data.Dept.Any())
{
    processor.Process(ws, data);
}
else
{
    // Optionally write a warning or keep the original sheet unchanged
}
```

### Tên worksheet tùy chỉnh

Scheme đặt tên mặc định có thể không phù hợp với mọi yêu cầu báo cáo. Sau khi xử lý, đổi tên mỗi sheet bằng một vòng lặp:

```csharp
for (int i = 1; i <= data.Dept.Length; i++)
{
    var sheet = package.Workbook.Worksheets[i]; // index 0 is the original
    sheet.Name = data.Dept[i - 1]; // use department name as tab title
}
```

### Điền thêm các cột

Nếu bạn cần **populate excel with array** giá trị vượt quá một marker duy nhất, mở rộng đối tượng dữ liệu:

```csharp
var data = new
{
    Dept = new[]
    {
        new { Name = "HR", Headcount = 12 },
        new { Name = "IT", Headcount = 25 },
        new { Name = "Finance", Headcount = 8 }
    }
};
```

Sau đó điều chỉnh các marker trong mẫu thành `${repeat:Dept.Name}` và `${repeat:Dept.Headcount}`. Bộ xử lý sẽ lặp lại hàng cho mỗi phòng ban và điền cả hai cột.

## Ví dụ đầy đủ hoạt động

Dưới đây là một ứng dụng console tự chứa, minh họa toàn bộ quy trình từ tải mẫu đến lưu workbook cuối cùng.

```csharp
using System;
using System.IO;
using OfficeOpenXml;               // Install-Package EPPlus
using GroupDocs.Viewer.Markup;    // SmartMarkerProcessor namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Create processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 2️⃣ Enable worksheet repetition
        processor.Options.RepeatWorksheet = true;

        // 3️⃣ Define data source (array of departments)
        var data = new { Dept = new[] { "HR", "IT", "Finance" } };

        // 4️⃣ Load template workbook (ensure Template.xlsx exists)
        var fileInfo = new FileInfo("Template.xlsx");
        using var package = new ExcelPackage(fileInfo);
        var ws = package.Workbook.Worksheets[0]; // first sheet contains ${repeat:Dept}

        // 5️⃣ Process template
        processor.Process(ws, data);

        // Optional: rename generated sheets
        for (int i = 1; i <= data.Dept.Length; i++)
        {
            var sheet = package.Workbook.Worksheets[i];
            sheet.Name = data.Dept[i - 1];
        }

        // Save the result
        var output = new FileInfo("Result.xlsx");
        package.SaveAs(output);

        Console.WriteLine("Workbook generated with repeated worksheets.");
    }
}
```

**Giải thích các phần chính**

- **Processor creation** – thiết lập engine sẽ diễn giải các marker.
- **RepeatWorksheet option** – kích hoạt tính năng cốt lõi trả lời *how to repeat worksheet*.
- **Data source** – sử dụng một mảng (`new[]`) để đáp ứng **populate excel with array**.
- **Template loading** – minh họa cách phổ biến để lấy một đối tượng worksheet.
- **Processing** – thực hiện việc sao chép và chèn dữ liệu trong một lần gọi.
- **Renaming** – cho thấy cách chuyển các tên chung “(1)”, “(2)” thành tiêu đề có ý nghĩa, một yêu cầu điển hình sau **generate multiple worksheets**.

Chạy chương trình này sẽ tạo ra `Result.xlsx` với ba tab riêng cho từng phòng ban, mỗi tab được điền dữ liệu từ mảng.

## Những lỗi thường gặp và mẹo chuyên nghiệp

- **Marker spelling** – marker phải khớp chính xác với tên thuộc tính (`${repeat:Dept}`). Một lỗi chính tả sẽ ngăn việc lặp lại.
- **Worksheet index** – sau khi xử lý, sheet gốc vẫn ở chỉ mục 0; các sheet được tạo ra theo thứ tự liên tiếp. Sai chỉ mục có thể dẫn đến việc đổi tên tab sai.
- **Large data sets** – tạo hàng trăm worksheet có thể làm tăng kích thước file đáng kể. Hãy cân nhắc chia báo cáo hoặc dùng một sheet duy nhất với các phần nhóm nếu hiệu năng gặp vấn đề.
- **Thread safety** – `SmartMarkerProcessor` không an toàn với đa luồng. Tạo một instance riêng cho mỗi luồng nếu bạn xử lý nhiều workbook đồng thời.

## Kết luận

Bây giờ bạn đã biết **how to repeat worksheet** trong Excel bằng SmartMarkerProcessor, cách **populate excel with array** dữ liệu, cách **generate multiple worksheets**, và cách **populate worksheet from list** một cách hiệu quả. Ví dụ hoàn chỉnh kết hợp tất cả các khái niệm, và bước đổi tên tùy chọn cho phép bạn tạo ra các tên tab sạch sẽ, thân thiện với người dùng.

Tiếp theo, bạn có thể khám phá:

- Sử dụng **populate worksheet from list** với các đối tượng phức tạp (các collection lồng nhau)
- Áp dụng định dạng có điều kiện sau khi sao chép worksheet
- Xuất workbook đã tạo ra sang PDF hoặc CSV để sử dụng tiếp downstream

Hãy tự do điều chỉnh mã cho các kịch bản báo cáo của bạn, và tận hưởng việc tự động hoá workbook Excel một cách tự tin!

## Bạn Nên Học Gì Tiếp Theo?

Các tutorial sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách Lặp Lại Worksheets – Hướng Dẫn Toàn Diện cho Tự Động Hóa Excel](/cells/english/net/smart-markers-dynamic-data/how-to-repeat-worksheets-complete-guide-for-excel-automation/)
- [Tạo Worksheet Cho Mỗi Mục – Cách Lặp Lại Worksheet trong C#](/cells/english/net/worksheet-operations/create-worksheet-per-item-how-to-repeat-worksheet-in-c/)
- [Cách mở rộng mảng trong Excel và điền vào mẫu](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}