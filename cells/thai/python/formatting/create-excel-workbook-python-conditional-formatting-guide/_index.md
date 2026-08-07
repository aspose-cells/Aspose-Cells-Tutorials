---
category: general
date: 2026-07-20
description: สร้างไฟล์ Excel ด้วย Python และ Aspose.Cells, ตั้งค่าสีพื้นหลังของเซลล์,
  และเพิ่มการจัดรูปแบบตามเงื่อนไขใน Python เพื่อจัดสไตล์เซลล์ตามวันที่.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- aspose cells conditional formatting
- add conditional formatting python
language: th
lastmod: 2026-07-20
og_description: สร้างไฟล์ Excel ด้วย Python โดยใช้ Aspose.Cells เรียนรู้วิธีตั้งค่าสีพื้นหลังของเซลล์และเพิ่มการจัดรูปแบบตามเงื่อนไขใน
  Python เพื่อจัดรูปแบบเซลล์ตามวันที่
og_image_alt: Screenshot of an Excel workbook created with Python showing conditional
  formatting applied to date cells
og_title: สร้างไฟล์ Excel ด้วย Python – เพิ่มการจัดรูปแบบตามเงื่อนไข
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
title: สร้างสมุดงาน Excel ด้วย Python – คู่มือการจัดรูปแบบตามเงื่อนไข
url: /th/python/formatting/create-excel-workbook-python-conditional-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง Excel Workbook ด้วย Python – คู่มือการจัดรูปแบบตามเงื่อนไข

เคยสงสัยไหมว่า **create Excel workbook Python** จากศูนย์และทำให้ดูเรียบร้อยโดยไม่ต้องเปิด UI? คุณไม่ได้เป็นคนเดียว นักพัฒนาหลายคนเจออุปสรรคเมื่อจำเป็นต้อง **set cell background color** หรือใช้สไตล์ตามวันที่โดยอัตโนมัติ  

ในบทแนะนำนี้เราจะเดินผ่านตัวอย่างที่ทำงานได้เต็มรูปแบบโดยใช้ Aspose.Cells เพื่อ **add conditional formatting python** กำหนดกฎ, จัดรูปแบบเซลล์ตามวันที่, และบันทึกผลลัพธ์เป็นไฟล์ XLSX สมัยใหม่ เมื่อเสร็จคุณจะมีสคริปต์ที่พร้อมใช้งานและสามารถนำไปใส่ในโปรเจกต์ใดก็ได้

## สิ่งที่คุณจะได้เรียน

- วิธีการเริ่มต้น workbook และดึง worksheet แรกออกมา  
- วิธี **set cell background color** ให้กับช่วงทั้งหมด  
- การใช้ **aspose cells conditional formatting** เพื่อไฮไลท์วันที่ “เมื่อวาน”  
- การปรับขนาดคอลัมน์อัตโนมัติและบันทึกไฟล์ลงดิสก์  

ไม่ต้องมีการตั้งค่าเพิ่มเติม—แค่ Python 3 และแพคเกจ Aspose.Cells หากคุณได้ติดตั้ง `aspose-cells` แล้วก็พร้อมใช้งาน; หากยังให้รัน `pip install aspose-cells` เพียงเท่านั้น

## ข้อกำหนดเบื้องต้น

- Python 3.8+ (โค้ดทำงานบน 3.9, 3.10 และรุ่นใหม่กว่า)  
- Aspose.Cells for Python via .NET (`aspose-cells` NuGet wrapper)  
- ความคุ้นเคยพื้นฐานกับแนวคิดของ Excel (เซลล์, ช่วง, การจัดรูปแบบ)  

พร้อมหรือยัง? ดีแล้ว—มาเริ่มกันเลย

## Create Excel Workbook Python – การตั้งค่าและ Worksheet

อย่างแรกที่ต้องทำคือสร้างอ็อบเจกต์ workbook ใหม่และอ้างอิงไปยัง worksheet เริ่มต้น นี่คือผ้าใบที่ทุกการดำเนินการต่อไปจะเกิดขึ้น

```python
# Import the necessary Aspose.Cells classes
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and grab the first sheet
workbook = Workbook()                     # create excel workbook python
worksheet = workbook.worksheets[0]        # default is the first worksheet
```

> **ทำไมจึงสำคัญ:** `Workbook()` สร้างไฟล์ Excel ในหน่วยความจำ ทำให้ไม่ต้องใช้ไฟล์ชั่วคราว ตัวแปร `worksheet` คือจุดเริ่มต้นสำหรับการทำงานระดับเซลล์

## ตั้งค่าสีพื้นหลังของเซลล์

ก่อนที่เราจะเพิ่มกฎใด ๆ ควรให้ช่วงเป้าหมายมีสีพื้นฐานเพื่อให้การจัดรูปแบบตามเงื่อนไขเด่นชัด ตัวช่วยด้านล่างจะดึง (หรือสร้าง) `FormatConditionCollection` สำหรับช่วงที่กำหนดและทาสีพื้นหลังแบบทึบให้เซลล์

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

> **เคล็ดลับ:** หากคุณต้องการใช้ช่วงเดียวกันกับหลายกฎ ให้เรียกตัวช่วยนี้เพียงครั้งเดียวและเก็บคอลเลกชันที่คืนค่าไว้; จะช่วยลดจำนวนการเรียก API ลง

