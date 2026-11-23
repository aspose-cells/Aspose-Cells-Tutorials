---
category: general
date: 2026-11-22
description: Tìm hiểu cách cung cấp Excel trong một ứng dụng web sử dụng Flask. Hướng
  dẫn này chỉ cách tải workbook Excel và hiển thị Excel trên web bằng GridJs.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to serve excel
- load excel workbook
- display excel web
language: vi
lastmod: 2026-11-22
og_description: Cách phục vụ tệp Excel bằng Flask và GridJs. Hãy theo dõi hướng dẫn
  chi tiết này để tải một workbook Excel và hiển thị nó trên web.
og_image_alt: Screenshot of a Flask‑powered GridJs table showing Excel data
og_title: Cách phục vụ Excel bằng Flask – hướng dẫn chi tiết từng bước
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to serve Excel in a web app using Flask. This guide shows
    how to load Excel workbook and display Excel on the web with GridJs.
  headline: How to serve Excel files with Flask and GridJs
  type: TechArticle
- description: Learn how to serve Excel in a web app using Flask. This guide shows
    how to load Excel workbook and display Excel on the web with GridJs.
  name: How to serve Excel files with Flask and GridJs
  steps:
  - name: Load the Excel workbook
    text: '```python # Step 1: Load the workbook you want to expose via GridJs import
      cells'
  - name: Create a GridJs server‑side handler
    text: '```python # Step 2: Create a GridJs server‑side handler for the workbook
      grid_handler = cells.GridJsHandler(workbook) ```'
  - name: Enable optional features (lazy loading)
    text: '```python # Step 3: Enable optional features (e.g., lazy loading for large
      sheets) grid_handler.settings.lazy_load = True ```'
  - name: Set up a minimal Flask application
    text: '```python # Step 4: Set up a minimal Flask application to serve the GridJs
      UI from flask import Flask, request, jsonify'
  - name: Define the GridJs endpoint
    text: '```python # Step 5: Define an endpoint that returns the current view state
      # and applies any client‑side edits sent as JSON @app.route("/gridjs", methods=["GET",
      "POST"]) def gridjs(): if request.method == "POST": # Apply edits sent from
      the GridJs UI grid_handler.apply_changes(request.json) # Retur'
  - name: Run the Flask server
    text: '```python # Step 6: Run the Flask server (default port 5000) if __name__
      == "__main__": # Debug mode is off for production; enable it only during development.
      app.run(port=5000, debug=False) ```'
  type: HowTo
tags:
- Flask
- Python
- Excel
title: Cách phục vụ tệp Excel bằng Flask và GridJs
url: /vi/python/integration-and-interoperability/how-to-serve-excel-files-with-flask-and-gridjs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách phục vụ tệp Excel với Flask và GridJs

Nếu bạn cần **cách phục vụ excel** trong một ứng dụng web Python, hướng dẫn này cung cấp giải pháp hoàn chỉnh. Bạn sẽ học cách **tải workbook excel** bằng thư viện `cells`, mở rộng nó qua một endpoint Flask, và cho phép người dùng **hiển thị excel trên web** bằng GridJs.

Chúng tôi sẽ đi qua từng dòng mã, giải thích tại sao mỗi phần lại quan trọng, và cung cấp cho bạn một ví dụ sẵn sàng chạy. Khi kết thúc hướng dẫn, bạn có thể nhúng bất kỳ tệp `.xlsx` nào vào một lưới phản hồi phía client mà không cần viết bộ phân tích dữ liệu JavaScript tùy chỉnh.

## Yêu cầu trước

- Python 3.9+ đã được cài đặt  
- `flask` và `cells` packages (`pip install flask cells`)  
- Một tệp Excel mẫu (ví dụ: `sample.xlsx`) trong một thư mục đã biết  

Không cần bất kỳ framework front‑end nào thêm; GridJs tự động xử lý giao diện người dùng.

## Tổng quan về giải pháp

Ý tưởng cốt lõi rất đơn giản:

1. **Tải** workbook Excel trên máy chủ.  
2. **Tạo** một `GridJsHandler` chuyển đổi dữ liệu worksheet sang định dạng JSON mà GridJs yêu cầu.  
3. **Mở rộng** một route Flask trả về view JSON và chấp nhận chỉnh sửa từ client.  
4. **Chạy** server Flask để trình duyệt có thể lấy dữ liệu và hiển thị lưới.

Bây giờ hãy thực hiện từng bước.

## Cách phục vụ Excel với Flask và GridJs

### Bước 1: Tải workbook Excel

```python
# Step 1: Load the workbook you want to expose via GridJs
import cells

