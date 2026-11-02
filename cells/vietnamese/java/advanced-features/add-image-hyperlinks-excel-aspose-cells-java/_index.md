---
date: '2026-09-02'
description: Tìm hiểu cách tạo sổ làm việc Excel với hình ảnh có thể nhấp bằng Aspose.Cells
  cho Java, thêm siêu liên kết vào hình ảnh để có bảng tính tương tác.
keywords:
- create clickable image
- add image hyperlink
- add hyperlink to picture
- interactive excel spreadsheet
- how to add hyperlink
lastmod: '2026-09-02'
og_description: Tìm hiểu cách tạo sổ làm việc Excel với hình ảnh có thể nhấp bằng
  Aspose.Cells cho Java, thêm siêu liên kết, chú giải màn hình và tối ưu hiệu năng
  chỉ trong vài dòng mã.
og_image_alt: 'Developer guide: create clickable image Excel using Aspose.Cells for
  Java'
og_title: Tạo hình ảnh có thể nhấp trong Excel bằng Aspose.Cells cho Java
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create clickable image Excel workbooks with Aspose.Cells
    for Java, adding hyperlinks to pictures for interactive spreadsheets.
  headline: Create clickable image Excel using Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create clickable image Excel workbooks with Aspose.Cells
    for Java, adding hyperlinks to pictures for interactive spreadsheets.
  name: Create clickable image Excel using Aspose.Cells for Java
  steps:
  - name: prepare your workbook
    text: We start by creating a new workbook and selecting the first sheet.
  - name: insert a label and adjust cell size
    text: Add a descriptive label and give the cell enough space for the picture.
  - name: add the image
    text: '`Picture` represents an image object placed on a worksheet. *Tip*: Replace
      `"path/to/aspose-logo.jpg"` with the actual path to your image file.'
  - name: configure placement and add the hyperlink
    text: '`Hyperlink` defines a link associated with a cell, shape, or picture, enabling
      navigation when clicked.'
  - name: set a screen tip and save the workbook
    text: Provide a helpful tooltip and write the workbook to disk.
  type: HowTo
- questions:
  - answer: Aspose.Cells for Java.
    question: What library is required?
  - answer: Yes – the API works with both .xls and .xlsx.
    question: Can I use .xlsx files?
  - answer: A trial works for evaluation; a permanent license is required for production.
    question: Do I need a license?
  - answer: About 20 lines to add a clickable image.
    question: How many lines of code?
  - answer: Workbook objects are not thread‑safe; create separate instances per thread.
    question: Is it thread‑safe?
  type: FAQPage
tags:
- create clickable image
- Aspose.Cells
- Java Excel automation
title: Tạo hình ảnh có thể nhấp trong Excel bằng Aspose.Cells cho Java
url: /vi/java/advanced-features/add-image-hyperlinks-excel-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo hình ảnh Excel có thể nhấp chuột bằng Aspose.Cells cho Java

## Giới thiệu

Nếu bạn muốn **tạo hình ảnh Excel có thể nhấp chuột** trong các workbook cho phép người dùng chuyển đến các trang web, tài liệu hoặc các tài nguyên khác chỉ bằng một cú nhấp, bạn đã đến đúng nơi. Trong hướng dẫn này, chúng tôi sẽ trình bày cách Aspose.Cells cho Java cho phép bạn **thêm đối tượng hình ảnh Excel có siêu liên kết**, cấu hình mẹo hiển thị, và giữ cho bảng tính của bạn vừa đẹp mắt vừa chức năng.

### Những gì bạn sẽ học
- Khởi tạo một workbook Aspose.Cells trong Java.  
- Chèn một hình ảnh và biến nó thành siêu liên kết có thể nhấp.  
- Các phương thức chính như `addHyperlink`, `setPlacement` và `setScreenTip`.  
- Các thực tiễn tốt nhất về hiệu suất và giấy phép.

## Câu trả lời nhanh
- **Thư viện cần thiết là gì?** Aspose.Cells cho Java.  
- **Tôi có thể sử dụng tệp .xlsx không?** Có – API hoạt động với cả .xls và .xlsx.  
- **Tôi có cần giấy phép không?** Bản dùng thử hoạt động để đánh giá; giấy phép vĩnh viễn cần thiết cho môi trường sản xuất.  
- **Bao nhiêu dòng mã?** Khoảng 20 dòng để thêm một hình ảnh có thể nhấp.  
- **Có an toàn với đa luồng không?** Các đối tượng Workbook không an toàn với đa luồng; tạo các thể hiện riêng cho mỗi luồng.  
- **Tôi có thể thêm mẹo hiển thị trong Excel không?** Có – sử dụng `Hyperlink.setScreenTip()` để hiển thị văn bản trợ giúp khi di chuột.

