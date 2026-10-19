---
category: general
date: 2026-08-14
description: คัดลอกช่วงข้อมูลระหว่างเวิร์กบุ๊กด้วย Java โดยใช้ Aspose.Cells. เรียนรู้การคัดลอก
  Pivot Table ระหว่างเวิร์กบุ๊ก, ส่งออกรูปภาพไปยัง PowerPoint และลบ AutoFilter จากตาราง
  Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range between workbooks
- copy pivot table workbook
- export picture to powerpoint
- copy excel range to new workbook
- remove autofilter from excel table
language: th
lastmod: 2026-08-14
og_description: คัดลอกช่วงข้อมูลระหว่างเวิร์กบุ๊กใน Java. คู่มือนี้แสดงวิธีคัดลอกเวิร์กบุ๊ก
  Pivot Table, ส่งออกรูปภาพไปยัง PowerPoint และลบ AutoFilter จากตาราง Excel.
og_image_alt: Screenshot of Java code copying range between workbooks with Aspose.Cells
og_title: คัดลอกช่วงข้อมูลระหว่างเวิร์กบุ๊กใน Java – คู่มือ Aspose.Cells ฉบับเต็ม
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Copy range between workbooks with Java using Aspose.Cells. Learn to
    copy pivot table workbook, export picture to PowerPoint and remove AutoFilter
    from Excel table.
  headline: Copy range between workbooks in Java – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: คัดลอกช่วงข้อมูลระหว่างเวิร์กบุ๊กใน Java – คู่มือแบบทีละขั้นตอน
url: /th/java/range-management/copy-range-between-workbooks-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# คัดลอกช่วงระหว่างเวิร์กบุ๊กใน Java – คู่มือแบบขั้นตอนต่อขั้นตอน

หากคุณต้องการ **คัดลอกช่วงระหว่างเวิร์กบุ๊ก** ใน Java, Aspose.Cells มี API ที่สะอาดและจัดการกับวัตถุซับซ้อนเช่น pivot tables และรูปภาพ บทแนะนำนี้แสดงวิธี **คัดลอกเวิร์กบุ๊กของ pivot table**, **ส่งออกรูปภาพไปยัง PowerPoint**, และ **ลบ AutoFilter จากตาราง Excel** พร้อมให้โค้ดอ่านง่ายและบำรุงรักษาได้ง่าย

คุณจะได้เรียนรู้วิธี:

* โหลดเวิร์กบุ๊กต้นฉบับและกำหนดช่วงต้นฉบับ  
* สร้างเวิร์กบุ๊กปลายทางและคัดลอกช่วงเพื่อให้ pivot table คงอยู่ครบถ้วน  
* ส่งออกรูปภาพแรกบนแผ่นงานเป็นออบเจ็กต์ PowerPoint ที่แก้ไขได้  
* ลบ AutoFilter จากตาราง Excel แรก  
* โหลดเวิร์กบุ๊กด้วย `SmartMarkerOptions` เพื่อจัดการอาเรย์ JSON เป็นค่าเซลล์เดียว

ตัวอย่างใช้ Aspose.Cells 23.10 สำหรับ Java, แต่แนวคิดสามารถนำไปใช้กับเวอร์ชันก่อนหน้าได้เช่นกัน

---

## Prerequisites

| Requirement | Why it matters |
|-------------|----------------|
| Java 17 หรือใหม่กว่า | จำเป็นสำหรับ runtime ของ Aspose.Cells เวอร์ชันล่าสุด |
| Aspose.Cells for Java (Maven artifact `com.aspose:aspose-cells`) | ให้คลาส `Workbook`, `Worksheet`, `Range` และคลาสที่เกี่ยวข้องที่ใช้ในโค้ด |
| ไฟล์ Excel ต้นฉบับ (`src.xlsx`) ที่มี pivot table, รูปภาพ, และตารางที่มี AutoFilter | บทแนะนำจะจัดการกับวัตถุเหล่านี้เพื่อสาธิตแต่ละฟีเจอร์ |

