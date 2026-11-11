---
category: general
date: 2026-07-16
description: สร้างเวิร์กบุ๊กใหม่และคัดลอกพีโวตเทเบิลโดยใช้ Aspose.Cells สำหรับ Java
  เรียนรู้วิธีทำสำเนาพีโวตเทเบิลและคัดลอกช่วง Excel ในไม่กี่นาที.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook
- copy pivot table
- duplicate pivot table
- how to copy pivot
- copy excel range
language: th
lastmod: 2026-07-16
og_description: สร้างเวิร์กบุ๊กใหม่และคัดลอกพีโวตเทเบิลด้วย Aspose.Cells สำหรับ Java
  คู่มือนี้แสดงวิธีทำสำเนาพีโวตเทเบิลและคัดลอกช่วง Excel อย่างมีประสิทธิภาพ
og_image_alt: Screenshot of Java code that creates a new workbook and copies a pivot
  table using Aspose.Cells
og_title: สร้างเวิร์กบุ๊กใหม่และคัดลอก Pivot Table ใน Java – คู่มือฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Create new workbook and copy pivot table using Aspose.Cells for Java.
    Learn how to duplicate pivot table and copy Excel range in minutes.
  headline: Create New Workbook and Copy Pivot Table in Java – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create new workbook and copy pivot table using Aspose.Cells for Java.
    Learn how to duplicate pivot table and copy Excel range in minutes.
  name: Create New Workbook and Copy Pivot Table in Java – Full Step‑by‑Step Guide
  steps:
  - name: What if the source pivot spans more than one sheet?
    text: Aspose.Cells can only copy ranges within a single worksheet at a time. If
      your pivot stretches across sheets, you’ll need to copy each relevant range
      separately and then re‑link them manually.
  - name: Does this method preserve custom number formats?
    text: Yes. The `copy` method copies cell styles, including number formats, fonts,
      and colors. However, if you have conditional formatting that references external
      ranges, double‑check those references after the copy.
  - name: How to copy a pivot that uses an external data source?
    text: When the pivot pulls data from an external connection (e.g., a SQL query),
      the connection information is **not** transferred by `copy`. You’ll need to
      recreate the data source in the destination workbook or embed the source data
      beforehand.
  - name: Can I copy only the pivot layout without the underlying data?
    text: You can achieve that by first clearing the data cells in the source range,
      then copying only the pivot’s layout. This is a more advanced scenario and usually
      not required for a simple **duplicate pivot table** task.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel Automation
title: สร้างเวิร์กบุ๊กใหม่และคัดลอก Pivot Table ด้วย Java – คู่มือเต็มขั้นตอน
url: /th/java/excel-pivot-tables/create-new-workbook-and-copy-pivot-table-in-java-full-step-b/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง Workbook ใหม่และคัดลอก Pivot Table ใน Java – คู่มือเต็มขั้นตอน

เคยสงสัยไหมว่า **สร้าง workbook ใหม่** อย่างไรโดยยังคงรักษา Pivot Table ที่ซับซ้อนจากไฟล์เดิมไว้? หากคุณเคยมองตาราง Excel แล้วคิดว่า “ต้องการ Pivot นี้ใน workbook อื่น” แล้วกดหัวไปหัวมา คุณไม่ได้อยู่คนเดียว ข่าวดีคือด้วย Aspose.Cells for Java คุณสามารถทำสำเนา Pivot Table ได้ด้วยไม่กี่บรรทัดโค้ด

ในบทเรียนนี้เราจะพาคุณผ่านขั้นตอนที่แน่นอนเพื่อ **คัดลอกข้อมูล Pivot Table** , **ทำสำเนาโครงสร้าง Pivot Table** และ **คัดลอกเนื้อหา Excel range** — ทั้งหมดนี้ขณะสร้าง workbook ใหม่จากศูนย์ เมื่อเสร็จคุณจะได้โปรแกรม Java ที่พร้อมรันตามที่ต้องการ

## สิ่งที่คุณจะได้เรียน

- วิธี **สร้าง workbook ใหม่** ด้วย Aspose.Cells อย่างโปรแกรมเมติก
- วิธีกำหนดช่วง (range) ที่บรรจุ Pivot Table อย่างแม่นยำ
- เทคนิค **คัดลอก Pivot Table** และ **ทำสำเนา Pivot Table** โดยไม่สูญเสียการจัดรูปแบบหรือการเชื่อมต่อข้อมูล
- วิธี **คัดลอก Excel range** อย่างมีประสิทธิภาพและบันทึกผลลัพธ์
- ข้อผิดพลาดที่พบบ่อยและเคล็ดลับสำหรับการจัดการ Pivot Table ขนาดใหญ่

