---
"date": "2025-04-08"
"description": "Học cách thiết lập công thức mảng, áp dụng kiểu số, tùy chỉnh phép tính và lưu sổ làm việc hiệu quả bằng Aspose.Cells cho Java."
"title": "Làm chủ công thức mảng Excel với Aspose.Cells Java & Tối ưu hóa tính toán và định dạng"
"url": "/vi/java/formulas-functions/aspose-cells-java-array-formulas-custom-calculations/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Làm chủ công thức mảng và tính toán tùy chỉnh với Aspose.Cells Java

## Giới thiệu

Bạn có muốn sắp xếp hợp lý các tác vụ xử lý dữ liệu Excel của mình bằng Java không? Nhiều nhà phát triển gặp phải thách thức khi cố gắng xử lý các công thức bảng tính phức tạp theo chương trình. Hướng dẫn này sẽ hướng dẫn bạn cách tận dụng **Aspose.Cells cho Java** để thiết lập công thức mảng, áp dụng kiểu số, tùy chỉnh phép tính và lưu công việc của bạn một cách hiệu quả. Cho dù bạn là một nhà phát triển dày dạn kinh nghiệm hay chỉ mới bắt đầu với tự động hóa Excel trong Java, hướng dẫn toàn diện này là hoàn hảo cho bạn.

### Những gì bạn sẽ học được
- Cách thiết lập công thức mảng bằng Aspose.Cells
- Áp dụng định dạng số cho các ô theo chương trình
- Triển khai các tùy chọn tính toán tùy chỉnh với các hàm do người dùng xác định
- Thiết lập chế độ tính toán và lưu sổ làm việc dưới dạng XLSX hoặc PDF
- Ứng dụng thực tế của các tính năng này trong các dự án Java của bạn

Hãy cùng tìm hiểu những điều kiện tiên quyết bạn cần có trước khi triển khai những tính năng mạnh mẽ này.

## Điều kiện tiên quyết
Trước khi tìm hiểu về Aspose.Cells for Java, hãy đảm bảo bạn có:

### Thư viện và thiết lập môi trường cần thiết
- **Aspose.Cells cho Java** phiên bản 25.3 trở lên
- Một IDE phù hợp (ví dụ: IntelliJ IDEA hoặc Eclipse)
- JDK đã được cài đặt trên máy của bạn

### Yêu cầu về kiến thức
- Hiểu biết cơ bản về lập trình Java
- Làm quen với các khái niệm bảng tính Excel

Bây giờ, chúng ta hãy thiết lập Aspose.Cells trong dự án của bạn!

## Thiết lập Aspose.Cells cho Java
Để bắt đầu sử dụng Aspose.Cells for Java, hãy bao gồm nó như một dependency trong dự án của bạn. Sau đây là các bước cài đặt cho Maven và Gradle:

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
implementation 'com.aspose:aspose-cells:25.3'
```

### Mua lại giấy phép
Aspose.Cells cung cấp giấy phép dùng thử miễn phí, bạn có thể mua bằng cách truy cập [Trang giấy phép tạm thời của Aspose](https://purchase.aspose.com/temporary-license/). Để có quyền truy cập đầy đủ, hãy cân nhắc mua gói đăng ký.

### Khởi tạo và thiết lập cơ bản
Sau khi thêm phần phụ thuộc, hãy khởi tạo Aspose.Cells như sau:

```java
import com.aspose.cells.Workbook;

