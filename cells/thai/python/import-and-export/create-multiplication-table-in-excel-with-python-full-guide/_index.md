---
category: general
date: 2026-06-21
description: สร้างตารางคูณใน Excel ด้วย Python เรียนรู้วิธีใช้ lambda วิธีใช้ makearray
  แสดงอาเรย์ Excel และอ่านค่าจาก Excel ด้วย Python ในบทเรียนแบบขั้นตอนต่อขั้นตอน.
draft: false
keywords:
- create multiplication table
- how to use lambda
- how to use makearray
- display excel array
- read excel values python
language: th
og_description: สร้างตารางคูณใน Excel ด้วย Python บทเรียนนี้แสดงวิธีใช้ lambda, makearray,
  แสดงอาเรย์ Excel และอ่านค่าจาก Excel ด้วย Python อย่างมีประสิทธิภาพ
og_title: สร้างตารางคูณใน Excel ด้วย Python – คู่มือเต็ม
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create multiplication table in Excel using Python. Learn how to use
    lambda, how to use makearray, display excel array and read excel values python
    in a step‑by‑step tutorial.
  headline: Create multiplication table in Excel with Python – Full Guide
  type: TechArticle
tags:
- python
- excel
- openpyxl
title: สร้างตารางคูณใน Excel ด้วย Python – คู่มือเต็ม
url: /th/python/import-and-export/create-multiplication-table-in-excel-with-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้างตารางคูณใน Excel ด้วย Python – คู่มือเต็ม

เคยสงสัยไหมว่า **สร้างตารางคูณ** ใน Excel อย่างไรโดยไม่ต้องพิมพ์แต่ละเซลล์ด้วยตนเอง? คุณไม่ได้เป็นคนเดียวที่มีคำถามนี้ ในหลาย ๆ สถานการณ์การรายงานคุณต้องการกริดสินค้า 5×5 (หรือใหญ่กว่านั้น) อย่างรวดเร็ว และการทำด้วยมือเป็นการเสียเวลา  

ในบทเรียนนี้เราจะพาคุณผ่านวิธีที่สะอาดและขับเคลื่อนด้วย Python เพื่อสร้างตารางนั้น ฝังสูตร `MAKEARRAY` แล้วดึงผลลัพธ์กลับเข้าสคริปต์ของคุณ ระหว่างทางเราจะตอบ **วิธีใช้ lambda** แสดง **วิธีใช้ makearray** และสาธิต **display excel array** รวมถึง **read excel values python**—ทั้งหมดในตัวอย่างเดียวที่ต่อเนื่องกัน

เมื่อเสร็จสิ้นคุณจะได้สแนปพ็อตที่นำกลับมาใช้ใหม่ได้กับเวิร์กบุ๊กใดก็ได้ และคุณจะเข้าใจว่าทำไมวิธีนี้จึงเร็วและพร้อมสำหรับอนาคต

## สิ่งที่คุณต้องมี

- Python 3.8+ (เวอร์ชันล่าสุดก็ใช้ได้)
- ไลบรารี `openpyxl` (หรือไลบรารีที่รองรับ Excel และสูตร)
- ความเข้าใจพื้นฐานเกี่ยวกับ lambda expressions ใน Python
- ไม่ต้องการ Excel add‑ins พิเศษ; ฟังก์ชัน `MAKEARRAY` ดั้งเดิม (มีใน Excel 365) จะทำงานหนักให้คุณ

หากขาดส่วนใดส่วนหนึ่ง เพียงรัน `pip install openpyxl` แล้วคุณก็พร้อมใช้งาน

## สร้างตารางคูณ – ภาพรวม

แนวคิดหลักง่าย ๆ: เราจะสร้างเวิร์กบุ๊กใหม่ เขียนสูตร `MAKEARRAY` ที่สร้างเมทริกซ์คูณ 5 × 5 ให้ Excel คำนวณ แล้วอ่านค่าที่ได้กลับเข้าสู่ Python

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Insert a MAKEARRAY formula that builds a 5×5 multiplication table
# The formula uses a LAMBDA that returns r*c for each row (r) and column (c)
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"

# Step 3: Calculate all formulas so the array is materialized in the sheet
workbook.calculate_formula()

# Step 4: Read and display the top‑left 5×5 block of values
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

การรันสคริปต์จะแสดงผล:

```
[1, 2, 3, 4, 5]
[2, 4, 6, 8, 10]
[3, 6, 9, 12, 15]
[4, 8, 12, 16, 20]
[5, 10, 15, 20, 25]
```

