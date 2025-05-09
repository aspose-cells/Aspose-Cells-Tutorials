---
"date": "2025-04-07"
"description": "Tìm hiểu cách chuyển đổi hiệu quả các tệp Excel sang định dạng CSV bằng Aspose.Cells for Java. Hướng dẫn này bao gồm tải, cấu hình và lưu sổ làm việc với các bước chi tiết."
"title": "Cách tải và lưu Excel dưới dạng CSV bằng Aspose.Cells cho Java&#58; Hướng dẫn toàn diện"
"url": "/vi/java/workbook-operations/aspose-cells-java-load-save-excel-csv/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Cách tải và lưu Excel dưới dạng CSV bằng Aspose.Cells cho Java
## Giới thiệu
Việc chuyển đổi các tập dữ liệu Excel sang các định dạng văn bản như CSV trong khi vẫn giữ nguyên các chi tiết cụ thể như dấu phân cách có thể là một thách thức. Hướng dẫn toàn diện này trình bày cách sử dụng Aspose.Cells cho Java để tải, cấu hình và lưu sổ làm việc Excel dưới dạng tệp CSV một cách hiệu quả. Đến cuối hướng dẫn này, bạn sẽ nắm vững các quy trình này trong các ứng dụng Java của mình.

**Những gì bạn sẽ học được:**
- Tải một tệp Excel hiện có vào đối tượng Workbook bằng Aspose.Cells
- Cấu hình TxtSaveOptions để quản lý các dấu phân cách cho các hàng trống
- Lưu sổ làm việc của bạn dưới dạng tệp CSV với các cấu hình cụ thể

## Điều kiện tiên quyết
Trước khi bắt đầu, hãy đảm bảo bạn có những điều sau:
- **Môi trường phát triển Java:** Đã cài đặt và cấu hình JDK.
- **Thư viện Aspose.Cells cho Java:** Yêu cầu phiên bản 25.3 trở lên.
- **Ý tưởng:** Sử dụng IntelliJ IDEA, Eclipse hoặc bất kỳ môi trường phát triển nào bạn thích.

