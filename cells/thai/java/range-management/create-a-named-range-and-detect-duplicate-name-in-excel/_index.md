---
category: general
date: 2026-09-27
description: สร้างช่วงที่มีชื่อใน Excel ด้วย Aspose.Cells, ตั้งชื่อตาราง, เพิ่มช่วงที่มีชื่อ,
  สร้างตาราง Excel, และตรวจจับข้อผิดพลาดชื่อซ้ำ.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create named range
- set table name
- create excel table
- add named range
- detect duplicate name
language: th
lastmod: 2026-09-27
og_description: สร้างช่วงที่มีชื่อใน Excel ด้วย Aspose.Cells จากนั้นตั้งชื่อตาราง,
  เพิ่มช่วงที่มีชื่อ, สร้างตาราง Excel และตรวจจับข้อผิดพลาดชื่อซ้ำ
og_image_alt: Screenshot showing how to create a named range in Excel with Aspose.Cells
og_title: สร้างช่วงที่มีชื่อและตรวจจับชื่อซ้ำใน Excel
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Create a named range in Excel using Aspose.Cells, set table name, add
    named range, create Excel table, and detect duplicate name errors.
  headline: Create a named range and detect duplicate name in Excel
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: สร้างช่วงที่มีชื่อและตรวจจับชื่อซ้ำใน Excel
url: /th/java/range-management/create-a-named-range-and-detect-duplicate-name-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง Named Range และตรวจจับชื่อซ้ำใน Excel

หากคุณต้องการ **สร้าง named range** ในเวิร์กบุ๊ก Excel และต้องการหลีกเลี่ยงการชนกันของชื่อ คำแนะนำนี้จะแสดงวิธีทำอย่างละเอียดด้วย Aspose.Cells for Java คุณจะได้เรียนรู้การ **เพิ่ม named range**, **สร้างตาราง Excel**, **ตั้งชื่อตาราง**, และ **ตรวจจับข้อผิดพลาดชื่อซ้ำ** ในตัวอย่างเดียวที่สมบูรณ์แบบ

การทำงานกับ named range เป็นความต้องการทั่วไปเมื่อคุณสร้างเครื่องมือรายงาน, แผ่นตรวจสอบข้อมูล, หรือแดชบอร์ดแบบไดนามิก เมื่อจบบทเรียนนี้คุณจะมีโปรแกรมที่รันได้ซึ่งสร้าง named range อย่างปลอดภัย, สร้างตาราง, และจัดการข้อยกเว้นจากการชนกันของชื่ออย่างราบรื่น

## ข้อกำหนดเบื้องต้น

- Java 17 หรือเวอร์ชันใหม่กว่า
- Maven หรือ Gradle สำหรับการจัดการ dependencies
- Aspose.Cells for Java (เวอร์ชันล่าสุด; Maven coordinate `com.aspose:aspose-cells:23.9` ณ เวลาที่เขียน)
- ความคุ้นเคยพื้นฐานกับแนวคิดของ Excel เช่น worksheets, ranges, และ tables

## ขั้นตอนที่ 1: สร้าง named range ในเวิร์กบุ๊ก

ขั้นตอนแรกคือการสร้างอ็อบเจกต์ `Workbook` และเพิ่ม named range ที่ชี้ไปยังบล็อกเซลล์เฉพาะ

```java
import com.aspose.cells.*;

public class NamedRangeDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the default first worksheet (named "Sheet1")
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Define a named range called "MyRange" that covers A1:C5
        // This demonstrates the "add named range" operation.
        workbook.getNames().add("MyRange", "'Sheet1'!$A$1:$C$5");
```

**ทำไมจึงสำคัญ:**  
named range ทำหน้าที่เป็นอ้างอิงที่ใช้ซ้ำได้ ซึ่งสูตรและตารางสามารถอ้างอิงได้ การเพิ่มมันตั้งแต่ต้นทำให้ขั้นตอนต่อไปสามารถใช้ตัวระบุเดียวกันโดยไม่ต้องเขียนที่อยู่เซลล์แบบฮาร์ดโค้ด

