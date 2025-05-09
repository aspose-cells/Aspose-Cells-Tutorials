---
"date": "2025-04-08"
"description": "Học cách tạo và tùy chỉnh biểu đồ hình tròn bằng Aspose.Cells cho Java. Hướng dẫn từng bước với các ví dụ mã dành cho nhà phát triển."
"title": "Làm chủ Aspose.Cells&#58; Tạo & Tùy chỉnh Biểu đồ hình tròn trong Java"
"url": "/vi/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Làm chủ Aspose.Cells: Tạo và tùy chỉnh biểu đồ hình tròn trong Java

## Giới thiệu
Tạo biểu đồ hấp dẫn trực quan là yêu cầu chung khi xử lý trực quan hóa dữ liệu trong Excel. Cho dù bạn đang trình bày thông tin nhân khẩu học hay phân tích xu hướng thị trường, biểu đồ hình tròn đều cung cấp một cách rõ ràng để biểu diễn dữ liệu theo tỷ lệ. Tuy nhiên, việc thiết lập các biểu đồ này theo chương trình có thể phức tạp. Hướng dẫn này hướng dẫn bạn cách tạo và tùy chỉnh Biểu đồ hình tròn Aspose.Cells bằng Java, giúp đơn giản hóa quy trình cho các nhà phát triển.

**Những gì bạn sẽ học được:**
- Thiết lập môi trường của bạn với Aspose.Cells cho Java.
- Tạo một bảng tính mới và truy cập các ô trong bảng tính.
- Điền dữ liệu vào các ô cụ thể để chuẩn bị cho việc tạo biểu đồ.
- Tạo biểu đồ hình tròn từ dữ liệu này.
- Tùy chỉnh giao diện biểu đồ hình tròn, bao gồm màu sắc, tiêu đề và chú thích.

Trước khi bắt đầu, hãy đảm bảo bạn có một số hiểu biết cơ bản về lập trình Java và quản lý phụ thuộc Maven hoặc Gradle. Hãy cùng thiết lập môi trường của chúng ta!

## Điều kiện tiên quyết
Để thực hiện theo hướng dẫn này, bạn sẽ cần:
- **Bộ phát triển Java (JDK)**: Phiên bản 8 trở lên.
- **Môi trường phát triển tích hợp (IDE)**: Chẳng hạn như IntelliJ IDEA hoặc Eclipse.
- **Quản lý phụ thuộc**: Sử dụng Maven hoặc Gradle để quản lý các phụ thuộc của bạn.

### Thư viện và phụ thuộc bắt buộc
Đảm bảo đưa Aspose.Cells for Java vào dự án của bạn bằng Maven hoặc Gradle.

