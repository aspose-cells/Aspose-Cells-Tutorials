---
date: '2026-09-27'
description: เรียนรู้วิธีสร้างแผนภูมิวงกลมใน Java ด้วย Aspose.Cells คู่มือแบบขั้นตอนเพื่อปรับแต่งแผนภูมิวงกลมของ
  Excel ตั้งค่าการพึ่งพา Maven และสร้างแผนภูมิระดับมืออาชีพ
keywords:
- create pie chart java
- customize excel pie chart
- maven dependency aspose cells
lastmod: '2026-09-27'
og_description: สร้างแผนภูมิวงกลมใน Java ด้วย Aspose.Cells สำหรับ Java เรียนรู้การปรับแต่งแผนภูมิวงกลมของ
  Excel เพิ่มการพึ่งพา Maven และสร้างแผนภูมิระดับมืออาชีพในไม่กี่นาที
og_image_alt: Java code generating a customized pie chart in Excel with Aspose.Cells
og_title: สร้างแผนภูมิวงกลมใน Java ด้วย Aspose.Cells – คู่มือ Java ฉบับเต็ม
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to create pie chart java using Aspose.Cells. Step‑by‑step
    guide to customize Excel pie chart, set up Maven dependency, and generate professional
    charts.
  headline: How to create pie chart java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes, repeat the chart‑creation steps for each data range; each chart is
      independent.
    question: Can I generate multiple pie charts in the same workbook?
  - answer: It does; set the chart type to `ChartType.PIE_3D` when adding the chart.
    question: Does Aspose.Cells support 3‑D pie charts?
  - answer: Use the `Workbook.setDefaultTheme` method before creating any charts.
    question: How do I apply a custom theme to all charts?
  - answer: Over 30 formats, including XLSX, CSV, PDF, and HTML.
    question: What file formats can I export the workbook to?
  - answer: Yes, a valid license removes evaluation watermarks and unlocks full functionality.
    question: Is a license required for commercial deployment?
  type: FAQPage
tags:
- Aspose.Cells
- Java charting
- Excel automation
- data visualization
title: วิธีสร้างแผนภูมิวงกลมใน Java ด้วย Aspose.Cells
url: /th/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีสร้างแผนภูมิวงกลม java ด้วย Aspose.Cells

## บทนำ
การสร้าง **แผนภูมิวงกลม** ด้วยโปรแกรมมักรู้สึกเหมือนปริศนา โดยเฉพาะเมื่อคุณต้องการควบคุมสี, คำอธิบาย, และหัวเรื่องอย่างละเอียด ในคู่มือนี้คุณจะได้เรียนรู้วิธี **สร้างแผนภูมิวงกลม java** ด้วย Aspose.Cells แล้วปรับแต่งแผนภูมิ Excel ให้ตรงกับแบรนด์หรือสไตล์การรายงานของคุณ เราจะเดินผ่านการตั้งค่าสภาพแวดล้อม, การเติมข้อมูล, การสร้างแผนภูมิ, และการปรับแต่งภาพ—all โดยไม่ต้องออกจาก IDE ของ Java ของคุณ

**สิ่งที่คุณจะได้เรียนรู้**
- เพิ่ม **Maven dependency Aspose.Cells** ไปยังโปรเจกต์ของคุณ
- สร้างเวิร์กบุ๊ก, เติมเซลล์ด้วยข้อมูล, และสร้างแผนภูมิวงกลม
- ใช้สี, หัวเรื่อง, และคำอธิบายที่กำหนดเองกับแผนภูมิ
- ส่งออกเวิร์กบุ๊กเป็นไฟล์ XLSX พร้อมแชร์

ก่อนเริ่ม คุณควรคุ้นเคยกับไวยากรณ์พื้นฐานของ Java และมี Maven หรือ Gradle ติดตั้งแล้ว

## คำตอบอย่างรวดเร็ว
- **ไลบรารีใดที่สร้างแผนภูมิวงกลมใน Java?** Aspose.Cells for Java
- **ต้องมีใบอนุญาตหรือไม่?** เวอร์ชันทดลองฟรีใช้ได้สำหรับการพัฒนา; ต้องมีใบอนุญาตแบบชำระเงินสำหรับการใช้งานจริง
- **พิกัด Maven ที่ต้องการคืออะไร?** `com.aspose:aspose-cells:24.10`
- **สามารถเปลี่ยนสีของส่วนได้หรือไม่?** ได้, ผ่านเมธอด `setAreaColor` ของแต่ละซีรีส์
- **แผนภูมิสามารถส่งออกเป็น XLSX ได้หรือไม่?** แน่นอน—แค่เรียก `workbook.save("output.xlsx")`

## แผนภูมิวงกลมใน Excel คืออะไร?
แผนภูมิวงกลมแสดงข้อมูลชุดเดียวเป็นส่วนของวงกลมตามสัดส่วน ทำให้เปรียบเทียบส่วนของทั้งหมดได้ง่าย แต่ละส่วนมีมุมที่สอดคล้องกับค่าของมันเมื่อเทียบกับผลรวมทั้งหมด ช่วยให้เห็นการกระจายของข้อมูลอย่างรวดเร็วในหมวดหมู่ต่าง ๆ เช่น ส่วนแบ่งตลาด, การจัดสรรงบประมาณ, หรือเปอร์เซ็นต์ประชากร