ไม่มีการอ้างอิงภายนอก — ทุกอย่างอยู่ในที่เดียว รันได้ทันทีและอธิบายครบถ้วน

---

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะลงลึก โปรดตรวจสอบว่าคุณมี:

1. **Java Development Kit (JDK) 11+** – เวอร์ชันล่าสุดใดก็ได้
2. **Aspose.Cells for Java** library (เวอร์ชันล่าสุด ณ วันที่ 2026‑07‑16) สามารถดาวน์โหลดจาก Maven Central:

   ```xml
   <dependency>
       <groupId>com.aspose</groupId>
       <artifactId>aspose-cells</artifactId>
       <version>23.12</version>
   </dependency>
   ```

3. ไฟล์ Excel ต้นฉบับ (`SourceWithPivot.xlsx`) ที่มี Pivot Table ที่ต้องการคัดลอก
4. IDE หรือโปรแกรมแก้ไขข้อความง่าย ๆ — IntelliJ IDEA, Eclipse หรือ VS Code ก็ใช้ได้

พร้อมหรือยัง? ดีมาก — ไปเริ่มกันเลย

---

## ขั้นตอนที่ 1: **สร้าง Workbook ใหม่** และโหลดไฟล์ต้นฉบับ

สิ่งแรกที่เราต้องการคืออ็อบเจกต์ workbook ใหม่ที่จะเก็บ Pivot ที่ทำสำเนาในภายหลัง พร้อมกับต้องโหลด workbook ดั้งเดิมเพื่ออ้างอิงช่วง Pivot ของมัน

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that already contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        // Grab the first worksheet where the pivot lives
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

> **ทำไมขั้นตอนนี้สำคัญ:**  
> การโหลด workbook ต้นฉบับทำให้เรามีสิทธิ์เข้าถึงอ็อบเจกต์ `Range` ที่บรรจุ Pivot หากข้ามขั้นตอนนี้ คุณจะไม่มีอะไรให้คัดลอกและการทำ **duplicate pivot table** จะล้มเหลวโดยไม่มีข้อความแจ้ง

---

## ขั้นตอนที่ 2: กำหนด **Copy Excel Range** ที่บรรจุ Pivot

Pivot Table ไม่ได้เป็นเซลล์เดียว มันครอบคลุมบล็อกสี่เหลี่ยม เราต้องบอก Aspose.Cells ว่าเซลล์ใดบ้างที่ต้องคัดลอก

```java
        // Define the cell range that includes the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

> **เคล็ดลับ:**  
> หากคุณไม่แน่ใจว่าช่วงที่แน่นอนคืออะไร ให้เปิดไฟล์ต้นฉบับใน Excel เลือก Pivot แล้วดูที่กล่องชื่อ (name box) จะเห็นเช่น `A1:G20` การใช้ช่วงที่ตรงกับจริงจะทำให้การตั้งค่าฟิลด์, ตัวกรองและการคำนวณทั้งหมดถูกรักษาไว้เมื่อเราทำ **copy pivot table** ต่อไป

---

## ขั้นตอนที่ 3: **สร้าง Workbook ใหม่** ที่จะรับ Pivot ที่คัดลอก

ตอนนี้เราจะสร้าง workbook ใหม่ — ที่นี่จะเป็นที่อยู่ของ **duplicate pivot table** ของเรา

```java
        // Create a completely empty workbook for the destination
        Workbook dstWb = new Workbook(); // this automatically creates one empty worksheet
        Worksheet dstWs = dstWb.getWorksheets().get(0);
```

> **สิ่งที่เกิดขึ้นเบื้องหลัง:**  
> ตัวสร้างเริ่มต้น (default constructor) จะสร้าง workbook ที่มีแผ่นงานเปล่าเดียว นี่คือผืนผ้าใบสะอาดที่เราต้องการสำหรับสถานการณ์ **create new workbook** ไม่มีสไตล์หรือแผ่นงานที่ซ่อนอยู่ให้กังวล

---

## ขั้นตอนที่ 4: **คัดลอก Pivot Table** – คัดลอกช่วง Excel ที่กำหนดไว้จริง ๆ

เมื่อทั้งแหล่งและปลายทางพร้อม เราจะทำการคัดลอก ช่วงนี้ทำให้เราได้คำตอบของ **how to copy pivot** ส่วนสำคัญของปริศนา

```java
        // Copy the defined range (which includes the pivot) to the destination worksheet
        srcRange.copy(dstWs.getCells().createRange("A1"));
