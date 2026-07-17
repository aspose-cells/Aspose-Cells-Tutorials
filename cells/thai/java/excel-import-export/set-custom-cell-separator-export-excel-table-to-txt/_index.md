---
category: general
date: 2026-07-16
description: ตั้งค่าตัวคั่นเซลล์แบบกำหนดเองเมื่อส่งออกตาราง Excel ไปเป็นไฟล์ TXT ด้วย
  Aspose.Cells. เรียนรู้วิธีส่งออกสูตร Excel เป็นข้อความและบันทึกแผ่นงานเป็นไฟล์ txt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom cell separator
- export excel table to txt
- export excel formulas to text
- save worksheet as txt file
- export excel data as plain text
language: th
lastmod: 2026-07-16
og_description: ตั้งค่าตัวคั่นเซลล์แบบกำหนดเองใน Aspose.Cells ช่วยให้คุณส่งออกตาราง
  Excel เป็นไฟล์ TXT ด้วยรูปแบบที่แม่นยำ ส่งออกสูตร Excel เป็นข้อความและบันทึกแผ่นงานเป็นไฟล์
  txt ได้อย่างง่ายดาย
og_image_alt: Screenshot showing set custom cell separator option in Aspose.Cells
  export settings
og_title: ตั้งค่าตัวคั่นเซลล์แบบกำหนดเอง – ส่งออกตาราง Excel เป็น TXT
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Set custom cell separator when exporting Excel table to TXT using Aspose.Cells.
    Learn how to export Excel formulas to text and save worksheet as txt file.
  headline: Set Custom Cell Separator – Export Excel Table to TXT
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel Export
title: ตั้งค่าตัวคั่นเซลล์แบบกำหนดเอง – ส่งออกตาราง Excel เป็น TXT
url: /th/java/excel-import-export/set-custom-cell-separator-export-excel-table-to-txt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ตั้งค่าตัวคั่นเซลล์แบบกำหนดเอง – ส่งออกตาราง Excel เป็น TXT

การตั้งค่าตัวคั่นเซลล์แบบกำหนดเองเป็นสูตรลับที่คุณต้องการเมื่ออยากได้การดึงข้อมูลเป็นข้อความที่เป็นระเบียบจากแผ่น Excel เคยสงสัยไหมว่าจะ **export excel table to txt** อย่างไรโดยไม่ต้องเจอข้อความที่เต็มไปด้วยเครื่องหมายจุลภาคและการขึ้นบรรทัดใหม่? ในบทแนะนำนี้เราจะเดินผ่านกระบวนการทั้งหมดโดยใช้ Aspose.Cells for Java ตั้งแต่การโหลดเวิร์กบุ๊กจนถึง **save worksheet as txt file** ด้วยตัวคั่นที่คุณเลือก

## สิ่งที่คุณจะได้เรียนรู้

- วิธี **set custom cell separator** สำหรับการส่งออกข้อความ.
- ขั้นตอนที่แน่นอนเพื่อ **export excel formulas to text** เพื่อให้ค่าที่ประเมินแล้วถูกส่งออกไปด้วย.
- วิธีการ **export excel data as plain text** พร้อมคงรูปแบบ.
- ตัวอย่างโค้ดที่สมบูรณ์และพร้อมรันที่คุณสามารถคัดลอก‑วางลงในโปรเจคของคุณ.

เมื่อจบคู่มือคุณจะสามารถนำเวิร์กบุ๊ก Excel ใด ๆ ก็ได้ เลือกตัวคั่นแบบ pipe (`|`), tab (`\t`) หรืออักขระใด ๆ ที่คุณต้องการ แล้วสร้างไฟล์ข้อความที่มีการคั่นอย่างเรียบร้อยซึ่งระบบต่อไปจะชอบใช้

### ข้อกำหนดเบื้องต้น

- ติดตั้ง Java 8 หรือใหม่กว่า
- Maven (หรือเครื่องมือสร้างใด ๆ) เพื่อดึงไลบรารี Aspose.Cells for Java
- เวิร์กบุ๊กตัวอย่าง (`TableDemo.xlsx`) ที่มีตารางพร้อมสูตร

