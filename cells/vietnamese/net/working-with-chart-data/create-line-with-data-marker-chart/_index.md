---
"description": "Tìm hiểu cách tạo biểu đồ Line with Data Markers trong Excel bằng Aspose.Cells for .NET. Thực hiện theo hướng dẫn từng bước này để dễ dàng tạo và tùy chỉnh biểu đồ."
"linktitle": "Tạo biểu đồ đường thẳng với dữ liệu đánh dấu"
"second_title": "API xử lý Excel Aspose.Cells .NET"
"title": "Tạo biểu đồ đường thẳng với dữ liệu đánh dấu"
"url": "/vi/net/working-with-chart-data/create-line-with-data-marker-chart/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tạo biểu đồ đường thẳng với dữ liệu đánh dấu

## Giới thiệu

Bạn đã bao giờ tự hỏi làm thế nào để tạo biểu đồ tuyệt đẹp trong Excel theo chương trình chưa? Vâng, hãy thắt dây an toàn, vì hôm nay chúng ta sẽ tìm hiểu sâu hơn về cách tạo Biểu đồ đánh dấu dòng dữ liệu bằng Aspose.Cells cho .NET. Hướng dẫn này sẽ hướng dẫn bạn từng bước, đảm bảo bạn nắm vững cách tạo biểu đồ, ngay cả khi bạn mới bắt đầu sử dụng Aspose.Cells.

## Điều kiện tiên quyết

Trước khi bắt đầu, hãy đảm bảo bạn đã chuẩn bị mọi thứ để có thể thực hiện theo một cách liền mạch.

