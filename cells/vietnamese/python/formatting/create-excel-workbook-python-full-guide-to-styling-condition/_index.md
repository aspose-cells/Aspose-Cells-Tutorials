---
category: general
date: 2026-07-06
description: Tạo workbook Excel bằng Python với mã để đặt màu nền cho ô, thiết lập
  kiểu ô bằng chương trình, và thêm định dạng có điều kiện trong Python để làm nổi
  bật ngày hiện tại.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- set cell style programmatically
- highlight today date excel
- add conditional formatting python
language: vi
lastmod: 2026-07-06
og_description: Tạo nhanh workbook Excel bằng Python. Tìm hiểu cách đặt màu nền cho
  ô, thiết lập kiểu ô bằng chương trình, và thêm định dạng có điều kiện trong Python
  để làm nổi bật ngày hiện tại.
og_image_alt: Screenshot of an Excel workbook created with Python showing colored
  cells and today’s date highlighted
og_title: Tạo Workbook Excel bằng Python – Định dạng ô & Tô sáng ngày hôm nay
schemas:
- author: Aspose
  dateModified: '2026-07-06'
  description: Create Excel workbook Python with code to set cell background color,
    set cell style programmatically, and add conditional formatting python for highlighting
    today’s date.
  headline: Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting
  type: TechArticle
- description: Create Excel workbook Python with code to set cell background color,
    set cell style programmatically, and add conditional formatting python for highlighting
    today’s date.
  name: Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting
  steps:
  - name: Converting a range like `"A1:C3"` into a `CellArea`.
    text: Converting a range like `"A1:C3"` into a `CellArea`.
  - name: Filling every cell in that area with a sequential number (just for demo
      purposes).
    text: Filling every cell in that area with a sequential number (just for demo
      purposes).
  - name: Applying a solid **set cell background color**.
    text: Applying a solid **set cell background color**.
  - name: Adding a conditional rule that **highlight today date excel**.
    text: Adding a conditional rule that **highlight today date excel**.
  type: HowTo
tags:
- Python
- Aspose.Cells
- Excel Automation
- Conditional Formatting
title: Tạo sổ làm việc Excel bằng Python – Hướng dẫn toàn diện về Định dạng và Định
  dạng có điều kiện
url: /vi/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Workbook Excel bằng Python – Hướng Dẫn Toàn Diện về Định Dạng & Định Dạng Có Điều Kiện

Bạn đã bao giờ tự hỏi làm thế nào để **tạo Excel workbook Python** từ đầu mà không cần mở Excel? Bạn không phải là người duy nhất. Nhiều nhà phát triển cần tạo báo cáo, bảng điều khiển, hoặc thậm chí các bản ghi dữ liệu đơn giản một cách tự động, và việc làm này bằng chương trình sẽ tiết kiệm hàng giờ công việc thủ công.

Trong hướng dẫn này, chúng ta sẽ đi qua toàn bộ quy trình: từ việc tạo một workbook mới, đến **đặt màu nền cho ô**, đến **đặt kiểu ô bằng chương trình**, và cuối cùng là **đánh dấu ngày hiện tại trong Excel** bằng **thêm định dạng có điều kiện python**. Khi hoàn thành, bạn sẽ có một script sẵn sàng chạy, tạo ra file .xlsx được định dạng đẹp mắt trong vài giây.

---

## Những gì bạn sẽ xây dựng

- Một file Excel mới với một vài ô đã được điền dữ liệu.
- Các ô được tô màu nền tùy chỉnh.
- Giá trị số và ngày được định dạng với kiểu số cụ thể.
- Một quy tắc có điều kiện tự động đánh dấu ô chứa ngày hiện tại.

Không cần cài đặt Excel bên ngoài—Aspose.Cells for Python via .NET sẽ thực hiện mọi công việc nặng.

---

## Yêu cầu trước

| Yêu cầu | Lý do quan trọng |
|-------------|----------------|
| Python 3.8+ | Cú pháp hiện đại và hỗ trợ type hints |
| `aspose-cells` package | Thư viện cốt lõi để thao tác workbook |
| `aspose-pydrawing` (được cài đặt cùng Aspose.Cells) | Cung cấp lớp `Color` |
| Kiến thức cơ bản về các khái niệm Excel (ô, phạm vi, định dạng) | Giúp quá trình học diễn ra suôn sẻ hơn |

Cài đặt thư viện bằng:

```bash
pip install aspose-cells
```

---

## Bước 1: Khởi tạo Workbook và Worksheet

Điều đầu tiên bạn làm khi **create excel workbook python** là tạo một đối tượng `Workbook` và lấy worksheet mặc định. Hãy nghĩ workbook như toàn bộ file Excel, trong khi worksheet là một tab duy nhất bên trong nó.