## Cách tạo hình ảnh Excel có thể nhấp chuột với Aspose.Cells cho Java

Bạn tạo một workbook Excel có thể nhấp chuột bằng cách tải hoặc tạo một `Workbook`, chèn một đối tượng `Picture`, gắn một `Hyperlink` vào hình ảnh đó, tùy chọn thiết lập mẹo hiển thị, và cuối cùng lưu tệp. API xử lý tất cả XML Excel cấp thấp, vì vậy bạn chỉ cần viết một vài dòng mã Java đơn giản.

### Yêu cầu trước
Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

- **Aspose.Cells cho Java** (v25.3 trở lên).  
- **JDK 8+** đã được cài đặt.  
- Một IDE (IntelliJ IDEA, Eclipse hoặc NetBeans) và Maven hoặc Gradle để quản lý phụ thuộc.  

### Thư viện cần thiết
Thêm Aspose.Cells vào dự án của bạn:

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
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```  

### Cách lấy giấy phép
Aspose.Cells là phần mềm thương mại, nhưng bạn có thể bắt đầu với bản dùng thử miễn phí hoặc yêu cầu giấy phép tạm thời:

- Bản dùng thử miễn phí: Tải xuống từ [Aspose Downloads](https://releases.aspose.com/cells/java/).  
- Giấy phép tạm thời: Yêu cầu qua [Temporary License page](https://purchase.aspose.com/temporary-license/).  
- Mua: Đối với sử dụng lâu dài, truy cập [Aspose Purchase](https://purchase.aspose.com/buy).

### Khởi tạo cơ bản
Lớp `Workbook` đại diện cho toàn bộ tệp Excel trong bộ nhớ. Bạn tạo một thể hiện của nó, sau đó lấy tham chiếu tới worksheet đầu tiên. `Worksheet` đại diện cho một sheet duy nhất trong workbook.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

// Initialize workbook
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```  

## Triển khai từng bước

### Bước 1: chuẩn bị workbook của bạn
Chúng ta bắt đầu bằng việc tạo một workbook mới và chọn sheet đầu tiên.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```  

### Bước 2: chèn nhãn và điều chỉnh kích thước ô
Thêm một nhãn mô tả và cung cấp đủ không gian cho hình ảnh trong ô.

```java
worksheet.getCells().get("C2").setValue("Image Hyperlink");
worksheet.getCells().setRowHeight(3, 100); // Set row height for C4
worksheet.getCells().setColumnWidth(2, 21); // Adjust column width for C column
```  

### Bước 3: thêm hình ảnh
`Picture` đại diện cho một đối tượng hình ảnh được đặt trên worksheet.

```java
int index = worksheet.getPictures().add(3, 2, "path/to/aspose-logo.jpg");
```  
*Mẹo*: Thay thế `"path/to/aspose-logo.jpg"` bằng đường dẫn thực tế tới tệp hình ảnh của bạn.

### Bước 4: cấu hình vị trí và thêm siêu liên kết
`Hyperlink` định nghĩa một liên kết liên kết với ô, hình dạng hoặc hình ảnh, cho phép điều hướng khi được nhấp.

```java
import com.aspose.cells.Picture;
import com.aspose.cells.PlacementType;

Picture pic = worksheet.getPictures().get(index);
pic.setPlacement(PlacementType.FREE_FLOATING);

// Add hyperlink to the picture
pic.addHyperlink("http://www.aspose.com/");
```  

### Bước 5: thiết lập mẹo hiển thị và lưu workbook
Cung cấp một tooltip hữu ích và ghi workbook ra đĩa.

```java
import com.aspose.cells.Hyperlink;

Hyperlink hlink = pic.getHyperlink();
hlink.setScreenTip("Click to go to Aspose site");

