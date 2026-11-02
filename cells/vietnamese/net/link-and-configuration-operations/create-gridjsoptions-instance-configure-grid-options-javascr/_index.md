---
category: general
date: 2026-05-30
description: Tìm hiểu cách tạo thể hiện GridJsOptions và cấu hình các tùy chọn lưới
  JavaScript cho bảng động. Hướng dẫn từng bước kèm mã đầy đủ.
draft: false
keywords:
- create gridjsoptions instance
- configure grid options javascript
- gridjs initialization
- javascript data grid settings
- dynamic table configuration
language: vi
og_description: Tạo thể hiện GridJsOptions và cấu hình các tùy chọn lưới JavaScript
  trong vài phút. Ví dụ đầy đủ, giải thích và các mẹo thực hành tốt nhất.
og_title: Tạo đối tượng GridJsOptions – Cấu hình tùy chọn lưới JavaScript
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to create GridJsOptions instance and configure grid options
    JavaScript for dynamic tables. Step‑by‑step guide with full code.
  headline: Create GridJsOptions Instance – Configure Grid Options JavaScript
  type: TechArticle
- description: Learn how to create GridJsOptions instance and configure grid options
    JavaScript for dynamic tables. Step‑by‑step guide with full code.
  name: Create GridJsOptions Instance – Configure Grid Options JavaScript
  steps:
  - name: Prerequisites
    text: '- A modern browser (Chrome, Edge, Firefox) – no build tools required. -
      Basic familiarity with JavaScript (variables, objects, DOM). - The Grid.js library
      (we’ll pull it from a CDN).'
  - name: Why this matters
    text: Loading the library from a CDN ensures you always get the latest stable
      version without a local install. The `<div id="grid-wrapper">` is the placeholder
      that the Grid.js constructor will target once we **configure grid options JavaScript**.
  - name: What you’re configuring
    text: '- **NumberFormatAlignment** – aligns numeric strings automatically. - **Pagination**
      – controls page size and navigation. - **Sorting** – toggles column sorting.
      - **Columns** – defines headers, data types, and custom renderers.'
  - name: Edge‑case note
    text: If you later supply a custom data source that already returns paginated
      results, you’ll want to disable Grid.js’s built‑in pagination to avoid double‑paging.
      Simply set `gridOptions.Pagination.enabled = false;`.
  - name: Expected Output
    text: 'When you open the HTML file in a browser you should see:'
  type: HowTo
tags:
- gridjs
- javascript
- data‑grid
title: Tạo đối tượng GridJsOptions – Cấu hình tùy chọn lưới JavaScript
url: /vi/net/link-and-configuration-operations/create-gridjsoptions-instance-configure-grid-options-javascr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo GridJsOptions Instance – Cấu hình Grid Options JavaScript

Bạn đã bao giờ tự hỏi làm thế nào để **create GridJsOptions instance** mà không phải mò mẫm qua các tài liệu rải rác? Bạn không phải là người duy nhất. Khi bạn cần một bảng slick, có thể sắp xếp trên trang web, việc nắm vững cách **configure grid options JavaScript** là bước đầu tiên hướng tới một giao diện người dùng tinh tế.

Trong tutorial này, chúng ta sẽ đi qua đoạn code chính xác bạn cần, giải thích lý do mỗi thiết lập quan trọng, và cho bạn một ví dụ hoàn chỉnh, có thể chạy ngay. Khi kết thúc, bạn sẽ tự tin tạo GridJsOptions instance, điều chỉnh căn chỉnh, phân trang, và thậm chí các renderer tùy chỉnh cho ô – tất cả bằng JavaScript thuần.

## Những gì bạn sẽ học

- Cách **create GridJsOptions instance** từ đầu.
- Các thuộc tính chính cho phép bạn **configure grid options JavaScript** (sắp xếp, phân trang, định dạng số, v.v.).
- Các lỗi thường gặp (ví dụ: trộn kiểu chuỗi và số) và cách tránh chúng.
- Một trang HTML đầy đủ mà bạn có thể sao chép‑dán vào bất kỳ dự án nào và thấy kết quả ngay lập tức.

### Yêu cầu trước

- Trình duyệt hiện đại (Chrome, Edge, Firefox) – không cần công cụ build.
- Kiến thức cơ bản về JavaScript (biến, đối tượng, DOM).
- Thư viện Grid.js (chúng ta sẽ lấy từ CDN).

Nếu bất kỳ mục nào trên chưa quen, đừng lo – mỗi bước đều có phần hướng dẫn nhanh.

