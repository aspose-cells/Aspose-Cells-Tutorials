---
date: '2026-10-28'
description: Tìm hiểu cách dán giá trị bằng tùy chọn sao chép và dán của Aspose.Cells
  trong Java, kèm mã từng bước, cấu hình phụ thuộc Maven và mẹo cấp phép.
keywords:
- how to paste values
- aspose cells maven dependency
- java generate excel report
- aspose cells license java
- copyoptions refertodestinationsheet
lastmod: '2026-10-28'
og_description: Tìm hiểu cách dán giá trị bằng tùy chọn sao chép và dán của Aspose.Cells
  trong Java, kèm mã từng bước, cấu hình phụ thuộc Maven và mẹo cấp phép.
og_image_alt: Developer guide showing Java code for copying and pasting Excel data
  with Aspose.Cells
og_title: Cách dán giá trị bằng tùy chọn sao chép và dán của Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to paste values using Aspose.Cells copy and paste options
    in Java, with step‑by‑step code, Maven dependency setup, and licensing tips.
  headline: How to paste values with Aspose.Cells copy and paste options
  type: TechArticle
- questions:
  - answer: It rewrites formula references so they point to the destination sheet
      after a copy, ensuring reporting formulas stay correct.
    question: What is `CopyOptions.ReferToDestinationSheet` used for?
  - answer: Set `PasteOptions.setOnlyVisibleCells(true)` and choose `PasteType.VALUES`.
    question: How do I paste only visible cells?
  - answer: Yes, a free trial or temporary license is available for evaluation, but
      a permanent license is required for production.
    question: Can I use Aspose.Cells without purchasing a license?
  - answer: Double‑check that `ReferToDestinationSheet` is enabled **before** the
      copy operation and that the source formulas don’t contain external workbook
      links.
    question: Why are some references still wrong after copying?
  - answer: Dispose of `Workbook` objects when finished, process large files in chunks,
      and monitor JVM heap usage.
    question: What memory‑management best practices should I follow?
  type: FAQPage
tags:
- paste values
- Aspose.Cells
- Java Excel automation
- copy options
- paste options
title: Cách dán giá trị bằng tùy chọn sao chép và dán của Aspose.Cells
url: /vi/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách dán giá trị với các tùy chọn sao chép và dán của Aspose.Cells

Tự động hoá báo cáo Excel trong Java có nghĩa là bạn có thể tạo, hợp nhất và định dạng các workbook mà không cần mở Excel thủ công. Với **Aspose.Cells** bạn có toàn quyền kiểm soát công thức, các hàng ẩn và giá trị ô, vì vậy báo cáo của bạn luôn chính xác và nhẹ nhàng. Trong hướng dẫn này, bạn sẽ học cách sử dụng **CopyOptions.ReferToDestinationSheet** để giữ công thức đúng và **PasteOptions** để dán chỉ các giá trị hiển thị mà bạn cần.

## Câu trả lời nhanh
- **CopyOptions.ReferToDestinationSheet` làm gì?** Nó ghi lại các công thức để chúng trỏ tới sheet đích sau khi thực hiện sao chép.  
- **Làm thế nào để dán chỉ các ô hiển thị?** Gọi `PasteOptions.setOnlyVisibleCells(true)` cùng với `PasteType.VALUES`.  
- **Phiên bản thư viện yêu cầu là gì?** Aspose.Cells 25.3 hoặc mới hơn.  
- **Tôi có cần giấy phép cho môi trường sản xuất không?** Có – giấy phép vĩnh viễn hoặc tạm thời sẽ loại bỏ các giới hạn đánh giá.  
- **Tôi có thể sử dụng Maven hoặc Gradle không?** Cả hai đều được hỗ trợ; xem các đoạn mã phụ thuộc bên dưới.

## “Tự động hoá báo cáo Excel” là gì?
Tự động hoá báo cáo Excel có nghĩa là tạo và cập nhật các workbook Excel một cách lập trình, cho phép bạn tạo, hợp nhất và định dạng báo cáo mà không cần sao chép‑dán thủ công, giúp giảm lỗi và tiết kiệm hàng giờ công việc lặp đi lặp lại. Cách tiếp cận này lý tưởng cho các công việc batch theo lịch, bảng điều khiển dựa trên dữ liệu và các quy trình hợp nhất tài chính.

## Tại sao nên sử dụng CopyOptions và PasteOptions cho báo cáo?
Hai lớp này cho phép bạn giữ nguyên các tham chiếu công thức khi sao chép dữ liệu **và** chỉ trích xuất các ô hiển thị sau khi lọc hoặc ẩn hàng. Sử dụng chúng cùng nhau giảm lượng dữ liệu truyền lên tới 80 % trong các kịch bản bảng đã lọc điển hình và đảm bảo các công thức vẫn tính toán đúng trong sheet đích.

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
- **Bản dùng thử miễn phí** – đầy đủ tính năng để đánh giá.  
- **Giấy phép tạm thời** – loại bỏ các giới hạn bản dùng thử trong khi bạn thử nghiệm.  
- **Giấy phép vĩnh viễn** – được khuyến nghị cho các tải công việc sản xuất.

Khởi tạo Aspose.Cells trong mã Java của bạn:  
```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Hướng dẫn từng bước

### 1. copyOptions với referToDestinationSheet

#### Tổng quan
`CopyOptions` là đối tượng cấu hình của Aspose.Cells, điều khiển cách các công thức và tham chiếu ô được xử lý trong quá trình sao chép. Đặt `CopyOptions.ReferToDestinationSheet` thành `true` sẽ ghi lại các tham chiếu công thức để chúng trỏ tới sheet mới sau khi sao chép.

