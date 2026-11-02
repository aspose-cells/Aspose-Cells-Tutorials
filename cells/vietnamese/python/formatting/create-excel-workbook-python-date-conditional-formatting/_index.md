---
category: general
date: 2026-08-08
description: Tạo workbook Excel bằng Python và thêm định dạng có điều kiện dựa trên
  ngày. Hướng dẫn từng bước sử dụng Aspose.Cells để làm nổi bật các ô của ngày hôm
  qua.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- conditional formatting based on date
- Aspose.Cells Python example
- Excel date formatting Python
- Python Excel automation
language: vi
lastmod: 2026-08-08
og_description: Tạo workbook Excel bằng Python với Aspose.Cells và áp dụng định dạng
  có điều kiện dựa trên ngày cho các bảng tính động.
og_image_alt: Screenshot of an Excel sheet created with Python showing cells highlighted
  by date conditional formatting
og_title: Tạo workbook Excel bằng Python – định dạng có điều kiện ngày
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Create Excel workbook Python and add conditional formatting based on
    date. Step‑by‑step guide using Aspose.Cells to highlight yesterday’s cells.
  headline: Create Excel workbook Python date conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: Tạo workbook Excel với định dạng có điều kiện ngày bằng Python
url: /vi/python/formatting/create-excel-workbook-python-date-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo workbook Excel bằng Python với định dạng có điều kiện dựa trên ngày

Nếu bạn cần **create Excel workbook Python** và tự động làm nổi bật các ô khớp với một ngày cụ thể, hướng dẫn này sẽ chỉ cho bạn cách thực hiện. Bạn sẽ học cách áp dụng **conditional formatting based on date** để các ngày hôm qua hiển thị màu hồng, sử dụng thư viện Aspose.Cells.

Hướng dẫn sẽ đi qua từng bước—từ cài đặt SDK đến lưu tệp .xlsx cuối cùng—để bạn có thể sao chép‑dán một ví dụ hoạt động vào dự án của mình. Không cần tài liệu bên ngoài; tất cả mã và giải thích đều tự chứa.

## Prerequisites

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* Python 3.8 hoặc mới hơn đã được cài đặt.
* Gói `aspose-cells` (bộ bao bọc Python cho Aspose.Cells). Cài đặt bằng:
  ```bash
  pip install aspose-cells
  ```
* Kiến thức cơ bản về Python và các khái niệm Excel như worksheet và style ô.

> **Pro tip:** Aspose.Cells hoạt động mà không cần cài đặt Microsoft Excel, rất phù hợp cho tự động hoá phía máy chủ.

## Step 1: Create the Excel workbook in Python

Nhiệm vụ đầu tiên là khởi tạo một workbook mới và lấy worksheet mặc định. Đối tượng này đại diện cho toàn bộ tệp Excel và cung cấp quyền truy cập vào các hàng, cột và API định dạng.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook – this automatically adds one worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]   # reference to the first (default) sheet
```

Tạo workbook là nền tảng cho mọi thao tác tiếp theo, dù bạn đang thêm dữ liệu, công thức hay quy tắc định dạng.

## Step 2: Define a date‑based conditional format

Bây giờ chúng ta thêm **conditional formatting based on date**. Enum `FormatConditionType.TIME_PERIOD` cho phép chỉ định các khoảng thời gian tích hợp như Yesterday, Today hoặc LastWeek.

```python
from aspose.cells import FormatConditionType, BackgroundType, TimePeriodType
from aspose.pydrawing import Color

# Target range I19:K20 – three columns by two rows
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions

# Add a new time‑period condition (e.g., Yesterday)
condition_index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[condition_index]

# Set the visual style: pink solid background
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Specify that the condition should trigger for "Yesterday"
condition.time_period = TimePeriodType.YESTERDAY
```

Tại sao bước này quan trọng: Excel sẽ đánh giá điều kiện cho mỗi ô trong phạm vi. Khi giá trị của ô nằm trong khoảng thời gian đã định (hôm qua), kiểu chúng ta chỉ định sẽ được áp dụng tự động.

## Step 3: Populate the range with sample dates

Để xem quy tắc hoạt động, chúng ta ghi một vài đối tượng `datetime` vào các ô mục tiêu. Một trong số chúng được đặt cố ý là ngày hôm qua so với hệ thống ngày nội bộ của workbook.

```python
from datetime import datetime

# Cell I19 – yesterday’s date (will be highlighted)
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # This date matches the "Yesterday" rule
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel’s built‑in date format
cell_i19.set_style(style_i19)

# Cell K20 – a random later date (no highlight)
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Not yesterday, so no formatting
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

Dòng `number = 30` cho Excel hiển thị giá trị bằng định dạng ngày ngắn tiêu chuẩn. Bạn có thể thay đổi chỉ mục này thành bất kỳ định dạng số tích hợp nào nếu muốn trình bày khác.