// Khởi tạo sổ làm việc
Workbook workbook = new Workbook();
```

## Hướng dẫn thực hiện
Bây giờ bạn đã thiết lập xong, chúng ta hãy cùng khám phá từng tính năng theo từng bước.

### Thiết lập công thức mảng trong một ô
Công thức mảng cho phép thực hiện các phép tính phức tạp trên nhiều ô. Sau đây là cách thiết lập một công thức mảng bằng Aspose.Cells:

#### Tổng quan
Sử dụng `setArrayFormula` phương pháp này, bạn có thể gán công thức mảng theo cách lập trình.

#### Các bước thực hiện
1. **Khởi tạo Workbook và Cells**

   ```java
   import com.aspose.cells.Cell;
   import com.aspose.cells.Cells;
   import com.aspose.cells.Workbook;

   String dataDir = "YOUR_DATA_DIRECTORY";
   Workbook workbook = new Workbook();
   Cells cells = workbook.getWorksheets().get(0).getCells();
   Cell cell = cells.get(0, 0);
   ```

2. **Đặt công thức mảng**

   ```java
   // Đặt công thức mảng trong phạm vi 2x2 bắt đầu từ (0,0)
   cell.setArrayFormula("=MYFUNC()", 2, 2);
   ```

#### Cấu hình chính
- Các `setArrayFormula` phương pháp này có ba tham số: chuỗi công thức, số hàng và số cột.
- Đảm bảo chức năng tùy chỉnh của bạn (`MYFUNC`) được định nghĩa trong Excel hoặc dưới dạng UDF (Hàm do người dùng xác định) nếu cần.

### Áp dụng Kiểu Số cho Ô
Định dạng ô giúp tăng khả năng đọc. Sau đây là cách áp dụng kiểu số:

#### Tổng quan
Sử dụng `setNumber` phương pháp trên đối tượng kiểu của ô để định dạng nó.

#### Các bước thực hiện
1. **Lấy lại và thiết lập phong cách**

   ```java
   import com.aspose.cells.Style;

   // Lấy kiểu hiện tại của ô
   Style style = cell.getStyle();
   
   // Đặt định dạng số (ví dụ: tiền tệ)
   style.setNumber(14);
   
   // Áp dụng kiểu trở lại ô
   cell.setStyle(style);
   ```

#### Cấu hình chính
- Định dạng số được xác định bởi các hằng số như `14` cho tiền tệ.
- Sửa đổi giá trị này dựa trên yêu cầu định dạng của bạn.

### Tùy chọn tính toán tùy chỉnh với các hàm do người dùng xác định
Nâng cao khả năng tính toán bằng cách sử dụng các hàm tùy chỉnh cho nhu cầu cụ thể:

#### Tổng quan
Tùy chỉnh đánh giá công thức bằng cách sử dụng `CalculationOptions`.

#### Các bước thực hiện
1. **Thiết lập chức năng tùy chỉnh**

   ```java
   import com.aspose.cells.CalculationOptions;
   import com.aspose.cells.CustomFunctionStaticValue;

   // Khởi tạo các tùy chọn tính toán bằng một hàm tùy chỉnh
   CalculationOptions copt = new CalculationOptions();
   copt.setCustomEngine(new CustomFunctionStaticValue());
   
   // Tính toán công thức với công cụ tùy chỉnh
   workbook.calculateFormula(copt);
   ```

#### Cấu hình chính
- Sử dụng `setCustomEngine` để xác định logic tính toán tùy chỉnh của bạn.
- Đảm bảo các chức năng tùy chỉnh của bạn phù hợp với kỳ vọng của Aspose.Cells.

### Thiết lập chế độ tính toán và lưu dưới dạng XLSX
Kiểm soát cách thực hiện tính toán và lưu công việc của bạn một cách hiệu quả:

#### Tổng quan
Đặt chế độ tính toán thủ công để tối ưu hóa hiệu suất trước khi lưu sổ làm việc.

#### Các bước thực hiện
1. **Cấu hình cài đặt tính toán**

   ```java
   import com.aspose.cells.CalcModeType;

   String outDir = "YOUR_OUTPUT_DIRECTORY";
   
   // Đặt chế độ tính toán thành MANUAL
   workbook.getSettings().getFormulaSettings().setCalculationMode(CalcModeType.MANUAL);
   ```

2. **Lưu dưới dạng XLSX**

   ```java
   // Lưu sổ làm việc ở định dạng Excel
   workbook.save(outDir + "output.xlsx");
   ```

#### Cấu hình chính
- `MANUAL` chế độ này ngăn chặn việc tính toán lại tự động, nâng cao hiệu suất.
- Điều chỉnh cài đặt tính toán dựa trên nhu cầu của dự án.

### Lưu Workbook dưới dạng PDF
Xuất sang PDF có thể hữu ích cho việc chia sẻ hoặc in ấn:

```java
// Lưu sổ làm việc ở định dạng PDF
workbook.save(outDir + "output.pdf");
```

## Ứng dụng thực tế
Sau đây là một số tình huống thực tế mà các tính năng này phát huy tác dụng:
1. **Báo cáo tài chính:** Tự động hóa và định dạng các mô hình tài chính phức tạp.
2. **Phân tích dữ liệu:** Áp dụng các tính toán tùy chỉnh để nâng cao hiểu biết về dữ liệu.
3. **Tạo tài liệu tự động:** Tạo báo cáo chuẩn để phân phối.

Các ứng dụng này chứng minh cách Aspose.Cells có thể tích hợp vào các hệ thống lớn hơn, hợp lý hóa quy trình làm việc trên nhiều ngành.

## Cân nhắc về hiệu suất
Để có hiệu suất tối ưu:
- Giảm thiểu việc sử dụng các hàm biến động trong công thức mảng.
- Tận dụng chế độ tính toán thủ công để giảm chi phí xử lý.
- Quản lý bộ nhớ Java hiệu quả bằng cách loại bỏ các đối tượng không sử dụng.

Việc thực hiện các biện pháp tốt nhất này sẽ đảm bảo ứng dụng của bạn luôn hiệu quả và phản hồi nhanh.

## Phần kết luận
Bây giờ bạn đã thành thạo việc thiết lập công thức mảng, áp dụng kiểu số, tùy chỉnh phép tính và lưu sổ làm việc bằng Aspose.Cells for Java. Những kỹ năng này giúp bạn tự động hóa các tác vụ bảng tính phức tạp một cách dễ dàng. Tiếp tục khám phá các tính năng mạnh mẽ của Aspose bằng cách truy cập [tài liệu](https://reference.aspose.com/cells/java/).

Sẵn sàng thực hiện bước tiếp theo? Hãy tìm hiểu sâu hơn về các chủ đề nâng cao hoặc tích hợp các giải pháp này vào các dự án hiện tại của bạn!

## Phần Câu hỏi thường gặp
1. **Công thức mảng trong Excel là gì?**
   - Công thức mảng thực hiện nhiều phép tính trên một hoặc nhiều mục trong một phạm vi.
2. **Làm thế nào để áp dụng kiểu số bằng Aspose.Cells?**
   - Sử dụng `setNumber` phương pháp trên đối tượng kiểu của ô để định dạng nó.
3. **Tôi có thể tùy chỉnh logic tính toán bằng Aspose.Cells không?**
   - Có, bằng cách thiết lập các chức năng tùy chỉnh và sử dụng `CalculationOptions`.
4. **Lợi ích của chế độ tính toán thủ công là gì?**
   - Nó nâng cao hiệu suất bằng cách ngăn chặn những tính toán lại không cần thiết.
5. **Làm thế nào để lưu bảng tính dưới dạng PDF bằng Aspose.Cells?**
   - Sử dụng `save` phương pháp với phần mở rộng tập tin thích hợp (`.pdf`).

## Tài nguyên
- [Tài liệu Aspose.Cells](https://reference.aspose.com/cells/java/)
- [Tải xuống Aspose.Cells cho Java](https://releases.aspose.com/cells/java/)
- [Mua giấy phép](https://purchase.aspose.com/pricing/aspose.cells)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}