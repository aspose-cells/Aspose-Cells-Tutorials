---
category: general
date: 2026-09-21
description: Học cách tạo workbook Excel trong Python, đặt màu nền cho ô và áp dụng
  định dạng có điều kiện dựa trên ngày với Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- excel conditional formatting python
- date based conditional formatting
language: vi
lastmod: 2026-09-21
og_description: Tạo workbook Excel trong Python, đặt màu nền cho ô và áp dụng định
  dạng có điều kiện dựa trên ngày tháng bằng Aspose.Cells. Thực hiện theo hướng dẫn
  từng bước.
og_image_alt: Screenshot of an Excel sheet showing a yellow‑green cell background
  for yesterday's dates
og_title: Tạo sổ làm việc Excel trong Python với định dạng có điều kiện
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to create Excel workbook in Python, set cell background color,
    and apply date based conditional formatting with Aspose.Cells.
  headline: Create Excel workbook in Python using conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: Tạo sổ làm việc Excel trong Python bằng định dạng có điều kiện
url: /vi/python/formatting/create-excel-workbook-in-python-using-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo workbook Excel trong Python bằng định dạng có điều kiện

Nếu bạn cần **tạo workbook Excel python** các script tự động làm nổi bật ngày tháng, hướng dẫn này sẽ chỉ cho bạn cách thực hiện. Bạn sẽ thấy cách **đặt màu nền cho ô**, thêm quy tắc “Yesterday”, và lưu file — tất cả đều với Aspose.Cells cho Python.

Làm việc với các file Excel một cách lập trình thường đồng nghĩa với việc lặp lại cùng một logic định dạng trên nhiều sheet. Khi kết thúc tutorial này, bạn sẽ có một mẫu có thể tái sử dụng cho **excel conditional formatting python** mà bạn có thể đưa vào bất kỳ dự án nào.

## Prerequisites

- Python 3.8+ đã được cài đặt  
- Gói `aspose-cells` (`pip install aspose-cells`)  
- Kiến thức cơ bản về hàm Python và mô-đun datetime  

Không cần thư viện bổ sung nào; Aspose.Cells xử lý mọi thao tác Excel.

## Bước 1: Tạo workbook và truy cập worksheet đầu tiên

Bước đầu tiên là **tạo excel workbook python** các đối tượng và lấy worksheet mặc định. Điều này cung cấp cho bạn một canvas sạch để tiếp tục định dạng.

```python
# Import required Aspose.Cells classes
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# Create a new workbook; the first worksheet is at index 0
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Lý do quan trọng:* `Workbook()` tạo một file Excel trong bộ nhớ. Truy cập `worksheets[0]` tránh việc hard‑code tên sheet và vẫn hoạt động ngay cả khi tên mặc định thay đổi.

## Bước 2: Trợ giúp để thêm định dạng có điều kiện TIME_PERIOD

Để giữ code gọn gàng, chúng ta gói việc tạo conditional‑format trong một hàm trợ giúp. Hàm này nhận một phạm vi ô, màu nền, và quy tắc thời gian mong muốn.

```python
def add_time_period(sheet, cell_range, bg_color, period_type):
    """
    Adds a TIME_PERIOD conditional formatting rule to `cell_range`.
    The rule paints the cells with `bg_color` when the date matches `period_type`.
    """
    # Retrieve (or create) the ConditionalFormatting collection for the range
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)

    # Insert a TIME_PERIOD condition and configure its style
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color          # set cell background color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type                # e.g., TimePeriodType.YESTERDAY
```

*Lý do quan trọng:* Trợ giúp này trừu tượng hoá các bước lặp lại khi tạo conditional format, giúp bạn dễ dàng tái sử dụng cho các quy tắc dựa trên ngày khác như “Today” hoặc “Last Week”.

## Bước 3: Áp dụng quy tắc “Yesterday” cho một phạm vi

Bây giờ chúng ta dùng trợ giúp để làm nổi bật các ô chứa ngày hôm qua. Phạm vi `I19:K20` sẽ chuyển sang **medium sea green** khi điều kiện được thỏa mãn.

```python
add_time_period(
    worksheet,
    "I19:K20",                # range to format
    Color.medium_sea_green,  # set cell background color
    TimePeriodType.YESTERDAY # date based conditional formatting
)
```

*Lý do quan trọng:* `TimePeriodType.YESTERDAY` là một phần của enumeration tích hợp sẵn trong Aspose.Cells, vì vậy bạn không cần tự tính toán ngày. Thư viện sẽ đánh giá quy tắc mỗi khi workbook được mở.

## Bước 4: Điền dữ liệu mẫu vào phạm vi

Để xem quy tắc hoạt động, chúng ta ghi hai ngày — một ngày khớp “Yesterday” và một ngày không khớp. Kiểu `number` `30` tương ứng với một định dạng ngày tích hợp sẵn.

```python
# Cell I19 gets a date that is exactly yesterday (relative to the sample data)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))   # 30 July 2008
cell.style.number = 30                # date format