เพิ่มการพึ่งพา Maven ลงในไฟล์ `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Copy range between workbooks – load source and destination

ขั้นตอนแรกคือเปิดเวิร์กบุ๊กต้นฉบับ, เลือกช่วงที่มีข้อมูลที่คุณต้องการคัดลอก, และสร้างเวิร์กบุ๊กปลายทางเปล่า

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table, picture, and table.
        Workbook sourceWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceWs = sourceWb.getWorksheets().get(0);

        // Define the range that includes the pivot table (A1:G20 in this example).
        Range sourceRange = sourceWs.getCells().createRange("A1:G20");

        // Create a new workbook that will receive the copied range.
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
        Range destRange = destWs.getCells().createRange("A1");
```

> **Why this matters:** โดยใช้ `Range.copy`, Aspose.Cells จะคัดลอกไม่เพียงค่าเซลล์ดิบแต่รวมถึง pivot cache ที่อยู่ภายใต้ด้วย, ทำให้ pivot table ทำงานได้ในเวิร์กบุ๊กปลายทาง

---

## Copy pivot table workbook while copying the range

ตอนนี้คัดลอกช่วงที่กำหนดจากเวิร์กบุ๊กต้นฉบับไปยังเวิร์กบุ๊กปลายทาง Pivot table จะถูกเก็บไว้โดยอัตโนมัติเนื่องจากช่วงนั้นรวม pivot cache ไว้ด้วย

```java
        // Copy the source range to the destination range.
        destRange.copy(sourceRange);

        // Save the intermediate workbook to verify that the pivot table was copied.
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
```

> **Result:** การเปิด `destination.xlsx` จะแสดงเค้าโครง pivot table เหมือนกับ `src.xlsx`. ไม่จำเป็นต้องเขียนโค้ดเพิ่มเติมเพื่อสร้าง pivot cache ใหม่

---

## Export picture to PowerPoint

Aspose.Cells สามารถทำเครื่องหมายรูปภาพเพื่อส่งออกเป็นออบเจ็กต์ PowerPoint ที่แก้ไขได้ โค้ดต่อไปนี้จะเลือกรูปภาพแรกบนแผ่นงานปลายทางและตั้งค่าสถานะการส่งออก

```java
        // Retrieve the first picture on the destination sheet.
        Shape picture = destWs.getPictures().get(0);

        // Instruct Aspose.Cells to export this picture as a PowerPoint object.
        picture.getPictureFormat().setExportToPptx(true);

        // Optionally, save the workbook as PPTX to see the result.
        destWb.save("YOUR_DIRECTORY/destination.pptx");
```

> **What you see:** การเปิด `destination.pptx` ใน PowerPoint จะเห็นรูปภาพเป็น shape แบบเนทีฟที่คุณสามารถแก้ไข, ปรับขนาด, หรือทำแอนิเมชันได้

---

## Remove AutoFilter from Excel table

หากแผ่นงานต้นฉบับมีตารางที่มี AutoFilter, คุณอาจต้องการลบมันหลังจากคัดลอก โค้ดด้านล่างจะเข้าถึงตารางแรกและลบฟิลเตอร์ออก

```java
        // Access the first table on the destination sheet.
        Table table = destWs.getTables().get(0);

        // Remove the AutoFilter by assigning null.
        table.setAutoFilter(null);

        // Save the final workbook.
        destWb.save("YOUR_DIRECTORY/final_output.xlsx");
```

> **Effect:** ตารางยังคงอยู่ในเวิร์กบุ๊ก, แต่ลูกศรฟิลเตอร์แบบดรอป‑ดาวน์จะหายไป, ทำให้คุณเห็นมุมมองข้อมูลที่สะอาดตา

---

## Load workbook with SmartMarker options – treat JSON arrays as a single cell

เมื่อคุณสร้างรายงานจาก JSON, Aspose.Cells สามารถจัดการอาเรย์ทั้งหมดเป็นค่าเซลล์เดียวได้ ซึ่งเป็นประโยชน์สำหรับการฝังสตริง JSON ลงในเทมเพลตโดยไม่ต้องขยายเป็นหลายเซลล์