1. Aspose.Cells cho Thư viện .NET – Bạn sẽ cần cài đặt cái này. Bạn có thể lấy nó [đây](https://releases.aspose.com/cells/net/).
2. .NET Framework – Đảm bảo môi trường phát triển của bạn được thiết lập với phiên bản .NET mới nhất.
3. IDE (Môi trường phát triển tích hợp) – Khuyến khích sử dụng Visual Studio.
4. Giấy phép Aspose.Cells hợp lệ – Nếu bạn không có, bạn có thể yêu cầu [giấy phép tạm thời](https://purchase.aspose.com/temporary-license/) hoặc kiểm tra của họ [dùng thử miễn phí](https://releases.aspose.com/).

Bạn đã sẵn sàng chưa? Chúng ta hãy cùng phân tích nhé!

## Nhập các gói cần thiết

Để bắt đầu, hãy đảm bảo bạn nhập các không gian tên sau vào dự án của mình. Chúng sẽ cung cấp các lớp và phương thức cần thiết để tạo biểu đồ của bạn.

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

Khi bạn đã hiểu rõ, chúng ta có thể bắt đầu viết mã!

## Bước 1: Thiết lập sổ làm việc và bảng tính của bạn

Trước tiên, bạn cần tạo một bảng tính mới và truy cập vào trang tính đầu tiên.

```csharp
//Thư mục đầu ra
static string outputDir = "Your Document Directory";
		
// Khởi tạo một sổ làm việc
Workbook workbook = new Workbook();

// Truy cập bảng tính đầu tiên
Worksheet worksheet = workbook.Worksheets[0];
```

Hãy nghĩ về sổ làm việc như tệp Excel của bạn và trang tính như trang tính cụ thể trong đó. Trong trường hợp này, chúng ta đang làm việc với trang tính đầu tiên.

## Bước 2: Điền dữ liệu vào bảng tính

Bây giờ chúng ta đã có bảng tính, hãy điền một số dữ liệu vào đó. Chúng ta đang tạo các điểm dữ liệu ngẫu nhiên cho hai chuỗi giá trị.

```csharp
// Đặt tiêu đề cột
worksheet.Cells[0, 0].Value = "X";
worksheet.Cells[0, 1].Value = "Y";

// Dữ liệu ngẫu nhiên để tạo biểu đồ
Random R = new Random();

// Tạo dữ liệu ngẫu nhiên và lưu vào ô
for (int i = 1; i < 21; i++)
{
    worksheet.Cells[i, 0].Value = i;
    worksheet.Cells[i, 1].Value = 0.8;
}

for (int i = 21; i < 41; i++)
{
    worksheet.Cells[i, 0].Value = i - 20;
    worksheet.Cells[i, 1].Value = 0.9;
}
```

Ở đây, chúng tôi sử dụng các số ngẫu nhiên để mô phỏng dữ liệu, nhưng trong các ứng dụng thực tế, bạn có thể điền vào đó các giá trị thực từ tập dữ liệu của mình.

## Bước 3: Thêm biểu đồ vào bảng tính

Tiếp theo, chúng ta thêm biểu đồ vào bảng tính và chọn loại – trong trường hợp này là Biểu đồ đường có đánh dấu dữ liệu.

```csharp
// Thêm biểu đồ vào bảng tính
int idx = worksheet.Charts.Add(ChartType.LineWithDataMarkers, 1, 3, 20, 20);

// Truy cập biểu đồ mới tạo
Chart chart = worksheet.Charts[idx];
```

Đoạn mã này thêm biểu đồ đường có đánh dấu dữ liệu vào bảng tính, đặt nó vào một phạm vi cụ thể (1,3 đến 20,20). Khá đơn giản, phải không?

## Bước 4: Tùy chỉnh giao diện của biểu đồ

Sau khi tạo xong biểu đồ, bạn có thể định dạng theo ý thích. Hãy thay đổi nền, tiêu đề và kiểu biểu đồ.

```csharp
// Thiết lập kiểu biểu đồ
chart.Style = 3;

// Đặt giá trị tự động điều chỉnh tỷ lệ thành true
chart.AutoScaling = true;

// Đặt màu nền trước thành màu trắng
chart.PlotArea.Area.ForegroundColor = Color.White;

// Đặt thuộc tính tiêu đề biểu đồ
chart.Title.Text = "Sample Chart";

// Đặt loại biểu đồ
chart.Type = ChartType.LineWithDataMarkers;
```

Ở đây, chúng tôi sẽ mang lại cho biểu đồ giao diện sạch sẽ bằng cách đặt nền trắng, tự động thay đổi tỷ lệ và đặt tiêu đề có ý nghĩa.

## Bước 5: Xác định Chuỗi và Vẽ Điểm Dữ liệu

Bây giờ biểu đồ của chúng ta đã trông ổn, chúng ta cần xác định chuỗi dữ liệu sẽ được vẽ.

```csharp
// Đặt Thuộc tính của tiêu đề trục danh mục
chart.CategoryAxis.Title.Text = "Units";

// Xác định hai chuỗi cho biểu đồ
int s2_idx = chart.NSeries.Add("A2: A21", true);
int s3_idx = chart.NSeries.Add("A22: A41", true);
```

Các chuỗi này tương ứng với phạm vi điểm dữ liệu mà chúng ta đã thu thập trước đó.

## Bước 6: Thêm màu sắc và tùy chỉnh các điểm đánh dấu chuỗi

Hãy làm cho biểu đồ này hấp dẫn hơn bằng cách thêm màu tùy chỉnh vào các điểm đánh dấu dữ liệu.

```csharp
// Tùy chỉnh loạt đầu tiên
chart.NSeries[s2_idx].Marker.Area.ForegroundColor = Color.Yellow;
chart.NSeries[s2_idx].Marker.Border.IsVisible = false;

// Tùy chỉnh loạt thứ hai
chart.NSeries[s3_idx].Marker.Area.ForegroundColor = Color.Green;
chart.NSeries[s3_idx].Marker.Border.IsVisible = false;
```

Bằng cách tùy chỉnh màu sắc, bạn không chỉ làm cho biểu đồ có chức năng mà còn hấp dẫn về mặt thị giác!

## Bước 7: Đặt giá trị X và Y cho từng chuỗi

Cuối cùng, hãy gán giá trị X và Y cho mỗi chuỗi của chúng ta.

```csharp
// Đặt giá trị X và Y của chuỗi đầu tiên
chart.NSeries[s2_idx].XValues = "A2: A21";
chart.NSeries[s2_idx].Values = "B2: B21";

// Đặt giá trị X và Y của chuỗi thứ hai
chart.NSeries[s3_idx].XValues = "A22: A41";
chart.NSeries[s3_idx].Values = "B22: B41";
```

Các giá trị dựa trên dữ liệu chúng tôi đã điền ở bước 2.

## Bước 8: Lưu sổ làm việc

Bây giờ mọi thứ đã sẵn sàng, hãy lưu bảng tính để có thể xem biểu đồ hoạt động.

```csharp
// Lưu sổ làm việc
workbook.Save(outputDir + @"LineWithDataMarkerChart.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```

Và thế là xong! Bạn vừa tạo xong biểu đồ đường có đánh dấu dữ liệu bằng Aspose.Cells cho .NET.

## Phần kết luận

Tạo biểu đồ theo chương trình trong Excel có vẻ khó khăn, nhưng với Aspose.Cells for .NET, việc này dễ như làm theo công thức từng bước. Từ việc thiết lập sổ làm việc đến tùy chỉnh giao diện biểu đồ, thư viện mạnh mẽ này xử lý tất cả. Cho dù bạn đang xây dựng báo cáo, bảng thông tin hay hình ảnh hóa dữ liệu, Aspose.Cells cho phép bạn thực hiện dễ dàng.

## Câu hỏi thường gặp

### Tôi có thể tùy chỉnh biểu đồ thêm nữa không?  
Chắc chắn rồi! Aspose.Cells cung cấp rất nhiều tùy chọn tùy chỉnh, từ phông chữ đến đường lưới và nhiều hơn nữa.

### Tôi có cần giấy phép để sử dụng Aspose.Cells không?  
Có, cần có giấy phép để có đầy đủ chức năng. Bạn có thể nhận được [giấy phép tạm thời](https://purchase.aspose.com/temporary-license/) hoặc bắt đầu với một [dùng thử miễn phí](https://releases.aspose.com/).

### Làm thế nào tôi có thể thêm nhiều chuỗi dữ liệu hơn?  
Chỉ cần thêm chuỗi bổ sung bằng cách sử dụng `NSeries.Add` phương pháp, chỉ định phạm vi ô cho dữ liệu mới.

### Tôi có thể xuất biểu đồ dưới dạng hình ảnh không?  
Có, bạn có thể xuất biểu đồ trực tiếp dưới dạng hình ảnh bằng cách sử dụng `Chart.ToImage` phương pháp.

### Aspose.Cells có hỗ trợ biểu đồ 3D không?  
Có, Aspose.Cells hỗ trợ nhiều loại biểu đồ, bao gồm cả biểu đồ 3D.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}