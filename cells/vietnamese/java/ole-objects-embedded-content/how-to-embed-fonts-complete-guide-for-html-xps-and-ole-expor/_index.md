---
category: general
date: 2026-03-01
description: Học cách nhúng phông chữ trong HTML và các định dạng khác. Hướng dẫn
  từng bước bao gồm nhúng phông chữ trong HTML, chuyển đổi Excel sang HTML, cách xuất
  OLE và chuyển đổi Excel sang XPS.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- convert excel to html
- how to export ole
- convert excel to xps
language: vi
og_description: Cách nhúng phông chữ trong xuất HTML, XPS và OLE. Tìm hiểu quy trình
  đầy đủ, xem mã Java có thể chạy, và thành thạo việc nhúng phông chữ trong HTML cho
  chuyển đổi Excel.
og_title: Cách Nhúng Phông Chữ – Hướng Dẫn Java Đầy Đủ
tags:
- Aspose.Cells
- Java
- Document Export
title: Cách Nhúng Phông Chữ – Hướng Dẫn Toàn Diện cho Xuất HTML, XPS và OLE
url: /vi/java/ole-objects-embedded-content/how-to-embed-fonts-complete-guide-for-html-xps-and-ole-expor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Nhúng Phông Chữ – Hướng Dẫn Toàn Diện cho HTML, XPS và Xuất OLE

Bạn đã bao giờ tự hỏi **cách nhúng phông chữ** khi chuyển một workbook Excel thành trang web hoặc tài liệu có thể in không? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi kết quả trông ổn trên máy của họ nhưng lại bị lỗi trên máy khác vì thiếu phông chữ cần thiết.  

Trong hướng dẫn này, chúng ta sẽ đi qua một kịch bản thực tế sử dụng Aspose.Cells for Java: chúng ta sẽ nhúng phông chữ trong HTML, giữ nguyên các bộ chọn biến thể emoji khi chuyển sang XPS, và thậm chí giữ cho một đối tượng OLE có thể chỉnh sửa khi xuất ra PPTX. Khi kết thúc, bạn sẽ có một giải pháp vững chắc, có thể sao chép và dán, trả lời câu hỏi “cách nhúng phông chữ” và cũng đề cập đến **embed fonts in html**, **convert excel to html**, **how to export ole**, và **convert excel to xps**.

## Yêu Cầu Trước

- Java 17 (hoặc bất kỳ JDK mới nào)  
- Aspose.Cells for Java 25.x hoặc mới hơn  
- Một IDE phát triển (IntelliJ IDEA, Eclipse, hoặc VS Code)  
- Kiến thức cơ bản về cấu trúc dữ liệu Excel  

Không cần dịch vụ bên ngoài—mọi thứ chạy trên máy cục bộ.

## Tổng Quan Giải Pháp

1. **Tạo một workbook** và sử dụng hàm `WRAPCOLS` để chuyển đổi một dải dọc thành bố cục ba cột.  
2. **Lưu workbook dưới dạng XPS** đồng thời bật các bộ chọn biến thể phông chữ để emoji giữ nguyên.  
3. **Xuất ra HTML** với phông chữ được nhúng, đảm bảo trang hiển thị giống nhau ở mọi nơi.  
4. **Xuất một workbook chứa đối tượng OLE sang PPTX**, giữ khả năng chỉnh sửa.  
5. **Áp dụng mẫu Smart Marker** thể hiện việc ràng buộc dữ liệu master‑detail.  

Mỗi bước được tách riêng trong một mục H2, giúp hướng dẫn dễ dàng lướt qua cho cả công cụ tìm kiếm và trợ lý AI.

![Minh hoạ cách nhúng phông chữ](image.png "cách nhúng phông chữ")

*Văn bản thay thế hình ảnh: sơ đồ cách nhúng phông chữ mô tả quy trình từ Excel sang HTML, XPS và PPTX.*

---

## Bước 1 – Tạo Workbook và Sử Dụng WRAPCOLS (Tại Sao Điều Này Quan Trọng cho embed fonts in html)

Trước khi chúng ta có thể nói về việc nhúng phông chữ, chúng ta cần một workbook thực sự chứa dữ liệu. Hàm `WRAPCOLS` là cách tiện lợi để chia một cột thành nhiều cột, thường làm cho HTML cuối cùng dễ đọc hơn.

```java
import com.aspose.cells.*;

public class EmbedFontsDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Populate A2:A10 with sample data
        for (int i = 2; i <= 10; i++) {
            sheet.getCells().get("A" + i).putValue("Item " + (i - 1));
        }

        // Use WRAPCOLS to create a 3‑column block starting at A1
        Cell resultCell = sheet.getCells().get("A1");
        resultCell.setFormula("=WRAPCOLS(A2:A10,3)");
        workbook.calculateFormula();

        System.out.println("WRAPCOLS result: " + resultCell.getStringValue());
        // -----------------------------------------------------------------
        // The rest of the steps are demonstrated after this point.
        // -----------------------------------------------------------------
```