```python
from aspose.cells import Workbook

# Create a new workbook – this is our empty Excel file
book = Workbook()

# Grab the first (default) worksheet
sheet = book.worksheets[0]
```

> **Mẹo chuyên nghiệp:** Nếu bạn cần nhiều sheet, hãy dùng `book.worksheets.add("MySheet")` để thêm các tab mới.

---

## Bước 2: Lớp Trợ Giúp cho Định Dạng & Định Dạng Có Điều Kiện

Dưới đây là một lớp `ConditionalFormatting` gọn gàng nhưng đầy đủ. Nó gói gọn các công việc lặp lại:

1. Chuyển đổi một phạm vi như `"A1:C3"` thành một `CellArea`.
2. Điền số thứ tự vào mỗi ô trong phạm vi (chỉ để minh họa).
3. Áp dụng màu nền **set cell background color** đặc.
4. Thêm quy tắc có điều kiện để **highlight today date excel**.

```python
from aspose.cells import (
    CellArea, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat, CellsHelper
)
from aspose.pydrawing import Color
from datetime import datetime

class ConditionalFormatting:
    """
    Utility class that demonstrates how to:
    • set cell background color
    • set cell style programmatically
    • add conditional formatting python
    """
    def __init__(self, worksheet):
        self._sheet = worksheet

    def get_format_condition(self, cell_range: str, color: Color):
        """
        Creates a conditional formatting object for the given range
        and fills the range with a background color.
        """
        index = self._sheet.conditional_formattings.add()
        cf = self._sheet.conditional_formattings[index]

        # Convert "A1:C3" → CellArea object
        area = self.get_cell_area_by_name(cell_range)
        cf.add_area(area)

        # Paint the whole area with the supplied color
        self.fill_cell(cell_range, color)
        return cf

    def fill_cell(self, cell_range: str, color: Color):
        """
        Populates each cell in the range with an incrementing integer
        and applies the supplied background color.
        """
        area = self.get_cell_area_by_name(cell_range)
        counter = 0
        for col in range(area.start_column, area.end_column + 1):
            for row in range(area.start_row, area.end_row + 1):
                cell = self._sheet.cells.get(row, col)

                # Apply background only if a real color is supplied
                if color != Color.empty:
                    style = cell.get_style()
                    style.foreground_color = color
                    style.pattern = BackgroundType.SOLID
                    cell.set_style(style)

                cell.put_value(counter)
                counter += 1

    @staticmethod
    def get_cell_area_by_name(name: str) -> CellArea:
        """
        Parses an Excel‑style address (e.g. "B2:D4") into a CellArea.
        """
        area = CellArea()
        parts = name.replace("$", "").split(':')

        start_row, start_col = CellsHelper.cell_name_to_index(parts[0])
        area.start_row = start_row
        area.start_column = start_col

        if len(parts) == 2:
            end_row, end_col = CellsHelper.cell_name_to_index(parts[1])
            area.end_row = end_row
            area.end_column = end_col
        else:
            area.end_row = start_row
            area.end_column = start_col
        return area

    # -----------------------------------------------------------------
    # Step 2: Add conditional formatting for TODAY
    # -----------------------------------------------------------------
    def add_time_period_1(self):
        """
        Demonstrates add conditional formatting python that highlights
        cells containing today’s date.
        """
        # 1️⃣ Create a formatting range and give it a neutral background
        cf = self.get_format_condition("I1:K2", Color.light_slate_gray)

        # 2️⃣ Add a TIME_PERIOD condition (Today)
        idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
        cond = cf[idx]
        cond.time_period = TimePeriodType.TODAY
        cond.style.background_color = Color.pink
        cond.style.pattern = BackgroundType.SOLID

        # 3️⃣ Populate the cells with date values
        # Cell I1 – today’s date, formatted as a date
        cell = self._sheet.cells.get("I1")
        style = cell.get_style()
        style.number = 30               # 30 = “mm-dd-yy” style in Aspose
        cell.set_style(style)
        cell.put_value(datetime.today())

        # Cell K2 – an arbitrary past date for contrast
        self._sheet.cells.get("K2").put_value(datetime(2008, 7, 30))

        # Cell I2 – a label so the reader knows what’s being highlighted
        self._sheet.cells.get("I2").put_value("Today")
```

### Tại sao lại có lớp trợ giúp?

- **Tái sử dụng:** Bạn có thể gọi `add_time_period_1()` cho bất kỳ worksheet nào mà không cần viết lại logic.
- **Rõ ràng:** Mỗi phương thức thực hiện một nhiệm vụ – đặc điểm của code sạch.
- **Mở rộng:** Muốn thêm quy tắc? Chỉ cần thêm một phương thức khác theo cùng mẫu.

---

## Bước 3: Áp dụng Định Dạng và Lưu File