**Maven**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Tốt nghiệp**
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Các bước xin cấp giấy phép
Aspose.Cells for Java là một thư viện thương mại, nhưng bạn có thể bắt đầu bằng bản dùng thử miễn phí hoặc đăng ký giấy phép tạm thời. Truy cập [trang mua hàng](https://purchase.aspose.com/buy) để khám phá các lựa chọn cấp phép.

## Thiết lập Aspose.Cells cho Java
Trước tiên, hãy đảm bảo môi trường dự án của bạn bao gồm các thư viện cần thiết bằng cách thêm chúng thông qua Maven hoặc Gradle như được hiển thị ở trên. Sau khi đã bao gồm, bạn có thể khởi tạo Aspose.Cells:

```java
import com.aspose.cells.Workbook;

// Khởi tạo một phiên bản sổ làm việc mới
Workbook workbook = new Workbook();
```

## Hướng dẫn thực hiện

### Tạo và cấu hình một sổ làm việc
Tạo bảng tính là bước đầu tiên để bạn thiết lập dữ liệu.

#### Nhập thư viện
Đảm bảo các mục nhập này được bao gồm ở đầu tệp của bạn:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Cells;
import com.aspose.cells.ChartType;
import com.aspose.cells.Chart;
import com.aspose.cells.Series;
import com.aspose.cells.Color;
import com.aspose.cells.LegendPositionType;
import com.aspose.cells.SaveFormat;
```

#### Bước 1: Tạo một phiên bản Workbook
```java
// Tạo một phiên bản sổ làm việc trống để làm việc.
Workbook workbook = new Workbook();
```
Bước này khởi tạo tệp Excel của bạn theo chương trình, cho phép bạn thao tác tệp này bằng các chức năng của Aspose.Cells.

### Truy cập hoặc sửa đổi ô bảng tính
Tiếp theo, nhập dữ liệu vào các ô trong bảng tính sẽ được sử dụng cho biểu đồ hình tròn.

#### Bước 2: Truy cập vào một trang tính và các ô của nó
```java
// Truy cập vào trang tính đầu tiên trong sổ làm việc.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Đưa các giá trị mẫu được sử dụng cho biểu đồ hình tròn vào các ô cụ thể.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Đặt giá trị phần trăm cho biểu đồ hình tròn vào các ô cụ thể.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```
Tại đây, bạn điền dữ liệu vào bảng tính để biểu diễn các phân đoạn khác nhau của biểu đồ hình tròn.

### Tạo biểu đồ hình tròn

#### Bước 3: Thêm biểu đồ hình tròn vào bảng tính
```java
// Tạo biểu đồ hình tròn trong bảng tính.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```
Bước này sẽ thêm một biểu đồ hình tròn mới vào bảng tính của bạn ở các vị trí và kích thước đã chỉ định.

### Cấu hình Chuỗi biểu đồ hình tròn và Dữ liệu

#### Bước 4: Thiết lập Chuỗi cho Biểu đồ
```java
// Cấu hình phạm vi dữ liệu chuỗi cho biểu đồ.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Liên kết tiêu đề biểu đồ hình tròn với ô chứa văn bản tiêu đề.
pie.getTitle().setLinkedSource("D2");
```
Mã này liên kết phạm vi dữ liệu của bạn và thiết lập chuỗi cho biểu đồ hình tròn.

### Cấu hình chú giải biểu đồ và giao diện tiêu đề

#### Bước 5: Tùy chỉnh chú giải và tiêu đề biểu đồ
```java
// Đặt vị trí chú giải ở cuối biểu đồ.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Đặt thuộc tính phông chữ cho tiêu đề biểu đồ.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```
Việc tùy chỉnh giao diện sẽ tăng khả năng đọc và tính hấp dẫn về mặt thị giác.

### Tùy chỉnh màu sắc của chuỗi biểu đồ

#### Bước 6: Thay đổi màu của phân đoạn hình tròn
```java
import com.aspose.cells.Color;

// Truy cập và tùy chỉnh màu sắc của từng phân đoạn biểu đồ hình tròn.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```
Các thiết lập này sẽ cá nhân hóa biểu đồ của bạn để phù hợp với các bảng màu cụ thể.

### Tự động điều chỉnh cột và lưu sổ làm việc

#### Bước 7: Điều chỉnh độ rộng cột và lưu tệp
```java
// Tự động điều chỉnh tất cả các cột.
worksheet.autoFitColumns();

// Xác định đường dẫn giữ chỗ thư mục đầu ra để lưu sổ làm việc.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Lưu bảng tính đã sửa đổi vào tệp Excel trong thư mục đã chỉ định.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```
Cuối cùng, tự động điều chỉnh các cột và lưu bảng tính của bạn.

## Ứng dụng thực tế
1. **Phân tích nhân khẩu học**:Sử dụng biểu đồ hình tròn để hiển thị sự phân bố dân số giữa các quốc gia hoặc khu vực khác nhau.
2. **Báo cáo thị phần**: Minh họa thị phần của các công ty khác nhau trong một lĩnh vực.
3. **Phân bổ ngân sách**: Hình dung cách phân bổ ngân sách cho các phòng ban khác nhau trong một tổ chức.

Các ứng dụng này chứng minh tính linh hoạt và tiện ích của Aspose.Cells trong các tình huống thực tế.

## Cân nhắc về hiệu suất
Để tối ưu hóa hiệu suất khi sử dụng Aspose.Cells:
- Giảm thiểu việc sử dụng bộ nhớ bằng cách loại bỏ các đối tượng không còn cần thiết.
- Sử dụng cấu trúc dữ liệu hiệu quả để xử lý các tập dữ liệu lớn.
- Phân tích ứng dụng của bạn để xác định điểm nghẽn.

Việc tuân thủ các biện pháp tốt nhất sẽ đảm bảo các ứng dụng hoạt động trơn tru và phản hồi nhanh.

## Phần kết luận
Hướng dẫn này hướng dẫn bạn các bước để tạo và tùy chỉnh biểu đồ hình tròn bằng Aspose.Cells trong Java. Với kiến thức này, giờ đây bạn có thể áp dụng các kỹ thuật này vào nhiều tác vụ trực quan hóa dữ liệu khác nhau trong các dự án của mình. Để khám phá thêm, hãy cân nhắc tìm hiểu sâu hơn về các loại biểu đồ bổ sung và các tùy chọn tùy chỉnh nâng cao có sẵn với Aspose.Cells.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}