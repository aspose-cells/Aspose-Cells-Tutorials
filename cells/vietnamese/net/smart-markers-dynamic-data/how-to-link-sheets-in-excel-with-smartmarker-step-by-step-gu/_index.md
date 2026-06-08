---
category: general
date: 2026-06-08
description: Cách liên kết các sheet trong Excel bằng SmartMarkerProcessor cho báo
  cáo master‑detail. Điền dữ liệu vào sheet master và tạo báo cáo Excel master‑detail
  một cách dễ dàng.
draft: false
keywords:
- how to link sheets
- populate master sheet
- create master detail excel
- generate master detail report
language: vi
og_description: Cách liên kết các sheet trong Excel bằng SmartMarkerProcessor. Học
  cách điền dữ liệu vào sheet chính và tạo báo cáo chi tiết master trong vài phút.
og_title: Cách liên kết các sheet trong Excel bằng SmartMarker – Từng bước
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to link sheets in Excel using SmartMarkerProcessor for master‑detail
    reports. Populate master sheet and generate a master detail Excel report effortlessly.
  headline: How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide
  type: TechArticle
- description: How to link sheets in Excel using SmartMarkerProcessor for master‑detail
    reports. Populate master sheet and generate a master detail Excel report effortlessly.
  name: How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide
  steps:
  - name: Multiple Detail Rows per Master
    text: If a master row has several related details, SmartMarker repeats the master
      row once and then writes *all* matching detail rows beneath it. No extra code
      is needed—just ensure your `Details` collection contains every row.
  - name: Missing Details
    text: When a master entry has no matching detail rows, the detail sheet simply
      skips that section. If you need a placeholder (e.g., “No items”), you can add
      a calculated column in the template that uses an Excel formula like `=IF(COUNTA(A2:B2)=0,"No
      items","")`.
  - name: Large Datasets
    text: 'Processing tens of thousands of rows can be memory‑intensive. To keep performance
      snappy:'
  - name: Custom Column Mapping
    text: If your property names don’t line up (`MasterKey` vs `Id`), you can use
      the `SmartMarkerProcessor.Map` method to create an alias before processing.
  type: HowTo
tags:
- Excel
- SmartMarker
- C#
- master‑detail
title: Cách liên kết các sheet trong Excel bằng SmartMarker – Hướng dẫn từng bước
url: /vi/net/smart-markers-dynamic-data/how-to-link-sheets-in-excel-with-smartmarker-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Liên Kết Các Sheet trong Excel bằng SmartMarker – Hướng Dẫn Từng Bước

Bạn đã bao giờ tự hỏi **cách liên kết các sheet** trong Excel mà không cần sao chép hàng thủ công hoặc viết vô số vòng lặp VBA? Bạn không phải là người duy nhất. Hầu hết các nhà phát triển gặp khó khăn khi họ cần một báo cáo master‑detail sạch sẽ, luôn đồng bộ khi dữ liệu thay đổi. Tin tốt là gì? SmartMarkerProcessor thực hiện phần việc nặng cho bạn, biến một vài dòng C# thành một workbook master‑detail đầy đủ.

Trong hướng dẫn này, chúng tôi sẽ đi qua các bước chính xác để **điền dữ liệu vào master sheet**, thiết lập detail sheet, và cuối cùng **tạo báo cáo master detail** tự động cập nhật. Khi kết thúc, bạn sẽ có một mẫu có thể tái sử dụng và chèn vào bất kỳ dự án .NET nào.

> **Lưu ý tiền đề:** Bạn cần GrapeCity Documents for Excel (GcExcel) phiên bản 2024 hoặc mới hơn, môi trường phát triển .NET (Visual Studio 2022 hoạt động tốt), và kiến thức cơ bản về C#. Không cần thêm bất kỳ gói NuGet nào ngoài GcExcel.

---

## Tổng Quan Về Giải Pháp

Trước khi đi sâu vào mã, hãy phân tích ý nghĩa của “liên kết các sheet” trong ngữ cảnh của SmartMarker:

1. **Master sheet** – Giữ một hàng cho mỗi thực thể (ví dụ: danh sách khách hàng).
2. **Detail sheet** – Chứa các hàng thuộc về một hàng master (ví dụ: đơn hàng cho mỗi khách hàng).
3. **SmartMarker syntax** – Một ngôn ngữ đánh dấu nhỏ (`{MasterSheet}#master;{DetailSheet}#detail`) cho biết bộ xử lý cách liên kết hai bảng dữ liệu.
4. **Processor options** – Bật `MasterDetail` khiến engine tự động lặp lại các hàng master và chèn các hàng detail liên quan phía dưới.

