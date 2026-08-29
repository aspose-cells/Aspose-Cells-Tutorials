---
category: general
date: 2026-08-11
description: สร้างเวิร์กบุ๊กใหม่ด้วย Aspose ใน Java, เพิ่มคุณสมบัติกำหนดเองใน Excel,
  แล้วบันทึกเวิร์กบุ๊กเป็น XLSB พร้อมตัวอย่างขั้นตอนเต็ม.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook aspose
- save workbook as xlsb
- add custom property excel
- Aspose.Cells Java
- custom properties Excel
- workbook serialization
language: th
lastmod: 2026-08-11
og_description: สร้างเวิร์กบุ๊กใหม่ด้วย Aspose ใน Java, เพิ่มคุณสมบัติกำหนดเองใน Excel
  และบันทึกเวิร์กบุ๊กเป็นไฟล์ XLSB พร้อมตัวอย่างที่สมบูรณ์และพร้อมใช้งาน
og_image_alt: Java code screenshot that creates a new workbook Aspose, adds a custom
  Excel property, and saves it as an XLSB file
og_title: สร้างเวิร์กบุ๊กใหม่ด้วย Aspose – เพิ่มคุณสมบัติกำหนดเองใน Excel
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  headline: Create new workbook Aspose – add custom property Excel and save as XLSB
  type: TechArticle
- description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  name: Create new workbook Aspose – add custom property Excel and save as XLSB
  steps:
  - name: What if I need to store a string property?
    text: '```java worksheet.getCustomProperties().add("Owner", "Alice"); ```'
  - name: Can I add multiple custom properties at once?
    text: Yes. Call `add` repeatedly for each name/value pair. Aspose.Cells does not
      limit the number of custom properties, but keep the total size reasonable to
      avoid bloating the file.
  - name: How does the binary format affect performance?
    text: XLSB files load faster because they avoid XML parsing. This is especially
      noticeable for workbooks with many rows, formulas, or embedded images.
  - name: What if I need to work with an existing XLSX file?
    text: Replace the `new Workbook()` constructor with `new Workbook("ExistingFile.xlsx")`.
      The rest of the steps (adding properties, saving as XLSB) remain identical.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- XLSB
- Custom Properties
title: สร้างเวิร์กบุ๊กใหม่ด้วย Aspose – เพิ่มคุณสมบัติกำหนดเองใน Excel และบันทึกเป็น
  XLSB
url: /th/java/spreadsheet-automation/create-new-workbook-aspose-add-custom-property-excel-and-sav/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง workbook ใหม่ Aspose – เพิ่ม custom property Excel และบันทึกเป็น XLSB

หากคุณต้องการ **create new workbook Aspose** ในแอปพลิเคชัน Java คำแนะนำนี้จะแสดงวิธีทำอย่างละเอียด คุณจะได้เรียนรู้วิธี **add custom property Excel**, ดึงค่ากลับมา, และ **save workbook as XLSB** โดยไม่สูญเสียเมตาดาต้าใด ๆ

บทแนะนำนี้ครอบคลุมทุกอย่างตั้งแต่การตั้งค่าโปรเจกต์จนถึงการตรวจสอบไฟล์ที่บันทึกไว้ ไม่จำเป็นต้องอ้างอิงเอกสารภายนอก; เพียงทำตามขั้นตอนและรันโค้ด

## ข้อกำหนดเบื้องต้น

- ติดตั้ง Java Development Kit (JDK) 8 หรือสูงกว่า
- Maven หรือ Gradle เพื่อจัดการ dependencies (ตัวอย่างใช้ Maven)
- ใบอนุญาต Aspose.Cells for Java ที่ใช้งานได้ (หรือใช้โหมดประเมินผลฟรีสำหรับการทดสอบ)

## ขั้นตอนที่ 1: เพิ่ม Aspose.Cells ไปยังโปรเจกต์ของคุณ

เพิ่ม Maven artifact ของ Aspose.Cells ไปยังไฟล์ `pom.xml` ของคุณ Dependency นี้จะให้คลาสที่จำเป็นสำหรับการ **create new workbook Aspose** objects.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** หากคุณต้องการใช้ Gradle ให้แทนที่ส่วนของ Maven ด้วยบรรทัดที่เทียบเท่า `implementation "com.aspose:aspose-cells:23.12"`

## ขั้นตอนที่ 2: สร้าง workbook ใหม่ Aspose

ขั้นตอนการทำงานแรกคือการสร้างอ็อบเจกต์ `Workbook` ซึ่งอ็อบเจกต์นี้เป็นตัวแทนของไฟล์ Excel ในหน่วยความจำและเป็นจุดเริ่มต้นสำหรับการดำเนินการต่อไปทั้งหมด.

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {

    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();               // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0); // Default first sheet
```

การสร้าง workbook ใหม่ Aspose จะให้ workbook ที่ว่างเปล่าพร้อมแผ่นงานเริ่มต้น พร้อมสำหรับการปรับแต่ง

## ขั้นตอนที่ 3: เพิ่ม custom property Excel

Custom properties ช่วยให้คุณเก็บเมตาดาต้าแบบกำหนดเองไว้ในไฟล์ Excel ได้ ที่นี่เราจะ **add custom property Excel** ชื่อ `ProjectId` พร้อมค่าตัวเลข

```java
        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);