```

> **ทำไม `copy` ถึงทำงานกับ Pivot:**  
> Aspose.Cells ถือ Pivot เป็นส่วนหนึ่งของคอลเลกชันเซลล์ เมื่อคุณคัดลอกช่วง มันจะนำ cache ของ Pivot, รายการฟิลด์และการจัดวางมาด้วย ผลลัพธ์คือ **duplicate pivot table** ที่ทำงานเต็มรูปแบบใน workbook ใหม่

---

## ขั้นตอนที่ 5: บันทึกผลลัพธ์และตรวจสอบการทำงานของ **Copy Pivot Table**

สุดท้าย เราจะบันทึก workbook ปลายทางลงดิสก์ เปิดไฟล์ใน Excel เพื่อตรวจสอบว่า Pivot ปรากฏเหมือนต้นฉบับหรือไม่

```java
        // Save the destination workbook with the duplicated pivot table
        dstWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

**ผลลัพธ์ที่คาดหวัง:**  
- `CopyPivotResult.xlsx` เปิดขึ้นมาพร้อมแผ่นงานที่มี Pivot Table เหมือนกับที่อยู่ใน `SourceWithPivot.xlsx`  
- ป้ายกำกับแถว/คอลัมน์, ตัวกรองและฟิลด์คำนวณทั้งหมดยังคงอยู่ครบถ้วน  
- ตอนนี้คุณสามารถแก้ไขข้อมูลต้นฉบับแยกกันได้ และ workbook ใหม่จะมี cache ของ Pivot ของมันเอง

---

## กรณีพิเศษและคำถามที่พบบ่อย

### หาก Pivot ต้นฉบับขยายข้ามหลายแผ่นงานจะทำอย่างไร?
Aspose.Cells สามารถคัดลอกช่วงได้เพียงแผ่นงานเดียวในแต่ละครั้ง หาก Pivot ของคุณกระจายข้ามแผ่นงาน คุณต้องคัดลอกแต่ละช่วงที่เกี่ยวข้องแยกกันแล้วทำการเชื่อมต่อด้วยตนเอง

### วิธีนี้รักษาฟอร์แมตตัวเลขที่กำหนดเองหรือไม่?
ใช่ วิธี `copy` จะคัดลอกสไตล์ของเซลล์รวมถึงฟอร์แมตตัวเลข, ฟอนต์และสี อย่างไรก็ตาม หากคุณมีการจัดรูปแบบตามเงื่อนไขที่อ้างอิงช่วงภายนอก ควรตรวจสอบการอ้างอิงเหล่านั้นหลังการคัดลอก

### จะคัดลอก Pivot ที่ใช้แหล่งข้อมูลภายนอกได้อย่างไร?
เมื่อ Pivot ดึงข้อมูลจากแหล่งภายนอก (เช่น คำสั่ง SQL) ข้อมูลการเชื่อมต่อ **จะไม่** ถูกถ่ายโอนด้วย `copy` คุณต้องสร้างแหล่งข้อมูลใหม่ใน workbook ปลายทางหรือฝังข้อมูลต้นฉบับไว้ล่วงหน้า

### สามารถคัดลอกเฉพาะโครงสร้าง Pivot โดยไม่คัดลอกข้อมูลพื้นฐานได้หรือไม่?
ทำได้โดยการล้างเซลล์ข้อมูลในช่วงต้นฉบับก่อน แล้วคัดลอกเฉพาะโครงสร้างของ Pivot นี่เป็นสถานการณ์ขั้นสูงและมักไม่จำเป็นสำหรับงาน **duplicate pivot table** อย่างง่าย

---

## ตัวอย่างทำงานเต็มรูปแบบ (รวมทุกขั้นตอน)

