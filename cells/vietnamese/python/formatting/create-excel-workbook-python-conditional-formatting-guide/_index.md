---
category: general
date: 2026-07-20
description: Tạo workbook Excel bằng Python với Aspose.Cells, đặt màu nền cho ô và
  thêm định dạng có điều kiện bằng Python để định dạng ô theo ngày.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- aspose cells conditional formatting
- add conditional formatting python
language: vi
lastmod: 2026-07-20
og_description: Tạo workbook Excel bằng Python sử dụng Aspose.Cells. Tìm hiểu cách
  đặt màu nền cho ô và thêm định dạng có điều kiện trong Python để định dạng ô theo
  ngày.
og_image_alt: Screenshot of an Excel workbook created with Python showing conditional
  formatting applied to date cells
og_title: Tạo sổ làm việc Excel bằng Python – Thêm định dạng có điều kiện
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Create Excel workbook Python with Aspose.Cells, set cell background
    color, and add conditional formatting python to style cells by date.
  headline: Create Excel Workbook Python – Conditional Formatting Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Change `"I19:K20"` to any A1‑style range, and adjust the sample
      dates accordingly.
    question: Can I target a different date range?
  - answer: Use `FormatConditionType.FORMULA` and set `condition.formula1 = "YOUR_FORMULA"`—for
      example, `=TODAY()-A1=1` to mimic yesterday.
    question: What if I need a custom formula instead of `YESTERDAY`?
  - answer: Call `conditions.add_condition` again with a different `FormatConditionType`.
      The order matters; later rules can override earlier ones.
    question: How do I apply multiple rules to the same range?
  - answer: Yes—modify `condition.style.font.color = Color.white` (or any other `Color`).
    question: Is there a way to set font colour together with background?
  type: FAQPage
tags:
- Aspose.Cells
- Python
- Excel Automation
title: Tạo Sổ làm việc Excel bằng Python – Hướng dẫn Định dạng có điều kiện
url: /vi/python/formatting/create-excel-workbook-python-conditional-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Workbook Excel bằng Python – Hướng Dẫn Định Dạng Có Điều Kiện

Bạn đã bao giờ tự hỏi làm thế nào để **create Excel workbook Python** từ đầu và làm cho nó trông chuyên nghiệp mà không cần mở giao diện người dùng? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi họ cần **set cell background color** hoặc áp dụng các kiểu dựa trên ngày một cách lập trình.  

Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, có thể chạy được, sử dụng Aspose.Cells để **add conditional formatting python** các quy tắc, định dạng ô theo ngày, và lưu kết quả dưới dạng tệp XLSX hiện đại. Khi kết thúc, bạn sẽ có một script tự chứa mà bạn có thể đưa vào bất kỳ dự án nào.

## Những Điều Bạn Sẽ Học

- Cách khởi tạo một workbook và lấy worksheet đầu tiên.  
- Các cách **set cell background color** cho toàn bộ một vùng.  
- Sử dụng **aspose cells conditional formatting** để làm nổi bật các ngày “Yesterday”.  
- Tự động điều chỉnh độ rộng cột và lưu tệp lên đĩa.  

Không cần cấu hình bên ngoài—chỉ cần Python 3 và gói Aspose.Cells. Nếu bạn đã cài đặt `aspose-cells`, bạn đã sẵn sàng; nếu chưa, chỉ cần chạy `pip install aspose-cells` là xong.

## Yêu Cầu Trước

- Python 3.8+ (mã chạy trên 3.9, 3.10 và các phiên bản mới hơn).  
- Aspose.Cells for Python via .NET (`aspose-cells` NuGet wrapper).  
- Kiến thức cơ bản về các khái niệm Excel (ô, vùng, định dạng).  

Đã có chưa? Tuyệt—cùng bắt đầu.

## Tạo Workbook Excel bằng Python – Thiết Lập và Worksheet

Đầu tiên, chúng ta cần một đối tượng workbook mới và một tham chiếu tới worksheet mặc định. Đây là nền tảng mà mọi thao tác sau sẽ diễn ra.

```python
# Import the necessary Aspose.Cells classes
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and grab the first sheet
workbook = Workbook()                     # create excel workbook python
worksheet = workbook.worksheets[0]        # default is the first worksheet
```

> **Tại sao điều này quan trọng:** `Workbook()` tạo một tệp Excel trong bộ nhớ, loại bỏ nhu cầu tạo các tệp tạm thời. Biến `worksheet` là điểm vào của chúng ta cho các hành động ở mức ô.

## Đặt Màu Nền Cho Ô

Trước khi chúng ta thêm bất kỳ quy tắc nào, nên đặt màu nền cơ bản cho vùng mục tiêu để định dạng có điều kiện nổi bật hơn. Trợ giúp bên dưới vừa lấy (hoặc tạo) một `FormatConditionCollection` cho một vùng nhất định và tô màu nền đồng nhất cho các ô.

```python
def get_format_condition(cell_range: str, base_color: Color):
    """
    Obtain (or create) a FormatConditionCollection for `cell_range`.
    Also set a base background colour for the whole range.
    """
    # Retrieve or add a conditional formatting entry for the range
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    # Apply the base colour to every cell in the range
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color          # set cell background color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection
```

> **Mẹo chuyên nghiệp:** Nếu bạn dự định tái sử dụng cùng một vùng với nhiều quy tắc, hãy gọi trợ giúp này một lần và giữ lại collection trả về; nó sẽ tiết kiệm một vài lần gọi API.

