---
"date": "2025-04-08"
"description": "Tìm hiểu cách quản lý và trích xuất hiệu quả các đối tượng OLE được nhúng trong tệp Excel bằng Aspose.Cells for Java. Làm theo hướng dẫn từng bước này để tích hợp liền mạch."
"title": "Trích xuất và lưu các đối tượng OLE từ Excel bằng Aspose.Cells Java&#58; Hướng dẫn đầy đủ"
"url": "/vi/java/ole-objects-embedded-content/aspose-cells-java-extract-save-ole-objects/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Trích xuất và lưu các đối tượng OLE từ Excel bằng Aspose.Cells Java: Hướng dẫn đầy đủ

## Giới thiệu

Quản lý các đối tượng OLE (Liên kết và Nhúng đối tượng) nhúng trong các tệp Excel có thể là một nhiệm vụ quan trọng đối với các nhà phát triển phần mềm và nhà phân tích dữ liệu. Hướng dẫn này cung cấp hướng dẫn toàn diện về cách sử dụng Aspose.Cells for Java để trích xuất và lưu các đối tượng này một cách hiệu quả, hợp lý hóa quy trình làm việc của bạn với nhiều định dạng tệp khác nhau.

**Những gì bạn sẽ học được:**
- Khởi tạo sổ làm việc Excel bằng Aspose.Cells
- Trích xuất các đối tượng OLE từ các trang tính
- Lưu các tập tin đã trích xuất ở nhiều định dạng khác nhau (DOCX, XLSX, PPTX, PDF)
- Xử lý các trường hợp cụ thể như lưu dưới dạng tệp Excel mới

Đến cuối hướng dẫn này, bạn sẽ có khả năng nâng cao các ứng dụng Java của mình với khả năng xử lý dữ liệu mạnh mẽ.

## Điều kiện tiên quyết

Trước khi tiếp tục, hãy đảm bảo bạn có:

**Thư viện cần thiết:**
- Aspose.Cells cho Java (phiên bản 25.3 trở lên)
- Khả năng tương thích với các phiên bản JDK phù hợp để chạy Aspose.Cells

**Yêu cầu thiết lập môi trường:**
- Hiểu biết cơ bản về Java và các công cụ xây dựng Maven/Gradle
- Một Môi trường phát triển tích hợp (IDE) như IntelliJ IDEA hoặc Eclipse

**Điều kiện tiên quyết về kiến thức:**
- Quen thuộc với việc xử lý tệp trong Java
- Hiểu về các đối tượng OLE trong Excel

## Thiết lập Aspose.Cells cho Java

Để bắt đầu, hãy đưa Aspose.Cells vào dự án của bạn bằng cách sử dụng các cấu hình sau:

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

### Mua lại giấy phép

Aspose.Cells cung cấp nhiều tùy chọn cấp phép khác nhau:
- **Dùng thử miễn phí**: Tải xuống bản dùng thử để kiểm tra chức năng.
- **Giấy phép tạm thời**: Xin giấy phép đánh giá mở rộng.
- **Mua**: Xin giấy phép sử dụng vĩnh viễn cho mục đích sản xuất.