## Thiết lập Aspose.Cells cho Java
### Phụ thuộc Maven
Để bao gồm Aspose.Cells trong dự án Maven của bạn, hãy thêm điều này vào `pom.xml`:
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```
### Phụ thuộc Gradle
Đối với người dùng Gradle, hãy thêm điều này vào `build.gradle`:
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```
## Xin giấy phép
Aspose.Cells for Java cung cấp cả giấy phép dùng thử và thương mại. Bắt đầu với [dùng thử miễn phí](https://releases.aspose.com/cells/java/) để khám phá khả năng của nó hoặc mua giấy phép nếu phù hợp. Đối với giấy phép tạm thời, hãy truy cập [trang giấy phép tạm thời](https://purchase.aspose.com/temporary-license/).
## Hướng dẫn thực hiện
### Tải một bảng tính Excel
**Tổng quan:**
Việc tải tệp Excel vào Aspose.Cells rất đơn giản và cần thiết cho các hoạt động tiếp theo.
#### Hướng dẫn từng bước:
1. **Nhập các lớp cần thiết**
   Nhập khẩu `Workbook` lớp từ gói Aspose.Cells:
   ```java
   import com.aspose.cells.Workbook;
   ```
2. **Tải một tập tin Excel**
   Tạo một phiên bản Workbook với đường dẫn tệp của bạn:
   ```java
   String dataDir = "YOUR_DATA_DIRECTORY";
   Workbook workbook = new Workbook(dataDir + "/KeepSeparatorsForBlankRow.xlsx");
   ```
### Cấu hình TxtSaveOptions để Xử lý Dấu phân cách
**Tổng quan:**
Tùy chỉnh cách lưu tệp văn bản, bao gồm giữ nguyên dấu phân cách trong các hàng trống bằng `TxtSaveOptions`.
#### Hướng dẫn từng bước:
1. **Nhập lớp TxtSaveOptions**
   Nhập lớp cần thiết để cấu hình tùy chọn lưu:
   ```java
   import com.aspose.cells.TxtSaveOptions;
   ```
2. **Đặt tùy chọn để giữ dấu phân cách**
   Cấu hình `TxtSaveOptions` để duy trì các dấu phân cách trong các hàng trống:
   ```java
   TxtSaveOptions options = new TxtSaveOptions();
   options.setKeepSeparatorsForBlankRow(true);
   ```
### Lưu sổ làm việc dưới dạng tệp CSV với các tùy chọn
**Tổng quan:**
Bước này bao gồm việc lưu sổ làm việc của bạn dưới dạng tệp văn bản, cụ thể là tệp CSV trong ví dụ này.
#### Hướng dẫn từng bước:
1. **Thiết lập đường dẫn lưu**
   Xác định vị trí lưu đầu ra:
   ```java
   String outDir = "YOUR_OUTPUT_DIRECTORY";
   ```
2. **Lưu sổ làm việc với các tùy chọn được cấu hình**
   Sử dụng `save` phương pháp ghi sổ làm việc của bạn dưới dạng tệp CSV, áp dụng các tùy chọn đã cấu hình:
   ```java
   Workbook workbook = new Workbook("YOUR_DATA_DIRECTORY/KeepSeparatorsForBlankRow.xlsx");
   TxtSaveOptions options = new TxtSaveOptions();
   options.setKeepSeparatorsForBlankRow(true);
   workbook.save(outDir + "/KeepSeparatorsForBlankRow.out.csv", options);
   ```
## Ứng dụng thực tế
1. **Xuất dữ liệu để báo cáo:** Chuyển đổi dữ liệu Excel sang định dạng CSV để làm công cụ báo cáo.
2. **Các tập lệnh xử lý hàng loạt:** Tự động chuyển đổi nhiều tệp Excel trong một thư mục.
3. **Tích hợp với cơ sở dữ liệu:** Chuẩn bị và xuất dữ liệu Excel dưới dạng CSV để nhập cơ sở dữ liệu.
## Cân nhắc về hiệu suất
Để xử lý các tập dữ liệu lớn một cách hiệu quả:
- Tối ưu hóa việc sử dụng bộ nhớ bằng cách giải phóng tài nguyên kịp thời bằng cách sử dụng `workbook.dispose()`.
- Sử dụng tính năng thu gom rác của Java để quản lý bộ nhớ hiệu quả trong các ứng dụng chạy lâu.
- Tạo hồ sơ cho ứng dụng của bạn để giải quyết mọi tắc nghẽn I/O của tệp.
## Phần kết luận
Bây giờ bạn đã hiểu cách tải, cấu hình và lưu sổ làm việc Excel dưới dạng tệp CSV bằng Aspose.Cells for Java. Hướng dẫn này đóng vai trò là nền tảng để tích hợp các khả năng này vào ứng dụng của bạn.
**Các bước tiếp theo:**
Khám phá thêm các tính năng của Aspose.Cells như thao tác dữ liệu và định dạng nâng cao để tăng cường chức năng.
## Phần Câu hỏi thường gặp
1. **Làm thế nào để xử lý các tệp lớn bằng Aspose.Cells?**
   - Sử dụng API phát trực tuyến và tối ưu hóa việc sử dụng bộ nhớ bằng cách phân bổ tài nguyên kịp thời.
2. **Tôi có thể sử dụng Aspose.Cells mà không cần giấy phép sản xuất không?**
   - Cần phải có giấy phép thương mại để sản xuất; hãy bắt đầu bằng bản dùng thử để khám phá các khả năng.
3. **Tôi phải xử lý các ký tự phân cách CSV khác nhau như thế nào?**
   - Cấu hình `TxtSaveOptions` sử dụng các phương pháp như `setSeparator(';')`.
4. **Nếu bảng tính của tôi có chứa công thức thì sao?**
   - Aspose.Cells sẽ tính toán và xuất kết quả công thức khi lưu sang định dạng văn bản.
5. **Tôi có thể tùy chỉnh định dạng ô trong quá trình chuyển đổi không?**
   - Có, hãy khám phá các tùy chọn bổ sung trong Aspose.Cells để tạo kiểu và trình bày dữ liệu.
## Tài nguyên
- [Tài liệu Aspose.Cells](https://reference.aspose.com/cells/java/)
- [Tải xuống Aspose.Cells](https://releases.aspose.com/cells/java/)
- [Mua giấy phép](https://purchase.aspose.com/buy)
- [Dùng thử miễn phí](https://releases.aspose.com/cells/java/)
- [Giấy phép tạm thời](https://purchase.aspose.com/temporary-license/)
- [Diễn đàn hỗ trợ Aspose](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}