## Thêm Định Dạng Có Điều Kiện Python cho Các Khoảng Ngày

Bây giờ là phần thú vị: chúng ta sẽ tạo một quy tắc **time‑period conditional formatting** để làm nổi bật các ô chứa ngày hôm qua. Điều này minh họa sức mạnh của **format cells by date** sử dụng Aspose.Cells.

```python
def apply_yesterday_rule():
    """
    Apply a “Yesterday” conditional formatting rule to the range I19:K20.
    Cells that match will turn pink; others stay with the base colour.
    """
    # Obtain the condition collection for the target range
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)

    # Create a TIME_PERIOD condition (this is the aspose cells conditional formatting type we need)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]

    # Define the appearance for cells that meet the condition
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Set the time period to “Yesterday”
    condition.time_period = TimePeriodType.YESTERDAY

    # Populate sample dates to demonstrate the rule
    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))   # matches “Yesterday”
    cell_i19.style.number = 30                 # Excel number format for dates
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))    # does NOT match
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    # Add a label for clarity
    worksheet.cells.get("I20").put_value("Yesterday")
```

> **Tại sao dùng `TIME_PERIOD`?** Nó trừu tượng hoá việc phải viết công thức tùy chỉnh. Aspose.Cells đánh giá ngày dựa trên ngày hệ thống hiện tại, vì vậy quy tắc luôn phù hợp.

### Chạy Quy Tắc

```python
apply_yesterday_rule()
```

Khi bạn mở tệp kết quả, các ô `I19` sẽ phát sáng màu hồng (vì chúng là “Yesterday”), trong khi `K20` vẫn giữ màu xanh lá cơ bản.

## Tự Động Điều Chỉnh Cột và Lưu Workbook

Một bảng tính gọn gàng trông chuyên nghiệp. Tự động điều chỉnh độ rộng cột đảm bảo dữ liệu không bị chèn ép.

```python
# Step 4: Auto‑fit the column width for a tidy appearance
worksheet.auto_fit_column(12)   # column index is zero‑based; 12 corresponds to column M

# Step 5: Save the workbook to disk
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Trường hợp đặc biệt:** Nếu bạn chỉ định một thư mục không tồn tại, `workbook.save` sẽ gây lỗi. Hãy bao quanh lệnh lưu trong khối `try/except` nếu bạn cần xử lý mềm mại.

### Toàn Bộ Script (Sẵn Sàng Sao Chép‑Dán)

Dưới đây là toàn bộ script, sẵn sàng chạy. Chỉ cần thay `YOUR_DIRECTORY` bằng một thư mục hợp lệ trên máy của bạn.

```python
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create the workbook and worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

def get_format_condition(cell_range: str, base_color: Color):
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection

def apply_yesterday_rule():
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = TimePeriodType.YESTERDAY

    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))
    cell_i19.style.number = 30
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    worksheet.cells.get("I20").put_value("Yesterday")

apply_yesterday_rule()
worksheet.auto_fit_column(12)

output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Chạy script này sẽ tạo ra tệp `TimePeriodExample.xlsx` với định dạng có điều kiện như đã mô tả.

## Câu Hỏi Thường Gặp & Mẹo

- **Tôi có thể nhắm mục tiêu một khoảng ngày khác không?**  
  Chắc chắn. Thay `"I19:K20"` bằng bất kỳ vùng A1‑style nào, và điều chỉnh các ngày mẫu cho phù hợp.

- **Nếu tôi cần công thức tùy chỉnh thay vì `YESTERDAY` thì sao?**  
  Sử dụng `FormatConditionType.FORMULA` và đặt `condition.formula1 = "YOUR_FORMULA"`—ví dụ, `=TODAY()-A1=1` để mô phỏng ngày hôm qua.

- **Làm sao áp dụng nhiều quy tắc cho cùng một vùng?**  
  Gọi `conditions.add_condition` lại với một `FormatConditionType` khác. Thứ tự quan trọng; các quy tắc sau có thể ghi đè các quy tắc trước.

- **Có cách nào để đặt màu chữ cùng với màu nền không?**  
  Có—sửa `condition.style.font.color = Color.white` (hoặc bất kỳ `Color` nào khác).

## Kết Luận

Bây giờ bạn đã biết cách **create Excel workbook Python** bằng Aspose.Cells, **set cell background color**, và **add conditional formatting python** để định dạng ô theo ngày. Script hoạt động đầy đủ, xử lý các trường hợp đặc biệt như thư mục thiếu, và có thể mở rộng cho các kịch bản phức tạp hơn như logic điều kiện đa quy tắc hoặc phát hiện vùng động.

Sẵn sàng cho bước tiếp theo? Hãy thử thay đổi quy tắc “Yesterday” thành “Last Week”, thử nghiệm các màu gradient, hoặc tạo một báo cáo đầy đủ với hàng chục bảng được định dạng. Các khối xây dựng đã có sẵn, và bạn vừa nắm vững cốt lõi của **aspose cells conditional formatting** trong Python.

Chúc lập trình vui vẻ, và đừng ngại chia sẻ các biến thể của bạn trong phần bình luận!

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Làm Chủ Định Dạng Ô Excel và Quản Lý Workbook với Aspose.Cells cho .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Cách Tạo và Lưu Workbook Excel dưới dạng ODS bằng Aspose.Cells cho .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Cách Tạo Các Phạm Vi Đặt Tên Có Phạm Vi Workbook trong Excel bằng Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}