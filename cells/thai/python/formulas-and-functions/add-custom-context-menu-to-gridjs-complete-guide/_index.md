---
category: general
date: 2026-06-08
description: เพิ่มเมนูคอนเท็กซ์แบบกำหนดเองใน GridJs และส่งออกกริดเป็น CSV พร้อมดาวน์โหลดไฟล์
  CSV เป็น Blob. ทำตามบทแนะนำขั้นตอนต่อไปนี้เพื่อดูตัวอย่างที่ทำงานได้เต็มรูปแบบ.
draft: false
keywords:
- add custom context menu
- export grid to csv
- download csv file blob
- GridJs context menu
- Flask CSV export
language: th
og_description: เพิ่มเมนูคลิกขวาแบบกำหนดเองใน GridJs และส่งออกกริดเป็น CSV พร้อมดาวน์โหลดไฟล์
  CSV เป็น Blob เรียนรู้การทำงานเต็มรูปแบบภายในเวลาไม่เกิน 10 นาที.
og_title: เพิ่มเมนูคอนเท็กซ์แบบกำหนดเองใน GridJs – คู่มือฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Add custom context menu to GridJs and export grid to CSV with a download
    CSV file blob. Follow this step‑by‑step tutorial for a fully working example.
  headline: Add Custom Context Menu to GridJs – Complete Guide
  type: TechArticle
tags:
- GridJs
- JavaScript
- Python
- Flask
title: เพิ่มเมนูบริบทแบบกำหนดเองให้กับ GridJs – คู่มือฉบับสมบูรณ์
url: /th/python/formulas-and-functions/add-custom-context-menu-to-gridjs-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เพิ่มเมนูคลิกขวาที่กำหนดเองให้ GridJs – คู่มือเต็ม

ต้องการ **เพิ่มเมนูคลิกขวาที่กำหนดเอง** ให้กับคอมโพเนนต์ GridJs หรือไม่? ในบทแนะนำนี้เราจะพาคุณผ่านขั้นตอนนั้นอย่างละเอียด และแสดงวิธี **ส่งออกกริดเป็น CSV** โดยใช้ **download CSV file blob**. ไม่ว่าคุณจะสร้างแผงผู้ดูแลระบบแบบเร็วหรือแดชบอร์ดรายงานที่เต็มรูปแบบ เมนูคลิกขวาที่ช่วยให้ผู้ใช้ดึงข้อมูลออกเป็น CSV สามารถเพิ่มประสิทธิภาพการทำงานได้จริง.

เราจะครอบคลุมทุกอย่างที่คุณต้องการ: ด้าน Python กับ Flask, ตัวจัดการ JavaScript ที่สร้าง Blob, และ HTML/JS ที่ GridJs สร้างขึ้น. เมื่อจบคุณจะมีตัวอย่างที่เป็นอิสระซึ่งสามารถนำไปใส่ในโปรเจกต์ใดก็ได้.

---

## สิ่งที่คุณต้องเตรียม

ก่อนที่เราจะเริ่มลงลึก, ตรวจสอบให้แน่ใจว่าคุณมี:

- **Python 3.9+** และ **Flask** ที่ติดตั้งแล้ว (`pip install flask`).
- **gridjs** Python wrapper (หรือไลบรารี JavaScript โดยตรง) – สำหรับคู่มือนี้เราจะสมมติว่ามี Python wrapper ที่บางเบาซึ่งสะท้อน API ของ JavaScript.
- ความเข้าใจพื้นฐานเกี่ยวกับ **async JavaScript** (`fetch`, `Promise`) – แต่ไม่ต้องกังวล, เราจะอธิบายแต่ละบรรทัด.
- โปรแกรมแก้ไขที่คุณชอบ (VS Code, PyCharm, หรือแม้แต่โปรแกรมแก้ไขข้อความธรรมดาก็ใช้ได้).

เท่านี้แหละ. ไม่ต้องใช้เครื่องมือสร้าง front‑end เพิ่มเติม, ไม่ต้องทำ Node npm. เพียง Flask ธรรมดาที่ให้บริการ HTML ที่ GridJs สร้าง.

---

