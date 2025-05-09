---
"date": "2025-04-07"
"description": "Tìm hiểu cách tạo và tùy chỉnh biểu đồ trong Excel bằng Aspose.Cells for Java. Tự động tạo biểu đồ, nâng cao khả năng trực quan hóa dữ liệu và tiết kiệm thời gian với hướng dẫn chi tiết này."
"title": "Tạo và định dạng biểu đồ Excel bằng Aspose.Cells Java&#58; Hướng dẫn toàn diện"
"url": "/vi/java/charts-graphs/aspose-cells-java-excel-charts-creation/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Tạo và định dạng biểu đồ Excel bằng Aspose.Cells Java

## Giới thiệu

Trong thế giới dữ liệu ngày nay, trực quan hóa thông tin hiệu quả là rất quan trọng đối với việc phân tích và ra quyết định. Thường thì cần phải tạo biểu đồ động trong sổ làm việc Excel theo chương trình—đặc biệt là khi xử lý các tập dữ liệu lớn hoặc hệ thống báo cáo tự động. Hướng dẫn này trình bày cách sử dụng Aspose.Cells cho Java để tạo và tùy chỉnh biểu đồ trong Excel một cách liền mạch. Bằng cách tích hợp Aspose.Cells vào các ứng dụng Java của bạn, bạn có thể tự động hóa việc tạo biểu đồ, cải thiện trình bày dữ liệu và tiết kiệm thời gian.

**Những gì bạn sẽ học được:**
- Khởi tạo một bảng tính và nhập dữ liệu vào đó bằng Aspose.Cells.
- Tạo và cấu hình biểu đồ đường với các điểm đánh dấu dữ liệu.
- Tùy chỉnh giao diện và màu sắc của chuỗi để trực quan hóa tốt hơn.
- Lưu bảng tính có biểu đồ mới tạo ở định dạng Excel.

Chúng ta hãy bắt đầu bằng cách thảo luận về các điều kiện tiên quyết cần thiết để bắt đầu.

## Điều kiện tiên quyết

Trước khi tạo và định dạng biểu đồ bằng Aspose.Cells for Java, hãy đảm bảo bạn đã thiết lập xong các bước sau:

### Thư viện bắt buộc
Bao gồm Aspose.Cells như một dependency trong dự án của bạn. Sau đây là hướng dẫn cho cả người dùng Maven và Gradle:

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
- Môi trường phát triển tích hợp (IDE) như IntelliJ IDEA hoặc Eclipse để mã hóa và thử nghiệm.

### Điều kiện tiên quyết về kiến thức
Cần có hiểu biết cơ bản về lập trình Java, cùng với sự quen thuộc với bảng tính Excel và các khái niệm về biểu đồ. 

### Mua lại giấy phép
Aspose.Cells là sản phẩm thương mại yêu cầu phải có giấy phép để có đầy đủ chức năng. Bạn có thể dùng thử miễn phí để đánh giá các tính năng, yêu cầu giấy phép tạm thời để thử nghiệm mở rộng hoặc mua sản phẩm để sử dụng lâu dài.

