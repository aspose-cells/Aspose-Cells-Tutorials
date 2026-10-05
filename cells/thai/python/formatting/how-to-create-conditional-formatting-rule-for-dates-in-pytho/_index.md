---
category: general
date: 2026-08-24
description: สร้างกฎการจัดรูปแบบตามเงื่อนไขใน Python โดยใช้ Aspose.Cells เพื่อเน้นวันที่
  พร้อมการปรับคอลัมน์อัตโนมัติและการจัดรูปแบบสีพื้นหลัง.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting rule
- auto fit column
- conditional formatting by date
- background color conditional format
- date based conditional format
language: th
lastmod: 2026-08-24
og_description: สร้างกฎการจัดรูปแบบตามเงื่อนไขใน Python ด้วย Aspose.Cells เรียนรู้วิธีเน้นวันที่
  ตั้งค่าสีพื้นหลัง และปรับขนาดคอลัมน์อัตโนมัติด้วยเพียงไม่กี่บรรทัดของโค้ด.
og_image_alt: Screenshot of an Excel sheet where yesterday's date cells are highlighted
  in pink
og_title: สร้างกฎการจัดรูปแบบตามเงื่อนไขสำหรับวันที่ใน Python – คู่มือขั้นตอนโดยละเอียด
schemas:
- author: Aspose
  dateModified: '2026-08-24'
  description: Create conditional formatting rule in Python using Aspose.Cells to
    highlight dates, with auto‑fit column and background color formatting.
  headline: How to create conditional formatting rule for dates in Python
  type: TechArticle
tags:
- Aspose.Cells
- Python
- Excel automation
- Conditional formatting
title: วิธีสร้างกฎการจัดรูปแบบตามเงื่อนไขสำหรับวันที่ใน Python
url: /th/python/formatting/how-to-create-conditional-formatting-rule-for-dates-in-pytho/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีสร้างกฎการจัดรูปแบบตามเงื่อนไขสำหรับวันที่ใน Python

หากคุณต้องการ **create conditional formatting rule** ที่ตอบสนองต่อวันที่ คู่มือนี้จะแสดงให้คุณเห็นอย่างชัดเจนว่าทำอย่างไรด้วย Aspose.Cells for Python ไม่ว่าคุณจะสร้างแดชบอร์ดรายงานหรือสเปรดชีตอัตโนมัติ คุณจะได้เห็นวิธีไฮไลต์วันที่ของเมื่อวาน, ใช้สีพื้นหลังแบบกำหนดเอง, และ **auto fit column** ความกว้างเพื่อให้ผลลัพธ์ดูเรียบหรู.

ในบทแนะนำนี้ เราจะครอบคลุม **conditional formatting by date**, แสดงตัวอย่าง **background color conditional format**, และสรุปด้วยการบันทึกเวิร์กบุ๊กเป็นไฟล์ XLSX เมื่อเสร็จคุณจะมีฟังก์ชันช่วยเหลือที่สามารถนำกลับมาใช้ใหม่ได้และปรับให้เข้ากับ **date based conditional format** ใด ๆ ที่คุณต้องการ.

## สิ่งที่คุณจะได้เรียนรู้

* ตั้งค่า workbook และ worksheet ด้วย Aspose.Cells
* เขียนฟังก์ชันช่วยเหลือที่เพิ่ม **date based conditional format** ให้กับช่วงเซลล์ใด ๆ
* เติมข้อมูลเซลล์ด้วยวันที่ตัวอย่างเพื่อให้กฎสามารถประเมินได้
* ใช้ **auto fit column** เพื่อทำให้เนื้อหาอ่านง่าย
* บันทึก workbook และตรวจสอบเซลล์ที่ถูกไฮไลต์

ข้อกำหนดเบื้องต้นเดียวคือสภาพแวดล้อม Python ที่ทำงานได้พร้อมกับแพคเกจ `aspose-cells` ที่ติดตั้งแล้ว.

## ข้อกำหนดเบื้องต้น

| ข้อกำหนด | รายละเอียด |
|-------------|---------|
| Python | 3.8+ |
| Aspose.Cells for Python via Java | `pip install aspose-cells` |
| ความรู้พื้นฐานเกี่ยวกับแนวคิดของ Excel | worksheets, cells, formatting |
| ทางเลือก: IDE (VS Code, PyCharm, ฯลฯ) | any editor that can run Python scripts |

## ขั้นตอนที่ 1: สร้าง workbook และรับ worksheet แรก

ขั้นตอนแรกคือการเตรียมวัตถุที่พร้อมสำหรับ **create conditional formatting rule**: `Workbook` และ `Worksheet` เริ่มต้นของมัน วัตถุเหล่านี้เป็นจุดเริ่มต้นสำหรับการดำเนินการต่อ ๆ ไปทั้งหมด.

