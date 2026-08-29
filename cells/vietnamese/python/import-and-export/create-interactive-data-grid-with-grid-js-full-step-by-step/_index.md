---
category: general
date: 2026-06-21
description: Tạo lưới dữ liệu tương tác bằng Grid.js và học cách hiển thị bảng dữ
  liệu JSON với tính năng sắp xếp, phân trang và tìm kiếm. Hoàn hảo cho các bảng điều
  khiển web.
draft: false
keywords:
- create interactive data grid
- display json data table
- how to use gridjs
language: vi
og_description: Tạo lưới dữ liệu tương tác trong vài phút. Tìm hiểu cách sử dụng Grid.js
  để hiển thị bảng dữ liệu JSON với phân trang, sắp xếp và tìm kiếm.
og_title: Tạo lưới dữ liệu tương tác với Grid.js – Hướng dẫn đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create interactive data grid using Grid.js and learn how to display
    JSON data table with sorting, pagination, and search. Perfect for web dashboards.
  headline: Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create interactive data grid using Grid.js and learn how to display
    JSON data table with sorting, pagination, and search. Perfect for web dashboards.
  name: Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide
  steps:
  - name: A modern browser (Chrome, Edge, or Firefox) – Grid.js relies on ES6 features.
    text: A modern browser (Chrome, Edge, or Firefox) – Grid.js relies on ES6 features.
  - name: A local or remote folder containing a `grid_data.json` file (we’ll show
      the format).
    text: A local or remote folder containing a `grid_data.json` file (we’ll show
      the format).
  - name: Basic familiarity with HTML and JavaScript – nothing fancy, just the ability
      to open a `.html` file in a browser.
    text: Basic familiarity with HTML and JavaScript – nothing fancy, just the ability
      to open a `.html` file in a browser.
  type: HowTo
tags:
- JavaScript
- Grid.js
- Data Visualization
title: Tạo Lưới Dữ liệu Tương tác với Grid.js – Hướng Dẫn Chi Tiết Từng Bước
url: /vi/python/import-and-export/create-interactive-data-grid-with-grid-js-full-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Lưới Dữ Liệu Tương Tác với Grid.js – Hướng Dẫn Chi Tiết Từng Bước

Bạn đã bao giờ tự hỏi làm sao **tạo lưới dữ liệu tương tác** cho phép người dùng sắp xếp, tìm kiếm và phân trang các hàng mà không cần viết backend chưa? Bạn không phải là người duy nhất. Trong nhiều bảng điều khiển, vấn đề lớn nhất là biến một file JSON tĩnh thành một bảng tìm kiếm mượt mà—giống như một bảng tính nhưng chạy hoàn toàn trong trình duyệt.

Trong tutorial này, chúng ta sẽ đi qua **cách sử dụng Grid.js** để **hiển thị bảng dữ liệu JSON** trên một trang HTML đơn giản. Khi hoàn thành, bạn sẽ có một ví dụ hoạt động mà có thể chèn vào bất kỳ dự án nào, cùng với các mẹo tùy chỉnh thanh công cụ, xử lý tập dữ liệu lớn và tránh các lỗi thường gặp.

## Những Điều Bạn Sẽ Học

- Cách lấy một file JSON định nghĩa các cột và các hàng.
- Cách khởi tạo **Grid.js** với phân trang, sắp xếp, tìm kiếm và thanh công cụ tùy chỉnh.
- Cách render lưới vào một container mục tiêu.
- Các tùy chỉnh tùy chọn: định dạng ô tùy chỉnh, chuyển đổi theme và xử lý lỗi.
- Một mẫu mã hoàn chỉnh, sẵn sàng sao chép‑dán.

### Yêu Cầu Trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

1. Trình duyệt hiện đại (Chrome, Edge hoặc Firefox) – Grid.js dựa vào các tính năng ES6.  
2. Một thư mục cục bộ hoặc từ xa chứa file `grid_data.json` (chúng tôi sẽ hiển thị định dạng).  
3. Kiến thức cơ bản về HTML và JavaScript – không cần gì phức tạp, chỉ cần khả năng mở file `.html` trong trình duyệt.

Không cần công cụ xây dựng, không cần npm install, không cần mã phía server. Đó là ưu điểm của **tạo lưới dữ liệu tương tác** với Grid.js: nó hoạt động ngay từ CDN.

---

## Bước 1: Chuẩn Bị JSON Định Nghĩa Bảng Của Bạn

Điều đầu tiên bạn cần là một payload JSON cho biết Grid.js có những cột nào và sẽ hiển thị những hàng nào. Hãy nghĩ nó như bản thiết kế cho **hiển thị bảng dữ liệu JSON** của bạn. Dưới đây là một ví dụ tối thiểu mà bạn có thể lưu dưới tên `grid_data.json` trong cùng thư mục với file HTML:

```json
{
  "columns": ["ID", "Name", "Email", "Country"],
  "rows": [
    [1, "Alice Johnson", "alice@example.com", "USA"],
    [2, "Bob Smith", "bob@example.com", "Canada"],
    [3, "Carlos Ruiz", "carlos@example.com", "Mexico"],
    [4, "Diana Lee", "diana@example.com", "UK"]
  ]
}
```

*Tại sao lại dùng định dạng này?* Grid.js mong đợi `columns` là một mảng các chuỗi (hoặc các đối tượng cho cấu hình nâng cao) và `rows` là một mảng các mảng, trong đó mỗi mảng con phải khớp với thứ tự cột. Tất nhiên, bạn có thể thêm nhiều cột hơn hoặc các đối tượng lồng nhau – Grid.js sẽ render chúng miễn là cấu trúc khớp nhau.

> **Pro tip:** Nếu bạn lấy dữ liệu từ một API, chỉ cần thay thế `fetch('grid_data.json')` tĩnh bằng URL endpoint của bạn. Phần còn lại của mã vẫn giữ nguyên.

---

## Bước 2: Khởi Tạo Grid.js – Trái Tim của **cách sử dụng gridjs**

Bây giờ nguồn dữ liệu đã sẵn sàng, chúng ta cần đưa Grid.js vào trang và chỉ định cách nó hoạt động. Đây là nơi chúng ta thực sự **tạo lưới dữ liệu tương tác** với các tính năng như phân trang, sắp xếp và một nút thanh công cụ tiện lợi.

```html
<!-- Load Grid.js from the CDN -->
<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
```

CDN cung cấp phiên bản ổn định mới nhất, và theme Meri­maid mang lại giao diện sạch sẽ, hiện đại ngay từ đầu. Bạn có thể thay thế bằng `gridjs.min.css` nếu muốn phong cách mặc định.

Tiếp theo, trong thẻ `<script>`, fetch JSON và khởi tạo lưới:

```javascript
// Step 2: Initialise Grid.js with pagination, sorting, searching, and a toolbar
fetch('grid_data.json')
  .then(response => response.json())
  .then(data => {
    const grid = new gridjs.Grid({
      columns: data.columns,      // Pull column headers from JSON
      data: data.rows,            // Pull row data from JSON
      pagination: { enabled: true, limit: 10 }, // Show 10 rows per page
      sort: true,                 // Enable column sorting
      search: true,               // Add a search box above the grid
      toolbar: {
        enabled: true,
        items: [
          {
            type: 'button',
            text: 'Help',
            onClick: () => alert('Use the search box to filter rows or click column headers to sort.')
          }
        ]
      },
      // Optional: custom cell formatter for the Email column
      // This demonstrates a deeper dive into how to use Grid.js
      // and shows you can embed HTML inside cells.
      columns: data.columns.map(col => {
        if (col === 'Email') {
          return {
            name: col,
            formatter: cell => gridjs.html(`<a href="mailto:${cell}">${cell}</a>`)
          };
        }
        return col; // Simple string for other columns
      })
    });

    // Step 3: Render the grid into the target container
    grid.render(document.getElementById('grid-container'));
  })
  .catch(err => console.error('Failed to load grid data:', err));
```

### Phân Tích Các Tùy Chọn

| Tùy chọn | Chức năng | Lý do quan trọng |
|----------|-----------|-------------------|
| `pagination` | Chia các hàng thành các trang (mặc định 10 hàng mỗi trang) | Giữ cho các bảng lớn vẫn dễ dùng mà không làm ngập UI. |
| `sort` | Các tiêu đề cột có thể click để chuyển đổi sắp xếp tăng/giảm | Người dùng nhanh chóng tìm được các hàng có giá trị cao nhất. |
| `search` | Thêm ô nhập liệu để lọc hàng ngay lập tức | Tuyệt vời cho các truy vấn ad‑hoc mà không cần tải lại dữ liệu. |
| `toolbar` | Thêm các nút hoặc dropdown tùy chỉnh phía trên lưới | Phù hợp cho các hành động “Help”, “Export”, hoặc “Refresh”. |
| `formatter` | Cho phép trả về HTML thô cho một ô | Ở đây chúng ta chuyển chuỗi email thành liên kết mailto có thể click. |

> **Tại sao lại chọn cách này?** Bằng cách giữ cấu hình lưới ở dạng khai báo, bạn có thể dễ dàng điều chỉnh hành vi mà không cần chạm vào logic render cốt lõi. Đây là cách được khuyến nghị để **cách sử dụng Grid.js** cho hầu hết các dự án.

---

## Bước 3: Render Lưới Vào Trang Của Bạn

Dòng cuối cùng của script—`grid.render(document.getElementById('grid-container'))`—sẽ chèn bảng đầy đủ chức năng vào một `<div>` mà bạn đã đặt ở đâu đó trong phần body của HTML:

```html
<div id="grid-container"></div>
```

Vậy là xong. Khi trang tải, trình duyệt sẽ fetch JSON, tạo instance Grid.js và vẽ bảng tương tác lên màn hình. Không cần refresh, không có cuộc gọi server nào sau lần tải ban đầu.

---

## Tùy Chọn: Tùy Chỉnh Giao Diện và Theme

Nếu theme Meri­maid mặc định không hợp khẩu vị, bạn có thể thay thế bằng bất kỳ theme có sẵn nào (`gridjs.min.css`) hoặc tự viết CSS. Ví dụ, để làm nền tiêu đề thành màu xám nhạt:

```css
.gridjs-th {
  background-color: #f5f5f5;
}
```

Thêm đoạn mã này vào thẻ `<style>` hoặc một stylesheet bên ngoài. Grid.js tuân theo các selector CSS tiêu chuẩn, vì vậy bạn có toàn quyền kiểm soát phông chữ, màu sắc và khoảng cách.

---

## Rủi Ro Thường Gặp & Cách Khắc Phục

| Rủi ro | Triệu chứng | Cách khắc phục |
|--------|-------------|----------------|
| **Lỗi CORS** khi fetch JSON từ domain khác | Console trình duyệt hiện “Blocked by CORS policy” | Đặt JSON trên cùng origin hoặc bật CORS trên server. |
| **Tập dữ liệu lớn gây lag** | Khi scroll bị chậm, phân trang chậm | Sử dụng phân trang phía server (`pagination: { server: { url: (prev, page, limit) => … } }`) hoặc lazy‑load các hàng. |
| **Nút toolbar không hiển thị** | Không có nút nào xuất hiện dù `toolbar.enabled: true` | Đảm bảo bạn đang dùng Grid.js phiên bản 2.0+; các phiên bản cũ có API toolbar khác. |
| **Liên kết email không click được** | Formatter trả về chuỗi thường | Trả về `gridjs.html(...)` thay vì chuỗi thuần, như trong ví dụ. |

Giải quyết những vấn đề này sớm sẽ tiết kiệm hàng giờ debug sau này.

---

## Ví Dụ Hoàn Chỉnh (Sẵn Sàng Sao Chép)

Dưới đây là file HTML hoàn chỉnh mà bạn có thể lưu dưới tên `index.html`. Mở nó trong trình duyệt, và bạn sẽ thấy một demo **tạo lưới dữ liệu tương tác** đầy đủ chức năng, **hiển thị bảng dữ liệu JSON** với sắp xếp, tìm kiếm và nút trợ giúp.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Create Interactive Data Grid with Grid.js</title>
  <!-- Grid.js core library -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
  <!-- Optional theme – Meri­maid -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    /* Simple custom styling */
    body { font-family: Arial, sans-serif; margin: 20px; }
    .gridjs-container { max-width: 900px; margin: auto; }
    .gridjs-th { background-color: #f0f8ff; }
  </style>
</head>
<body>
  <h1>Create Interactive Data Grid with Grid.js</h1>
  <p>This page demonstrates how to <strong>display JSON data table</strong> using Grid.js. Feel free to edit <code>grid_data.json</code> and refresh.</p>

  <!-- Grid will be rendered here -->
  <div id="grid-container"></div>

  <script>
    // Load JSON data and initialise Grid.js
    fetch('grid_data.json')
      .then(r => r.json())
      .then(data => {
        const grid = new gridjs.Grid({
          columns: data.columns.map(col => {
            // Custom formatter for Email column
            if (col === 'Email') {
              return {
                name: col,
                formatter: cell => gridjs.html(`<a href="mailto:${cell}">${cell}</a>`)
              };
            }
            return col;
          }),
          data: data.rows,
          pagination: { enabled: true, limit: 5 },
          sort: true,
          search: true,
          toolbar: {
            enabled: true,
            items: [
              {
                type: 'button',
                text: 'Formula Help',
                onClick: () => alert('Hover over a cell to see its formula description.')
              }
            ]
          }
        });

        // Render the grid
        grid.render(document.getElementById('grid-container'));
      })
      .catch(err => console.error('Error loading grid data:', err));
  </script>
</body>
</html


## Bạn Nên Học Gì Tiếp Theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên đều bao gồm mã mẫu hoàn chỉnh với giải thích chi tiết từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách Tạo Danh Sách Xác Thực Dữ Liệu Excel với Aspose.Cells cho Java: Hướng Dẫn Từng Bước](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)
- [Cách Tạo Hộp Kiểm Tra trong Excel bằng Aspose.Cells cho .NET | Tutorial Xác Thực Dữ Liệu](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)
- [Tạo & Nhập Dữ Liệu XML vào Excel Sử Dụng Aspose.Cells cho Java](/cells/english/java/import-export/create-import-xml-data-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}