Bây giờ chúng ta gắn mọi thứ lại với nhau: khởi tạo lớp trợ giúp, chạy quy trình định dạng, và cuối cùng ghi workbook ra đĩa.

```python
# Instantiate the helper with our worksheet
formatter = ConditionalFormatting(sheet)

# Fill a demo range with numbers and a light blue background
formatter.get_format_condition("A1:C3", Color.light_sky_blue)

# Add the “today” conditional rule
formatter.add_time_period_1()

# Save the workbook – choose any location you like
output_path = "styled_workbook.xlsx"
book.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

Khi bạn mở *styled_workbook.xlsx* bạn sẽ thấy:

- Các ô **A1:C3** được đánh số 0‑8 với nền màu xanh da trời nhạt.
- Ô **I1** hiển thị ngày hiện tại với nền màu hồng (nhờ quy tắc có điều kiện).
- Ô **K2** hiển thị ngày tĩnh *2008‑07‑30* để so sánh.
- Ô **I2** chứa văn bản “Today”.

Đó là dấu hiệu trực quan chính xác những gì yêu cầu **highlight today date excel** đề ra.

---

## Bước 4: Đi sâu hơn – Tùy chỉnh Kiểu

Nếu bạn cần điều chỉnh phông chữ, viền, hoặc định dạng số, bạn có thể mở rộng phương thức `fill_cell` hoặc tạo một lớp trợ giúp mới:

```python
def apply_custom_style(cell, font_name="Calibri", font_size=11, bold=False):
    style = cell.get_style()
    style.font.name = font_name
    style.font.size = font_size
    style.font.bold = bold
    cell.set_style(style)
```

Bạn có thể gọi `apply_custom_style(cell, bold=True)` trong vòng lặp để **set cell style programmatically** cho mọi ô trong một phạm vi.

---

## Các vấn đề thường gặp & Cách tránh

| Triệu chứng | Nguyên nhân có thể | Cách khắc phục |
|---------|--------------|-----|
| Các ô vẫn trắng mặc dù đã dùng `Color.light_sky_blue` | Kiểu chưa được áp dụng sau khi đặt `foreground_color` | Luôn gọi `cell.set_style(style)` sau khi chỉnh sửa đối tượng style. |
| Quy tắc có điều kiện không bao giờ kích hoạt | `style.number` chưa được đặt cho ô ngày, vì vậy Excel coi giá trị là chuỗi | Đặt `style.number = 30` (hoặc bất kỳ định dạng ngày nào) trước `cell.put_value(datetime…)`. |
| Workbook lưu dưới dạng .xls mặc dù đã dùng `SaveFormat.XLSX` | Phiên bản Aspose cũ mặc định lưu ở định dạng legacy | Nâng cấp lên phiên bản mới nhất của gói `aspose-cells`. |
| Phạm vi như `"A1"` gây lỗi chỉ mục | Dùng `cells.get("A1")` trên sheet chưa được khởi tạo | Đảm bảo worksheet tồn tại (nó đã có ngay sau `Workbook()`), hoặc dùng `cells.get(row, col)` với chỉ số bắt đầu từ 0. |

---

## Script đầy đủ để Copy‑Paste

Dưới đây là **toàn bộ** script bạn có thể sao chép vào file có tên `create_excel.py` và chạy ngay lập tức.

```python
# create_excel.py
from aspose.cells import (
    Workbook, CellArea, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat, CellsHelper
)
from aspose.pydrawing import Color
from datetime import datetime

class ConditionalFormatting:
    """Utility for styling cells and adding conditional formatting."""
    def __init__(self, worksheet):
        self._sheet = worksheet

    def get_format_condition(self, cell_range: str, color: Color):
        index = self._sheet.conditional_formattings.add()
        cf = self._sheet.conditional_formattings[index]
        area = self.get_cell_area_by_name(cell_range)
        cf.add_area(area)
        self.fill_cell(cell_range, color)
        return cf

    def fill_cell(self, cell_range: str, color: Color):
        area = self.get_cell_area_by_name(cell_range)
        counter = 0
        for col in range(area.start_column, area.end_column + 1):
            for row in range(area.start_row, area.end_row + 1):
                cell = self._sheet.cells.get(row, col)
                if color != Color.empty:
                    style = cell.get_style()
                    style.foreground_color = color
                    style.pattern = BackgroundType.SOLID
                    cell.set_style(style)
                cell.put_value(counter)
                counter += 1

    @staticmethod
    def get_cell_area_by_name(name:


## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây liên quan chặt chẽ và mở rộng các kỹ thuật được trình bày trong bài viết này. Mỗi tài nguyên đều bao gồm mã nguồn hoàn chỉnh cùng các giải thích chi tiết từng bước, giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Excel Automation with Aspose.Cells .NET: Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Excel Automation: Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}