workbook.save("AIHyperlinks_out.xls");
```  

## Tại sao thêm siêu liên kết vào hình ảnh Excel?

Nhúng một hình ảnh có thể nhấp cho phép bạn biến các yếu tố thương hiệu, biểu tượng hoặc sơ đồ thành các điểm điều hướng trực tiếp, giảm số lần nhấp cần thiết để đến nội dung liên quan. Cách tiếp cận này tăng hiệu quả người dùng trong các bảng điều khiển marketing, tài liệu kỹ thuật và bảng tính giáo dục.

## Cách thêm mẹo hiển thị trong Excel

Bạn thêm mẹo hiển thị bằng cách gọi `hyperlink.setScreenTip("Your tip here")` trên đối tượng `Hyperlink` được gắn vào hình ảnh. Mẹo sẽ xuất hiện khi con trỏ di chuột qua hình ảnh, cung cấp hướng dẫn ngữ cảnh cho người dùng mà không làm rối sheet.

## Mẹo khắc phục sự cố
- **Lỗi đường dẫn hình ảnh** – kiểm tra lại vị trí tệp và đảm bảo ứng dụng có quyền đọc.  
- **Giấy phép chưa được áp dụng** – nếu bản dùng thử hết hạn, các siêu liên kết có thể không hoạt động; áp dụng giấy phép hợp lệ bằng `License.setLicense`.  
- **Siêu liên kết không thể nhấp** – xác minh rằng `PlacementType` của hình ảnh được đặt thành `FREE_FLOATING`.

## Ứng dụng thực tiễn
Nhúng hình ảnh có thể nhấp hữu ích trong nhiều kịch bản:

1. **Báo cáo marketing** – liên kết logo thương hiệu tới trang sản phẩm.  
2. **Tài liệu kỹ thuật** – đính kèm sơ đồ mở các bản vẽ chi tiết.  
3. **Bảng tính giáo dục** – biến biểu tượng thành phím tắt cho video bổ sung.  
4. **Bảng điều khiển dự án** – làm cho các biểu tượng trạng thái mở các công cụ theo dõi nhiệm vụ liên quan.

## Các lưu ý về hiệu suất
- Giữ kích thước tệp hình ảnh ở mức hợp lý; hình ảnh lớn làm tăng mức sử dụng bộ nhớ của workbook.  
- Giải phóng các đối tượng không dùng (`workbook.dispose()`) khi xử lý nhiều tệp trong vòng lặp.  
- Nâng cấp lên phiên bản Aspose.Cells mới nhất để cải thiện hiệu suất và sửa lỗi.

## Kết luận
Bây giờ bạn đã biết cách thêm siêu liên kết vào hình ảnh trong Excel bằng Aspose.Cells cho Java, cho phép bạn **tạo hình ảnh Excel có thể nhấp chuột** trong các workbook phong phú và tương tác hơn. Thử nghiệm với các URL khác nhau, mẹo hiển thị và vị trí hình ảnh để phù hợp với nhu cầu báo cáo của bạn. Tiếp theo, bạn có thể khám phá việc thêm siêu liên kết vào các hình dạng hoặc tự động chèn hàng loạt hình ảnh trên nhiều worksheet.

## Câu hỏi thường gặp

**Q:** Kích thước hình ảnh tối đa được Aspose.Cells cho Java hỗ trợ là bao nhiêu?  
**A:** Không có giới hạn nghiêm ngặt, nhưng hình ảnh rất lớn có thể ảnh hưởng đến hiệu suất và làm tăng kích thước tệp.

**Q:** Tôi có thể sử dụng tính năng này với tệp .xlsx không?  
**A:** Có, API hoạt động với cả định dạng `.xls` và `.xlsx`.

**Q:** Tôi nên xử lý ngoại lệ như thế nào khi thêm siêu liên kết?  
**A:** Bao quanh mã trong khối try‑catch và ghi lại chi tiết `Exception` để chẩn đoán các vấn đề về đường dẫn hoặc giấy phép.

**Q:** Có thể xóa siêu liên kết khỏi hình ảnh sau khi đã thêm không?  
**A:** Có – lấy đối tượng `Picture` và gọi `pic.getHyperlink().remove()` hoặc xóa hình ảnh khỏi bộ sưu tập.

**Q:** Tại sao siêu liên kết của tôi có thể không hoạt động như mong đợi?  
**A:** Nguyên nhân thường gặp bao gồm chuỗi URL không đúng, thiếu tiền tố `http://`/`https://`, hoặc bản dùng thử không có giấy phép khiến một số tính năng bị vô hiệu hoá.

## Tài nguyên bổ sung
- **Tài liệu:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Tải xuống:** [Aspose Cells Release](https://releases.aspose.com/cells/java/)  
- **Mua và dùng thử:** Truy cập [Aspose Purchase](https://purchase.aspose.com/buy) hoặc [Temporary License Page](https://purchase.aspose.com/temporary-license/) để biết các tùy chọn giấy phép.  
- **Diễn đàn hỗ trợ:** Để được trợ giúp, xem [Aspose Support Forum](https://forum.aspose.com/c/cells/9).

---

**Last updated:** 2026-09-02  
**Tested with:** Aspose.Cells for Java 25.3  
**Author:** Aspose

## Hướng dẫn liên quan

- [Cách tạo siêu liên kết trong Excel bằng Aspose.Cells cho Java - Hướng dẫn từng bước](/cells/java/advanced-features/create-hyperlinks-excel-aspose-cells-java/)
- [Cách định dạng ô Excel và thêm siêu liên kết bằng Aspose.Cells cho Java](/cells/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)
- [Thêm hình ảnh vào bình luận Excel bằng Aspose.Cells cho Java: Hướng dẫn đầy đủ](/cells/java/comments-annotations/add-image-excel-comment-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}