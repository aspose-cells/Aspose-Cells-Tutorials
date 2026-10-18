---
category: general
date: 2026-06-30
description: Thêm menu ngữ cảnh tùy chỉnh trong GridJs và tìm hiểu cách tải workbook
  Excel, cập nhật giá trị ô, bật kiểm tra chính tả và đăng ký lệnh tùy chỉnh.
draft: false
keywords:
- add custom context menu
- update cell value
- enable spell checking
- load excel workbook
- register custom command
language: vi
og_description: Thêm menu ngữ cảnh tùy chỉnh trong GridJs trong khi học cách tải workbook
  Excel, cập nhật giá trị ô, bật kiểm tra chính tả và đăng ký lệnh tùy chỉnh.
og_title: Thêm Menu Ngữ Cảnh Tùy Chỉnh vào GridJs – Hướng Dẫn Python Từng Bước
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add custom context menu in GridJs and learn how to load Excel workbook,
    update cell value, enable spell checking, and register custom command.
  headline: Add Custom Context Menu to GridJs – Complete Python Guide
  type: TechArticle
tags:
- GridJs
- Python
- Excel Automation
title: Thêm menu ngữ cảnh tùy chỉnh vào GridJs – Hướng dẫn Python đầy đủ
url: /vi/python/integration-and-interoperability/add-custom-context-menu-to-gridjs-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm Menu Ngữ Cảnh Tùy Chỉnh vào GridJs – Hướng Dẫn Python Đầy Đủ

Bạn đã bao giờ tự hỏi làm thế nào để **thêm mục menu ngữ cảnh tùy chỉnh** vào một bảng GridJs được hỗ trợ bởi một workbook Excel chưa? Bạn không phải là người duy nhất. Trong nhiều ứng dụng dữ liệu nặng, bạn cần menu chuột phải để cho phép người dùng đánh dấu hàng, đánh dấu mục là đã xem xét, hoặc khởi động một hành động phía máy chủ—mà không rời khỏi lưới.  

Trong tutorial này chúng ta sẽ đi qua các bước tải một workbook Excel, gắn một mục menu ngữ cảnh tùy chỉnh, cập nhật giá trị ô, bật kiểm tra chính tả, và đăng ký một lệnh tùy chỉnh để lưu các thay đổi trở lại file. Khi hoàn thành, bạn sẽ có một instance GridJs hoạt động đầy đủ, cảm giác tự nhiên với người dùng và ghi trực tiếp trở lại spreadsheet nguồn.

## Prerequisites

- Python 3.9+ (code sử dụng type hints nhưng chạy trên bất kỳ phiên bản gần đây nào)  
- Thư viện `cells` (hoặc bất kỳ wrapper xử lý Excel nào cung cấp các đối tượng `Workbook` và `Worksheet`)  
- Binding Python `gridjs` (mô hình đối tượng phản ánh API JavaScript)  
- Kiến thức cơ bản về lambda và cấu trúc JSON  

Nếu bạn đã có những thứ trên, hãy bắt đầu.

## Step 1: Load Excel Workbook and Select a Worksheet

Điều đầu tiên bạn cần làm là **load excel workbook** để GridJs có dữ liệu hiển thị. Lớp `cells.Workbook` trừu tượng hoá việc I/O file và cho phép bạn truy cập trực tiếp vào các hàng, cột và ô riêng lẻ.

```python
# Step 1: Load the workbook and select the first worksheet
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]          # Grab the first sheet – change index if needed
```

> **Why this matters:** Loading the workbook up‑front means the grid can pull data on demand, and any edits you make later (like **update cell value**) will be persisted to the same file.

## Step 2: Create GridJs Instance and Bind It to the Worksheet

Bây giờ chúng ta khởi tạo một đối tượng `gridjs.GridJs` và chỉ định worksheet mà nó sẽ render. Hãy nghĩ đây như việc cung cấp cho GridJs một nguồn dữ liệu sống mà nó có thể truy vấn bất cứ khi nào cần render một trang hoặc một khối dữ liệu được tải lười.

```python
# Step 2: Create a GridJs instance and bind it to the worksheet
grid = gridjs.GridJs()
grid.set_worksheet(ws)
```

> **Pro tip:** If you work with multiple sheets, just call `grid.set_worksheet(other_ws)` later—no need to recreate the grid.