#### Bước 1: khởi tạo workbook và worksheets  
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Bước 2: cấu hình copyOptions  
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Bước 3: thực hiện thao tác sao chép  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Tiêu đề quan trọng*: Các công thức ban đầu tham chiếu `Sheet1` bây giờ sẽ đúng tham chiếu `DestSheet`, giữ cho các báo cáo tự động của bạn đáng tin cậy.

**Mẹo khắc phục**: Nếu các công thức vẫn tham chiếu sheet cũ, hãy đảm bảo `setReferToDestinationSheet(true)` được gọi **trước** khi sao chép.

### 2. pasteOptions cho chỉ giá trị từ các ô hiển thị

#### Tổng quan
`PasteOptions` là đối tượng cài đặt của Aspose.Cells, xác định những gì sẽ được dán. Sử dụng `PasteType.VALUES` cùng với `onlyVisibleCells=true` sẽ sao chép chỉ các giá trị hiển thị, bỏ qua các hàng/cột ẩn và định dạng.

#### Bước 1: khởi tạo workbook và worksheets  
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Bước 2: cấu hình pasteOptions  
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Bước 3: thực hiện thao tác dán  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Tiêu đề quan trọng*: Lý tưởng để trích xuất dữ liệu đã lọc hoặc tạo báo cáo sạch sẽ mà không có các hàng ẩn hoặc nhiễu định dạng.

**Mẹo khắc phục**: Kiểm tra rằng các hàng/cột thực sự đã bị ẩn trong Excel trước khi sao chép; nếu không, chúng sẽ được bao gồm.

## Ứng dụng thực tế
1. **Hợp nhất tài chính** – hợp nhất các sheet hàng tháng vào một workbook chính trong khi giữ mọi công thức chính xác.  
2. **Xuất dữ liệu đã lọc** – chỉ lấy các hàng hiển thị từ bảng đã lọc vào sheet tóm tắt.  
3. **Tạo báo cáo theo lịch** – tự động tạo báo cáo Excel hàng đêm với các giá trị ô chính xác và tham chiếu đúng.

## Các cân nhắc về hiệu năng
- **Giải phóng workbook** khi hoàn thành (`wb.dispose();`) để giải phóng tài nguyên gốc.  
- **Thao tác batch** – nhóm nhiều lệnh sao chép/dán để giảm chi phí.  
- **Giám sát bộ nhớ** – workbook lớn có thể cần tăng heap (`-Xmx2g`).  
- Aspose.Cells hỗ trợ **hơn 50 định dạng nhập và xuất** và có thể xử lý workbook với **lên tới 2 triệu hàng** mà không cần tải toàn bộ tệp vào bộ nhớ, mang lại hiệu năng cao cho các tải công việc doanh nghiệp.

## Câu hỏi thường gặp

**Q: `CopyOptions.ReferToDestinationSheet` được dùng để làm gì?**  
A: Nó ghi lại các tham chiếu công thức để chúng trỏ tới sheet đích sau khi sao chép, đảm bảo các công thức báo cáo vẫn đúng.

**Q: Làm sao để dán chỉ các ô hiển thị?**  
A: Đặt `PasteOptions.setOnlyVisibleCells(true)` và chọn `PasteType.VALUES`.

**Q: Tôi có thể sử dụng Aspose.Cells mà không mua giấy phép không?**  
A: Có, bản dùng thử miễn phí hoặc giấy phép tạm thời có sẵn để đánh giá, nhưng giấy phép vĩnh viễn là bắt buộc cho môi trường sản xuất.

**Q: Tại sao một số tham chiếu vẫn sai sau khi sao chép?**  
A: Kiểm tra lại rằng `ReferToDestinationSheet` đã được bật **trước** khi sao chép và các công thức nguồn không chứa liên kết tới workbook bên ngoài.

**Q: Tôi nên tuân thủ những thực hành quản lý bộ nhớ nào?**  
A: Giải phóng các đối tượng `Workbook` khi xong, xử lý các tệp lớn theo từng phần, và giám sát việc sử dụng heap của JVM.

**Q: Có thể kết hợp CopyOptions và PasteOptions trong một thao tác không?**  
A: Có, bạn có thể nối chúng bằng cách sao chép đầu tiên với `CopyOptions` rồi áp dụng `PasteOptions` lên vùng đích.

## Tài nguyên
- **Tài liệu**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Tải xuống**: [Aspose.Cells releases for Java](https://releases.aspose.com/cells/java/)  
- **Mua**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Bản dùng thử miễn phí**: [Aspose.Cells free trial](https://releases.aspose.com/cells/java/)  
- **Giấy phép tạm thời**: [Apply for a temporary license](https://purchase.aspose.com/temporary-license/)  
- **Diễn đàn hỗ trợ**: [Aspose support](https://forum.aspose.com/c/cells)

---

**Cập nhật lần cuối:** 2026-10-28  
**Kiểm tra với:** Aspose.Cells 25.3 for Java  
**Tác giả:** Aspose

## Hướng dẫn liên quan

- [Đọc tệp Excel Java – Thao tác ô Workbook nâng cao với Aspose.Cells](/cells/java/cell-operations/aspose-cells-java-workbook-cell-manipulation/)
- [Thêm dữ liệu vào ô trong Excel bằng Aspose.Cells cho Java](/cells/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Chuyển đổi chỉ số hàng cột ô Excel với Aspose.Cells Java](/cells/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}