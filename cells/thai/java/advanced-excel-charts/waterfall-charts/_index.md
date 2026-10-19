---
date: 2026-09-02
description: เรียนรู้วิธีสร้างแผนภูมิน้ำตก Excel ใน Java ด้วย Aspose.Cells ตั้งค่าช่วงข้อมูลของแผนภูมิ
  ปรับแต่งป้ายกำกับ และส่งออกเป็น XLSX
keywords:
- create excel waterfall chart
- waterfall chart data labels
- Aspose.Cells Java chart
lastmod: 2026-09-02
linktitle: แผนภูมิน้ำตก
og_description: สร้างแผนภูมิน้ำตก Excel ด้วย Aspose.Cells สำหรับ Java – ตั้งค่าช่วงข้อมูลของแผนภูมิ
  เพิ่มป้ายข้อมูล และส่งออกเป็น XLSX ในไม่กี่ขั้นตอน
og_image_alt: 'Tutorial: create excel waterfall chart with Aspose.Cells Java'
og_title: สร้างแผนภูมิน้ำตก Excel ด้วย Aspose.Cells สำหรับ Java
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  headline: Create excel waterfall chart with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  name: Create excel waterfall chart with Aspose.Cells for Java
  steps:
  - name: import Aspose.Cells
    text: The `com.aspose.cells` package contains all classes required for Excel manipulation,
      including workbook creation, worksheet handling, and chart generation.
  - name: initialize workbook and worksheet
    text: A **Workbook** represents an Excel file, and a **Worksheet** is a single
      sheet within that file. Creating these objects provides the canvas for both
      raw data and the chart.
  - name: enter data
    text: Column A holds category labels, while column B contains the numeric values
      for the waterfall. This layout matches the typical profit‑and‑loss flow used
      in financial analysis.
  - name: create the waterfall chart
    text: The **Chart** object creates a visual representation; setting its type to
      `ChartType.WATERFALL` configures it as a waterfall chart. Use the `add` method
      to set the chart data range for the series (`"B2:B6"`), and link the category
      axis to `"A2:A6"`.
  - name: save the workbook
    text: Saving the workbook writes the chart and data to the specified file format.
      Call `workbook.save("WaterfallChart.xlsx")` to generate an XLSX file, or change
      the format parameter to export to PDF, CSV, or HTML.
  type: HowTo
- questions:
  - answer: Use the `add` method on the chart’s series, passing the cell range that
      contains your values, e.g., `"B2:B6"`.
    question: How do I set the chart data range for a financial waterfall chart?
  - answer: Yes, call `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` to generate
      a PDF version.
    question: Can I export the workbook to PDF instead of XLSX?
  - answer: Extend the data range in both the values column and the category column,
      then update the `add` and `setCategoryData` calls accordingly.
    question: What if I need to create a waterfall chart with more categories?
  - answer: Iterate through the `Series` collection and set the `FillFormat` color
      based on each value’s sign; Aspose.Cells lets you apply conditional formatting
      programmatically.
    question: Is there a way to automatically format positive and negative bars?
  - answer: Yes. After modifying cell values, simply re‑save the workbook—the chart
      will reflect the new data automatically.
    question: Does Aspose.Cells support dynamic data updates for charts?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- waterfall chart
- Aspose.Cells
- java excel charts
- excel automation
title: สร้างแผนภูมิน้ำตก Excel ด้วย Aspose.Cells สำหรับ Java
url: /th/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แผนภูมิน้ำตก

## บทนำสู่แผนภูมิน้ำตกโดยใช้ Aspose.Cells for Java

ในบทแนะนำนี้คุณจะได้เรียนรู้วิธี **สร้างแผนภูมิน้ำตกใน Excel** และ **ตั้งค่าช่วงข้อมูลของแผนภูมิ** ด้วย Aspose.Cells for Java. แผนภูมิน้ำตกเปลี่ยนชุดของตัวเลขบวกและลบให้เป็นเรื่องราวภาพที่ชัดเจน ทำให้เหมาะสำหรับงบการเงิน, การทบทวนประสิทธิภาพการขาย, และสถานการณ์ใด ๆ ที่คุณต้องการเห็นว่ารายการแต่ละรายการมีส่วนช่วยอย่างไรต่อยอดรวม.

