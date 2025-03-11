---
title: Gộp các ô trong phạm vi được đặt tên trong Excel
linktitle: Gộp các ô trong phạm vi được đặt tên trong Excel
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách hợp nhất các ô trong một phạm vi được đặt tên bằng Aspose.Cells cho .NET trong hướng dẫn từng bước này. Khám phá cách định dạng, tạo kiểu và tự động hóa các báo cáo Excel.
weight: 11
url: /vi/net/excel-advanced-named-ranges/merge-cells-in-named-range/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Gộp các ô trong phạm vi được đặt tên trong Excel

## Giới thiệu

Khi làm việc với các tệp Excel theo chương trình, một trong những tác vụ phổ biến mà bạn có thể gặp phải là hợp nhất các ô trong một phạm vi được đặt tên. Cho dù bạn đang tự động tạo báo cáo, xây dựng bảng thông tin hay chỉ đơn giản là quản lý các tập dữ liệu lớn, thì việc hợp nhất các ô là một kỹ thuật thiết yếu. Trong hướng dẫn này, chúng ta sẽ khám phá cách hợp nhất các ô trong một phạm vi được đặt tên bằng Aspose.Cells for .NET—một thư viện mạnh mẽ cho phép các nhà phát triển thao tác các tệp Excel mà không cần cài đặt Microsoft Excel.

## Điều kiện tiên quyết

Trước khi bắt đầu, hãy đảm bảo bạn đã chuẩn bị những thứ sau:

-  Aspose.Cells cho .NET: Bạn có thể tải xuống từ[Trang phát hành Aspose.Cells](https://releases.aspose.com/cells/net/).
- .NET Framework được cài đặt trên máy của bạn.
- Hiểu biết cơ bản về C#: Sự quen thuộc với các khái niệm như lớp, phương thức và đối tượng sẽ giúp ích.

## Nhập gói

Trước khi bắt đầu viết mã, bạn cần nhập các không gian tên cần thiết. Các không gian tên này sẽ cho phép bạn truy cập vào chức năng của thư viện Aspose.Cells.

```csharp
using System;
using System.IO;
using Aspose.Cells;
```

Sau khi đã chuẩn bị xong các điều kiện tiên quyết và gói, chúng ta hãy chuyển sang phần thú vị: viết mã!

Sau đây là hướng dẫn chi tiết về cách bạn có thể hợp nhất các ô trong một phạm vi được đặt tên trong trang tính Excel bằng Aspose.Cells cho .NET.

## Bước 1: Tạo một Workbook mới

Đầu tiên chúng ta cần một sổ làm việc. Sổ làm việc theo thuật ngữ Excel tương đương với một tệp Excel. Hãy tạo một tệp.

```csharp
// Tạo một Workbook mới.
Workbook wb1 = new Workbook();
```

Bằng cách khởi tạo một sổ làm việc mới, giờ đây chúng ta có một tệp Excel trống sẵn sàng để thao tác. Giống như bắt đầu với một trang giấy trắng!

## Bước 2: Truy cập vào Bảng tính đầu tiên

Mỗi sổ làm việc đều chứa các trang tính và trong trường hợp này, chúng ta muốn làm việc với trang tính đầu tiên. Hãy bắt đầu nào!

```csharp
// Lấy bài tập đầu tiên trong sổ làm việc.
Worksheet worksheet1 = wb1.Worksheets[0];
```

Hãy nghĩ về worksheet như các tab riêng lẻ trong một tệp Excel nơi dữ liệu thực tế nằm. Theo mặc định, chúng ta đang truy cập vào tab đầu tiên.

## Bước 3: Tạo một phạm vi ô

Bây giờ chúng ta đã có bảng tính, đã đến lúc tạo một phạm vi. Phạm vi là một khối ô, có thể trải dài trên nhiều hàng và cột.

```csharp
//Tạo một phạm vi.
Range mrange = worksheet1.Cells.CreateRange("D6", "I12");
```

Ở đây, chúng ta đang chọn các ô từ D6 đến I12—một khối bao gồm nhiều hàng và cột. Chúng ta sẽ sớm hợp nhất phạm vi này!

## Bước 4: Đặt tên cho phạm vi

Việc đặt tên cho một phạm vi giúp việc tham chiếu sau này dễ dàng hơn, đặc biệt là khi xử lý các tập dữ liệu lớn.

```csharp
// Đặt tên cho phạm vi.
mrange.Name = "TestRange";
```

Bằng cách đặt tên cho phạm vi này là "TestRange", chúng ta có thể nhanh chóng truy xuất phạm vi này sau đó trong mã mà không cần phải chỉ định lại tọa độ ô.

## Bước 5: Hợp nhất Phạm vi Ô

Bây giờ là lúc thực hiện phép thuật—hợp nhất các ô trong phạm vi mà chúng ta vừa tạo!

```csharp
// Gộp các ô trong phạm vi.
mrange.Merge();
```

Bước này hợp nhất tất cả các ô từ D6 đến I12 thành một ô duy nhất. Hoàn hảo cho những thứ như tiêu đề hoặc tóm tắt!

## Bước 6: Lấy lại phạm vi được đặt tên

Sau khi các ô được hợp nhất, chúng ta có thể muốn áp dụng một số định dạng. Trước tiên, hãy lấy lại phạm vi được đặt tên của chúng ta.

```csharp
// Nhận phạm vi.
Range range1 = wb1.Worksheets.GetRangeByName("TestRange");
```

Việc lấy phạm vi theo tên cho phép chúng ta thực hiện các thao tác tiếp theo, như thêm kiểu hoặc nhập dữ liệu.

## Bước 7: Xác định Kiểu cho các Ô được Hợp nhất

Một ô được hợp nhất có tác dụng gì nếu nó trông không được trau chuốt? Hãy tạo một đối tượng kiểu để căn chỉnh văn bản và áp dụng màu nền.

```csharp
// Xác định đối tượng kiểu.
Style style = wb1.CreateStyle();

// Thiết lập căn chỉnh.
style.HorizontalAlignment = TextAlignmentType.Center;
style.VerticalAlignment = TextAlignmentType.Center;
style.Pattern = BackgroundType.Solid;
style.ForegroundColor = System.Drawing.Color.Aqua;
```

Ở đây, chúng ta căn chỉnh văn bản theo cả chiều ngang và chiều dọc ở giữa, và đặt màu nền là màu xanh lam nhạt (aqua). Thật phong cách, phải không?

## Bước 8: Áp dụng Kiểu cho Phạm vi

Sau khi xác định kiểu, đã đến lúc áp dụng kiểu đó vào phạm vi đã hợp nhất.

```csharp
// Tạo đối tượng StyleFlag.
StyleFlag flag = new StyleFlag();

// Bật thuộc tính kiểu tương đối.
flag.HorizontalAlignment = true;
flag.VerticalAlignment = true;
flag.CellShading = true;

// Áp dụng kiểu cho phạm vi.
range1.ApplyStyle(style, flag);
```

 Các`StyleFlag` cho Aspose.Cells biết thuộc tính kiểu nào cần áp dụng—căn chỉnh, đổ bóng, v.v. Điều này giúp bạn kiểm soát chi tiết cách áp dụng kiểu.

## Bước 9: Nhập dữ liệu vào phạm vi đã hợp nhất

Một phạm vi định dạng không có nội dung là gì? Hãy thêm một số văn bản.

```csharp
// Nhập dữ liệu vào phạm vi.
range1[0, 0].PutValue("Welcome to Aspose APIs.");
```

Điều này đặt văn bản "Welcome to Aspose APIs" vào ô đầu tiên của phạm vi đã hợp nhất của chúng tôi. Khi ô được hợp nhất, văn bản này sẽ trải dài trên tất cả các ô từ D6 đến I12.

## Bước 10: Lưu tệp Excel

Cuối cùng, hãy lưu bảng tính dưới dạng tệp Excel.

```csharp
// Lưu tệp Excel.
wb1.Save(dataDir + "outputMergeCellsInNamedRange.xlsx");
```

Tại đây, sổ làm việc được lưu với tên "outputMergeCellsInNamedRange.xlsx" trong thư mục bạn chỉ định.

## Phần kết luận

Và bạn đã có nó! Bạn đã hợp nhất thành công các ô trong một phạm vi được đặt tên, áp dụng một số định dạng đẹp và thậm chí nhập một số dữ liệu—tất cả đều bằng Aspose.Cells cho .NET. Cho dù bạn đang làm việc để tự động hóa các báo cáo, thao tác các tệp Excel hay chỉ đang học các kỹ thuật mới, hướng dẫn từng bước này sẽ cung cấp cho bạn nền tảng bạn cần.

## Câu hỏi thường gặp

### Tôi có thể hợp nhất nhiều phạm vi không liền kề trong Aspose.Cells không?  
Không, bạn chỉ có thể hợp nhất các ô liền kề trong Aspose.Cells.

### Tôi có thể hoàn tác thao tác hợp nhất theo chương trình không?  
 Sau khi các ô được hợp nhất, bạn có thể hủy hợp nhất chúng bằng cách sử dụng`UnMerge()` phương pháp trong Aspose.Cells.

### Việc hợp nhất các ô có xóa dữ liệu trong đó không?  
Nếu có bất kỳ dữ liệu nào trong các ô trước khi hợp nhất, dữ liệu từ ô đầu tiên của phạm vi sẽ được giữ lại.

### Tôi có thể áp dụng các kiểu khác nhau cho từng ô trong một phạm vi được hợp nhất không?  
Không, một phạm vi được hợp nhất hoạt động như một ô duy nhất, do đó bạn không thể áp dụng các kiểu khác nhau cho từng ô trong đó.

### Làm thế nào để truy cập vào ô đã hợp nhất sau khi hợp nhất?  
Sau khi hợp nhất, bạn vẫn có thể truy cập vào ô đã hợp nhất bằng cách sử dụng tọa độ ở góc trên cùng bên trái của ô đó.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
