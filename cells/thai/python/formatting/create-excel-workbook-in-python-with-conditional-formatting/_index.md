---
category: general
date: 2026-09-05
description: สร้างไฟล์ Excel ใน Python และเพิ่มการจัดรูปแบบตามเงื่อนไขเพื่อไฮไลท์เซลล์ของวันเมื่อวาน
  เรียนรู้โค้ดเต็มและเหตุผลของแต่ละขั้นตอน.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- add conditional formatting excel
- highlight cells based on date
- add conditional formatting range
- how to highlight yesterday cells
language: th
lastmod: 2026-09-05
og_description: สร้างไฟล์ Excel ใน Python และเพิ่มการจัดรูปแบบตามเงื่อนไขเพื่อไฮไลท์เซลล์ของวันเมื่อวาน
  ทำตามคู่มือขั้นตอนต่อขั้นตอนนี้เพื่อรับโซลูชันที่ครบถ้วน.
og_image_alt: Screenshot of an Excel sheet where cells are highlighted after creating
  Excel workbook in Python
og_title: สร้างเวิร์กบุ๊ก Excel ด้วย Python – เพิ่มการจัดรูปแบบตามเงื่อนไข
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
title: สร้างเวิร์กบุ๊ก Excel ใน Python พร้อมการจัดรูปแบบตามเงื่อนไข
url: /th/python/formatting/create-excel-workbook-in-python-with-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง Excel workbook ด้วย Python พร้อมการจัดรูปแบบตามเงื่อนไข

หากคุณต้องการ **create Excel workbook python** สำหรับงานรายงาน คู่มือนี้จะแสดงวิธีสร้าง workbook และใช้กฎการจัดรูปแบบตามเงื่อนไขที่ทำให้วันที่ของเมื่อวานโดดเด่น คุณจะได้เห็นโค้ดที่แน่นอน เหตุผลที่แต่ละบรรทัดมีอยู่ และวิธีปรับโซลูชันสำหรับช่วงวันที่อื่น

การจัดรูปแบบตามเงื่อนไขเป็นวิธีที่ทรงพลังในการดึงความสนใจไปยังข้อมูลที่ตรงกับเงื่อนไขเฉพาะ ในบทแนะนำนี้เราใช้ไลบรารี Aspose.Cells สำหรับ Python via .NET ซึ่งให้การสนับสนุนคุณสมบัติของ Excel อย่างเต็มที่โดยไม่ต้องใช้ Microsoft Office เมื่อตอนจบคู่มือคุณจะได้ไฟล์ที่เซลล์ในช่วง *I19:K20* จะเปลี่ยนเป็นสีชมพูเมื่อมีวันที่ของเมื่อวาน

## ข้อกำหนดเบื้องต้น

* Python 3.9+ ที่ติดตั้งแล้ว
* `aspose-cells` package (install with `pip install aspose-cells`)
* ความคุ้นเคยพื้นฐานกับไวยากรณ์ Python
* สิทธิ์การเขียนในไดเรกทอรีที่ workbook จะถูกบันทึก

โค้ดทำงานบน Windows, macOS, และ Linux ตราบใดที่มี .NET runtime

## สร้าง Excel workbook ด้วย Python

ขั้นตอนแรกคือการสร้างอ็อบเจ็กต์ `Workbook` และดึง worksheet เริ่มต้น อ็อบเจ็กต์นี้แทนไฟล์ Excel ทั้งหมดในหน่วยความจำ

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*ทำไมเรื่องนี้สำคัญ*: `Workbook()` สร้าง workbook ว่างที่มี worksheet เดียว การเข้าถึง `worksheets[0]` จะให้ตัวจัดการเพื่อเพิ่มข้อมูล, สไตล์, และการจัดรูปแบบในภายหลัง.

## เพิ่มช่วงการจัดรูปแบบตามเงื่อนไข

ต่อไปเรากำหนดพื้นที่ที่จะถูกประเมินโดยกฎเงื่อนไข ช่วง `I19:K20` ครอบคลุมหกเซลล์ในสองแถว

```python
# Define the range that will receive the conditional formatting rule
condition_collection = worksheet.conditional_formattings.add("I19:K20")
```

*ทำไมเรื่องนี้สำคัญ*: การเพิ่มคอลเลกชันการจัดรูปแบบตามเงื่อนไขให้กับช่วงเฉพาะจะทำให้กฎแยกออกจากเซลล์ที่ไม่เกี่ยวข้อง ซึ่งสอดคล้องกับความต้องการ **add conditional formatting range**

## กำหนดกฎ: ไฮไลท์เซลล์ตามวันที่

ตอนนี้เราสร้างเงื่อนไขประเภท `TIME_PERIOD` ซึ่งบอก Excel ให้เปรียบเทียบค่าของแต่ละเซลล์กับช่วงเวลาที่กำหนดไว้ล่วงหน้า

```python
from aspose.cells import FormatConditionType, TimePeriodType

# Add a TIME_PERIOD condition to the collection
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Set the time period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY
```

