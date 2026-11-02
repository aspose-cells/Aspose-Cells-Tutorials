---
category: general
date: 2026-07-03
description: Bài hướng dẫn master‑detail Excel cho thấy cách điền dữ liệu vào mẫu
  Excel và tạo file Excel từ mẫu bằng Smart Markers – hướng dẫn nhanh, ưu tiên code.
draft: false
keywords:
- master detail excel
- populate excel template
- generate excel from template
- use smart markers
- how to create master‑detail report
language: vi
og_description: Hướng dẫn master‑detail Excel dạy bạn cách điền dữ liệu vào mẫu Excel
  và tạo file Excel từ mẫu bằng Smart Markers trong C#.
og_title: Excel master-detail – Điền mẫu bằng Smart Markers
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: master detail excel tutorial shows how to populate excel template and
    generate excel from template using Smart Markers – quick, code‑first guide.
  headline: master detail excel guide – populate templates with Smart Markers
  type: TechArticle
- description: master detail excel tutorial shows how to populate excel template and
    generate excel from template using Smart Markers – quick, code‑first guide.
  name: master detail excel guide – populate templates with Smart Markers
  steps:
  - name: '**Loading the template** – By keeping the template separate, you preserve
      formatting, formulas, and any static content. The `Workbook` constructor reads
      the file into memory without locking it, which is essential for web‑service
      scenarios.'
    text: '**Loading the template** – By keeping the template separate, you preserve
      formatting, formulas, and any static content. The `Workbook` constructor reads
      the file into memory without locking it, which is essential for web‑service
      scenarios.'
  - name: '**Hierarchical data model** – Smart Markers rely on *named* collections
      (`Master`, `Detail`). The anonymous type we create mirrors the relational structure:
      each master row can have multiple detail rows sharing the same `Id`. This is
      the same pattern you’d use with a DataSet or Entity Framework quer'
    text: '**Hierarchical data model** – Smart Markers rely on *named* collections
      (`Master`, `Detail`). The anonymous type we create mirrors the relational structure:
      each master row can have multiple detail rows sharing the same `Id`. This is
      the same pattern you’d use with a DataSet or Entity Framework quer'
  - name: '**SmartMarkerProcessor** – This class is the heart of the **use smart markers**
      feature. It parses the worksheet, builds an internal map of markers, and then
      iterates over the data model. You don’t need to manually loop through rows;
      the processor does it for you, guaranteeing correct cell merging a'
    text: '**SmartMarkerProcessor** – This class is the heart of the **use smart markers**
      feature. It parses the worksheet, builds an internal map of markers, and then
      iterates over the data model. You don’t need to manually loop through rows;
      the processor does it for you, guaranteeing correct cell merging a'
  - name: '**Process call** – The single `processor.Process(workbook, dataModel)`
      line triggers the expansion of both master and detail ranges. If your template
      includes grouping, totals, or conditional formatting, the processor respects
      those as well.'
    text: '**Process call** – The single `processor.Process(workbook, dataModel)`
      line triggers the expansion of both master and detail ranges. If your template
      includes grouping, totals, or conditional formatting, the processor respects
      those as well.'
  - name: '**Saving the result** – The final `Save` call writes a brand‑new file (`MasterDetail.xlsx`).
      Because the original template remains untouched, you can reuse it for subsequent
      runs—perfect for batch jobs.'
    text: '**Saving the result** – The final `Save` call writes a brand‑new file (`MasterDetail.xlsx`).
      Because the original template remains untouched, you can reuse it for subsequent
      runs—perfect for batch jobs.'
  type: HowTo
tags:
- Excel automation
- C#
- Aspose.Cells
title: Hướng dẫn Excel master-detail – điền mẫu bằng Smart Markers
url: /vi/net/smart-markers-dynamic-data/master-detail-excel-guide-populate-templates-with-smart-mark/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# master detail excel – Điền dữ liệu vào mẫu Excel bằng Smart Markers

Bạn đã bao giờ tự hỏi làm sao để **master detail excel** báo cáo mà không phải sao chép‑dán thủ công? Bạn không phải là người duy nhất. Ở nhiều doanh nghiệp, nhu cầu tạo báo cáo master‑detail—ví dụ hoá đơn có các mục chi tiết hoặc danh mục sản phẩm kèm thông số—là công việc hằng ngày. Tin tốt? Chỉ với vài dòng C# bạn có thể **populate excel template** tự động, để Smart Markers thực hiện phần việc nặng.

Trong tutorial này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, có thể chạy được, cho thấy **how to create master‑detail report** bằng engine Smart Marker của Aspose.Cells. Khi kết thúc, bạn sẽ có thể **generate excel from template** trong vài giây, và hiểu lý do đằng sau mỗi bước để có thể áp dụng mẫu này cho nguồn dữ liệu của riêng bạn.

## What You’ll Need

Trước khi bắt đầu, hãy chắc chắn bạn có:

- .NET 6.0 hoặc mới hơn (mã cũng chạy được với .NET Framework 4.6+)
- Gói NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`)
- Một file Excel đơn giản (`template.xlsx`) chứa Smart Markers như `{Master}` và `{Detail}`
- IDE mà bạn thích (Visual Studio, Rider, VS Code…)

Đó là tất cả—không cần thư viện phụ, không cần COM interop, chỉ C# thuần.

> **Pro tip:** Giữ mẫu của bạn trong cùng thư mục với dự án để dễ xử lý đường dẫn, hoặc dùng một thiết lập cấu hình nếu bạn đóng gói ứng dụng.

## master detail excel: Preparing the Smart Marker Template

Smart Markers là các placeholder mà Aspose.Cells thay thế bằng dữ liệu tại thời gian chạy. Đối với kịch bản master‑detail, bạn thường cần hai marker:

| Marker   | Purpose                              |
|----------|--------------------------------------|
| `{Master}` | Expands a row for each master record |
| `{Detail}` | Expands a nested range for related details |

Mở Excel, nhập một vài tiêu đề tĩnh, sau đó ở hàng mà bạn muốn dữ liệu master viết `{Master.Id}` và `{Master.Name}`. Bên dưới, tạo một bảng phụ và đặt `{Detail.Id}` và `{Detail.Item}` vào các ô thích hợp. Lưu file dưới tên `template.xlsx`.

![master detail excel report example](https://example.com/placeholder.png "master detail excel report example")

*Văn bản thay thế ảnh: ví dụ báo cáo master detail excel hiển thị các placeholder Smart Marker.*

## Step‑by‑Step Code Walkthrough

Dưới đây là chương trình đầy đủ, tự chứa. Chúng ta sẽ chia nó thành các khối logic, giải thích lý do, và chỉ ra các lỗi thường gặp.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // Step 1: Load the Excel template that contains Smart Markers {Master}
        //         and {Detail}
        // -----------------------------------------------------------------
        var templatePath = @"YOUR_DIRECTORY/template.xlsx";
        Workbook workbook = new Workbook(templatePath);

        // -----------------------------------------------------------------
        // Step 2: Build a hierarchical data model (master collection + detail)
        // -----------------------------------------------------------------
        var dataModel = new
        {
            Master = new[]
            {
                new { Id = 1, Name = "Alpha" },
                new { Id = 2, Name = "Beta" }
            },
            Detail = new[]
            {
                new { Id = 1, Item = "Item X" },
                new { Id = 1, Item = "Item Y" },
                new { Id = 2, Item = "Item Z" }
            }
        };

        // -----------------------------------------------------------------
        // Step 3: Create a SmartMarkerProcessor – this is the engine that
        //         scans the workbook, finds markers, and injects data.
        // -----------------------------------------------------------------
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // -----------------------------------------------------------------
        // Step 4: Apply the data model to the workbook. The processor will
        //         automatically expand master‑detail ranges based on the
        //         relationships defined in the model.
        // -----------------------------------------------------------------
        processor.Process(workbook, dataModel);

        // -----------------------------------------------------------------
        // Step 5: Save the populated workbook – now you have a ready‑to‑use
        //         master‑detail Excel file.
        // -----------------------------------------------------------------
        var outputPath = @"YOUR_DIRECTORY/MasterDetail.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine("Excel file generated successfully at: " + outputPath);
    }
}
```

### Why This Structure Works

1. **Loading the template** – Bằng cách giữ mẫu riêng biệt, bạn bảo toàn định dạng, công thức và bất kỳ nội dung tĩnh nào. Hàm khởi tạo `Workbook` đọc file vào bộ nhớ mà không khóa nó, điều này rất quan trọng cho các kịch bản dịch vụ web.

2. **Hierarchical data model** – Smart Markers dựa vào các collection *được đặt tên* (`Master`, `Detail`). Kiểu ẩn danh chúng ta tạo ra phản ánh cấu trúc quan hệ: mỗi hàng master có thể có nhiều hàng detail cùng `Id`. Đây là mẫu tương tự bạn sẽ dùng với DataSet hoặc kết quả truy vấn Entity Framework.

3. **SmartMarkerProcessor** – Lớp này là trái tim của tính năng **use smart markers**. Nó phân tích worksheet, xây dựng bản đồ nội bộ của các marker, và sau đó lặp qua mô hình dữ liệu. Bạn không cần tự viết vòng lặp qua các hàng; processor làm việc này cho bạn, đảm bảo việc gộp ô và giữ nguyên style đúng.

4. **Process call** – Dòng lệnh duy nhất `processor.Process(workbook, dataModel)` kích hoạt việc mở rộng cả phạm vi master và detail. Nếu mẫu của bạn có nhóm, tổng, hoặc định dạng có điều kiện, processor cũng sẽ tôn trọng chúng.

5. **Saving the result** – Lệnh `Save` cuối cùng ghi ra một file mới hoàn toàn (`MasterDetail.xlsx`). Vì mẫu gốc không bị thay đổi, bạn có thể tái sử dụng cho các lần chạy tiếp theo—lý tưởng cho các job batch.

### Edge Cases & How to Handle Them

