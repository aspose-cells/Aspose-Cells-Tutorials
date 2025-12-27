---
date: '2025-12-27'
description: Tìm hiểu cách thay đổi nguồn dữ liệu Excel một cách lập trình bằng Aspose.Cells
  cho Java, chỉnh sửa các kết nối dữ liệu Excel và tự động hoá quy trình làm việc
  của bạn.
keywords:
- Excel data connections
- Aspose.Cells Java
- modify Excel data connections programmatically
title: Cách thay đổi nguồn dữ liệu Excel bằng Aspose.Cells cho Java
url: /vi/java/advanced-features/master-excel-data-connections-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Thay đổi nguồn dữ liệu Excel bằng Aspose.Cells cho Java

## Giới thiệu
Bạn đang gặp khó khăn trong việc **thay đổi nguồn dữ liệu Excel** và sửa đổi các kết nối dữ liệu trong các tệp Excel một cách lập trình? Hướng dẫn toàn diện này được thiết kế cho các nhà phát triển muốn tự động hoá quy trình báo cáo của mình với thư viện mạnh mẽ **Aspose.Cells for Java**. Chúng tôi sẽ hướng dẫn bạn cách tải một workbook Excel, cập nhật kết nối bên ngoài của nó và lưu các thay đổi — tất cả bằng mã Java.

### Bạn sẽ học được gì
- Cách thiết lập Aspose.Cells cho Java trong Maven hoặc Gradle.  
- **Load Excel workbook Java** – đọc một tệp hiện có vào bộ nhớ.  
- **Modify Excel data connections** – cập nhật tên kết nối, đường dẫn ODC và câu lệnh SQL.  
- **Save Excel workbook Java** – ghi workbook đã cập nhật trở lại đĩa.  

Hãy chắc chắn rằng bạn có mọi thứ cần thiết trước khi chúng ta bắt đầu.

## Câu trả lời nhanh
- **What is the primary library?** Aspose.Cells for Java.  
- **Which method loads a workbook?** `new Workbook(filePath)`.  
- **How do I update the connection string?** Use `DBConnection.setConnectionInfo(...)`.  
- **Can I change the ODC file path?** Yes, via `ExternalConnection.setOdcFile(...)`.  
- **Do I need a license for production?** A commercial license removes evaluation limits.

## Yêu cầu trước
Trước khi bắt đầu, hãy xác nhận rằng bạn có những thứ sau:

### Thư viện yêu cầu
Aspose.Cells for Java phiên bản 25.3 trở lên cung cấp các API được sử dụng trong hướng dẫn này.

### Cài đặt môi trường
- Java Development Kit (JDK) đã được cài đặt.  
- Một IDE như IntelliJ IDEA, Eclipse hoặc NetBeans.

### Kiến thức yêu cầu
Hiểu biết về Java, Maven hoặc Gradle, và các khái niệm cơ bản về SQL sẽ giúp bạn theo dõi một cách suôn sẻ.

## Cài đặt Aspose.Cells cho Java
Để bắt đầu sử dụng Aspose.Cells, thêm thư viện vào dự án của bạn:

**Cài đặt Maven**  
Add the dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Cài đặt Gradle**  
Insert the following line into `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Các bước lấy giấy phép
Aspose.Cells cung cấp bản dùng thử miễn phí để bạn có thể đánh giá thư viện trước khi mua:

- Truy cập [free trial page](https://releases.aspose.com/cells/java/) và tải gói đánh giá.  
- Để sử dụng đầy đủ tính năng, mua giấy phép từ [purchase portal](https://purchase.aspose.com/buy).  
- Cần truy cập tạm thời? Yêu cầu một [temporary license](https://purchase.aspose.com/temporary-license/).

Khi thư viện đã được tham chiếu và cấp giấy phép, bạn đã sẵn sàng để viết mã.

## Hướng dẫn thực hiện

### Tính năng 1: Tải Workbook từ tệp
**Mục đích của bước này là gì?** Nó minh họa cách **load Excel workbook Java** để bạn có thể làm việc với các kết nối dữ liệu của nó.

#### Hướng dẫn từng bước
**Xác định Thư mục Dữ liệu của Bạn** – cho chương trình biết tệp nguồn nằm ở đâu:

```java
String dataDir = "YOUR_DATA_DIRECTORY";
```
Đảm bảo `DataConnection.xlsx` tồn tại trong thư mục đó.

**Tải Workbook** – khởi tạo đối tượng `Workbook`:

```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook(dataDir + "DataConnection.xlsx");
```
Đối tượng `Workbook` hiện đại diện cho tệp Excel của bạn trong bộ nhớ.

### Tính năng 2: Sửa đổi Kết nối Dữ liệu trong Workbook
**Tại sao phải sửa đổi?** Cập nhật kết nối bên ngoài cho phép bạn **change Excel data source** mà không cần mở tệp thủ công.

#### Hướng dẫn từng bước
**Truy cập Kết nối Dữ liệu** – lấy kết nối đầu tiên (bạn có thể lặp lại cho nhiều kết nối):

```java
import com.aspose.cells.DBConnection;
import com.aspose.cells.ExternalConnection;
import com.aspose.cells.OLEDBCommandType;

