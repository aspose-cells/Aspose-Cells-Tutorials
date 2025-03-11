---
title: Thêm chữ ký số vào tệp Excel đã ký
linktitle: Thêm chữ ký số vào tệp Excel đã ký
second_title: Tài liệu tham khảo API Aspose.Cells cho .NET
description: Tìm hiểu cách thêm chữ ký số vào tệp Excel đã ký bằng Aspose.Cells cho .NET với hướng dẫn từng bước chi tiết này.
weight: 30
url: /vi/net/excel-workbook/add-digital-signature-to-an-already-signed-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm chữ ký số vào tệp Excel đã ký

## Giới thiệu

Trong thế giới số ngày nay, việc bảo mật tài liệu quan trọng hơn bao giờ hết. Chữ ký số cung cấp một cách để đảm bảo tính xác thực và toàn vẹn của các tệp của bạn, đặc biệt là khi xử lý thông tin nhạy cảm. Nếu bạn đang làm việc với các tệp Excel và muốn thêm chữ ký số mới vào sổ làm việc đã được ký, bạn đã đến đúng nơi rồi! Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn quy trình thêm chữ ký số vào tệp Excel đã được ký bằng Aspose.Cells cho .NET. Vậy, hãy cùng bắt đầu nhé!

## Điều kiện tiên quyết

Trước khi đi sâu vào phần cốt lõi của việc viết mã, bạn cần phải chuẩn bị một số điều sau:

1.  Aspose.Cells cho .NET: Đảm bảo bạn đã cài đặt thư viện Aspose.Cells trong dự án .NET của mình. Bạn có thể tải xuống từ[địa điểm](https://releases.aspose.com/cells/net/).
2.  Tệp chứng chỉ: Bạn sẽ cần một tệp chứng chỉ hợp lệ (thường là`.pfx`tệp) có chứa chứng chỉ số của bạn. Đảm bảo bạn biết mật khẩu cho tệp này.
3. Môi trường phát triển: Thiết lập môi trường phát triển của bạn bằng Visual Studio hoặc bất kỳ IDE nào khác hỗ trợ .NET.
4. Kiến thức cơ bản về C#: Sự quen thuộc với lập trình C# sẽ giúp bạn theo dõi dễ dàng hơn.
5. Tệp mẫu: Có tệp Excel mẫu đã được ký kỹ thuật số. Đây sẽ là tệp mà bạn sẽ thêm chữ ký mới.

Bây giờ chúng ta đã có mọi thứ, hãy bắt đầu viết mã nhé!

## Nhập gói

Để bắt đầu, bạn sẽ cần nhập các gói cần thiết vào tệp C# của mình. Sau đây là cách thực hiện:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Các không gian tên này sẽ cho phép bạn làm việc với các tệp Excel và xử lý chữ ký số một cách liền mạch.

## Bước 1: Thiết lập thư mục nguồn và thư mục đầu ra của bạn

Trước khi bạn có thể thao tác với các tệp Excel, bạn cần xác định vị trí các tệp nguồn và nơi bạn muốn lưu tệp đầu ra. Sau đây là cách thực hiện:

```csharp
// Thư mục nguồn
string sourceDir = "Your Document Directory";
// Thư mục đầu ra
string outputDir = "Your Document Directory";
```

Trong bước này, chúng tôi sử dụng phương pháp để lấy đường dẫn cho thư mục nguồn và thư mục đầu ra. Đảm bảo các thư mục này tồn tại và chứa các tệp cần thiết.

## Bước 2: Tải Workbook đã ký

 Tiếp theo, bạn sẽ cần tải sổ làm việc Excel mà bạn muốn sửa đổi. Điều này được thực hiện bằng cách tạo một phiên bản của`Workbook` lớp và truyền đường dẫn đến tệp đã ký.

```csharp
// Tải sổ làm việc đã được ký số
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(sourceDir + "sampleDigitallySignedByCells.xlsx");
```

 Ở đây, chúng tôi đang tải sổ làm việc có tên`sampleDigitallySignedByCells.xlsx`. Hãy chắc chắn rằng tập tin này đã được ký.

## Bước 3: Tạo Bộ sưu tập chữ ký số

Bây giờ, hãy tạo một bộ sưu tập chữ ký số. Bộ sưu tập này sẽ chứa tất cả các chữ ký số mà bạn muốn thêm vào sổ làm việc.

```csharp
// Tạo bộ sưu tập chữ ký số
Aspose.Cells.DigitalSignatures.DigitalSignatureCollection dsCollection = new Aspose.Cells.DigitalSignatures.DigitalSignatureCollection();
```

Bước này rất quan trọng vì nó cho phép bạn quản lý nhiều chữ ký nếu cần.

## Bước 4: Tạo chứng chỉ mới

 Bạn cần tải tệp chứng chỉ của mình để tạo chữ ký số mới. Đây là nơi bạn chỉ định đường dẫn đến`.pfx` tập tin và mật khẩu của nó.

```csharp
// Tệp chứng chỉ và mật khẩu của nó
string certFileName = sourceDir + "AsposeDemo.pfx";
string password = "aspose";

// Tạo chứng chỉ mới
System.Security.Cryptography.X509Certificates.X509Certificate2 certificate = new System.Security.Cryptography.X509Certificates.X509Certificate2(certFileName, password);
```

 Hãy chắc chắn thay thế`AsposeDemo.pfx`và mật khẩu với tên tệp chứng chỉ và mật khẩu thực tế của bạn.

## Bước 5: Tạo chữ ký số

Với chứng chỉ trong tay, giờ đây bạn có thể tạo chữ ký số. Bạn cũng sẽ muốn cung cấp lý do cho chữ ký và ngày giờ hiện tại.

```csharp
// Tạo chữ ký số mới và thêm vào bộ sưu tập chữ ký số
Aspose.Cells.DigitalSignatures.DigitalSignature signature = new Aspose.Cells.DigitalSignatures.DigitalSignature(certificate, "Aspose.Cells added new digital signature in existing digitally signed workbook.", DateTime.Now);
```

Bước này sẽ thêm chữ ký mới vào bộ sưu tập của bạn, sau đó bạn sẽ áp dụng chữ ký này vào sổ làm việc.

## Bước 6: Thêm Bộ sưu tập chữ ký số vào Sổ làm việc

Bây giờ là lúc thêm bộ sưu tập chữ ký số vào sổ làm việc. Đây chính là nơi phép thuật xảy ra!

```csharp
// Thêm bộ sưu tập chữ ký số vào sổ làm việc
workbook.AddDigitalSignature(dsCollection);
```

Bằng cách thực hiện dòng này, về cơ bản bạn đang đính kèm chữ ký số mới vào sổ làm việc đã được ký.

## Bước 7: Lưu và xóa sổ làm việc

Cuối cùng, bạn sẽ muốn lưu bảng tính đã sửa đổi vào thư mục đầu ra và giải phóng mọi tài nguyên đang được sử dụng.

```csharp
//Lưu bảng tính và xóa nó.
workbook.Save(outputDir + "outputDigitallySignedByCells.xlsx");
workbook.Dispose();
```

Bước này đảm bảo rằng những thay đổi của bạn được lưu và sổ làm việc được xử lý đúng cách để giải phóng tài nguyên.

## Bước 8: Xác nhận thực hiện

Để kết thúc, bạn nên xác nhận mã của mình đã được thực thi thành công. Bạn có thể thực hiện việc này bằng một thông báo console đơn giản.

```csharp
Console.WriteLine("AddDigitalSignatureToAnAlreadySignedExcelFile executed successfully.\r\n");
```

Điều này cung cấp phản hồi cho biết hoạt động của bạn đã thành công, điều này luôn tuyệt vời!

## Phần kết luận

Và bạn đã có nó! Bạn đã thêm thành công chữ ký số mới vào tệp Excel đã ký bằng Aspose.Cells cho .NET. Chữ ký số là một cách mạnh mẽ để đảm bảo tính xác thực của tài liệu của bạn và bây giờ bạn biết cách quản lý chúng theo chương trình. Cho dù bạn đang làm việc trên các tài liệu tài chính, hợp đồng hay bất kỳ thông tin nhạy cảm nào, việc triển khai chữ ký số có thể tăng cường bảo mật và sự tin cậy.

## Câu hỏi thường gặp

### Chữ ký số là gì?
Chữ ký số là phương pháp mật mã được sử dụng để xác thực tính xác thực và toàn vẹn của một thông điệp hoặc tài liệu.

### Tôi có thể thêm nhiều chữ ký số vào cùng một tệp Excel không?
Có, bạn có thể tạo bộ sưu tập chữ ký số và thêm nhiều chữ ký vào cùng một bảng tính.

### Aspose.Cells hỗ trợ những định dạng nào cho chữ ký số?
 Aspose.Cells hỗ trợ nhiều định dạng khác nhau, bao gồm`.pfx` để cấp chứng chỉ.

### Tôi có cần phiên bản .NET cụ thể để sử dụng Aspose.Cells không?
 Kiểm tra[Tài liệu Aspose.Cells](https://reference.aspose.com/cells/net/) để tương thích với phiên bản .NET của bạn.

### Làm thế nào tôi có thể nhận được giấy phép tạm thời cho Aspose.Cells?
 Bạn có thể yêu cầu giấy phép tạm thời từ[Trang mua hàng của Aspose](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
