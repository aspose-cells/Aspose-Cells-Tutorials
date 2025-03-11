---
title: Thay thế Tag bằng Text trong TextBox trong Excel
linktitle: Thay thế Tag bằng Text trong TextBox trong Excel
second_title: API xử lý Excel Aspose.Cells .NET
description: Dễ dàng thay thế văn bản trong hộp văn bản trong bảng tính Excel của bạn bằng Aspose.Cells cho .NET. Hướng dẫn từng bước để tự động hóa Excel.
weight: 11
url: /vi/net/excel-shape-text-modifications/replace-tag-text-textbox-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thay thế Tag bằng Text trong TextBox trong Excel

## Giới thiệu
Trong bài viết này, chúng ta sẽ đi sâu vào một nhiệm vụ cụ thể: thay thế các thẻ bằng văn bản bên trong hộp văn bản trong một trang tính Excel bằng Aspose.Cells. Chúng tôi sẽ hướng dẫn bạn từng bước trong toàn bộ quy trình, đảm bảo bạn nắm bắt được mọi chi tiết. Đến cuối hướng dẫn này, bạn sẽ không chỉ nâng cao hiểu biết của mình về Aspose.Cells mà còn hợp lý hóa các nhiệm vụ liên quan đến Excel!
## Điều kiện tiên quyết
Trước khi bắt đầu, bạn cần chuẩn bị một số thứ sau:
1. Visual Studio: Đảm bảo bạn đã cài đặt Visual Studio. Đây là IDE linh hoạt giúp việc viết mã bằng C# trở nên dễ dàng.
2.  Thư viện Aspose.Cells: Nếu bạn chưa thực hiện, hãy tải xuống thư viện Aspose.Cells cho .NET từ[trang](https://releases.aspose.com/cells/net/)Bạn cũng có thể dùng thử phiên bản miễn phí để kiểm tra các tính năng của nó.
3. Kiến thức cơ bản về C#: Hiểu biết cơ bản về lập trình C# sẽ giúp bạn dễ dàng thực hiện hướng dẫn này.
Bây giờ bạn đã sẵn sàng, chúng ta hãy chuyển sang phần thú vị nhất—viết mã!
## Nhập gói
Trước tiên, hãy nhập các gói cần thiết. Điều này rất quan trọng vì nếu không có các gói nhập phù hợp, mã của bạn sẽ không nhận ra các lớp và phương thức mà chúng ta sẽ sử dụng.
## Bắt đầu dự án C# của bạn
Mở Visual Studio và tạo một dự án C# mới, tốt nhất là Ứng dụng Console, vì nó sẽ cho phép bạn dễ dàng xem đầu ra.
## Thêm tham chiếu Aspose.Cells
- Nhấp chuột phải vào dự án của bạn trong Solution Explorer.
- Chọn “Thêm” > “Tham chiếu”.
- Duyệt đến vị trí bạn đã tải xuống thư viện Aspose.Cells và đưa nó vào dự án của bạn.
## Nhập các không gian tên cần thiết
 Sau khi bạn đã thêm tham chiếu, hãy thêm nội dung sau`using` chỉ thị ở đầu tệp chính của bạn:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
Điều này cho phép bạn truy cập vào các lớp trong không gian tên Aspose.Cells.
Bây giờ chúng ta đã thiết lập môi trường, hãy cùng đi vào phần hấp dẫn—lập trình! Mục tiêu của chúng ta là tìm các thẻ cụ thể trong hộp văn bản trong tệp Excel và thay thế chúng bằng văn bản được cung cấp.
## Bước 1: Xác định thư mục nguồn và đầu ra
Đầu tiên, chúng ta cần xác định vị trí lưu tệp Excel nguồn và vị trí chúng ta muốn lưu phiên bản đã sửa đổi.
```csharp
// Thư mục nguồn và đầu ra
string sourceDir = "Your Document Directory"; // Thay đổi vào Thư mục của bạn
string outputDir = "Your Document Directory"; // Thay đổi vào Thư mục của bạn
```
## Bước 2: Tải Workbook
Đây là nơi chúng ta sẽ tải sổ làm việc Excel của mình. Nếu tệp không tồn tại, nó sẽ báo lỗi. Vì vậy, hãy đảm bảo đường dẫn tệp của bạn là chính xác!
```csharp
Workbook wb = new Workbook(sourceDir + "sampleReplaceTagWithText.xlsx");
```
 Ở đây, chúng tôi đang tải một tệp Excel hiện có có tên là`sampleReplaceTagWithText.xlsx`.
## Bước 3: Xác định thẻ và văn bản thay thế
Tiếp theo, chúng ta cần xác định các thẻ chúng ta đang tìm kiếm và thẻ chúng ta muốn thay thế.
```csharp
string tag = "TAG_2$TAG_1";
string replace = "1$ys";
```
 Trong ví dụ này, các thẻ được chia bằng cách sử dụng`$`. Bạn có thể thay thế bằng bất kỳ dấu phân cách nào bạn thích.
## Bước 4: Lặp lại các thẻ và thay thế
Chúng ta sẽ tạo một vòng lặp để duyệt qua từng thẻ mà chúng ta muốn thay thế. Đây chính là nơi phép thuật xảy ra!
```csharp
for (int i = 0; i < tag.Split('$').Length; i++)
{
    sheetReplace(wb, "<" + tag.Split('$')[i] + ">", replace.Split('$')[i]);
}
```
## Bước 5: Lưu sổ làm việc
Bây giờ chúng ta đã thực hiện thay thế, đã đến lúc lưu sổ làm việc đã sửa đổi thành định dạng mong muốn. Sau đây là cách chúng tôi chuyển đổi nó thành PDF.
```csharp
PdfSaveOptions opts = new PdfSaveOptions();
wb.Save(outputDir + "outputReplaceTagWithText.pdf", opts);
```
Bạn cũng có thể lưu nó ở nhiều định dạng khác nhau, bao gồm cả XLSX.
## Bước 6: Triển khai Logic thay thế
 Đây là nơi mà trái tim của chức năng của chúng tôi cư trú.`sheetReplace` phương pháp này sẽ xử lý việc thay thế thực tế trong các bảng tính Excel.
```csharp
public static void sheetReplace(Workbook workbook, string sFind, string sReplace)
{
    string finding = sFind;
    foreach (Worksheet sheet in workbook.Worksheets)
    {
        sheet.Replace(finding, sReplace);
        for (int j = 0; j < 3; j++)
        {
            if (sheet.PageSetup.GetHeader(j) != null)
                sheet.PageSetup.SetHeader(j, sheet.PageSetup.GetHeader(j).Replace(finding, sReplace));
                
            if (sheet.PageSetup.GetFooter(j) != null)
                sheet.PageSetup.SetFooter(j, sheet.PageSetup.GetFooter(j).Replace(finding, sReplace));
        }
    }
    foreach (Worksheet sheet in workbook.Worksheets)
    {
        sFind = sFind.Replace("<", "&lt;");
        sFind = sFind.Replace(">", "&gt;");
        foreach (Aspose.Cells.Drawing.TextBox mytextbox in sheet.TextBoxes)
        {
            if (mytextbox.HtmlText != null)
            {
                if (mytextbox.HtmlText.IndexOf(sFind) >= 0)
                {
                    mytextbox.HtmlText = mytextbox.HtmlText.Replace(sFind, sReplace);
                }
            }
        }
    }
}
```
- Đầu tiên, chúng ta lặp qua từng trang tính trong sổ làm việc.
- Chúng tôi thay thế thẻ chính không chỉ trong nội dung ô mà còn trong phần đầu trang và chân trang (nếu có).
- Cuối cùng, chúng tôi kiểm tra từng hộp văn bản trong trang tính và thay thế văn bản bên trong hộp đó dựa trên thẻ mà chúng tôi đang tìm kiếm.
## Phần kết luận
Và voila! Bây giờ bạn đã biết cách thay thế thẻ bằng văn bản trong hộp văn bản trên các tài liệu Excel của mình bằng Aspose.Cells cho .NET. Điều này có thể tiết kiệm thời gian thực sự, đặc biệt là khi xử lý các tác vụ lặp đi lặp lại trong bảng tính.
## Câu hỏi thường gặp
### Tôi có thể thay thế thẻ trên nhiều tệp Excel cùng một lúc không?
Có, bằng cách lặp qua danh sách các tệp, bạn có thể áp dụng cùng một logic cho nhiều tệp Excel.
### Tôi có cần phải trả phí để sử dụng Aspose.Cells không?
 Bạn có thể bắt đầu bằng bản dùng thử miễn phí, nhưng để có đầy đủ chức năng, bạn sẽ cần phải mua giấy phép. Kiểm tra[Các tùy chọn mua của Aspose](https://purchase.aspose.com/buy).
### Tôi có thể thay thế hình ảnh trong hộp văn bản bằng Aspose.Cells không?
Aspose.Cells chủ yếu xử lý văn bản. Tuy nhiên, bạn có thể thao tác hình ảnh riêng nếu cần.
### Tôi có thể lưu tệp Excel đã sửa đổi của mình ở định dạng nào?
Bạn có thể lưu ở nhiều định dạng khác nhau bao gồm XLSX, PDF, CSV, v.v.
### Tôi có thể tìm thấy hỗ trợ cho Aspose.Cells ở đâu?
 Bạn có thể tìm thấy sự hỗ trợ và đặt câu hỏi trên[Diễn đàn Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