- **Dùng thử miễn phí:** [Tải xuống bản dùng thử miễn phí](https://releases.aspose.com/cells/java/)
- **Giấy phép tạm thời:** [Yêu cầu Giấy phép tạm thời](https://purchase.aspose.com/temporary-license/)
- **Mua:** [Mua Aspose.Cells](https://purchase.aspose.com/buy)

## Thiết lập Aspose.Cells cho Java

Sau khi bạn đã cài đặt các phụ thuộc cần thiết, hãy thiết lập môi trường phát triển của bạn để sử dụng Aspose.Cells. Bắt đầu bằng cách nhập thư viện và khởi tạo đối tượng Workbook trong ứng dụng Java của bạn:

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // Khởi tạo một phiên bản sổ làm việc mới
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## Hướng dẫn thực hiện

Trong phần này, chúng tôi sẽ chia nhỏ quá trình triển khai thành các tính năng riêng biệt: Khởi tạo sổ làm việc và điền dữ liệu, Tạo và cấu hình biểu đồ, Tùy chỉnh chuỗi và Lưu sổ làm việc.

### Tính năng 1: Khởi tạo sổ làm việc và điền dữ liệu

**Tổng quan:** Tính năng này tập trung vào việc tạo một bảng tính mới, truy cập vào trang tính đầu tiên của bảng tính đó và điền dữ liệu vào đó để tạo biểu đồ.

#### Bước 1: Khởi tạo Workbook
Bắt đầu bằng cách khởi tạo một `Workbook` sự vật:

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // Khởi tạo một sổ làm việc
        Workbook workbook = new Workbook();
        
        // Truy cập bảng tính đầu tiên
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### Bước 2: Đặt Tiêu đề Cột và Điền Dữ liệu
Xác định tiêu đề cột và điền dữ liệu mẫu vào các hàng:

```java
        // Đặt tiêu đề cột 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // Tạo dữ liệu ngẫu nhiên cho chuỗi 1
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // Tạo dữ liệu ngẫu nhiên cho chuỗi 2
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### Tính năng 2: Tạo và cấu hình biểu đồ

**Tổng quan:** Tính năng này trình bày cách thêm biểu đồ vào bảng tính của sổ làm việc, thiết lập kiểu biểu đồ và cấu hình các thuộc tính cơ bản.

#### Bước 3: Thêm biểu đồ vào bảng tính
Thêm biểu đồ đường có đánh dấu dữ liệu:

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // Khởi tạo một sổ làm việc
        Workbook workbook = new Workbook();
        
        // Truy cập bảng tính đầu tiên
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Thêm biểu đồ vào bảng tính
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // Truy cập và cấu hình biểu đồ
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // Đặt một kiểu được xác định trước
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### Tính năng 3: Cấu hình và tùy chỉnh Series

**Tổng quan:** Tăng tính hấp dẫn trực quan cho biểu đồ của bạn bằng cách tùy chỉnh cài đặt chuỗi, chẳng hạn như nhiều màu sắc và kiểu đánh dấu khác nhau.

#### Bước 4: Tùy chỉnh cài đặt Series
Cấu hình dữ liệu chuỗi, áp dụng định dạng tùy chỉnh và điều chỉnh điểm đánh dấu:

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // Khởi tạo một sổ làm việc
        Workbook workbook = new Workbook();
        
        // Truy cập bảng tính đầu tiên
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Thêm chuỗi vào biểu đồ
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // Cho phép nhiều màu sắc khác nhau cho các điểm chuỗi
        chart.getNSeries().setColorVaried(true);

        // Tùy chỉnh kiểu dáng và màu sắc của dấu hiệu đầu tiên
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // Đặt giá trị X và Y cho chuỗi đầu tiên
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // Tùy chỉnh kiểu dáng và màu sắc của dấu hiệu sê-ri thứ hai
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // Đặt giá trị X và Y cho chuỗi thứ hai
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### Tính năng 4: Lưu sổ làm việc

**Tổng quan:** Cuối cùng, hãy lưu sổ làm việc để lưu lại những thay đổi và đảm bảo rằng biểu đồ được bao gồm trong tệp Excel.

#### Bước 5: Lưu sổ làm việc
Lưu bảng tính của bạn với các biểu đồ mới tạo:

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // Khởi tạo một sổ làm việc
        Workbook workbook = new Workbook();
        
        // Truy cập bảng tính đầu tiên và thêm dữ liệu, cấu hình biểu đồ theo các bước trước đó...
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // (Triển khai thêm dữ liệu và cấu hình biểu đồ sẽ ở đây)

        // Lưu sổ làm việc vào tệp Excel
        workbook.save("StyledChart.xlsx");
    }
}
```

**Đề xuất từ khóa:**
- "Aspose.Cells dành cho Java"
- "Tạo biểu đồ Excel bằng Java"
- "Lập trình Java để tự động hóa Excel"

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}