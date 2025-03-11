---
title: Thêm chữ ký số vào tệp Excel đã ký
linktitle: Thêm chữ ký số vào tệp Excel đã ký
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách thêm chữ ký số vào tệp Excel đã ký bằng Aspose.Cells cho .NET trong hướng dẫn từng bước này. Bảo mật tài liệu của bạn.
weight: 12
url: /vi/net/workbook-operations/add-digital-signature-to-signed-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm chữ ký số vào tệp Excel đã ký

## Giới thiệu
Trong thế giới kỹ thuật số ngày nay, việc đảm bảo tính xác thực và toàn vẹn của tài liệu là rất quan trọng. Chữ ký số đóng vai trò là phương tiện mạnh mẽ để xác minh rằng tài liệu không bị thay đổi và đến từ nguồn hợp pháp. Nếu bạn đang làm việc với các tệp Excel trong .NET và muốn thêm chữ ký số vào tệp đã được ký, bạn đã đến đúng nơi rồi! Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn quy trình thêm chữ ký số mới vào tệp Excel đã ký hiện có bằng Aspose.Cells cho .NET. 
## Điều kiện tiên quyết
Trước khi đi sâu vào chi tiết, hãy đảm bảo rằng bạn có mọi thứ cần thiết để bắt đầu:
1.  Aspose.Cells cho .NET: Trước tiên và quan trọng nhất, bạn cần phải cài đặt Aspose.Cells trong môi trường .NET của mình. Bạn có thể tải xuống từ[trang phát hành](https://releases.aspose.com/cells/net/).
2. .NET Framework: Đảm bảo bạn đã thiết lập .NET Framework trên máy của mình. Hướng dẫn này giả định rằng bạn đã quen thuộc với các khái niệm lập trình .NET cơ bản.
3. Chứng chỉ số: Bạn sẽ cần một chứng chỉ số hợp lệ (ở định dạng .pfx) để tạo chữ ký số. Nếu bạn không có, bạn có thể tạo chứng chỉ tự ký cho mục đích thử nghiệm.
4. Môi trường phát triển: Trình soạn thảo mã hoặc IDE như Visual Studio nơi bạn có thể viết và thực thi mã C#.
5. Tệp Excel mẫu: Bạn phải có tệp Excel hiện có đã được ký kỹ thuật số. Đây sẽ là tệp chúng ta thêm chữ ký khác vào.
Sau khi đã đáp ứng được những điều kiện tiên quyết này, chúng ta hãy bắt tay vào viết mã nhé!
## Nhập gói
Trước khi bắt đầu mã hóa, hãy đảm bảo nhập các không gian tên cần thiết. Sau đây là những gì bạn cần đưa vào đầu tệp C# của mình:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Các không gian tên này sẽ cung cấp cho bạn quyền truy cập vào các lớp và phương thức cần thiết để thao tác với các tệp Excel và xử lý chữ ký số.
Bây giờ, chúng ta hãy chia nhỏ quy trình thành các bước dễ quản lý. Chúng ta sẽ thực hiện từng bước để đảm bảo bạn hiểu cách thêm chữ ký số vào tệp Excel đã ký.
## Bước 1: Xác định thư mục của bạn
Đầu tiên, bạn cần chỉ định vị trí các tệp nguồn của bạn và nơi lưu tệp đầu ra. Điều này rất đơn giản nhưng rất quan trọng:
```csharp
// Thư mục nguồn
string sourceDir = "Your Document Directory"; // Thay thế bằng thư mục thực tế của bạn
// Thư mục đầu ra
string outputDir = "Your Document Directory"; // Thay thế bằng thư mục thực tế của bạn
```
 Thay thế`"Your Document Directory"` với đường dẫn thực tế nơi các tệp của bạn được lưu trữ. Điều này thiết lập bối cảnh cho các hoạt động tệp của bạn.
## Bước 2: Tải Workbook đã ký hiện có
Tiếp theo, bạn sẽ tải sổ làm việc Excel hiện có đã được ký. Đây là nơi phép thuật bắt đầu:
```csharp
// Tải sổ làm việc đã được ký số để thêm chữ ký số mới
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(sourceDir + "sampleDigitallySignedByCells.xlsx");
```
 Dòng này khởi tạo một cái mới`Workbook` đối tượng với tệp đã chỉ định. Đảm bảo tên tệp khớp với tệp Excel đã ký hiện tại của bạn.
## Bước 3: Tạo Bộ sưu tập chữ ký số
Để quản lý chữ ký số của bạn, bạn cần tạo một bộ sưu tập. Điều này cho phép bạn giữ nhiều chữ ký nếu cần:
```csharp
// Tạo bộ sưu tập chữ ký số
Aspose.Cells.DigitalSignatures.DigitalSignatureCollection dsCollection = new Aspose.Cells.DigitalSignatures.DigitalSignatureCollection();
```
Bộ sưu tập này sẽ là nơi bạn thêm chữ ký số mới trước khi áp dụng vào sổ làm việc.
## Bước 4: Tải chứng chỉ của bạn
Bây giờ, đã đến lúc tải chứng chỉ số của bạn. Chứng chỉ này sẽ được sử dụng để tạo chữ ký mới:
```csharp
// Tệp chứng chỉ và mật khẩu của nó
string certFileName = sourceDir + "AsposeDemo.pfx"; // Tệp chứng chỉ của bạn
string password = "aspose"; //Mật khẩu chứng chỉ của bạn
// Tạo chứng chỉ mới
System.Security.Cryptography.X509Certificates.X509Certificate2 certificate = new System.Security.Cryptography.X509Certificates.X509Certificate2(certFileName, password);
```
 Hãy chắc chắn thay thế`AsposeDemo.pfx` với tên tệp chứng chỉ của bạn và cập nhật mật khẩu cho phù hợp. Bước này rất quan trọng vì nếu không có chứng chỉ chính xác, bạn sẽ không thể tạo chữ ký hợp lệ.
## Bước 5: Tạo chữ ký số mới
Sau khi chứng chỉ của bạn được tải, bây giờ bạn có thể tạo chữ ký số mới. Chữ ký này sẽ được thêm vào bộ sưu tập của bạn:
```csharp
// Tạo chữ ký số mới và thêm vào bộ sưu tập chữ ký số
Aspose.Cells.DigitalSignatures.DigitalSignature signature = new Aspose.Cells.DigitalSignatures.DigitalSignature(certificate, "Aspose.Cells added new digital signature in existing digitally signed workbook.", DateTime.Now);
dsCollection.Add(signature);
```
Tại đây, bạn cung cấp một thông báo mô tả chữ ký, có thể hữu ích cho việc lưu giữ hồ sơ. Dấu thời gian đảm bảo rằng chữ ký được liên kết với thời điểm chính xác.
## Bước 6: Thêm Bộ sưu tập chữ ký vào Sổ làm việc
Sau khi tạo chữ ký, đã đến lúc thêm toàn bộ bộ sưu tập vào sổ làm việc:
```csharp
// Thêm bộ sưu tập chữ ký số vào sổ làm việc
workbook.AddDigitalSignature(dsCollection);
```
Bước này sẽ áp dụng chữ ký số mới của bạn vào sổ làm việc, đánh dấu nó bằng tính xác thực được thêm vào.
## Bước 7: Lưu sổ làm việc
Cuối cùng, lưu sổ làm việc với chữ ký số mới được bao gồm. Đây là thời điểm mà mọi công sức của bạn được đền đáp:
```csharp
//Lưu bảng tính và xóa nó.
workbook.Save(outputDir + "outputDigitallySignedByCells.xlsx");
workbook.Dispose();
```
Đảm bảo chỉ định tên cho tệp đầu ra của bạn. Đây sẽ là phiên bản mới của tệp Excel, hoàn chỉnh với chữ ký số bổ sung.
## Bước 8: Xác nhận thành công
Để kết thúc, bạn nên cung cấp phản hồi sau khi hoạt động hoàn tất thành công:
```csharp
Console.WriteLine("AddDigitalSignatureToAnAlreadySignedExcelFile executed successfully.\r\n");
```
Dòng này sẽ in thông báo xác nhận tới bảng điều khiển, cho bạn biết mọi thứ đã diễn ra suôn sẻ.
## Phần kết luận
Và bạn đã có nó! Bạn đã thêm thành công chữ ký số mới vào tệp Excel đã ký bằng Aspose.Cells cho .NET. Quá trình này không chỉ tăng cường tính bảo mật cho tài liệu của bạn mà còn đảm bảo rằng chúng đáng tin cậy và có thể xác minh được. 
Chữ ký số là điều cần thiết trong bối cảnh kỹ thuật số ngày nay, đặc biệt là đối với các doanh nghiệp và chuyên gia cần duy trì tính toàn vẹn của tài liệu. Bằng cách làm theo hướng dẫn này, bạn có thể dễ dàng quản lý chữ ký số trong các tệp Excel của mình, đảm bảo dữ liệu của bạn vẫn an toàn và xác thực.
## Câu hỏi thường gặp
### Chữ ký số là gì?
Chữ ký số là một chương trình toán học để xác minh tính xác thực và toàn vẹn của tin nhắn hoặc tài liệu kỹ thuật số. Nó đảm bảo rằng tài liệu không bị thay đổi và xác nhận danh tính của người ký.
### Tôi có cần chứng chỉ đặc biệt để tạo chữ ký số không?
Có, bạn cần có chứng chỉ số do một cơ quan cấp chứng chỉ (CA) đáng tin cậy cấp để tạo chữ ký số hợp lệ.
### Tôi có thể sử dụng chứng chỉ tự ký để thử nghiệm không?
Hoàn toàn được! Bạn có thể tạo chứng chỉ tự ký cho mục đích phát triển và thử nghiệm, nhưng đối với sản xuất, tốt nhất là sử dụng chứng chỉ từ CA đáng tin cậy.
### Điều gì xảy ra nếu tôi cố gắng thêm chữ ký vào một tài liệu chưa được ký?
Nếu bạn thử thêm chữ ký số vào một tài liệu chưa được ký, thao tác này sẽ không có vấn đề gì, nhưng chữ ký gốc sẽ không có.
### Tôi có thể tìm thêm thông tin về Aspose.Cells ở đâu?
 Bạn có thể kiểm tra[Tài liệu Aspose.Cells](https://reference.aspose.com/cells/net/) để biết hướng dẫn chi tiết và tài liệu tham khảo API.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
