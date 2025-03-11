---
title: Hỗ trợ chữ ký Xades
linktitle: Hỗ trợ chữ ký Xades
second_title: Tài liệu tham khảo API Aspose.Cells cho .NET
description: Tìm hiểu cách thêm chữ ký Xades vào tệp Excel bằng Aspose.Cells cho .NET với hướng dẫn từng bước này. Bảo mật tài liệu của bạn.
weight: 190
url: /vi/net/excel-workbook/xades-signature-support/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hỗ trợ chữ ký Xades

## Giới thiệu

Trong thế giới kỹ thuật số ngày nay, việc bảo mật tài liệu trở nên quan trọng hơn bao giờ hết. Cho dù bạn đang xử lý thông tin kinh doanh nhạy cảm hay dữ liệu cá nhân, việc đảm bảo tính toàn vẹn và tính xác thực của các tệp của bạn là tối quan trọng. Một cách để đạt được điều này là thông qua chữ ký số, và cụ thể là chữ ký Xades. Nếu bạn là nhà phát triển .NET đang tìm cách triển khai hỗ trợ chữ ký Xades trong các ứng dụng của mình, bạn đã đến đúng nơi rồi! Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn quy trình thêm chữ ký Xades vào các tệp Excel bằng Aspose.Cells cho .NET. Vậy, hãy cùng bắt đầu ngay nhé!

## Điều kiện tiên quyết

Trước khi bắt đầu, bạn cần chuẩn bị một số thứ sau:

1.  Aspose.Cells cho .NET: Đảm bảo bạn đã cài đặt thư viện Aspose.Cells. Bạn có thể dễ dàng tải xuống từ[Trang web Aspose](https://releases.aspose.com/cells/net/).
2. Môi trường phát triển: Môi trường phát triển .NET đang hoạt động (như Visual Studio) nơi bạn có thể viết và thực thi mã của mình.
3. Chứng chỉ số: Bạn cần một chứng chỉ số hợp lệ (tệp PFX) có mật khẩu. Chứng chỉ này rất cần thiết để tạo chữ ký số.
4. Kiến thức cơ bản về C#: Sự quen thuộc với lập trình C# sẽ giúp bạn hiểu các ví dụ tốt hơn.

Khi đã đáp ứng được các điều kiện tiên quyết này, bạn đã sẵn sàng bắt đầu triển khai chữ ký Xades vào tệp Excel của mình!

## Nhập gói

Để làm việc với Aspose.Cells cho .NET, bạn cần nhập các không gian tên cần thiết. Sau đây là cách bạn có thể thực hiện:

```csharp
using Aspose.Cells.DigitalSignatures;
using System;
using System.IO;
```

Các không gian tên này cung cấp quyền truy cập vào các lớp và phương thức cần thiết để làm việc với các tệp Excel và quản lý chữ ký số.

Bây giờ chúng ta đã thiết lập mọi thứ, hãy chia nhỏ quy trình thêm chữ ký Xades vào tệp Excel thành các bước rõ ràng, dễ quản lý.

## Bước 1: Thiết lập thư mục nguồn và thư mục đầu ra của bạn

Đầu tiên, chúng ta cần xác định vị trí tệp Excel nguồn của mình và nơi chúng ta muốn lưu tệp đầu ra đã ký. Đây là bước quan trọng vì nó giúp sắp xếp các tệp của bạn một cách hiệu quả.

```csharp
// Thư mục nguồn
string sourceDir = "Your Document Directory";
// Thư mục đầu ra
string outputDir = "Your Output Directory";
```

## Bước 2: Tải Workbook

Tiếp theo, hãy tải sổ làm việc Excel mà chúng ta muốn ký. Đây là nơi bạn sẽ tải tệp Excel hiện có của mình.

```csharp
Workbook workbook = new Workbook(sourceDir + "sourceFile.xlsx");
```

 Ở đây, chúng ta tạo một phiên bản mới của`Workbook` lớp, truyền đường dẫn của tệp Excel nguồn. Đảm bảo rằng tên tệp khớp với tên bạn có trong thư mục nguồn.

## Bước 3: Chuẩn bị chứng chỉ số của bạn

Để tạo chữ ký số, bạn cần tải chứng chỉ số của mình. Điều này bao gồm việc đọc tệp PFX và cung cấp mật khẩu cho tệp đó.

```csharp
string password = "pfxPassword"; // Thay thế bằng mật khẩu PFX của bạn
string pfx = "pfxFile"; // Thay thế bằng đường dẫn đến tệp PFX của bạn
```

 Trong bước này, thay thế`pfxPassword` với mật khẩu thực tế của bạn và`pfxFile` với đường dẫn đến tệp PFX của bạn. Đây là chìa khóa để ký tài liệu của bạn!

## Bước 4: Tạo chữ ký số

 Bây giờ, chúng ta hãy tạo chữ ký số bằng cách sử dụng`DigitalSignature` lớp học. Đây chính là nơi phép thuật xảy ra!

```csharp
DigitalSignature signature = new DigitalSignature(File.ReadAllBytes(pfx), password, "testXAdES", DateTime.Now);
signature.XAdESType = XAdESType.XAdES;
```

 Trong đoạn mã này, chúng tôi đọc tệp PFX vào một mảng byte và tạo một mảng mới`DigitalSignature` đối tượng. Chúng tôi cũng thiết lập`XAdESType` ĐẾN`XAdES`, điều này rất cần thiết cho chữ ký của chúng tôi.

## Bước 5: Thêm chữ ký vào sổ làm việc

Sau khi tạo chữ ký số, bước tiếp theo là thêm chữ ký đó vào sổ làm việc.

```csharp
DigitalSignatureCollection dsCollection = new DigitalSignatureCollection();
dsCollection.Add(signature);
workbook.SetDigitalSignature(dsCollection);
```

 Ở đây, chúng tôi tạo ra một`DigitalSignatureCollection`, thêm chữ ký của chúng tôi vào đó, sau đó đặt bộ sưu tập này vào sổ làm việc. Đây là cách chúng tôi đính kèm chữ ký vào tệp Excel.

## Bước 6: Lưu Workbook đã ký

Cuối cùng, đã đến lúc lưu sổ làm việc đã ký vào thư mục đầu ra. Bước này hoàn tất quy trình.

```csharp
workbook.Save(outputDir + "XAdESSignatureSupport_out.xlsx");
Console.WriteLine("XAdESSignatureSupport executed successfully.");
```

 Trong mã này, chúng ta lưu sổ làm việc với tên mới,`XAdESSignatureSupport_out.xlsx`, trong thư mục đầu ra. Bạn sẽ thấy thông báo thành công trong bảng điều khiển sau khi hoàn tất bước này.

## Phần kết luận

Và bạn đã có nó! Bạn đã thêm thành công chữ ký Xades vào tệp Excel của mình bằng Aspose.Cells cho .NET. Quá trình này không chỉ tăng cường tính bảo mật cho tài liệu của bạn mà còn xây dựng lòng tin với người dùng bằng cách đảm bảo tính xác thực của tệp. 
Chữ ký số là một phần thiết yếu của việc quản lý tài liệu hiện đại và với sức mạnh của Aspose.Cells, bạn có thể dễ dàng triển khai chúng trong các ứng dụng của mình.

## Câu hỏi thường gặp

### Chữ ký Xades là gì?
Xades (Chữ ký điện tử nâng cao XML) là một tiêu chuẩn cho chữ ký số cung cấp các tính năng bổ sung để đảm bảo tính toàn vẹn và xác thực của tài liệu điện tử.

### Tôi có cần chứng chỉ số để tạo chữ ký Xades không?
Có, bạn cần có chứng chỉ số hợp lệ (tệp PFX) để tạo chữ ký Xades.

### Tôi có thể dùng thử Aspose.Cells cho .NET trước khi mua không?
 Chắc chắn rồi! Bạn có thể nhận được bản dùng thử miễn phí từ[Trang web Aspose](https://releases.aspose.com/).

### Aspose.Cells có tương thích với tất cả các phiên bản .NET không?
 Aspose.Cells hỗ trợ nhiều phiên bản khác nhau của .NET framework. Kiểm tra[tài liệu](https://reference.aspose.com/cells/net/) để biết thông tin chi tiết về khả năng tương thích.

### Tôi có thể nhận được hỗ trợ ở đâu nếu gặp vấn đề?
 Bạn có thể ghé thăm[Diễn đàn Aspose](https://forum.aspose.com/c/cells/9) để được cộng đồng hỗ trợ và giúp đỡ.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
