---
category: general
date: 2026-08-08
description: สร้างไฟล์ Excel ด้วย Python และเพิ่มการจัดรูปแบบตามเงื่อนไขโดยอิงจากวันที่
  คู่มือขั้นตอนโดยใช้ Aspose.Cells เพื่อไฮไลท์เซลล์ของเมื่อวาน.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- conditional formatting based on date
- Aspose.Cells Python example
- Excel date formatting Python
- Python Excel automation
language: th
lastmod: 2026-08-08
og_description: สร้างเวิร์กบุ๊ก Excel ด้วย Python และ Aspose.Cells พร้อมใช้การจัดรูปแบบตามเงื่อนไขตามวันที่สำหรับสเปรดชีตแบบไดนามิก
og_image_alt: Screenshot of an Excel sheet created with Python showing cells highlighted
  by date conditional formatting
og_title: สร้างไฟล์ Excel ด้วย Python – การจัดรูปแบบตามเงื่อนไขของวันที่
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
title: สร้างเวิร์กบุ๊ก Excel ด้วย Python การจัดรูปแบบตามเงื่อนไขของวันที่
url: /th/python/formatting/create-excel-workbook-python-date-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง Excel workbook Python ด้วยการจัดรูปแบบตามเงื่อนไขของวันที่

หากคุณต้องการ **create Excel workbook Python** และทำให้เซลล์ที่ตรงกับวันที่เฉพาะโดยอัตโนมัติเป็นสีไฮไลท์ บทแนะนำนี้จะแสดงวิธีทำอย่างละเอียด คุณจะได้เรียนรู้การใช้ **conditional formatting based on date** เพื่อให้วันที่ของเมื่อวานแสดงเป็นสีชมพูโดยใช้ไลบรารี Aspose.Cells

คู่มือจะพาคุณผ่านทุกขั้นตอน—ตั้งแต่การติดตั้ง SDK จนถึงการบันทึกไฟล์ .xlsx สุดท้าย—เพื่อให้คุณสามารถคัดลอก‑วางตัวอย่างที่ทำงานได้ลงในโปรเจกต์ของคุณเอง ไม่จำเป็นต้องอ้างอิงเอกสารภายนอก; โค้ดและคำอธิบายทั้งหมดอยู่ในที่เดียว

## ข้อกำหนดเบื้องต้น

* ติดตั้ง Python 3.8 หรือใหม่กว่า
* `aspose-cells` package (wrapper ของ Python สำหรับ Aspose.Cells) ติดตั้งด้วย:
  ```bash
  pip install aspose-cells
  ```
* ความคุ้นเคยพื้นฐานกับ Python และแนวคิดของ Excel เช่น worksheet และสไตล์ของเซลล์

> **เคล็ดลับ:** Aspose.Cells ทำงานได้โดยไม่ต้องติดตั้ง Microsoft Excel ทำให้เหมาะสำหรับการทำงานอัตโนมัติบนเซิร์ฟเวอร์

## ขั้นตอนที่ 1: สร้าง Excel workbook ใน Python

งานแรกคือการสร้างอินสแตนซ์ของ workbook ใหม่และดึง worksheet เริ่มต้น วัตถุนี้แทนไฟล์ Excel ทั้งหมดและให้การเข้าถึงแถว, คอลัมน์, และ API การจัดรูปแบบ

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook – this automatically adds one worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]   # reference to the first (default) sheet
```

การสร้าง workbook เป็นพื้นฐานสำหรับการจัดการต่อไป ไม่ว่าจะเป็นการเพิ่มข้อมูล, สูตร, หรือกฎการจัดรูปแบบ

## ขั้นตอนที่ 2: กำหนดการจัดรูปแบบตามเงื่อนไขที่อิงวันที่

ตอนนี้เราจะเพิ่ม **conditional formatting based on date**. enum `FormatConditionType.TIME_PERIOD` ช่วยให้เรากำหนดช่วงเวลาในตัวอย่างเช่น Yesterday, Today หรือ LastWeek

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

เหตุผลที่ขั้นตอนนี้สำคัญ: Excel จะประเมินเงื่อนไขสำหรับแต่ละเซลล์ในช่วง เมื่อค่าของเซลล์อยู่ในช่วงที่กำหนด (เมื่อวาน) สไตล์ที่เราตั้งไว้จะถูกนำไปใช้โดยอัตโนมัติ

## ขั้นตอนที่ 3: เติมช่วงด้วยวันที่ตัวอย่าง

เพื่อดูกฎทำงาน เราจะเขียนอ็อบเจ็กต์ `datetime` สองตัวลงในเซลล์เป้าหมาย หนึ่งในนั้นตั้งค่าให้เป็นวันที่ของเมื่อวานตามระบบวันที่ภายในของ workbook อย่างเจตนา

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

บรรทัด `number = 30` บอก Excel ให้แสดงค่าโดยใช้รูปแบบวันที่สั้นมาตรฐาน คุณสามารถเปลี่ยนดัชนีนี้เป็นรูปแบบตัวเลขในตัวอื่นได้หากต้องการการแสดงผลที่แตกต่าง

## ขั้นตอนที่ 4: ปรับความกว้างของคอลัมน์เพื่อความอ่านง่าย

การปรับขนาดคอลัมน์ที่มีวันที่โดยอัตโนมัติทำให้ผลลัพธ์อ่านง่ายขึ้น โดยเฉพาะเมื่อเปิด workbook ใน Excel หรือโปรแกรมดูไฟล์

```python
# Column 12 corresponds to column L (zero‑based indexing)
worksheet.auto_fit_column(12)
```

## ขั้นตอนที่ 5: บันทึก workbook ลงดิสก์

สุดท้าย ให้บันทึก workbook เป็นไฟล์ .xlsx แทนที่ `"YOUR_DIRECTORY"` ด้วยพาธจริงบนเครื่องของคุณ

```python
import os

