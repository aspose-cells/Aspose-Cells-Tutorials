---
category: general
date: 2026-09-05
description: Tạo workbook Excel trong Python và thêm định dạng có điều kiện để làm
  nổi bật các ô ngày hôm qua. Tìm hiểu toàn bộ mã và lý do mỗi bước quan trọng.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- add conditional formatting excel
- highlight cells based on date
- add conditional formatting range
- how to highlight yesterday cells
language: vi
lastmod: 2026-09-05
og_description: Tạo workbook Excel trong Python và thêm định dạng có điều kiện để
  làm nổi bật các ô ngày hôm qua. Hãy làm theo hướng dẫn từng bước này để có giải
  pháp hoàn chỉnh.
og_image_alt: Screenshot of an Excel sheet where cells are highlighted after creating
  Excel workbook in Python
og_title: Tạo sổ làm việc Excel trong Python – thêm định dạng có điều kiện
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create Excel workbook in Python and add conditional formatting to highlight
    yesterday cells. Learn the full code and why each step matters.
  headline: Create Excel workbook in Python with conditional formatting
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Tạo workbook Excel trong Python với định dạng có điều kiện
url: /vi/python/formatting/create-excel-workbook-in-python-with-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo sổ làm việc Excel trong Python với định dạng có điều kiện

Nếu bạn cần **create Excel workbook python** cho một nhiệm vụ báo cáo, hướng dẫn này sẽ chỉ cho bạn cách tạo một sổ làm việc và áp dụng quy tắc định dạng có điều kiện để làm nổi bật các ngày hôm qua. Bạn sẽ thấy mã chính xác, lý do mỗi dòng tồn tại, và cách điều chỉnh giải pháp cho các khoảng thời gian ngày khác.

Định dạng có điều kiện là một cách mạnh mẽ để thu hút sự chú ý đến dữ liệu đáp ứng một điều kiện cụ thể. Trong hướng dẫn này, chúng tôi sử dụng thư viện Aspose.Cells cho Python via .NET, cung cấp đầy đủ hỗ trợ tính năng Excel mà không cần Microsoft Office. Khi kết thúc hướng dẫn, bạn sẽ có một tệp mà các ô trong phạm vi *I19:K20* sẽ chuyển sang màu hồng khi chứa ngày hôm qua.

## Yêu cầu trước

* Cài đặt Python 3.9+
* Gói `aspose-cells` (cài đặt bằng `pip install aspose-cells`)
* Kiến thức cơ bản về cú pháp Python
* Quyền ghi vào thư mục sẽ lưu sổ làm việc

Mã này hoạt động trên Windows, macOS và Linux miễn là runtime .NET có sẵn.

## Tạo sổ làm việc Excel trong Python

Bước đầu tiên là khởi tạo một đối tượng `Workbook` và lấy worksheet mặc định. Đối tượng này đại diện cho toàn bộ tệp Excel trong bộ nhớ.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Tại sao điều này quan trọng*: `Workbook()` tạo một sổ làm việc trống với một worksheet duy nhất. Truy cập `worksheets[0]` cung cấp cho bạn một tay cầm để thêm dữ liệu, kiểu dáng và định dạng sau này.

## Thêm phạm vi định dạng có điều kiện

Tiếp theo chúng ta định nghĩa khu vực sẽ được quy tắc định dạng có điều kiện đánh giá. Phạm vi `I19:K20` bao gồm sáu ô trên hai hàng.

```python
# Define the range that will receive the conditional formatting rule
condition_collection = worksheet.conditional_formattings.add("I19:K20")
```

*Tại sao điều này quan trọng*: Thêm một bộ sưu tập định dạng có điều kiện vào một phạm vi cụ thể cô lập quy tắc, ngăn nó ảnh hưởng đến các ô không liên quan. Điều này đáp ứng yêu cầu **add conditional formatting range**.

## Định nghĩa quy tắc: làm nổi bật các ô dựa trên ngày

Bây giờ chúng ta tạo một điều kiện loại `TIME_PERIOD`. Điều này yêu cầu Excel so sánh giá trị của mỗi ô với một khoảng thời gian đã định trước.

```python
from aspose.cells import FormatConditionType, TimePeriodType

# Add a TIME_PERIOD condition to the collection
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Set the time period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY
```

*Tại sao điều này quan trọng*: `TIME_PERIOD` là loại tích hợp duy nhất hỗ trợ trực tiếp “Yesterday”, “Today”, “Last Week”, v.v. Bằng cách đặt `condition.time_period` thành `YESTERDAY`, quy tắc sẽ tự động đánh giá giá trị ngày của mỗi ô so với ngày trước ngày hiện tại.

## Định dạng các ô đáp ứng điều kiện