## ทำไมต้องใช้ Aspose.Cells เพื่อสร้างแผนภูมิวงกลม java?
Aspose.Cells รองรับประเภทแผนภูมิกว่า 50 ชนิดและสามารถจัดการแผ่นงานที่มีแถวถึงหนึ่งล้านแถวโดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ ความได้เปรียบด้านประสิทธิภาพนี้ทำให้คุณสร้างรายงานขนาดใหญ่บนฮาร์ดแวร์ที่จำกัดได้ พร้อมการควบคุมลักษณะแผนภูมิ, การผูกข้อมูล, และรูปแบบการส่งออกอย่างละเอียด ทำให้เป็นตัวเลือกที่เหนือกว่าหลายไลบรารีโอเพ่นซอร์ส

## ข้อกำหนดเบื้องต้น
- **Java Development Kit (JDK)** 8 หรือใหม่กว่า
- **IDE** เช่น IntelliJ IDEA หรือ Eclipse
- **Maven** หรือ **Gradle** สำหรับการจัดการพึ่งพา
- ใบอนุญาต Aspose.Cells แบบทดลองหรือแบบซื้อ

### ไลบรารีและการพึ่งพาที่จำเป็น
เพิ่ม Maven artifact ของ Aspose.Cells ไปยัง `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

หรือใช้ Gradle ที่เทียบเท่า:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### ขั้นตอนการรับใบอนุญาต
Aspose.Cells for Java เป็นผลิตภัณฑ์เชิงพาณิชย์ แต่คุณสามารถเริ่มต้นด้วยเวอร์ชันทดลองได้ เยี่ยมชม [purchase page](https://purchase.aspose.com/buy) เพื่อรับคีย์ใบอนุญาตชั่วคราว

## การตั้งค่า Aspose.Cells สำหรับ Java
ก่อนอื่น ตรวจสอบให้แน่ใจว่าไลบรารีอยู่ใน classpath หลังจากเพิ่มพึ่งพาแล้ว คุณสามารถเริ่มต้น API ได้ตามตัวอย่างด้านล่าง

```java
import com.aspose.cells.Workbook;

// Initialize a new workbook instance
Workbook workbook = new Workbook();
```

## คู่มือการดำเนินการ

### สร้างและกำหนดค่าเวิร์กบุ๊ก
คลาส `Workbook` แทนไฟล์ Excel ทั้งหมดในหน่วยความจำ

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Cells;
import com.aspose.cells.ChartType;
import com.aspose.cells.Chart;
import com.aspose.cells.Series;
import com.aspose.cells.Color;
import com.aspose.cells.LegendPositionType;
import com.aspose.cells.SaveFormat;
```

#### ขั้นตอนที่ 1: สร้างอินสแตนซ์ของเวิร์กบุ๊ก
```java
// Creates an empty workbook instance to work with.
Workbook workbook = new Workbook();
```  
บรรทัดนี้จะสร้างเวิร์กบุ๊กใหม่ที่ว่างเปล่า ซึ่งคุณสามารถเริ่มเติมข้อมูลได้ทันที

### เข้าถึงหรือแก้ไขเซลล์ในแผ่นงาน
`Worksheet` แทนแผ่นงานเดียวภายในเวิร์กบุ๊ก ซึ่งประกอบด้วยเซลล์, แถว, และคอลัมน์ คุณจะเขียนข้อมูลที่ใช้เป็นแหล่งข้อมูลให้แผนภูมิวงกลมในแผ่นงานนี้

#### ขั้นตอนที่ 2: ดึงแผ่นงานแรกและเซลล์ของมัน
```java
// Access the first worksheet in the workbook.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Put sample values used for a pie chart into specific cells.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Put percentage values for a pie chart into specific cells.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```  
เติมเซลล์ด้วยชื่อหมวดหมู่และค่าที่แผนภูมิจะใช้

### สร้างแผนภูมิวงกลม
อ็อบเจกต์ `Chart` แสดงข้อมูลในแผ่นงานและรองรับหลายประเภท เช่น วงกลม, คอลัมน์, และเส้น

#### ขั้นตอนที่ 3: เพิ่มแผนภูมิวงกลมลงในแผ่นงาน
```java
// Create a pie chart in the worksheet.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```  

### กำหนดค่าซีรีส์และข้อมูลของแผนภูมิวงกลม
`Series` กำหนดช่วงข้อมูลและการจัดรูปแบบสำหรับแผนภูมิ เชื่อมต่อเซลล์ในแผ่นงานกับองค์ประกอบภาพ

#### ขั้นตอนที่ 4: ตั้งค่าซีรีส์สำหรับแผนภูมิ
```java
// Configure the series data range for the chart.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Link the pie chart title to a cell containing the title text.
pie.getTitle().setLinkedSource("D2");
```  

