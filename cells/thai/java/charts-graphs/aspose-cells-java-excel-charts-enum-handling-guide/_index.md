---
date: '2026-04-11'
description: เรียนรู้วิธีแสดงเวอร์ชันของ Aspose Cells, โหลดเวิร์กบุ๊ก Excel ใน Java,
  และจัดการ enum ของแผนภูมิด้วย Aspose.Cells. ทำตามตัวอย่างแบบทีละขั้นตอน.
keywords:
- display aspose cells version
- load excel workbook java
- excel chart manipulation
title: แสดงเวอร์ชันของ Aspose Cells และการจัดการ Chart Enum ใน Java
url: /th/java/charts-graphs/aspose-cells-java-excel-charts-enum-handling-guide/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# แสดงเวอร์ชัน Aspose Cells และการจัดการ Chart Enum ใน Java

## บทนำ

หากคุณต้องการ **แสดงเวอร์ชัน Aspose Cells**, โหลดไฟล์ Excel workbook ใน Java, และทำงานกับ chart enums, คุณมาถูกที่แล้ว ในบทเรียนนี้เราจะอธิบายขั้นตอนที่จำเป็นเพื่อผสานรวม Aspose.Cells สำหรับ Java เข้ากับโปรเจกต์ของคุณ, ดึงข้อมูล chart, และแปลง enum ที่เป็นจำนวนเต็มให้เป็นสตริงที่อ่านได้ เมื่อเสร็จคุณจะได้โซลูชันที่มั่นคงพร้อมใช้งานในระดับ production ที่สามารถนำไปใส่ในโค้ดของคุณได้ทันที.

**สิ่งที่คุณจะได้เรียนรู้**
- วิธีแสดงเวอร์ชันของ Aspose.Cells.
- วิธี **โหลด Excel workbook ใน Java** และเข้าถึงข้อมูล chart.
- วิธีแปลงค่าตัวเลขของ enum ให้เป็นสตริงที่เทียบเท่า.
- วิธีดึงประเภทค่า X และ Y จากจุดของ chart.

มาเริ่มกันเลย!

## คำตอบด่วน
- **วิธีตรวจสอบเวอร์ชันของ Aspose.Cells?** เรียก `CellsHelper.getVersion()` แล้วพิมพ์ผลลัพธ์.  
- **Maven coordinate ที่เพิ่ม Aspose.Cells คืออะไร?** `com.aspose:aspose-cells:25.3`.  
- **ฉันสามารถโหลด Excel workbook ใน Java ได้หรือไม่?** ใช่—ใช้ `new Workbook(filePath)`.  
- **ค่า enum ถูกแปลงอย่างไร?** เก็บใน `HashMap<Integer, String>` แล้วค้นหาคีย์จำนวนเต็ม.  
- **เมธอดใดที่พิมพ์ประเภทค่า X/Y?** `pnt.getXValueType()` และ `pnt.getYValueType()`.

## “แสดงเวอร์ชัน Aspose Cells” คืออะไร?
วลีนี้หมายถึงการดึงสตริงเวอร์ชันของไลบรารีในขณะรัน การรู้เวอร์ชันที่แน่นอนช่วยในการดีบัก, ยืนยันความเข้ากันได้, และยืนยันว่าลิขสิทธิ์ของคุณถูกนำไปใช้กับรุ่นที่ต้องการ.

## ทำไมต้องแสดงเวอร์ชันและโหลด Excel workbook ใน Java?
- **Debugging** – ยืนยันว่าไลบรารีที่ถูกต้องอยู่ใน classpath.  
- **Compliance** – ทำให้ตรวจสอบได้ง่ายว่าคุณกำลังใช้เวอร์ชันที่มีลิขสิทธิ์.  
- **Automation** – ทำให้สคริปต์สามารถปรับตัวกับการปล่อยไลบรารีต่างๆ ได้โดยไม่ต้องแก้ไขด้วยตนเอง.

## ข้อกำหนดเบื้องต้น

### ไลบรารีและการพึ่งพาที่จำเป็น
- **Aspose.Cells for Java** – ไลบรารีหลักสำหรับการจัดการ Excel.  
- **Java Development Kit (JDK)** – เวอร์ชัน 8 หรือใหม่กว่า.

### การตั้งค่าสภาพแวดล้อม
- IDE ที่คุณเลือก (IntelliJ IDEA, Eclipse, NetBeans).  
- เครื่องมือสร้าง: Maven **หรือ** Gradle (คำแนะนำด้านล่าง).

### ความรู้ที่ต้องการ
- การเขียนโปรแกรม Java เบื้องต้น.  
- ความคุ้นเคยกับแนวคิดของ Excel (worksheet, chart) เป็นประโยชน์แต่ไม่จำเป็น.

## การตั้งค่า Aspose.Cells สำหรับ Java

