---
"date": "2025-04-07"
"description": "เรียนรู้วิธีการสร้างและปรับแต่งแผนภูมิใน Excel โดยใช้ Aspose.Cells สำหรับ Java สร้างแผนภูมิโดยอัตโนมัติ ปรับปรุงการแสดงข้อมูล และประหยัดเวลาด้วยคู่มือโดยละเอียดนี้"
"title": "การสร้างและกำหนดรูปแบบแผนภูมิ Excel ด้วย Aspose.Cells Java&#58; คู่มือฉบับสมบูรณ์"
"url": "/th/java/charts-graphs/aspose-cells-java-excel-charts-creation/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# การสร้างและกำหนดรูปแบบแผนภูมิ Excel ด้วย Aspose.Cells Java

## การแนะนำ

ในโลกปัจจุบันที่ข้อมูลเป็นปัจจัยสำคัญในการวิเคราะห์และการตัดสินใจ การสร้างภาพข้อมูลที่มีประสิทธิภาพถือเป็นสิ่งสำคัญอย่างยิ่ง มักมีความจำเป็นต้องสร้างแผนภูมิแบบไดนามิกในเวิร์กบุ๊ก Excel ด้วยโปรแกรม โดยเฉพาะเมื่อต้องจัดการกับชุดข้อมูลขนาดใหญ่หรือระบบรายงานอัตโนมัติ บทช่วยสอนนี้สาธิตวิธีใช้ Aspose.Cells สำหรับ Java เพื่อสร้างและปรับแต่งแผนภูมิใน Excel ได้อย่างราบรื่น ด้วยการผสานรวม Aspose.Cells เข้ากับแอปพลิเคชัน Java ของคุณ คุณจะสามารถสร้างแผนภูมิอัตโนมัติ ปรับปรุงการนำเสนอข้อมูล และประหยัดเวลาได้

**สิ่งที่คุณจะได้เรียนรู้:**
- การเริ่มต้นเวิร์กบุ๊กและการเติมข้อมูลโดยใช้ Aspose.Cells
- การสร้างและกำหนดค่าแผนภูมิเส้นด้วยเครื่องหมายข้อมูล
- ปรับแต่งลักษณะและสีของซีรีส์เพื่อการมองเห็นที่ดีขึ้น
- บันทึกสมุดงานด้วยแผนภูมิที่สร้างขึ้นใหม่ในรูปแบบ Excel

มาเริ่มต้นด้วยการหารือถึงข้อกำหนดเบื้องต้นที่จำเป็นในการเริ่มต้นกัน

## ข้อกำหนดเบื้องต้น

ก่อนที่จะสร้างและกำหนดรูปแบบแผนภูมิโดยใช้ Aspose.Cells สำหรับ Java ตรวจสอบให้แน่ใจว่าคุณมีการตั้งค่าต่อไปนี้:

### ห้องสมุดที่จำเป็น
รวม Aspose.Cells เป็นส่วนที่ต้องพึ่งพาในโปรเจ็กต์ของคุณ ต่อไปนี้เป็นคำแนะนำสำหรับผู้ใช้ Maven และ Gradle:

**เมเวน:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**เกรเดิ้ล:**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### ข้อกำหนดการตั้งค่าสภาพแวดล้อม
- Java Development Kit (JDK) ติดตั้งอยู่บนระบบของคุณ
- สภาพแวดล้อมการพัฒนาแบบบูรณาการ (IDE) เช่น IntelliJ IDEA หรือ Eclipse สำหรับการเขียนโค้ดและการทดสอบ

### ข้อกำหนดเบื้องต้นของความรู้
จำเป็นต้องมีความเข้าใจพื้นฐานเกี่ยวกับการเขียนโปรแกรม Java รวมถึงมีความคุ้นเคยกับเวิร์กบุ๊ก Excel และแนวคิดการสร้างแผนภูมิ 

### การขอใบอนุญาต
Aspose.Cells เป็นผลิตภัณฑ์เชิงพาณิชย์ที่ต้องมีใบอนุญาตจึงจะใช้งานได้เต็มรูปแบบ คุณสามารถรับรุ่นทดลองใช้งานฟรีเพื่อประเมินคุณสมบัติ ขอใบอนุญาตชั่วคราวเพื่อการทดสอบขยายเวลา หรือซื้อผลิตภัณฑ์เพื่อใช้งานในระยะยาว