Ghé thăm [trang mua hàng](https://purchase.aspose.com/buy) hoặc yêu cầu một [giấy phép tạm thời](https://purchase.aspose.com/temporary-license/) dựa trên nhu cầu của bạn.

### Khởi tạo cơ bản

Sau đây là cách bạn khởi tạo Aspose.Cells trong ứng dụng Java của mình:
```java
import com.aspose.cells.Workbook;

public class InitializeWorkbook {
    public static void main(String[] args) {
        Workbook workbook = new Workbook("path/to/excel/file.xlsx");
        // Tiến hành sử dụng đối tượng sổ làm việc khi cần thiết
    }
}
```

## Hướng dẫn thực hiện

### Tính năng 1: Trích xuất các đối tượng OLE từ Excel

**Tổng quan:** Khởi tạo một bảng tính và trích xuất các đối tượng nhúng từ bảng tính đầu tiên.

#### Bước 1: Khởi tạo Workbook
Thiết lập đường dẫn thư mục dữ liệu của bạn và tạo một `Workbook` ví dụ:
```java
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook(dataDir + "/oleFile.xlsx");
```

#### Bước 2: Trích xuất các đối tượng OLE
Truy cập bộ sưu tập các đối tượng OLE trong bảng tính đầu tiên:
```java
import com.aspose.cells.OleObjectCollection;

OleObjectCollection oleObjects = workbook.getWorksheets().get(0).getOleObjects();
for (int i = 0; i < oleObjects.getCount(); i++) {
    OleObject object = oleObjects.get(i);
    // Xử lý từng đối tượng ở đây
}
```

#### Bước 3: Lưu các đối tượng đã trích xuất
Lưu từng đối tượng OLE đã trích xuất dựa trên loại tệp của nó:
```java
import com.aspose.cells.FileFormatType;
import java.io.FileOutputStream;

String outDir = "YOUR_OUTPUT_DIRECTORY";
for (int i = 0; i < oleObjects.getCount(); i++) {
    OleObject object = oleObjects.get(i);
    String fileName = outDir + "/object" + i + ".";

    switch (object.getFileFormatType()) {
        case FileFormatType.DOCX:
            fileName += "docx";
            break;
        case FileFormatType.XLSX:
            fileName += "xlsx";
            break;
        // Thêm các định dạng khác khi cần thiết
    }

    if (object.getFileFormatType() == FileFormatType.XLSX) {
        byte[] bytes = object.getObjectData();
        Workbook oleBook = new Workbook(new java.io.ByteArrayInputStream(bytes));
        oleBook.getSettings().setHidden(false);
        oleBook.save(fileName);
    } else {
        try (FileOutputStream fos = new FileOutputStream(fileName)) {
            fos.write(object.getObjectData());
        }
    }
}
```

### Tính năng 2: Lưu đối tượng OLE dưới dạng tệp Excel
**Tổng quan:** Trình bày cách lưu đối tượng OLE đã trích xuất cụ thể dưới dạng tệp Excel.

#### Bước 1: Lấy dữ liệu OLE
Giả sử bạn có `byte[] bytes` từ một `OleObject`:
```java
import com.aspose.cells.Workbook;
import java.io.ByteArrayInputStream;

Workbook oleBook = new Workbook(new ByteArrayInputStream(bytes));
oleBook.getSettings().setHidden(false);
oleBook.save("YOUR_OUTPUT_DIRECTORY/object.xlsx");
```

## Ứng dụng thực tế

- **Hợp nhất dữ liệu:** Trích xuất nhiều loại tài liệu khác nhau từ Excel để lưu trữ tập trung.
- **Tạo báo cáo tự động:** Tích hợp và lưu báo cáo ở nhiều định dạng khác nhau trực tiếp từ ứng dụng của bạn.
- **Công cụ di chuyển dữ liệu:** Sử dụng dữ liệu đã trích xuất cho quá trình di chuyển giữa các hệ thống.

## Cân nhắc về hiệu suất

- Tối ưu hóa việc sử dụng bộ nhớ bằng cách quản lý các đối tượng lớn một cách hiệu quả, có thể thông qua phương pháp phát trực tuyến.
- Sử dụng cài đặt của Aspose.Cells để quản lý khả năng hiển thị và kích thước của bảng tính một cách linh hoạt.
- Triển khai các biện pháp xử lý tệp hiệu quả để ngăn ngừa rò rỉ tài nguyên.

## Phần kết luận

Bằng cách làm theo hướng dẫn này, bạn có thể trích xuất và lưu các đối tượng OLE hiệu quả bằng Aspose.Cells for Java. Các khả năng này cải thiện đáng kể quy trình quản lý dữ liệu của bạn.

**Các bước tiếp theo:**
Hãy cân nhắc khám phá các tính năng bổ sung của Aspose.Cells như thao tác biểu đồ hoặc chuyển đổi tệp Excel nâng cao để mở rộng thêm các ứng dụng Java của bạn.

## Phần Câu hỏi thường gặp

1. **Tôi phải xử lý các định dạng đối tượng OLE không được hỗ trợ như thế nào?**
   - Sử dụng định dạng mặc định (như JPG) cho các đối tượng không xác định.
2. **Tôi có thể trích xuất các đối tượng OLE từ nhiều trang tính không?**
   - Có, hãy lặp lại từng bảng tính trong sổ làm việc và lặp lại quy trình trích xuất.
3. **Nếu đối tượng OLE không lưu đúng cách thì sao?**
   - Kiểm tra quyền của tệp và đảm bảo đường dẫn thư mục đầu ra là chính xác.
4. **Aspose.Cells có hỗ trợ tất cả các phiên bản Excel không?**
   - Aspose.Cells hỗ trợ nhiều định dạng Excel, bao gồm cả những định dạng cũ như XLS.
5. **Làm thế nào để tối ưu hóa hiệu suất khi xử lý các tệp lớn?**
   - Hãy cân nhắc xử lý theo từng phần hoặc sử dụng kỹ thuật truyền phát tệp để quản lý việc sử dụng bộ nhớ hiệu quả.

## Tài nguyên
- [Tài liệu](https://reference.aspose.com/cells/java/)
- [Tải xuống Aspose.Cells](https://releases.aspose.com/cells/java/)
- [Mua giấy phép](https://purchase.aspose.com/buy)
- [Tải xuống dùng thử miễn phí](https://releases.aspose.com/cells/java/)
- [Yêu cầu cấp giấy phép tạm thời](https://purchase.aspose.com/temporary-license/)
- [Diễn đàn hỗ trợ cộng đồng](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}