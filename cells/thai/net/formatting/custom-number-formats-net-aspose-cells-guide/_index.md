---
"date": "2025-04-05"
"description": "เรียนรู้วิธีการนำรูปแบบตัวเลขที่กำหนดเองไปใช้ใน .NET โดยใช้ Aspose.Cells เพื่อการนำเสนอข้อมูล Excel ที่แม่นยำ คู่มือนี้ครอบคลุมถึงการตั้งค่า การจัดรูปแบบวันที่ เปอร์เซ็นต์ และสกุลเงิน"
"title": "วิธีใช้รูปแบบตัวเลขแบบกำหนดเองใน .NET ด้วย Aspose.Cells คำแนะนำทีละขั้นตอน"
"url": "/th/net/formatting/custom-number-formats-net-aspose-cells-guide/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# วิธีใช้รูปแบบตัวเลขแบบกำหนดเองใน .NET ด้วย Aspose.Cells: คำแนะนำทีละขั้นตอน

## การแนะนำ

ปรับปรุงการจัดการไฟล์ Excel ของคุณโดยใช้ C# และ .NET ด้วยการควบคุมรูปแบบตัวเลขที่แม่นยำ บทช่วยสอนนี้จะแนะนำคุณเกี่ยวกับการตั้งค่ารูปแบบตัวเลขแบบกำหนดเองในแอปพลิเคชัน .NET โดยใช้ Aspose.Cells สำหรับ .NET ซึ่งเป็นไลบรารีอันทรงพลังที่ออกแบบมาสำหรับการจัดการ Excel

การใช้ Aspose.Cells ช่วยให้คุณใช้รูปแบบต่างๆ กับข้อมูลได้อย่างง่ายดาย ช่วยให้รายงานของคุณมีความชัดเจนและแม่นยำ ไม่ว่าจะเป็นการจัดรูปแบบวันที่ เปอร์เซ็นต์ หรือค่าสกุลเงิน การเชี่ยวชาญฟังก์ชันเหล่านี้จะช่วยเพิ่มประสิทธิภาพเวิร์กโฟลว์ของคุณ

**สิ่งที่คุณจะได้เรียนรู้:**
- การตั้งค่า Aspose.Cells สำหรับ .NET
- การนำรูปแบบตัวเลขแบบกำหนดเองไปใช้ด้วย C#
- การใช้รูปแบบโปรแกรมกับเซลล์ Excel
- การประยุกต์ใช้การจัดรูปแบบตัวเลขแบบกำหนดเองในโลกแห่งความเป็นจริง

## ข้อกำหนดเบื้องต้น

ให้แน่ใจว่าคุณมีสิ่งต่อไปนี้ก่อนที่จะเริ่มต้น:
1. **สภาพแวดล้อมการพัฒนา**:การตั้งค่าการทำงานของ .NET กับ Visual Studio หรือ IDE ที่เข้ากันได้
2. **Aspose.Cells สำหรับไลบรารี .NET**:ต้องใช้เวอร์ชัน 22.x ขึ้นไปสำหรับคู่มือนี้
3. **ความรู้พื้นฐานเกี่ยวกับ C#**:ความคุ้นเคยกับรูปแบบภาษา C# และแนวคิดการเขียนโปรแกรมจะช่วยให้คุณทำตามได้อย่างราบรื่น

## การตั้งค่า Aspose.Cells สำหรับ .NET

หากต้องการใช้ Aspose.Cells ในโปรเจ็กต์ของคุณ ให้ติดตั้งไลบรารีโดยใช้ .NET CLI หรือคอนโซลตัวจัดการแพ็คเกจภายใน Visual Studio

**การติดตั้ง .NET CLI:**
```bash
dotnet add package Aspose.Cells
```

**การติดตั้งตัวจัดการแพ็คเกจ:**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

### การขอใบอนุญาต