Hiểu các thành phần này giúp bạn điều chỉnh cách tiếp cận sau này—có thể bạn cần lồng ba cấp hoặc định dạng có điều kiện. Hãy giữ mô hình tư duy này trong tay khi chúng ta thực hiện các bước.

---

## Bước 1: Chuẩn Bị Dữ Liệu Phân Cấp cho Xử Lý Master‑Detail

Điều đầu tiên bạn cần là một nguồn dữ liệu phản ánh mối quan hệ master‑detail. Trong hầu hết các trường hợp thực tế, dữ liệu này đến từ cơ sở dữ liệu, nhưng để minh bạch chúng ta sẽ sử dụng một đối tượng ẩn danh.

```csharp
// Step 1: Prepare hierarchical data for master‑detail processing
var sampleData = new
{
    // Master collection – one row per category
    Master = new[]
    {
        new { Id = 1, Name = "A" },
        new { Id = 2, Name = "B" }
    },

    // Detail collection – rows reference MasterId
    Details = new[]
    {
        new { MasterId = 1, Item = "Item1" },
        new { MasterId = 2, Item = "Item2" }
    }
};
```

**Tại sao điều này quan trọng:** SmartMarker không tự động đoán các mối quan hệ; nó tìm các tên thuộc tính khớp nhau (`MasterId` → `Id`). Bằng cách cấu trúc dữ liệu như vậy, chúng ta cung cấp cho bộ xử lý một bản đồ rõ ràng, là nền tảng của **cách liên kết các sheet** một cách hiệu quả.

> **Mẹo chuyên nghiệp:** Nếu dữ liệu của bạn ở trong các đối tượng `DataTable`, chỉ cần khai báo chúng như các thuộc tính với cùng tên—SmartMarker hoạt động với bất kỳ collection nào có thể lặp.

---

## Bước 2: Tạo Workbook và Tải Mẫu

SmartMarker hoạt động trên một workbook Excel hiện có, thường là một mẫu đã chứa tên sheet và các marker placeholder. Hãy tạo một workbook trong bộ nhớ và thêm hai worksheet trống có tên *MasterSheet* và *DetailSheet*.

```csharp
using GrapeCity.Documents.Excel;

// Step 2: Create a workbook and add template sheets
IWorkbook wb = new Workbook();

// Create the master sheet and add a header row
IWorksheet masterSheet = wb.Worksheets.Add("MasterSheet");
masterSheet.Range["A1"].Value = "ID";
masterSheet.Range["B1"].Value = "Name";

// Create the detail sheet and add its header
IWorksheet detailSheet = wb.Worksheets.Add("DetailSheet");
detailSheet.Range["A1"].Value = "Master ID";
detailSheet.Range["B1"].Value = "Item";
```

Bạn cũng có thể tải một tệp `.xlsx` từ đĩa (`wb.Open("Template.xlsx")`) nếu muốn thiết kế bố cục trong Excel trước. Điều quan trọng là tên sheet phải khớp với những tên bạn sẽ tham chiếu trong chuỗi SmartMarker.

---

## Bước 3: Khởi Tạo SmartMarkerProcessor và Bật Chế Độ Master‑Detail

Bây giờ chúng ta đưa vào engine sẽ đọc các marker và dán dữ liệu. `SmartMarkerProcessor` nhận workbook làm đối số của constructor, và cờ `Options.MasterDetail` chỉ cho nó xử lý các marker `#master` và `#detail` như một cặp liên kết.

```csharp
// Step 3: Create a SmartMarkerProcessor for the workbook
SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

// Enable master‑detail mode on the processor options
processor.Options.MasterDetail = true;
```

**Tại sao bật `MasterDetail`?** Nếu không có cờ này, bộ xử lý sẽ coi `{MasterSheet}#master` và `{DetailSheet}#detail` là các thao tác độc lập, mất mối quan hệ quan trọng giữa các hàng. Đặt cờ này là dòng lệnh duy nhất khiến **cách liên kết các sheet** thực sự hoạt động.

---

## Bước 4: Định Nghĩa Chuỗi SmartMarker và Chạy Processor

Chuỗi marker cho SmartMarker biết sheet nào là master và sheet nào là detail. Cú pháp đơn giản: `{SheetName}#master;{SheetName}#detail`. Bạn cũng có thể thêm các marker khác (ví dụ: `#header`) nhưng chúng không cần thiết cho một báo cáo cơ bản.

```csharp
// Step 4: Execute the smart‑marker processing, linking master and detail sheets
string marker = "{MasterSheet}#master;{DetailSheet}#detail";
processor.Process(marker, sampleData);
```

