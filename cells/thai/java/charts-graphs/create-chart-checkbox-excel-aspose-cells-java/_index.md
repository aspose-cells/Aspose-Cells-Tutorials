---
"date": "2025-04-07"
"description": "เรียนรู้วิธีปรับปรุงไฟล์ Excel ของคุณโดยการสร้างแผนภูมิแบบโต้ตอบพร้อมช่องกาเครื่องหมายโดยใช้ Aspose.Cells สำหรับ Java ปฏิบัติตามคำแนะนำทีละขั้นตอนนี้เพื่อปรับปรุงการแสดงภาพข้อมูล"
"title": "สร้างแผนภูมิโต้ตอบใน Excel พร้อมกล่องกาเครื่องหมายโดยใช้ Aspose.Cells สำหรับ Java"
"url": "/th/java/charts-graphs/create-chart-checkbox-excel-aspose-cells-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# สร้างแผนภูมิโต้ตอบใน Excel พร้อมกล่องกาเครื่องหมายโดยใช้ Aspose.Cells สำหรับ Java

## การแนะนำ

การปรับปรุงการแสดงภาพข้อมูลและการโต้ตอบใน Excel สามารถทำได้โดยการรวมองค์ประกอบแบบไดนามิก เช่น ช่องกาเครื่องหมาย ลงในแผนภูมิ บทช่วยสอนนี้จะแนะนำคุณตลอดกระบวนการสร้างแผนภูมิแบบโต้ตอบโดยใช้ Aspose.Cells สำหรับ Java ซึ่งเหมาะอย่างยิ่งสำหรับการเพิ่มฟังก์ชันการทำงานให้กับไฟล์ Excel ของคุณ

**สิ่งที่คุณจะได้เรียนรู้:**
- วิธีตั้งค่าและใช้ Aspose.Cells สำหรับ Java
- ขั้นตอนการสร้างเวิร์กบุ๊ก Excel และการแทรกแผนภูมิ
- วิธีการเพิ่มช่องกาเครื่องหมายภายในพื้นที่แผนภูมิของคุณ
- เทคนิคการบันทึกการเปลี่ยนแปลงของคุณลงในไฟล์ Excel

ก่อนที่เราจะเริ่ม ให้แน่ใจว่าคุณมีเครื่องมือและความรู้ที่จำเป็น

## ข้อกำหนดเบื้องต้น

หากต้องการทำตามบทช่วยสอนนี้ โปรดแน่ใจว่าคุณมี:
- **ชุดพัฒนา Java (JDK):** ติดตั้งเวอร์ชัน 8 ขึ้นไปบนเครื่องของคุณ
- **Aspose.Cells สำหรับ Java:** ไลบรารี Aspose.Cells เวอร์ชันล่าสุด สำหรับคู่มือนี้ เราจะใช้เวอร์ชัน 25.3
- **Maven หรือ Gradle:** ตั้งค่าในสภาพแวดล้อมการพัฒนาของคุณเพื่อจัดการการอ้างอิง

### ข้อกำหนดเบื้องต้นของความรู้

แม้ว่าความเข้าใจพื้นฐานเกี่ยวกับการเขียนโปรแกรม Java และความคุ้นเคยกับโครงสร้างไฟล์ Excel จะเป็นประโยชน์ แต่คู่มือนี้จะครอบคลุมรายละเอียดทั้งหมดที่จำเป็นสำหรับผู้เริ่มต้น

## การตั้งค่า Aspose.Cells สำหรับ Java

การรวม Aspose.Cells เข้ากับโปรเจ็กต์ของคุณนั้นทำได้ง่าย เริ่มต้นด้วยการตั้งค่าไลบรารีโดยใช้ Maven หรือ Gradle

### การใช้ Maven

เพิ่มการอ้างอิงต่อไปนี้ให้กับของคุณ `pom.xml` ไฟล์:

```xml
<dependency>
  <groupId>com.aspose</groupId>
  <artifactId>aspose-cells</artifactId>
  <version>25.3</version>
</dependency>
```

### การใช้ Gradle

รวมบรรทัดนี้ไว้ในของคุณ `build.gradle` ไฟล์:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### ขั้นตอนการรับใบอนุญาต