## เพิ่มเมนูคลิกขวาที่กำหนดเองให้ GridJs

สิ่งแรกที่คุณต้องทำคือบอก GridJs ว่าคุณต้องการเมนูคลิกขวาที่กำหนดเอง. โดยค่าเริ่มต้น GridJs มาพร้อมชุดเมนูขั้นต่ำ (คัดลอก, วาง, ฯลฯ), แต่คุณสามารถแทนที่ทั้งหมดได้.

```python
# Step 1: Create a new workbook that will be displayed in the grid
workbook = Workbook()

# Step 2: Initialise the GridJs component with the workbook
grid_js = GridJs(workbook)

# Step 3: Define a custom context‑menu that includes an "Export CSV" command
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]
```

**ทำไมเรื่องนี้ถึงสำคัญ:**  
การตั้งค่า `CustomContextMenu` จะทดแทนรายการเริ่มต้นด้วยรายการที่คุณกำหนด. สตริง `"Export CSV"` เป็นเพียงป้ายชื่อ – งานจริงจะเกิดขึ้นเมื่อผู้ใช้คลิก, ซึ่งเราจะเชื่อมต่อในขั้นตอนต่อไป.

> *เคล็ดลับ:* ให้รายการสั้น. เมนูคลิกขวาที่รกจะทำลายจุดประสงค์ของการกระทำที่รวดเร็ว.

---

## ส่งออกกริดเป็น CSV ด้วยการดาวน์โหลด Blob

ตอนนี้เมนูไอเท็มมีแล้ว, เราต้องการตัวจัดการ JavaScript ที่สื่อสารกับเซิร์ฟเวอร์, ดึง CSV, แปลงเป็น **Blob**, และบังคับให้ดาวน์โหลด. นี่คือที่ที่วลี **download CSV file blob** ปรากฏ.

```python
# Step 4: Attach a JavaScript handler that runs when "Export CSV" is chosen.
#         The handler sends an AJAX request to a server endpoint,
#         receives the CSV file as a Blob, and triggers a download.
grid_js.CustomContextMenuHandler = """
function(action, cell) {
    if (action === "Export CSV") {
        fetch('/export/csv?sheet=' + cell.sheetName)
            .then(r => r.blob())
            .then(b => {
                const url = URL.createObjectURL(b);
                const a = document.createElement('a');
                a.href = url;
                a.download = cell.sheetName + ".csv";
                a.click();
            });
    }
}
"""
```

### แยกส่วนตัวจัดการ

| บรรทัด | ทำอะไร |
|------|--------------|
| `fetch('/export/csv?sheet=' + cell.sheetName)` | เรียกเส้นทาง Flask (`/export/csv`) โดยส่งชื่อชีตเป็น query string. |
| `.then(r => r.blob())` | แปลงการตอบกลับ HTTP เป็น **Blob** – ซึ่งเป็นคอนเทนเนอร์ไบนารีสำหรับข้อมูล CSV. |
| `URL.createObjectURL(b)` | สร้าง URL ชั่วคราวที่เบราว์เซอร์สามารถถือว่าเป็นไฟล์ได้. |
| `a.download = cell.sheetName + ".csv"` | ตั้งชื่อไฟล์ที่ผู้ใช้จะเห็นในกล่องโต้ตอบการดาวน์โหลด. |
| `a.click()` | คลิกแท็ก `<a>` ที่ซ่อนอยู่โดยโปรแกรม, ทำให้เบราว์เซอร์ดาวน์โหลด Blob. |

> **ทำไมต้องใช้ Blob?**  
> เบราว์เซอร์ไม่สามารถดาวน์โหลดข้อความดิบที่คืนจาก `fetch` ได้โดยตรงโดยไม่แปลงเป็นสิ่งที่คล้ายไฟล์. เทคนิค Blob‑URL เป็นวิธีที่เชื่อถือได้ที่สุด, ทำงานข้ามเบราว์เซอร์เพื่อเรียกใช้ **download CSV file blob** โดยไม่ต้องรีเฟรชหน้า.

---

## ตั้งค่า Flask Backend

