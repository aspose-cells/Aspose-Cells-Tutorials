---
"description": "Học cách thao tác bảng trục Excel bằng Aspose.Cells cho .NET, bao gồm cập nhật dữ liệu, cài đặt tương thích và định dạng ô."
"linktitle": "Chỉ định khả năng tương thích của tệp Excel theo chương trình trong .NET"
"second_title": "API xử lý Excel Aspose.Cells .NET"
"title": "Chỉ định khả năng tương thích của tệp Excel theo chương trình trong .NET"
"url": "/vi/net/creating-and-configuring-pivot-tables/specifying-compatibility/"
"weight": 23
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Chỉ định khả năng tương thích của tệp Excel theo chương trình trong .NET

## Giới thiệu

Trong thế giới dữ liệu ngày nay, việc quản lý và thao tác các tệp Excel theo chương trình đã trở nên cần thiết đối với nhiều nhà phát triển. Nếu bạn đang làm việc với Excel trong .NET, Aspose.Cells là một thư viện mạnh mẽ giúp bạn dễ dàng tạo, đọc, sửa đổi và lưu các tệp Excel. Một tính năng quan trọng của thư viện này cho phép bạn chỉ định khả năng tương thích của các tệp Excel theo chương trình. Trong hướng dẫn này, chúng ta sẽ khám phá cách thao tác các tệp Excel, đặc biệt tập trung vào việc quản lý khả năng tương thích bằng Aspose.Cells cho .NET. Cuối cùng, bạn sẽ hiểu cách thiết lập khả năng tương thích cho các tệp Excel, đặc biệt là đối với các bảng trục, trong khi làm mới và quản lý dữ liệu.

## Điều kiện tiên quyết

Trước khi bắt đầu giai đoạn mã hóa, hãy đảm bảo bạn có những điều sau:

1. Kiến thức cơ bản về C#: Vì chúng ta sẽ viết mã bằng C#, nên việc quen thuộc với ngôn ngữ này sẽ giúp bạn hiểu hướng dẫn tốt hơn.
2. Thư viện Aspose.Cells cho .NET: Bạn có thể tải xuống từ [Trang phát hành Aspose Cells](https://releases.aspose.com/cells/net/). Nếu bạn chưa dùng thử, hãy cân nhắc dùng thử miễn phí để khám phá các tính năng trước.
3. Visual Studio: Một IDE nơi bạn có thể viết và kiểm tra mã C# của mình một cách hiệu quả.
4. Tệp Excel mẫu: Đảm bảo bạn có tệp Excel mẫu, tốt nhất là tệp có chứa bảng trục cho bản demo. Đối với ví dụ của chúng tôi, chúng tôi sẽ sử dụng `sample-pivot-table.xlsx`.

Với những điều kiện tiên quyết này, chúng ta hãy bắt đầu quá trình viết mã.

## Nhập gói

Trước khi bắt đầu viết ứng dụng, bạn cần đưa các không gian tên cần thiết vào mã của mình để sử dụng thư viện Aspose.Cells một cách hiệu quả. Sau đây là cách thực hiện.

### Nhập không gian tên Aspose.Cells

```csharp
using System.IO;
using System;
using Aspose.Cells;
using Aspose.Cells.Pivot;
using System.Drawing;
```

Dòng mã này đảm bảo rằng bạn có thể truy cập tất cả các lớp và phương thức trong thư viện Aspose.Cells.

Bây giờ, chúng ta hãy phân tích chi tiết quy trình để đảm bảo mọi thứ đều rõ ràng và dễ hiểu.

## Bước 1: Thiết lập thư mục của bạn

Trước tiên, hãy thiết lập thư mục chứa các tệp Excel của bạn. Điều quan trọng là phải cung cấp đúng đường dẫn tệp.

```csharp
// Đường dẫn đến thư mục tài liệu.
string dataDir = "Your Document Directory";
```

Ở đây, thay thế `"Your Document Directory"` với đường dẫn thực tế đến các tệp Excel của bạn. Đây là nơi tệp bảng trục mẫu của bạn sẽ nằm.

## Bước 2: Tải tệp Excel nguồn

Tiếp theo, chúng ta cần tải tệp Excel có chứa bảng trục mẫu. 

```csharp
// Tải tệp excel nguồn chứa bảng trục mẫu
Workbook wb = new Workbook(dataDir + "sample-pivot-table.xlsx");
```

Trong bước này, chúng ta tạo một phiên bản của `Workbook` lớp này sẽ tải tệp Excel được chỉ định. 

## Bước 3: Truy cập vào các trang tính

Bây giờ bảng tính đã được tải, bạn phải truy cập vào trang tính chứa dữ liệu bảng tổng hợp.

```csharp
// Truy cập trang tính đầu tiên có chứa dữ liệu bảng trục
Worksheet dataSheet = wb.Worksheets[0];
```

Tại đây, chúng ta truy cập vào trang tính đầu tiên nơi bảng trục được đặt. Bạn cũng có thể lặp qua hoặc chỉ định các trang tính khác dựa trên cấu trúc Excel của bạn.

## Bước 4: Xử lý dữ liệu ô

Tiếp theo, bạn sẽ sửa đổi một số giá trị ô trong bảng tính. 

### Bước 4.1: Sửa đổi ô A3

Chúng ta hãy bắt đầu bằng cách truy cập ô A3 và thiết lập giá trị của ô này.

```csharp
// Truy cập ô A3 và thiết lập dữ liệu của nó
Cells cells = dataSheet.Cells;
Cell cell = cells["A3"];
cell.PutValue("FooBar");
```

Đoạn mã này cập nhật ô A3 với giá trị “FooBar”.

### Bước 4.2: Sửa đổi ô B3 bằng chuỗi dài

Bây giờ, hãy đặt một chuỗi ký tự dài vào ô B3, vượt quá giới hạn ký tự chuẩn của Excel.

```csharp
// Truy cập ô B3, thiết lập dữ liệu của nó
string longStr = "Very long text 1. very long text 2.... [continue your long string]";
cell = cells["B3"];
cell.PutValue(longStr);
```

Mã này rất quan trọng vì nó thiết lập kỳ vọng của bạn về giới hạn dữ liệu, đặc biệt là khi làm việc với các cài đặt tương thích trong Excel.

## Bước 5: Kiểm tra độ dài của ô B3

Việc xác nhận độ dài của chuỗi ký tự mà chúng ta nhập cũng rất quan trọng.

```csharp
// In ra độ dài của chuỗi ô B3
Console.WriteLine("Length of original data string: " + cell.StringValue.Length);
```

Đây chỉ là để xác minh xem điện thoại của bạn đang lưu trữ bao nhiêu ký tự.

## Bước 6: Đặt các giá trị ô khác

Bây giờ chúng ta sẽ truy cập vào nhiều ô hơn và thiết lập một số giá trị.

```csharp
// Truy cập ô C3 và thiết lập dữ liệu của nó
cell = cells["C3"];
cell.PutValue("closed");

// Truy cập ô D3 và thiết lập dữ liệu của nó
cell = cells["D3"];
cell.PutValue("2016/07/21");
```

Mỗi đoạn mã này sẽ cập nhật thêm nhiều ô trong bảng tính.

## Bước 7: Truy cập Bảng Pivot

Tiếp theo, bạn sẽ truy cập vào bảng tính thứ hai, bao gồm dữ liệu bảng tổng hợp.

```csharp
// Truy cập vào bảng tính thứ hai có chứa bảng trục
Worksheet pivotSheet = wb.Worksheets[1];

// Truy cập bảng trục
PivotTable pivotTable = pivotSheet.PivotTables[0];
```

Đoạn mã này cho phép bạn thao tác bảng trục để thiết lập khả năng tương thích.

## Bước 8: Thiết lập khả năng tương thích cho Excel 2003

Điều quan trọng là phải thiết lập xem bảng trục của bạn có tương thích với Excel 2003 hay không. 

```csharp
// Thuộc tính IsExcel2003Compatible cho biết PivotTable có tương thích với Excel2003 hay không trong khi làm mới PivotTable
pivotTable.IsExcel2003Compatible = true;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

Đây là nơi sự chuyển đổi thực sự bắt đầu. Bằng cách thiết lập `IsExcel2003Compatible` ĐẾN `true`bạn giới hạn độ dài ký tự ở mức 255 khi làm mới.

## Bước 9: Kiểm tra độ dài sau khi thiết lập khả năng tương thích

Sau khi thiết lập khả năng tương thích, hãy xem nó ảnh hưởng đến dữ liệu như thế nào.

```csharp
// Kiểm tra giá trị của ô B5 trong bảng tính tổng hợp.
Cell b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to True: " + b5.StringValue.Length);
```

Bạn có thể sẽ thấy kết quả xác nhận hiệu ứng cắt bớt nếu dữ liệu ban đầu vượt quá 255 ký tự.

## Bước 10: Thay đổi cài đặt tương thích

Bây giờ, hãy thay đổi cài đặt tương thích và kiểm tra lại.

```csharp
// Bây giờ hãy đặt thuộc tính IsExcel2003Compatible thành false và làm mới lại
pivotTable.IsExcel2003Compatible = false;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

Điều này cho phép dữ liệu của bạn phản ánh độ dài ban đầu mà không có những hạn chế trước đó.

## Bước 11: Kiểm tra lại độ dài 

Hãy xác minh rằng dữ liệu hiện đang phản ánh chính xác độ dài thực của nó.

```csharp
// Bây giờ nó sẽ in ra độ dài ban đầu của dữ liệu ô. Dữ liệu hiện chưa bị cắt bớt.
b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to False: " + b5.StringValue.Length);
```

Bạn sẽ thấy kết quả xác nhận việc cắt bớt đã được loại bỏ.

## Bước 12: Định dạng các ô

Để nâng cao trải nghiệm trực quan, bạn có thể muốn định dạng các ô. 

```csharp
// Đặt chiều cao hàng và chiều rộng cột của ô B5 và cũng bao quanh văn bản của nó
pivotSheet.Cells.SetRowHeight(b5.Row, 100);
pivotSheet.Cells.SetColumnWidth(b5.Column, 65);
Style st = b5.GetStyle();
st.IsTextWrapped = true;
b5.SetStyle(st);
```

Những dòng mã này giúp dữ liệu dễ đọc hơn bằng cách điều chỉnh kích thước ô và cho phép ngắt dòng văn bản.

## Bước 13: Lưu sổ làm việc

Cuối cùng, hãy lưu bảng tính với những thay đổi bạn đã thực hiện.

```csharp
// Lưu sổ làm việc ở định dạng xlsx
wb.Save(dataDir + "SpecifyCompatibility_out.xlsx", SaveFormat.Xlsx);
```

Việc lựa chọn định dạng tệp phù hợp là rất quan trọng khi lưu tệp Excel. `Xlsx` Định dạng này được sử dụng rộng rãi và tương thích với nhiều phiên bản Excel.

## Phần kết luận

Xin chúc mừng! Bây giờ bạn đã lập trình được các thiết lập tương thích tệp Excel bằng Aspose.Cells cho .NET. Hướng dẫn này phác thảo từng bước, từ thiết lập môi trường của bạn đến thay đổi các thiết lập tương thích cho các bảng trục. Nếu bạn đã từng làm việc với dữ liệu yêu cầu các giới hạn hoặc khả năng tương thích cụ thể, thì đây là một kỹ năng mà bạn sẽ không muốn bỏ qua.

## Câu hỏi thường gặp

### Aspose.Cells là gì?  
Aspose.Cells là thư viện .NET được thiết kế để giúp các nhà phát triển tạo, thao tác và chuyển đổi các tệp Excel một cách liền mạch.

### Tại sao khả năng tương thích của Excel lại quan trọng?  
Khả năng tương thích của Excel rất quan trọng để đảm bảo các tệp có thể được mở và sử dụng trong các phiên bản Excel mong muốn, đặc biệt nếu chúng chứa các tính năng hoặc định dạng không được hỗ trợ trong các phiên bản trước đó.

### Tôi có thể lập trình tạo Bảng Pivot bằng Aspose.Cells không?  
Có, bạn có thể tạo và thao tác Pivot Table theo chương trình bằng Aspose.Cells. Thư viện cung cấp nhiều phương pháp khác nhau để thêm nguồn dữ liệu, trường và tính năng liên quan đến Pivot Table.

### Làm thế nào để kiểm tra độ dài của chuỗi trong ô Excel?  
Bạn có thể sử dụng `StringValue` tài sản của một `Cell` đối tượng để lấy nội dung của ô và sau đó gọi `.Length` tính chất để tìm ra độ dài của chuỗi.

### Tôi có thể tùy chỉnh định dạng ô ngoài chiều cao và chiều rộng của hàng không?  
Chắc chắn rồi! Aspose.Cells cho phép định dạng ô mở rộng. Bạn có thể thay đổi kiểu phông chữ, màu sắc, đường viền, định dạng số và nhiều hơn nữa thông qua `Style` lớp học.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}