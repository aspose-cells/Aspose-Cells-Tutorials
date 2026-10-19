---
category: general
date: 2026-06-30
description: Tạo định dạng có điều kiện trong một workbook Excel bằng Aspose.Cells.
  Tìm hiểu cách đặt nền cho ô, xếp hạng các ô và xây dựng tệp một cách lập trình.
draft: false
keywords:
- create conditional formatting
- create excel workbook
- set cell background
- how to rank cells
- how to use aspose
language: vi
og_description: Tạo định dạng có điều kiện trong một workbook Excel bằng Aspose.Cells.
  Tham khảo hướng dẫn đầy đủ này để thiết lập nền ô, xếp hạng ô và tự động hoá Excel.
og_title: Tạo Định dạng Có điều kiện trong Excel với Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create conditional formatting in an Excel workbook using Aspose.Cells.
    Learn how to set cell background, rank cells, and build the file programmatically.
  headline: Create Conditional Formatting in Excel with Aspose.Cells – Step‑by‑Step
    Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Tạo Định Dạng Có Điều Kiện trong Excel với Aspose.Cells – Hướng Dẫn Từng Bước
url: /vi/net/excel-conditional-formatting/create-conditional-formatting-in-excel-with-aspose-cells-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Định Dạng Có Điều Kiện trong Excel bằng Aspose.Cells – Hướng Dẫn Từng Bước

Bạn đã bao giờ tự hỏi làm thế nào **tạo định dạng có điều kiện** trong một tệp Excel mà không cần mở giao diện người dùng chưa? Bạn không phải là người duy nhất. Nhiều nhà phát triển cần **tạo workbook excel** một cách nhanh chóng, và việc làm này bằng mã sẽ tiết kiệm hàng giờ công việc thủ công. Trong tutorial này, chúng tôi sẽ chỉ cho bạn cách **tạo định dạng có điều kiện**, định dạng ô, và thậm chí xếp hạng các giá trị cao nhất — tất cả đều nhờ thư viện mạnh mẽ Aspose.Cells cho .NET.

Chúng ta sẽ đi qua một ví dụ thực tế: tạo một bảng điểm, tô sáng các điểm cao bằng màu xanh nhạt, và đặt nền màu vàng cho ba người biểu diễn hàng đầu. Khi kết thúc, bạn sẽ biết **cách đặt nền cho ô**, **cách xếp hạng ô**, và **cách sử dụng Aspose** cho việc tự động hoá Excel phức tạp. Không có phần thừa, chỉ có giải pháp hoàn chỉnh, có thể chạy ngay mà bạn có thể đưa vào bất kỳ dự án C# nào.

## Những Điều Bạn Sẽ Học

- Cách **tạo excel workbook** bằng Aspose.Cells  
- Cách điền một vùng dữ liệu ngẫu nhiên (điểm)  
- Cách **đặt nền cho ô** bằng màu đặc  
- Cách áp dụng quy tắc dựa trên công thức để **xếp hạng ô** và tô sáng ba ô tốt nhất  
- Cách lưu kết quả dưới dạng tệp .xlsx  