---

## Bước 1: Tải Grid.js và chuẩn bị khung HTML

Trước khi chúng ta có thể **create GridJsOptions instance**, cần tải thư viện. Cách dễ nhất là dùng CDN chính thức. Dưới đây là một khung HTML tối thiểu, đồng thời dành một `<div>` để grid sẽ được render.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Grid.js Demo – Configuring Options</title>
  <!-- Grid.js CSS -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
</head>
<body>
  <h2>Simple Data Grid</h2>
  <div id="grid-wrapper"></div>

  <!-- Grid.js JS -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
  <!-- Our custom script will go here -->
  <script src="grid-config.js"></script>
</body>
</html>
```

> **Pro tip:** Đặt liên kết CSS trước các style của bạn để theme mặc định của grid tải đúng cách.

### Tại sao lại quan trọng

Tải thư viện từ CDN đảm bảo bạn luôn nhận được phiên bản ổn định mới nhất mà không cần cài đặt cục bộ. `<div id="grid-wrapper">` là placeholder mà constructor của Grid.js sẽ nhắm tới sau khi bạn **configure grid options JavaScript**.

---

## Bước 2: Tạo một GridJsOptions Instance mới

Bây giờ là phần trọng tâm của tutorial: dòng code thực sự **creates GridJsOptions instance**. Trong một file riêng tên `grid-config.js` (được tham chiếu trong HTML ở trên) chúng ta sẽ viết:

```javascript
// grid-config.js

// Step 2: Create a new GridJsOptions instance to configure grid behavior
const gridOptions = new GridJsOptions();
```

Dòng duy nhất này cho bạn một object sạch sẽ để bắt đầu thêm các thiết lập. Hãy nghĩ `gridOptions` như bảng điều khiển cho mọi tính năng bạn sẽ bật sau.

### Những gì bạn đang cấu hình

- **NumberFormatAlignment** – tự động căn chỉnh các chuỗi số.
- **Pagination** – điều khiển kích thước trang và navigation.
- **Sorting** – bật/tắt sắp xếp cột.
- **Columns** – định nghĩa tiêu đề, kiểu dữ liệu, và renderer tùy chỉnh.

Bạn có thể thêm bất kỳ thuộc tính nào trong số này trước khi cuối cùng instantiate Grid.

---

## Bước 3: Bật Number Alignment (Yêu cầu thường gặp)

Hầu hết các bảng chứa hỗn hợp văn bản và số. Mặc định Grid.js căn trái mọi thứ, khiến các giá trị tiền tệ trông lạ. Để **configure grid options JavaScript** cho căn chỉnh đúng, bật cờ `NumberFormatAlignment`:

```javascript
// Enable left/right alignment for numeric strings
gridOptions.NumberFormatAlignment = true;
```

Tại sao cần bật? Khi cờ này true, Grid.js sẽ kiểm tra mỗi ô; nếu nó trông giống số (ví dụ: “1234”, “12.34%”), nó sẽ tự động căn phải. Thay đổi nhỏ này làm cho báo cáo dễ đọc hơn rất nhiều.

---

## Bước 4: Thêm Pagination và Sorting

Một grid thực tế hiếm khi vừa trong một màn hình. Hãy bật phân trang (10 hàng mỗi trang) và cho phép người dùng sắp xếp bất kỳ cột nào.

```javascript
gridOptions.Pagination = {
  limit: 10,          // rows per page
  enabled: true
};

gridOptions.Sort = true;   // enables click‑to‑sort on all columns
```

### Lưu ý trường hợp đặc biệt

Nếu sau này bạn cung cấp nguồn dữ liệu tùy chỉnh đã trả về kết quả đã được phân trang, bạn sẽ muốn tắt pagination tích hợp của Grid.js để tránh double‑paging. Chỉ cần đặt `gridOptions.Pagination.enabled = false;`.

---

## Bước 5: Định nghĩa Columns và Dữ liệu mẫu

Bây giờ chúng ta sẽ cung cấp cho grid một số dữ liệu mô phỏng và cho nó biết mỗi cột đại diện cho gì. Đây là nơi mẫu **create gridjsoptions instance** thực sự tỏa sáng – mọi thứ nằm trong một object gọn gàng.

```javascript
// Sample data array of objects
const sampleData = [
  { id: 1, name: "Alice", salary: "54000", department: "Engineering" },
  { id: 2, name: "Bob",   salary: "47000", department: "Marketing" },
  { id: 3, name: "Cara",  salary: "62000", department: "Design" },
  // ...more rows as needed
];

