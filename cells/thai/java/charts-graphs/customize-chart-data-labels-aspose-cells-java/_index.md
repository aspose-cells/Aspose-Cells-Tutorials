---
date: '2026-10-17'
description: เรียนรู้วิธีตั้งรูปทรงของป้ายข้อมูลแผนภูมิ Excel ใน Java ด้วย Aspose.Cells
  คู่มือนี้จะแสดงให้คุณทราบวิธีแก้ไขป้ายแผนภูมิ Excel อย่างรวดเร็วและมีประสิทธิภาพ
keywords:
- how to set shape
- modify excel chart labels
- customize chart data labels
- add data label shape
lastmod: '2026-10-17'
og_description: เรียนรู้วิธีตั้งรูปทรงของป้ายข้อมูลแผนภูมิ Excel ใน Java ด้วย Aspose.Cells
  คู่มือขั้นตอนต่อขั้นตอนนี้ช่วยให้คุณแก้ไขป้ายแผนภูมิ Excel อย่างรวดเร็ว
og_image_alt: Guide showing how to set shape of Excel chart data labels using Aspose.Cells
  for Java
og_title: วิธีตั้งรูปทรงของป้ายข้อมูลแผนภูมิ Excel ใน Java
schemas:
- author: Aspose
  dateModified: '2026-10-17'
  description: Learn how to set shape of Excel chart data labels in Java using Aspose.Cells.
    This guide shows you how to modify Excel chart labels quickly and efficiently.
  headline: How to set shape of Excel chart data labels in Java
  type: TechArticle
