---
"date": "2025-04-07"
"description": "Tìm hiểu cách tạo và tùy chỉnh biểu đồ hình tròn trong Excel bằng Aspose.Cells for Java. Thực hiện theo hướng dẫn từng bước này để nâng cao kỹ năng trực quan hóa dữ liệu của bạn."
"title": "Tạo biểu đồ hình tròn trong Excel bằng Aspose.Cells cho Java&#58; Hướng dẫn toàn diện"
"url": "/vi/java/charts-graphs/master-pie-chart-creation-excel-aspose-cells-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# Tạo biểu đồ hình tròn trong Excel bằng Aspose.Cells cho Java
## Giới thiệu
Tạo biểu đồ hình tròn hấp dẫn và nhiều thông tin trong Excel có thể chuyển đổi dữ liệu thô thành thông tin chi tiết mạnh mẽ, cho phép bạn đưa ra quyết định kinh doanh sáng suốt một cách nhanh chóng. Bạn đang gặp khó khăn với các tính năng tích hợp của Microsoft Excel hoặc đang tìm kiếm giải pháp có thể mở rộng tích hợp liền mạch với các ứng dụng Java của mình? Aspose.Cells for Java ở đây để giúp bạn.

Hướng dẫn này hướng dẫn bạn cách tạo và tùy chỉnh biểu đồ hình tròn trong tệp Excel bằng Aspose.Cells for Java. Khám phá cách thêm dữ liệu, cấu hình các thành phần biểu đồ và hoàn thiện sổ làm việc của bạn một cách hiệu quả—tất cả đều dễ dàng và chính xác.

**Những gì bạn sẽ học được:**
- Thiết lập và sử dụng Aspose.Cells cho Java
- Tạo một sổ làm việc mới và điền dữ liệu mẫu vào đó
- Thêm và tùy chỉnh biểu đồ hình tròn trong bảng tính Excel
- Thực hành tốt nhất để cấu hình và tối ưu hóa biểu đồ