Điều kiện tiên quyết: .NET 6+ (hoặc .NET Framework 4.6+), Visual Studio (hoặc bất kỳ IDE C# nào), và tham chiếu tới gói NuGet Aspose.Cells. Nếu bạn chưa từng dùng Aspose trước đây, đừng lo — chúng tôi sẽ hướng dẫn **cách sử dụng Aspose** từ đầu.

---

![Create conditional formatting example](https://example.com/images/create-conditional-formatting.png "Screenshot showing conditional formatting in the generated Excel file")

*Văn bản thay thế ảnh: ví dụ tạo định dạng có điều kiện trong một workbook Excel được tạo bằng Aspose.Cells.*

## Cách Tạo Excel Workbook với Aspose.Cells

Điều đầu tiên cần làm: bạn cần một đối tượng workbook để làm việc. Aspose.Cells biến việc này thành một dòng lệnh.

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Instantiate a new workbook and give the first sheet a friendly name
    Workbook workbook = new Workbook();                 // creates an empty workbook
    Worksheet sheet = workbook.Worksheets[0];           // grab the default worksheet
    sheet.Name = "Scores";                              // rename it to something meaningful
```

Tại sao chúng ta đổi tên sheet? Một tên rõ ràng (như **Scores**) giúp việc tham chiếu sau này dễ dàng hơn, đặc biệt khi bạn chia sẻ tệp với người dùng không chuyên môn.  

Bây giờ workbook đã tồn tại, hãy điền cột A bằng các điểm ngẫu nhiên.

## Cách Điền Dữ Liệu – Tạo Điểm Ngẫu Nhiên

```csharp
    // Step 2: Populate A2:A21 with random values between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)               // 20 rows of data
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }
```

Lưu ý nhanh: `PutValue` tự động phát hiện kiểu dữ liệu, vì vậy bạn không cần ép kiểu sang `int`. Vòng lặp bắt đầu ở `i = 0` nhưng ghi vào hàng `i + 1` vì các hàng trong Excel bắt đầu từ 1 trong khi bộ sưu tập `Cells` bắt đầu từ 0.

## Cách Đặt Nền Cho Ô Khi Điểm Cao

Bây giờ chúng ta sẽ **tạo định dạng có điều kiện** để tô bất kỳ điểm nào ≥ 80 bằng màu xanh nhạt.

```csharp
    // Step 3: Define a conditional formatting range (A2:A21)
    int firstRow = 1, lastRow = 20;                     // zero‑based indices for rows 2‑21
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];

    // Add a rule: cell value >= 80 → light‑green background
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");

    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;
```

Thuộc tính `ForegroundColor` điều khiển màu nền, trong khi `Pattern = BackgroundType.Solid` yêu cầu Excel sử dụng màu đặc thay vì gradient hoặc mẫu. Đây là phần cốt lõi của **cách đặt nền cho ô** dựa trên ngưỡng số.

## Cách Xếp Hạng Ô và Tô Sáng Ba Ô Hàng Đầu

Xếp hạng hơi phức tạp hơn vì chúng ta cần một công thức đánh giá mỗi ô so với toàn bộ vùng. Aspose.Cells cho phép bạn sử dụng cùng cú pháp công thức Excel như khi gõ trực tiếp trong UI.

```csharp
    // Step 4: Add a formula‑based rule to color the top‑3 scores gold
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);

    // The formula uses the RANK function; note the absolute references ($) lock the range
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";

    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;
```

Tại sao lại dùng `A2` trong công thức? Aspose đánh giá công thức tương đối với mỗi ô trong vùng, vì vậy `A2` sẽ tự động chuyển thành `A3`, `A4`, v.v., khi quy tắc được áp dụng từng hàng một. Hàm `RANK` trả về vị trí của một giá trị trong phạm vi đã chỉ định, và phần `<=3` đảm bảo chỉ ba điểm cao nhất nhận nền màu vàng.

## Cách Lưu Workbook

```csharp
    // Step 5: Persist the workbook to disk
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

Thay thế `YOUR_DIRECTORY` bằng đường dẫn tuyệt đối hoặc tương đối mà ứng dụng của bạn có thể ghi vào. Sau khi chạy phương thức, mở tệp trong Excel và bạn sẽ thấy:

- Các ô màu xanh nhạt cho bất kỳ điểm nào ≥ 80  
- Các ô màu vàng cho ba điểm cao nhất, bất kể chúng có ≥ 80 hay không  

Đó là quy trình **tạo định dạng có điều kiện** hoàn chỉnh.

---

## Ví Dụ Đầy Đủ, Có Thể Chạy

Dưới đây là toàn bộ phương thức, sẵn sàng sao chép‑dán vào một ứng dụng console hoặc bất kỳ lớp C# nào:

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Create a new workbook and name the first worksheet
    Workbook workbook = new Workbook();
    Worksheet sheet = workbook.Worksheets[0];
    sheet.Name = "Scores";

    // Step 2: Fill column A (A2:A21) with random scores between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }

    // Step 3: Highlight scores >= 80 with a light‑green background
    int firstRow = 1, lastRow = 20;
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");
    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;

    // Step 4: Color the top‑3 scores with a gold background using a formula rule
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";
    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;

    // Step 5: Save the workbook
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