| Situation                               | What to watch for                              | Suggested fix |
|----------------------------------------|-----------------------------------------------|---------------|
| No matching detail rows for a master   | The detail block will be empty, but the master row still appears. | Ensure your LINQ or data source returns an empty collection rather than `null`. |
| Large data sets (10k+ rows)            | Memory consumption can spike during processing. | Use `SmartMarkerProcessor` with `SmartMarkerOptions` to enable streaming (`processor.Options = new SmartMarkerOptions { UseFastProcessing = true };`). |
| Custom formatting on detail rows       | Formatting can be lost if the template row isn’t styled. | Apply the desired style to the *first* detail row in the template; the processor clones it for each new row. |
| Need to insert a grand‑total row        | Smart Markers don’t calculate totals automatically. | Add a normal Excel formula in the template that references the expanded range (e.g., `=SUM(C2:C{Detail.RowCount})`). |

## populate excel template: Testing the Output

Chạy chương trình. Mở `MasterDetail.xlsx` và bạn sẽ thấy một bảng như sau:

| Id | Name  | Id (Detail) | Item   |
|----|-------|-------------|--------|
| 1  | Alpha | 1           | Item X |
|    |       | 1           | Item Y |
| 2  | Beta  | 2           | Item Z |

Chú ý cách các hàng master (`Alpha`, `Beta`) được gộp lại qua các cột detail, tạo nên giao diện master‑detail sạch sẽ. Tất cả công thức, định dạng có điều kiện và độ rộng cột từ mẫu gốc đều được giữ nguyên.

Nếu bạn không thấy các hàng mong muốn, hãy kiểm tra lại:

- Tên marker phải khớp với tên thuộc tính trong mô hình dữ liệu (phân biệt chữ hoa/thường).  
- Các ô marker trong mẫu phải *ở trong* một bảng hoặc một named range; nếu không, processor có thể coi chúng là các ô riêng lẻ.  

## generate excel from template: Extending the Pattern

Bây giờ bạn đã nắm vững các nguyên tắc cơ bản, có thể dễ dàng điều chỉnh mã cho các kịch bản phức tạp hơn:

- **Multiple master tables** – Thêm một collection khác (ví dụ `Orders`) và các marker tương ứng (`{Orders}`) trong một worksheet riêng.  
- **Dynamic worksheets** – Tạo một `Worksheet` mới tại thời gian chạy, sao chép sheet mẫu, rồi chạy `processor.Process` trên sheet mới.  
- **Web API endpoint** – Trả về workbook đã tạo dưới dạng `FileResult` (`return File(workbook.SaveToStream(), "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "Report.xlsx");`).  

Tất cả đều tuân theo nguyên tắc **populate excel template**: load, bind, process, save.

## How to Create Master‑Detail Report: Common Questions

**Q: Do I need to install Microsoft Office on the server?**  
No. Aspose.Cells là thư viện .NET thuần; nó hoạt động mà không cần Office, rất thích hợp cho các pipeline CI/CD.

**Q: Can I use a DataTable instead of an anonymous type?**  
Absolutely. The processor accepts any `IEnumerable` or `DataTable` as long as the property/column names align with the markers.

**Q: What if my detail rows need a running number?**  
Insert a Smart Marker like `{Detail.RowNumber}`; the engine automatically supplies a sequential index for each expanded row.

**Q: Is it possible to localize the generated Excel file?**  
Yes. Place your static text (headers, titles) in the template in the target language, then let Smart Markers fill the dynamic parts. No extra code required.

## Conclusion

Chúng ta vừa xây dựng một giải pháp **master detail excel** cho phép **populate excel template**, **generate excel from template**, và hoàn toàn **use smart markers** để **how to create master‑detail report** một cách sạch sẽ, dễ bảo trì. Cách tiếp cận này loại bỏ mã tự động hoá Excel lặp đi lặp lại, đảm bảo tính nhất quán về style, và mở rộng từ vài hàng đến hàng chục ngàn.

Tiếp theo, hãy thử thêm biểu đồ tham chiếu các bảng mới tạo, hoặc gắn một truy vấn cơ sở dữ liệu thực vào phần xây dựng `dataModel`. Mẫu này áp dụng cho việc tạo hoá đơn, danh sách tồn kho, hay dashboard phân tích.

Có ý tưởng nào muốn chia sẻ? Để lại bình luận, và chúc bạn lập trình vui vẻ!

## What Should You Learn Next?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, mở rộng các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên đều bao gồm mã mẫu đầy đủ, kèm giải thích từng bước để giúp bạn làm chủ các tính năng API khác và khám phá các cách triển khai thay thế trong dự án của mình.

- [Generate Dynamic Excel Reports Using Aspose.Cells .NET Smart Markers](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Master Dynamic Excel Reporting: Smart Markers & Charts with Aspose.Cells for .NET](/cells/english/net/templates-reporting/dynamic-excel-reports-aspose-cells-net/)
- [Master Aspose.Cells .NET Smart Markers for Data Integration in Excel](/cells/english/net/import-export/mastering-data-integration-aspose-cells-smart-markers/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}