Chúng ta hãy bắt đầu bằng cách tìm hiểu các điều kiện tiên quyết.
## Điều kiện tiên quyết
Trước khi bắt đầu, hãy đảm bảo bạn có những điều sau:
### Thư viện, Phiên bản và Phụ thuộc bắt buộc
Đảm bảo Aspose.Cells for Java phiên bản 25.3 trở lên được đưa vào dự án của bạn bằng Maven hoặc Gradle.
**Chuyên gia:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```
**Cấp độ:**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```
### Yêu cầu thiết lập môi trường
- Bộ công cụ phát triển Java (JDK) được cài đặt trên hệ thống của bạn.
- Môi trường phát triển tích hợp (IDE) như IntelliJ IDEA, Eclipse hoặc NetBeans.
### Điều kiện tiên quyết về kiến thức
Hiểu biết cơ bản về lập trình Java và quen thuộc với cấu trúc tệp Excel sẽ rất có lợi.
## Thiết lập Aspose.Cells cho Java
Aspose.Cells là một thư viện mạnh mẽ cho phép các nhà phát triển tạo, sửa đổi và hiển thị bảng tính Excel trong các ứng dụng Java. Sau đây là cách bạn có thể thiết lập:
1. **Cài đặt**: Thêm sự phụ thuộc Maven hoặc Gradle như được hiển thị ở trên.
2. **Mua lại giấy phép**:
   - Nhận giấy phép dùng thử miễn phí để thử nghiệm ban đầu từ [Dùng thử miễn phí Aspose](https://releases.aspose.com/cells/java/).
   - Nộp đơn xin cấp giấy phép tạm thời để kiểm tra đầy đủ các tính năng mà không có giới hạn thông qua [Giấy phép tạm thời](https://purchase.aspose.com/temporary-license/).
3. **Khởi tạo cơ bản**: Bắt đầu bằng cách tạo một phiên bản của `Workbook` lớp đại diện cho tệp Excel của bạn.
```java
import com.aspose.cells.Workbook;
// Tạo và khởi tạo một sổ làm việc mới
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook();
```
## Hướng dẫn thực hiện
Bây giờ, chúng ta hãy triển khai từng tính năng theo từng bước để tạo một bảng tính Excel có biểu đồ hình tròn.
### 1. Tạo và khởi tạo sổ làm việc
**Tổng quan**: Chúng tôi bắt đầu bằng cách khởi tạo `Workbook` đối tượng và truy cập vào bảng tính đầu tiên của đối tượng, tại đó chúng ta sẽ thêm dữ liệu và biểu đồ.
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorksheetCollection;

String dataDir = "YOUR_DATA_DIRECTORY";
// Tạo một phiên bản sổ làm việc mới
Workbook workbook = new Workbook();
// Truy cập trang tính đầu tiên trong sổ làm việc
WorksheetCollection worksheets = workbook.getWorksheets();
Worksheet sheet = worksheets.get(0);
```
### 2. Thêm dữ liệu mẫu vào ô
**Tổng quan**: Điền dữ liệu mẫu vào bảng tính của bạn để biểu diễn trong biểu đồ hình tròn.
```java
import com.aspose.cells.Cells;
import com.aspose.cells.Cell;

Cells cells = sheet.getCells();
// Thêm tên quốc gia vào cột A
Cell cell = cells.get("A1");
cell.setValue("Italy");
cell = cells.get("A2");
cell.setValue("Germany");
// Tiếp tục cho các quốc gia khác...
// Thêm dữ liệu bán hàng tương ứng vào cột B
cell = cells.get("B1");
cell.setValue(10000);
cell = cells.get("B2");
cell.setValue(20000);
// Tiếp tục với phần dữ liệu còn lại...
```
### 3. Thêm biểu đồ hình tròn vào bảng tính
**Tổng quan**Chèn biểu đồ hình tròn vào bảng tính bằng cách sử dụng các phạm vi dữ liệu được xác định trước.
```java
import com.aspose.cells.ChartCollection;
import com.aspose.cells.ChartType;

ChartCollection charts = sheet.getCharts();
// Thêm biểu đồ hình tròn ở vị trí và kích thước đã chỉ định
int chartIndex = charts.add(ChartType.PIE, 15, 4, 40, 15);
Chart chart = charts.get(chartIndex);
```
### 4. Cấu hình Chuỗi Biểu đồ
**Tổng quan**: Xác định phạm vi dữ liệu cho dữ liệu doanh số và danh mục (tên quốc gia) để đảm bảo biểu đồ hình tròn thể hiện chính xác tập dữ liệu của bạn.
```java
import com.aspose.cells.SeriesCollection;

SeriesCollection serieses = chart.getNSeries();
// Đặt dữ liệu bán hàng làm nguồn dữ liệu của biểu đồ
serieses.add("B1:B8", true);
// Chỉ định dữ liệu danh mục (tên quốc gia)
serieses.setCategoryData("A1:A8");
// Cho phép nhiều màu sắc khác nhau cho mỗi lát bánh
serieses.setColorVaried(true);

// Hiển thị bảng dữ liệu trên biểu đồ để rõ ràng hơn
chart.setShowDataTable(true);
```
### 5. Thiết lập tiêu đề và kiểu biểu đồ
**Tổng quan**: Tùy chỉnh tiêu đề biểu đồ để tăng khả năng đọc và trình bày.
```java
import com.aspose.cells.Color;

// Đặt tiêu đề biểu đồ với các tùy chọn kiểu dáng
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```
### 6. Cấu hình nhãn dữ liệu cho chuỗi biểu đồ
**Tổng quan**: Thêm nhãn dữ liệu vào từng phần biểu đồ hình tròn, cung cấp sự phân tích giá trị rõ ràng.
```java
import com.aspose.cells.DataLabels;
import com.aspose.cells.LabelPositionType;

for (int i = 0; i < serieses.getCount(); i++) {
    DataLabels datalabels = serieses.get(i).getDataLabels();
    // Vị trí nhãn bên trong đáy của mỗi lát bánh
    datalabels.setPosition(LabelPositionType.INSIDE_BASE);
    // Cấu hình tùy chọn hiển thị nhãn
    datalabels.setShowCategoryName(true);
    datalabels.setShowValue(true);
    datalabels.setShowPercentage(false);
    datalabels.setShowLegendKey(true);
}
```
### 7. Lưu sổ làm việc
**Tổng quan**Hoàn thiện tệp Excel của bạn với tất cả dữ liệu và biểu đồ được lưu vào đĩa.
```java
import com.aspose.cells.SaveFormat;

String outDir = "YOUR_OUTPUT_DIRECTORY";
// Lưu sổ làm việc vào tệp Excel
workbook.save(outDir + "/HTCPChart_out.xls", SaveFormat.EXCEL_97_TO_2003);
```
## Ứng dụng thực tế
- **Phân tích kinh doanh**:Sử dụng biểu đồ hình tròn trong báo cáo bán hàng để trực quan hóa thị phần hoặc phân bổ doanh thu trên khắp các khu vực.
- **Công cụ giáo dục**: Tạo các mô-đun học tập tương tác hiển thị phân phối dữ liệu thống kê.
- **Quản lý dự án**: Thể hiện trực quan việc phân bổ nguồn lực và sử dụng ngân sách cho các bên liên quan.
## Cân nhắc về hiệu suất
Để tối ưu hóa hiệu suất:
- Giảm thiểu việc sử dụng bộ nhớ bằng cách quản lý hiệu quả kích thước sổ làm việc.
- Sử dụng các tính năng của Aspose.Cells như truyền phát các tệp lớn nếu xử lý các tập dữ liệu mở rộng.
- Thực hiện theo các biện pháp quản lý bộ nhớ tốt nhất của Java, đảm bảo giải phóng tài nguyên phù hợp sau khi sử dụng.
## Phần kết luận
Bằng cách làm theo hướng dẫn này, bạn đã học cách tạo, cấu hình và tùy chỉnh biểu đồ hình tròn trong Excel bằng Aspose.Cells for Java. Thư viện mạnh mẽ này cho phép các nhà phát triển tích hợp các chức năng bảng tính nâng cao trong các ứng dụng Java của họ một cách liền mạch.
Để khám phá sâu hơn, hãy cân nhắc tìm hiểu các loại biểu đồ khác hoặc mở rộng khả năng thao tác dữ liệu của bạn bằng các tính năng bổ sung do Aspose.Cells cung cấp.
## Phần Câu hỏi thường gặp
1. **Tôi có thể sử dụng Aspose.Cells miễn phí không?**
   - Có, có bản dùng thử miễn phí. Để có quyền truy cập đầy đủ tính năng mà không bị giới hạn, bạn có thể đăng ký giấy phép tạm thời.
2. **Có thể tạo các loại biểu đồ khác bằng Aspose.Cells không?**
   - Chắc chắn rồi! Bạn có thể tạo biểu đồ thanh, biểu đồ đường và nhiều hơn nữa bằng cách điều chỉnh `ChartType`.
3. **Làm thế nào để xử lý các tập dữ liệu lớn trong Excel bằng Java?**
   - Sử dụng các kỹ thuật tải dữ liệu hiệu quả và cân nhắc phát trực tuyến đối với các tệp rất lớn.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}