workbook_path = "YOUR_DIRECTORY/sample.xlsx"
workbook = cells.Workbook(workbook_path)
```

**Tại sao điều này quan trọng:**  
`cells.Workbook` phân tích tệp `.xlsx` thành một biểu diễn trong bộ nhớ. Tải workbook một lần khi khởi động giúp server nhanh hơn vì các yêu cầu tiếp theo sẽ tái sử dụng cùng một đối tượng thay vì truy cập hệ thống tệp liên tục.

### Bước 2: Tạo một handler phía server cho GridJs

```python
# Step 2: Create a GridJs server‑side handler for the workbook
grid_handler = cells.GridJsHandler(workbook)
```

**Tại sao điều này quan trọng:**  
`GridJsHandler` trừu tượng hoá việc chuyển đổi từ các hàng/cột Excel sang schema JSON mà GridJs tiêu thụ. Nó cũng theo dõi các chỉnh sửa phía client, cho phép bạn lưu lại các thay đổi trở lại workbook sau này nếu cần.

### Bước 3: Bật các tính năng tùy chọn (lazy loading)

```python
# Step 3: Enable optional features (e.g., lazy loading for large sheets)
grid_handler.settings.lazy_load = True
```

**Tại sao điều này quan trọng:**  
Khi một worksheet chứa hàng ngàn dòng, việc gửi toàn bộ dữ liệu một lúc có thể làm quá tải trình duyệt. Lazy loading truyền dữ liệu theo trang, cải thiện hiệu năng cho kịch bản **hiển thị excel trên web**.

### Bước 4: Thiết lập một ứng dụng Flask tối thiểu

```python
# Step 4: Set up a minimal Flask application to serve the GridJs UI
from flask import Flask, request, jsonify

app = Flask(__name__)
```

**Tại sao điều này quan trọng:**  
Flask cung cấp một máy chủ HTTP nhẹ có thể phục vụ các endpoint JSON và tệp tĩnh. Giữ ứng dụng Flask tối giản giảm bề mặt tấn công và làm cho ví dụ dễ thích nghi.

### Bước 5: Định nghĩa endpoint GridJs

```python
# Step 5: Define an endpoint that returns the current view state
#         and applies any client‑side edits sent as JSON
@app.route("/gridjs", methods=["GET", "POST"])
def gridjs():
    if request.method == "POST":
        # Apply edits sent from the GridJs UI
        grid_handler.apply_changes(request.json)
    # Return the JSON view expected by GridJs
    return jsonify(grid_handler.get_view())
```

**Tại sao điều này quan trọng:**  

- **GET** – Trình duyệt lấy view worksheet ban đầu.  
- **POST** – Khi người dùng chỉnh sửa một ô, GridJs gửi payload JSON; `apply_changes` hợp nhất các chỉnh sửa đó trở lại trạng thái nội bộ của handler.  

Trả về `grid_handler.get_view()` đảm bảo client luôn nhận được dữ liệu mới nhất, điều này rất quan trọng cho trải nghiệm **hiển thị excel trên web** mượt mà.

### Bước 6: Chạy server Flask

```python
# Step 6: Run the Flask server (default port 5000)
if __name__ == "__main__":
    # Debug mode is off for production; enable it only during development.
    app.run(port=5000, debug=False)
```

**Tại sao điều này quan trọng:**  
Chạy trên cổng 5000 là mặc định của Flask, giúp dễ dàng kiểm tra cục bộ (`http://localhost:5000/gridjs`). Trong môi trường production, bạn sẽ đặt Flask phía sau một server WSGI (ví dụ: Gunicorn) và có thể bật HTTPS.

## Đầu ra JSON dự kiến

Khi bạn truy cập `http://localhost:5000/gridjs` bằng yêu cầu GET, phản hồi sẽ trông như sau:

```json
{
  "columns": ["A", "B", "C"],
  "data": [
    ["Header1", "Header2", "Header3"],
    ["Row1Col1", "Row1Col2", "Row1Col3"],
    ["Row2Col1", "Row2Col2", "Row2Col3"]
  ],
  "settings": {
    "lazy_load": true
  }
}
```

GridJs tự động tiêu thụ payload này, hiển thị một bảng có khả năng tìm kiếm, sắp xếp trong trình duyệt.