หากต้องการสำรวจความสามารถทั้งหมดของ Aspose.Cells โปรดพิจารณาซื้อใบอนุญาตชั่วคราวหรือถาวร คุณสามารถเริ่มทดลองใช้งานฟรีได้โดยดาวน์โหลดจาก [เว็บไซต์ของ Aspose](https://releases.aspose.com/cells/java/)สำหรับการใช้งานในการผลิต คุณอาจต้องการซื้อใบอนุญาตหรือขอใบอนุญาตชั่วคราวเพื่อวัตถุประสงค์ในการประเมิน

#### การเริ่มต้นขั้นพื้นฐาน

เมื่อเพิ่ม Aspose.Cells ลงในโปรเจ็กต์ของคุณแล้ว ให้เริ่มต้นการทำงานในแอปพลิเคชัน Java ดังต่อไปนี้:

```java
import com.aspose.cells.Workbook;

public class AsposeSetup {
    public static void main(String[] args) throws Exception {
        // เริ่มต้นวัตถุเวิร์กบุ๊ก
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## คู่มือการใช้งาน

เมื่อคุณตั้งค่าสภาพแวดล้อมของคุณเรียบร้อยแล้ว มาสร้างแผนภูมิพร้อมช่องกาเครื่องหมายใน Excel กัน

### สร้างตัวอย่างสมุดงานและเพิ่มแผนภูมิ

#### ภาพรวม

หัวข้อนี้จะอธิบายวิธีการสร้างเวิร์กบุ๊ก Excel และเพิ่มแผนภูมิประเภทคอลัมน์โดยใช้ Aspose.Cells สำหรับ Java แผนภูมิช่วยให้แสดงข้อมูลได้อย่างมีประสิทธิภาพ จึงมีความสำคัญอย่างยิ่งสำหรับรายงานและแดชบอร์ด

##### ขั้นตอนที่ 1: สร้างสมุดงานใหม่

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.SheetType;

public class ChartCreation {
    public static void main(String[] args) throws Exception {
        // สร้างอินสแตนซ์ของวัตถุเวิร์กบุ๊กใหม่ที่แสดงไฟล์ Excel
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook created.");
    }
}
```

##### ขั้นตอนที่ 2: เพิ่มแผ่นงานแผนภูมิ

```java
import com.aspose.cells.Worksheet;
import com.aspose.cells.ChartType;

public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        
        // การเพิ่มแผ่นงานแผนภูมิลงในสมุดงาน
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        System.out.println("Chart worksheet added.");
    }
}
```

##### ขั้นตอนที่ 3: แทรกแผนภูมิคอลัมน์

```java
public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // เพิ่มแผนภูมิลอยตัวประเภท COLUMN ลงในเวิร์กชีตแผนภูมิที่เพิ่มใหม่
        sheet.getCharts().addFloatingChart(ChartType.COLUMN, 0, 0, 1024, 960);

        System.out.println("Column chart inserted.");
    }
}
```

##### ขั้นตอนที่ 4: เพิ่มข้อมูลซีรีส์

```java
public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // เพิ่มแผนภูมิลอยตัวประเภท COLUMN
        sheet.getCharts().addFloatingChart(ChartType.COLUMN, 0, 0, 1024, 960);

        // การเพิ่มข้อมูลชุดให้กับแผนภูมิ
        sheet.getCharts().get(0).getNSeries().add("{1,2,3}", false);
        
        System.out.println("Series data added to the chart.");
    }
}
```

### เพิ่มช่องกาเครื่องหมายลงในแผนภูมิ

#### ภาพรวม

การฝังกล่องกาเครื่องหมายไว้ในพื้นที่แผนภูมิ Excel ของคุณจะช่วยให้สามารถสลับการมองเห็นหรือฟีเจอร์อื่นๆ ได้อย่างคล่องตัว หัวข้อนี้จะแนะนำคุณเกี่ยวกับการฝังกล่องกาเครื่องหมายไว้ในแผนภูมิ

##### ขั้นตอนที่ 1: ฝังรูปร่างกล่องกาเครื่องหมาย

```java
import com.aspose.cells.MsoDrawingType;
import com.aspose.cells.PlacementType;

public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // เพิ่มรูปร่างกล่องกาเครื่องหมายภายในพื้นที่แผนภูมิบนแผนภูมิแรกของเวิร์กชีต
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);
        
        System.out.println("Checkbox added to the chart.");
    }
}
```

##### ขั้นตอนที่ 2: ตั้งค่าข้อความกล่องกาเครื่องหมาย

```java
public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // เพิ่มรูปร่างช่องกาเครื่องหมายภายในแผนภูมิ
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);

        // การตั้งค่าข้อความให้กับรูปร่างกล่องกาเครื่องหมายที่เพิ่มใหม่
        sheet.getCharts().get(0).getShapes().get(0).setText("CheckBox 1");

        System.out.println("Checkbox labeled successfully.");
    }
}
```

### บันทึกสมุดงานเป็นไฟล์ Excel

#### ภาพรวม

เมื่อคุณกำหนดค่าแผนภูมิและกล่องกาเครื่องหมายแล้ว ให้บันทึกเวิร์กบุ๊กเพื่อคงการเปลี่ยนแปลงของคุณไว้

```java
public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // เพิ่มรูปร่างช่องกาเครื่องหมายและติดป้ายกำกับ
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);
        sheet.getCharts().get(0).getShapes().get(0).setText("CheckBox 1");

        // บันทึกสมุดงาน
        String outDir = "YOUR_OUTPUT_DIRECTORY"; // แทนที่ด้วยเส้นทางไดเร็กทอรีเอาท์พุตจริงของคุณ
        workbook.save(outDir + "/InsertCheckboxInChartSheet_out.xlsx");
        
        System.out.println("Workbook saved successfully.");
    }
}
```

## การประยุกต์ใช้งานจริง

ต่อไปนี้เป็นสถานการณ์จริงบางสถานการณ์ที่คุณสามารถนำความรู้จากบทช่วยสอนนี้ไปใช้:
1. **รายงานแบบโต้ตอบ:** ใช้กล่องกาเครื่องหมายเพื่อสลับการมองเห็นชุดข้อมูลในรายงาน เพื่อปรับปรุงการโต้ตอบและการปรับแต่งของผู้ใช้
2. **การวิเคราะห์ข้อมูล:** เปิดใช้งานหรือปิดใช้งานชุดข้อมูลบางชุดในแผนภูมิสำหรับการวิเคราะห์เชิงเปรียบเทียบ ช่วยให้เน้นเฉพาะด้านของข้อมูลได้ง่ายยิ่งขึ้น
3. **เครื่องมือทางการศึกษา:** สร้างสื่อการเรียนรู้แบบไดนามิกที่นักเรียนสามารถโต้ตอบกับเนื้อหาได้โดยการเลือกตัวเลือกต่างๆ ในแผนภูมิ

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}