ถ้าคุณมีทั้งหมดนี้แล้ว ไปต่อกันเลย—ไม่มีเนื้อหาเกินความจำเป็น เพียงขั้นตอนที่เป็นประโยชน์

## ขั้นตอนที่ 1: เพิ่ม Aspose.Cells ไปยังโปรเจคของคุณ

ก่อนที่คุณจะ **set custom cell separator** คุณต้องมีไฟล์ JAR ของ Aspose.Cells อยู่ใน classpath วิธีที่ง่ายที่สุดคือผ่าน Maven:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

หากคุณชอบใช้ Gradle ให้เปลี่ยน XML เป็น `implementation 'com.aspose:aspose-cells:24.10'` เมื่อจัดการ dependency แล้ว คุณก็พร้อมเขียนโค้ด Java ที่ทำงานกับไฟล์ Excel

## ขั้นตอนที่ 2: โหลดเวิร์กบุ๊ก – เตรียมส่งออกตาราง Excel เป็น TXT

บรรทัดโค้ดแรกที่สำคัญมักจะเหมือนกันเสมอ: เปิดเวิร์กบุ๊กที่มีตารางที่คุณต้องการส่งออก

```java
import com.aspose.cells.*;

public class ExportTableWithOptions {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/TableDemo.xlsx");
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

ที่นี่เราดึง worksheet แรก (`get(0)`) หากข้อมูลของคุณอยู่ในชีตอื่น เพียงเปลี่ยนดัชนีหรือใช้ `get("SheetName")` ส่วนนี้สำคัญสำหรับ **export excel table to txt** เนื่องจากตัวส่งออกทำงานระดับ worksheet

## ขั้นตอนที่ 3: ตั้งค่าตัวคั่นเซลล์แบบกำหนดเอง – แกนหลักของการส่งออก

ต่อไปคือส่วนสำคัญของกระบวนการ: การกำหนดค่า `ExportTableOptions` วัตถุนี้ให้คุณกำหนดอย่างแม่นยำว่าตารางแต่ละเซลล์จะปรากฏอย่างไรในไฟล์ข้อความสุดท้าย

```java
        // Define how the table should be exported
        ExportTableOptions exportTableOptions = new ExportTableOptions();

        // 1️⃣ Export cell contents as plain strings (no rich formatting)
        exportTableOptions.setExportAsString(true);

        // 2️⃣ Include the evaluated formula result, not the formula itself
        exportTableOptions.setFormulaValueInCell(true);

        // 3️⃣ Set the custom separator – this is where we set custom cell separator
        exportTableOptions.setCellValueSeparator("|"); // you can use any char you like
```

ทำไมเราต้อง **set custom cell separator**? เพราะตัวคั่นเริ่มต้นคือแท็บ ซึ่งอาจชนกับข้อมูลที่มีแท็บอยู่แล้ว การเลือก pipe (`|`) หรือเซมิโคลอน จะทำให้แต่ละคอลัมน์แยกจากกันอย่างชัดเจนเมื่อโปรแกรมอ่านต่อมาวิเคราะห์ไฟล์

### ส่งออกสูตร Excel เป็นข้อความ

บรรทัด `setFormulaValueInCell(true)` บอก Aspose.Cells ให้เขียน **export excel formulas to text** เป็น *ผลลัพธ์* ของสูตร ไม่ใช่ข้อความสูตรเอง หากคุณละเว้นบรรทัดนี้ เซลล์ที่มี `=SUM(A1:A5)` จะปรากฏเป็น `=SUM(A1:A5)` ในไฟล์ TXT ซึ่งมักไม่ใช่สิ่งที่ต้องการ

## ขั้นตอนที่ 4: แนบตัวเลือกการส่งออกเข้ากับ TXT Save Options

ตอนนี้เรานำตัวเลือกตารางเหล่านั้นผูกเข้ากับการกำหนดค่าการส่งออก TXT ทั้งหมด

```java
        // Attach the table export options to TXT save options
        TxtSaveOptions txtSaveOptions = new TxtSaveOptions();
        txtSaveOptions.setExportTableOptions(exportTableOptions);
