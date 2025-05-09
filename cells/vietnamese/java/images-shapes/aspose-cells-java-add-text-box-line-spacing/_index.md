---
"date": "2025-04-08"
"description": "Tìm hiểu cách sử dụng Aspose.Cells for Java để thêm hộp văn bản và thiết lập khoảng cách dòng trong sổ làm việc Excel. Cải thiện bài thuyết trình sổ làm việc của bạn bằng các hình dạng văn bản có kiểu dáng."
"title": "Thêm hộp văn bản và thiết lập khoảng cách dòng trong Excel bằng Aspose.Cells cho Java"
"url": "/vi/java/images-shapes/aspose-cells-java-add-text-box-line-spacing/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Thêm hộp văn bản và thiết lập khoảng cách dòng trong Excel bằng Aspose.Cells cho Java

## Giới thiệu

Việc tạo báo cáo Excel động thường yêu cầu định dạng văn bản tùy chỉnh, chẳng hạn như thêm hộp văn bản có khoảng cách dòng cụ thể. Với Aspose.Cells for Java, điều này trở nên đơn giản và hiệu quả. Hướng dẫn này sẽ hướng dẫn bạn cách cải thiện bản trình bày sổ làm việc của mình bằng Aspose.Cells for Java để thêm hình dạng văn bản có kiểu.

Đến cuối hướng dẫn này, bạn sẽ học cách:
- Tạo một bảng tính Excel mới và truy cập vào các trang tính của nó
- Thêm hình hộp văn bản vào bảng tính
- Đặt khoảng cách dòng tùy chỉnh bên trong hình dạng văn bản
- Lưu sổ làm việc đã định dạng của bạn ở định dạng XLSX

Hãy bắt đầu bằng cách thiết lập môi trường của bạn.

### Điều kiện tiên quyết

Trước khi bắt đầu, hãy đảm bảo bạn có những điều sau:
- Bộ công cụ phát triển Java (JDK) được cài đặt trên máy của bạn
- Một IDE hoặc trình soạn thảo để viết mã Java
- Hệ thống xây dựng Maven hoặc Gradle được cấu hình để quản lý các phụ thuộc

Hiểu biết cơ bản về lập trình Java và quen thuộc với cấu trúc tệp Excel sẽ rất có lợi.

## Thiết lập Aspose.Cells cho Java

Bao gồm Aspose.Cells vào quản lý phụ thuộc của dự án bằng Maven hoặc Gradle:

**Maven**

Thêm khối phụ thuộc sau vào `pom.xml` tài liệu:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Tốt nghiệp**

Bao gồm điều này trong `build.gradle` tài liệu:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

Tiếp theo, hãy mua giấy phép cho Aspose.Cells bằng cách chọn dùng thử miễn phí, yêu cầu giấy phép tạm thời hoặc mua giấy phép đầy đủ.

### Khởi tạo Aspose.Cells