output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

เมื่อคุณเปิดไฟล์ `TimePeriodDemo.out.xlsx` ใน Excel เซลล์ **I19** จะมีพื้นหลังสีชมพูเพราะค่าตรงกับกฎ “Yesterday” ส่วน **K20** จะคงเดิมไม่มีการเปลี่ยนแปลง

### ผลลัพธ์ที่คาดหวัง

| I19 (วันที่) | I20 (ป้าย) | J19 | J20 | K19 | K20 (วันที่) |
|------------|-------------|-----|-----|-----|------------|
| *2008‑07‑30* (พื้นหลังสีชมพู) | เมื่อวาน | – | – | – | *2008‑08‑03* (ไม่มีการจัดรูปแบบ) |

การไล่สีชมพูยืนยันว่า **conditional formatting based on date** ทำงานตามที่คาดหวัง

## ความแปรผันทั่วไปและกรณีขอบ

| สถานการณ์ | วิธีปรับโค้ด |
|-----------|-----------------------|
| **ไฮไลท์ “Today” แทน “Yesterday”** | Change `condition.time_period = TimePeriodType.TODAY` |
| **ใช้กฎกับคอลัมน์ทั้งหมด** | Use `worksheet.get_range("A:A").format_conditions` |
| **ใช้ช่วงวันที่กำหนดเอง (เช่น 7 วันที่ผ่านมา)** | Replace the time‑period condition with a formula condition: <br>```python<br>condition = conditions.add_condition(FormatConditionType.FORMULA)<br>condition.formula1 = 'AND(A1>=TODAY()-7, A1<=TODAY())'<br>``` |
| **สีพื้นหลังที่ต่างกัน** | Set `condition.style.background_color = Color.light_green` (or any `Color` you prefer) |
| **รันบน Linux โดยไม่มีหน้าจอ** | Aspose.Cells ทำงานแบบ headless อย่างเต็มที่; ไม่ต้องการการกำหนดค่าเพิ่มเติม. |

## ตัวอย่างเต็มที่สามารถรันได้

ด้านล่างเป็นสคริปต์เต็มที่คุณสามารถรันได้ทันที (หลังจากอัปเดตไดเรกทอรีเอาต์พุต) ทั้งการนำเข้า, คอมเมนต์, และพื้นฐานการจัดการข้อผิดพลาดรวมอยู่ด้วย

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

การรันสคริปต์จะสร้างไฟล์ Excel ที่เซลล์ “Yesterday” ถูกไฮไลท์โดยอัตโนมัติ แสดงให้เห็นการผสมผสานระหว่าง **create Excel workbook Python** กับ **conditional formatting based on date**.

## สรุป

คุณตอนนี้รู้วิธี **create Excel workbook Python** objects, กำหนด **date‑based conditional formatting**

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดที่ทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการดำเนินการแบบอื่นในโปรเจกต์ของคุณ

- [สร้าง Excel Workbook ด้วย Aspose.Cells ใน Java: คู่มือขั้นตอนโดยละเอียด](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [สร้าง Excel Workbook พร้อมแผนภูมิด้วย Aspose.Cells .NET | คู่มือขั้นตอนโดยละเอียด](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)
- [Excel Automation: สร้าง Workbook และเพิ่ม ListBox ด้วย Aspose.Cells สำหรับ .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}