## Step 4: Adjust column width for readability

Tự động điều chỉnh độ rộng cột chứa ngày giúp đầu ra dễ đọc hơn, đặc biệt khi workbook được mở trong Excel hoặc một trình xem.

```python
# Column 12 corresponds to column L (zero‑based indexing)
worksheet.auto_fit_column(12)
```

## Step 5: Save the workbook to disk

Cuối cùng, lưu workbook dưới dạng tệp .xlsx. Thay `"YOUR_DIRECTORY"` bằng đường dẫn thực tế trên máy của bạn.

```python
import os

output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

Khi bạn mở `TimePeriodDemo.out.xlsx` trong Excel, ô **I19** sẽ hiển thị nền màu hồng vì giá trị của nó khớp với quy tắc “Yesterday”, trong khi **K20** không thay đổi.

### Expected output

| I19 (ngày) | I20 (nhãn) | J19 | J20 | K19 | K20 (ngày) |
|------------|------------|-----|-----|-----|------------|
| *2008‑07‑30* (nền màu hồng) | Hôm qua | – | – | – | *2008‑08‑03* (không định dạng) |

Màu hồng xác nhận rằng **conditional formatting based on date** hoạt động như mong đợi.

## Common variations and edge cases

| Tình huống | Cách điều chỉnh mã |
|-----------|--------------------|
| **Làm nổi bật “Today” thay vì “Yesterday”** | Thay `condition.time_period = TimePeriodType.TODAY` |
| **Áp dụng quy tắc cho toàn bộ cột** | Dùng `worksheet.get_range("A:A").format_conditions` |
| **Sử dụng khoảng ngày tùy chỉnh (ví dụ: 7 ngày gần nhất)** | Thay thế điều kiện thời gian bằng điều kiện công thức: <br>```python<br>condition = conditions.add_condition(FormatConditionType.FORMULA)<br>condition.formula1 = 'AND(A1>=TODAY()-7, A1<=TODAY())'<br>``` |
| **Màu nền khác nhau** | Đặt `condition.style.background_color = Color.light_green` (hoặc bất kỳ `Color` nào bạn muốn) |
| **Chạy trên Linux mà không có màn hình** | Aspose.Cells hoàn toàn headless; không cần cấu hình thêm. |

## Full, runnable example

Dưới đây là script hoàn chỉnh bạn có thể chạy ngay (sau khi cập nhật thư mục đầu ra). Tất cả import, comment và các xử lý lỗi cơ bản đều được bao gồm.

```python
# -*- coding: utf-8 -*-
"""
Create Excel workbook Python with date conditional formatting.
Demonstrates how to highlight yesterday’s dates using Aspose.Cells.
"""

import os
from datetime import datetime
from aspose.cells import (
    Workbook, SaveFormat,
    FormatConditionType, BackgroundType,
    TimePeriodType
)
from aspose.pydrawing import Color

# ----------------------------------------------------------------------
# 1️⃣ Initialize workbook
# ----------------------------------------------------------------------
workbook = Workbook()
worksheet = workbook.worksheets[0]

# ----------------------------------------------------------------------
# 2️⃣ Add conditional formatting for "Yesterday"
# ----------------------------------------------------------------------
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions
cond_idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[cond_idx]

# Visual style: pink solid fill
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
condition.time_period = TimePeriodType.YESTERDAY

# ----------------------------------------------------------------------
# 3️⃣ Populate sample dates
# ----------------------------------------------------------------------
# Cell that should match the condition
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Yesterday relative to demo data
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel short‑date format
cell_i19.set_style(style_i19)

# Cell that does NOT match
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label
worksheet.cells.get("I20").put_value("Yesterday")

# ----------------------------------------------------------------------
# 4️⃣ Auto‑fit column for better visibility
# ----------------------------------------------------------------------
worksheet.auto_fit_column(12)   # Column L (0‑based index)

# ----------------------------------------------------------------------
# 5️⃣ Save workbook
# ----------------------------------------------------------------------
output_dir = "YOUR_DIRECTORY"   # <-- replace with a real folder
os.makedirs(output_dir, exist_ok=True)
output_path = os.path.join(output_dir, "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Chạy script sẽ tạo ra một tệp Excel trong đó ô “Yesterday” được tự động làm nổi bật, minh họa **create Excel workbook Python** kết hợp với **conditional formatting based on date**.

## Conclusion

Bạn giờ đã biết cách **create Excel workbook Python** các đối tượng, định nghĩa một **date‑based conditional formatting**.

## What Should You Learn Next?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Tạo Workbook Excel bằng Aspose.Cells trong Java: Hướng dẫn từng bước](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Tạo Workbook Excel với Biểu đồ bằng Aspose.Cells .NET | Hướng dẫn từng bước](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)
- [Tự động hoá Excel: Tạo Workbook và Thêm ListBox bằng Aspose.Cells cho .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}