ExternalConnection conn = workbook.getDataConnections().get(0);
```
`getDataConnections()` trả về một tập hợp các kết nối, cho phép bạn **modify excel data connections** riêng lẻ.

**Sửa đổi Thuộc tính Kết nối** – thay đổi tên, tệp ODC, loại lệnh và câu lệnh SQL:

```java
conn.setName("MyConnectionName");
conn.setOdcFile(dataDir + "MyDefaulConnection.odc");
```

Ép kiểu sang `DBConnection` để thiết lập các thông số đặc thù của cơ sở dữ liệu:

```java
DBConnection dbConn = (DBConnection) conn;
dbConn.setCommandType(OLEDBCommandType.SQL_STATEMENT);
dbConn.setCommand("SELECT * FROM AdminTable");

String connectionString = "Server=myServerAddress;Database=myDataBase;User ID=myUsername;Password=myPassword;Trusted_Connection=False";
dbConn.setConnectionInfo(connectionString);
```
Ở đây bạn **update excel external connection** các chi tiết như truy vấn SQL và chuỗi kết nối.

### Tính năng 3: Lưu Workbook vào tệp
**Tiếp theo sẽ xảy ra gì?** Sau khi cập nhật kết nối, bạn cần **save Excel workbook Java** để các thay đổi được lưu lại.

#### Hướng dẫn từng bước
**Xác định Thư mục Đầu ra** – nơi tệp đã sửa sẽ được ghi:

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
```

**Lưu Workbook** – ghi workbook trở lại đĩa:

```java
workbook.save(outDir + "MESQLDataConnection_out.xlsx");
```
Phương thức `save()` hoàn thiện thao tác **change excel data source**.

## Ứng dụng thực tế
Việc sửa đổi các kết nối dữ liệu Excel bằng lập trình mở ra nhiều cơ hội:

1. **Automated Reporting** – tạo báo cáo luôn lấy dữ liệu mới nhất từ cơ sở dữ liệu.  
2. **Data Syncing** – giữ cho các workbook đồng bộ với hệ thống trực tiếp mà không cần làm mới thủ công.  
3. **Dynamic Dashboards** – xây dựng bảng điều khiển phản ánh các chỉ số thời gian thực.

Việc tích hợp Aspose.Cells với các nền tảng CRM, ERP hoặc BI có thể giảm đáng kể công sức thủ công.

## Xem xét về hiệu năng
Khi làm việc với các workbook lớn hoặc tập kết quả khổng lồ:

- Xử lý dữ liệu theo lô để tránh tăng đột biến bộ nhớ.  
- Tối ưu hóa các truy vấn SQL để tăng tốc.  
- Giải phóng tài nguyên kịp thời; gọi `workbook.dispose()` nếu không còn cần đối tượng.

Những thực hành này đảm bảo ứng dụng của bạn vẫn phản hồi nhanh trong khi **changing Excel data source**.

## Kết luận
Bạn đã học cách **change Excel data source** bằng cách tải một workbook, **modify excel data connections**, và lưu tệp đã cập nhật bằng **Aspose.Cells for Java**. Khả năng này cho phép bạn tự động hoá các quy trình dựa trên dữ liệu và giữ các tệp Excel đồng bộ với các hệ thống bên ngoài.

### Bước tiếp theo
- Thử nghiệm với nhiều kết nối bằng cách lặp qua `workbook.getDataConnections()`.  
- Khám phá các tính năng khác của Aspose.Cells như tạo biểu đồ, định dạng ô, và thao tác bảng pivot.

Sẵn sàng nâng cao tự động hoá? Áp dụng các đoạn mã này ngay hôm nay và xem năng suất của bạn tăng vọt!

## Câu hỏi thường gặp

**Q1: Làm thế nào để xử lý nhiều kết nối dữ liệu trong một workbook?**  
A1: Sử dụng `workbook.getDataConnections().get(index)` trong vòng lặp để truy cập từng kết nối riêng lẻ.

**Q2: Tôi có thể sửa đổi các thuộc tính khác của tệp Excel bằng Aspose.Cells Java không?**  
A2: Chắc chắn! Aspose.Cells hỗ trợ định dạng ô, quản lý worksheet, tạo biểu đồ, và nhiều hơn nữa.

**Q3: Nếu lệnh SQL của tôi không thực thi được thì sao?**  
A3: Kiểm tra chuỗi kết nối, quyền truy cập cơ sở dữ liệu, và xem chi tiết ngoại lệ để tìm nguyên nhân.

**Q4: Tôi có thể nhận hỗ trợ cho các vấn đề Aspose.Cells ở đâu?**  
A4: Truy cập [Aspose forum](https://forum.aspose.com/c/cells/9) để đặt câu hỏi hoặc xem các giải pháp hiện có.

**Q5: Phiên bản dùng thử có hạn chế gì không?**  
A5: Phiên bản đánh giá sẽ thêm watermark và có thể giới hạn khả năng xử lý. Mua giấy phép để sử dụng không giới hạn.

## Tài nguyên
- **Documentation:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Download:** [Aspose.Cells for Java Releases](https://releases.aspose.com/cells/java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Cập nhật lần cuối:** 2025-12-27  
**Đã kiểm tra với:** Aspose.Cells Java 25.3  
**Tác giả:** Aspose