```

`TxtSaveOptions` คืออ็อบเจกต์หลักที่ควบคุมการเขียน worksheet ทั้งหมดออกมา โดยการใส่ `exportTableOptions` เข้าไป คุณจะทำให้ทุกตารางบนชีตปฏิบัติตามกฎ **set custom cell separator**

## ขั้นตอนที่ 5: บันทึก Worksheet เป็นไฟล์ TXT – สรุปการส่งออก

สุดท้าย เราเขียนไฟล์ลงดิสก์

```java
        // Save the worksheet as a TXT file using the configured options
        workbook.save("YOUR_DIRECTORY/TableExported.txt", txtSaveOptions);
    }
}
```

การรันโปรแกรมนี้จะสร้างไฟล์ `TableExported.txt` แต่ละแถวของตาราง Excel ดั้งเดิมจะปรากฏเป็นบรรทัดของค่าที่คั่นด้วย pipe, เช่น:

```
Name|Quantity|Price|Total
Apple|10|0.50|5.00
Banana|5|0.30|1.50
```

สังเกตว่าสูตรในคอลัมน์ **Total** ถูกประเมินผลก่อนเขียนลงไฟล์—ขอบคุณ `setFormulaValueInCell(true)` นั่นคือสาระสำคัญของ **export excel data as plain text** พร้อมคงผลลัพธ์ที่คำนวณไว้

## ขั้นตอนที่ 6: ตรวจสอบผลลัพธ์ – เป็นอย่างที่ต้องการหรือไม่?

เปิดไฟล์ `TableExported.txt` ที่สร้างขึ้นในโปรแกรมแก้ไขข้อความใดก็ได้ คุณควรเห็น:

- หนึ่งบรรทัดต่อหนึ่งแถวของ Excel
- คอลัมน์คั่นด้วยอักขระ pipe ที่คุณตั้งค่าโดยใช้ `setCellValueSeparator`
- ไม่มีเครื่องหมายจุลภาคหรือแท็บที่ไม่ได้ตั้งใจ ยกเว้นกรณีที่เป็นส่วนหนึ่งของค่าของเซลล์เดิม
- ผลลัพธ์ของสูตร ไม่ใช่สูตรเอง

หากคุณพบอักขระที่ไม่คาดคิด ให้ตรวจสอบตัวคั่นที่เลือกอีกครั้ง บางอักขระ (เช่น pipe) ปลอดภัยสำหรับตัวแยกแบบ CSV ส่วนใหญ่ แต่หากข้อมูลของคุณมี pipe อยู่แล้ว ให้พิจารณาใช้ตัวคั่นอื่น เช่น `~` หรือแท็บ (`\t`)

## เคล็ดลับ, กรณีขอบ, และแนวปฏิบัติที่ดีที่สุด – Export Excel Data as Plain Text

| สถานการณ์ | วิธีทำ |
|-----------|------------|
| **ข้อมูลมีตัวคั่นที่คุณเลือกอยู่แล้ว** | เปลี่ยนไปใช้อักขระที่ไม่ค่อยใช้ (`^`, `~`, หรืออักขระ Unicode ที่ไม่แสดงผล). |
| **คุณต้องการการเข้ารหัส UTF‑8** |  |

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดที่ทำงานได้เต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้แบบอื่นในโปรเจคของคุณ

- [บันทึก Excel เป็นไฟล์ข้อความด้วยตัวคั่นแบบกำหนดเองโดยใช้ Aspose.Cells](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [บันทึกข้อความ Excel ตัวคั่นแบบกำหนดเอง Aspose Cells Net](/cells/german/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [บันทึกข้อความ Excel ตัวคั่นแบบกำหนดเอง Aspose Cells Net](/cells/french/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}