*ทำไมเรื่องนี้สำคัญ*: `TIME_PERIOD` เป็นประเภทในตัวเดียวที่รองรับโดยตรง “Yesterday”, “Today”, “Last Week” เป็นต้น การตั้งค่า `condition.time_period` เป็น `YESTERDAY` ทำให้กฎประเมินค่าของวันที่ในแต่ละเซลล์โดยอัตโนมัติกับวันก่อนวันปัจจุบัน

## ตั้งสไตล์ให้เซลล์ที่ตรงกับเงื่อนไข

การจัดรูปแบบตามเงื่อนไขยังต้องการสไตล์ภาพ เราเลือกสีชมพูแบบเติมเต็มเพื่อทำให้เซลล์ที่ตรงกันเด่นขึ้น

```python
from aspose.pydrawing import Color as DrawingColor
from aspose.cells import BackgroundType

# Apply a pink solid background to cells that satisfy the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID
```

*ทำไมเรื่องนี้สำคัญ*: อ็อบเจ็กต์สไตล์กำหนดวิธีที่ Excel แสดงเซลล์ที่ตรงกับเงื่อนไข การใช้สีชมพูแบบเติมเต็มสอดคล้องกับความต้องการ **highlight cells based on date** และทำให้ผลลัพธ์ตรวจสอบได้ง่าย

## เติมวันที่ตัวอย่างสำหรับการประเมิน

เพื่อดูกฎทำงาน เราแทรกวันที่สองค่า—หนึ่งที่ตรงกับวันที่ของเมื่อวานและอีกหนึ่งที่ไม่ตรง รูปแบบ `number` `30` สอดคล้องกับรูปแบบวันที่ในตัว `mm-dd-yy`

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

*ทำไมเรื่องนี้สำคัญ*: การให้ทั้งวันที่ตรงและไม่ตรงทำให้คุณตรวจสอบว่าการจัดรูปแบบตามเงื่อนไขทำงานถูกต้อง ปรับวันที่ให้เป็นเดือนปัจจุบันเมื่อรันสคริปต์ หรือแทนที่ด้วยค่าที่เปลี่ยนแปลงได้

## บันทึก workbook

สุดท้ายเราจะเขียนไฟล์ลงดิสก์ ค่าคงที่ `SaveFormat.XLSX` ทำให้แน่ใจว่าเอาต์พุตเป็นไฟล์ Excel สมัยใหม่

```python
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

*ทำไมเรื่องนี้สำคัญ*: การบันทึก workbook ทำให้คุณเปิดได้ใน Excel, LibreOffice หรือโปรแกรมดูไฟล์ที่รองรับ XLSX เส้นทางที่พิมพ์ออกมายืนยันตำแหน่งที่ไฟล์ถูกเขียน

## สคริปต์เต็ม

เมื่อนำส่วนต่าง ๆ มารวมกัน สคริปต์ที่สมบูรณ์และสามารถรันได้มีลักษณะดังนี้:

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

### ผลลัพธ์ที่คาดหวัง

เมื่อคุณเปิดไฟล์ `TimePeriodExample.xlsx`:

* เซลล์ **I19** แสดงพื้นหลังสีชมพูเพราะค่าตรงกับวันที่ของเมื่อวาน.
* เซลล์ **K20** คงพื้นหลังค่าเริ่มต้นเพราะวันที่อยู่นอกช่วง.
* ป้าย **“Yesterday”** อยู่ในเซลล์ I20 เพื่อความชัดเจน.

## ความแปรผันทั่วไปและกรณีขอบ

| Situation | Adjustment |
|-----------|------------|
| **ไฮไลท์วันนี้แทนเมื่อวาน** | เปลี่ยนเป็น `condition.time_period = TimePeriodType.TODAY`. |
| **ใช้กฎกับพื้นที่ใหญ่ขึ้น** | อัปเดตสตริงช่วงใน `add("I19:K20")` เป็นอย่างเช่น `"A1:Z100"`. |
| **ใช้สีเติมเต็มอื่น** | แทนที่ `DrawingColor.pink` ด้วย `DrawingColor` ใด ๆ (เช่น `DrawingColor.light_green`). |
| **ทำงานกับวันที่แบบไดนามิก** | คำนวณ `datetime.now() - timedelta(days=1)` สำหรับเมื่อวานและเขียนค่าดังกล่าวลงในเซลล์ก่อนนำกฎไปใช้. |

**เคล็ดลับ:** เมื่อคุณสร้าง workbook โดยโปรแกรมสำหรับผู้ใช้หลายคน ให้แยกการกำหนดการจัดรูปแบบตามเงื่อนไขออกจากการใส่ข้อมูล เพื่อให้สามารถใช้สไตล์เดียวกันหลายแผ่นโดยไม่ต้องทำซ้ำโค้ด

## ตรวจสอบผลลัพธ์โดยโปรแกรม (ทางเลือก)

หากต้องการยืนยันการจัดรูปแบบโดยไม่เปิด Excel คุณสามารถตรวจสอบสไตล์ของเซลล์หลังจากบันทึกได้:



## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการนำไปใช้แบบอื่นในโครงการของคุณ

- [Excel Automation&#58; Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Create Excel Workbook and Add Labels with Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/data-labeling/)
- [Excel Automation Create Workbook Add Listbox Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}