## คำตอบอย่างรวดเร็ว
- **แผนภูนีน้ำตกคืออะไร?** ภาพที่แสดงว่าค่าตั้งต้นเพิ่มหรือลดลงอย่างไรโดยชุดของค่ากลาง, สุดท้ายได้ผลรวมสุดท้าย.  
- **ไลบรารีที่ใช้คืออะไร?** Aspose.Cells for Java.  
- **ฉันต้องการไลเซนส์หรือไม่?** การทดลองใช้ฟรีทำงานสำหรับการพัฒนา; จำเป็นต้องมีไลเซนส์เชิงพาณิชย์สำหรับการใช้งานจริง.  
- **ฉันสามารถบันทึกไฟล์เป็น XLSX ได้หรือไม่?** ได้ – ใช้ `workbook.save("FileName.xlsx")`.  
- **เหมาะสำหรับการสร้างภาพข้อมูลด้วย Java หรือไม่?** แน่นอน; Aspose.Cells ให้คุณสมบัติการสร้างแผนภูมิที่ครบครันโดยไม่ต้องติดตั้ง Office.

## แผนภูมิน้ำตกคืออะไร?
แผนภูมิน้ำตกแสดงการมีส่วนร่วมเชิงบวกและเชิงลบแบบต่อเนื่องต่อค่าตั้งต้น, ช่วยให้คุณเข้าใจว่าทุกส่วนมีผลต่อผลลัพธ์โดยรวมอย่างไร. การแสดงกำไรและขาดทุนเคียงข้างกันทำให้การไหลของการเงินที่ซับซ้อนอ่านได้ทันที.

## ทำไมต้องใช้ Aspose.Cells for Java เพื่อเพิ่มแผนภูมิน้ำตก?
Aspose.Cells ให้คุณสร้างแผนภูมิ Excel บนเซิร์ฟเวอร์ใด ๆ, สายงาน CI, หรือเดสก์ท็อปโดยไม่ต้องใช้ Microsoft Excel. รองรับ **15+ รูปแบบผลลัพธ์** (XLSX, PDF, HTML, CSV และอื่น ๆ), ประมวลผลเวิร์กบุ๊กที่มี **500+ แถว** ภายในไม่ถึงหนึ่งวินาที, และให้การควบคุมแบบโปรแกรมต่อองค์ประกอบทุกอย่างของแผนภูมิ—ตั้งแต่สีจนถึงป้ายข้อมูล.

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะลงลึกในโค้ด, โปรดตรวจสอบว่าคุณมีข้อกำหนดต่อไปนี้พร้อมใช้งาน:

- Aspose.Cells for Java: คุณต้องติดตั้ง Aspose.Cells for Java. คุณสามารถดาวน์โหลดได้จากหน้าปล่อย Aspose.Cells for Java: [Aspose.Cells for Java releases](https://releases.aspose.com/cells/java/).
- สภาพแวดล้อมการพัฒนา Java: ตรวจสอบว่าคุณได้ติดตั้ง Java บนระบบของคุณและมีเครื่องมือสร้าง (Maven/Gradle) พร้อมใช้งาน.

ตอนนี้, มาเริ่มสร้างแผนภูมิน้ำตกขั้นตอนต่อขั้นตอนกัน.

## วิธีตั้งค่าช่วงข้อมูลของแผนภูมิน้ำตกใน Java

โหลดเวิร์กบุ๊กใหม่, เติมข้อมูลลงไป, เพิ่มอ็อบเจ็กต์ `Chart`, กำหนดช่วงของซีรีส์, และสุดท้ายบันทึกไฟล์. กระบวนการนี้ตรงไปตรงมา: คุณสร้างเวิร์กบุ๊ก, เติมเซลล์ด้วยหมวดหมู่และค่า, สร้างแผนภูมิ, ผูกช่วงข้อมูล, แล้วส่งออกเวิร์กบุ๊ก. ผลลัพธ์คือแผนภูมิน้ำตกที่ทำงานเต็มรูปแบบพร้อมใช้ในรายงานหรือแดชบอร์ด.

### ขั้นตอนที่ 1: นำเข้า Aspose.Cells
แพ็กเกจ `com.aspose.cells` มีคลาสทั้งหมดที่จำเป็นสำหรับการจัดการ Excel, รวมถึงการสร้างเวิร์กบุ๊ก, การจัดการเวิร์กชีต, และการสร้างแผนภูมิ.

### ขั้นตอนที่ 2: เริ่มต้นเวิร์กบุ๊กและเวิร์กชีต
**Workbook** แทนไฟล์ Excel, และ **Worksheet** คือแผ่นงานเดียวภายในไฟล์นั้น. การสร้างอ็อบเจ็กต์เหล่านี้ให้พื้นที่สำหรับข้อมูลดิบและแผนภูมิ.

### ขั้นตอนที่ 3: ป้อนข้อมูล
คอลัมน์ A เก็บป้ายชื่อหมวดหมู่, ส่วนคอลัมน์ B มีค่าตัวเลขสำหรับแผนภูมิน้ำตก. การจัดวางนี้สอดคล้องกับกระแสกำไร‑ขาดทุนทั่วไปที่ใช้ในการวิเคราะห์การเงิน.

### ขั้นตอนที่ 4: สร้างแผนภูมิน้ำตก
อ็อบเจ็กต์ **Chart** สร้างการแสดงผลภาพ; การตั้งค่าชนิดเป็น `ChartType.WATERFALL` จะกำหนดให้เป็นแผนภูนีน้ำตก. ใช้เมธอด `add` เพื่อตั้งค่าช่วงข้อมูลของแผนภูมิสำหรับซีรีส์ (`"B2:B6"`), และเชื่อมแกนหมวดหมู่กับ `"A2:A6"`.

### ขั้นตอนที่ 5: บันทึกเวิร์กบุ๊ก
การบันทึกเวิร์กบุ๊กจะเขียนแผนภูมิและข้อมูลลงในรูปแบบไฟล์ที่ระบุ. เรียก `workbook.save("WaterfallChart.xlsx")` เพื่อสร้างไฟล์ XLSX, หรือเปลี่ยนพารามิเตอร์รูปแบบเพื่อส่งออกเป็น PDF, CSV, หรือ HTML.

## ปัญหาทั่วไปและวิธีแก้

- **แผนภูมิแสดงเป็นสีขาว** – ตรวจสอบว่าการอ้างอิงช่วงข้อมูล (`B2:B6` และ `A2:A6`) ตรงกับเซลล์จริงที่มีค่าและหมวดหมู่ของคุณ.  
- **ค่าลบไม่แสดงอย่างถูกต้อง** – ตรวจสอบว่าชนิดของซีรีส์ตั้งเป็น `ChartType.WATERFALL`; ชนิดแผนภูมิอื่นจะจัดการค่าลบต่างกัน.  
- **ไฟล์ไม่เปิดใน Excel** – ใช้เวอร์ชันล่าสุดของ Aspose.Cells และยืนยันว่านามสกุลไฟล์ตรงกับรูปแบบ (`.xlsx` สำหรับ Excel).

## คำถามที่พบบ่อย

### ฉันจะปรับแต่งลักษณะของแผนภูมิน้ำตกได้อย่างไร?
คุณสามารถแก้ไขคุณสมบัติเช่น `Chart.getSeries().get(0).getFillFormat().setColor(Color.getRed())` เพื่อเปลี่ยนสีของแถบ, เปิดใช้งานป้ายข้อมูลด้วย `setShowDataLabels(true)`, และปรับหัวข้อแกนผ่าน `getCategoryAxis().setTitle("Stage")`. เอกสารอ้างอิง Aspose.Cells API มีรายการเต็มของตัวเลือกที่สามารถปรับแต่งได้.

### ฉันสามารถสร้างแผนภูมิน้ำตกหลายแผนภูมิในเวิร์กชีตเดียวกันได้หรือไม่?
ได้. หลังจากเพิ่มแผนภูมิเพิ่มแรก, ทำซ้ำขั้นตอนการสร้างแผนภูมิด้วยช่วงข้อมูลที่แตกต่างและอ็อบเจ็กต์ `Chart` ใหม่. แต่ละแผนภูมิมีอิสระและสามารถวางตำแหน่งได้ทุกที่บนแผ่นงาน.

### Aspose.Cells รองรับสภาพแวดล้อมการพัฒนา Java ต่าง ๆ หรือไม่?
แน่นอน. ไลบรารีทำงานกับ Eclipse, IntelliJ IDEA, NetBeans, และระบบสร้างใด ๆ ที่รองรับ Maven หรือ Gradle. ไม่ต้องการปลั๊กอินเพิ่มเติม.

### ฉันสามารถเพิ่มซีรีส์ข้อมูลเพิ่มเติมในแผนภูนีน้ำตกของฉันได้หรือไม่?
คุณสามารถเพิ่มซีรีส์เพิ่มเติมโดยเรียก `chart.getNSeries().add("C2:C6", true)` และกำหนดค่าซีรีส์แต่ละอันแยกกัน. สิ่งนี้ทำให้คุณเปรียบเทียบหลายสถานการณ์เคียงข้างกัน.

### ฉันจะหาแหล่งข้อมูลและตัวอย่างเพิ่มเติมสำหรับ Aspose.Cells for Java ได้จากที่ไหน?
สำรวจเอกสารเต็มที่ Aspose.Cells Java API reference: [Aspose.Cells Java API reference](https://reference.aspose.com/cells/java/).

## คำถามที่พบบ่อย

**Q: ฉันจะตั้งค่าช่วงข้อมูลของแผนภูมิน้ำตกทางการเงินได้อย่างไร?**  
A: ใช้เมธอด `add` บนซีรีส์ของแผนภูมิ, ส่งช่วงเซลล์ที่มีค่าของคุณ, เช่น `"B2:B6"`.

**Q: ฉันสามารถส่งออกเวิร์กบุ๊กเป็น PDF แทน XLSX ได้หรือไม่?**  
A: ได้, เรียก `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` เพื่อสร้างเวอร์ชัน PDF.

**Q: ถ้าฉันต้องการสร้างแผนภูนีน้ำตกที่มีหมวดหมู่มากขึ้นจะทำอย่างไร?**  
A: ขยายช่วงข้อมูลในคอลัมน์ค่าทั้งสองและคอลัมน์หมวดหมู่, จากนั้นอัปเดตการเรียก `add` และ `setCategoryData` ให้สอดคล้อง.

**Q: มีวิธีใดที่จะจัดรูปแบบแถบบวกและลบโดยอัตโนมัติหรือไม่?**  
A: วนลูปผ่านคอลเลกชัน `Series` และตั้งค่าสี `FillFormat` ตามเครื่องหมายของแต่ละค่า; Aspose.Cells ให้คุณใช้การจัดรูปแบบตามเงื่อนไขแบบโปรแกรมได้.

**Q: Aspose.Cells รองรับการอัปเดตข้อมูลแบบไดนามิกสำหรับแผนภูมิหรือไม่?**  
A: ใช่. หลังจากแก้ไขค่าของเซลล์, เพียงบันทึกเวิร์กบุ๊กใหม่—แผนภูมิจะสะท้อนข้อมูลใหม่โดยอัตโนมัติ.

---

**อัปเดตล่าสุด:** 2026-09-02  
**ทดสอบด้วย:** Aspose.Cells for Java (latest)  
**ผู้เขียน:** Aspose  









```java
import com.aspose.cells.*;
```

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

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

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

```java
workbook.save("WaterfallChart.xlsx");
```

## บทแนะนำที่เกี่ยวข้อง

- [ปรับแต่งป้ายข้อมูลแผนภูมิ Excel ด้วย Aspose.Cells for Java: คู่มือขั้นตอนต่อขั้นตอน](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [เพิ่มป้ายข้อมูลในแผนภูมิ Excel ด้วย Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)
- [วิธีสร้างและส่งออกแผนภูมิใน Java ด้วย Aspose.Cells: คู่มือฉบับสมบูรณ์](/cells/java/charts-graphs/aspose-cells-java-create-export-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}