// Column definitions
gridOptions.Columns = [
  { id: "id",   name: "ID",          width: "5%" },
  { id: "name", name: "Employee",    width: "35%" },
  { id: "salary", name: "Salary ($)", width: "20%" },
  { id: "department", name: "Dept.",  width: "40%" }
];

// Attach data source
gridOptions.Data = sampleData;
```

Chú ý chúng ta giữ giá trị `id` của cột trùng với các key trong mỗi object dữ liệu. Quy ước này cho phép Grid.js tự động ánh xạ giá trị, giúp bạn không phải viết formatter tùy chỉnh cho mỗi cột.

---

## Bước 6: Instantiate Grid với Options của chúng ta

Cuối cùng chúng ta **configure grid options javascript** bằng cách truyền object `gridOptions` vào constructor của Grid. Grid sẽ được render bên trong `<div id="grid-wrapper">` mà chúng ta đã chuẩn bị trước.

```javascript
// Create the Grid instance using the previously built options
const grid = new Grid(gridOptions);

// Render the grid into the page
grid.render(document.getElementById("grid-wrapper"));
```

Xong rồi. Toàn bộ quy trình – từ **create gridjsoptions instance** đến render – chỉ mất chưa tới một phút code.

### Kết quả mong đợi

Khi mở file HTML trong trình duyệt, bạn sẽ thấy:

- Dòng tiêu đề với “ID”, “Employee”, “Salary ($)”, “Dept.”.
- Các số lương được căn phải (nhờ `NumberFormatAlignment`).
- Điều khiển phân trang ở dưới cùng (nếu bạn có hơn mười hàng).
- Các tiêu đề cột có thể click để sắp xếp tăng/giảm.

Nếu có gì không đúng, mở console của trình duyệt (F12) và kiểm tra thông báo lỗi – hầu hết bug xuất phát từ ID cột không khớp hoặc thiếu script thư viện.

---

## Bước 7: Tinh chỉnh nâng cao (Tùy chọn)

Dưới đây là một vài ý tưởng nhanh bạn có thể thử nghiệm sau khi grid cơ bản hoạt động.

| Feature | How to enable | Why it helps |
|---------|---------------|--------------|
| **Custom cell renderer** | `gridOptions.Columns[2].formatter = (cell) => \`<b>$${cell}</b>\`;` | Làm nổi bật mức lương bằng chữ đậm. |
| **Search bar** | `gridOptions.Search = true;` | Cho phép người dùng lọc hàng ngay lập tức. |
| **Server‑side data** | Set `gridOptions.Server = { url: "/api/employees", then: data => data.items };` | Mở rộng quy mô lên hàng nghìn hàng. |
| **Theme switching** | Add `gridOptions.ClassName = "gridjs-theme-dark";` | Phù hợp với thiết kế dark‑mode. |

Bạn có thể kết hợp tùy ý – Grid.js được thiết kế linh hoạt. Chỉ cần nhớ giữ lại dòng **create gridjsoptions instance** ở đầu; mọi tinh chỉnh sau này đều dựa trên object duy nhất đó.

---

## Kết luận

Chúng ta vừa đi qua quy trình hoàn chỉnh để **create GridJsOptions instance** và **configure grid options JavaScript** cho một bảng dữ liệu có chức năng sắp xếp, phân trang. Bắt đầu từ một trang HTML thuần, chúng ta đã tải thư viện, xây dựng object options, bật căn chỉnh số, thêm pagination, định nghĩa cột, và cuối cùng render grid.

Từ đây bạn có thể:

- Thay thế `sampleData` tĩnh bằng một cuộc gọi AJAX.
- Thêm formatter tùy chỉnh cho ngày tháng, tiền tệ, hoặc biểu tượng.
- Tích hợp grid vào framework như React hoặc Vue (object `gridOptions` vẫn hoạt động tương tự).

Khả năng là gần như vô hạn, và mẫu chúng ta dùng – tập trung tất cả cài đặt trong một GridJsOptions instance – giúp mã của bạn sạch sẽ và dễ bảo trì.

Có trường hợp sử dụng nào bạn chưa chắc? Hãy để lại bình luận, chúng tôi sẽ cùng khám phá. Chúc bạn coding vui vẻ và tận hưởng việc xây dựng các bảng động với Grid.js!

## Bạn nên học gì tiếp theo?

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [How to Create and Style Excel Tables Using Aspose.Cells for .NET | Step‑By‑Step Guide](/cells/english/net/tables-structured-references/aspose-cells-net-excel-tables-styling/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}