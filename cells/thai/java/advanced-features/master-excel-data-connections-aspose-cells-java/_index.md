---
date: '2025-12-27'
description: เรียนรู้วิธีเปลี่ยนแหล่งข้อมูลของ Excel อย่างโปรแกรมโดยใช้ Aspose.Cells
  for Java, แก้ไขการเชื่อมต่อข้อมูลของ Excel และทำให้กระบวนการทำงานของคุณเป็นอัตโนมัติ
keywords:
- Excel data connections
- Aspose.Cells Java
- modify Excel data connections programmatically
title: วิธีเปลี่ยนแหล่งข้อมูล Excel ด้วย Aspose.Cells สำหรับ Java
url: /th/java/advanced-features/master-excel-data-connections-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# เปลี่ยนแหล่งข้อมูล Excel ด้วย Aspose.Cells สำหรับ Java

## บทนำ
กำลังประสบปัญหาในการ **change Excel data source** และแก้ไขการเชื่อมต่อข้อมูลภายในไฟล์ Excel ด้วยโปรแกรมหรือไม่? คู่มือฉบับสมบูรณ์นี้ออกแบบมาสำหรับนักพัฒนาที่ต้องการอัตโนมัติขั้นตอนการสร้างรายงานด้วยไลบรารี **Aspose.Cells for Java** ที่ทรงพลัง เราจะพาคุณผ่านการโหลดเวิร์กบุ๊ก Excel, การอัปเดตการเชื่อมต่อภายนอก, และการบันทึกการเปลี่ยนแปลง—ทั้งหมดโดยใช้โค้ด Java

### สิ่งที่คุณจะได้เรียนรู้
- วิธีตั้งค่า Aspose.Cells สำหรับ Java ใน Maven หรือ Gradle.  
- **Load Excel workbook Java** – อ่านไฟล์ที่มีอยู่เข้าสู่หน่วยความจำ.  
- **Modify Excel data connections** – ปรับปรุงชื่อการเชื่อมต่อ, เส้นทาง ODC, และคำสั่ง SQL.  
- **Save Excel workbook Java** – เขียนเวิร์กบุ๊กที่อัปเดตกลับไปยังดิสก์.  

ให้แน่ใจว่าคุณมีทุกอย่างที่ต้องการก่อนที่เราจะเริ่มลงลึก

## คำตอบอย่างรวดเร็ว
- **What is the primary library?** Aspose.Cells for Java.  
- **Which method loads a workbook?** `new Workbook(filePath)`.  
- **How do I update the connection string?** Use `DBConnection.setConnectionInfo(...)`.  
- **Can I change the ODC file path?** Yes, via `ExternalConnection.setOdcFile(...)`.  
- **Do I need a license for production?** A commercial license removes evaluation limits.

## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเริ่ม, โปรดตรวจสอบว่าคุณมีสิ่งต่อไปนี้:

### ไลบรารีที่จำเป็น
Aspose.Cells for Java รุ่น 25.3 หรือใหม่กว่าให้ API ที่ใช้ในบทแนะนำนี้

### การตั้งค่าสภาพแวดล้อม
- ติดตั้ง Java Development Kit (JDK)  
- IDE เช่น IntelliJ IDEA, Eclipse หรือ NetBeans

### ความรู้เบื้องต้นที่จำเป็น
ความคุ้นเคยกับ Java, Maven หรือ Gradle, และแนวคิดพื้นฐานของ SQL จะช่วยให้คุณตามได้อย่างราบรื่น

## การตั้งค่า Aspose.Cells สำหรับ Java
เพื่อเริ่มใช้ Aspose.Cells, เพิ่มไลบรารีลงในโปรเจกต์ของคุณ:

**การตั้งค่า Maven**  
เพิ่ม dependency ลงใน `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**การตั้งค่า Gradle**  
แทรกบรรทัดต่อไปนี้ลงใน `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### ขั้นตอนการรับใบอนุญาต
Aspose.Cells มีรุ่นทดลองฟรีเพื่อให้คุณประเมินไลบรารีก่อนซื้อ:

- เยี่ยมชม [free trial page](https://releases.aspose.com/cells/java/) และดาวน์โหลดแพคเกจประเมินผล  
- สำหรับการใช้งานเต็มรูปแบบ, ซื้อใบอนุญาตจาก [purchase portal](https://purchase.aspose.com/buy)  
- ต้องการเข้าถึงชั่วคราว? ขอ [temporary license](https://purchase.aspose.com/temporary-license/)  

เมื่อไลบรารีถูกอ้างอิงและมีใบอนุญาตแล้ว, คุณพร้อมเขียนโค้ดแล้ว

## คู่มือการดำเนินการ

### ฟีเจอร์ 1: โหลดเวิร์กบุ๊กจากไฟล์
**What does this step do?** It demonstrates how to **load Excel workbook Java** so you can work with its data connections.

#### คำแนะนำแบบขั้นตอน
**Define Your Data Directory** – บอกโปรแกรมว่าที่อยู่ของไฟล์ต้นทางอยู่ที่ไหน:

```java
String dataDir = "YOUR_DATA_DIRECTORY";
```
ตรวจสอบให้แน่ใจว่า `DataConnection.xlsx` มีอยู่ในโฟลเดอร์นั้น

**Load the Workbook** – สร้างอินสแตนซ์ของอ็อบเจกต์ `Workbook`:

```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook(dataDir + "DataConnection.xlsx");
```
อินสแตนซ์ `Workbook` ตอนนี้เป็นตัวแทนของไฟล์ Excel ของคุณในหน่วยความจำ

### ฟีเจอร์ 2: แก้ไขการเชื่อมต่อข้อมูลในเวิร์กบุ๊ก
**Why modify?** การอัปเดตการเชื่อมต่อภายนอกทำให้คุณ **change Excel data source** ได้โดยไม่ต้องเปิดไฟล์ด้วยตนเอง

#### คำแนะนำแบบขั้นตอน
**Access the Data Connection** – ดึงการเชื่อมต่อแรก (คุณสามารถวนลูปสำหรับหลายการเชื่อมต่อได้):

```java
import com.aspose.cells.DBConnection;
import com.aspose.cells.ExternalConnection;
import com.aspose.cells.OLEDBCommandType;

ExternalConnection conn = workbook.getDataConnections().get(0);
```
`getDataConnections()` คืนคอลเลกชันของการเชื่อมต่อทั้งหมด, ทำให้คุณสามารถ **modify excel data connections** แยกแต่ละอันได้

**Modify Connection Properties** – เปลี่ยนชื่อ, ไฟล์ ODC, ประเภทคำสั่ง, และคำสั่ง SQL:

```java
conn.setName("MyConnectionName");
conn.setOdcFile(dataDir + "MyDefaulConnection.odc");
```

Cast to `DBConnection` for database‑specific settings:

```java
DBConnection dbConn = (DBConnection) conn;
dbConn.setCommandType(OLEDBCommandType.SQL_STATEMENT);
dbConn.setCommand("SELECT * FROM AdminTable");

String connectionString = "Server=myServerAddress;Database=myDataBase;User ID=myUsername;Password=myPassword;Trusted_Connection=False";
dbConn.setConnectionInfo(connectionString);
```
ที่นี่คุณ **update excel external connection** รายละเอียดเช่น คำสั่ง SQL และสตริงการเชื่อมต่อ

### ฟีเจอร์ 3: บันทึกเวิร์กบุ๊กไปยังไฟล์
**What happens next?** หลังจากอัปเดตการเชื่อมต่อ, คุณต้อง **save Excel workbook Java** เพื่อให้การเปลี่ยนแปลงคงอยู่

#### คำแนะนำแบบขั้นตอน
**Define Output Directory** – กำหนดที่ที่ไฟล์ที่แก้ไขแล้วจะถูกเขียนออกไป:

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
```

**Save the Workbook** – เขียนเวิร์กบุ๊กกลับไปยังดิสก์:

```java
workbook.save(outDir + "MESQLDataConnection_out.xlsx");
```
เมธอด `save()` สรุปการทำงาน **change excel data source** ให้เสร็จสมบูรณ์

## การประยุกต์ใช้งานจริง
การแก้ไขการเชื่อมต่อข้อมูลของ Excel ด้วยโปรแกรมเปิดประตูหลายด้าน:

1. **Automated Reporting** – สร้างรายงานที่ดึงข้อมูลล่าสุดจากฐานข้อมูลเสมอ  
2. **Data Syncing** – ทำให้เวิร์กบุ๊กสอดคล้องกับระบบสดโดยไม่ต้องรีเฟรชด้วยมือ  
3. **Dynamic Dashboards** – สร้างแดชบอร์ดที่แสดงเมตริกแบบเรียลไทม์  

การผสานรวม Aspose.Cells กับ CRM, ERP หรือแพลตฟอร์ม BI สามารถลดความพยายามในการทำงานด้วยมือได้อย่างมาก

## ข้อควรพิจารณาด้านประสิทธิภาพ
เมื่อจัดการกับเวิร์กบุ๊กขนาดใหญ่หรือผลลัพธ์จำนวนมหาศาล:

- ประมวลผลข้อมูลเป็นชุดเพื่อหลีกเลี่ยงการกระโดดของหน่วยความจำ  
- ปรับแต่งคำสั่ง SQL ของคุณให้เร็วที่สุด  
- ปล่อยทรัพยากรโดยเร็ว; เรียก `workbook.dispose()` หากไม่ต้องการอ็อบเจกต์อีกต่อไป  

แนวปฏิบัติเหล่านี้ทำให้แอปพลิเคชันของคุณตอบสนองได้ดีขณะ **changing Excel data source**

## สรุป
คุณได้เรียนรู้วิธี **change Excel data source** ด้วยการโหลดเวิร์กบุ๊ก, **modify excel data connections**, และบันทึกไฟล์ที่อัปเดตโดยใช้ **Aspose.Cells for Java** ความสามารถนี้ช่วยให้คุณอัตโนมัติขั้นตอนการทำงานที่ขับเคลื่อนด้วยข้อมูลและทำให้ไฟล์ Excel สอดคล้องกับระบบภายนอกได้เสมอ

### ขั้นตอนต่อไป
- ทดลองใช้หลายการเชื่อมต่อด้วยลูปผ่าน `workbook.getDataConnections()`  
- สำรวจคุณลักษณะอื่นของ Aspose.Cells เช่น การสร้างแผนภูมิ, การจัดรูปแบบเซลล์, และการจัดการพีโวท์เทเบิล  

พร้อมเพิ่มประสิทธิภาพการทำงานของคุณหรือยัง? นำโค้ดสคริปต์เหล่านี้ไปใช้วันนี้และดูผลผลิตของคุณพุ่งสูงขึ้น!

## คำถามที่พบบ่อย

**Q1: How do I handle multiple data connections in a workbook?**  
A1: ใช้ `workbook.getDataConnections().get(index)` ภายในลูปเพื่อเข้าถึงแต่ละการเชื่อมต่อแยกกัน

**Q2: Can I modify other properties of an Excel file using Aspose.Cells Java?**  
A2: แน่นอน! Aspose.Cells รองรับการจัดรูปแบบเซลล์, การจัดการเวิร์กชีต, การสร้างแผนภูมิ, และอื่น ๆ อีกมากมาย

**Q3: What if my SQL command fails to execute?**  
A3: ตรวจสอบสตริงการเชื่อมต่อ, ตรวจสอบสิทธิ์ของฐานข้อมูล, และตรวจสอบรายละเอียดของข้อยกเว้นเพื่อหาสาเหตุ

**Q4: Where can I get support for Aspose.Cells issues?**  
A4: เยี่ยมชม [Aspose forum](https://forum.aspose.com/c/cells/9) เพื่อถามคำถามหรือค้นหาโซลูชันที่มีอยู่

**Q5: Are there limitations in the free trial version?**  
A5: รุ่นประเมินผลจะเพิ่มลายน้ำและอาจจำกัดความจุการประมวลผล ซื้อใบอนุญาตเพื่อใช้งานโดยไม่มีข้อจำกัด

## แหล่งข้อมูล
- **Documentation:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Download:** [Aspose.Cells for Java Releases](https://releases.aspose.com/cells/java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**อัปเดตล่าสุด:** 2025-12-27  
**ทดสอบด้วย:** Aspose.Cells Java 25.3  
**ผู้เขียน:** Aspose