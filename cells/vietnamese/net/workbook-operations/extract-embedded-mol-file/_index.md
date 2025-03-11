---
title: Trích xuất tệp Mol nhúng từ sổ làm việc
linktitle: Trích xuất tệp Mol nhúng từ sổ làm việc
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách trích xuất các tệp MOL nhúng từ sổ làm việc Excel bằng Aspose.Cells cho .NET trong hướng dẫn từng bước chi tiết này.
weight: 18
url: /vi/net/workbook-operations/extract-embedded-mol-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất tệp Mol nhúng từ sổ làm việc

## Giới thiệu
Khi nói đến việc quản lý dữ liệu trong sổ làm việc Excel, đôi khi bạn gặp phải nhiều đối tượng nhúng không có định dạng chuẩn. Một trong những định dạng đó là MOL (Tệp cấu trúc phân tử), thường được sử dụng trong hóa học để biểu diễn thông tin phân tử. Nếu bạn đang muốn trích xuất các tệp MOL này từ sổ làm việc Excel bằng Aspose.Cells cho .NET, bạn đã tìm đúng hướng dẫn rồi. Trong bài viết này, chúng tôi sẽ hướng dẫn bạn từng bước thực hiện quy trình, giải thích từng phần trong suốt quá trình.
## Điều kiện tiên quyết
Trước khi bắt đầu viết mã, điều quan trọng là phải đảm bảo rằng bạn có các kỹ năng và công cụ cần thiết. Sau đây là những gì bạn cần:
1. Hiểu biết cơ bản về lập trình .NET: Bạn nên quen thuộc với C# và .NET framework.
2.  Aspose.Cells cho .NET: Đảm bảo bạn có thư viện Aspose.Cells. Bạn có thể[tải xuống ở đây](https://releases.aspose.com/cells/net/).
3. IDE: Bạn có thể sử dụng Visual Studio hoặc bất kỳ IDE nào khác tương thích với .NET.
4. Sổ làm việc Excel có tệp MOL nhúng: Đối với hướng dẫn này, bạn cần một tệp Excel chứa các đối tượng MOL. Bạn có thể tự tạo tệp hoặc sử dụng bất kỳ tệp mẫu nào.
## Nhập gói
Để bắt đầu, bạn sẽ cần nhập các không gian tên cần thiết vào dự án của mình. Điều này rất quan trọng để truy cập các chức năng của Aspose.Cells. Sau đây là cách bạn có thể thực hiện:

```csharp
using Aspose.Cells.Drawing;
using Aspose.Cells.WebExtensions;
using System;
using System.IO;
```

Các không gian tên này sẽ cho phép bạn thao tác với sổ làm việc, truy cập trang tính và làm việc với các tệp nói chung.
Bây giờ chúng ta đã sắp xếp xong các điều kiện tiên quyết, hãy cùng tìm hiểu mã và hiểu từng bước liên quan đến việc trích xuất các tệp MOL nhúng từ bảng tính Excel. 
## Bước 1: Thiết lập thư mục của bạn
Bước đầu tiên là xác định vị trí tài liệu nguồn của bạn và nơi bạn muốn lưu các tệp MOL đã trích xuất. Hãy thiết lập các thư mục đó.
```csharp
string SourceDir = "Your Document Directory"; // Thay thế bằng đường dẫn thư mục của bạn
string outputDir = "Your Document Directory"; // Thay thế bằng đường dẫn đầu ra của bạn
```
 Ở đây, bạn thay thế`"Your Document Directory"`với đường dẫn đến thư mục thực tế của bạn. Điều quan trọng là cả thư mục nguồn và thư mục đầu ra đều có thể truy cập được vào ứng dụng của bạn.
## Bước 2: Tải Workbook
Sau khi thiết lập xong các thư mục, nhiệm vụ tiếp theo là tải sổ làm việc Excel. Hãy thực hiện ngay bây giờ.

```csharp
Workbook workbook = new Workbook(SourceDir + "EmbeddedMolSample.xlsx");
```

 Chúng tôi đang tạo ra một trường hợp của`Workbook` lớp và truyền vào đường dẫn đến tệp Excel có tên của chúng tôi`EmbeddedMolSample.xlsx`. Bước này khởi tạo sổ làm việc, cho phép bạn truy cập vào nội dung của sổ làm việc.
## Bước 3: Lặp lại các trang tính
Bây giờ sổ làm việc của bạn đã được tải, bạn cần lặp qua từng trang tính trong sổ làm việc. Điều này cho phép bạn kiểm tra từng trang tính để tìm các đối tượng nhúng.

```csharp
var index = 1; // Được sử dụng để đặt tên cho các tệp MOL đã trích xuất
foreach (Worksheet sheet in workbook.Worksheets)
{
    OleObjectCollection oles = sheet.OleObjects;
    // Logic trích xuất thêm ở đây
}
```

 Ở đây, bạn đang sử dụng một`foreach` vòng lặp để điều hướng qua các bảng tính. Đối với mỗi bảng tính, bạn truy cập`OleObjects` bộ sưu tập chứa tất cả các đối tượng nhúng.
## Bước 4: Giải nén các tập tin MOL
Bây giờ đến phần quan trọng—trích xuất các tệp MOL từ các đối tượng OLE. Điều này đòi hỏi một vòng lặp khác bên trong vòng lặp bảng tính.

```csharp
foreach (OleObject ole in oles)
{
    string fileName = outputDir + "OleObject" + index + ".mol ";
    FileStream fs = File.Create(fileName);
    fs.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    fs.Close();
    index++;
}
```

 Đối với mỗi đối tượng OLE bạn tìm thấy, bạn đang tạo một tệp mới trong thư mục đầu ra.`ObjectData` tài sản của`OleObject` giữ dữ liệu của đối tượng nhúng, mà bạn ghi vào một tệp mới được tạo bằng cách sử dụng`FileStream`. Tệp được đặt tên tuần tự (`OleObject1.mol`, `OleObject2.mol` , v.v.) dựa trên`index` biến đổi.
## Bước 5: Xác nhận hoàn tất quá trình
Cuối cùng, sau khi đã giải nén tất cả các tệp MOL, bạn nên thông báo cho người dùng biết rằng quá trình đã hoàn tất thành công.

```csharp
Console.WriteLine("ExtractEmbeddedMolFile executed successfully.");
```

Dòng này chỉ in một thông báo đến bảng điều khiển cho bạn biết rằng việc trích xuất đã thành công. Đây là một điểm nhấn tuyệt vời để người dùng phản hồi.
## Phần kết luận
Và bạn đã có nó! Bạn đã trích xuất thành công các tệp MOL nhúng từ sổ làm việc Excel bằng Aspose.Cells cho .NET. Quy trình này tích hợp một vài bước cốt lõi, đảm bảo phương pháp tiếp cận có cấu trúc để xử lý các đối tượng nhúng. Cho dù bạn đang nghiên cứu khoa học, phân tích hóa học hay chỉ đơn giản là xử lý các tập dữ liệu phức tạp, khả năng trích xuất và thao tác các loại tệp này có thể tạo ra sự khác biệt đáng kể trong cách bạn quản lý thông tin của mình. 
## Câu hỏi thường gặp
### Tôi có thể trích xuất các loại tệp khác ngoài MOL từ Excel không?
Có, bạn có thể trích xuất nhiều loại tệp nhúng khác bằng các kỹ thuật tương tự.
### Aspose.Cells có miễn phí sử dụng không?
 Aspose.Cells là một thư viện thương mại, nhưng bạn có thể[dùng thử miễn phí trong thời gian có hạn](https://releases.aspose.com/).
### Phương pháp này có áp dụng được với mọi phiên bản Excel không?
Có, miễn là định dạng tệp đó được Aspose.Cells hỗ trợ.
### Tôi có thể tự động hóa quá trình trích xuất này không?
Chắc chắn rồi! Bạn có thể tự động hóa quy trình này bằng cách đặt mã vào tác vụ đã lên lịch hoặc tập lệnh.
### Tôi có thể tìm thêm tài liệu về Aspose.Cells ở đâu?
 Bạn có thể kiểm tra[Tài liệu Aspose.Cells](https://reference.aspose.com/cells/net/) để biết thêm chi tiết và ví dụ.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