ตัวจัดการ front‑end คาดหวัง endpoint ที่ `/export/csv`. นี่คือตัวอย่าง view ของ Flask อย่างง่ายที่รับชื่อชีต, ดึงข้อมูลจาก workbook, และส่ง CSV กลับ.

```python
from flask import Flask, request, Response
import csv
import io

app = Flask(__name__)

# Assume `workbook` is a global object we created earlier
# (in a real app you’d probably fetch it from a database or session)
@app.route('/export/csv')
def export_csv():
    sheet_name = request.args.get('sheet', 'default')
    # Retrieve the sheet data – this is pseudo‑code; replace with your actual API
    sheet = workbook.get_sheet(sheet_name)

    # Convert rows to CSV in memory
    output = io.StringIO()
    writer = csv.writer(output)
    writer.writerow(sheet.headers)          # Header row
    writer.writerows(sheet.rows)            # Data rows

    # Create a Flask response with the correct MIME type
    csv_bytes = output.getvalue().encode('utf-8')
    return Response(
        csv_bytes,
        mimetype='text/csv',
        headers={'Content-Disposition': f'attachment;filename={sheet_name}.csv'}
    )
```

### จุดสำคัญ

- **`io.StringIO`** ทำให้เราสร้าง CSV ในหน่วยความจำโดยไม่ต้องเข้าถึงระบบไฟล์.
- **`Content‑Disposition`** บอกเบราว์เซอร์ว่าไฟล์เป็น attachment และแนะนำชื่อไฟล์. แม้ว่า front‑end จะตั้งค่า `a.download` ด้วย, การกำหนดบนเซิร์ฟเวอร์ให้เป็นทางสำรองสำหรับไคลเอนต์ที่ไม่ใช้ JS.
- เส้นทางนี้ตั้งใจให้เรียบง่าย; คุณสามารถเพิ่มการตรวจสอบสิทธิ์, การตรวจสอบการอนุญาต, หรือการสตรีมสำหรับชุดข้อมูลขนาดใหญ่ในภายหลัง.

---

## การแสดงผล Grid บน Client

เมื่อเมนูคลิกขวาและ backend พร้อม, ส่วนสุดท้ายคือการเรนเดอร์คอมโพเนนต์ GridJs และส่ง HTML/JS ไปยังเบราว์เซอร์.

```python
# Step 5: Render the grid to obtain the full HTML/JS needed on the client side
html_output = grid_js.Render()
print(html_output)   # Sends the HTML/JS to the client (e.g., in a Flask view)
```

ใน view ของ Flask คุณมักทำแบบนี้:

```python
@app.route('/')
def index():
    html_output = grid_js.Render()
    return f"""
    <!doctype html>
    <html>
    <head>
        <title>Grid with Custom Context Menu</title>
        <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
        <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
    </head>
    <body>
        {html_output}
    </body>
    </html>
    """
```

เมื่อหน้าโหลด, GridJs จะสร้างตาราง, แทรกเมนูคลิกขวาที่กำหนดเอง, และตัวจัดการ JavaScript ที่เรากำหนดไว้ก่อนหน้านี้พร้อมทำงาน. คลิกขวาที่เซลล์ใดก็ได้, เลือก **Export CSV**, แล้วดูเบราว์เซอร์ดาวน์โหลดไฟล์ที่มีชื่อตามชีต.

---

## ตัวอย่างทำงานเต็ม (ทุกไฟล์)

ด้านล่างเป็นโค้ดที่สมบูรณ์และสามารถรันได้ซึ่งคุณสามารถคัดลอก‑วางไปยังโฟลเดอร์ใหม่. ติดตั้ง Flask (`pip install flask`) และรัน `python app.py`.

**`app.py`**



## สิ่งที่คุณควรเรียนต่อไป

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้. แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานทางเลือกในโปรเจกต์ของคุณ.

- [โหลดไฟล์ CSV ด้วยตัวแยกแบบกำหนดเอง Aspose Cells Java](/cells/hindi/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)
- [โค้ดการส่งออก CSV ด้วย Java](/cells/hindi/java/excel-import-export/csv-export-java-code/)
- [ส่งออก Excel CSV แถวว่าง Aspose Cells .NET](/cells/hindi/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}