Khi `Process` chạy, engine:

1. Ghi mỗi hàng master vào *MasterSheet* bắt đầu từ hàng trống đầu tiên sau tiêu đề.
2. Đối với mỗi hàng master, nó quét collection `Details`, chọn các hàng có `MasterId` khớp với `Id` của master, và ghi chúng vào *DetailSheet* ngay dưới mục master tương ứng.

---

## Bước 5: Lưu hoặc Xuất Workbook Đã Tạo

Tại thời điểm này, bạn đã có một workbook được điền đầy đủ. Bạn có thể lưu nó vào đĩa, truyền lại cho client web, hoặc thậm chí chuyển đổi sang PDF.

```csharp
// Save the workbook to a file (you could also stream it to a response)
wb.Save("MasterDetailReport.xlsx");
```

Mở tệp và bạn sẽ thấy hai sheet: *MasterSheet* liệt kê `A` và `B`, trong khi *DetailSheet* hiển thị `Item1` dưới master `1` và `Item2` dưới master `2`. Đó là bản chất của **điền dữ liệu vào master sheet** và **tạo báo cáo master detail** trong một lần.

---

## Tổng Quan Trực Quan

![Diagram illustrating how to link sheets in Excel using SmartMarkerProcessor](https://example.com/diagram.png "How to link sheets diagram")

Sơ đồ (văn bản thay thế bao gồm từ khóa chính) cho thấy luồng dữ liệu từ các đối tượng C# → SmartMarkerProcessor → các sheet Excel được liên kết.

---

## Xử Lý Các Trường Hợp Đặc Biệt Thông Thường

### Nhiều Hàng Detail cho Mỗi Master

Nếu một hàng master có nhiều detail liên quan, SmartMarker sẽ lặp lại hàng master một lần và sau đó ghi *tất cả* các hàng detail phù hợp dưới nó. Không cần mã bổ sung—chỉ cần đảm bảo collection `Details` của bạn chứa mọi hàng.

### Thiếu Detail

Khi một mục master không có hàng detail phù hợp, sheet detail sẽ bỏ qua phần đó. Nếu bạn cần một placeholder (ví dụ: “No items”), bạn có thể thêm một cột tính toán trong mẫu sử dụng công thức Excel như `=IF(COUNTA(A2:B2)=0,"No items","")`.

### Dữ Liệu Lớn

Xử lý hàng chục ngàn hàng có thể tốn nhiều bộ nhớ. Để duy trì hiệu năng nhanh:

- Sử dụng `processor.Options.EnableStreaming = true` (có sẵn trong GcExcel 2025+).
- Chia dữ liệu thành các phần nhỏ và xử lý từng phần riêng biệt, sau đó hợp nhất các workbook.

### Ánh Xạ Cột Tùy Chỉnh

Nếu tên thuộc tính của bạn không khớp (`MasterKey` vs `Id`), bạn có thể sử dụng phương thức `SmartMarkerProcessor.Map` để tạo bí danh trước khi xử lý.

```csharp
processor.Map("MasterId", "Id"); // tells the engine that MasterId maps to Id
```

---

## Ví Dụ Hoàn Chỉnh Hoạt Động

Kết hợp tất cả lại, đây là một chương trình hoàn chỉnh, sẵn sàng sao chép‑dán mà bạn có thể chạy ngay lập tức.

```csharp
using System;
using GrapeCity.Documents.Excel;

namespace MasterDetailDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Prepare hierarchical data
            var sampleData = new
            {
                Master = new[]
                {
                    new { Id = 1, Name = "A" },
                    new { Id = 2, Name = "B" }
                },
                Details = new[]
                {
                    new { MasterId = 1, Item = "Item1" },
                    new { MasterId = 1, Item = "Item1‑Extra" },
                    new { MasterId = 2, Item = "Item2" }
                }
            };

            // 2️⃣ Create workbook and template sheets
            IWorkbook wb = new Workbook();

            var master = wb.Worksheets.Add("MasterSheet");
            master.Range["A1"].Value


## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Master External Link Formulas in Excel Using Aspose.Cells for Java](/cells/english/java/formulas-functions/aspose-cells-java-external-link-formulas-excel/)
- [Master Dynamic Excel Sheets in Java with Aspose.Cells&#58; A Comprehensive Guide](/cells/english/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)
- [Master Dynamic Excel Reports Using Aspose.Cells Java&#58; Named Ranges & Complex Formulas](/cells/english/java/templates-reporting/dynamic-excel-reports-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}