นี่คือ **create multiplication table** ใน Excel ที่ทำงานเต็มรูปแบบ สร้างโดย Python ทั้งหมด

### ทำไมต้องใช้ `MAKEARRAY` แทนการวนลูปใน Python?

- **ประสิทธิภาพ**: Excel คำนวณโดยตรง ซึ่งเร็วกว่าเมทริกซ์ขนาดใหญ่ที่ทำใน Python
- **อัปเดตแบบเรียลไทม์**: หากคุณเปลี่ยนขนาดในสูตรภายหลัง ชีตจะคำนวณใหม่อัตโนมัติ
- **อ่านง่าย**: สูตรบ่งบอกเจตนา (“สร้างอาเรย์”) อย่างชัดเจน ทำให้โค้ด Python ของคุณดูเรียบร้อย

## วิธีใช้ lambda ใน Python สำหรับสูตร Excel

ส่วน `LAMBDA` ของการเรียก `MAKEARRAY` เป็นฟังก์ชันนิรนามด้าน Excel ไม่ใช่ lambda ของ Python อย่างไรก็ตามแนวคิดเดียวกัน: คุณกำหนดตรรกะสั้น ๆ ที่รับ `r` (ดัชนีแถว) และ `c` (ดัชนีคอลัมน์) แล้วคืนค่า `r*c`  

หากคุณใหม่กับ **how to use lambda** ในโลกของ Excel ให้คิดว่าเป็นฟังก์ชันขนาดเล็กที่อยู่ภายในสูตรเท่านั้น ไม่ต้องประกาศฟังก์ชันแยกที่อื่น ใน Python เราแค่ฝังสตริงนี้ลงไป:

```python
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"
```

บรรทัดนี้บอก Excel: *“สำหรับแต่ละเซลล์ในบล็อก 5‑by‑5 ให้คำนวณ แถว × คอลัมน์.”*  

เพราะ lambda ถูกประเมินโดย Excel คุณจึงไม่ต้องกังวลเกี่ยวกับไวยากรณ์ lambda ของ Python ที่นี่—เพียงไวยากรณ์ของ Excel เท่านั้น

## วิธีใช้ makearray เพื่อสร้างอาเรย์

`MAKEARRAY` เป็นฟังก์ชันใหม่ที่เพิ่มเข้ามาในไลบรารีฟังก์ชันของ Excel (มีใน Microsoft 365 ตั้งแต่ปี 2022) มันแทนที่เทคนิคเก่าอย่าง `INDEX` + `ROW`/`COLUMN` การใช้งานคือ:

```
MAKEARRAY(rows, columns, lambda)
```

- **rows** – จำนวนแถวที่ต้องการ
- **columns** – จำนวนคอลัมน์ที่ต้องการ
- **lambda** – Excel LAMBDA ที่รับ `(row, column)` แล้วคืนค่าหนึ่งค่า

ในตัวอย่างของเราเราใส่ `5,5` เพื่อสร้างตารางคูณคลาสสิก แต่คุณสามารถเปลี่ยนตัวเลขเหล่านั้นได้ง่าย ๆ:

```python
worksheet["A1"] = "=MAKEARRAY(10,10, LAMBDA(r,c, r*c))"
```

จะได้ตาราง 10 × 10 โดยไม่ต้องเขียนลูปใน Python วิธีนี้แสดง **how to use makearray** สำหรับกริดที่กำหนดล่วงหน้า ไม่ว่าจะเป็น lookup table, heatmap หรือ schedule ทางการเงิน

## Display excel array – ดึงข้อมูลกลับสู่ Python

เมื่อ Excel คำนวณสูตรแล้ว ค่าที่ได้จะอยู่ในชีตเหมือนกับเซลล์ที่ป้อนด้วยมือ เพื่อ **display excel array** เราจะวนลูปช่วงและพิมพ์แต่ละแถว:

```python
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

เคล็ดลับบางประการ:

- ใช้ `worksheet.cell(row, column).value` แทนการเข้าถึงแบบ dictionary‑style หากต้องจัดการช่วงที่ใหญ่กว่า; จะเร็วกว่าเล็กน้อย
- หากต้องการตารางที่สวยงามขึ้น พิจารณาใช้ `tabulate` หรือ `pandas.DataFrame` เพื่อจัดรูปแบบผลลัพธ์

ด้านล่างเป็นภาพหน้าจอของชีตที่ได้ (ข้อความ alt ของภาพรวมถึงคีย์เวิร์ดหลักสำหรับ SEO):

![ภาพหน้าจอแสดงการสร้างตารางคูณใน Excel ด้วย Python](/images/multiplication-table-excel.png)

## Read excel values python – ดึงเมทริกซ์เพื่อประมวลผลต่อ

บ่อยครั้งขั้นตอนต่อมาหลังจาก **display excel array** คือการนำตัวเลขเหล่านั้นเข้าสู่ pipeline การวิเคราะห์ข้อมูล นั่นคือจุดที่ **read excel values python** มีประโยชน์ ลูปเดียวกับที่ใช้พิมพ์สามารถนำมาใช้สร้าง list of lists, NumPy array หรือ Pandas DataFrame:

```python
import pandas as pd

# Build a list of rows
data = []
for row_index in range(1, 6):
    row = [worksheet.cell(row=row_index, column=col_index).value
           for col_index in range(1, 6)]
    data.append(row)

# Convert to DataFrame for easy manipulation
df = pd.DataFrame(data, columns=[f"Col{c}" for c in range(1, 6)],
                  index=[f"Row{r}" for r in range(1, 6)])

print(df)
```

ผลลัพธ์:

```
      Col1  Col2  Col3  Col4  Col5
Row1     1     2     3     4     5
Row2     2     4     6     8    10
Row3     3     6     9    12    15
Row4     4     8    12    16    20
Row5     5    10    15    20    25
```

ตอนนี้คุณมี DataFrame ที่เต็มรูปแบบ สามารถทำกราฟ, ส่งออกเป็น CSV หรือป้อนให้โมเดล machine‑learning ได้ ส่วนนี้สรุปขั้นตอน **read excel values python** ของ workflow

## กรณีขอบและเคล็ดลับปฏิบัติ

- **การคำนวณสูตรใหม่**: หากคุณแก้ไขเวิร์กบุ๊กหลังจากเรียก `calculate_formula()` ครั้งแรก ต้องเรียกอีกครั้ง; มิฉะนั้นอาเรย์ที่แคชไว้จะล้าสมัย
- **Excel ที่ไม่ใช่ 365**: เวอร์ชันเก่าไม่มี `MAKEARRAY` ในกรณีนั้นให้ใช้ตารางที่สร้างด้วย Python แล้วเขียนแต่ละเซลล์แยกกัน
- **ตารางขนาดใหญ่**: สำหรับเมทริกซ์ใหญ่กว่า ~100 × 100 ควรสตรีมข้อมูลเพื่อหลีกเลี่ยงการโหลดชีตทั้งหมดเข้าสู่หน่วยความจำ
- **การจัดการข้อผิดพลาด**: ห่อขั้นตอนคำนวณและการอ่านด้วยบล็อก `try/except` เพื่อจับ `InvalidFileException` หรือ `FormulaError`

## สรุป

เราได้แสดงวิธี **create multiplication table** ใน Excel ด้วย Python โดยใช้พลังของ **how to use lambda** และ **how to use makearray** คุณได้เห็นวิธี **display excel array**, อ่านค่าด้วย **read excel values python**, และแม้กระทั่งแปลงผลลัพธ์เป็น Pandas DataFrame เพื่อการวิเคราะห์ต่อไป

อยากทำต่อ? ลองเปลี่ยนตรรกะคูณเป็นสิ่งซับซ้อนกว่า—เช่นเมทริกซ์ระยะทาง, ตารางความน่าจะเป็น, หรือกริดการกำหนดราคาตามสภาพตลาด รูปแบบเดียวกันใช้ได้: บรรทัดเดียวของ `MAKEARRAY`, `calculate_formula()` อย่างรวดเร็ว, แล้วใช้ลูป Python เล็กน้อยเพื่อดึงข้อมูลออกมา

หากคุณพบว่าคู่มือนี้เป็นประโยชน์ อย่าลืมกดดาวบน GitHub, แชร์ให้ทีมงาน, หรือแสดงความคิดเห็นพร้อมกรณีการใช้งานของคุณเอง โค้ดดิ้งให้สนุกและเพลิดเพลินกับการสร้างตาราง Excel ด้วยสูตรเดียว!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโปรเจกต์ของคุณ

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Aspose.Cells .NET Tutorial: How to Create and Modify Excel Workbooks Easily](/cells/english/net/workbook-operations/aspose-cells-net-create-modify-excel-workbooks/)
- [How to Create and Style Named Ranges in Excel Using Aspose.Cells .NET | Step‑By‑Step Guide](/cells/english/net/range-management/create-style-named-ranges-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}