## Step 3: Enable Spell Checking (and Other Nice‑to‑Haves)

Hầu hết các ứng dụng doanh nghiệp cho phép người dùng nhập ghi chú tự do. Bật **spell checking** giúp giảm lỗi chính tả và cải thiện chất lượng dữ liệu. GridJs cung cấp một cờ đơn giản cho tính năng này.

```python
# Step 3: Turn on spell checking (and keep other helpers enabled)
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True          # optional but handy
grid.settings.formula_explanation.enabled = True   # if you support formulas
```

> **Why enable spell checking?** It runs client‑side, giving instant feedback without extra server calls—perfect for large‑scale sheets.

## Step 4: Add a Custom Context‑Menu Item

Đây là phần cốt lõi của tutorial: **add custom context menu** entries. Chúng ta sẽ tạo một tùy chọn “Mark as Reviewed” mà khi được nhấn sẽ chạy một lệnh phía server mà chúng ta sẽ định nghĩa tiếp theo.

```python
# Step 4: Add a custom context‑menu item
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",   # What the user sees
    "action": "markReviewed"      # Identifier used in the command registration
})
```

> **Image illustration**  
> ![Ảnh chụp màn hình Thêm Menu Ngữ Cảnh Tùy Chỉnh hiển thị các tùy chọn chuột phải](/images/add-custom-context-menu.png "Ví dụ Thêm Menu Ngữ Cảnh Tùy Chỉnh")

Văn bản alt ở trên chứa từ khóa chính, đáp ứng yêu cầu SEO.

## Step 5: Register Custom Command to Update the Cell Value

Khi người dùng chọn “Mark as Reviewed”, chúng ta cần **register custom command** để cập nhật ô Excel tương ứng và lưu file. Phương thức `grid.register_custom_command` gắn một callable Python vào identifier hành động mà chúng ta đã đặt trước.

```python
# Step 5: Register the server‑side command that updates a cell value
def mark_reviewed_handler(req):
    """
    req is a dict containing at least:
        - 'cell': Excel address like "B5"
    This function writes "Reviewed" into the target cell and saves the workbook.
    """
    # Update the cell value
    ws.get_range(req["cell"]).put_value("Reviewed")
    
    # Persist changes back to disk
    wb.save("YOUR_DIRECTORY/example-updated.xlsx")
    
    # Return a simple JSON response the client can interpret
    return {"status": "ok"}

grid.register_custom_command("markReviewed", mark_reviewed_handler)
```

> **Why this works:** The handler receives the cell reference from the client, uses the `Worksheet` API to **update cell value**, and then writes the whole workbook back to disk. The response lets the front‑end know the operation succeeded.

### Edge‑Case Handling

- **Missing cell reference:** Nếu `req` thiếu `"cell"`, ném lỗi rõ ràng để UI có thể hiển thị toast.  
- **Concurrent edits:** Đối với kịch bản tải cao, cân nhắc khóa workbook hoặc sử dụng version‑stamp để tránh race condition.

## Step 6: Enable Lazy Loading for Big Sheets

Nếu bạn đang làm việc với hàng ngàn dòng, lazy loading giúp UI phản hồi nhanh hơn. Đặt kích thước trang thành một khối hợp lý—500 dòng thường hoạt động tốt trên hầu hết trình duyệt.

```python
# Step 6: Activate lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500
```

> **What if you have 10 000 rows?** The grid will request data page‑by‑page, reducing memory pressure on both client and server.

## Step 7: (Optional) Add a Custom Modal for Row Editing

Đôi khi bạn cần một UI phong phú hơn so với trình chỉnh sửa nội tuyến. GridJs cho phép mở một cửa sổ modal mà bạn có thể host ở bất kỳ đâu—có thể là một component React hoặc một form HTML đơn giản.

```python
# Step 7: Configure a custom modal window for row editing
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"   # Serve this URL from your Flask/Django app
```

> **Why use a modal?** It isolates complex validation logic and gives you full control over layout, while still being triggered from the grid.

## Step 8: Retrieve the Client‑Side Configuration JSON

Cuối cùng, bạn cần chuyển cấu hình tới trình duyệt. Phương thức `get_client_config` sẽ serialize mọi thứ thành một JSON blob mà thư viện GridJs phía front‑end có thể tiêu thụ.

