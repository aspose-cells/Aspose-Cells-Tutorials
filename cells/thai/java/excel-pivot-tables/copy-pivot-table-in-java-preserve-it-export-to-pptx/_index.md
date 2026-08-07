---
category: general
date: 2026-03-01
description: คัดลอก Pivot Table ใน Java พร้อมคง Pivot ไว้, จากนั้นส่งออก Excel ไปเป็น
  PPTX, ปิด AutoFilter ของ Excel, และใช้ Smart Marker สำหรับอาเรย์ JSON – คู่มือเต็มขั้นตอนโดยละเอียด.
draft: false
keywords:
- copy pivot table
- preserve pivot table
- use smart marker
- disable excel autofilter
- export excel to pptx
language: th
og_description: คัดลอก Pivot Table ใน Java, รักษาการกำหนด Pivot, ส่งออกเป็นไฟล์ PPTX,
  ปิด AutoFilter, และใช้ Smart Marker – คู่มือเต็มสำหรับนักพัฒนา
og_title: คัดลอกตาราง Pivot ใน Java – เก็บไว้, ส่งออกเป็น PPTX
tags:
- Aspose.Cells
- Java
- Excel Automation
title: คัดลอก Pivot Table ใน Java – รักษาไว้, ส่งออกเป็น PPTX
url: /th/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# คัดลอก Pivot Table ใน Java – รักษาไว้, ส่งออกเป็น PPTX

เคยต้องการ **copy pivot table** จาก workbook หนึ่งไปยังอีก workbook หนึ่งโดยไม่สูญเสียการกำหนด pivot ด้านล่างหรือไม่? คุณไม่ได้เป็นคนเดียวที่สับสนกับเรื่องนี้ ในหลายโครงการจริง ๆ คุณจะพบว่าต้องย้ายข้อมูลไปมา และสิ่งสุดท้ายที่คุณต้องการคือ pivot ที่เสียหายและทำให้เกิดข้อผิดพลาดขณะรัน  

ในบทเรียนนี้เราจะเดินผ่านโซลูชันที่ครบถ้วนซึ่งไม่เพียงแต่ **copy pivot table** แต่ยังแสดงวิธี **preserve pivot table** เมื่อคัดลอก, **export Excel to PPTX**, **disable Excel AutoFilter**, และ **use smart marker** เพื่อใส่ JSON array ลงในเซลล์เดียว สุดท้ายคุณจะได้โปรแกรม Java เดียวที่ทำงานได้ครบทุกสถานการณ์สี่แบบ

## Prerequisites

- Java 8 หรือใหม่กว่า (โค้ดทำงานกับ Java 11 ด้วยเช่นกัน)  
- ไลบรารี Aspose.Cells for Java (เวอร์ชัน 23.9 หรือใหม่กว่า) – คุณสามารถดาวน์โหลดได้จาก Maven Central  
- ความคุ้นเคยพื้นฐานกับแนวคิดของ Excel เช่น pivot tables, tables, และ text boxes  

If you’re missing the Aspose.Cells JAR, add this to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

ตอนนี้ ไปดูกันต่อ

## Step 1: Copy Pivot Table – Preserving the Pivot Definition

เมื่อคุณคัดลอกช่วงเซลล์ที่บรรจุ pivot table อย่างง่าย ๆ เมตาดาต้า pivot มักจะถูกทิ้งไว้ Aspose.Cells มีวิธีที่สะดวกในการรักษาการกำหนดไว้โดยใช้ `copyRange` พร้อมกับอ็อบเจกต์ `CopyOptions`

```java
import com.aspose.cells.*;

public class PivotCopyDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot (A1:G20 is just an example)
        Range pivotRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Prepare the destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range – the pivot definition travels with it
        destSheet.getCells().copyRange(pivotRange,
                new CellArea(0, 0, 19, 6), // destination area (rows 0‑19, cols 0‑6)
                new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Why this works:** `CopyOptions` บอก Aspose.Cells ให้คัดลอกทุกอย่างรวมถึง pivot cache และการตั้งค่า field ด้วย หากไม่มีตัวเลือกนี้ คุณจะได้ค่าเป็นค่าธรรมดาและเสียความสามารถในการรีเฟรช pivot  

**Edge case:** หาก pivot ต้นทางของคุณกว้างเกิน `A1:G20` ที่กำหนดไว้ล่วงหน้า ให้ปรับช่วงให้เหมาะสมหรือใช้ `sourceSheet.getPivotTables().get(0).getDataRange()` เพื่อดึงแบบไดนามิก

![Copy pivot table example](image.png "Copy pivot table in Java")

*ข้อความแทนภาพ: แผนผังการคัดลอก pivot table ใน Java*

## Step 2: Export a Worksheet with an Editable TextBox to PPTX

บ่อยครั้งที่คุณต้องแปลงแผ่นงาน Excel ให้เป็นสไลด์ PowerPoint — เช่นแดชบอร์ดประจำสัปดาห์ที่ต้องนำเสนอ Aspose.Cells สามารถบันทึกแผ่นงานเป็นไฟล์ PPTX ได้โดยตรงพร้อมคงรูปทรงเช่น TextBox ไว้

```java
import com.aspose.cells.*;