```python
# Step 1 – initialize workbook and worksheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create a new, empty workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*ทำไมสิ่งนี้ถึงสำคัญ:* `Workbook` ถือไฟล์ Excel ทั้งหมด, ส่วน `Worksheet` คือที่คุณใช้กำหนดเซลล์, สไตล์, และ **conditional formatting by date** หากไม่มีวัตถุเหล่านี้ โค้ดส่วนที่เหลือจะไม่มีที่ทำงาน.

## ขั้นตอนที่ 2: สร้างฟังก์ชันช่วยเหลือเพื่อเพิ่ม conditional format ประเภท TIME_PERIOD

แทนที่จะทำซ้ำโค้ดพื้นฐานเดียวกันสำหรับแต่ละช่วง เราจะบรรจุตรรกะไว้ในฟังก์ชันช่วยเหลือ ฟังก์ชันนี้จะผูก **background color conditional format** ที่เปลี่ยนสีเซลล์ตาม `TimePeriodType` (เช่น Yesterday, Today, LastWeek).

```python
def add_time_period_condition(cell_range: str, bg_color: Color, period: TimePeriodType):
    """
    Attach a TIME_PERIOD conditional format to `cell_range`.
    The rule highlights cells that fall within `period` using `bg_color`.

    Args:
        cell_range: A1‑style range string, e.g., "I19:K20".
        bg_color:   Desired background color for matching cells.
        period:     Aspose.Cells TimePeriodType enum value.
    Returns:
        The FormatConditionCollection for further customization if needed.
    """
    # 1️⃣ Attach a new ConditionalFormatting block to the specified range
    worksheet.conditional_formattings.add(cell_range)

    # 2️⃣ Grab the collection of conditions for that block
    conditions = worksheet.conditional_formattings[-1].format_conditions

    # 3️⃣ (Optional) Set a default background for the whole range
    conditions.back_color = bg_color

    # 4️⃣ Add a TIME_PERIOD condition and configure its appearance
    idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[idx]

    # Apply the visual style – pink background in this example
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Define which period triggers the formatting
    condition.time_period = period

    return conditions
```

*ทำไมเราถึงใช้ฟังก์ชันช่วยเหลือ:* มันแยกตรรกะของ **date based conditional format** ทำให้โค้ดอ่านง่ายขึ้น, ทดสอบได้, และนำกลับมาใช้ใหม่ได้ในหลายชีตหรือโครงการ.

## ขั้นตอนที่ 3: ใช้กฎการจัดรูปแบบตามเงื่อนไขกับช่วงเฉพาะ

ตอนนี้เราจะใช้ฟังก์ชันช่วยเหลือเพื่อไฮไลต์เซลล์ที่มีค่า “Yesterday”. นี่คือหัวใจของการทำงาน **create conditional formatting rule** ของเรา.

```python
# Step 3 – highlight cells I19:K20 that contain “Yesterday”
add_time_period_condition(
    cell_range="I19:K20",
    bg_color=Color.medium_sea_green,   # optional default background for the whole range
    period=TimePeriodType.YESTERDAY   # the date‑based trigger
)
```

เมื่อเปิด workbook, เซลล์ใดในช่วง `I19:K20` ที่วันที่ตรงกับวันที่ของเมื่อวานจะปรากฏด้วยสีเติมสีชมพู (สไตล์ที่เราตั้งค่าในฟังก์ชันช่วยเหลือ) พารามิเตอร์ `bg_color` แสดงวิธีที่คุณสามารถวางพื้นหลังเริ่มต้นไว้หลังสีตามเงื่อนไขได้หากต้องการ.

## ขั้นตอนที่ 4: เติมข้อมูลช่วงด้วยวันที่ตัวอย่าง

กฎตามเงื่อนไขจะมองเห็นได้เฉพาะหลังจาก worksheet มีข้อมูลที่ตรงกับเงื่อนไข เราจะใส่วันที่สองค่า: หนึ่งค่าที่ตรงกับ “Yesterday” และอีกค่าที่อยู่นอกช่วง.

```python
# Step 4 – insert sample dates for demonstration

# Cell I19 will match the YESTERDAY period
yesterday_cell = worksheet.cells.get("I19")
yesterday_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008 is “yesterday” relative to 31‑Jul‑2008
yesterday_cell.get_style().number = 30          # 30 = built‑in date format
yesterday_cell.set_style(yesterday_cell.get_style())

# Cell K20 will NOT match the period (it’s a later date)
outside_cell = worksheet.cells.get("K20")
outside_cell.put_value(datetime(2008, 8, 3))     # 03‑Aug‑2008 is outside “Yesterday”
outside_cell.get_style().number = 30
outside_cell.set_style(outside_cell.get_style())

