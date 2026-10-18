---
category: general
date: 2026-10-07
description: Tạo workbook Excel trong Python, đặt màu nền cho ô, tự động điều chỉnh
  độ rộng cột và điền ngày vào Excel với một ví dụ mã ngắn gọn.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- auto fit excel columns
- populate dates in excel
- how to create excel
language: vi
lastmod: 2026-10-07
og_description: Tạo sổ làm việc Excel trong Python, sau đó đặt màu nền cho ô, tự động
  điều chỉnh độ rộng cột và điền ngày vào Excel. Hãy làm theo hướng dẫn từng bước
  này để tạo file TimePeriodDemo.xlsx.
og_image_alt: Screenshot of a Python‑generated Excel workbook with pink highlighted
  cells
og_title: Tạo workbook Excel trong Python – đặt nền và tự động điều chỉnh kích thước
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  headline: Create Excel workbook in Python and set cell background
  type: TechArticle
- description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  name: Create Excel workbook in Python and set cell background
  steps:
  - name: Import required namespaces and define a helper function
    text: '```python # Step 1: Import Aspose.Cells classes and supporting modules
      from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType,
      SaveFormat from aspose.pydrawing import Color from datetime import datetime
      import os ```'
  - name: Create the workbook and get the first worksheet
    text: '```python def create_workbook(): # Step 2: Instantiate a new workbook (empty
      Excel file) book = Workbook() # Aspose.Cells creates a default worksheet; we
      retrieve it for further work sheet = book.worksheets[0] return book, sheet ```'
  - name: Set cell background color with a conditional format
    text: '```python def add_yesterday_rule(sheet): # Define a conditional format
      for the range I19:K20 (Yesterday) conds = sheet.get_range("I19:K20").format_conditions
      idx = conds.add_condition(FormatConditionType.TIME_PERIOD) cond = conds[idx]'
  - name: Populate dates in Excel
    text: '```python def populate_sample_dates(sheet): # Insert a date that falls
      on yesterday relative to the demo data cell = sheet.cells.get("I19") cell.put_value(datetime(2008,
      7, 30)) # sample date cell.style.number = 30 # Excel’s date format ID cell.set_style(cell.style)'
  - name: Auto‑fit Excel columns for better visibility
    text: '```python def auto_fit_columns(sheet): # Auto‑fit column L (index 12) so
      the content is fully visible sheet.auto_fit_column(12) # <-- auto fit excel
      columns ```'
  - name: Save the workbook
    text: '```python def save_workbook(book, filename="TimePeriodDemo.xlsx"): out_path
      = os.path.join("YOUR_DIRECTORY", filename) os.makedirs(os.path.dirname(out_path),
      exist_ok=True) book.save(out_path, SaveFormat.XLSX) print(f"Workbook saved to:
      {out_path}") ```'
  - name: Full script – putting it all together
    text: '```python def main(): # Create workbook and obtain the first worksheet
      book, sheet = create_workbook()'
  type: HowTo
tags:
- Excel
- Python
- Aspose.Cells
title: Tạo workbook Excel bằng Python và đặt nền cho ô
url: /vi/python/import-and-export/create-excel-workbook-in-python-and-set-cell-background/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo workbook Excel trong Python và đặt nền cho ô

Tạo workbook Excel trong Python và áp dụng định dạng có điều kiện chỉ với vài dòng mã. Hướng dẫn này cho bạn thấy **cách tạo file excel** một cách lập trình, đặt màu nền cho ô, tự động điều chỉnh độ rộng cột Excel, và điền ngày vào Excel bằng thư viện Aspose.Cells.

Bạn sẽ học cách:
* Khởi tạo một workbook và lấy worksheet đầu tiên.  
* Định nghĩa định dạng có điều kiện để làm nổi bật các ngày “Yesterday”.  
* Chèn các ngày mẫu vào các ô cụ thể.  
* Tự động điều chỉnh độ rộng cột để dữ liệu hiển thị rõ ràng.  
* Lưu workbook vào thư mục đã chọn.

Yêu cầu duy nhất là có môi trường Python 3 hoạt động với các gói `aspose-cells` và `aspose-pydrawing` đã được cài đặt:

```bash
pip install aspose-cells aspose-pydrawing
```

---

## Tạo workbook Excel trong Python – từng bước

Các phần sau chia quy trình thành các bước dễ quản lý. Mỗi bước bao gồm mã cần thiết, giải thích **tại sao** nó quan trọng, và một mẹo để tránh các lỗi thường gặp.

### Bước 1: Nhập các namespace cần thiết và định nghĩa hàm trợ giúp

```python
# Step 1: Import Aspose.Cells classes and supporting modules
from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime
import os
```

*Tại sao điều này quan trọng*: Việc nhập các lớp đúng sẽ cho phép bạn truy cập vào việc tạo workbook, định dạng có điều kiện, và xử lý màu sắc.  
**Mẹo chuyên nghiệp**: Giữ các import ở đầu file; nó giúp script dễ đọc hơn và ngăn lỗi import vòng.

### Bước 2: Tạo workbook và lấy worksheet đầu tiên

```python
def create_workbook():
    # Step 2: Instantiate a new workbook (empty Excel file)
    book = Workbook()
    # Aspose.Cells creates a default worksheet; we retrieve it for further work
    sheet = book.worksheets[0]
    return book, sheet
```

Constructor `Workbook()` tạo một workbook Excel trống trong bộ nhớ.  
**Tại sao**: Bắt đầu với một workbook mới đảm bảo không có định dạng thừa từ các lần chạy trước.

### Bước 3: Đặt màu nền cho ô bằng định dạng có điều kiện

```python
def add_yesterday_rule(sheet):
    # Define a conditional format for the range I19:K20 (Yesterday)
    conds = sheet.get_range("I19:K20").format_conditions
    idx = conds.add_condition(FormatConditionType.TIME_PERIOD)
    cond = conds[idx]

    # Apply visual style – this is where we set the cell background color
    cond.style.background_color = Color.pink          # <-- set cell background color
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

*Tại sao*: Sử dụng điều kiện **time period** tự động làm nổi bật bất kỳ ô nào chứa ngày “Yesterday”, loại bỏ việc kiểm tra ngày thủ công.  
**Mẹo**: `Color.pink` chỉ là một ví dụ; bạn có thể sử dụng bất kỳ đối tượng `Color` nào (`Color.yellow`, `Color.light_green`, v.v.).

### Bước 4: Điền ngày vào Excel

```python
def populate_sample_dates(sheet):
    # Insert a date that falls on yesterday relative to the demo data
    cell = sheet.cells.get("I19")
    cell.put_value(datetime(2008, 7, 30))   # sample date
    cell.style.number = 30                 # Excel’s date format ID
    cell.set_style(cell.style)

    # Insert another date outside the “Yesterday” range
    cell = sheet.cells.get("K20")
    cell.put_value(datetime(2008, 8, 3))
    cell.style.number = 30
    cell.set_style(cell.style)

    # Add a label for the rule
    sheet.cells.get("I20").put_value("Yesterday")
```

Ở đây chúng tôi **điền ngày vào Excel** các ô `I19` và `K20`. Ngày đầu tiên sẽ kích hoạt định dạng có điều kiện, trong khi ngày thứ hai sẽ không.  
**Tại sao điều này quan trọng**: Việc minh họa cả giá trị khớp và không khớp giúp bạn xác nhận rằng quy tắc hoạt động như mong đợi.

### Bước 5: Tự động điều chỉnh độ rộng cột Excel để hiển thị tốt hơn

```python
def auto_fit_columns(sheet):
    # Auto‑fit column L (index 12) so the content is fully visible
    sheet.auto_fit_column(12)   # <-- auto fit excel columns
```

`auto_fit_column` điều chỉnh độ rộng cột dựa trên giá trị ô dài nhất.  
**Mẹo**: Gọi hàm này sau khi bạn đã ghi hết dữ liệu; nếu không độ rộng có thể được tính dựa trên nội dung chưa đầy đủ.

### Bước 6: Lưu workbook

```python
def save_workbook(book, filename="TimePeriodDemo.xlsx"):
    out_path = os.path.join("YOUR_DIRECTORY", filename)
    os.makedirs(os.path.dirname(out_path), exist_ok=True)
    book.save(out_path, SaveFormat.XLSX)
    print(f"Workbook saved to: {out_path}")
```

Lưu file sẽ ghi workbook đang ở trong bộ nhớ ra đĩa ở định dạng XLSX hiện đại.

### Script đầy đủ – kết hợp tất cả lại

```python
def main():
    # Create workbook and obtain the first worksheet
    book, sheet = create_workbook()

    # Apply conditional formatting (set cell background color)
    add_yesterday_rule(sheet)

    # Populate the demo dates (populate dates in excel)
    populate_sample_dates(sheet)

    # Auto‑fit the relevant column (auto fit excel columns)
    auto_fit_columns(sheet)

    # Persist the file
    save_workbook(book)

if __name__ == "__main__":
    main()
```

**Expected output**

```
Workbook saved to: YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

Mở file đã tạo trong Excel – các ô `I19:K20` sẽ hiển thị nền màu hồng cho ngày thuộc “Yesterday”, và cột L sẽ đủ rộng để hiển thị nhãn mà không bị cắt.

---

## Tại sao cách tiếp cận này hoạt động tốt nhất

* **Quy trình một lần** – Tất cả các thao tác diễn ra trên cùng một instance `Workbook`, tránh I/O không cần thiết.  
* **Định dạng có điều kiện** – Sử dụng `FormatConditionType.TIME_PERIOD` cho phép Excel xử lý logic ngày, đáng tin cậy hơn so với việc viết kiểm tra ngày tùy chỉnh bằng Python.  
* **Định dạng rõ ràng** – Đặt `background_color` và `pattern` đảm bảo kết quả hiển thị nhất quán trên các phiên bản Excel.  
* **Tự động điều chỉnh sau khi có dữ liệu**

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên đều có các ví dụ mã hoàn chỉnh kèm giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Tạo Excel Workbook Python – Hướng dẫn đầy đủ](/cells/english/python/import-and-export/create-excel-workbook-python-full-guide/)
- [Tạo Excel Workbook Python – Hướng dẫn chi tiết từng bước](/cells/english/python/import-and-export/create-excel-workbook-python-complete-step-by-step-guide/)
- [Tạo Excel Workbook Python – Hướng dẫn đầy đủ với Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}