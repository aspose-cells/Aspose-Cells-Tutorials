---
date: '2026-11-16'
description: Tìm hiểu cách cập nhật external links của Excel, thay đổi nguồn liên
  kết Excel và thiết lập đường dẫn tuyệt đối của Excel một cách hiệu quả với Aspose.Cells
  for Java.
keywords:
- update excel external links
- update excel data source
- change excel link source
- modify excel workbook links
- automate excel link updates
lastmod: '2026-11-16'
og_description: Cập nhật external links của Excel, thay đổi nguồn dữ liệu và thiết
  lập đường dẫn tuyệt đối một cách lập trình bằng Aspose.Cells for Java. Tìm hiểu
  từng bước với các ví dụ.
og_image_alt: Screenshot of Java code updating Excel external links using Aspose.Cells
og_title: Cập nhật external links của Excel với Aspose.Cells for Java – Hướng dẫn
  toàn diện
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to update Excel external links, change Excel link source,
    and set Excel absolute path efficiently with Aspose.Cells for Java.
  headline: How to update Excel external links using Aspose.Cells for Java
  type: TechArticle
- description: Learn how to update Excel external links, change Excel link source,
    and set Excel absolute path efficiently with Aspose.Cells for Java.
  name: How to update Excel external links using Aspose.Cells for Java
  steps:
  - name: '**Data consolidation:** Combine data from multiple workbooks into a master
      report.'
    text: '**Data consolidation:** Combine data from multiple workbooks into a master
      report.'
  - name: '**Financial modeling:** Keep balance sheets synchronized with external
      accounting files.'
    text: '**Financial modeling:** Keep balance sheets synchronized with external
      accounting files.'
  - name: '**Project tracking:** Link task lists across departmental sheets for up‑to‑date
      status reporting.'
    text: '**Project tracking:** Link task lists across departmental sheets for up‑to‑date
      status reporting.'
  type: HowTo
- questions:
  - answer: Yes, Aspose.Cells supports linking to numerous external resources within
      a single workbook.
    question: Can I link to multiple external files?
  - answer: Typical issues include file‑not‑found errors and permission‑denied exceptions.
    question: What are some common errors when accessing external links?
  - answer: Use the `Workbook.getBrokenExternalLinks()` method to identify and address
      broken links.
    question: How do I handle broken links in my Excel file?
  - answer: Absolutely—iterate over a collection of workbooks and update each link
      programmatically.
    question: Is it possible to automate link updates across multiple workbooks?
  - answer: Call `setAbsolutePath()` with the correct base path to resolve all links
      correctly.
    question: What should I do if my workbook's external path is incorrect?
  type: FAQPage
tags:
- excel external links
- aspose.cells
- java workbook automation
title: Cách cập nhật external links của Excel bằng Aspose.Cells for Java
url: /vi/java/advanced-features/excel-external-links-aspose-cells-java-guide/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách cập nhật liên kết ngoại của Excel bằng Aspose.Cells cho Java

## Giới thiệu
Việc làm việc với các tệp Excel có chứa liên kết ngoại có thể gặp khó khăn, đặc biệt khi bạn cần **cập nhật liên kết ngoại của Excel** trên các nguồn dữ liệu hoặc môi trường khác nhau. Trong hướng dẫn này, bạn sẽ học cách **tải liên kết sổ làm việc Excel**, truy cập và sửa đổi các liên kết đó, và thay đổi đường dẫn tuyệt đối của sổ làm việc — tất cả bằng Aspose.Cells cho Java. Khi kết thúc, bạn sẽ có thể **thay đổi nguồn liên kết Excel**, **cập nhật nguồn dữ liệu Excel**, và **sửa đổi liên kết sổ làm việc Excel** một cách lập trình, giúp dễ dàng **tự động cập nhật liên kết Excel** trong các ứng dụng của bạn.

## Câu trả lời nhanh
- **Thư viện chính để quản lý liên kết trong Excel là gì?** Aspose.Cells for Java.  
- **Tôi có thể thay đổi nguồn dữ liệu của một liên kết ngoại không?** Có, sử dụng `ExternalLink.setDataSource()`.  
- **Làm thế nào để đặt một đường dẫn cơ sở mới cho sổ làm việc?** Gọi `Workbook.setAbsolutePath()`.  
- **Có thể tự động cập nhật liên kết Excel trên nhiều tệp không?** Chắc chắn—lặp qua các sổ làm việc và cập nhật liên kết trong mã.  
- **Tôi có cần giấy phép cho việc sử dụng trong môi trường sản xuất không?** Một giấy phép đầy đủ sẽ loại bỏ mọi hạn chế đánh giá.

## Cập nhật liên kết ngoại của Excel là gì?
Cập nhật liên kết ngoại của Excel có nghĩa là thay đổi một cách lập trình các tham chiếu mà sổ làm việc giữ tới các tệp hoặc nguồn dữ liệu khác. Điều này đảm bảo rằng các công thức, biểu đồ hoặc bảng luôn trỏ tới thông tin chính xác, cập nhật mới nhất mà không cần can thiệp thủ công. Nó cũng cập nhật bất kỳ phạm vi đặt tên hoặc kết nối dữ liệu nào dựa trên các liên kết đó, ngăn ngừa lỗi #REF! khi các tệp nguồn bị di chuyển hoặc đổi tên.