```

เมธอด `add` รับชื่อ property และค่าที่รองรับได้ทุกประเภท (string, number, date ฯลฯ) เมตาดาต้านี้จะติดตามไฟล์ไปทุกที่ที่คุณคัดลอก

## ขั้นตอนที่ 4: ดึงและแสดง custom property

การอ่านค่ากลับของ property จะยืนยันว่ามันถูกเก็บอย่างถูกต้อง คุณยังสามารถใช้ค่าที่ดึงมาในตรรกะธุรกิจของคุณได้

```java
        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);
```

การแคสท์เป็น `int` ทำงานได้เพราะเราเก็บค่าตัวเลขไว้ หากคุณเก็บเป็นสตริง ให้ใช้ `(String)` แทน

## ขั้นตอนที่ 5: บันทึก workbook เป็น XLSB

ตอนนี้คุณจะ **save workbook as XLSB** ฟอร์แมต XLSB จะเก็บ workbook ในรูปแบบไบนารี ซึ่งเปิดได้เร็วกว่าและใช้พื้นที่บนดิสก์น้อยกว่า Custom properties ทั้งหมดจะถูกเก็บไว้โดยอัตโนมัติ

```java
        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

แทนที่ `"WithCustomProps.xlsb"` ด้วยพาธเต็มหากคุณต้องการไฟล์ในไดเรกทอรีเฉพาะ `SaveFormat.XLSB` enum จะบอก Aspose.Cells ให้เขียนเป็นฟอร์แมตไบนารี

## ขั้นตอนที่ 6: ตรวจสอบผลลัพธ์

รันโปรแกรมจาก IDE หรือ command line ของคุณ:

```bash
mvn compile exec:java -Dexec.mainClass=CustomPropertiesXlsb
```

คุณควรเห็น:

```
ProjectId = 12345
```

เปิด `WithCustomProps.xlsb` ใน Excel แล้วไปที่ **File → Info → Properties → Advanced Properties → Custom** รายการ `ProjectId` พร้อมค่าที่เป็น `12345` จะปรากฏ แสดงให้เห็นว่าขั้นตอน **add custom property excel** สำเร็จและการ **save workbook as xlsb** รักษาเมตาดาต้าไว้

## คำถามทั่วไปและกรณีขอบ

### หากต้องการเก็บ property เป็นสตริง?

```java
worksheet.getCustomProperties().add("Owner", "Alice");
```

ดึงค่าด้วย:

```java
String owner = (String) worksheet.getCustomProperties().get("Owner").getValue();
```

### สามารถเพิ่มหลาย custom properties พร้อมกันได้หรือไม่?

ได้ คุณสามารถเรียก `add` ซ้ำสำหรับแต่ละคู่ชื่อ/ค่า Aspose.Cells ไม่จำกัดจำนวน custom properties แต่ควรควบคุมขนาดรวมให้เหมาะสมเพื่อหลีกเลี่ยงไฟล์บวม

### ฟอร์แมตไบนารีมีผลต่อประสิทธิภาพอย่างไร?

ไฟล์ XLSB โหลดได้เร็วกว่าเพราะหลีกเลี่ยงการพาร์ส XML ซึ่งเห็นได้ชัดใน workbook ที่มีแถวจำนวนมาก สูตร หรือรูปภาพฝัง

### หากต้องทำงานกับไฟล์ XLSX ที่มีอยู่แล้ว?

แทนที่คอนสตรัคเตอร์ `new Workbook()` ด้วย `new Workbook("ExistingFile.xlsx")` ขั้นตอนที่เหลือ (การเพิ่ม properties, การบันทึกเป็น XLSB) จะเหมือนเดิม

## โค้ดเต็ม

ด้านล่างเป็นตัวอย่างที่สมบูรณ์พร้อมรันคัดลอกไปยังไฟล์ชื่อ `CustomPropertiesXlsb.java` ในโฟลเดอร์ `src/main/java` ของคุณ

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {
    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();                       // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // Default first sheet

        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);

        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);

        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

การรันคลาสนี้จะสร้างไฟล์ XLSB ที่มี custom property และสามารถเปิดได้ใน Microsoft Excel รุ่นใหม่ใดก็ได้

## สรุป

ตอนนี้คุณรู้วิธี **create new workbook Aspose**, **add custom property Excel**, และ **save workbook as XLSB** ด้วย Java ตัวอย่างนี้แสดงวงจรชีวิตเต็มรูปแบบ: การเริ่มต้น, การใส่เมตาดาต้า, การตรวจสอบ, และการแปลงเป็นไบนารี

ต่อไปสำรวจหัวข้อที่เกี่ยวข้องเช่น **setting document properties**, **working with Excel formulas**, หรือ **converting between XLSX and XLSB** แต่ละหัวข้อใช้ Aspose.Cells API เดียวกันที่คุณเพิ่งใช้ ทำให้คุณสามารถขยายโซลูชันได้โดยไม่ต้องเรียนรู้ไลบรารีใหม่

คุณสามารถทดลองใช้ประเภทข้อมูลต่าง ๆ, หลายแผ่นงาน, หรือการป้องกันด้วยรหัสผ่าน—Aspose.Cells รองรับทุกสถานการณ์เหล่านี้โดยตรง ขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [สร้างและบันทึก Excel Workbook ด้วย Aspose Cells Java](/cells/english/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [วิธีสร้างและบันทึก Excel Workbook เป็น SVG ด้วย Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [สร้าง Excel Workbook และเพิ่ม Labels ด้วย Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/data-labeling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}