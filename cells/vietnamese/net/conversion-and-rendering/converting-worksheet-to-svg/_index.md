---
title: Chuyển đổi Worksheet sang SVG trong .NET
linktitle: Chuyển đổi Worksheet sang SVG trong .NET
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách chuyển đổi bảng tính Excel sang SVG bằng Aspose.Cells cho .NET với hướng dẫn từng bước này. Hoàn hảo cho các nhà phát triển .NET muốn chuyển Excel sang SVG.
weight: 11
url: /vi/net/conversion-and-rendering/converting-worksheet-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chuyển đổi Worksheet sang SVG trong .NET

## Giới thiệu

Nếu bạn đang muốn chuyển đổi một bảng tính Excel sang định dạng SVG, bạn đã đến đúng nơi rồi! Aspose.Cells for .NET là một công cụ mạnh mẽ cho phép các nhà phát triển thao tác các tệp Excel và chuyển đổi chúng thành nhiều định dạng khác nhau, bao gồm SVG (Đồ họa vectơ có thể mở rộng) được hỗ trợ rộng rãi. Hướng dẫn này sẽ hướng dẫn bạn quy trình chuyển đổi một bảng tính sang SVG trong .NET, chia nhỏ từng bước để ngay cả người mới bắt đầu cũng có thể dễ dàng làm theo.

## Điều kiện tiên quyết

Trước khi tìm hiểu mã, hãy đảm bảo rằng bạn có mọi thứ cần thiết:

1.  Aspose.Cells cho .NET: Tải xuống và cài đặt phiên bản mới nhất của Aspose.Cells cho .NET từ[Aspose.Cells cho .NET](https://releases.aspose.com/cells/net/).
2. Môi trường phát triển .NET: Bạn cần cài đặt Visual Studio hoặc bất kỳ IDE .NET nào khác.
3. Kiến thức cơ bản về C#: Cần phải quen thuộc với C#, nhưng đừng lo lắng, chúng tôi sẽ giải thích mọi thứ một cách rõ ràng.
4. Tệp Excel: Chuẩn bị tệp Excel mà bạn muốn chuyển đổi sang định dạng SVG.

## Nhập các gói cần thiết

Trước khi bắt đầu phần mã hóa, hãy đảm bảo bạn đã thêm các không gian tên bắt buộc vào đầu tệp C# của mình.

```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Rendering;
```

Các gói này cần thiết để làm việc với Aspose.Cells và xử lý các tùy chọn kết xuất như xuất SVG.

Sau khi đã nắm được những kiến thức cơ bản, chúng ta hãy cùng tìm hiểu các bước thực tế để chuyển đổi bảng tính Excel sang hình ảnh SVG.

## Bước 1: Thiết lập đường dẫn đến thư mục tài liệu của bạn

Điều đầu tiên chúng ta cần là xác định đường dẫn đến thư mục chứa tệp Excel của bạn. Điều này rất quan trọng vì mã của bạn sẽ tham chiếu đến thư mục để tải và lưu tệp.

```csharp
// Đường dẫn đến thư mục tài liệu
string dataDir = "Your Document Directory";
```

 Hãy chắc chắn thay thế`"Your Document Directory"`với đường dẫn thực tế nơi lưu trữ tệp Excel của bạn.

##  Bước 2: Tải tệp Excel bằng`Workbook`

 Tiếp theo, chúng ta cần tải tệp Excel vào một phiên bản của`Workbook` lớp học. Các`Workbook` lớp biểu thị toàn bộ tệp Excel, bao gồm tất cả các bảng tính trong đó.

```csharp
string filePath = dataDir + "Template.xlsx";
Workbook book = new Workbook(filePath);
```

 Đây,`"Template.xlsx"` là tên của tệp Excel bạn đang làm việc. Đảm bảo rằng tệp này tồn tại trong thư mục đã chỉ định, nếu không, bạn sẽ gặp lỗi.

## Bước 3: Thiết lập tùy chọn hình ảnh hoặc in để chuyển đổi SVG

 Trước khi chúng ta có thể chuyển đổi bảng tính sang định dạng SVG, chúng ta cần chỉ định các tùy chọn hình ảnh.`ImageOrPrintOptions` lớp cho phép bạn kiểm soát cách bảng tính sẽ được chuyển đổi. Cụ thể, chúng ta cần thiết lập`SaveFormat` ĐẾN`SVG` và đảm bảo mỗi bảng tính được chuyển đổi thành một trang duy nhất.

```csharp
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.SaveFormat = SaveFormat.Svg;
imgOptions.OnePagePerSheet = true;
```

 Các`SaveFormat.Svg` tùy chọn đảm bảo định dạng đầu ra sẽ là SVG, trong khi`OnePagePerSheet` đảm bảo rằng mỗi bảng tính sẽ được hiển thị trên một trang duy nhất.

## Bước 4: Lặp lại từng trang tính trong sổ làm việc

Bây giờ chúng ta cần lặp qua tất cả các bảng tính trong tệp Excel. Mỗi bảng tính sẽ được chuyển đổi riêng lẻ.

```csharp
foreach (Worksheet sheet in book.Worksheets)
{
    // Chúng tôi sẽ xử lý từng bảng tính một
}
```

Vòng lặp này đảm bảo rằng bất kể có bao nhiêu trang tính trong sổ làm việc của bạn, thì mỗi trang tính đều sẽ được xử lý.

##  Bước 5: Tạo một`SheetRender` Object for Rendering

 Đối với mỗi bảng tính, chúng tôi sẽ tạo một`SheetRender` đối tượng. Đối tượng này có nhiệm vụ chuyển đổi bảng tính sang định dạng hình ảnh mong muốn, trong trường hợp này là SVG.

```csharp
SheetRender sr = new SheetRender(sheet, imgOptions);
```

 Các`SheetRender` đối tượng có hai đối số: bảng tính bạn đang chuyển đổi và các tùy chọn hình ảnh bạn đã xác định trước đó.

## Bước 6: Chuyển đổi bảng tính sang SVG

 Cuối cùng, trong vòng lặp, chúng ta sẽ chuyển đổi từng trang tính sang định dạng SVG. Chúng ta sử dụng vòng lặp lồng nhau để lặp qua các trang (mặc dù trong trường hợp này, chỉ có một trang cho mỗi trang tính, nhờ vào`OnePagePerSheet` lựa chọn).

```csharp
for (int i = 0; i < sr.PageCount; i++)
{
    // Xuất bảng tính thành định dạng hình ảnh Svg
    sr.ToImage(i, filePath + sheet.Name + i + ".out.svg");
}
```

Mã này sẽ lưu bảng tính dưới dạng tệp SVG trong cùng thư mục với tệp Excel. Mỗi tệp SVG sẽ được đặt tên theo tên bảng tính và số chỉ mục để tránh xung đột tên.

## Phần kết luận

Và thế là xong! Bạn đã chuyển đổi thành công một bảng tính Excel sang định dạng SVG bằng Aspose.Cells for .NET. Quy trình này cho phép bạn giữ nguyên bố cục và thiết kế của bảng tính trong khi vẫn có thể xem được trên bất kỳ trình duyệt hoặc thiết bị nào hỗ trợ SVG, tức là hầu như tất cả chúng. Cho dù bạn đang làm việc với các tệp Excel phức tạp hay chỉ là một bảng đơn giản, phương pháp này đảm bảo rằng dữ liệu của bạn được hiển thị đẹp mắt ở định dạng thân thiện với web.

## Câu hỏi thường gặp

### SVG là gì và tại sao tôi nên sử dụng nó?
SVG (Đồ họa vectơ có thể mở rộng) là định dạng thân thiện với web có thể mở rộng vô hạn mà không làm giảm chất lượng. Định dạng này hoàn hảo cho biểu đồ, sơ đồ và hình ảnh cần hiển thị ở nhiều kích cỡ khác nhau.

### Aspose.Cells có thể xử lý các tệp Excel lớn để chuyển đổi không?
Có, Aspose.Cells có thể xử lý hiệu quả các tệp Excel lớn và chuyển đổi chúng sang SVG mà không gây ra sự cố đáng kể nào về hiệu suất.

### Có giới hạn số lượng trang tính tôi có thể chuyển đổi sang SVG không?
Không, Aspose.Cells không có giới hạn cố hữu nào cho việc chuyển đổi nhiều bảng tính. Hạn chế duy nhất sẽ là bộ nhớ và hiệu suất của hệ thống.

### Tôi có cần giấy phép để sử dụng Aspose.Cells không?
 Có, Aspose.Cells yêu cầu giấy phép để sử dụng sản xuất. Bạn có thể xin giấy phép tạm thời[đây](https://purchase.aspose.com/temporary-license/) hoặc khám phá[dùng thử miễn phí](https://releases.aspose.com/).

### Tôi có thể tùy chỉnh đầu ra SVG không?
 Vâng, bạn có thể điều chỉnh`ImageOrPrintOptions` để tùy chỉnh nhiều khía cạnh khác nhau của đầu ra SVG, chẳng hạn như độ phân giải và tỷ lệ.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