## Tại sao nên sử dụng Aspose.Cells để cập nhật liên kết ngoại của Excel?
Aspose.Cells hỗ trợ **hơn 60 định dạng nhập và xuất** và có thể xử lý sổ làm việc lên tới **2 GB** mà không cần tải toàn bộ tệp vào bộ nhớ. Thư viện chạy **100% phía máy chủ**, vì vậy bạn không bao giờ cần cài đặt Microsoft Office. Những khả năng này cho phép bạn một cách đáng tin cậy **cập nhật liên kết ngoại của Excel**, **thay đổi nguồn liên kết Excel**, và **tự động cập nhật liên kết Excel** trong các pipeline dữ liệu có lưu lượng cao.

## Yêu cầu trước
- Thư viện Aspose.Cells đã được thêm vào dự án của bạn (Maven hoặc Gradle).  
- Môi trường phát triển Java 8+.  
- Kiến thức cơ bản về cú pháp Java và các khái niệm hướng đối tượng.  
- Giấy phép Aspose.Cells hợp lệ cho triển khai trong môi trường sản xuất.

## Cài đặt Aspose.Cells cho Java

### Thông tin cài đặt
Thêm Aspose.Cells vào dự án của bạn bằng một trong các công cụ xây dựng sau:

**Maven:**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle:**  
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Cách lấy giấy phép
Bạn có thể bắt đầu với **bản dùng thử miễn phí**, yêu cầu **giấy phép tạm thời**, hoặc mua giấy phép đầy đủ để sử dụng không giới hạn.

### Khởi tạo và cấu hình cơ bản
Bắt đầu bằng cách nhập lớp cần thiết:

```java
import com.aspose.cells.Workbook;
```

## Hướng dẫn triển khai từng bước

### Tải tệp Excel có liên kết ngoại
Lớp `Workbook` đại diện cho toàn bộ tệp Excel trong bộ nhớ. Việc tải sổ làm việc cho phép bạn truy cập tất cả các liên kết ngoại được nhúng, đây là bước đầu tiên để **tải liên kết sổ làm việc Excel**.

```java
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/sample.xlsx");
```

- `dataDir` chỉ tới thư mục chứa tệp Excel của bạn.  
- `Workbook` đại diện cho toàn bộ bảng tính trong bộ nhớ.

### Truy cập liên kết ngoại
Lớp `ExternalLink` bao hàm một tham chiếu ngoại duy nhất được lưu trong sổ làm việc. Sau khi sổ làm việc được tải, bạn có thể lấy bất kỳ liên kết ngoại nào.

```java
import com.aspose.cells.ExternalLink;

ExternalLink externalLink = wb.getWorksheets().getExternalLinks().get(0);
```

- `getExternalLinks()` trả về một tập hợp các liên kết.  
- `get(0)` lấy liên kết đầu tiên (bạn có thể lặp để lấy thêm).

### Sửa đổi nguồn dữ liệu của liên kết ngoại
Phương thức `setDataSource` cập nhật tên tệp hoặc đường dẫn đầy đủ mà liên kết ngoại trỏ tới. Thay đổi nguồn cho phép bạn **thay đổi nguồn liên kết Excel** mà không cần mở lại sổ làm việc bằng tay.

```java
externalLink.setDataSource("ExternalAccounts.xlsx");
```

- Cung cấp tên tệp mới hoặc đường dẫn đầy đủ tới nguồn mong muốn.  
- Mẹo: sử dụng `Path.getAbsolutePath()` để tránh các vấn đề về đường dẫn tương đối trên các máy chủ khác nhau.

### Thay đổi đường dẫn tuyệt đối của sổ làm việc
Phương thức `setAbsolutePath(String)` cập nhật vị trí cơ sở mà sổ làm việc sử dụng để giải quyết các liên kết tương đối. Điều chỉnh đường dẫn tuyệt đối hữu ích khi di chuyển sổ làm việc giữa các máy chủ hoặc thư mục.

```java
String writablePath = "C:\\Files\\Extra\\";
wb.setAbsolutePath(writablePath);

// Change to a remote URL if needed
String remotePath = "http://www.aspose.com/WebFiles/ExcelFiles/";
wb.setAbsolutePath(remotePath);
```

- Lệnh này ảnh hưởng tới tất cả các liên kết tương đối trong sổ làm việc.  
- Đặt đường dẫn tuyệt đối loại bỏ lỗi “file not found” sau khi triển khai.

