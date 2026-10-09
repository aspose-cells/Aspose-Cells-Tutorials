---
date: '2026-04-05'
description: Tìm hiểu cách thêm hộp văn bản vào biểu đồ Excel bằng Aspose.Cells cho
  Java, bao gồm việc tải workbook và lưu tệp Excel bằng Java.
keywords:
- how to add textbox
- save excel file java
- excel chart textbox
- load excel workbook java
- Aspose.Cells Java
title: Cách Thêm Hộp Văn Bản vào Biểu Đồ Excel bằng Aspose.Cells Java
url: /vi/java/charts-graphs/add-textbox-excel-chart-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Cách Thêm TextBox vào Biểu Đồ Excel Sử Dụng Aspose.Cells Java

## Giới thiệu

Việc khám phá thế giới trực quan hoá dữ liệu có thể gặp khó khăn, đặc biệt khi bạn cần thêm các chú thích văn bản tùy chỉnh hoặc nhãn trực tiếp lên biểu đồ trong bảng tính Excel của mình. Hướng dẫn này sẽ chỉ cho bạn cách sử dụng Aspose.Cells cho Java — một thư viện mạnh mẽ giúp đơn giản hoá các nhiệm vụ này — để tích hợp một TextBox vào biểu đồ Excel một cách liền mạch.

**Bạn sẽ học được:**
- Tải và thao tác các tệp Excel bằng Aspose.Cells cho Java.
- Truy cập và chỉnh sửa các đối tượng biểu đồ trong sổ làm việc Excel.
- Thêm và tùy chỉnh điều khiển TextBox trên biểu đồ.
- Lưu các thay đổi của bạn trở lại tệp Excel.

### Câu trả lời nhanh
- **Lớp chính để tải một workbook là gì?** `Workbook` từ `com.aspose.cells`.
- **Phương thức nào thêm TextBox vào biểu đồ?** `addTextBoxInChart` trên bộ sưu tập shape của biểu đồ.
- **Tôi có thể thay đổi màu nền của TextBox không?** Có, thông qua `FillFormat` và `SolidFill`.
- **Làm thế nào để lưu tệp đã chỉnh sửa?** Sử dụng `workbook.save` với một `SaveFormat` đã chọn.
- **Tôi có cần giấy phép cho môi trường sản xuất không?** Có, giấy phép thương mại loại bỏ các giới hạn đánh giá.

## Cách Thêm TextBox vào Biểu Đồ Excel

Bây giờ bạn đã hiểu quy trình tổng thể, hãy đi sâu vào việc triển khai từng bước. Mỗi bước bao gồm một đoạn mã ngắn (giữ nguyên) và một giải thích rõ ràng về những gì nó thực hiện.

## Yêu cầu trước

- **Thư viện yêu cầu:** Aspose.Cells cho Java phiên bản 25.3 trở lên. Hướng dẫn này sử dụng cấu hình Maven và Gradle.
- **Cài đặt môi trường:** JDK (Java Development Kit) tương thích được cài đặt trên máy của bạn.
- **Kiến thức nền:** Hiểu biết cơ bản về lập trình Java và quen thuộc với cấu trúc tệp Excel.

## Cài đặt Aspose.Cells cho Java

Để sử dụng Aspose.Cells trong dự án của bạn, bạn cần thêm nó như một phụ thuộc. Dưới đây là cách thực hiện bằng Maven hoặc Gradle:

### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Nhận giấy phép

Aspose.Cells cung cấp bản dùng thử miễn phí, giấy phép tạm thời cho việc thử nghiệm kéo dài, và các tùy chọn mua thương mại:

- **Bản dùng thử:** Tải xuống thư viện để bắt đầu thử nghiệm các tính năng.
- **Giấy phép tạm thời:** Nhận một giấy phép từ [here](https://purchase.aspose.com/temporary-license/) để đánh giá đầy đủ khả năng mà không có giới hạn.
- **Mua:** Đối với việc sử dụng liên tục trong môi trường sản xuất, mua giấy phép tại [Aspose Purchase](https://purchase.aspose.com/buy).

### Khởi tạo và Cấu hình Cơ bản

Sau khi bạn đã thêm thư viện, khởi tạo nó với giấy phép của bạn nếu có:

```java
License license = new License();
license.setLicense("path/to/your/license/file.lic");
```

## Hướng dẫn triển khai

Chúng ta sẽ đi qua việc thêm TextBox vào biểu đồ Excel bằng Aspose.Cells cho Java. Mỗi tính năng sẽ được chi tiết trong hướng dẫn này.

### Tải tệp Excel

**Tổng quan:** Chúng ta bắt đầu bằng việc tải một tệp Excel hiện có vào ứng dụng, cho phép chúng ta thao tác nội dung của nó một cách lập trình.

#### Bước 1: Nhập các lớp cần thiết
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
```

#### Bước 2: Tải Workbook
```java
String dataDir = "YOUR_DATA_DIRECTORY";
String filePath = dataDir + "/chart.xls";
Workbook workbook = new Workbook(filePath);
Worksheet worksheet = workbook.getWorksheets().get(0);
```
**Giải thích:** Lớp `Workbook` đại diện cho một tệp Excel. Việc tải nó cho phép truy cập vào tất cả các sheet và nội dung của nó.

### Truy cập Đối tượng Biểu đồ

**Tổng quan:** Khi tệp đã được tải, chúng ta cần lấy đối tượng biểu đồ từ một worksheet được chỉ định.

#### Bước 3: Nhập lớp Chart
```java
import com.aspose.cells.Chart;
```

#### Bước 4: Truy cập Biểu đồ Đầu tiên
```java
Chart chart = worksheet.getCharts().get(0);
```
**Giải thích:** Điều này lấy biểu đồ đầu tiên trong worksheet hiện hoạt của bạn để tiếp tục thao tác.

### Thêm Điều khiển TextBox vào Biểu đồ

**Tổng quan:** Bây giờ, hãy thêm một TextBox tùy chỉnh vào biểu đồ của chúng ta để hiển thị bất kỳ chú thích văn bản nào mà chúng ta muốn.

#### Bước 5: Nhập các lớp cần thiết
```java
import com.aspose.cells.TextBox;
import com.aspose.cells.FillFormat;
import com.aspose.cells.LineFormat;
import java.awt.Color;
import com.aspose.cells.MsoLineDashStyle;
```

#### Bước 6: Thêm và Tùy chỉnh TextBox
```java
TextBox txt = chart.getShapes().addTextBoxInChart(100, 100, 850, 2500);
txt.setText("Aspose");
txt.getFont().setItalic(true);
txt.getFont().setSize(20);
txt.getFont().setBold(true);

// Set Fill Format
FillFormat fillformat = txt.getFill();
fillformat.setFillType(FillFormat.FillType.SOLID);
fillformat.getSolidFill().setColor(Color.getSilver());

// Configure Line Format
LineFormat lineformat = txt.getLine();
lineformat.setWeight(2);
lineformat.setDashStyle(MsoLineDashStyle.SOLID);
```
**Giải thích:** Điều này thêm một TextBox tại tọa độ xác định, tùy chỉnh giao diện văn bản, và áp dụng các kiểu nền và đường viền.

### Lưu tệp Excel

**Tổng quan:** Cuối cùng, lưu workbook đã chỉnh sửa trở lại định dạng tệp Excel.

#### Bước 7: Nhập lớp SaveFormat
```java
import com.aspose.cells.SaveFormat;
```

#### Bước 8: Lưu Workbook
```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "/ATBoxControl_out.xls", SaveFormat.EXCEL_97_TO_2003);
```
**Giải thích:** Workbook được lưu vào thư mục đã chỉ định, giữ lại các thay đổi đã thực hiện trong quá trình chạy.

## Ứng dụng Thực tiễn

Dưới đây là một số kịch bản thực tế mà việc thêm TextBox vào biểu đồ Excel có thể hữu ích:

1. **Chú thích cho báo cáo:** Sử dụng text box để cung cấp ngữ cảnh hoặc làm nổi bật các phát hiện quan trọng trực tiếp trên biểu đồ.
2. **Chú giải và nhãn tùy chỉnh:** Tăng cường hiểu biết bằng thông tin bổ sung hoặc giải thích mà các chú giải tiêu chuẩn có thể không bao gồm.
3. **Thương hiệu:** Thêm logo công ty hoặc tuyên bố thương hiệu trong biểu đồ cho các buổi thuyết trình.

## Các lưu ý về hiệu suất

Khi làm việc với các tệp Excel lớn, hãy xem xét các mẹo sau:

- **Tối ưu hoá việc sử dụng tài nguyên:** Giảm thiểu số lần thao tác biểu đồ và tạo đối tượng để giảm dung lượng bộ nhớ.
- **Quản lý bộ nhớ Java:** Đảm bảo xử lý đúng các đối tượng `Workbook` bằng cách đóng chúng sau khi sử dụng để giải phóng tài nguyên kịp thời.
- **Xử lý dữ liệu hiệu quả:** Chỉ tải các phần cần thiết của workbook khi làm việc với bộ dữ liệu lớn.

## Cách Lưu Tệp Excel Java

Bước cuối cùng — lưu workbook — minh họa quy trình **save excel file java**. Bằng cách chỉ định `SaveFormat` mong muốn, bạn có thể xuất ra định dạng `.xls` cổ điển, `.xlsx` hiện đại, hoặc thậm chí CSV, cho phép bạn kiểm soát hoàn toàn loại tệp phù hợp nhất với quy trình downstream của mình.

## Cách Tải Workbook Excel Java

Việc khởi tạo `Workbook` ở trên minh họa mẫu **load excel workbook java**. Aspose.Cells trừu tượng hoá sự phức tạp của việc phân tích cấu trúc Excel nhị phân, cho phép bạn tập trung vào logic nghiệp vụ thay vì các chi tiết I/O của tệp.

## Kết luận

Chúng tôi đã hướng dẫn cách thêm TextBox vào biểu đồ Excel bằng Aspose.Cells cho Java. Hướng dẫn này bao gồm mọi thứ từ việc thiết lập môi trường, tải tệp, truy cập đối tượng biểu đồ, tùy chỉnh text box, đến việc lưu tài liệu cuối cùng.

**Bước tiếp theo:** Thử nghiệm thêm bằng cách áp dụng các kiểu khác nhau hoặc khám phá các loại biểu đồ khác có trong Aspose.Cells. Kiểm tra tài liệu của họ tại [Aspose Reference](https://reference.aspose.com/cells/java/) để biết các chức năng nâng cao hơn.

## Phần Câu hỏi Thường gặp

1. **Tôi có thể thêm nhiều TextBox vào một biểu đồ không?** - Có, bạn có thể lặp lại phương thức `addTextBoxInChart` khi cần với các tọa độ khác nhau.
2. **Điều gì xảy ra nếu tệp Excel của tôi không có biểu đồ?** - Cố gắng truy cập một biểu đồ không tồn tại sẽ gây ra ngoại lệ. Đảm bảo workbook của bạn có ít nhất một biểu đồ trước khi tiếp tục.
3. **Có thể lưu tệp ở định dạng khác .xls không?** - Có, bạn có thể sử dụng các tùy chọn `SaveFormat` khác như `XLSX`, tùy theo nhu cầu.
4. **Làm thế nào để xử lý ngoại lệ trong quá trình thao tác tệp?** - Thực hiện các khối try‑catch quanh các thao tác tải và lưu tệp để quản lý lỗi một cách nhẹ nhàng.
5. **Aspose.Cells cho Java có thể dùng với các ngôn ngữ lập trình khác không?** - Mặc dù hướng dẫn này tập trung vào Java, Aspose.Cells cũng có sẵn cho .NET, C++, và hơn thế nữa. Kiểm tra [documentation](https://reference.aspose.com/cells/java/) của họ để có hướng dẫn cho từng ngôn ngữ.

## Câu hỏi Thường gặp

**Q: Việc thêm TextBox có ảnh hưởng đến hiệu suất biểu đồ không?**  
A: Ảnh hưởng là tối thiểu; tuy nhiên, với các workbook rất lớn, hãy giới hạn số lượng đối tượng shape để giữ mức sử dụng bộ nhớ thấp.

**Q: Tôi có thể định vị TextBox bằng tham chiếu ô thay vì pixel không?**  
A: Có, bạn có thể tính toán tọa độ pixel từ chỉ số ô hoặc sử dụng phương thức `addTextBox` trên worksheet để định vị dựa trên ô.

**Q: Có cách nào để liên kết nội dung TextBox với giá trị ô không?**  
A: Aspose.Cells không cung cấp ràng buộc dữ liệu trực tiếp cho shape, nhưng bạn có thể cập nhật nội dung TextBox một cách lập trình sau khi đọc giá trị của ô.

**Q: Cần những giấy phép nào cho triển khai thương mại?**  
A: Giấy phép Aspose.Cells đã mua sẽ loại bỏ mọi hạn chế đánh giá và là bắt buộc cho việc sử dụng trong môi trường sản xuất.

**Q: Tôi có thể tìm thêm ví dụ về thao tác biểu đồ ở đâu?**  
A: Tài liệu chính thức của Aspose.Cells và kho mẫu chứa nhiều kịch bản, bao gồm series động, các loại biểu đồ và kiểu dáng.

## Tài nguyên

- **Tài liệu:** Khám phá các hướng dẫn toàn diện tại [Aspose Reference](https://reference.aspose.com/cells/java/).
- **Tải xuống:** Truy cập phiên bản thư viện mới nhất từ [Releases](https://releases.aspose.com/cells/java/).
- **Mua và Dùng thử:** Nhận giấy phép hoặc bắt đầu với bản dùng thử miễn phí qua [Purchase Aspose](https://purchase.aspose.com/buy) và [Free Trial](https://releases.aspose.com/cells/java/).
- **Hỗ trợ:** Tham gia cộng đồng tại [Aspose Forum](https://forum.aspose.com/c/cells/9) để được trợ giúp.

Bằng cách theo dõi hướng dẫn này, bạn có thể tích hợp Aspose.Cells một cách hiệu quả vào các dự án Java của mình để nâng cao chức năng biểu đồ Excel với các chú thích văn bản tùy chỉnh. Chúc lập trình vui vẻ!

---

**Last Updated:** 2026-04-05  
**Tested With:** Aspose.Cells Java 25.3  
**Author:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}