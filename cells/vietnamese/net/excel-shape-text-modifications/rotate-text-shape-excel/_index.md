---
title: Xoay Văn bản có Hình dạng trong Excel
linktitle: Xoay Văn bản có Hình dạng trong Excel
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách xoay văn bản có hình dạng trong Excel bằng Aspose.Cells cho .NET. Làm theo hướng dẫn từng bước này để có bản trình bày Excel hoàn hảo.
weight: 12
url: /vi/net/excel-shape-text-modifications/rotate-text-shape-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Xoay Văn bản có Hình dạng trong Excel

## Giới thiệu
Trong thế giới Excel, biểu diễn trực quan cũng quan trọng như chính dữ liệu. Cho dù bạn đang tạo báo cáo hay thiết kế bảng điều khiển động, cách thông tin được trình bày có thể ảnh hưởng đáng kể đến khả năng đọc và giao diện tổng thể của nó. Vậy, bạn đã bao giờ muốn xoay văn bản để căn chỉnh theo phong cách với các hình dạng chưa? Bạn thật may mắn! Trong hướng dẫn này, chúng ta sẽ tìm hiểu cách xoay văn bản có hình dạng bằng Aspose.Cells cho .NET, đảm bảo rằng bảng tính của bạn không chỉ cung cấp thông tin mà còn gây ấn tượng.
## Điều kiện tiên quyết
Trước khi bắt đầu, hãy đảm bảo rằng bạn đã có mọi thứ cần thiết:
1. Visual Studio: Đảm bảo bạn đã cài đặt Visual Studio trên máy của mình, vì đó là nơi chúng ta sẽ viết code.
2.  Aspose.Cells cho .NET: Bạn sẽ cần thư viện Aspose.Cells. Bạn có thể[tải phiên bản mới nhất tại đây](https://releases.aspose.com/cells/net/) hoặc dùng thử miễn phí với[dùng thử miễn phí](https://releases.aspose.com/).
3. Kiến thức cơ bản về C#: Sự quen thuộc với môi trường C# và .NET sẽ rất hữu ích, mặc dù chúng tôi sẽ hướng dẫn bạn từng bước thực hiện.
4.  Tệp Excel: Một tệp Excel mẫu, chúng ta hãy gọi nó là`sampleRotateTextWithShapeInsideWorksheet.xlsx`, là cần thiết để kiểm tra mã của chúng tôi. Bạn nên đặt tệp này vào một thư mục mà bạn có thể dễ dàng truy cập.
Bạn đã chuẩn bị mọi thứ chưa? Tuyệt vời! Hãy cùng bắt đầu phần thú vị nhé.
## Nhập gói
Để bắt đầu, chúng ta cần nhập các gói cần thiết vào dự án của mình. Sau đây là cách thực hiện:
### Tạo một dự án mới
1. Mở Visual Studio.
2. Chọn "Tạo dự án mới".
3. Chọn "Console App" và chọn C# làm ngôn ngữ lập trình ưa thích của bạn.
### Cài đặt Aspose.Cells
Bây giờ, hãy thêm Aspose.Cells vào dự án của bạn. Bạn có thể thực hiện việc này bằng NuGet Package Manager:
1. Mở "Công cụ" ở menu trên cùng.
2. Chọn "NuGet Package Manager" rồi chọn "Manage NuGet Packages for Solution".
3. Tìm kiếm "Aspose.Cells."
4. Nhấp vào "Cài đặt" để thêm vào dự án của bạn.
### Thêm Sử dụng Chỉ thị
Ở đầu tệp C# chính của bạn, bạn cần thêm lệnh sau:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
Bây giờ chúng ta đã sẵn sàng để bắt đầu viết mã!
Hãy chia nhỏ quy trình thành các bước dễ hiểu. Sau đây là cách xoay văn bản có hình dạng trong tệp Excel:
## Bước 1: Thiết lập đường dẫn thư mục của bạn
Trước tiên, bạn cần thiết lập thư mục nguồn và thư mục đầu ra nơi lưu trữ các tệp Excel của bạn. Sau đây là cách thực hiện:
```csharp
//Thư mục nguồn
string sourceDir = "Your Document Directory"; // Thiết lập thư mục tài liệu của bạn
//Thư mục đầu ra
string outputDir = "Your Document Directory"; // Thiết lập thư mục đầu ra của bạn
```
 Thay thế`"Your Document Directory"` với con đường thực tế nơi bạn`sampleRotateTextWithShapeInsideWorksheet.xlsx` tập tin được đặt ở đâu.
## Bước 2: Tải tệp Excel mẫu
Bây giờ, hãy tải tệp Excel mẫu. Điều này rất quan trọng vì chúng ta muốn thao tác dữ liệu hiện có.
```csharp
//Tải tệp Excel mẫu.
Workbook wb = new Workbook(sourceDir + "sampleRotateTextWithShapeInsideWorksheet.xlsx");
```
## Bước 3: Truy cập vào Bảng tính
Sau khi tệp được tải, chúng ta cần truy cập vào bảng tính cụ thể mà chúng ta muốn sửa đổi. Trong trường hợp của chúng ta, đó là bảng tính đầu tiên.
```csharp
//Truy cập bảng tính đầu tiên.
Worksheet ws = wb.Worksheets[0];
```
## Bước 4: Sửa đổi một ô
Tiếp theo, chúng ta sẽ sửa đổi một ô cụ thể để hiển thị một thông báo. Trong ví dụ của chúng ta, chúng ta sẽ sử dụng ô B4.
```csharp
//Truy cập ô B4 và thêm tin nhắn vào bên trong.
Cell b4 = ws.Cells["B4"];
b4.PutValue("Text is not rotating with shape because RotateTextWithShape is false.");
```
Bước này liên quan đến việc giao tiếp—đảm bảo bất kỳ ai mở bảng tính này đều hiểu chúng ta đang điều chỉnh điều gì.
## Bước 5: Truy cập hình dạng đầu tiên
Để xoay văn bản, chúng ta cần một hình dạng để làm việc. Ở đây, chúng ta sẽ truy cập hình dạng đầu tiên trong bảng tính.
```csharp
//Truy cập hình dạng đầu tiên.
Shape sh = ws.Shapes[0];
```
## Bước 6: Điều chỉnh căn chỉnh văn bản hình dạng
Đây chính là nơi phép thuật xảy ra. Chúng ta sẽ điều chỉnh các thuộc tính căn chỉnh văn bản của hình dạng.
```csharp
//Truy cập căn chỉnh văn bản hình dạng.
Aspose.Cells.Drawing.Texts.ShapeTextAlignment shapeTextAlignment = sh.TextBody.TextAlignment;
//Không xoay văn bản có hình dạng bằng cách đặt RotateTextWithShape thành false.
shapeTextAlignment.RotateTextWithShape = false;
```
 Bằng cách thiết lập`RotateTextWithShape` thành sai, chúng ta đảm bảo rằng văn bản vẫn thẳng đứng và không xoay theo hình dạng, do đó giữ cho mọi thứ gọn gàng và có tổ chức.
## Bước 7: Lưu tệp Excel đầu ra
Cuối cùng, hãy lưu các thay đổi của chúng ta vào một tệp Excel mới. Điều này đảm bảo chúng ta không mất các chỉnh sửa và có đầu ra gọn gàng.
```csharp
//Lưu tệp Excel đầu ra.
wb.Save(outputDir + "outputRotateTextWithShapeInsideWorksheet.xlsx");
```
Và thế là xong! Tệp đầu ra của bạn hiện đã được lưu, bao gồm văn bản trong ô B4 và các điều chỉnh đã thực hiện cho hình dạng.
## Bước 8: Thực thi mã
 Trong của bạn`Main` phương pháp, gói tất cả các đoạn mã trên và chạy dự án của bạn. Xem những thay đổi được phản ánh trong tệp đầu ra của bạn!
```csharp
Console.WriteLine("RotateTextWithShapeInsideWorksheet executed successfully.");
```
## Phần kết luận
Xoay văn bản có hình dạng trong Excel bằng Aspose.Cells cho .NET thoạt đầu có vẻ là một quá trình phức tạp, nhưng khi bạn phân tích nó thì lại khá đơn giản. Bằng cách làm theo các bước đơn giản này, bạn có thể tùy chỉnh bảng tính của mình để trông chuyên nghiệp hơn và hấp dẫn hơn về mặt hình ảnh. Bây giờ, cho dù bạn đang làm điều này cho khách hàng hay các dự án cá nhân của mình, mọi người sẽ đều khen ngợi về chất lượng công việc của bạn!
## Câu hỏi thường gặp
### Tôi có thể sử dụng Aspose.Cells miễn phí không?
 Vâng! Bạn có thể sử dụng[dùng thử miễn phí](https://releases.aspose.com/) để dùng thử thư viện.
### Aspose.Cells hỗ trợ những phiên bản Excel nào?
Aspose.Cells hỗ trợ nhiều định dạng Excel, bao gồm XLS, XLSX, CSV, v.v.
### Có thể xoay văn bản có hình dạng trong các phiên bản Excel cũ hơn không?
Có, chức năng này có thể được áp dụng cho các định dạng cũ hơn được Aspose.Cells hỗ trợ.
### Tôi có thể tìm thêm tài liệu về Aspose.Cells ở đâu?
 Bạn có thể khám phá toàn diện[tài liệu](https://reference.aspose.com/cells/net/) để có thêm thông tin chi tiết.
### Làm thế nào để tôi nhận được hỗ trợ cho Aspose.Cells?
 Bạn có thể yêu cầu hỗ trợ bằng cách truy cập[Diễn đàn Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
