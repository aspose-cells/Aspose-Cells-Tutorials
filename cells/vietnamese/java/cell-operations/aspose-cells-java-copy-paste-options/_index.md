---
date: '2026-02-22'
description: Tìm hiểu cách tự động hoá báo cáo Excel với Aspose.Cells trong Java bằng
  cách sử dụng CopyOptions và PasteOptions để giữ công thức chính xác và chỉ dán các
  giá trị hiển thị.
keywords:
- Aspose.Cells Java
- CopyOptions ReferToDestinationSheet
- PasteOptions Excel
title: Tự động hoá báo cáo Excel – Làm chủ CopyOptions & PasteOptions trong Java với
  Aspose.Cells
url: /vi/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

 produce final answer.{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tự động tạo báo cáo Excel với Aspose.Cells: CopyOptions & PasteOptions trong Java

Bạn có muốn **tự động tạo báo cáo Excel** bằng Java không? Với Aspose.Cells, bạn có thể sao chép, dán và điều chỉnh công thức một cách lập trình để báo cáo của bạn luôn chính xác và chỉ truyền dữ liệu bạn cần. Trong hướng dẫn này, chúng tôi sẽ trình bày hai tính năng quan trọng—**CopyOptions.ReferToDestinationSheet** và **PasteOptions**—giúp bạn giữ nguyên tham chiếu công thức và dán giá trị chỉ từ các ô hiển thị.

## Câu trả lời nhanh
- **`CopyOptions.ReferToDestinationSheet` làm gì?** Điều chỉnh công thức để trỏ tới sheet đích khi sao chép dữ liệu.  
- **Làm sao để dán chỉ các ô hiển thị?** Đặt `PasteOptions.setOnlyVisibleCells(true)` cùng với `PasteType.VALUES`.  
- **Phiên bản thư viện nào được yêu cầu?** Aspose.Cells 25.3 trở lên.  
- **Có cần giấy phép cho môi trường production không?** Có, giấy phép vĩnh viễn hoặc tạm thời sẽ loại bỏ các giới hạn đánh giá.  
- **Có thể sử dụng Maven hoặc Gradle không?** Cả hai đều được hỗ trợ; xem các đoạn mã phụ thuộc bên dưới.

## “Tự động tạo báo cáo Excel” là gì?
Tự động tạo báo cáo Excel có nghĩa là tạo, hợp nhất và định dạng các workbook Excel một cách lập trình, loại bỏ các bước sao chép‑dán thủ công và giảm thiểu lỗi. Aspose.Cells cung cấp một API phong phú cho phép các nhà phát triển Java thao tác với bảng tính ở quy mô lớn.

## Tại sao nên sử dụng CopyOptions và PasteOptions cho việc báo cáo?
- **Duy trì tính toàn vẹn của công thức** khi di chuyển dữ liệu giữa các sheet.  
- **Loại bỏ các hàng/cột ẩn** để báo cáo luôn sạch sẽ và tập trung.  
- **Tăng hiệu năng** bằng cách sao chép chỉ dữ liệu cần thiết thay vì toàn bộ phạm vi.

## Yêu cầu trước
- Java 8 hoặc cao hơn.  
- Maven hoặc Gradle để quản lý phụ thuộc.  
- Aspose.Cells 25.3+ (bản dùng thử, giấy phép tạm thời hoặc vĩnh viễn).

## Cài đặt Aspose.Cells cho Java

Thêm thư viện vào dự án của bạn bằng một trong các cách sau:

**Maven**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**  
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Nhận giấy phép
- **Bản dùng thử miễn phí** – Tính năng đầy đủ để đánh giá.  
- **Giấy phép tạm thời** – Loại bỏ các hạn chế của bản dùng thử trong quá trình thử nghiệm.  
- **Giấy phép vĩnh viễn** – Được khuyến nghị cho môi trường sản xuất.

Khởi tạo Aspose.Cells trong mã Java của bạn:

```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Hướng dẫn từng bước

### 1. CopyOptions với ReferToDestinationSheet

#### Tổng quan
Đặt `CopyOptions.ReferToDestinationSheet` thành `true` sẽ ghi lại lại các tham chiếu công thức sao cho chúng trỏ tới sheet mới sau khi thực hiện sao chép.

#### Bước 1: Khởi tạo Workbook và Worksheets  
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Bước 2: Cấu hình CopyOptions  
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Bước 3: Thực hiện thao tác sao chép  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```

*Why this matters*: Các công thức ban đầu tham chiếu `Sheet1` sẽ bây giờ đúng tham chiếu `DestSheet`, giúp các báo cáo tự động của bạn luôn đáng tin cậy.  
**Mẹo khắc phục**: Nếu công thức vẫn còn tham chiếu sheet cũ, hãy chắc chắn rằng `setReferToDestinationSheet(true)` được gọi **trước** khi sao chép.

### 2. PasteOptions cho chỉ giá trị từ các ô hiển thị

#### Tổng quan
`PasteOptions` cho phép bạn xác định những gì sẽ được dán. Sử dụng `PasteType.VALUES` kết hợp với `onlyVisibleCells=true` sẽ sao chép chỉ các giá trị hiển thị, bỏ qua các hàng/cột ẩn và định dạng.

#### Bước 1: Khởi tạo Workbook và Worksheets  
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Bước 2: Cấu hình PasteOptions  
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Bước 3: Thực hiện thao tác dán  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```

*Why this matters*: Thích hợp để trích xuất dữ liệu đã lọc hoặc tạo báo cáo sạch sẽ mà không có các hàng ẩn hoặc nhiễu định dạng.  
**Mẹo khắc phục**: Kiểm tra rằng các hàng/cột thực sự đã bị ẩn trong Excel trước khi sao chép; nếu không, chúng sẽ được bao gồm.

## Ứng dụng thực tế
1. **Hợp nhất tài chính** – Gộp các sheet hàng tháng vào một workbook chính trong khi giữ mọi công thức luôn chính xác.  
2. **Xuất dữ liệu đã lọc** – Lấy chỉ các hàng hiển thị từ một bảng đã lọc vào sheet tóm tắt.  
3. **Tạo báo cáo theo lịch trình** – Tự động tạo báo cáo Excel hàng đêm với các giá trị ô chính xác và tham chiếu đúng.

## Các cân nhắc về hiệu năng
- **Giải phóng Workbook** khi hoàn thành (`wb.dispose();`) để giải phóng tài nguyên gốc.  
- **Thao tác batch** – Nhóm nhiều lệnh sao chép/dán lại để giảm tải.  
- **Giám sát bộ nhớ** – Các workbook lớn có thể cần tăng heap (`-Xmx2g`).

## Câu hỏi thường gặp

**Q1: `CopyOptions.ReferToDestinationSheet` được dùng để làm gì?**  
A: Nó ghi lại các tham chiếu công thức sao cho chúng trỏ tới sheet đích sau khi sao chép, đảm bảo các công thức báo cáo luôn đúng.

**Q2: Làm sao để dán chỉ các ô hiển thị?**  
A: Đặt `PasteOptions.setOnlyVisibleCells(true)` và chọn `PasteType.VALUES`.

**Q3: Có thể sử dụng Aspose.Cells mà không mua giấy phép không?**  
A: Có, bản dùng thử miễn phí hoặc giấy phép tạm thời có sẵn để đánh giá, nhưng giấy phép vĩnh viễn là bắt buộc cho môi trường production.

**Q4: Tại sao một số tham chiếu vẫn sai sau khi sao chép?**  
A: Kiểm tra lại rằng `ReferToDestinationSheet` đã được bật **trước** khi thực hiện sao chép và các công thức nguồn không chứa liên kết tới workbook bên ngoài.

**Q5: Những thực hành tốt nào về quản lý bộ nhớ nên tuân theo?**  
A: Giải phóng các đối tượng `Workbook` khi hoàn tất, xử lý các tệp lớn theo từng phần, và giám sát việc sử dụng heap của JVM.

**Q6: Có thể kết hợp CopyOptions và PasteOptions trong một thao tác không?**  
A: Có, bạn có thể chuỗi chúng lại bằng cách sao chép trước với `CopyOptions` rồi áp dụng `PasteOptions` lên phạm vi đích.

## Tài nguyên
- **Tài liệu**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Tải xuống**: [Aspose.Cells Releases for Java](https://releases.aspose.com/cells/java/)  
- **Mua**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Bản dùng thử miễn phí**: [Aspose.Cells Free Trial](https://releases.aspose.com/cells/java/)  
- **Giấy phép tạm thời**: [Apply for a Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Diễn đàn hỗ trợ**: [Aspose Support](https://forum.aspose.com/c/cells)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Cập nhật lần cuối:** 2026-02-22  
**Kiểm tra với:** Aspose.Cells 25.3 for Java  
**Tác giả:** Aspose