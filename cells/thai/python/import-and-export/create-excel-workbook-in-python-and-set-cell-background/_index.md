---
category: general
date: 2026-10-07
description: สร้างไฟล์ Excel ด้วย Python ตั้งค่าสีพื้นหลังของเซลล์ ปรับความกว้างคอลัมน์อัตโนมัติ
  และใส่วันที่ใน Excel พร้อมตัวอย่างโค้ดสั้น ๆ
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- auto fit excel columns
- populate dates in excel
- how to create excel
language: th
lastmod: 2026-10-07
og_description: สร้างเวิร์กบุ๊ก Excel ด้วย Python จากนั้นตั้งค่าสีพื้นหลังของเซลล์
  ปรับขนาดคอลัมน์อัตโนมัติ และใส่วันที่ใน Excel ทำตามคู่มือขั้นตอนต่อขั้นตอนนี้เพื่อสร้างไฟล์
  TimePeriodDemo.xlsx
og_image_alt: Screenshot of a Python‑generated Excel workbook with pink highlighted
  cells
og_title: สร้างเวิร์กบุ๊ก Excel ด้วย Python – ตั้งค่าพื้นหลังและปรับขนาดอัตโนมัติ
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  headline: Create Excel workbook in Python and set cell background
  type: TechArticle
- description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  name: Create Excel workbook in Python and set cell background
  steps:
  - name: Import required namespaces and define a helper function
    text: '```python # Step 1: Import Aspose.Cells classes and supporting modules
      from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType,
      SaveFormat from aspose.pydrawing import Color from datetime import datetime
      import os ```'
  - name: Create the workbook and get the first worksheet
    text: '```python def create_workbook(): # Step 2: Instantiate a new workbook (empty
      Excel file) book = Workbook() # Aspose.Cells creates a default worksheet; we
      retrieve it for further work sheet = book.worksheets[0] return book, sheet ```'
  - name: Set cell background color with a conditional format
    text: '```python def add_yesterday_rule(sheet): # Define a conditional format
      for the range I19:K20 (Yesterday) conds = sheet.get_range("I19:K20").format_conditions
      idx = conds.add_condition(FormatConditionType.TIME_PERIOD) cond = conds[idx]'
  - name: Populate dates in Excel
    text: '```python def populate_sample_dates(sheet): # Insert a date that falls
      on yesterday relative to the demo data cell = sheet.cells.get("I19") cell.put_value(datetime(2008,
      7, 30)) # sample date cell.style.number = 30 # Excel’s date format ID cell.set_style(cell.style)'
  - name: Auto‑fit Excel columns for better visibility
    text: '```python def auto_fit_columns(sheet): # Auto‑fit column L (index 12) so
      the content is fully visible sheet.auto_fit_column(12) # <-- auto fit excel
      columns ```'
  - name: Save the workbook
    text: '```python def save_workbook(book, filename="TimePeriodDemo.xlsx"): out_path
      = os.path.join("YOUR_DIRECTORY", filename) os.makedirs(os.path.dirname(out_path),
      exist_ok=True) book.save(out_path, SaveFormat.XLSX) print(f"Workbook saved to:
      {out_path}") ```'
  - name: Full script – putting it all together
    text: '```python def main(): # Create workbook and obtain the first worksheet
      book, sheet = create_workbook()'
  type: HowTo
tags:
- Excel
- Python
- Aspose.Cells
title: สร้างไฟล์งาน Excel ด้วย Python และตั้งค่าพื้นหลังเซลล์
url: /th/python/import-and-export/create-excel-workbook-in-python-and-set-cell-background/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง Excel workbook ใน Python และตั้งค่าพื้นหลังของเซลล์

สร้าง Excel workbook ใน Python และใช้การจัดรูปแบบตามเงื่อนไขด้วยเพียงไม่กี่บรรทัดของโค้ด บทเรียนนี้จะแสดงให้คุณ **วิธีสร้าง excel** อย่างอัตโนมัติ ตั้งค่าสีพื้นหลังของเซลล์ ปรับขนาดคอลัมน์ Excel ให้พอดีอัตโนมัติ และใส่วันที่ใน Excel โดยใช้ไลบรารี Aspose.Cells

คุณจะได้เรียนรู้วิธี:
* เริ่มต้น workbook และดึง worksheet แรกออกมา  
* กำหนดรูปแบบตามเงื่อนไขที่ไฮไลท์วันที่ “Yesterday”  
* ใส่ตัวอย่างวันที่ลงในเซลล์ที่ระบุ  
* ปรับขนาดคอลัมน์ให้พอดีเพื่อให้ข้อมูลมองเห็นชัดเจน  
* บันทึก workbook ไปยังโฟลเดอร์ที่เลือก

ข้อกำหนดเบื้องต้นเพียงอย่างเดียวคือมีสภาพแวดล้อม Python 3 ที่ทำงานได้พร้อมแพคเกจ `aspose-cells` และ `aspose-pydrawing` ติดตั้งแล้ว:

```bash
pip install aspose-cells aspose-pydrawing
```

---

## สร้าง Excel workbook ใน Python – ทีละขั้นตอน

ส่วนต่อไปนี้จะแบ่งกระบวนการออกเป็นขั้นตอนที่จัดการได้ง่าย แต่ละขั้นตอนจะมีโค้ดที่จำเป็น คำอธิบาย **ทำไม** จึงสำคัญ และเคล็ดลับเพื่อหลีกเลี่ยงข้อผิดพลาดทั่วไป

### ขั้นตอน 1: นำเข้า namespace ที่จำเป็นและกำหนดฟังก์ชันช่วยเหลือ

```python
# Step 1: Import Aspose.Cells classes and supporting modules
from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime
import os
```

*ทำไมจึงสำคัญ*: การนำเข้าคลาสที่ถูกต้องทำให้คุณเข้าถึงการสร้าง workbook, การจัดรูปแบบตามเงื่อนไข, และการจัดการสีได้  
**เคล็ดลับ**: เก็บการนำเข้าที่ส่วนบนของไฟล์ไว้เสมอ จะทำให้สคริปต์อ่านง่ายขึ้นและป้องกันข้อผิดพลาดการนำเข้าแบบวนลูป

### ขั้นตอน 2: สร้าง workbook และดึง worksheet แรก

```python
def create_workbook():
    # Step 2: Instantiate a new workbook (empty Excel file)
    book = Workbook()
    # Aspose.Cells creates a default worksheet; we retrieve it for further work
    sheet = book.worksheets[0]
    return book, sheet
```

คอนสตรัคเตอร์ `Workbook()` จะสร้าง Excel workbook ว่างเปล่าในหน่วยความจำ  
**ทำไม**: การเริ่มต้นด้วย workbook ใหม่ทำให้ไม่มีการจัดรูปแบบที่เหลือจากการรันครั้งก่อน

### ขั้นตอน 3: ตั้งค่าสีพื้นหลังของเซลล์ด้วยรูปแบบตามเงื่อนไข

```python
def add_yesterday_rule(sheet):
    # Define a conditional format for the range I19:K20 (Yesterday)
    conds = sheet.get_range("I19:K20").format_conditions
    idx = conds.add_condition(FormatConditionType.TIME_PERIOD)
    cond = conds[idx]

    # Apply visual style – this is where we set the cell background color
    cond.style.background_color = Color.pink          # <-- set cell background color
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

*ทำไม*: การใช้เงื่อนไข **time period** จะไฮไลท์อัตโนมัติทุกเซลล์ที่มีวันที่เป็น “Yesterday” ทำให้ไม่ต้องตรวจสอบวันที่ด้วยตนเอง  
**เคล็ดลับ**: `Color.pink` เป็นเพียงตัวอย่าง คุณสามารถใช้วัตถุ `Color` ใดก็ได้ (`Color.yellow`, `Color.light_green` เป็นต้น)

### ขั้นตอน 4: ใส่วันที่ลงใน Excel

```python
def populate_sample_dates(sheet):
    # Insert a date that falls on yesterday relative to the demo data
    cell = sheet.cells.get("I19")
    cell.put_value(datetime(2008, 7, 30))   # sample date
    cell.style.number = 30                 # Excel’s date format ID
    cell.set_style(cell.style)

    # Insert another date outside the “Yesterday” range
    cell = sheet.cells.get("K20")
    cell.put_value(datetime(2008, 8, 3))
    cell.style.number = 30
    cell.set_style(cell.style)

    # Add a label for the rule
    sheet.cells.get("I20").put_value("Yesterday")
```

ที่นี่เราจะ **ใส่วันที่ใน Excel** ที่เซลล์ `I19` และ `K20` วันที่แรกจะทำให้รูปแบบตามเงื่อนไขทำงาน ส่วนวันที่สองจะไม่ทำงาน  
**ทำไมจึงสำคัญ**: การแสดงตัวอย่างค่าที่ตรงและไม่ตรงช่วยให้คุณตรวจสอบว่ากฎทำงานตามที่คาดหวังหรือไม่

### ขั้นตอน 5: ปรับขนาดคอลัมน์ Excel ให้มองเห็นได้ชัดเจนขึ้น

```python
def auto_fit_columns(sheet):
    # Auto‑fit column L (index 12) so the content is fully visible
    sheet.auto_fit_column(12)   # <-- auto fit excel columns
```

`auto_fit_column` ปรับความกว้างของคอลัมน์ตามค่าที่ยาวที่สุดในเซลล์  
**เคล็ดลับ**: เรียกใช้หลังจากเขียนข้อมูลทั้งหมดแล้ว มิฉะนั้นความกว้างอาจคำนวณจากเนื้อหาที่ยังไม่สมบูรณ์

### ขั้นตอน 6: บันทึก workbook

```python
def save_workbook(book, filename="TimePeriodDemo.xlsx"):
    out_path = os.path.join("YOUR_DIRECTORY", filename)
    os.makedirs(os.path.dirname(out_path), exist_ok=True)
    book.save(out_path, SaveFormat.XLSX)
    print(f"Workbook saved to: {out_path}")
```

การบันทึกไฟล์จะเขียน workbook ที่อยู่ในหน่วยความจำลงดิสก์ในรูปแบบ XLSX สมัยใหม่

### สคริปต์เต็ม – รวมทุกขั้นตอนเข้าด้วยกัน

```python
def main():
    # Create workbook and obtain the first worksheet
    book, sheet = create_workbook()

    # Apply conditional formatting (set cell background color)
    add_yesterday_rule(sheet)

    # Populate the demo dates (populate dates in excel)
    populate_sample_dates(sheet)

    # Auto‑fit the relevant column (auto fit excel columns)
    auto_fit_columns(sheet)

    # Persist the file
    save_workbook(book)

if __name__ == "__main__":
    main()
```

**ผลลัพธ์ที่คาดหวัง**

```
Workbook saved to: YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

เปิดไฟล์ที่สร้างขึ้นใน Excel – เซลล์ `I19:K20` จะมีพื้นหลังสีชมพูสำหรับวันที่ตรงกับ “Yesterday” และคอลัมน์ L จะกว้างพอให้แสดงป้ายกำกับโดยไม่ถูกตัด

---

## ทำไมวิธีนี้ถึงทำงานได้ดีที่สุด

* **กระบวนการแบบ single‑pass** – ทุกการดำเนินการเกิดขึ้นบนอินสแตนซ์ `Workbook` เดียวกัน ลดการ I/O ที่ไม่จำเป็น  
* **Conditional formatting** – การใช้ `FormatConditionType.TIME_PERIOD` ให้ Excel จัดการตรรกะของวันที่ ซึ่งเชื่อถือได้กว่าการเขียนตรวจสอบวันที่ด้วย Python เอง  
* **Explicit styling** – การตั้งค่า `background_color` และ `pattern` รับประกันผลลัพธ์ด้านภาพเดียวกันในทุกเวอร์ชันของ Excel  
* **Auto‑fit after data** – ปรับขนาดคอลัมน์หลังจากใส่ข้อมูลครบถ้วนเพื่อให้ได้ความกว้างที่เหมาะสมที่สุด

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโครงการของคุณเอง

- [สร้าง Excel Workbook ด้วย Python – คู่มือเต็ม](/cells/english/python/import-and-export/create-excel-workbook-python-full-guide/)
- [สร้าง Excel Workbook ด้วย Python – คู่มือขั้นตอนเต็ม](/cells/english/python/import-and-export/create-excel-workbook-python-complete-step-by-step-guide/)
- [สร้าง Excel Workbook ด้วย Python – คู่มือเต็มพร้อม Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}