---
category: general
date: 2026-11-16
description: Tạo định dạng có điều kiện trong Excel bằng Python. Học cách thêm phạm
  vi định dạng có điều kiện, làm nổi bật ngày tháng và xây dựng một workbook một cách
  lập trình.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting
- create excel workbook python
- how to highlight dates
- add conditional formatting range
- add conditional formatting python
language: vi
lastmod: 2026-11-16
og_description: Tạo định dạng có điều kiện trong Excel bằng Python. Hướng dẫn này
  chỉ cách thêm phạm vi định dạng có điều kiện, làm nổi bật ngày tháng và tạo một
  sổ làm việc.
og_image_alt: Screenshot of Excel sheet with conditional formatting applied using
  Python
og_title: Tạo định dạng có điều kiện trong Excel bằng Python – hướng dẫn từng bước
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create conditional formatting in Excel using Python. Learn to add a
    conditional formatting range, highlight dates, and build a workbook programmatically.
  headline: How to create conditional formatting in Excel with Python
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Cách tạo định dạng có điều kiện trong Excel bằng Python
url: /vi/python/formatting/how-to-create-conditional-formatting-in-excel-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách tạo định dạng có điều kiện trong Excel bằng Python

Nếu bạn cần **tạo định dạng có điều kiện** trong một tệp Excel khi làm việc bằng Python, hướng dẫn này sẽ chỉ cho bạn cách thực hiện chi tiết. Bạn sẽ học cách **create excel workbook python**‑style, xác định phạm vi định dạng và làm nổi bật các ngày mà không rời khỏi IDE.

Định dạng có điều kiện cho phép bạn đánh dấu trực quan các ô thỏa mãn tiêu chí nhất định—hoàn hảo cho bảng điều khiển, báo cáo hoặc các bảng kiểm tra dữ liệu. Khi kết thúc hướng dẫn này, bạn sẽ có một workbook hoạt động đầy đủ, trong đó các ô có ngày “Yesterday” sẽ được tô màu hồng trong khi phần còn lại của phạm vi vẫn giữ màu xanh lá.

## Những gì bạn sẽ đạt được

* Xây dựng một workbook mới từ đầu.  
* Thêm một bộ sưu tập conditional‑format cho một khối ô cụ thể.  
* Áp dụng quy tắc **TIME_PERIOD** để làm nổi bật các ngày (kịch bản “cách làm nổi bật ngày”).  
* Lưu tệp dưới dạng workbook XLSX sẵn sàng cho quá trình xử lý tiếp theo.

**Yêu cầu trước**  
* Python 3.8+  
* `aspose-cells` gói Python (`pip install aspose-cells`)  
* Hiểu biết cơ bản về module `datetime` của Python  

---

## Cách tạo định dạng có điều kiện trong Python

Bước đầu tiên là thiết lập workbook và worksheet sẽ chứa các quy tắc định dạng.

```python
# Step 1: Import required classes and create a new workbook
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Instantiate a blank workbook and grab the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Optional: auto‑fit column 12 (L) to make the output readable
worksheet.auto_fit_column(12)
```

**Tại sao điều này quan trọng** – `Workbook` là điểm vào cho mọi thao tác Excel. Tạo workbook bằng chương trình thay thế bước “File → New” thủ công, cho phép tự động hoá quy trình báo cáo.

---

## Chuẩn bị bộ sưu tập conditional‑format – thêm phạm vi định dạng có điều kiện

Tiếp theo chúng ta xác định khối ô sẽ nhận quy tắc. Trong ví dụ này, phạm vi là **I19:K20**.

```python
# Step 2: Create a conditional‑format collection for the target range
conds = worksheet.conditional_formattings.add("I19:K20")

# Apply a base style (green background) that will show when no rule matches
conds[0].style.background_color = Color.medium_sea_green
conds[0].style.pattern = BackgroundType.SOLID
```

**Giải thích** – `conditional_formattings.add` đăng ký một bộ sưu tập mới gắn với chuỗi địa chỉ. Điều kiện đầu tiên (`conds[0]`) hoạt động như kiểu “mặc định”; quy tắc sau sẽ ghi đè khi đáp ứng tiêu chí.

---

## Thêm điều kiện TIME_PERIOD – cách làm nổi bật ngày

Bây giờ chúng ta thêm logic thực tế để xác định các ngày “Yesterday” và tô chúng màu hồng.

```python
# Step 3: Add a TIME_PERIOD condition that highlights cells dated “Yesterday”
idx = conds.add_condition(FormatConditionType.TIME_PERIOD)   # returns the new index
condition = conds[idx]

# Define the visual style for cells that satisfy the condition
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Set the rule to the built‑in YESTERDAY period
condition.time_period = TimePeriodType.YESTERDAY
```