# Cell K20 gets a date that is outside the rule
cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))    # 3 August 2008
cell.style.number = 30
```

*Lý do quan trọng:* Bằng cách chèn các ngày cụ thể, bạn có thể xác nhận rằng conditional formatting hoạt động mà không cần mở file vào một ngày nhất định.

## Bước 5: Thêm nhãn mô tả và tự động điều chỉnh độ rộng cột

Một nhãn ngắn gọn làm rõ mục đích của phạm vi đã định dạng, và `auto_fit_column` giúp sheet dễ đọc hơn.

```python
# Add a label under the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Adjust column width for better visibility (column 12 = L)
worksheet.auto_fit_column(12)
```

## Bước 6: Lưu workbook

Cuối cùng, ghi workbook ra đĩa. Lệnh `os.makedirs` đảm bảo thư mục đích tồn tại.

```python
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)

# Save as XLSX – the most widely supported Excel format
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Khi bạn mở *TimePeriodDemo.xlsx* sẽ thấy:

- Ô **I19** được tô **medium sea green** vì giá trị của nó khớp với quy tắc “Yesterday”.  
- Ô **K20** giữ nền mặc định vì ngày của nó không thỏa mãn điều kiện.  

Điều này minh họa **format cells by date** chỉ với một dòng code Python.

## Ví dụ đầy đủ, có thể chạy ngay

Kết hợp tất cả các phần lại, đây là script hoàn chỉnh mà bạn có thể sao chép‑dán và chạy:

```python
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# 1️⃣ Create workbook and get first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# 2️⃣ Helper to add TIME_PERIOD conditional formatting
def add_time_period(sheet, cell_range, bg_color, period_type):
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type

# 3️⃣ Apply “Yesterday” rule (set cell background color)
add_time_period(
    worksheet,
    "I19:K20",
    Color.medium_sea_green,
    TimePeriodType.YESTERDAY
)

# 4️⃣ Fill sample dates (format cells by date)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))
cell.style.number = 30

cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))
cell.style.number = 30

# 5️⃣ Add label and auto‑fit column
worksheet.cells.get("I20").put_value("Yesterday")
worksheet.auto_fit_column(12)

# 6️⃣ Save the workbook
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Chạy script, mở file kết quả, và bạn sẽ thấy conditional formatting đang hoạt động.

## Các biến thể phổ biến và trường hợp đặc biệt

| Variation | How to implement | When to use |
|-----------|------------------|-------------|
| **Highlight “Today”** | Thay `TimePeriodType.YESTERDAY` bằng `TimePeriodType.TODAY` | Bảng điều khiển thời gian thực |
| **Multiple ranges** | Gọi `add_time_period` cho mỗi phạm vi, truyền màu khác nhau | Báo cáo phức tạp |
| **Dynamic date range** | Sử dụng `TimePeriodType.LAST_7_DAYS` hoặc `TimePeriodType.NEXT_MONTH` | Báo cáo cuộn |
| **Custom color** | Dùng `Color.from_argb(255, r, g, b)` để tạo bất kỳ màu nào | Định dạng đồng nhất với thương hiệu |

**Mẹo chuyên nghiệp:** Luôn đặt `condition.style.pattern = BackgroundType.SOLID` khi bạn muốn nền đặc; nếu không Excel có thể hiển thị gradient gây bất đồng nhất giữa các phiên bản.

## Kết luận

Bây giờ bạn đã biết cách **tạo Excel workbook python** các script **đặt màu nền cho ô**, áp dụng **excel conditional formatting python**, và **format cells by date** bằng Aspose.Cells. Ví dụ này bao phủ một kịch bản **date based conditional formatting**, nhưng cùng một mẫu có thể áp dụng cho bất kỳ quy tắc thời gian nào.

Tiếp theo, bạn có thể khám phá:

- Thêm data bars hoặc icon sets (`FormatConditionType.DATA_BAR`)  
- Kết hợp nhiều quy tắc conditional trên cùng một phạm vi  
- Xuất workbook ra PDF (`SaveFormat.PDF`) để báo cáo  

Hãy thoải mái thử nghiệm các màu sắc, phạm vi và loại thời gian khác nhau để phù hợp với nhu cầu báo cáo của bạn. Chúc lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ code hoàn chỉnh với giải thích chi tiết từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Làm chủ định dạng ô Excel và quản lý workbook với Aspose.Cells cho .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Tự động hoá Excel với Aspose.Cells .NET: Tạo Workbook & Đặt liên kết bên ngoài](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Cách tạo Named Ranges có phạm vi Workbook trong Excel bằng Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}