## เพิ่ม Conditional Formatting Python สำหรับช่วงวันที่

ตอนนี้มาสร้างกฎ **time‑period conditional formatting** ที่ไฮไลท์เซลล์ที่มีวันที่ “เมื่อวาน” นี่แสดงให้เห็นพลังของ **format cells by date** ด้วย Aspose.Cells

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

> **ทำไมต้องใช้ `TIME_PERIOD`?** มันทำให้เราไม่ต้องเขียนสูตรเอง Aspose.Cells จะเปรียบเทียบวันที่กับวันที่ระบบปัจจุบันโดยอัตโนมัติ ทำให้กฎยังคงใช้ได้ตลอดเวลา

### การรันกฎ

```python
apply_yesterday_rule()
```

เมื่อเปิดไฟล์ที่ได้ เซลล์ `I19` จะสว่างสีชมพู (เพราะเป็น “Yesterday”) ส่วน `K20` จะคงสีเขียวพื้นฐาน

## ปรับขนาดคอลัมน์อัตโนมัติและบันทึก Workbook

สเปรดชีตที่เรียบร้อยดูเป็นมืออาชีพ การปรับขนาดอัตโนมัติทำให้ข้อมูลไม่อัดแน่น

```python
# Step 4: Auto‑fit the column width for a tidy appearance
worksheet.auto_fit_column(12)   # column index is zero‑based; 12 corresponds to column M

# Step 5: Save the workbook to disk
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **กรณีขอบเขต:** หากคุณระบุไดเรกทอรีที่ไม่มีอยู่จริง `workbook.save` จะเกิดข้อผิดพลาด ให้ห่อการบันทึกด้วย `try/except` หากต้องการจัดการอย่างอ่อนโยน

### สคริปต์เต็ม (พร้อมคัดลอก‑วาง)

ด้านล่างเป็นสคริปต์ทั้งหมดพร้อมรัน เพียงเปลี่ยน `YOUR_DIRECTORY` ให้เป็นโฟลเดอร์ที่มีอยู่บนเครื่องของคุณ

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

การรันสคริปต์นี้จะสร้างไฟล์ `TimePeriodExample.xlsx` พร้อมการจัดรูปแบบตามเงื่อนไขที่อธิบายไว้

## คำถามที่พบบ่อย & เคล็ดลับ

- **สามารถกำหนดช่วงวันที่อื่นได้หรือไม่?**  
  ทำได้เลย เปลี่ยน `"I19:K20"` เป็นช่วงสไตล์ A1 ใดก็ได้และปรับวันที่ตัวอย่างให้สอดคล้อง

- **ต้องการสูตรกำหนดเองแทน `YESTERDAY` จะทำอย่างไร?**  
  ใช้ `FormatConditionType.FORMULA` แล้วตั้ง `condition.formula1 = "YOUR_FORMULA"` เช่น `=TODAY()-A1=1` เพื่อจำลอง “เมื่อวาน”

- **จะใส่หลายกฎในช่วงเดียวกันได้อย่างไร?**  
  เรียก `conditions.add_condition` อีกครั้งพร้อม `FormatConditionType` ที่ต่างกัน ลำดับสำคัญ; กฎที่ตามมาสามารถทับกฎก่อนหน้าได้

- **สามารถตั้งสีฟอนต์พร้อมสีพื้นหลังได้หรือไม่?**  
  ทำได้—แก้ `condition.style.font.color = Color.white` (หรือ `Color` ใดก็ได้)

## สรุป

คุณได้เรียนรู้วิธี **create Excel workbook Python** ด้วย Aspose.Cells, **set cell background color**, และ **add conditional formatting python** ที่จัดรูปแบบเซลล์ตามวันที่ สคริปต์ทำงานเต็มรูปแบบ, รองรับกรณีขอบเขตเช่นไดเรกทอรีที่ไม่มี, และสามารถขยายต่อเป็นสถานการณ์ซับซ้อนเช่นตรรกะหลายกฎหรือการตรวจจับช่วงแบบไดนามิก

พร้อมก้าวต่อไปหรือยัง? ลองเปลี่ยนกฎ “Yesterday” เป็น “Last Week”, ทดลองเติมสีไล่ระดับ, หรือสร้างรายงานเต็มรูปแบบที่มีตารางจัดรูปแบบหลายสิบตาราง บล็อกพื้นฐานทั้งหมดอยู่ที่นี่แล้ว และคุณก็เชี่ยวชาญการใช้ **aspose cells conditional formatting** ใน Python แล้ว

ขอให้สนุกกับการเขียนโค้ด, และอย่าลืมแชร์วิธีของคุณในคอมเมนต์!

## สิ่งที่คุณควรเรียนต่อไป

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [เชี่ยวชาญการจัดรูปแบบเซลล์ Excel และการจัดการ Workbook ด้วย Aspose.Cells สำหรับ .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [วิธีสร้างและบันทึก Excel Workbook เป็น ODS ด้วย Aspose.Cells สำหรับ .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [วิธีสร้าง Named Ranges ระดับ Workbook ใน Excel ด้วย Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}