public class ExportToPptxDemo {

    public static void main(String[] args) throws Exception {
        // Load workbook that contains a TextBox shape
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Export the first worksheet to PPTX
        wb.save("YOUR_DIRECTORY/output.pptx", SaveFormat.PPTX);

        System.out.println("Worksheet exported to PPTX successfully.");
    }
}
```

**What’s happening:** เมธอด `save` พร้อม `SaveFormat.PPTX` จะเปลี่ยนแปลงทั้งแผ่นรวมถึง TextBox ที่แก้ไขได้ให้เป็นสไลด์ PowerPoint ข้อความภายในกล่องจะยังคงแก้ไขได้เมื่อคุณเปิดไฟล์ PPTX ใน PowerPoint  

**Tip:** หากคุณมีหลายแผ่นและต้องการเพียงแผ่นเดียว ให้เรียก `wb.getWorksheets().removeAt(index)` เพื่อลบแผ่นอื่นก่อนบันทึก

## Step 3: Disable Excel AutoFilter from a Table

AutoFilter มีประโยชน์สำหรับผู้ใช้ปลายทาง แต่บางครั้งคุณต้องปิดมันโดยโปรแกรม — อาจก่อนส่งออกข้อมูลหรือเมื่อต้องสร้างรายงานที่สะอาด นี่คือวิธี **disable excel autofilter** บนตาราง Excel

```java
import com.aspose.cells.*;

public class DisableAutoFilterDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");
        Worksheet sheet = wb.getWorksheets().get(0);

        // Assume the first table in the sheet is the target
        Table table = sheet.getTables().get(0);

        // Turn off the AutoFilter arrows
        table.setShowAutoFilter(false);

        // Save the modified workbook
        wb.save("YOUR_DIRECTORY/noFilter.xlsx");
        System.out.println("AutoFilter disabled and workbook saved.");
    }
}
```

**Why you might need this:** การส่งออกเป็นฟอร์แมตที่ไม่รองรับ AutoFilter (เช่น CSV หรือ PDF) อาจทำให้ไอคอนฟิลเตอร์หลงเหลืออยู่ การปิดมันช่วยให้ผลลัพธ์สะอาดตา  

**Common pitfall:** หากแผ่นงานไม่มีตาราง `getTables().get(0)` จะทำให้เกิด `IndexOutOfBoundsException` ควรตรวจสอบ `sheet.getTables().size()` ก่อนเสมอในโค้ดจริง

## Step 4: Use Smart Marker – Insert a JSON Array as a Single Cell Value

Smart Marker คือเอนจินเทมเพลตของ Aspose เทคนิคที่สะดวกคือการถือ JSON array ทั้งหมดเป็นค่าเซลล์เดียว ซึ่งเหมาะสำหรับการบันทึกหรือส่งข้อมูลโครงสร้างต่อไป ให้เรา **use smart marker** เพื่อทำเช่นนั้น

```java
import com.aspose.cells.*;

public class SmartMarkerDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Initialise the SmartMarker processor with the workbook
        SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

        // JSON array we want to embed
        String jsonArray = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";

        // Configure the processor to treat arrays as a single cell
        processor.setOptions(SmartMarkerOptions.ArrayAsSingle);

        // Apply the marker – assume cell A1 contains the marker ${json}
        processor.apply(jsonArray);

        // Save the result
        wb.save("YOUR_DIRECTORY/smartMarkerResult.xlsx");
        System.out.println("JSON array inserted via Smart Marker.");
    }
}
```

**How it works:** ตัวมาร์คเกอร์ `${json}` ในเวิร์กบุ๊กจะถูกแทนที่ด้วยสตริง JSON ทั้งหมดเพราะเราตั้งค่า `ArrayAsSingle` หากไม่ตั้งค่านี้ Aspose จะพยายามขยายแต่ละองค์ประกอบของอาเรย์เป็นแถวแยกต่างหาก  

**Variation:** หากต้องการให้แอเรย์แยกเป็นหลายแถว เพียงละเว้น `ArrayAsSingle` แล้วให้ Smart Marker จัดการขยายอัตโนมัติ

## Full Working Example – All Steps Combined

ด้านล่างเป็นคลาส Java เดียวที่รวมทุกขั้นตอนที่อธิบายไว้ รันเป็นเมธอด `main` ปกติ; เพียงปรับเส้นทางไฟล์ให้ตรงกับสภาพแวดล้อมของคุณ

```java
import com.aspose.cells.*;

public class CompleteExcelAutomation {

    public static void main(String[] args) throws Exception {
        // ----------- Step 1: Copy Pivot Table -----------
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet srcSheet = srcWb.getWorksheets

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}