## ขั้นตอนที่ 2: สร้างตาราง Excel ที่ใช้ named range

ต่อไปเราจะสร้างตารางแบบโครงสร้าง (ListObject) ที่ครอบคลุมพื้นที่เดียวกับ named range ซึ่งแสดงแนวคิด **create excel table**

```java
        // Create an Excel table (ListObject) that spans the same area as the named range.
        // The parameters (0,0,4,2) represent the top‑left cell (A1) and bottom‑right cell (C5).
        ListObject table = sheet.getListObjects().add(0, 0, 4, 2, true);
```

**ทำไมจึงสำคัญ:**  
ตารางให้ฟีเจอร์การจัดเรียง, การกรอง, และการจัดรูปแบบในตัว การจัดตารางให้สอดคล้องกับ named range ทำให้โมเดลข้อมูลคงที่

## ขั้นตอนที่ 3: ตั้งชื่อตารางและจัดการความขัดแย้งที่อาจเกิดขึ้น

ต่อมาเราจะพยายามตั้งชื่อตารางให้ตรงกับ named range ที่สร้างไว้ก่อนหน้านี้ ขั้นตอนนี้แสดง **set table name** และกระตุ้นความขัดแย้งของชื่อโดยเจตนา

```java
        try {
            // Attempt to set the table name to "MyRange".
            // Because a named range with the same identifier already exists,
            // Aspose.Cells will throw an exception.
            table.setName("MyRange"); // <-- conflict expected
        } catch (Exception e) {
            // Step 4: Detect duplicate name and respond appropriately
            System.out.println("Name conflict detected: " + e.getMessage());
        }
```

**ทำไมจึงสำคัญ:**  
Excel ไม่อนุญาตให้ตารางและ named range ใช้ตัวระบุเดียวกัน การตรวจจับความขัดแย้งตั้งแต่ต้นช่วยป้องกันเวิร์กบุ๊กเสียหายและทำให้การดีบักง่ายขึ้น

## ขั้นตอนที่ 4: ตรวจจับชื่อซ้ำและแก้ไข

เมื่อจับข้อยกเว้นได้ คุณสามารถเปลี่ยนชื่อของตารางหรือเอา named range ที่ขัดแย้งออกได้ ด้านล่างเป็นกลยุทธ์การแก้ไขอย่างง่ายที่เพิ่ม suffix ให้กับชื่อตาราง

```java
            // Resolve the conflict by appending a numeric suffix
            String baseName = "MyRange";
            int suffix = 1;
            String newName;
            do {
                newName = baseName + "_" + suffix;
                suffix++;
            } while (workbook.getNames().get(newName) != null);

            table.setName(newName);
            System.out.println("Table renamed to: " + newName);
        }

        // Save the workbook to verify the result
        workbook.save("NamedRangeDemo.xlsx");
    }
}
```

**จุดสำคัญของการแก้ไข:**

- **detect duplicate name** – บล็อก `catch` ยืนยันว่ามีความขัดแย้ง
- ลูปตรวจสอบคอลเลกชันชื่อของเวิร์กบุ๊กเพื่อให้แน่ใจว่าตัวระบุใหม่เป็นเอกลักษณ์
- สุดท้ายเวิร์กบุ๊กจะถูกบันทึกเพื่อให้คุณเปิดใน Excel และตรวจสอบว่าตารางมีชื่อที่แตกต่างในขณะที่ named range ดั้งเดิมยังคงอยู่

## ตัวอย่างเต็มที่สามารถรันได้

เมื่อรวมทุกส่วนเข้าด้วยกัน โปรแกรมเต็มจะเป็นดังนี้:

```java
import com.aspose.cells.*;

public class NamedRangeDemo {
    public static void main(String[] args) throws Exception {
        // Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Add a named range called "MyRange" covering A1:C5
        workbook.getNames().add("MyRange", "'Sheet1'!$A$1:$C$5");

        // Create an Excel table that occupies the same cells
        ListObject table = sheet.getListObjects().add(0, 0, 4, 2, true);

        try {
            // Try to set the table name to the same identifier
            table.setName("MyRange");
        } catch (Exception e) {
            // Detect duplicate name and resolve it
            System.out.println("Name conflict detected: " + e.getMessage());

            String baseName = "MyRange";
            int suffix = 1;
            String newName;
            do {
                newName = baseName + "_" + suffix;
                suffix++;
            } while (workbook.getNames().get(newName) != null);

            table.setName(newName);
            System.out.println("Table renamed to: " + newName);
        }

        // Save the file for inspection
        workbook.save("NamedRangeDemo.xlsx");
    }
}
```

**ผลลัพธ์ที่คาดว่าจะได้เมื่อรันโปรแกรม:**

```
Name conflict detected: A name with the specified identifier already exists.
Table renamed to: MyRange_1
```

การเปิดไฟล์ `NamedRangeDemo.xlsx` ใน Excel จะเห็น:

- named range **MyRange** ที่อ้างอิงเซลล์ A1:C5
- ตารางชื่อ **MyRange_1** ที่ครอบคลุมเซลล์เดียวกัน
- ไม่มีข้อผิดพลาดชื่อเมื่อคุณเพิ่มสูตรที่อ้างอิง `MyRange`

## ข้อผิดพลาดทั่วไปและแนวทางปฏิบัติที่ดีที่สุด

- **ห้ามใช้ตัวระบุซ้ำ**: ตรวจสอบเสมอว่าชื่อยังไม่มีอยู่ก่อนที่จะกำหนดให้กับตาราง  
- **แนะนำให้ตรวจสอบอย่างชัดเจน**: `workbook.getNames().get("Name")` จะคืนค่า `null` หากชื่อนั้นว่างเปล่า ซึ่งปลอดภัยกว่าการจับข้อยกเว้นทั่วไป  
- **รักษาความสอดคล้องของแนวปฏิบัติการตั้งชื่อ**: ใช้คำนำหน้าเช่น `tbl_` สำหรับตารางและ `rng_` สำหรับ range เพื่อลดโอกาสชนกันของชื่อ  
- **ความเข้ากันได้ของเวอร์ชัน**: โค้ดทำงานกับ Aspose.Cells 23.9 ขึ้นไป; เวอร์ชันก่อนหน้าอาจมีข้อความข้อยกเว้นที่แตกต่างกัน

## สรุป

ตอนนี้คุณรู้วิธี **สร้าง named range**, **เพิ่ม named range**, **สร้างตาราง Excel**, **ตั้งชื่อตาราง**, และ **ตรวจจับชื่อซ้ำ** ด้วย Aspose.Cells for Java การจัดการการชนกันของชื่ออย่างเชิงรุกช่วยให้เวิร์กบุ๊กของคุณสะอาดและสคริปต์อัตโนมัติของคุณมั่นคง

**ขั้นตอนต่อไป**

- สำรวจ API **set table name** เพิ่มเติมเพื่อใช้ตัวเลือกการจัดรูปแบบ  
- ใช้รูปแบบ **detect duplicate name** เมื่อสร้างหลายตารางโดยอัตโนมัติ  
- ผสาน named range กับสูตรหรือการตรวจสอบข้อมูลเพื่อการรายงานแบบไดนามิก

ขอให้เขียนโค้ดอย่างสนุกสนาน!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดที่ทำงานได้เต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้แบบต่าง ๆ ในโครงการของคุณ

- [สร้าง Style Named Range Excel Aspose Cells Java](/cells/hindi/java/tables-structured-references/create-style-named-range-excel-aspose-cells-java/)
- [สร้าง Style Named Range Excel Aspose Cells Java](/cells/german/java/tables-structured-references/create-style-named-range-excel-aspose-cells-java/)
- [สร้าง Style Named Range Excel Aspose Cells Java](/cells/french/java/tables-structured-references/create-style-named-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}