Aspose.Cells เสนอการทดลองใช้ฟรีเพื่อการประเมินและตัวเลือกสำหรับการใช้งานขยายเวลาผ่านใบอนุญาตชั่วคราวหรือที่ซื้อมา
- **ทดลองใช้งานฟรี**: ดาวน์โหลดจาก [ที่นี่](https://releases-aspose.com/cells/net/).
- **ใบอนุญาตชั่วคราว**: สมัครได้ที่ [หน้าใบอนุญาตชั่วคราวของ Aspose](https://purchase.aspose.com/temporary-license/) เพื่อลบข้อจำกัดในการประเมิน
- **ซื้อ**: สำหรับการเข้าถึงแบบเต็ม กรุณาเยี่ยมชม [หน้าการสั่งซื้อ](https://purchase-aspose.com/buy).

ในการเริ่มต้น Aspose.Cells ในโครงการของคุณ:
```csharp
// นำเข้าเนมสเปซ
using Aspose.Cells;

// สร้างวัตถุเวิร์กบุ๊กใหม่
Workbook workbook = new Workbook();
```

## คู่มือการใช้งาน

เราจะครอบคลุมคุณลักษณะหลักในการปรับแต่งรูปแบบตัวเลขโดยใช้ Aspose.Cells

### การเพิ่มรูปแบบวันที่แบบกำหนดเอง
**ภาพรวม**:เรียนรู้การจัดรูปแบบวันที่ในเซลล์ Excel ด้วยรูปแบบที่กำหนดเอง
1. **สร้างหรือเข้าถึงแผ่นงาน**
   ```csharp
   int sheetIndex = workbook.Worksheets.Add();
   Worksheet worksheet = workbook.Worksheets[sheetIndex];
   ```
2. **ตั้งค่าวันที่ระบบปัจจุบันด้วยรูปแบบที่กำหนดเอง**
   เพิ่มวันที่ปัจจุบันลงในเซลล์ "A1" และใช้รูปแบบการแสดงแบบกำหนดเอง
   ```csharp
   // แทรกวันที่ระบบปัจจุบันลงใน A1
   worksheet.Cells["A1"].PutValue(DateTime.Now);

   // ดึงวัตถุสไตล์เพื่อปรับแต่ง
   Style style = worksheet.Cells["A1"].GetStyle();

   // ตั้งค่ารูปแบบตัวเลขที่กำหนดเองเป็น "d-mmm-yy"
   style.Custom = "d-mmm-yy";

   // นำรูปแบบที่กำหนดเองกลับไปใช้กับเซลล์ A1
   worksheet.Cells["A1"].SetStyle(style);
   ```

### การจัดรูปแบบค่าตัวเลขเป็นเปอร์เซ็นต์
**ภาพรวม**: แสดงค่าตัวเลขในรูปแบบเปอร์เซ็นต์
1. **การแทรกและการจัดรูปแบบค่า**
   ```csharp
   // เพิ่มค่าตัวเลขลงในเซลล์ A2
   worksheet.Cells["A2"].PutValue(20);

   // ดึงสไตล์สำหรับการจัดรูปแบบ
   Style style = worksheet.Cells["A2"].GetStyle();

   // ใช้รูปแบบตัวเลขที่กำหนดเองเป็นเปอร์เซ็นต์
   style.Custom = "0.0%";

   // ตั้งค่ารูปแบบกลับเป็นเซลล์ A2
   worksheet.Cells["A2"].SetStyle(style);
   ```

### การใช้รูปแบบสกุลเงิน
**ภาพรวม**:แสดงตัวเลขในรูปแบบสกุลเงินโดยมีการจัดรูปแบบเฉพาะสำหรับค่าลบ
1. **การแทรกและรูปแบบค่าสกุลเงิน**
   ```csharp
   // เพิ่มค่าลงในเซลล์ A3
   worksheet.Cells["A3"].PutValue(2546);

   // เข้าถึงวัตถุสไตล์
   Style style = worksheet.Cells["A3"].GetStyle();

   // ตั้งค่ารูปแบบสกุลเงินที่กำหนดเอง
   style.Custom = "\u00a3#,##0;[Red]$-#,##0";

   // นำไปใช้กับเซลล์ A3
   worksheet.Cells["A3"].SetStyle(style);
   ```

## การประยุกต์ใช้งานจริง

การจัดรูปแบบตัวเลขแบบกำหนดเองนั้นมีคุณค่าอย่างยิ่งในสถานการณ์เช่น:
1. **รายงานทางการเงิน**:การจัดรูปแบบค่าสกุลเงินเพื่อความชัดเจน
2. **แดชบอร์ดการขาย**:การแสดงตัวเลขยอดขายเป็นเปอร์เซ็นต์เพื่อเน้นย้ำตัวชี้วัดประสิทธิภาพ
3. **การวางแผนกิจกรรม**:ใช้รูปแบบวันที่เพื่อจัดระเบียบและนำเสนอกำหนดการกิจกรรมได้อย่างราบรื่น

## การพิจารณาประสิทธิภาพ
เมื่อทำงานกับชุดข้อมูลขนาดใหญ่ ให้เพิ่มประสิทธิภาพการทำงานของ Aspose.Cells:
- ลดการใช้หน่วยความจำโดยกำจัดวัตถุทันทีโดยใช้ `GC.Collect()` หลังจากบันทึกไฟล์แล้ว
- ใช้สตรีมสำหรับการอ่าน/เขียนไฟล์ Excel แทนการโหลดเอกสารทั้งหมดลงในหน่วยความจำ
- ใช้แนวปฏิบัติที่ดีที่สุดในการจัดการหน่วยความจำ .NET เพื่อรักษาประสิทธิภาพ

## บทสรุป
เมื่อทำตามคำแนะนำนี้ คุณจะได้เรียนรู้วิธีนำรูปแบบตัวเลขที่กำหนดเองไปใช้ในแอปพลิเคชัน .NET โดยใช้ Aspose.Cells ความสามารถนี้ช่วยปรับปรุงการนำเสนอข้อมูลและรับรองความถูกต้องแม่นยำและความสวยงามของรายงานและสเปรดชีต

**ขั้นตอนต่อไป**:ทดลองใช้ตัวเลือกการจัดรูปแบบอื่น ๆ ที่มีใน Aspose.Cells เช่น การจัดรูปแบบตามเงื่อนไขหรือการปรับปรุงแผนภูมิ

## ส่วนคำถามที่พบบ่อย
1. **ฉันจะขอใบอนุญาตชั่วคราวสำหรับ Aspose.Cells ได้อย่างไร**
   - สมัครได้ที่ [หน้าใบอนุญาตชั่วคราว](https://purchase-aspose.com/temporary-license/).
2. **รูปแบบใดบ้างที่รองรับรูปแบบตัวเลขแบบกำหนดเองใน Aspose.Cells?**
   - วันที่ เปอร์เซ็นต์ สกุลเงิน และอื่นๆ โดยใช้สตริงรูปแบบ Excel มาตรฐาน
3. **ฉันสามารถใช้ Aspose.Cells กับภาษา .NET อื่นๆ เช่น VB.NET ได้หรือไม่**
   - ใช่ ไลบรารีนี้สามารถใช้งานได้กับทุกภาษาที่รองรับ .NET
4. **ฉันควรทำอย่างไรหากตัวเลขที่จัดรูปแบบของฉันไม่แสดงอย่างถูกต้อง?**
   - ตรวจสอบสตริงรูปแบบตัวเลขที่กำหนดเองของคุณอีกครั้งเพื่อดูว่ามีการพิมพ์ผิดหรือข้อผิดพลาดทางไวยากรณ์หรือไม่
5. **ฉันสามารถหาตัวอย่างการใช้งาน Aspose.Cells เพิ่มเติมได้ที่ไหน**
   - สำรวจเอกสารรายละเอียดและโค้ดตัวอย่างได้ที่ [เอกสารประกอบ Aspose](https://reference-aspose.com/cells/net/).

## ทรัพยากร
- [เอกสาร Aspose.Cells สำหรับ .NET](https://reference.aspose.com/cells/net/)
- [ดาวน์โหลดเวอร์ชั่นล่าสุด](https://releases.aspose.com/cells/net/)
- [ซื้อใบอนุญาต](https://purchase.aspose.com/buy)
- [ดาวน์โหลดทดลองใช้งานฟรี](https://releases.aspose.com/cells/net/)
- [การขอใบอนุญาตชั่วคราว](https://purchase.aspose.com/temporary-license/)
- [ฟอรั่มสนับสนุน Aspose](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}