**Tại sao bước này?**  
Lệnh `WRAPCOLS` tạo ra một dải đa cột mà sau này xuất hiện trong HTML dưới dạng bảng. Khi chúng ta sau này **embed fonts in html**, kiểu dáng của bảng sẽ dựa vào các phông chữ chúng ta nhúng, đảm bảo việc hiển thị nhất quán trên các trình duyệt.

## Bước 2 – Lưu Workbook dưới dạng XPS Trong Khi Bảo Vệ Emoji (convert excel to xps)

Nếu bạn cần một định dạng sẵn sàng để in, XPS là lựa chọn ổn định. Tuy nhiên, các tài liệu hiện đại thường chứa emoji hoặc ký hiệu sử dụng bộ chọn biến thể. Bật `EnableFontVariationSelectors` đảm bảo các ký tự này tồn tại qua quá trình chuyển đổi.

```java
        // --------------------------------------------------------------
        // Step 2: Save as XPS with font variation selectors enabled
        // --------------------------------------------------------------
        WorkbookSettings settings = workbook.getSettings();
        settings.setEnableFontVariationSelectors(true); // crucial for emoji

        String xpsPath = "output/withVariations.xps";
        workbook.save(xpsPath, SaveFormat.XPS);
        System.out.println("Workbook saved as XPS at: " + xpsPath);
```

**Bạn nhận được:**  
Một tệp XPS hiển thị bất kỳ emoji nào được nhúng chính xác như trong workbook nguồn. Điều này đáp ứng yêu cầu **convert excel to xps** và chứng minh việc xử lý phông chữ không chỉ giới hạn trong HTML.

## Bước 3 – Xuất ra HTML với Phông Chữ Được Nhúng (how to embed fonts & embed fonts in html)

Bây giờ chúng ta đến phần cốt lõi của hướng dẫn: **cách nhúng phông chữ** khi chuyển Excel sang HTML. Aspose.Cells cho phép chúng ta nhúng phông chữ trực tiếp vào tệp HTML được tạo, loại bỏ nhu cầu sử dụng các tệp phông chữ bên ngoài.

```java
        // --------------------------------------------------------------
        // Step 3: Export to HTML with embedded fonts
        // --------------------------------------------------------------
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
        htmlOptions.setEmbedFonts(true); // this is the key line for embed fonts in html
        htmlOptions.setExportImagesAsBase64(true); // optional, keeps all assets in one file

        String htmlPath = "output/embeddedFonts.html";
        workbook.save(htmlPath, htmlOptions);
        System.out.println("HTML with embedded fonts saved at: " + htmlPath);
```

**Cách hoạt động:**  
`setEmbedFonts(true)` chỉ cho trình render đọc các tệp phông chữ được sử dụng trong workbook và nhúng chúng dưới dạng quy tắc `@font-face` được mã hoá Base64 trong thẻ `<style>`. HTML tạo ra là tự chứa, vì vậy bạn có thể đặt nó lên bất kỳ máy chủ nào và phông chữ sẽ hiển thị đúng—đúng như những gì các nhà phát triển tìm kiếm khi họ tra **cách nhúng phông chữ**.

**Đoạn mã đầu ra dự kiến (trong `embeddedFonts.html`):**

```html
<style>
@font-face{font-family:"Arial";src:url(data:font/ttf;base64,AAEAAA... ) format('truetype');}
</style>
<table>
  <tr><td>Item 1</td><td>Item 4</td><td>Item 7</td></tr>
  <tr><td>Item 2</td><td>Item 5</td><td>Item 8</td></tr>
  <tr><td>Item 3</td><td>Item 6</td><td>Item 9</td></tr>
</table>
```

Lưu ý quy tắc `@font-face`—đây là câu trả lời cụ thể cho **embed fonts in html**.

## Bước 4 – Xuất Workbook Chứa Đối Tượng OLE sang PPTX (how to export ole)

Nhiều báo cáo kinh doanh nhúng tài liệu Word, PDF hoặc các sheet Excel khác dưới dạng đối tượng OLE. Khi bạn xuất một workbook như vậy sang PowerPoint, thường mất khả năng chỉnh sửa đối tượng. Aspose.Cells giữ nguyên khả năng chỉnh sửa ngay từ đầu.

