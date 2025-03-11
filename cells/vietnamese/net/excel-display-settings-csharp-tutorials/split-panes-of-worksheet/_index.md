---
title: Chia ô của bảng tính
linktitle: Chia ô của bảng tính
second_title: Tài liệu tham khảo API Aspose.Cells cho .NET
description: Tìm hiểu cách chia ngăn bảng tính trong Aspose.Cells cho .NET với hướng dẫn từng bước của chúng tôi. Cải thiện khả năng điều hướng tệp Excel với hướng dẫn dễ dàng này.
weight: 130
url: /vi/net/excel-display-settings-csharp-tutorials/split-panes-of-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chia ô của bảng tính

## Giới thiệu

Bạn đã sẵn sàng chia các ngăn của một bảng tính Excel bằng Aspose.Cells cho .NET chưa? Hãy tưởng tượng thế này: bạn có một bảng tính Excel khổng lồ và bạn mệt mỏi vì phải liên tục cuộn lại các tiêu đề chỉ để nhớ mình đang làm việc với cột nào. Nhập "Chia ngăn". Tính năng tiện dụng này cho phép bạn đóng băng một phần bảng tính của mình, giúp bạn dễ dàng điều hướng hơn nhiều. Cho dù bạn đang làm việc với dữ liệu tài chính, quản lý hàng tồn kho hay các tập dữ liệu lớn, việc chia ngăn có thể tăng năng suất của bạn gấp mười lần. 

## Điều kiện tiên quyết

Trước khi chúng ta bắt đầu chia các ngăn như trình hướng dẫn bảng tính, hãy thiết lập đúng. Sau đây là những gì bạn cần:

-  Aspose.Cells cho .NET: Hãy đảm bảo bạn đã tải xuống và cài đặt nó. Nếu bạn chưa tải xuống, hãy tải xuống[đây](https://releases.aspose.com/cells/net/).
- .NET Framework: Hướng dẫn này giả định rằng bạn đang làm việc trong môi trường .NET.
- Sổ làm việc Excel: Chúng tôi sẽ sử dụng một tệp Excel mẫu để hiển thị cách tính năng này hoạt động.
-  Giấy phép tạm thời hoặc đầy đủ: Aspose.Cells yêu cầu giấy phép. Nếu bạn chỉ đang dùng thử, hãy lấy[giấy phép tạm thời miễn phí](https://purchase.aspose.com/temporary-license/) để tránh những hạn chế khi đánh giá.

## Nhập gói

Trước khi đi sâu vào mã, trước tiên hãy nhập các không gian tên cần thiết. Bạn thực sự không thể làm bất cứ điều gì trong Aspose.Cells nếu không bao gồm những điều này.

```csharp
using System.IO;
using Aspose.Cells;
```

Bây giờ chúng ta đã nắm được những điều cần thiết, hãy chuyển sang phần thú vị nhất—chia tách các ô cửa sổ!

## Bước 1: Khởi tạo một Workbook

 Bước đầu tiên trong quá trình này là tạo ra một`Workbook` đối tượng, sẽ đại diện cho tệp Excel mà bạn muốn sửa đổi. Trong trường hợp này, chúng ta sẽ tải tệp từ một thư mục. Đây là canvas của bạn, trang tính Excel mà bạn sẽ thực hiện phép thuật của mình.

Trước khi chúng ta có thể chia khung, chúng ta cần một sổ làm việc để làm việc! Bước này cũng quan trọng như việc mở một cuốn sách trước khi bạn bắt đầu đọc nó.

```csharp
// Đường dẫn đến thư mục tài liệu
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Khởi tạo một bảng tính mới và mở một tệp mẫu
Workbook book = new Workbook(dataDir + "Book1.xls");
```

 Trong đoạn mã trên, hãy thay thế`"YOUR DOCUMENT DIRECTORY"` với đường dẫn thực tế nơi tệp Excel của bạn được lưu trữ.`Workbook`lớp tải tệp Excel vào bộ nhớ.

## Bước 2: Thiết lập ô đang hoạt động

 Sau khi tải sổ làm việc, đã đến lúc thiết lập ô đang hoạt động. Theo thuật ngữ của Excel, ô đang hoạt động là ô hiện đang được chọn hoặc đang được lấy nét. Trong hướng dẫn này, chúng ta sẽ chọn ô`A20` trong bài tập đầu tiên.

Việc thiết lập ô hoạt động rất quan trọng vì việc chia khung bắt đầu từ ô hoạt động này. Giống như việc chọn vị trí cắt đầu tiên trên một chiếc bánh pizza—hãy chọn miếng của bạn!

```csharp
// Đặt ô đang hoạt động
book.Worksheets[0].ActiveCell = "A20";
```

 Đoạn mã này làm cho`A20` ô đang hoạt động. Điều này quan trọng vì quá trình phân tách diễn ra xung quanh điểm này, giống như cách điều hướng trong Excel thường tập trung vào một ô cụ thể.

## Bước 3: Chia nhỏ bảng tính

Bây giờ ô đang hoạt động đã được thiết lập, hãy chuyển sang phần thú vị—chia trang tính! Đây là bước mà phép thuật xảy ra. Bạn sẽ có thể chia trang tính thành nhiều ngăn để xem và điều hướng dễ dàng hơn.

Đây là cốt lõi của toàn bộ hướng dẫn. Bằng cách chia nhỏ bảng tính, bạn tạo các ngăn riêng biệt cho phép bạn cuộn qua các phần khác nhau của bảng tính Excel mà không mất dấu tiêu đề hoặc các khu vực quan trọng khác.

```csharp
// Chia cửa sổ bảng tính
book.Worksheets[0].Split();
```

 Với`Split()` phương pháp, bạn đang yêu cầu Aspose.Cells chia trang tính tại ô đang hoạt động (`A20` trong trường hợp này). Từ thời điểm này, Excel sẽ tạo một phân vùng trong trang tính để phân tách các ngăn để bạn có thể điều hướng độc lập.

## Bước 4: Lưu sổ làm việc

Sau khi tách các ngăn, tất cả những gì còn lại là lưu công việc của bạn. Bước cuối cùng này sẽ đảm bảo rằng các thay đổi của bạn được lưu trong tệp đầu ra đã chỉ định.

Mọi công sức của bạn có ích gì nếu bạn không lưu lại? Việc lưu lại đảm bảo rằng những tấm kính đẹp mắt của bạn được giữ nguyên vẹn để sử dụng trong tương lai.

```csharp
// Lưu tệp Excel
book.Save(dataDir + "output.xls");
```

 Ở đây,`Save()` phương pháp lưu sổ làm việc với các ngăn mới tách của bạn vào tệp Excel đầu ra. Những thay đổi bạn thực hiện giờ đã sẵn sàng để bạn—hoặc bất kỳ ai khác—sử dụng.

## Phần kết luận

Và bạn đã có nó! Bạn vừa học cách chia ngăn trong bảng tính Excel bằng Aspose.Cells cho .NET. Không còn phải cuộn vô tận hoặc mất dấu dữ liệu của bạn nữa. Phương pháp này giúp việc xử lý các tệp Excel lớn bớt quá sức và hiệu quả hơn nhiều. Với khả năng chia ngăn, giờ đây bạn có thể theo dõi các điểm dữ liệu quan trọng trong khi làm việc với các bảng tính phức tạp.

## Câu hỏi thường gặp

### Tôi có thể chia nhiều hơn hai khung không?  
 Có, bạn có thể chia bảng tính thành nhiều ngăn bằng cách chỉ định các ô đang hoạt động khác nhau và gọi`Split()` phương pháp.

### Sự khác biệt giữa tách cửa kính và đóng băng cửa kính là gì?  
Tách ngăn cho phép bạn cuộn trong cả hai ngăn một cách độc lập. Đóng băng ngăn sẽ khóa tiêu đề hoặc các hàng/cột cụ thể để chúng vẫn hiển thị khi cuộn.

### Tôi có thể loại bỏ vết nứt sau khi sử dụng sản phẩm này không?  
Có, bạn có thể xóa phần chia tách bằng cách đóng và mở lại sổ làm việc hoặc thiết lập lại sổ làm việc theo chương trình.

### Tính năng chia khung có hoạt động giống nhau đối với các định dạng tệp Excel khác nhau (XLS, XLSX) không?  
 Vâng,`Split()` Phương pháp này áp dụng được cho cả định dạng XLS và XLSX.

### Tôi có thể sử dụng Aspose.Cells mà không cần giấy phép không?  
 Có, nhưng nó đi kèm với những hạn chế. Để có trải nghiệm đầy đủ, tốt nhất là sử dụng[tạm thời](https://purchase.aspose.com/temporary-license/) hoặc[giấy phép trả phí](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