Sau khi thư viện được đưa vào dự án của bạn, hãy khởi tạo nó trong ứng dụng Java của bạn:

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) {
        // Khởi tạo một phiên bản của Workbook (đại diện cho một tệp Excel)
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## Hướng dẫn thực hiện

### Tạo một Workbook và Access Worksheet

Bắt đầu bằng cách tạo một sổ làm việc Excel mới và truy cập vào trang tính đầu tiên của sổ làm việc đó. Đây là nơi bạn sẽ thêm hộp văn bản của mình.

#### Tổng quan

Việc tạo một bảng tính mới sẽ cung cấp một bảng trống để thêm dữ liệu, hình dạng và định dạng khi cần.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

public class ExcelDemo {
    public static void main(String[] args) {
        // Tạo một Workbook mới (tệp Excel)
        Workbook workbook = new Workbook();
        
        // Truy cập vào bảng tính đầu tiên
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        System.out.println("Workbook and first worksheet accessed.");
    }
}
```

### Thêm hộp văn bản vào trang tính

Tiếp theo, thêm hình hộp văn bản vào trang tính đã chọn. Hình hộp này có thể chứa bất kỳ nội dung văn bản nào bạn cần.

#### Tổng quan

Hộp văn bản là công cụ đa năng để đưa các văn bản tùy chỉnh như ghi chú hoặc hướng dẫn trực tiếp vào trang tính Excel.

```java
import com.aspose.cells.Shape;
import com.aspose.cells.MsoDrawingType;

public class ExcelDemo {
    public static void main(String[] args) {
        // Tạo một Workbook mới (tệp Excel)
        Workbook workbook = new Workbook();
        
        // Truy cập vào bảng tính đầu tiên
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Thêm hình hộp văn bản vào bảng tính
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        System.out.println("Text box added.");
    }
}
```

### Đặt Văn bản trong Hình dạng

Khi hộp văn bản đã sẵn sàng, hãy thiết lập nội dung và định dạng văn bản bên trong.

```java
import com.aspose.cells.Shape;

public class ExcelDemo {
    public static void main(String[] args) {
        // Tạo một Workbook mới (tệp Excel)
        Workbook workbook = new Workbook();
        
        // Truy cập vào bảng tính đầu tiên
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Thêm hình hộp văn bản vào bảng tính
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Đặt nội dung văn bản bên trong hình dạng
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        System.out.println("Text set in shape.");
    }
}
```

### Truy cập đoạn văn bản trong hình dạng

Bạn có thể truy cập từng đoạn văn bản trong hộp văn bản để áp dụng định dạng cụ thể.

```java
import com.aspose.cells.TextParagraph;

public class ExcelDemo {
    public static void main(String[] args) {
        // Tạo một Workbook mới (tệp Excel)
        Workbook workbook = new Workbook();
        
        // Truy cập vào bảng tính đầu tiên
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Thêm hình hộp văn bản vào bảng tính
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Đặt nội dung văn bản bên trong hình dạng
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Truy cập đoạn văn thứ hai trong hình dạng
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);
        
        System.out.println("Accessed second paragraph in text box.");
    }
}
```

### Thiết lập khoảng cách dòng của đoạn văn

Tùy chỉnh khoảng cách dòng có thể cải thiện khả năng đọc. Sau đây là cách thiết lập:

```java
import com.aspose.cells.LineSpaceSizeType;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Tạo một Workbook mới (tệp Excel)
        Workbook workbook = new Workbook();
        
        // Truy cập vào bảng tính đầu tiên
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Thêm hình hộp văn bản vào bảng tính
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Đặt nội dung văn bản bên trong hình dạng
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Truy cập đoạn văn thứ hai trong hình dạng
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Đặt khoảng cách dòng là 20 điểm
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // Cấu hình khoảng cách trước và sau đoạn văn
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        System.out.println("Line spacing set.");
    }
}
```

### Lưu sổ làm việc

Cuối cùng, lưu sổ làm việc của bạn với hộp văn bản vừa được thêm và định dạng.

```java
import com.aspose.cells.SaveFormat;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Tạo một Workbook mới (tệp Excel)
        Workbook workbook = new Workbook();
        
        // Truy cập vào bảng tính đầu tiên
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Thêm hình hộp văn bản vào bảng tính
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Đặt nội dung văn bản bên trong hình dạng
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Truy cập đoạn văn thứ hai trong hình dạng
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Đặt khoảng cách dòng là 20 điểm
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // Cấu hình khoảng cách trước và sau đoạn văn
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        // Lưu sổ làm việc
        workbook.save("StyledTextShape.xlsx", SaveFormat.XLSX);
    }
}
```

## Phần kết luận

Bạn đã học thành công cách thêm hộp văn bản và đặt khoảng cách dòng trong sổ làm việc Excel bằng Aspose.Cells for Java. Điều này giúp bạn nâng cao khả năng tạo báo cáo động, hấp dẫn về mặt hình ảnh.

## Khuyến nghị từ khóa
- "Aspose.Cells dành cho Java"
- "Thêm hộp văn bản vào Excel"
- "Thiết lập khoảng cách dòng trong Excel"
- "Sổ làm việc Excel có văn bản được định dạng"
- "Java và Aspose.Cells"


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}