```java
        // --------------------------------------------------------------
        // Step 4: Export a workbook with an OLE object to PPTX
        // --------------------------------------------------------------
        // Load a workbook that already contains an OLE object.
        Workbook oleWorkbook = new Workbook("input/oleObject.xlsx");

        String pptxPath = "output/oleEditable.pptx";
        oleWorkbook.save(pptxPath, SaveFormat.PPTX);
        System.out.println("PPTX with editable OLE object saved at: " + pptxPath);
```

**Tại sao điều này quan trọng:**  
Nếu bạn đang tìm **how to export ole**, đoạn mã này hiển thị lệnh API chính xác. Slide PowerPoint tạo ra chứa đối tượng OLE dưới dạng thành phần sống, nhấp đúp để chỉnh sửa—không cần xử lý hậu kỳ thêm.

## Bước 5 – Áp Dụng Mẫu Smart Marker (master‑detail) và Hoàn Thành Demo

Smart Markers cho phép bạn ràng buộc nguồn dữ liệu (Map, JSON, DataTable) trực tiếp vào mẫu Excel. Dưới đây là một ví dụ tối thiểu in các hàng master‑detail.

```java
        // --------------------------------------------------------------
        // Step 5: Apply Smart Marker template (master‑detail)
        // --------------------------------------------------------------
        String smartMarkerTemplate = "${Orders.Master:OrderID,Customer}\n${Orders.Detail:Product,Qty,Price}";
        // Simulated data source
        java.util.Map<String, Object> dataSource = new java.util.HashMap<>();
        java.util.List<java.util.Map<String, Object>> master = new java.util.ArrayList<>();
        java.util.Map<String, Object> masterRow = new java.util.HashMap<>();
        masterRow.put("OrderID", 1001);
        masterRow.put("Customer", "Acme Corp");
        master.add(masterRow);
        dataSource.put("Orders.Master", master);

        java.util.List<java.util.Map<String, Object>> detail = new java.util.ArrayList<>();
        java.util.Map<String, Object> detailRow = new java.util.HashMap<>();
        detailRow.put("Product", "Widget");
        detailRow.put("Qty", 5);
        detailRow.put("Price", 9.99);
        detail.add(detailRow);
        dataSource.put("Orders.Detail", detail);

        SmartMarkerProcessor processor = new SmartMarkerProcessor(new Workbook());
        processor.apply(smartMarkerTemplate, dataSource);
        processor.getWorkbook().save("output/smartMarkerResult.xlsx");
        System.out.println("Smart Marker workbook saved.");
    }
}
```

**Bạn sẽ thấy:**  
Một workbook mới (`smartMarkerResult.xlsx`) trong đó các placeholder trong mẫu được thay thế bằng dữ liệu. Bước này không trực tiếp liên quan đến phông chữ, nhưng nó hoàn thiện hướng dẫn bằng cách hiển thị quy trình báo cáo thường đi trước khi xuất **embed fonts in html**.

## Những Cạm Bẫy Thường Gặp & Mẹo Chuyên Gia (Đảm Bảo Nhúng Phông Chữ Thành Công)

| Vấn đề | Tại sao xảy ra | Cách khắc phục |
|-------|----------------|----------------|
| Phông chữ bị thiếu trong tệp HTML | Workbook sử dụng phông chữ hệ thống không được cài đặt trên máy chủ. | Sử dụng `Workbook.getSettings().setDefaultFont("Arial")` trước khi tải dữ liệu, hoặc nhúng các tệp phông chữ cần thiết theo cách thủ công. |
| HTML đầu ra quá lớn | Nhúng nhiều phông chữ lớn làm tăng kích thước tệp. | Giới hạn việc nhúng chỉ các phông chữ thực sự sử dụng: `htmlOptions.setFontEmbeddingMode(HtmlFontEmbeddingMode.EmbedSubset)`. |
| Emoji biến mất sau khi chuyển đổi sang XPS | Các bộ chọn biến thể bị loại bỏ theo mặc định. | Bật `settings.setEnableFontVariationSelectors(true)` như đã trình bày ở Bước 2. |
| Đối tượng OLE trở thành hình ảnh tĩnh trong PPTX | Workbook nguồn được lưu với `setSuppressOLEObjects(true)`. | Đảm bảo **không** suppress OLE objects khi lưu sang PPTX. |

## Xác Minh Kết Quả

1. Mở `embeddedFonts.html` trong Chrome/Firefox. Bảng nên hiển thị bằng phông chữ đã nhúng (ví dụ, Arial) ngay cả khi phông chữ đó không được cài đặt trên máy.  
2. Mở `withVariations.xps` trong Windows XPS Viewer. Emoji như 👍 nên hiển thị đúng.  
3. Mở `oleEditable.pptx` trong PowerPoint. Nhấp đúp vào hình dạng OLE;

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}