Định dạng có điều kiện cũng cần một kiểu hiển thị. Ở đây chúng tôi chọn màu nền hồng đặc để làm nổi bật các ô phù hợp.

```python
from aspose.pydrawing import Color as DrawingColor
from aspose.cells import BackgroundType

# Apply a pink solid background to cells that satisfy the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID
```

*Tại sao điều này quan trọng*: Đối tượng style xác định cách Excel sẽ hiển thị các ô đáp ứng điều kiện. Sử dụng màu nền hồng đặc đáp ứng yêu cầu **highlight cells based on date** và giúp kết quả dễ kiểm tra.

## Điền các ngày mẫu để đánh giá

Để xem quy tắc hoạt động, chúng tôi chèn hai ngày—một ngày trùng với ngày hôm qua và một ngày không. Định dạng `number` `30` tương ứng với định dạng ngày tích hợp `mm-dd-yy`.

```python
from datetime import datetime

# Cell I19: a date that matches “Yesterday”
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Example date; adjust as needed
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

# Cell K20: a date outside the “Yesterday” period
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Example date; adjust as needed
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Optional label for the range
worksheet.cells.get("I20").put_value("Yesterday")
```

*Tại sao điều này quan trọng*: Cung cấp cả ngày khớp và ngày không khớp cho phép bạn xác minh rằng định dạng có điều kiện hoạt động đúng. Điều chỉnh các ngày theo tháng hiện tại khi chạy script, hoặc thay thế chúng bằng các giá trị động.

## Lưu sổ làm việc

Cuối cùng chúng tôi ghi tệp ra đĩa. Hằng số `SaveFormat.XLSX` đảm bảo đầu ra là tệp Excel hiện đại.

```python
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

*Tại sao điều này quan trọng*: Lưu trữ sổ làm việc cho phép bạn mở nó trong Excel, LibreOffice hoặc bất kỳ trình xem nào hỗ trợ XLSX. Đường dẫn được in ra xác nhận nơi tệp đã được ghi.

## Toàn bộ script

Kết hợp tất cả các phần lại, script hoàn chỉnh, có thể chạy được trông như sau:

```python
# -*- coding: utf-8 -*-
"""
Create an Excel workbook in Python, add a conditional formatting rule,
and highlight yesterday's cells.
"""

from aspose.cells import (
    Workbook, SaveFormat, FormatConditionType,
    BackgroundType, TimePeriodType
)
from aspose.pydrawing import Color as DrawingColor
from datetime import datetime

# Step 1: Create a new workbook and access the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Add a conditional formatting rule for the range I19:K20
condition_collection = worksheet.conditional_formattings.add("I19:K20")
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Step 3: Define the visual style for cells that meet the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID

# Step 4: Set the time‑period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Step 5: Populate sample dates for evaluation
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # yesterday relative to the example
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # outside the period
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Step 6: Add a label for the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### Kết quả mong đợi

Khi bạn mở `TimePeriodExample.xlsx`:

* Ô **I19** hiển thị nền màu hồng vì giá trị của nó trùng với ngày hôm qua.
* Ô **K20** giữ nền mặc định vì ngày của nó nằm ngoài khoảng thời gian.
* Nhãn **“Yesterday”** nằm ở ô I20 để làm rõ.

## Các biến thể phổ biến và trường hợp đặc biệt

| Tình huống | Điều chỉnh |
|-----------|------------|
| **Highlight today instead of yesterday** | Change `condition.time_period = TimePeriodType.TODAY`. |
| **Apply the rule to a larger area** | Update the range string in `add("I19:K20")` to something like `"A1:Z100"`. |
| **Use a different fill color** | Replace `DrawingColor.pink` with any other `DrawingColor` (e.g., `DrawingColor.light_green`). |
| **Work with dynamic dates** | Compute `datetime.now() - timedelta(days=1)` for yesterday and write that value into the cells before applying the rule. |

**Pro tip:** Khi bạn tạo sổ làm việc bằng chương trình cho nhiều người dùng, hãy giữ định nghĩa định dạng có điều kiện tách biệt khỏi việc chèn dữ liệu. Như vậy bạn có thể tái sử dụng cùng một style trên nhiều sheet mà không cần sao chép mã.

## Xác minh kết quả bằng chương trình (tùy chọn)

Nếu bạn muốn xác nhận định dạng mà không mở Excel, bạn có thể kiểm tra style của một ô sau khi lưu:



## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Excel Automation: Tạo Workbook và Thêm ListBox Sử dụng Aspose.Cells cho .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Tạo Excel Workbook và Thêm Nhãn với Aspose.Cells cho Java](/cells/english/java/advanced-excel-charts/data-labeling/)
- [Excel Automation Tạo Workbook Thêm Listbox Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}