**Tại sao sử dụng TIME_PERIOD?** – Aspose.Cells cung cấp các enumeration tích hợp sẵn như `YESTERDAY`, `TODAY`, và `LAST_WEEK`. Chúng đánh giá giá trị ngày của ô so với ngày hệ thống hiện tại, loại bỏ nhu cầu sử dụng công thức tùy chỉnh.

---

## Điền dữ liệu mẫu – minh họa quy tắc

Để xem định dạng hoạt động, chúng ta chèn một ngày phù hợp với quy tắc và một ngày không phù hợp.

```python
# Step 4: Populate sample dates so the rule can be seen

# Cell I19 gets a date that is “yesterday” relative to 2008‑07‑31
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))  # yesterday for the example
style = cell_i19.get_style()
style.number = 30                         # full date format (e.g., 7/30/2008)
cell_i19.set_style(style)

# Cell K20 gets a later date – it should stay green
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))   # a future date
style = cell_k20.get_style()
style.number = 30
cell_k20.set_style(style)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

**Lưu ý trường hợp biên** – Quy tắc `TIME_PERIOD` chỉ hoạt động với các ngày *thực* . Nếu một ô chứa văn bản (ví dụ, “N/A”), quy tắc sẽ bị bỏ qua, ngăn ngừa việc thay đổi màu không mong muốn.

---

## Lưu workbook – add conditional formatting python

Cuối cùng, ghi workbook ra đĩa. Tệp có thể mở trong bất kỳ chương trình bảng tính nào để xác minh màu sắc.

```python
# Step 5: Save the workbook
output_path = "TimePeriodExample.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

**Kết quả mong đợi**  

| I19 (xanh → hồng) | J19 (xanh) | K19 (xanh) |
|--------------------|------------|------------|
| 7/30/2008 (hôm qua) | – | – |
| **I20**: nhãn “Yesterday” | – | – |
| I21‑K21 (xanh)    | – | – |

Ô **I19** hiển thị nền màu hồng vì ngày của nó khớp với khoảng thời gian “Yesterday”, trong khi **K20** vẫn giữ màu xanh.

---

## Câu hỏi thường gặp và mẹo thực tế

* **Tôi có thể sử dụng phạm vi ngày tùy chỉnh thay vì khoảng thời gian tích hợp không?**  
  Có. Thay thế `condition.time_period` bằng `condition.formula1 = "TODAY()-1"` và đặt `condition.type = FormatConditionType.FORMULA`.

* **Nếu workbook của tôi đã chứa dữ liệu thì sao?**  
  Sử dụng `worksheet.cells.import_data` để tải dữ liệu hàng loạt trước khi thêm bộ sưu tập định dạng có điều kiện.

* **Hiệu năng với các sheet lớn?**  
  Thêm nhiều điều kiện có thể làm chậm quá trình render. Nhóm các ô có cùng quy tắc vào một phạm vi duy nhất (ví dụ, “A1:C1000”) để giảm số lượng điều kiện.

* **Tính tương thích đa nền tảng?**  
  Tệp XLSX được tạo tuân theo tiêu chuẩn Office Open XML, vì vậy nó hoạt động trên các ứng dụng bảng tính Windows, macOS và Linux.

---

## Kết luận

Bây giờ bạn đã biết cách **tạo định dạng có điều kiện** trong một workbook Excel bằng Python. Hướng dẫn đã bao gồm việc tạo workbook, xác định **add conditional formatting range**, áp dụng quy tắc **how to highlight dates**, và lưu tệp — tất cả đều bằng cách **add conditional formatting python** do Aspose.Cells cung cấp.

Từ đây bạn có thể:

* Mở rộng bộ quy tắc với các giá trị `TimePeriodType` khác (ví dụ, `TODAY`, `LAST_MONTH`).  
* Kết hợp nhiều điều kiện trên cùng một phạm vi để có dấu hiệu trực quan phong phú hơn.  
* Tích hợp quy trình này vào các pipeline báo cáo tự động hoặc dịch vụ web.

Chúc lập trình vui vẻ, và hãy tự do thử nghiệm các màu sắc, phạm vi và logic ngày khác nhau để phù hợp với nhu cầu báo cáo của bạn!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên đều có các ví dụ mã hoạt động đầy đủ kèm theo giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Tạo Excel workbook Python định dạng có điều kiện ngày](/cells/english/python/formatting/create-excel-workbook-python-date-conditional-formatting/)
- [Cách áp dụng định dạng có điều kiện thời gian trong Excel bằng Python](/cells/english/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/)
- [Tạo Excel Workbook Python – Hướng dẫn đầy đủ về Styling & Conditional Formatting](/cells/english/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}