- **ทดลองใช้งานฟรี:** [ดาวน์โหลดทดลองใช้งานฟรี](https://releases.aspose.com/cells/java/)
- **ใบอนุญาตชั่วคราว:** [ขอใบอนุญาตชั่วคราว](https://purchase.aspose.com/temporary-license/)
- **ซื้อ:** [ซื้อ Aspose.Cells](https://purchase.aspose.com/buy)

## การตั้งค่า Aspose.Cells สำหรับ Java

เมื่อคุณติดตั้งส่วนที่ต้องมีแล้ว ให้ตั้งค่าสภาพแวดล้อมการพัฒนาของคุณเพื่อใช้ Aspose.Cells เริ่มต้นด้วยการนำเข้าไลบรารีและเริ่มต้นวัตถุ Workbook ในแอปพลิเคชัน Java ของคุณ:

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // เริ่มต้นอินสแตนซ์เวิร์กบุ๊กใหม่
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## คู่มือการใช้งาน

ในส่วนนี้ เราจะแบ่งการใช้งานออกเป็นคุณลักษณะที่แตกต่างกัน ได้แก่ การเริ่มต้นเวิร์กบุ๊กและการเติมข้อมูล การสร้างและกำหนดค่าแผนภูมิ การปรับแต่งชุด และการบันทึกเวิร์กบุ๊ก

### คุณลักษณะที่ 1: การเริ่มต้นเวิร์กบุ๊กและการเติมข้อมูล

**ภาพรวม:** คุณลักษณะนี้มุ่งเน้นไปที่การสร้างเวิร์กบุ๊กใหม่ การเข้าถึงเวิร์กชีตแรก และการเติมข้อมูลสำหรับการสร้างแผนภูมิ

#### ขั้นตอนที่ 1: เริ่มต้นเวิร์กบุ๊ก
เริ่มต้นด้วยการสร้างตัวอย่าง `Workbook` วัตถุ:

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // สร้างตัวอย่างสมุดงาน
        Workbook workbook = new Workbook();
        
        // เข้าถึงแผ่นงานแรก
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### ขั้นตอนที่ 2: ตั้งชื่อคอลัมน์และป้อนข้อมูล
กำหนดส่วนหัวคอลัมน์และเติมแถวด้วยข้อมูลตัวอย่าง:

```java
        // ตั้งค่าชื่อคอลัมน์ 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // สร้างข้อมูลสุ่มสำหรับซีรีส์ 1
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // สร้างข้อมูลสุ่มสำหรับซีรีย์ 2
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### คุณสมบัติ 2: การสร้างและกำหนดค่าแผนภูมิ

**ภาพรวม:** คุณลักษณะนี้สาธิตวิธีการเพิ่มแผนภูมิลงในเวิร์กชีตของเวิร์กบุ๊ก ตั้งค่ารูปแบบ และกำหนดค่าคุณสมบัติพื้นฐาน

#### ขั้นตอนที่ 3: เพิ่มแผนภูมิลงในเวิร์กชีต
เพิ่มแผนภูมิเส้นพร้อมเครื่องหมายข้อมูล:

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // สร้างตัวอย่างสมุดงาน
        Workbook workbook = new Workbook();
        
        // เข้าถึงแผ่นงานแรก
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // เพิ่มแผนภูมิลงในแผ่นงาน
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // การเข้าถึงและกำหนดค่าแผนภูมิ
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // ตั้งค่ารูปแบบที่กำหนดไว้ล่วงหน้า
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### คุณสมบัติที่ 3: การกำหนดค่าและการปรับแต่งซีรีส์

**ภาพรวม:** เพิ่มความน่าสนใจทางภาพของแผนภูมิของคุณด้วยการปรับแต่งการตั้งค่าชุด เช่น สีที่หลากหลายและรูปแบบของเครื่องหมาย

#### ขั้นตอนที่ 4: ปรับแต่งการตั้งค่าซีรีส์
กำหนดค่าข้อมูลชุด ใช้การจัดรูปแบบแบบกำหนดเอง และปรับเครื่องหมาย:

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // สร้างตัวอย่างสมุดงาน
        Workbook workbook = new Workbook();
        
        // เข้าถึงแผ่นงานแรก
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // เพิ่มซีรีส์ลงในแผนภูมิ
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // เปิดใช้งานสีที่หลากหลายสำหรับจุดซีรีส์
        chart.getNSeries().setColorVaried(true);

        // ปรับแต่งรูปแบบและสีของเครื่องหมายซีรีส์แรก
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // ตั้งค่า X และ Y สำหรับซีรีส์แรก
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // ปรับแต่งรูปแบบและสีของเครื่องหมายซีรีส์ที่สอง
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // ตั้งค่า X และ Y สำหรับซีรีส์ที่สอง
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### คุณสมบัติที่ 4: การบันทึกสมุดงาน

**ภาพรวม:** สุดท้าย ให้บันทึกเวิร์กบุ๊กเพื่อคงการเปลี่ยนแปลงของคุณและให้แน่ใจว่าแผนภูมิจะรวมอยู่ในไฟล์ Excel

#### ขั้นตอนที่ 5: บันทึกสมุดงาน
บันทึกสมุดงานของคุณด้วยแผนภูมิที่สร้างขึ้นใหม่:

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // สร้างตัวอย่างสมุดงาน
        Workbook workbook = new Workbook();
        
        // เข้าถึงเวิร์กชีตแรกและเพิ่มข้อมูล การกำหนดค่าแผนภูมิตามขั้นตอนก่อนหน้า...
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // (การดำเนินการเพิ่มข้อมูลและกำหนดค่าแผนภูมิจะอยู่ที่นี่)

        // บันทึกสมุดงานไปยังไฟล์ Excel
        workbook.save("StyledChart.xlsx");
    }
}
```

**คำแนะนำคีย์เวิร์ด:**
- "Aspose.Cells สำหรับ Java"
- "การสร้างแผนภูมิ Excel ด้วย Java"
- “การเขียนโปรแกรม Java สำหรับการทำงานอัตโนมัติของ Excel”

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}