---
"description": "Dễ dàng cập nhật các mục công thức Power Query trong Excel bằng Aspose.Cells cho .NET. Hướng dẫn từng bước để hợp lý hóa quy trình thao tác dữ liệu của bạn."
"linktitle": "Cập nhật mục công thức Power Query"
"second_title": "Tài liệu tham khảo API Aspose.Cells cho .NET"
"title": "Cập nhật mục công thức Power Query"
"url": "/vi/net/excel-workbook/update-power-query-formula-item/"
"weight": 160
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Cập nhật mục công thức Power Query

## Giới thiệu

Nếu bạn đã từng làm việc với Excel, bạn sẽ biết nó mạnh mẽ như thế nào—đặc biệt là khi bạn bắt đầu tìm hiểu về Power Query. Đây là công thức bí mật cho phép bạn chuyển đổi, dọn dẹp và phân tích dữ liệu của mình một cách dễ dàng. Một cách khéo léo để thao tác các công thức Power Query của bạn trong Excel là thông qua Aspose.Cells cho .NET. Hôm nay, chúng tôi sẽ hướng dẫn bạn cập nhật các mục công thức Power Query từng bước. Vì vậy, hãy đội mũ lập trình của bạn và bắt đầu thôi!

## Điều kiện tiên quyết

Trước khi bắt đầu viết mã, bạn cần thiết lập một số thứ sau:

1. Visual Studio: Bạn sẽ cần một môi trường phát triển tích hợp (IDE) để viết và chạy mã .NET của mình. Visual Studio là lựa chọn phù hợp.
2. Thư viện Aspose.Cells: Đảm bảo bạn có thư viện Aspose.Cells trong dự án của mình. Bạn có thể tải xuống từ [địa điểm](https://releases.aspose.com/cells/net/).
3. Kiến thức cơ bản về C#: Mặc dù chúng ta sẽ cùng nhau tìm hiểu, nhưng việc có một số hiểu biết cơ bản về C# chắc chắn sẽ hữu ích, đặc biệt là khi điều hướng qua các lớp và phương thức khác nhau.
4. Tệp Excel mẫu: Bạn sẽ cần các tệp Excel được đề cập trong đoạn mã. Đảm bảo bạn có:
   - `SamplePowerQueryFormula.xlsx`
   - `SamplePowerQueryFormulaSource.xlsx`

5. .NET Framework: Đảm bảo dự án của bạn hướng tới phiên bản tương thích của .NET Framework.

Bây giờ chúng ta đã có bộ công cụ sẵn sàng, chúng ta có thể tiến hành phần thú vị: viết mã!

## Nhập gói

Trước tiên, bạn sẽ muốn nhập các không gian tên cần thiết. Sau đây là cách thực hiện:

```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```

Bằng cách thêm các không gian tên này, bạn cho trình biên dịch biết rằng bạn định sử dụng các lớp và phương thức từ thư viện Aspose.Cells. Bước này rất quan trọng vì nó đặt nền tảng cho mã tiếp theo.

Hãy phân tích đoạn mã bạn cung cấp. Hướng dẫn này sẽ hướng dẫn bạn từng phần, đảm bảo bạn hiểu những gì đang diễn ra.

## Bước 1: Thiết lập thư mục làm việc

Trong bước này, chúng ta sẽ xác định vị trí các tệp nguồn và tệp đầu ra. Điều này đảm bảo Aspose biết nơi tìm kiếm các tệp Excel của bạn.

```csharp
// Thư mục làm việc
string SourceDir = "Your Document Directory";
string outputDir = "Your Output Directory";
```

## Bước 2: Tải Workbook

Bây giờ, hãy tải tệp Excel có chứa Power Query.

```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
Các `Workbook` class là điểm vào của bạn vào tệp Excel. Bằng cách truyền đường dẫn đến tệp nguồn, chúng ta đang tạo một thể hiện cho phép chúng ta thao tác nó. Bạn có thể tưởng tượng nó giống như việc mở một cuốn sách—bạn đang chuẩn bị đọc (hoặc chỉnh sửa) nội dung của nó.

## Bước 3: Truy cập vào Data Mashup

Tiếp theo, chúng ta sẽ truy cập các công thức Power Query được lưu trữ trong Data Mashup của sổ làm việc.

```csharp
DataMashup mashupData = workbook.DataMashup;
```
Các `DataMashup` lớp chứa tất cả các công thức Power Query liên quan đến sổ làm việc của bạn. Đây là nơi chúng ta sẽ thực hiện công việc nặng nhọc, giống như khi bạn mở hộp công cụ để sửa chữa.

## Bước 4: Lặp qua các công thức Power Query

Bây giờ đến phần lặp lại các công thức Power Query để tìm công thức cụ thể mà chúng ta muốn cập nhật.

```csharp
foreach (PowerQueryFormula formula in mashupData.PowerQueryFormulas)
{
    foreach (PowerQueryFormulaItem item in formula.PowerQueryFormulaItems)
    {
        if (item.Name == "Source")
        {
            item.Value = "Excel.Workbook(File.Contents(\"" + SourceDir + "SamplePowerQueryFormulaSource.xlsx\"), null, true)";
        }
    }
}
```

- Chúng tôi lặp lại từng cái một `PowerQueryFormula` TRONG `mashupData`.
- Trong vòng lặp đó, chúng ta đi sâu vào từng `PowerQueryFormulaItem`.
- Chúng tôi kiểm tra xem tên mục có khớp với "Nguồn" hay không. Nếu khớp, chúng tôi sẽ cập nhật giá trị của mục đó để liên kết đến tệp nguồn mới.

Điều này giống như việc tìm đúng trang trong sách hướng dẫn rồi thực hiện các cập nhật cần thiết—đây là một quá trình đơn giản và tỉ mỉ.

## Bước 5: Lưu sổ làm việc đã cập nhật

Sau khi thực hiện các cập nhật, đã đến lúc lưu lại những thay đổi.

```csharp
// Lưu bảng tính đầu ra.
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
Các `Save` phương pháp ghi sổ làm việc đã cập nhật vào thư mục đầu ra đã chỉ định. Giống như niêm phong các chỉnh sửa của bạn trong phiên bản mới của hướng dẫn, sẵn sàng để người khác sử dụng!

## Phần kết luận

Xin chúc mừng! Bạn đã cập nhật thành công một mục công thức Power Query bằng Aspose.Cells cho .NET. Với phương pháp này, bạn có thể tự động sửa đổi công thức Power Query trong tệp Excel của mình, giúp bạn tiết kiệm thời gian và công sức.

## Câu hỏi thường gặp

### Aspose.Cells là gì?
Aspose.Cells là một thư viện mạnh mẽ để xử lý các tệp Excel trong các ứng dụng .NET mà không cần cài đặt Microsoft Excel.

### Tôi có cần Microsoft Excel để chạy Aspose.Cells không?
Không, Aspose.Cells cho phép bạn tạo và chỉnh sửa các tệp Excel theo chương trình mà không cần Excel trên máy chủ hoặc máy phát triển của bạn.

### Tôi có thể làm việc với những loại tệp Excel nào khi sử dụng Aspose.Cells?
Bạn có thể làm việc với .xlsx, .xls, .xlsm và một số định dạng Excel khác bằng Aspose.Cells.

### Có phiên bản dùng thử nào cho Aspose.Cells không?
Có, bạn có thể tải xuống phiên bản dùng thử miễn phí từ [Trang phát hành Aspose Cells](https://releases.aspose.com/).

### Tôi có thể nhận được hỗ trợ cho Aspose.Cells như thế nào?
Bạn có thể truy cập hỗ trợ thông qua [Diễn đàn Aspose](https://forum.aspose.com/c/cells/9), nơi bạn có thể đặt câu hỏi và tìm câu trả lời từ cộng đồng và nhóm Aspose.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}