```java
        // Configure LoadOptions to enable SmartMarker array handling.
        LoadOptions loadOptions = new LoadOptions();
        SmartMarkerOptions smOptions = new SmartMarkerOptions();
        smOptions.setArrayAsSingle(true);
        loadOptions.setSmartMarkerOptions(smOptions);

        // Load a template workbook using the configured options.
        Workbook smartMarkerWb = new Workbook("YOUR_DIRECTORY/template.xlsx", loadOptions);

        // Continue processing (e.g., populate markers) as needed.
        // ...

        // Save the processed workbook.
        smartMarkerWb.save("YOUR_DIRECTORY/template_filled.xlsx");
    }
}
```

> **Why you might use this:** หาก payload JSON ของคุณมีอาเรย์ที่ควรแสดงเป็นสตริง JSON ในเซลล์เดียว, `setArrayAsSingle(true)` จะป้องกันไม่ให้ Aspose.Cells ขยายอาเรย์เป็นแถวหรือคอลัมน์แยกกัน

---

![Copy range between workbooks in Java – Aspose.Cells code example](copy-range-workbooks.png)

*Image alt text:* **คัดลอกช่วงระหว่างเวิร์กบุ๊กใน Java – ตัวอย่างโค้ด Aspose.Cells** (matches the primary keyword)

---

## Expected output

| File name                | Contains |
|--------------------------|----------|
| `destination.xlsx`       | ช่วงที่คัดลอกพร้อม pivot table ที่ทำงานได้ |
| `destination.pptx`       | รูปภาพที่ส่งออกเป็น shape PowerPoint ที่แก้ไขได้ |
| `final_output.xlsx`      | ตารางที่ไม่มีลูกศร AutoFilter |
| `template_filled.xlsx`   | อาเรย์ JSON ถูกเก็บเป็นค่าเซลล์เดียว |

เปิดแต่ละไฟล์ในแอปพลิเคชันที่เหมาะสม (Excel หรือ PowerPoint) เพื่อยืนยันว่าการดำเนินการสำเร็จ

---

## Conclusion

ตอนนี้คุณรู้วิธี **คัดลอกช่วงระหว่างเวิร์กบุ๊ก** ใน Java ด้วย Aspose.Cells, พร้อมคง pivot table, ส่งออกรูปภาพไปยัง PowerPoint, และลบ AutoFilter จากตาราง Excel แล้ว แพทเทิร์นเดียวกันนี้สามารถขยายเพื่อคัดลอกช่วง Excel ใด ๆ ไปยังเวิร์กบุ๊กใหม่, จัดการอาเรย์ JSON ของ SmartMarker, หรือเชื่อมต่อการแปลงเพิ่มเติมได้

ขั้นตอนต่อไปที่คุณอาจสำรวจ:

* **Copy Excel range to new workbook** พร้อมหลายแผ่นงาน  
* ใช้ **export picture to PowerPoint** สำหรับการสกัดภาพเป็นชุด  
* ใช้ **remove autofilter from excel table** ใน pipeline รายงานขนาดใหญ่  
* ผสานเทคนิคเหล่านี้กับ Aspose.Slides เพื่อทำการอัตโนมัติเต็มรูปแบบจาก Excel ไปยัง PowerPoint

อย่ากลัวทดลองกับที่อยู่ช่วงต่าง ๆ, pivot table หลายตัว, หรือรูปแบบรูปภาพที่กำหนดเอง Aspose.Cells API ถูกออกแบบให้ยืดหยุ่นสำหรับการเขียนโปรแกรม, ดังนั้นคุณสามารถปรับรูปแบบที่แสดงในที่นี้ให้เข้ากับสถานการณ์อัตโนมัติ Excel ขององค์กรได้ทุกกรณี

## What Should You Learn Next?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้แบบต่าง ๆ ในโครงการของคุณ

- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Copy Page Setup Settings Between Worksheets in Excel Using Aspose.Cells Java](/cells/english/java/headers-footers/copy-page-setup-excel-aspose-cells-java/)
- [Excel Copy Worksheets Between Workbooks](/cells/english/net/excel-copy-worksheet/excel-copy-worksheets-between-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}