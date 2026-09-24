---
date: '2026-04-08'
description: เรียนรู้วิธีสร้างแผนภูมิเส้นพร้อมเครื่องหมายโดยใช้ Aspose.Cells for Java,
  เพิ่มแผนภูมิลงในแผ่นงาน, และปรับแต่งแผนภูมิ Excel สำหรับการรายงานอัตโนมัติ.
keywords:
- line chart with markers
- add chart to worksheet
- automate excel chart creation
- populate data for chart
- export styled chart excel
title: สร้างแผนภูมิเส้นพร้อมเครื่องหมายโดยใช้ Aspose.Cells สำหรับ Java
url: /th/java/charts-graphs/aspose-cells-java-excel-charts-creation/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# การสร้างและจัดรูปแบบแผนภูมิ Excel ด้วย Aspose.Cells Java

## บทนำ

ในโลกที่ขับเคลื่อนด้วยข้อมูลในทุกวันนี้, **line chart with markers** เป็นหนึ่งในวิธีที่มีประสิทธิภาพที่สุดในการแสดงแนวโน้มและค่าผิดปกติ ไม่ว่าคุณจะสร้างรายงานอัตโนมัติหรือแดชบอร์ดที่อัปเดตทุกวัน การสามารถเพิ่ม line chart with markers ไปยังแผ่นงานโดยโปรแกรมได้จะช่วยประหยัดขั้นตอนที่ต้องทำด้วยมือจำนวนมาก บทเรียนนี้จะพาคุณผ่านการใช้ Aspose.Cells สำหรับ Java เพื่อสร้าง, จัดรูปแบบ, และส่งออกแผนภูมิเช่นนี้ เพื่อให้คุณมุ่งเน้นที่การวิเคราะห์ข้อมูลแทนการจัดการ Excel ที่น่าเบื่อ

**สิ่งที่คุณจะได้เรียนรู้**
- การเริ่มต้น Workbook และเติมข้อมูลลงในนั้นโดยใช้ Aspose.Cells.  
- **วิธีเพิ่ม line chart with markers ไปยังแผ่นงาน** และกำหนดลักษณะการแสดงผล.  
- การปรับแต่งสีของ Series, ตัวทำเครื่องหมาย, และตัวเลือกการจัดรูปแบบอื่นๆ.  
- การบันทึก Workbook เป็นไฟล์ Excel ที่รวมแผนภูมิที่จัดรูปแบบของคุณ.  

## คำตอบอย่างรวดเร็ว
- **คลาสหลักที่ใช้เริ่มต้นคืออะไร?** `Workbook` เริ่มต้นไฟล์ Excel ใหม่.  
- **ประเภทแผนภูมิใดที่สร้าง line chart with markers?** `ChartType.LINE_WITH_DATA_MARKERS`.  
- **ฉันจะตั้งค่าสีที่กำหนดเองสำหรับจุดของ Series อย่างไร?** ใช้ `chart.getNSeries().setColorVaried(true)` และตั้งค่าสีของพื้นที่ตัวทำเครื่องหมาย.  
- **ฉันต้องการไลเซนส์เพื่อใช้งานเต็มรูปแบบหรือไม่?** ใช่, ไลเซนส์ Aspose.Cells แบบชำระเงินหรือชั่วคราวจะลบข้อจำกัดการประเมินผล.  
- **ฉันสามารถส่งออกผลลัพธ์เป็น XLSX ได้หรือไม่?** แน่นอน—`workbook.save("StyledChart.xlsx")` จะสร้างไฟล์ XLSX.  

## ข้อกำหนดเบื้องต้น

ก่อนที่จะสร้างและจัดรูปแบบแผนภูมิด้วย Aspose.Cells สำหรับ Java, โปรดตรวจสอบว่าคุณได้ตั้งค่าต่อไปนี้เรียบร้อยแล้ว:

### ไลบรารีที่จำเป็น

รวม Aspose.Cells เป็น dependency ในโปรเจคของคุณ ด้านล่างเป็นคำแนะนำสำหรับผู้ใช้ Maven และ Gradle:

**Maven:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle:**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### ความต้องการในการตั้งค่าสภาพแวดล้อม
- Java Development Kit (JDK) ที่ติดตั้งบนระบบของคุณ.  
- Integrated Development Environment (IDE) เช่น IntelliJ IDEA หรือ Eclipse สำหรับการเขียนโค้ดและทดสอบ.  

### ความรู้เบื้องต้นที่จำเป็น
จำเป็นต้องมีความเข้าใจพื้นฐานของการเขียนโปรแกรม Java พร้อมกับความคุ้นเคยกับ Workbook ของ Excel และแนวคิดการสร้างแผนภูมิ.

### การรับไลเซนส์

Aspose.Cells เป็นผลิตภัณฑ์เชิงพาณิชย์ที่ต้องมีไลเซนส์เพื่อใช้งานเต็มรูปแบบ คุณสามารถรับการทดลองใช้ฟรีเพื่อประเมินคุณสมบัติ, ขอไลเซนส์ชั่วคราวสำหรับการทดสอบต่อเนื่อง, หรือซื้อผลิตภัณฑ์เพื่อการใช้งานระยะยาว.

- **ทดลองใช้ฟรี:** [ดาวน์โหลดการทดลองใช้ฟรี](https://releases.aspose.com/cells/java/)  
- **ไลเซนส์ชั่วคราว:** [ขอไลเซนส์ชั่วคราว](https://purchase.aspose.com/temporary-license/)  
- **ซื้อ:** [ซื้อ Aspose.Cells](https://purchase.aspose.com/buy)  

## การตั้งค่า Aspose.Cells สำหรับ Java

เมื่อคุณได้ติดตั้ง dependency ที่จำเป็นแล้ว, ตั้งค่าสภาพแวดล้อมการพัฒนาเพื่อใช้ Aspose.Cells เริ่มต้นด้วยการนำเข้าไลบรารีและสร้างอ็อบเจ็กต์ `Workbook` ในแอปพลิเคชัน Java ของคุณ:

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook instance
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## คู่มือการดำเนินการ

ในส่วนนี้ เราจะแบ่งการดำเนินการออกเป็นคุณลักษณะต่างๆ: การเริ่มต้น Workbook และการเติมข้อมูล, การสร้างและกำหนดค่าแผนภูมิ, การปรับแต่ง Series, และการบันทึก Workbook.

### คุณลักษณะ 1: การเริ่มต้น Workbook และการเติมข้อมูล

**ภาพรวม:** คุณลักษณะนี้มุ่งเน้นที่การสร้าง workbook ใหม่, เข้าถึง worksheet แรก, และเติมข้อมูลเพื่อสร้างแผนภูมิ.

#### ขั้นตอนที่ 1: เริ่มต้น Workbook

เริ่มต้นด้วยการสร้างอ็อบเจ็กต์ `Workbook`:

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### ขั้นตอนที่ 2: ตั้งค่าชื่อคอลัมน์และเติมข้อมูล

กำหนดหัวคอลัมน์และเติมแถวด้วยข้อมูลตัวอย่าง:

```java
        // Set columns title 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // Create random data for series 1
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // Create random data for series 2
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### คุณลักษณะ 2: การสร้างและกำหนดค่าแผนภูมิ

**ภาพรวม:** คุณลักษณะนี้แสดงวิธีการเพิ่มแผนภูมิไปยัง worksheet ของ workbook, ตั้งสไตล์, และกำหนดคุณสมบัติพื้นฐาน.

#### ขั้นตอนที่ 3: เพิ่มแผนภูมิไปยัง Worksheet

เพิ่ม line chart with data markers:

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add chart to the worksheet
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // Access and configure the chart
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // Set a predefined style
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### คุณลักษณะ 3: การกำหนดค่าและปรับแต่ง Series

**ภาพรวม:** ปรับปรุงความสวยงามของแผนภูมิของคุณโดยการปรับแต่งการตั้งค่า series, เช่น สีที่หลากหลายและสไตล์ของตัวทำเครื่องหมาย.

#### ขั้นตอนที่ 4: ปรับแต่งการตั้งค่า Series

กำหนดข้อมูล series, ใช้การจัดรูปแบบที่กำหนดเอง, และปรับตัวทำเครื่องหมาย:

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add series to the chart
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // Enable varied colors for series points
        chart.getNSeries().setColorVaried(true);

        // Customize first series marker styles and colors
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the first series
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // Customize second series marker styles and colors
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the second series
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### คุณลักษณะ 4: การบันทึก Workbook

**ภาพรวม:** สุดท้าย, บันทึก workbook เพื่อบันทึกการเปลี่ยนแปลงและรับประกันว่าแผนภูมิจะรวมอยู่ในไฟล์ Excel.

#### ขั้นตอนที่ 5: บันทึก Workbook

บันทึก workbook ของคุณพร้อมกับแผนภูมิที่สร้างใหม่:

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet and add data, chart configuration as per previous steps...
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // (Implementation of adding data and configuring the chart would be here)

        // Save the workbook to an Excel file
        workbook.save("StyledChart.xlsx");
    }
}
```

### ปัญหาทั่วไปและการแก้ไขข้อผิดพลาด
- **แผนภูมิแสดงเป็นสีขาว:** ตรวจสอบให้แน่ใจว่าช่วงเซลล์ที่ใช้ใน `setXValues` และ `setValues` อ้างอิงถึงเซลล์ที่มีข้อมูลอย่างถูกต้อง.  
- **สีไม่ถูกนำไปใช้:** ตรวจสอบว่าได้เรียก `chart.getNSeries().setColorVaried(true)` ก่อนการปรับแต่ง series แต่ละรายการ.  
- **ข้อผิดพลาดของไลเซนส์:** ไลเซนส์ทดลองอาจจำกัดจำนวนแผนภูมิ; ติดตั้งไลเซนส์เต็มเพื่อยกเลิกข้อจำกัด.  

## คำถามที่พบบ่อย

**Q: ฉันสามารถสร้างประเภทแผนภูมิอื่น (เช่น แถบ, พาย) ด้วย Aspose.Cells ได้หรือไม่?**  
A: ใช่, Aspose.Cells รองรับประเภทแผนภูมิหลายประเภท; เพียงเปลี่ยน `ChartType.LINE_WITH_DATA_MARKERS` เป็นค่า enum ที่ต้องการ.

**Q: ฉันต้องปิด workbook หรือปล่อยทรัพยากรหรือไม่?**  
A: คลาส `Workbook` จัดการทรัพยากรโดยอัตโนมัติ, แต่คุณสามารถเรียก `workbook.dispose()` ในแอปพลิเคชันที่ทำงานเป็นเวลานานเพื่อคืนหน่วยความจำ.

**Q: สามารถเพิ่มหลายแผนภูมิใน worksheet เดียวกันได้หรือไม่?**  
A: แน่นอน—เรียก `worksheet.getCharts().add(...)` สำหรับแต่ละแผนภูมิที่ต้องการแทรก.

**Q: ฉันจะส่งออกไฟล์เป็นรูปแบบ Excel เก่า (XLS) อย่างไร?**  
A: ใช้ `workbook.save("StyledChart.xls", SaveFormat.EXCEL_97_TO_2003);`.

**Q: แผนภูมิจะคงรูปแบบการจัดรูปแบบเมื่อเปิดใน Microsoft Excel หรือไม่?**  
A: ใช่, Aspose.Cells เขียนวัตถุแผนภูมิ Excel แบบดั้งเดิม, ดังนั้นสไตล์, สี, และตัวทำเครื่องหมายทั้งหมดจะปรากฏตามที่กำหนดไว้.

---

**อัปเดตล่าสุด:** 2026-04-08  
**ทดสอบด้วย:** Aspose.Cells 25.3 for Java  
**ผู้เขียน:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}