### กำหนดลักษณะของคำอธิบายแผนภูมิและหัวเรื่อง
`Legend` ของแผนภูมิแสดงชื่อซีรีส์และสี ช่วยให้ผู้อ่านระบุแต่ละส่วนได้ง่าย

#### ขั้นตอนที่ 5: ปรับแต่งคำอธิบายแผนภูมิและหัวเรื่อง
```java
// Set legend position at bottom of the chart.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Set font properties for the chart title.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```  

### ปรับแต่งสีของซีรีส์แผนภูมิ
เมธอด `setAreaColor` ตั้งค่าสีเติมของส่วนแผนภูมิโดยใช้ค่า RGB

#### ขั้นตอนที่ 6: เปลี่ยนสีส่วนของแผนภูมิวงกลม
```java
import com.aspose.cells.Color;

// Access and customize colors of individual pie chart segments.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```  

### ปรับขนาดคอลัมน์อัตโนมัติและบันทึกเวิร์กบุ๊ก
เมธอด `autoFitColumns` ปรับความกว้างคอลัมน์ให้พอดีกับเนื้อหาเซลล์โดยอัตโนมัติ

#### ขั้นตอนที่ 7: ปรับความกว้างของคอลัมน์และบันทึกไฟล์
```java
// Autofit all columns.
worksheet.autoFitColumns();

// Define output directory placeholder path for saving the workbook.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Save the modified workbook to an Excel file in the specified directory.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```  

## กรณีการใช้งานทั่วไป
- **การวิเคราะห์ประชากร:** แสดงการกระจายประชากรตามภูมิภาค
- **การรายงานส่วนแบ่งตลาด:** มองเห็นส่วนแบ่งของแต่ละคู่แข่งในครั้งเดียว
- **การจัดสรรงบประมาณ:** เน้นว่าทุนถูกแบ่งให้แต่ละแผนกอย่างไร

## ข้อควรพิจารณาด้านประสิทธิภาพ
- ปล่อยออบเจกต์ (`workbook.dispose()`) เมื่อไม่ต้องการแล้วเพื่อคืนหน่วยความจำเนทีฟ
- สำหรับชุดข้อมูลขนาดใหญ่ ใช้ `WorkbookDesigner` เพื่อสตรีมข้อมูลแทนการโหลดทั้งหมดพร้อมกัน
- ใช้ Java Flight Recorder เพื่อตรวจสอบคอขวดในการสร้างแผนภูมิ

## คำถามที่พบบ่อย

**Q: สามารถสร้างแผนภูมิวงกลมหลายอันในเวิร์กบุ๊กเดียวได้หรือไม่?**  
A: ได้, ทำซ้ำขั้นตอนการสร้างแผนภูมิสำหรับแต่ละช่วงข้อมูล; แต่ละแผนภูมิทำงานอิสระกัน

**Q: Aspose.Cells รองรับแผนภูมิวงกลม 3‑D หรือไม่?**  
A: รองรับ; ตั้งค่าชนิดแผนภูมิเป็น `ChartType.PIE_3D` เมื่อต้องการเพิ่มแผนภูมิ

**Q: จะใช้ธีมกำหนดเองกับแผนภูมิทั้งหมดอย่างไร?**  
A: ใช้เมธอด `Workbook.setDefaultTheme` ก่อนสร้างแผนภูมิใด ๆ

**Q: สามารถส่งออกเวิร์กบุ๊กเป็นรูปแบบไฟล์อะไรได้บ้าง?**  
A: มากกว่า 30 รูปแบบ รวมถึง XLSX, CSV, PDF, และ HTML

**Q: จำเป็นต้องมีใบอนุญาตสำหรับการใช้งานเชิงพาณิชย์หรือไม่?**  
A: จำเป็น, ใบอนุญาตที่ถูกต้องจะลบลายน้ำการประเมินและเปิดใช้งานฟังก์ชันเต็มรูปแบบ

## สรุป
คุณมีสูตรครบวงจรสำหรับ **สร้างแผนภูมิวงกลม java** ด้วย Aspose.Cells แล้ว โดยทำตามขั้นตอนข้างต้น คุณสามารถสร้างแผนภูมิวงกลม Excel ที่ดูเป็นมืออาชีพ ปรับสีและหัวเรื่องตามต้องการ และฝังลงในกระบวนการรายงานใด ๆ อย่าลืมสำรวจประเภทแผนภูมิอื่น ๆ — คอลัมน์, เส้น, เรดาร์ — เพื่อขยายเครื่องมือการแสดงผลข้อมูลของคุณ

---

**Last Updated:** 2026-09-27  
**Tested with:** Aspose.Cells 24.10 for Java  
**Author:** Aspose

## บทแนะนำที่เกี่ยวข้อง

- [Customize Excel Chart Data Labels Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Create Dynamic Excel Charts with Aspose.Cells Java&#58; A Comprehensive Guide for Developers](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [Create and Customize Excel Workbooks Using Aspose.Cells Java&#58; A Step-by-Step Guide](/cells/java/workbook-operations/create-customize-excel-workbooks-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}