## Ví dụ đầy đủ có thể chạy

Dưới đây là script hoàn chỉnh bạn có thể sao chép vào `app.py` và thực thi:

```python
import cells
from flask import Flask, request, jsonify

# -------------------------------------------------
# 1. Load the Excel workbook
# -------------------------------------------------
workbook_path = "YOUR_DIRECTORY/sample.xlsx"
workbook = cells.Workbook(workbook_path)

# -------------------------------------------------
# 2. Create the GridJs handler
# -------------------------------------------------
grid_handler = cells.GridJsHandler(workbook)

# -------------------------------------------------
# 3. Enable lazy loading (optional but recommended)
# -------------------------------------------------
grid_handler.settings.lazy_load = True

# -------------------------------------------------
# 4. Initialize Flask
# -------------------------------------------------
app = Flask(__name__)

# -------------------------------------------------
# 5. Define the GridJs endpoint
# -------------------------------------------------
@app.route("/gridjs", methods=["GET", "POST"])
def gridjs():
    if request.method == "POST":
        # Apply client‑side edits
        grid_handler.apply_changes(request.json)
    # Return current view as JSON
    return jsonify(grid_handler.get_view())

# -------------------------------------------------
# 6. Run the server
# -------------------------------------------------
if __name__ == "__main__":
    app.run(port=5000, debug=False)
```

Chạy script với:

```bash
python app.py
```

Mở trình duyệt và truy cập một trang HTML đơn giản tải GridJs (xem tài liệu GridJs để biết thẻ `<script>`). Lưới sẽ hiển thị nội dung Excel ngay lập tức.

## Các biến thể phổ biến và trường hợp đặc biệt

| Tình huống | Cách điều chỉnh |
|-----------|-----------------|
| **Multiple worksheets** | Tạo một `GridJsHandler` riêng cho mỗi sheet và mở rộng các endpoint distinct (`/gridjs/sheet1`, `/gridjs/sheet2`). |
| **Large files (>10 MB)** | Tăng giới hạn kích thước yêu cầu của Flask (`app.config['MAX_CONTENT_LENGTH']`) và giữ `lazy_load` bật. |
| **Persisting edits back to the file** | Sau `apply_changes`, gọi `workbook.save("output.xlsx")` để ghi các thay đổi lên đĩa. |
| **Authentication** | Bao bọc endpoint bằng Flask‑Login hoặc kiểm tra token API trước khi trả về dữ liệu. |
| **CORS for external front‑ends** | Thêm `from flask_cors import CORS; CORS(app)` để cho phép yêu cầu cross‑origin. |

Những điều chỉnh này cho phép bạn mở rộng quy trình **tải workbook excel** lên các khối lượng công việc production.

## Mẹo chuyên nghiệp

- **Cache view JSON** nếu workbook hiếm khi thay đổi; sử dụng `functools.lru_cache` quanh `grid_handler.get_view()` để giảm tải serialization.  
- **Xác thực các chỉnh sửa đến** (`request.json`) để ngăn dữ liệu sai định dạng làm hỏng workbook.  
- Khi phục vụ qua HTTPS, đặt `app.run(ssl_context=('cert.pem', 'key.pem'))` để mã hoá lưu lượng.

## Kết luận

Bạn đã biết **cách phục vụ excel** bằng Flask và GridJs, từ việc tải workbook đến việc trả về view JSON mà trình duyệt có thể render. Ví dụ bao gồm toàn bộ vòng đời: **tải workbook excel**, bật lazy loading, mở rộng endpoint REST, và chạy một server sẵn sàng cho production.

Tiếp theo, khám phá các chủ đề liên quan như **hiển thị excel trên web** trong front‑end React, hoặc mở rộng handler để **tải workbook excel** từ lưu trữ đám mây (ví dụ: AWS S3). Thử nghiệm với việc tạo kiểu cho các cột GridJs, thêm phân trang, hoặc lưu lại các chỉnh sửa của người dùng trở lại bảng tính gốc.

Chúc bạn lập trình vui vẻ, và tận hưởng việc biến các tệp Excel tĩnh thành các bảng web tương tác!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã mẫu hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách tải và chỉnh sửa tệp Excel bằng Aspose.Cells cho .NET: Hướng dẫn toàn diện](/cells/english/net/workbook-operations/load-modify-excel-aspose-cells-net/)
- [Cách tạo và xuất Excel sang HTML bằng Aspose.Cells Java \| Hướng dẫn thao tác Workbook](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}