ด้านล่างเป็นคลาส Java ที่พร้อมรัน เพียงเปลี่ยน `YOUR_DIRECTORY` ให้เป็นพาธโฟลเดอร์ที่ใช้จริงบนเครื่องของคุณ

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook containing the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Define the exact range that holds the pivot table
        // Adjust "A1:G20" to match your pivot's size
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 3: Create a brand‑new workbook that will receive the copy
        Workbook dstWb = new Workbook(); // creates an empty workbook with one sheet
        Worksheet dstWs = dstWb.getWorksheets().get(0);

        // Step 4: Copy the pivot (and any surrounding data) to the new workbook
        srcRange.copy(dstWs.getCells().createRange("A1"));

        // Step 5: Save the destination file – now it contains the duplicated pivot table
        dstWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");

        System.out.println("Pivot table copied successfully! Check CopyPivotResult.xlsx.");
    }
}
```

รันโปรแกรม (`java CopyPivotTableDemo`) แล้วคุณจะเห็นข้อความในคอนโซลยืนยันความสำเร็จ

---

## เคล็ดลับระดับมืออาชีพและแนวปฏิบัติที่ดีที่สุด

- **ตรวจสอบช่วง** ก่อนคัดลอก ใช้ `srcWs.getCells().maxDisplayRange` เพื่อค้นหาพื้นที่ที่ใช้โดยอัตโนมัติ หากไม่ต้องการกำหนด `"A1:G20"` ด้วยตนเอง
- **ปิดการคำนวณ** ชั่วคราวสำหรับ workbook ขนาดใหญ่เพื่อเร่งความเร็วการคัดลอก:

  ```java
  srcWb.getSettings().setCalculateFormulaOnOpen(false);
  ```

- **ปลดปล่อยทรัพยากร** (`srcWb.dispose(); dstWb.dispose();`) ในบริการที่ทำงานต่อเนื่องเพื่อหลีกเลี่ยง memory leak
- **ความเข้ากันได้ของเวอร์ชัน:** โค้ดนี้ทำงานกับ Aspose.Cells 23.12 ขึ้นไป เวอร์ชันเก่าอาจต้องใช้ `srcRange.copyTo` แทน `copy`

---

## ขั้นตอนต่อไป

เมื่อคุณเชี่ยวชาญ **create new workbook** และ **copy pivot table** แล้ว คุณอาจอยากสำรวจ:

- **วิธีคัดลอก Pivot** ข้ามหลายแผ่นงานในงานแบตช์
- การเพิ่ม **copy excel range** สำหรับตารางข้อมูลทั่วไปควบคู่กับ Pivot
- การทำอัตโนมัติ **duplicate pivot table** สำหรับรายงานของแต่ละเดือนโดยใช้ลูป
- การส่งออก Pivot ที่ทำสำเนาเป็น PDF หรือ HTML ด้วย renderer ในตัวของ Aspose.Cells

หัวข้อเหล่านี้ต่อยอดจากพื้นฐานที่เราตั้งไว้และทั้งหมดใช้แนวทางโปรแกรมเมติกที่สะอาดและเป็นระบบ

---

## สรุป

เราผ่านกระบวนการทั้งหมดของ **create new workbook**, กำหนด **copy excel range** ของแหล่งข้อมูล, และ **copy pivot table** เพื่อสร้าง **duplicate pivot table** ใน Java ด้วย Aspose.Cells โซลูชันสั้น กระชับ พร้อมใช้งานในสภาพแวดล้อมการผลิต อย่าลังเลที่จะปรับช่วง, ทดลองไฟล์ต้นฉบับต่าง ๆ หรือฝังตรรกะนี้เข้าไปใน pipeline รายงานขนาดใหญ่ของคุณ

หากคุณเจออุปสรรคหรือมีไอเดียขยายบทเรียนนี้ แสดงความคิดเห็นด้านล่างได้เลย ขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมาพร้อมตัวอย่างโค้ดทำงานเต็มรูปแบบและคำอธิบายขั้นตอน‑โดย‑ขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบต่าง ๆ ในโครงการของคุณ

- [วิธีสร้าง Pivot Table ใน Excel ด้วย Aspose.Cells for Java: คู่มือฉบับสมบูรณ์](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [วิธีอัปเดตแหล่งข้อมูล Pivot Table ใน Excel ด้วย Aspose.Cells for Java: คู่มือฉบับสมบูรณ์](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [การจัดการ Pivot Table ใน Excel ด้วย Aspose.Cells Java: คู่มือฉบับสมบูรณ์](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}