- description: Learn how to set shape of Excel chart data labels in Java using Aspose.Cells.
    This guide shows you how to modify Excel chart labels quickly and efficiently.
  name: How to set shape of Excel chart data labels in Java
  steps:
  - name: load your workbook
    text: The `Workbook` class is Aspose.Cells' top‑level object that represents a
      single Excel file in memory. Use `new Workbook("input.xlsx")` to load the file
      you want to modify.
  - name: access the chart
    text: '`Worksheet` represents a single sheet within a workbook. `Worksheet ws
      = workbook.getWorksheets().get(0);` retrieves the first worksheet. `Chart` is
      an object that represents a chart embedded in a worksheet. `Chart chart = ws.getCharts().get(0);`
      obtains the first chart on that sheet.'
  - name: retrieve series and modify data labels
    text: '`Series` represents a data series plotted on a chart. Each `Series` object
      contains a `DataLabel` collection. `DataLabel` controls the appearance of a
      data label for a series. `DataLabelShapeType` is an enumeration of possible
      shapes for data labels. Call `series.getDataLabels().setShapeType(DataLab'
  - name: save your workbook
    text: After applying the shape, invoke `workbook.save("output.xlsx");` to write
      the changes back to disk.
  type: HowTo
- questions:
  - answer: Loop through each series in the chart and call `setShapeType` on the series’
      `DataLabel` object.
    question: How do I change the shape of multiple data labels at once?
  - answer: Yes. With proper memory management, it processes workbooks containing
      hundreds of thousands of rows without loading the entire file into memory.
    question: Can Aspose.Cells for Java handle large Excel files efficiently?
  - answer: Missing Maven dependencies, using an outdated library version, or providing
      an invalid license file are typical pitfalls.
    question: What are common issues when setting up Aspose.Cells?
  - answer: Set the shape type to `DataLabelShapeType.DEFAULT` to restore the original
      appearance.
    question: Is there a way to revert data label shapes to default?
  - answer: Iterate over `ws.getCharts()` and apply the same `setShapeType` logic
      to each chart’s series collection.
    question: How can I apply this customization to multiple charts in a workbook?
  type: FAQPage
tags:
- excel chart
- aspose.cells
- java chart customization
- data label shape
title: วิธีตั้งรูปทรงของป้ายข้อมูลแผนภูมิ Excel ใน Java
url: /th/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เชี่ยวชาญการปรับแต่งแผนภูมิใน Java ด้วย Aspose.Cells: ปรับเปลี่ยนรูปแบบป้ายข้อมูล

## บทนำ

การเพิ่มความสวยงามให้กับแผนภูมิ Excel มีความสำคัญเมื่อเตรียมรายงานหรือแดชบอร์ด โดยเฉพาะอย่างยิ่งหากคุณใช้ Java ด้วย Aspose.Cells—ไลบรารีที่ทรงพลังสำหรับการจัดการและการปรับแต่งสเปรดชีต—คุณสามารถ **how to set shape** ของป้ายข้อมูลแผนภูมิได้ด้วยเพียงไม่กี่บรรทัดของโค้ด บทแนะนำนี้จะพาคุณผ่านขั้นตอนการเปลี่ยนรูปแบบของป้ายข้อมูลในแผนภูมิ Excel โดยใช้ Aspose.Cells สำหรับ Java เมื่อจบคุณจะรู้วิธี:

- เข้าถึงและแก้ไขป้ายข้อมูลของแผนภูมิ
- ตั้งค่ารูปแบบที่กำหนดเองสำหรับป้ายข้อมูล
- บันทึกการเปลี่ยนแปลงลงในเวิร์กบุ๊กของคุณ

## คำตอบอย่างรวดเร็ว
- **คลาสหลักที่ใช้ทำงานกับไฟล์ Excel คืออะไร?** `Workbook` แทนไฟล์ Excel ทั้งไฟล์ในหน่วยความจำ.  
- **เมธอดใดที่ตั้งค่ารูปแบบป้าย?** `setShapeType(DataLabelShapeType shape)` บนวัตถุ `DataLabel`.  
- **ต้องการใบอนุญาตสำหรับการพัฒนาหรือไม่?** ใบอนุญาตชั่วคราวฟรีใช้ได้สำหรับการประเมิน; ต้องมีใบอนุญาตเต็มสำหรับการใช้งานจริง.  
- **ฉันสามารถใช้รูปแบบกับหลายซีรีส์ได้หรือไม่?** ใช่—วนลูปผ่านแต่ละซีรีส์และเรียก `setShapeType`.  
- **วิธีนี้เข้ากันได้กับเวิร์กบุ๊กขนาดใหญ่หรือไม่?** Aspose.Cells ประมวลผลเวิร์กบุ๊กหลายร้อยหน้าโดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ.

## อะไรคือ how to set shape?
วลี **how to set shape** หมายถึงการกำหนดโครงร่างภาพของป้ายข้อมูลในแผนภูมิ เช่น การเปลี่ยนสี่เหลี่ยมธรรมดาให้เป็น callout หรือ ellipse การเปลี่ยนรูปแบบช่วยเพิ่มความอ่านง่ายและเน้นจุดข้อมูลสำคัญ โดยการเลือกรูปแบบที่เหมาะสม คุณสามารถทำให้ป้ายเด่นขึ้น, จัดกลุ่มจุดที่เกี่ยวข้อง, หรือให้สอดคล้องกับแนวทางการสร้างแบรนด์ขององค์กร ซึ่งจะทำให้ความอ่านของแผนภูมิโดยรวมดีขึ้น

## ทำไมต้องใช้ Aspose.Cells สำหรับการปรับแต่งป้ายแผนภูมิ?
Aspose.Cells รองรับ **รูปแบบการนำเข้าและส่งออกกว่า 50 แบบ**—รวมถึง XLSX, CSV, ODS, และ PDF—และสามารถจัดการเวิร์กบุ๊กที่มี **สูงสุด 1 ล้านแถว** โดยไม่ทำให้หน่วยความจำหมด API ของมันทำให้คุณสามารถแก้ไขแผนภูมิด้วยโปรแกรมได้ ลดความจำเป็นในการแก้ไข Excel ด้วยมือและรับประกันการจัดรูปแบบที่สม่ำเสมอในรายงานอัตโนมัติ

## ข้อกำหนดเบื้องต้น

- **Aspose.Cells for Java Library**: ต้องใช้เวอร์ชัน 25.3 หรือใหม่กว่า
- **Java Development Environment**: ต้องติดตั้ง JDK บนเครื่องของคุณ
- **IDE Setup**: ใช้ IDE เช่น IntelliJ IDEA หรือ Eclipse เพื่อเขียนและรันโค้ดของคุณ

### ไลบรารีและการพึ่งพาที่จำเป็น

สำหรับผู้ใช้ Maven ให้เพิ่ม dependency ต่อไปนี้ในไฟล์ `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

ผู้ใช้ Gradle ควรเพิ่มสิ่งนี้ในไฟล์ `build.gradle` ของคุณ:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### การรับใบอนุญาต

Aspose.Cells มีใบอนุญาตทดลองฟรี ซึ่งคุณสามารถรับได้จากหน้า [Aspose temporary license page](https://purchase.aspose.com/temporary-license/). สิ่งนี้ให้การเข้าถึงคุณสมบัติทั้งหมดโดยไม่มีข้อจำกัดในช่วงเวลาที่จำกัด

## การตั้งค่า Aspose.Cells สำหรับ Java

เมื่อสภาพแวดล้อมของคุณพร้อมแล้ว ให้ตั้งค่า Aspose.Cells กันเลย นี่คือวิธีเริ่มต้น:

### ขั้นตอนการติดตั้ง

1. **ดาวน์โหลดไลบรารี**: ใช้ Maven หรือ Gradle ตามที่แสดงข้างต้น.
2. **การกำหนดค่าใบอนุญาต**:  
   - `License` เป็นคลาสที่ใช้ไฟล์ใบอนุญาต Aspose.Cells ของคุณเพื่อเปิดใช้งานฟังก์ชันเต็ม.  
   - ดาวน์โหลดและใช้ใบอนุญาตชั่วคราวโดยใช้โค้ดสแนปชอตนี้หลังจากสร้างอ็อบเจกต์ `Workbook`:

    ```java
    License license = new License();
    license.setLicense("path/to/your/license/file");
    ```
3. **การเริ่มต้นพื้นฐาน**: สร้างอินสแตนซ์ของ `Workbook` เพื่อเริ่มทำงานกับไฟล์ Excel

## วิธีตั้งค่ารูปแบบของป้ายข้อมูลในแผนภูมิ?

โหลดเวิร์กบุ๊กของคุณ, ค้นหาแผนภูมิเป้าหมาย, และใช้รูปแบบที่ต้องการกับป้ายข้อมูลของมัน ขั้นตอนต่อไปนี้ทำได้ภายในไม่กี่วินาที.

### ขั้นตอนการทำงานทีละขั้นตอน

#### ขั้นตอนที่ 1: โหลดเวิร์กบุ๊กของคุณ

`Workbook` เป็นอ็อบเจกต์ระดับบนของ Aspose.Cells ที่แทนไฟล์ Excel หนึ่งไฟล์ในหน่วยความจำ ใช้ `new Workbook("input.xlsx")` เพื่อโหลดไฟล์ที่คุณต้องการแก้ไข.

#### ขั้นตอนที่ 2: เข้าถึงแผนภูมิ

`Worksheet` แทนชีตเดียวภายในเวิร์กบุ๊ก  
`Worksheet ws = workbook.getWorksheets().get(0);` ดึงชีตแรกออกมา  
`Chart` เป็นอ็อบเจกต์ที่แทนแผนภูมิที่ฝังอยู่ในชีต  
`Chart chart = ws.getCharts().get(0);` ได้แผนภูมิแรกบนชีตนั้น.

#### ขั้นตอนที่ 3: ดึงซีรีส์และแก้ไขป้ายข้อมูล

`Series` แทนชุดข้อมูลที่แสดงบนแผนภูมิ  
แต่ละอ็อบเจกต์ `Series` มีคอลเลกชันของ `DataLabel`  
`DataLabel` ควบคุมลักษณะของป้ายข้อมูลสำหรับซีรีส์นั้น  
`DataLabelShapeType` เป็น enumeration ของรูปแบบที่เป็นไปได้สำหรับป้ายข้อมูล  
เรียก `series.getDataLabels().setShapeType(DataLabelShapeType.WEDGE_ELLIPSE_CALLOUT);` เพื่อกำหนดรูปแบบ enum มีตัวเลือกหลายสิบแบบ เช่น `RECTANGLE`, `CLOUD`, และ `WEDGE_ELLIPSE_CALLOUT`

#### ขั้นตอนที่ 4: บันทึกเวิร์กบุ๊กของคุณ

หลังจากตั้งค่ารูปแบบแล้ว เรียก `workbook.save("output.xlsx");` เพื่อบันทึกการเปลี่ยนแปลงกลับไปยังดิสก์

## เคล็ดลับการแก้ไขปัญหา

- **ปัญหาเส้นทางไฟล์**: ตรวจสอบว่าเส้นทางไฟล์เป็นแบบ absolute หรือ relative อย่างถูกต้องต่อไดเรกทอรีทำงานของโปรเจค
- **เวอร์ชันไลบรารีไม่ตรงกัน**: ตรวจสอบว่าคุณใช้ Aspose.Cells เวอร์ชัน 25.3 หรือใหม่กว่า; เวอร์ชันเก่าจะไม่มีเมธอด `setShapeType`
- **ประเภทแผนภูมิที่ไม่รองรับ**: บางประเภทแผนภูมิเก่า (เช่น radar) อาจไม่เปิดเผยคุณสมบัติโปรไฟล์ป้ายข้อมูล; เปลี่ยนไปใช้ประเภทแผนภูมิที่รองรับเช่น column หรือ line

## การประยุกต์ใช้ในทางปฏิบัติ

1. **การรายงานทางการเงิน** – เน้นอัตรากำไรสำคัญด้วยป้ายแบบ callout.  
2. **เนื้อหาการศึกษา** – ใช้ป้ายรูปเมฆเพื่อดึงดูดความสนใจไปยังจุดข้อมูลสำคัญในสื่อการสอน.  
3. **การวิเคราะห์การตลาด** – ใช้รูปแบบที่กำหนดเองเพื่อแยกแยะเมตริกประสิทธิภาพแคมเปญในแดชบอร์ด.

## ข้อควรพิจารณาด้านประสิทธิภาพ

เมื่อทำงานกับไฟล์ Excel ขนาดใหญ่:

- **เพิ่มประสิทธิภาพการใช้หน่วยความจำ**: เรียก `workbook.dispose();` หลังบันทึกเพื่อปล่อยทรัพยากร native อย่างรวดเร็ว.  
- **การประมวลผลแบบแบตช์**: ประมวลผลแผนภูมิเป็นกลุ่มแทนการทำทีละอันเพื่อลดค่าใช้จ่ายของการสร้างอ็อบเจกต์.  
- **การจัดการข้อมูลอย่างมีประสิทธิภาพ**: หลีกเลี่ยงการคำนวณหนักภายในลูปที่วนผ่านหลายพันแถว; คำนวณค่าล่วงหน้า.

## สรุป

ตอนนี้คุณรู้แล้วว่า **how to set shape** ของป้ายข้อมูลแผนภูมิ Excel ใน Java ด้วย Aspose.Cells ความสามารถนี้ไม่เพียงเพิ่มความสวยงามของแผนภูมิ แต่ยังช่วยให้ผู้ใช้เข้าใจข้อมูลได้ดีขึ้น สำรวจตัวเลือกการปรับแต่งเพิ่มเติม—เช่น สีของป้าย, ฟอนต์, และเส้นนำ—เพื่อปรับปรุงการแสดงผลของคุณต่อไป

หากมีคำถามหรือขอความช่วยเหลือ โปรดดูที่ [Aspose support forum](https://forum.aspose.com/c/cells/9).

## คำถามที่พบบ่อย

**Q: ฉันจะเปลี่ยนรูปแบบของหลายป้ายข้อมูลพร้อมกันอย่างไร?**  
A: วนลูปผ่านแต่ละซีรีส์ในแผนภูมิและเรียก `setShapeType` บนวัตถุ `DataLabel` ของซีรีส์นั้น.

**Q: Aspose.Cells สำหรับ Java สามารถจัดการไฟล์ Excel ขนาดใหญ่ได้อย่างมีประสิทธิภาพหรือไม่?**  
A: ได้. ด้วยการจัดการหน่วยความจำที่เหมาะสม มันประมวลผลเวิร์กบุ๊กที่มีหลายแสนแถวโดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ.

**Q: ปัญหาที่พบบ่อยเมื่อตั้งค่า Aspose.Cells คืออะไร?**  
A: การขาด dependencies ของ Maven, ใช้เวอร์ชันไลบรารีเก่า, หรือให้ไฟล์ใบอนุญาตที่ไม่ถูกต้องเป็นอุปสรรคทั่วไป.

**Q: มีวิธีคืนรูปแบบป้ายข้อมูลเป็นค่าเริ่มต้นหรือไม่?**  
A: ตั้งค่า shape type เป็น `DataLabelShapeType.DEFAULT` เพื่อคืนลักษณะเดิม.

**Q: ฉันจะใช้การปรับแต่งนี้กับหลายแผนภูมิในเวิร์กบุ๊กได้อย่างไร?**  
A: วนลูปผ่าน `ws.getCharts()` และใช้ตรรกะ `setShapeType` เดียวกันกับคอลเลกชันซีรีส์ของแต่ละแผนภูมิ.

## แหล่งข้อมูล

- [เอกสาร Aspose.Cells](https://reference.aspose.com/cells/java/)
- [ดาวน์โหลด Aspose.Cells สำหรับ Java](https://releases.aspose.com/cells/java/)
- [ซื้อใบอนุญาต](https://purchase.aspose.com/buy)
- [ใบอนุญาตทดลองใช้งานฟรี](https://releases.aspose.com/cells/java/)
- [ใบอนุญาตชั่วคราว](https://purchase.aspose.com/temporary-license/)

---  

**อัปเดตล่าสุด:** 2026-10-17  
**ทดสอบด้วย:** Aspose.Cells 25.3 สำหรับ Java  
**ผู้เขียน:** Aspose  



```java
Workbook wb = new Workbook("YOUR_DATA_DIRECTORY/sampleSetShapeTypeOfDataLabelsOfChart.xlsx");
```
```java
Worksheet ws = wb.getWorksheets().get(0);
Chart ch = ws.getCharts().get(0);
```
```java
Series srs = ch.getNSeries().get(0);
srs.getDataLabels().setShapeType(DataLabelShapeType.WEDGE_ELLIPSE_CALLOUT);
```
```java
wb.save("YOUR_OUTPUT_DIRECTORY/outputSetShapeTypeOfDataLabelsOfChart.xlsx");
```

## บทแนะนำที่เกี่ยวข้อง

- [แก้ไขป้ายข้อมูลแผนภูมิ Excel ด้วย Aspose.Cells Java](/cells/java/charts-graphs/modify-excel-chart-data-labels-aspose-cells-java/)
- [วิธีปรับขนาดป้ายในแผนภูมิ Excel ด้วย Aspose.Cells for Java](/cells/java/charts-graphs/aspose-cells-java-auto-resize-chart-data-labels/)
- [เพิ่มป้ายให้กับแผนภูมิ Excel ด้วย Aspose Cells for Java](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}