### Kết Quả Mong Đợi

Khi bạn mở `Scores_ConditionalFormatting.xlsx`:

- Các ô có giá trị **80** trở lên sẽ phát sáng màu xanh nhạt.  
- Ba số lớn nhất (ngay cả khi chúng dưới 80) sẽ hiển thị nền **vàng**.  
- Tất cả các ô còn lại giữ nền trắng mặc định.

Điểm nhấn trực quan này ngay lập tức cho quản lý biết ai là người biểu diễn tốt nhất, mà không cần sắp xếp thủ công.

---

## Câu Hỏi Thường Gặp & Các Trường Hợp Cạnh

**Nếu tôi cần nhiều hơn ba điểm hàng đầu thì sao?**  
Chỉ cần thay đổi phần `<=3` trong công thức thành `<=5` (hoặc bất kỳ số nào bạn muốn). Quy tắc sẽ tự động điều chỉnh.

**Tôi có thể áp dụng nhiều vùng định dạng không?**  
Chắc chắn. Gọi `sheet.ConditionalFormattings.Add` một lần nữa với một vùng khác, sau đó thêm các điều kiện vào đối tượng `ConditionalFormatting` mới đó.

**Còn các phiên bản Excel cũ hơn thì sao?**  
Aspose.Cells lưu mặc định ở định dạng hiện đại `.xlsx`, tương thích với Excel 2007 trở lên. Nếu bạn cần `.xls`, truyền `SaveFormat.Excel97To2003` vào phương thức `Save`.

**Có ảnh hưởng hiệu năng khi làm việc với sheet lớn không?**  
Định dạng có điều kiện được lưu dưới dạng metadata, vì vậy không ảnh hưởng đáng kể tới kích thước tệp. Tuy nhiên, tạo hàng hàng trăm ngàn có thể tăng mức tiêu thụ bộ nhớ — hãy cân nhắc xử lý theo lô.

---

## Bước Tiếp Theo

Bây giờ bạn đã thành thạo **cách tạo định dạng có điều kiện**, bạn có thể muốn khám phá:

- **Cách tạo biểu đồ Excel** bằng mã (một tính năng tuyệt vời khác của Aspose.Cells)  
- **Cách đặt nền cho ô** dựa trên giá trị văn bản (ví dụ: “Pass/Fail”)  
- **Cách sử dụng Aspose.Cells cho việc kiểm tra dữ liệu** và danh sách thả xuống  

Mỗi chủ đề này dựa trên những nguyên tắc cơ bản bạn vừa học, vì vậy bạn sẽ cảm thấy quen thuộc ngay lập tức.

---

## Tổng Kết

Chúng ta vừa đi qua một ví dụ hoàn chỉnh, từ đầu đến cuối, về cách **tạo định dạng có điều kiện** trong một workbook Excel bằng Aspose.Cells. Từ khởi tạo workbook, điền dữ liệu, **đặt nền cho ô**, xếp hạng các người biểu diễn hàng đầu, đến cuối cùng là lưu tệp, mọi bước đều được trình bày kèm **cách xếp hạng ô** và **cách sử dụng Aspose**.  

Hãy chạy thử code, điều chỉnh ngưỡng, và xem bạn có thể tạo ra những báo cáo chuyên nghiệp cho bất kỳ kịch bản kinh doanh nào nhanh chóng như thế nào. Có ý tưởng nào muốn chia sẻ? Để lại bình luận bên dưới — chúc bạn lập trình vui vẻ!

## Bạn Nên Học Gì Tiếp Theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, dựa trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên đều bao gồm mã mẫu đầy đủ và giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Automate Excel Conditional Formatting Using Aspose.Cells for Java&#58; A Complete Guide](/cells/english/java/formatting/automate-conditional-formatting-excel-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java&#58; A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Create an Excel Workbook using Aspose.Cells in Java&#58; A Step‑By‑Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}