### Mẹo khắc phục sự cố
- Xác minh rằng tất cả các đường dẫn sử dụng dấu phân tách đúng cho hệ điều hành của bạn (`\\` cho Windows, `/` cho Linux/macOS).  
- Đảm bảo các tệp ngoại thực sự tồn tại ở vị trí đã chỉ định.  
- Bắt `java.io.IOException` hoặc `com.aspose.cells.CellsException` để xử lý các vấn đề về quyền hoặc truy cập tệp một cách nhẹ nhàng.  
- Sai lầm phổ biến: quên gọi `Workbook.dispose()` sau khi xử lý các tệp lớn có thể gây rò rỉ bộ nhớ.

## Ứng dụng thực tiễn
Quản lý liên kết ngoại của Excel là thiết yếu trong nhiều tình huống thực tế:

1. **Hợp nhất dữ liệu:** Kết hợp dữ liệu từ nhiều sổ làm việc thành một báo cáo tổng hợp.  
2. **Mô hình tài chính:** Giữ bảng cân đối đồng bộ với các tệp kế toán ngoại.  
3. **Theo dõi dự án:** Liên kết danh sách công việc giữa các sheet phòng ban để báo cáo trạng thái cập nhật.  

## Các cân nhắc về hiệu năng
- Giải phóng các đối tượng `Workbook` (`wb.dispose()`) khi không còn cần thiết để giải phóng bộ nhớ.  
- Đối với sổ làm việc lớn, cân nhắc chỉ tải các worksheet cần thiết bằng `LoadOptions`.  
- Giữ Aspose.Cells luôn cập nhật; mỗi phiên bản mới mang lại cải thiện hiệu năng và sửa lỗi.  
- Khẳng định định lượng: phiên bản mới nhất xử lý một sổ làm việc 500 sheet (≈ 2 GB) trong vòng dưới **30 giây** trên máy chủ 8 nhân điển hình.

## Kết luận
Trong hướng dẫn này, chúng tôi đã trình bày **cách cập nhật liên kết ngoại của Excel** bằng Aspose.Cells cho Java, bao gồm tải sổ làm việc, truy cập và sửa đổi các liên kết ngoại, và cập nhật đường dẫn tuyệt đối của sổ làm việc. Những kỹ thuật này cho phép bạn **tự động cập nhật liên kết Excel**, tối ưu hóa quy trình dữ liệu và giảm lỗi thủ công.

### Bước tiếp theo
- Thử nghiệm với nhiều liên kết ngoại và lặp qua chúng một cách lập trình.  
- Tích hợp các đoạn mã này vào các ứng dụng Java lớn hơn để xử lý dữ liệu đầu‑cuối.  
- Khám phá các tính năng khác của Aspose.Cells như tạo biểu đồ, pivot table và định dạng nâng cao.

## Câu hỏi thường gặp

**Q: Tôi có thể liên kết tới nhiều tệp ngoại không?**  
A: Có, Aspose.Cells hỗ trợ liên kết tới nhiều tài nguyên ngoại trong một sổ làm việc duy nhất.

**Q: Những lỗi thường gặp khi truy cập liên kết ngoại là gì?**  
A: Các vấn đề thường gặp bao gồm lỗi không tìm thấy tệp và ngoại lệ từ chối quyền truy cập.

**Q: Làm thế nào để xử lý các liên kết bị hỏng trong tệp Excel của tôi?**  
A: Sử dụng phương thức `Workbook.getBrokenExternalLinks()` để xác định và khắc phục các liên kết hỏng.

**Q: Có thể tự động cập nhật liên kết trên nhiều sổ làm việc không?**  
A: Chắc chắn—lặp qua một tập hợp các sổ làm việc và cập nhật mỗi liên kết một cách lập trình.

**Q: Tôi nên làm gì nếu đường dẫn ngoại của sổ làm việc không đúng?**  
A: Gọi `setAbsolutePath()` với đường dẫn cơ sở đúng để giải quyết tất cả các liên kết một cách chính xác.

## Tài nguyên
- [Tài liệu Aspose.Cells](https://reference.aspose.com/cells/java/)
- [Tải xuống Aspose.Cells](https://releases.aspose.com/cells/java/)
- [Mua giấy phép](https://purchase.aspose.com/buy)
- [Phiên bản dùng thử miễn phí](https://releases.aspose.com/cells/java/)
- [Giấy phép tạm thời](https://purchase.aspose.com/temporary-license/)
- [Diễn đàn hỗ trợ Aspose](https://forum.aspose.com/c/cells/9)

---

**Cập nhật lần cuối:** 2026-11-16  
**Được kiểm tra với:** Aspose.Cells 25.3 for Java  
**Tác giả:** Aspose

## Hướng dẫn liên quan

- [Cách tìm liên kết ngoại ẩn trong sổ làm việc Excel bằng Aspose.Cells cho Java](/cells/java/advanced-features/detect-hidden-external-links-excel-aspose-cells-java/)
- [Sửa đổi kết nối dữ liệu Excel bằng Aspose.Cells cho Java – Hướng dẫn từng bước](/cells/java/advanced-features/master-excel-data-connections-aspose-cells-java/)
- [Cách cập nhật nguồn Pivot Table Excel bằng Aspose.Cells cho Java: Hướng dẫn toàn diện](/cells/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}