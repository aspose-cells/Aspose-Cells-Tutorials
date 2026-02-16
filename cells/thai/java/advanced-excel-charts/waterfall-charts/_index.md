---
date: 2026-02-16
description: เรียนรู้วิธีตั้งช่วงข้อมูลของแผนภูมิและสร้างแผนภูมิน้ำตกใน Java ด้วย
  Aspose.Cells คู่มือขั้นตอนต่อขั้นตอนในการเพิ่มแผนภูมิซีรีส์ข้อมูล ปรับแต่ง และส่งออกเป็น
  XLSX.
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: กำหนดช่วงข้อมูลของแผนภูมิ – แผนภูมิน้ำตก Aspose.Cells สำหรับ Java
url: /th/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

/products-backtop-button >}}

Now ensure we didn't miss any markdown formatting.

We must keep code block placeholders as they are.

Now produce final content with all translations.

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# แผนภูมิน้ำตก

## บทนำสู่แผนภูมิน้ำตกโดยใช้ Aspose.Cells for Java

ในบทเรียนนี้คุณจะได้เรียนรู้วิธี **set chart data range** และสร้าง **waterfall chart** ด้วย Aspose.Cells for Java. แผนภูมิน้ำตกเป็นเครื่องมือสำคัญในการแสดงผลข้อมูล เพราะช่วยให้คุณเห็นผลรวมของค่าบวกและค่าลบหลายค่า ไม่ว่าคุณจะกำลังจัดทำงบการเงิน รายงานผลการขาย หรือการวิเคราะห์ข้อมูลอื่น ๆ แผนภูมิน้ำตกสามารถเปลี่ยนตัวเลขดิบให้เป็นข้อมูลเชิงลึกที่ชัดเจนและนำไปปฏิบัติได้

## คำตอบอย่างรวดเร็ว
- **What is a waterfall chart?** ภาพที่แสดงว่าค่าตั้งต้นเพิ่มหรือลดลงโดยค่ากลางหลายค่า สุดท้ายได้ผลรวมสุดท้าย.  
- **Which library is used?** Aspose.Cells for Java.  
- **Do I need a license?** การทดลองใช้ฟรีใช้ได้สำหรับการพัฒนา; จำเป็นต้องมีลิขสิทธิ์เชิงพาณิชย์สำหรับการใช้งานจริง.  
- **Can I save the file as XLSX?** ใช่ – ใช้ `workbook.save("FileName.xlsx")`.  
- **Is it suitable for Java data visualization?** แน่นอน; Aspose.Cells ให้คุณสมบัติการสร้างแผนภูมิที่หลากหลายโดยไม่ต้องติดตั้ง Office.

## แผนภูนิน้ำตกคืออะไร?
แผนภูมิน้ำตกแสดงการมีส่วนร่วมเชิงบวกและเชิงลบต่อค่าตั้งต้นอย่างต่อเนื่อง ช่วยให้คุณเข้าใจว่าทุกส่วนมีผลต่อผลลัพธ์โดยรวมอย่างไร.

## ทำไมต้องใช้ Aspose.Cells for Java เพื่อเพิ่มแผนภูมิน้ำตก?
- **No Microsoft Excel required** – สร้างแผนภูมิบนเซิร์ฟเวอร์หรือ pipeline CI ใดก็ได้โดยไม่ต้องใช้ Microsoft Excel.  
- **Full control over formatting** – สามารถปรับสี, ป้ายข้อมูล, และแกนต่าง ๆ ได้โดยโปรแกรม.  
- **Supports multiple output formats** – รองรับหลายรูปแบบการส่งออก เช่น XLSX, PDF, HTML และอื่น ๆ.  
- **High performance** – เหมาะสำหรับสมุดงานขนาดใหญ่และการรายงานอัตโนมัติ.

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะลงลึกในโค้ด โปรดตรวจสอบว่าคุณมีข้อกำหนดต่อไปนี้พร้อมใช้งาน:

- Aspose.Cells for Java: คุณต้องติดตั้ง Aspose.Cells for Java คุณสามารถดาวน์โหลดได้จาก [here](https://releases.aspose.com/cells/java/).
- Java Development Environment: ตรวจสอบว่าคุณได้ติดตั้ง Java บนระบบของคุณแล้ว.

ตอนนี้มาเริ่มสร้างแผนภูมิน้ำตกขั้นตอนต่อขั้นตอนกันเถอะ.

## วิธีตั้งช่วงข้อมูลแผนภูมิสำหรับแผนภูมิน้ำตกใน Java

### ขั้นตอนที่ 1: นำเข้า Aspose.Cells

```java
import com.aspose.cells.*;
```

ก่อนอื่นคุณต้องนำเข้าไลบรารี Aspose.Cells ไปยังโครงการ Java ของคุณ ไลบรารีนี้ให้ฟังก์ชันการทำงานที่ครอบคลุมสำหรับการทำงานกับไฟล์ Excel รวมถึงการสร้างแผนภูมิ.

### ขั้นตอนที่ 2: เริ่มต้น Workbook และ Worksheet

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

สร้าง workbook ใหม่และเพิ่ม worksheet เข้าไป เราจะใช้ worksheet นี้เพื่อใส่ข้อมูลของเราและ **add chart to worksheet**.

### ขั้นตอนที่ 3: ป้อนข้อมูล

ตอนนี้ให้เติมข้อมูลลงใน worksheet ที่เราต้องการแสดงในแผนภูมิน้ำตก.

```java
Cells cells = worksheet.getCells();

// Insert data
cells.get("A1").putValue("Categories");
cells.get("A2").putValue("Start");
cells.get("A3").putValue("Positive Value 1");
cells.get("A4").putValue("Negative Value 1");
cells.get("A5").putValue("Positive Value 2");
cells.get("A6").putValue("End");

cells.get("B1").putValue("Values");
cells.get("B2").putValue(0);
cells.get("B3").putValue(20);
cells.get("B4").putValue(-10);
cells.get("B5").putValue(15);
cells.get("B6").putValue(25);
```

ในตัวอย่างนี้ เรามีหมวดหมู่ในคอลัมน์ A และค่าที่สอดคล้องในคอลัมน์ B คุณสามารถแทนที่ข้อมูลนี้ด้วยชุดข้อมูลของคุณเองได้.

### ขั้นตอนที่ 4: สร้างแผนภูมิน้ำตก

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

เราได้เพิ่มแผนภูมิน้ำตกลงใน worksheet ของเราและระบุ series ของข้อมูลและข้อมูลหมวดหมู่ นี่คือขั้นตอนสำคัญที่ **adds waterfall chart** ไปยังแผ่นของคุณ โปรดสังเกตว่าเมธอด `add` ใช้ช่วง `"B2:B6"` – นี่คือที่ที่เรา **set chart data range** สำหรับ series คุณสามารถปรับแต่งลักษณะของแผนภูมิ (สี, ป้ายข้อมูล ฯลฯ) เพิ่มเติมได้โดยใช้คุณสมบัติของอ็อบเจกต์ `Chart`.

### ขั้นตอนที่ 5: บันทึก Workbook

```java
workbook.save("WaterfallChart.xlsx");
```

บันทึก workbook ลงไฟล์ ตัวอย่างใช้รูปแบบ XLSX แต่ Aspose.Cells ยังช่วยให้คุณ **export excel pdf java**‑compatible เช่น PDF, CSV และรูปแบบอื่น ๆ อีกมากมาย ซึ่งสอดคล้องกับความต้องการ **save workbook xlsx**.

## ปัญหาทั่วไปและวิธีแก้

- **Chart appears blank** – ตรวจสอบว่าการอ้างอิงช่วงข้อมูล (`B2:B6` และ `A2:A6`) ตรงกับเซลล์ที่มีค่าหรือหมวดหมู่ของคุณจริงหรือไม่.  
- **Negative values not displayed correctly** – ตรวจสอบให้แน่ใจว่า type ของ series ตั้งเป็น `ChartType.WATERFALL`; ชนิดแผนภูมิอื่นอาจจัดการค่าลบต่างกัน.  
- **File not opening in Excel** – ตรวจสอบว่าคุณใช้ Aspose.Cells รุ่นล่าสุดและนามสกุลไฟล์ตรงกับรูปแบบ (`.xlsx` สำหรับ Excel).

## คำถามที่พบบ่อย

### ฉันจะปรับแต่งลักษณะของแผนภูมิน้ำตกของฉันได้อย่างไร?

คุณสามารถปรับแต่งลักษณะของแผนภูมิน้ำตกโดยการแก้ไขคุณสมบัติต่าง ๆ เช่น สี, ป้ายข้อมูล, และป้ายแกน ดูเอกสาร Aspose.Cells สำหรับคำแนะนำโดยละเอียด.

### ฉันสามารถสร้างแผนภูมิน้ำตกหลายแผนภูมิใน worksheet เดียวได้หรือไม่?

ได้ คุณสามารถสร้างแผนภูมิน้ำตกหลายแผนภูมิใน worksheet เดียวโดยทำตามขั้นตอนเดียวกันแต่ใช้ช่วงข้อมูลที่ต่างกัน.

### Aspose.Cells รองรับสภาพแวดล้อมการพัฒนา Java ต่าง ๆ หรือไม่?

ใช่ Aspose.Cells for Java รองรับสภาพแวดล้อมการพัฒนา Java ต่าง ๆ เช่น Eclipse, IntelliJ IDEA, และ NetBeans.

### ฉันสามารถเพิ่ม series ของข้อมูลเพิ่มเติมในแผนภูมิน้ำตกของฉันได้หรือไม่?

แน่นอน คุณสามารถเพิ่ม series ของข้อมูลเพิ่มเติมในแผนภูมิน้ำตกเพื่อแสดงสถานการณ์ข้อมูลที่ซับซ้อนได้อย่างมีประสิทธิภาพ นี่คือตัวอย่างว่าคุณสามารถ **add data series chart** ได้โดยโปรแกรม.

### ฉันจะหาแหล่งข้อมูลและตัวอย่างเพิ่มเติมสำหรับ Aspose.Cells for Java ได้จากที่ไหน?

คุณสามารถสำรวจเอกสารของ Aspose.Cells for Java ที่ [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/) เพื่อรับข้อมูลเชิงลึกและตัวอย่างโค้ด.

## FAQ

**Q: ฉันจะตั้งช่วงข้อมูลแผนภูมิสำหรับแผนภูมิน้ำตกทางการเงินอย่างไร?**  
A: ใช้เมธอด `add` บน series ของแผนภูมิ โดยส่งช่วงเซลล์ที่มีค่าของคุณ เช่น `"B2:B6"`.

**Q: ฉันสามารถส่งออก workbook เป็น PDF แทน XLSX ได้หรือไม่?**  
A: ใช่ เรียก `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` เพื่อ **export excel pdf java**‑compatible output.

**Q: ถ้าฉันต้องการสร้างแผนภูมิน้ำตกทางการเงินที่มีหมวดหมู่มากขึ้นจะทำอย่างไร?**  
A: ขยายช่วงข้อมูลในคอลัมน์ค่าทั้งสองและคอลัมน์หมวดหมู่ แล้วอัปเดตการเรียก `add` และ `setCategoryData` ให้สอดคล้องกัน.

**Q: มีวิธีใดที่จะแฟอร์แมตแท่งบวกและลบโดยอัตโนมัติหรือไม่?**  
A: คุณสามารถวนลูปผ่านคอลเลกชัน `Series` และตั้งค่าสี `FillFormat` ตามเครื่องหมายของแต่ละค่า.

**Q: Aspose.Cells รองรับการอัปเดตข้อมูลแบบไดนามิกสำหรับแผนภูมิหรือไม่?**  
A: ใช่ คุณสามารถแก้ไขค่าของเซลล์หลังจากสร้างแผนภูมิ; แผนภูมิจะสะท้อนการเปลี่ยนแปลงเมื่อบันทึก workbook.

---

**อัปเดตล่าสุด:** 2026-02-16  
**ทดสอบกับ:** Aspose.Cells for Java (latest)  
**ผู้เขียน:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}