### ใช้ Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### ใช้ Gradle
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### ขั้นตอนการรับลิขสิทธิ์
- **Free Trial**: ดาวน์โหลดจาก [Aspose's Release Page](https://releases.aspose.com/cells/java/).  
- **Temporary License**: รับลิขสิทธิ์ระยะสั้นที่ [Aspose's Temporary License Page](https://purchase.aspose.com/temporary-license/).  
- **Purchase**: สำหรับโครงการระยะยาว, ซื้อไลเซนส์ผ่าน [Aspose Purchase Page](https://purchase.aspose.com/buy).

### การเริ่มต้นและตั้งค่าเบื้องต้น
```java
import com.aspose.cells.*;

public class InitializeAsposeCells {
    public static void main(String[] args) {
        // Set the license if available
        License license = new License();
        try {
            license.setLicense("Path_to_License_File");
        } catch (Exception e) {
            System.out.println("Error setting license: " + e.getMessage());
        }

        // Print Aspose.Cells version to confirm setup
        System.out.println("Aspose.Cells for Java Version: " + CellsHelper.getVersion());
    }
}
```

## คู่มือการดำเนินการ

### วิธีแสดงเวอร์ชัน Aspose Cells
**Overview** – ตรวจสอบเวอร์ชันของไลบรารีอย่างรวดเร็วขณะรัน

#### ขั้นตอนที่ 1: นำเข้าแพ็กเกจที่จำเป็น
```java
import com.aspose.cells.*;
```

#### ขั้นตอนที่ 2: สร้างคลาสและเมธอด main
```java
public class DisplayAsposeCellsVersion {
    public static void main(String[] args) throws Exception {
        // This prints the Aspose.Cells version
        System.out.println("Aspose.Cells for Java Version: " + CellsHelper.getVersion());
    }
}
```

#### คำอธิบาย
- `CellsHelper.getVersion()` คืนสตริงเวอร์ชันที่แน่นอนของ Aspose.Cells DLL ที่แอปพลิเคชันของคุณกำลังใช้.

### วิธีแปลง Integer Enums เป็น String Enums
**Overview** – แปลงค่าตัวเลขของ enum (เช่น `CellValueType.IS_NUMERIC`) ให้เป็นข้อความที่อ่านได้

#### ขั้นตอนที่ 1: ตั้งค่า HashMap สำหรับการแปลง
```java
import java.util.HashMap;

HashMap<Integer, String> cvTypes = new HashMap<>();
cvTypes.put(CellValueType.IS_NUMERIC, "IsNumeric");
cvTypes.put(CellValueType.IS_STRING, "IsString");
```

#### ขั้นตอนที่ 2: แปลงและพิมพ์ค่า Enum
```java
public class EnumConversion {
    public static void main(String[] args) {
        int exampleEnumValue = CellValueType.IS_NUMERIC;
        System.out.println("Converted Enum Value: " + cvTypes.get(exampleEnumValue));
    }
}
```

#### คำอธิบาย
- แผนที่ `cvTypes` เชื่อมช่องว่างระหว่างค่าคงที่เชิงตัวเลขและป้ายกำกับที่มนุษย์อ่านได้.

### วิธีโหลด Excel Workbook ใน Java และเข้าถึงข้อมูล Chart
**Overview** – เปิด workbook ที่มีอยู่, ค้นหา chart, และทำให้ข้อมูลของมันเป็นปัจจุบัน

#### ขั้นตอนที่ 1: นำเข้าแพ็กเกจที่จำเป็น
```java
import com.aspose.cells.*;
```

#### ขั้นตอนที่ 2: โหลด Workbook และเข้าถึง Worksheet
```java
public class LoadExcelAndAccessChart {
    static String dataDir = "YOUR_DATA_DIRECTORY";

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook(dataDir + "/sampleFindTypeOfXandYValuesOfPointsInChartSeries.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);
        Chart ch = ws.getCharts().get(0);
        ch.calculate();
    }
}
```

#### คำอธิบาย
- `new Workbook(filePath)` โหลดไฟล์เข้าสู่หน่วยความจำ.  
- `ch.calculate()` บังคับให้ chart คำนวณสูตรใหม่เพื่อให้ข้อมูลที่คุณอ่านเป็นปัจจุบัน.

### วิธีดึงและพิมพ์ประเภทค่า X และ Y ของจุด Chart
**Overview** – ดึงประเภทข้อมูลของค่า X และ Y ของจุดเฉพาะ

#### ขั้นตอนที่ 1: ตั้งค่า HashMap สำหรับการแปลง Enum (ใช้ซ้ำจากก่อนหน้า)
```java
HashMap<Integer, String> cvTypes = new HashMap<>();
cvTypes.put(CellValueType.IS_NUMERIC, "IsNumeric");
cvTypes.put(CellValueType.IS_STRING, "IsString");
```

#### ขั้นตอนที่ 2: เข้าถึง Chart Point และพิมพ์ประเภทค่า
```java
public class RetrieveChartPointTypes {
    static String dataDir = "YOUR_DATA_DIRECTORY";

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook(dataDir + "/sampleFindTypeOfXandYValuesOfPointsInChartSeries.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);
        Chart ch = ws.getCharts().get(0);
        ch.calculate();

        ChartPoint pnt = ch.getNSeries().get(0).getPoints().get(0);

        System.out.println("X Value Type: " + cvTypes.get(pnt.getXValueType()));
        System.out.println("Y Value Type: " + cvTypes.get(pnt.getYValueType()));
    }
}
```

#### คำอธิบาย
- `pnt.getXValueType()` / `pnt.getYValueType()` คืนค่าคงที่จำนวนเต็มที่บ่งบอกว่าค่าเป็นตัวเลข, สตริง, วันที่ ฯลฯ  
- แผนที่ `cvTypes` แปลจำนวนเต็มเหล่านั้นเป็นข้อความที่อ่านได้.

## การประยุกต์ใช้งานจริง
1. **Financial Reporting** – สร้าง chart อัตโนมัติพร้อมประเภทข้อมูลที่ตรวจสอบแล้วสำหรับเส้นทางการตรวจสอบ.  
2. **Data Visualization Dashboards** – ดึงจุด chart ไปยังคอมโพเนนต์ UI ที่กำหนดเอง.  
3. **Automated Testing** – ตรวจสอบว่า series ของ chart มีประเภทข้อมูลที่คาดหวัง.  
4. **Business Intelligence** – ส่งเมตาดาต้า chart ไปยัง pipeline การวิเคราะห์ต่อเนื่อง.  
5. **Custom Reporting Tools** – สร้างเครื่องมือรายงานที่กำหนดเองที่ต้องการการจัดการ enum อย่างแม่นยำ.

## ข้อควรพิจารณาด้านประสิทธิภาพ
- **Load Only Needed Sheets** – ใช้ `Workbook.getWorksheets().get(index)` แทนการโหลดทุก sheet เมื่อจัดการไฟล์ขนาดใหญ่.  
- **Dispose Objects Promptly** – ตั้งค่าอ้างอิง workbook เป็น `null` หลังการประมวลผลเพื่อช่วยการเก็บกวาดหน่วยความจำ.  
- **Batch Process Files** – เมื่อจัดการหลาย workbook, ประมวลผลเป็นชุดเพื่อควบคุมการใช้หน่วยความจำ.

## ปัญหาและวิธีแก้ไขทั่วไป
- **License Not Found** – ตรวจสอบว่าเส้นทางไฟล์ลิขสิทธิ์ถูกต้องและไฟล์รวมอยู่ในผลลัพธ์การสร้าง.  
- **Chart Not Calculated** – เรียก `chart.calculate()` เสมอก่อนอ่านค่าจุด.  
- **Incorrect Enum Mapping** – ตรวจสอบว่าคุณได้เพิ่มคอนสแตนต์ `CellValueType` ที่เกี่ยวข้องทั้งหมดลงใน `HashMap`.

## คำถามที่พบบ่อย

**Q: ฉันสามารถใช้โค้ดนี้กับ Aspose.Cells 24.x ได้หรือไม่?**  
A: ใช่, API สำหรับการดึงเวอร์ชัน, การโหลด workbook, และการเข้าถึง chart point ยังคงเสถียรในรุ่นล่าสุด.

**Q: ถ้า chart ของฉันมีค่าเป็นวันที่จะทำอย่างไร?**  
A: เพิ่ม `CellValueType.IS_DATE_TIME` ลงในแผนที่ `cvTypes` และแมปเป็น `"IsDateTime"`.

**Q: ฉันต้องการลิขสิทธิ์สำหรับการทดลองใช้หรือไม่?**  
A: จำเป็นต้องมีลิขสิทธิ์ทดลองเพื่อใช้งานเต็มรูปแบบ; หากไม่มีคุณจะเห็นลายน้ำบนไฟล์ที่สร้าง.

**Q: ฉันจะจัดการหลาย worksheet อย่างไร?**  
A: วนลูปผ่าน `wb.getWorksheets()` และประมวลผลแต่ละอ็อบเจกต์ `Chart` ที่พบ.

**Q: มีวิธีส่งออกข้อมูล chart ไปเป็น CSV หรือไม่?**  
A: มี—ดึงค่าซีรีส์ผ่าน `chart.getNSeries().get(i).getValues()` แล้วเขียนโดยใช้ Java I/O มาตรฐาน.

---

**Last Updated:** 2026-04-11  
**Tested With:** Aspose.Cells 25.3 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}