# Optional label for clarity – not part of the rule
worksheet.cells.get("I20").put_value("Yesterday")
```

*ทำไมสิ่งนี้ถึงสำคัญ:* การใช้วัตถุ `datetime` ทำให้แน่ใจว่า Excel ถือค่าดังกล่าวเป็นวันที่จริง ซึ่งจำเป็นสำหรับการทำงานของ **conditional formatting by date** อย่างถูกต้อง รูปแบบตัวเลข (`30`) ทำให้เซลล์แสดงเป็นวันที่ที่เข้าใจได้.

## ขั้นตอนที่ 5: Auto‑fit คอลัมน์และบันทึก workbook

หลังจากข้อมูลและการจัดรูปแบบพร้อมแล้ว ขั้นตอนสุดท้ายคือการ **auto fit column** ความกว้างเพื่อให้วันที่แสดงเต็มที่ จากนั้นเราจะเขียนไฟล์ลงดิสก์.

```python
# Step 5 – adjust column width and save the file

# Auto‑fit column 12 (the column that contains our sample data)
worksheet.auto_fit_column(12)

# Save the workbook as an XLSX file
output_path = "YOUR_DIRECTORY/TimePeriodDemo.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

คำสั่ง `auto_fit_column` ตรวจสอบเนื้อหาที่ยาวที่สุดในคอลัมน์ 12 (ซึ่งสอดคล้องกับคอลัมน์ **L** ใน Excel) แล้วขยายความกว้างตามนั้น ขั้นตอนเล็ก ๆ นี้ป้องกันวันที่ถูกตัดและทำให้ **background color conditional format** ปรากฏอย่างชัดเจน.

### ผลลัพธ์ที่คาดหวัง

When you open `TimePeriodDemo.out.xlsx`:

| I19 (date) | I20 (label) | K20 (date) |
|------------|------------|------------|
| 30‑Jul‑2008 (highlighted pink) | Yesterday | 03‑Aug‑2008 (no highlight) |

* เซลล์ที่มีวันที่ของเมื่อวานแสดงพื้นหลังสีชมพูเพราะ **create conditional formatting rule** ตรงกับช่วง `YESTERDAY`.
* เซลล์อื่น ๆ คงพื้นหลังเริ่มต้น (หรือ `medium_sea_green` ที่คุณระบุไว้เป็นตัวเลือก).
* คอลัมน์ L ถูกขยายอัตโนมัติ ทำให้วันที่แสดงเต็มที่และอ่านง่าย.

## ความหลากหลายทั่วไปและกรณีขอบ

| สถานการณ์ | วิธีปรับโค้ด |
|-----------|-----------------------|
| **ไฮไลต์ “Today” แทน “Yesterday”** | แทนที่ `TimePeriodType.YESTERDAY` ด้วย `TimePeriodType.TODAY`. |
| **ใช้สีพื้นหลังอื่น** | เปลี่ยน `condition.style.background_color = Color.pink` เป็น `Color` ใดก็ได้ (เช่น `Color.light_sky_blue`). |
| **ใช้กฎกับช่วงที่ไม่ต่อเนื่อง** | เรียก `add_time_period_condition` หลายครั้งด้วยสตริง `cell_range` ที่ต่างกัน (เช่น `"A1:A10", "C1:C10"`). |
| **ทำงานกับ workbook ที่มีอยู่แล้ว** | โหลดไฟล์ด้วย `Workbook("myfile.xlsx")` แทนการสร้างใหม่. |
| **หลายเงื่อนไขตามวันที่บนช่วงเดียวกัน** | หลังจากเรียก `add_time_period_condition` ครั้งแรก ให้เพิ่มเงื่อนไขอีกอันด้วย `conditions.add_condition(FormatConditionType.TIME_PERIOD)` แล้วกำหนด `time_period` ที่ต่างกัน. |

## สรุป

คุณตอนนี้รู้วิธี **create conditional formatting rule** ที่ตอบสนองต่อวันที่, ใช้ **background color conditional format**, และ **auto fit column** ความกว้างด้วย Aspose.Cells for Python ฟังก์ชันช่วยเหลือทำให้ตรรกะถูกแยกออก ทำให้คุณสามารถนำรูปแบบเดียวกันไปใช้กับสถานการณ์ **conditional formatting by date** ใด ๆ ไม่ว่าจะเป็น “Yesterday”, “LastWeek”, หรือช่วงกำหนดเอง.

ต่อไปคุณอาจสำรวจ:

* เพิ่ม **icon sets** หรือ **data bars** ควบคู่กับกฎวันที่.
* สร้างรายงานไดนามิกที่ดึงวันที่จากฐานข้อมูล.
* รวมหลายกฎ **date based conditional format** บนชีตเดียว.

Feel free to experiment with different colors, periods, and ranges to fit your project’s needs. Happy coding!

## คุณควรเรียนรู้อะไรต่อไป?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [ทำความเข้าใจการจัดรูปแบบตามเงื่อนไขใน Excel ด้วย Aspose.Cells .NET: คู่มือครบถ้วน](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [วิธีดึงสีการจัดรูปแบบตามเงื่อนไขโดยใช้ Aspose.Cells for .NET](/cells/english/net/formatting/extract-conditional-formatting-colors-aspose-cells-net/)
- [ทำความเข้าใจการจัดรูปแบบตามเงื่อนไขด้วยฟอนต์กำหนดเองใน Excel โดยใช้ Aspose.Cells for .NET และ C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}