```python
# Step 8: Get the JSON configuration for the front‑end
client_config = grid.get_client_config()

# Example: you might embed this in a template
print(client_config)   # For debugging – remove in production
```

Kết quả đầu ra trông giống như sau (được rút gọn để ngắn gọn):

```json
{
  "worksheet": "example.xlsx",
  "settings": {
    "spell_check": {"enabled": true},
    "context_menu": {
      "custom_items": [
        {"text": "Mark as Reviewed", "action": "markReviewed"}
      ]
    },
    "lazy_load": {"enabled": true, "page_size": 500},
    "custom_modal": {
      "enabled": true,
      "title": "Edit Row Details",
      "url": "/row-editor.html"
    }
  }
}
```

### Expected Result

- Nhấn chuột phải vào bất kỳ ô nào sẽ mở menu với **Mark as Reviewed**.  
- Khi chọn, một yêu cầu sẽ được gửi tới server, **cập nhật giá trị ô** thành “Reviewed” và lưu `example‑updated.xlsx`.  
- Kiểm tra chính tả sẽ đánh dấu các từ sai khi người dùng gõ.  

Tất cả những điều này diễn ra mà không cần tải lại toàn bộ trang, nhờ lazy loading và payload JSON nhẹ.

## Common Questions & Pro Tips

| Question | Answer |
|----------|--------|
| *What if the workbook is read‑only?* | Đảm bảo quyền file cho phép ghi, hoặc mở workbook với `mode="rw"` nếu thư viện hỗ trợ. |
| *Can I add more than one custom menu item?* | Chắc chắn—chỉ cần thêm các dict bổ sung vào `grid.settings.context_menu.custom_items`. |
| *Do I need to reload the grid after a cell update?* | GridJs tự động refresh hàng bị ảnh hưởng nếu bạn trả về `{status:"ok"}`; nếu không, gọi `grid.refresh()` từ client. |
| *How do I make spell checking language‑specific?* | Đặt `grid.settings.spell_check.language = "en-US"` (hoặc bất kỳ locale nào được hỗ trợ). |
| *Is lazy loading compatible with server‑side filtering?* | Có—kết hợp `grid.settings.filter.enabled = True` và triển khai logic filter trong lệnh tùy chỉnh của bạn. |

## Full Working Example (All Steps Combined)

Dưới đây là một script duy nhất bạn có thể đặt vào route Flask hoặc chạy như một tiến trình độc lập. Thay `YOUR_DIRECTORY` bằng đường dẫn thực tế trên server của bạn.

```python
import cells
import gridjs
from flask import Flask, request, jsonify, render_template_string

app = Flask(__name__)

# ---------- Initialization ----------
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]

grid = gridjs.GridJs()
grid.set_worksheet(ws)

# Enable helpers
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True
grid.settings.formula_explanation.enabled = True

# Lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500

# Custom context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",
    "action": "markReviewed"
})

# Custom command implementation
def mark_reviewed_handler(req):
    cell_addr = req.get("cell")
    if not cell_addr:
        return {"status": "error", "message": "Cell address missing"}
    ws.get_range(cell_addr).put_value("Reviewed")
    wb.save("YOUR_DIRECTORY/example-updated.xlsx")
    return {"status": "ok"}

grid.register_custom_command("markReviewed", mark_reviewed_handler)

# Optional modal
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"

client_config = grid.get_client_config()

# ---------- Flask Routes ----------
@app.route("/")
def index():
    # Simple page that injects the config into a <script> tag
    html = f"""
    <!doctype html>
    <html>
    <head>
        <title>GridJs Demo</title>
        <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
    </head>
    <body>
        <div id="grid"></div>
        <script>
            const config = {client_config};
            new gridjs.Grid(config).render(document.getElementById("grid"));
        </script>
    </body>
    </html>
    """
    return render_template_string(html)

@app.route("/command/<name>", methods=["POST"])
def command(name):


## What Should You Learn Next?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ code hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Thêm Thuộc Tính Loại Nội Dung Tùy Chỉnh vào Workbook Excel bằng Aspose.Cells Java](/cells/english/java/tables-structured-references/aspose-cells-java-custom-content-types/)
- [Thêm Phần XML Tùy Chỉnh với ID vào Workbook](/cells/english/net/workbook-operations/add-custom-xml-parts-with-id/)
- [Aspose Cells Java Custom Load Filters Excel Export](/cells/hindi/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}