---
"description": "เรียนรู้วิธีการรับความกว้างและความสูงของกระดาษของเวิร์กชีตใน Aspose.Cells สำหรับ .NET ด้วยคำแนะนำทีละขั้นตอนง่ายๆ"
"linktitle": "รับความกว้างและความสูงของกระดาษของแผ่นงาน"
"second_title": "เอกสารอ้างอิง API Aspose.Cells สำหรับ .NET"
"title": "รับความกว้างและความสูงของกระดาษของแผ่นงาน"
"url": "/th/net/excel-display-settings-csharp-tutorials/get-paper-width-and-height-of-worksheet/"
"weight": 80
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# รับความกว้างและความสูงของกระดาษของแผ่นงาน

## การแนะนำ

เคยลองพิมพ์แผ่นงาน Excel และต้องจัดการกับขนาดของกระดาษที่แตกต่างกันซึ่งสร้างความสับสนหรือไม่ ถ้าคุณเป็นเหมือนฉัน คุณจะรู้ว่าไม่มีอะไรจะทำให้วันของคุณแย่ลงได้เท่ากับการจัดวางที่ออกมาไม่ถูกต้อง ไม่ว่าคุณจะกำลังพิมพ์รายงาน ใบแจ้งหนี้ หรือเพียงแค่รายการธรรมดา การทำความเข้าใจวิธีการปรับขนาดกระดาษด้วยโปรแกรมจะช่วยให้คุณหลีกเลี่ยงปัญหาได้มาก วันนี้ เราจะเจาะลึกเข้าไปในโลกของ Aspose.Cells สำหรับ .NET เพื่อดูว่าจะเรียกค้นและตั้งค่าขนาดกระดาษโดยตรงในแอปพลิเคชันของคุณได้อย่างไร มาลงมือทำและลงมือจัดการรายละเอียดเกี่ยวกับขนาดกระดาษกันเลย!

## ข้อกำหนดเบื้องต้น 

ก่อนที่เราจะเข้าสู่เรื่องการเขียนโค้ด เรามารวบรวมสิ่งที่คุณต้องมีเพื่อเริ่มต้นกันก่อน:

1. ความเข้าใจเบื้องต้นเกี่ยวกับ C#: คุณควรมีความเข้าใจเบื้องต้นเกี่ยวกับ C# หากคุณเพิ่งเริ่มเขียนโปรแกรม ไม่ต้องกังวล เราจะอธิบายให้เข้าใจง่ายๆ
2. ไลบรารี Aspose.Cells: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้งไลบรารี Aspose.Cells สำหรับ .NET ไว้ในเครื่องของคุณแล้ว คุณสามารถดาวน์โหลดได้จาก [ลิงค์นี้](https://releases-aspose.com/cells/net/).
3. สภาพแวดล้อมการพัฒนา .NET: ตั้งค่า Visual Studio หรือ IDE ใดๆ ที่คุณเลือกเพื่อเขียนและดำเนินการโค้ด C# หากคุณไม่แน่ใจว่าจะเริ่มต้นจากที่ใด Visual Studio Community Edition ถือเป็นตัวเลือกที่ดี
4. เอกสารอ้างอิงและเอกสารประกอบ: ทำความคุ้นเคยกับเอกสารประกอบของ Aspose.Cells เพื่อข้อมูลเชิงลึกที่มากขึ้น คุณสามารถค้นหาได้ [ที่นี่](https://reference-aspose.com/cells/net/).
5. ความรู้พื้นฐานเกี่ยวกับไฟล์ Excel: การทำความเข้าใจว่าไฟล์ Excel มีโครงสร้างอย่างไร (เวิร์กชีต แถว และคอลัมน์) จะเป็นประโยชน์มาก

เยี่ยมมาก! ตอนนี้เราได้ตรวจสอบสิ่งสำคัญแล้ว เรามาเริ่มนำเข้าแพ็คเกจที่จำเป็นกันเลย

## แพ็คเกจนำเข้า

เพื่อให้ชีวิตของเราง่ายขึ้นและใช้ประโยชน์จาก Aspose.Cells ได้อย่างเต็มที่ เราจำเป็นต้องนำเข้าแพ็คเกจสองสามตัว ซึ่งง่ายพอๆ กับการเพิ่ม `using` คำสั่งที่ด้านบนของไฟล์โค้ดของคุณ นี่คือสิ่งที่คุณต้องนำเข้า:

```csharp
using System;
using System.IO;
```

บรรทัดนี้ช่วยให้เราเข้าถึงคลาสและเมธอดทั้งหมดภายในไลบรารี Aspose.Cells ทำให้จัดการไฟล์ Excel ได้ง่ายขึ้น ตอนนี้มาดูคำแนะนำทีละขั้นตอนในการดึงข้อมูลความกว้างและความสูงของกระดาษสำหรับกระดาษขนาดต่างๆ กัน

## ขั้นตอนที่ 1: สร้างสมุดงานใหม่

ขั้นตอนแรกในการใช้งาน Aspose.Cells คือการสร้างเวิร์กบุ๊กใหม่ ลองนึกถึงเวิร์กบุ๊กเป็นผืนผ้าใบเปล่าที่คุณสามารถเพิ่มเวิร์กชีต เซลล์ และในกรณีของเราคือกำหนดขนาดกระดาษ

```csharp
//สร้างสมุดงาน
Workbook wb = new Workbook();
```

บรรทัดนี้จะสร้างอ็อบเจ็กต์เวิร์กบุ๊กใหม่ซึ่งพร้อมให้เราจัดการ คุณจะยังไม่เห็นอะไรเลย แต่แคนวาสของเราถูกตั้งค่าเรียบร้อยแล้ว!

## ขั้นตอนที่ 2: เข้าถึงแผ่นงานแรก

ตอนนี้เรามีเวิร์กบุ๊กแล้ว เราต้องเข้าถึงเวิร์กชีตเฉพาะภายในเวิร์กบุ๊กนั้น เวิร์กชีตเปรียบเสมือนหน้าเดียวในเวิร์กบุ๊กของคุณ และเป็นที่ที่ทุกการกระทำเกิดขึ้น

```csharp
//เข้าถึงแผ่นงานแรก
Worksheet ws = wb.Worksheets[0];
```

ที่นี่ เรากำลังหยิบแผ่นงานแรก (ดัชนี 0) จากสมุดงานของเรา คุณอาจคิดเหมือนการพลิกไปที่หน้าแรกของหนังสือ 

## ขั้นตอนที่ 3: ตั้งค่าขนาดกระดาษและรับขนาด

ตอนนี้มาถึงส่วนที่น่าตื่นเต้นแล้ว! เราจะตั้งค่าขนาดกระดาษที่แตกต่างกันและดึงข้อมูลขนาดออกมาทีละขนาด ขั้นตอนนี้มีความสำคัญมาก เพราะช่วยให้เราเห็นว่าขนาดที่แตกต่างกันส่งผลต่อเค้าโครงอย่างไร

```csharp
//ตั้งค่าขนาดกระดาษเป็น A2 และพิมพ์ความกว้างและความสูงของกระดาษเป็นนิ้ว
ws.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```

ในบล็อกนี้ เรากำหนดขนาดกระดาษเป็น A2 จากนั้นดึงความกว้างและความสูงออกมา `PaperWidth` และ `PaperHeight` คุณสมบัตินี้ระบุขนาดเป็นนิ้ว เหมือนกับการตรวจสอบขนาดของกรอบก่อนจะใส่รูปลงไป

## ขั้นตอนที่ 4: ทำซ้ำสำหรับขนาดกระดาษอื่นๆ

มาทำซ้ำขั้นตอนนี้กับขนาดกระดาษทั่วไปอื่นๆ กัน เราจะตรวจสอบขนาด A3, A4 และ Letter การทำซ้ำนี้มีความสำคัญในการทำความเข้าใจว่าแต่ละขนาดถูกกำหนดไว้อย่างไรภายในกรอบงาน Aspose.Cells

```csharp
//ตั้งค่าขนาดกระดาษเป็น A3 และพิมพ์ความกว้างและความสูงของกระดาษเป็นนิ้ว
ws.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
//ตั้งค่าขนาดกระดาษเป็น A4 และพิมพ์ความกว้างและความสูงของกระดาษเป็นนิ้ว
ws.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
//ตั้งค่าขนาดกระดาษเป็น Letter และพิมพ์ความกว้างและความสูงของกระดาษเป็นนิ้ว
ws.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```

แต่ละบล็อกเหล่านี้เลียนแบบขั้นตอนก่อนหน้าแต่มีการปรับเปลี่ยน `PaperSize` ปรับเปลี่ยนขนาดได้ตามต้องการ เพียงเปลี่ยนตัวระบุขนาด ก็สามารถปรับขนาดกระดาษได้หลากหลายแบบอย่างง่ายดาย เหมือนกับการเปลี่ยนขนาดกล่องตามขนาดที่คุณต้องการจัดเก็บ!

## บทสรุป

และแล้วคุณก็ทำได้! ด้วยการทำตามขั้นตอนเหล่านี้ คุณสามารถตั้งค่าและเรียกค้นขนาดของกระดาษขนาดต่างๆ ใน Aspose.Cells สำหรับ .NET ได้อย่างง่ายดาย ความสามารถนี้ไม่เพียงแต่ช่วยประหยัดเวลาของคุณเท่านั้น แต่ยังป้องกันความผิดพลาดในการพิมพ์ที่อาจเกิดขึ้นได้เนื่องจากการตั้งค่าหน้ากระดาษที่ไม่ถูกต้องอีกด้วย ดังนั้น ครั้งต่อไปที่คุณต้องพิมพ์แผ่นงาน Excel หรือสร้างรายงาน คุณก็สามารถทำได้อย่างมั่นใจ เพราะรู้ว่าคุณมีมิติอยู่ในมือแล้ว 

## คำถามที่พบบ่อย

### Aspose.Cells คืออะไร?
Aspose.Cells คือไลบรารี .NET ที่ออกแบบมาเพื่อประมวลผลไฟล์ Excel โดยไม่ต้องติดตั้ง Excel

### ฉันสามารถใช้ Aspose.Cells ได้ฟรีหรือไม่?
ใช่! คุณสามารถเริ่มต้นด้วยการทดลองใช้ฟรีได้ที่ [ลิงค์นี้](https://releases-aspose.com/).

### ฉันจะตั้งค่าขนาดกระดาษเองได้อย่างไร?
Aspose.Cells ให้ตัวเลือกในการกำหนดขนาดกระดาษแบบกำหนดเองโดยใช้ `PageSetup` ระดับ.

### จำเป็นต้องมีความรู้ในการเขียนโค้ดเพื่อใช้ Aspose.Cells หรือไม่
ความรู้พื้นฐานในการเขียนโค้ดเป็นประโยชน์ แต่คุณสามารถทำตามบทช่วยสอนเพื่อให้เข้าใจง่ายยิ่งขึ้น!

### ฉันสามารถหาตัวอย่างเพิ่มเติมได้ที่ไหน
การ [เอกสารประกอบ Aspose.Cells](https://reference.aspose.com/cells/net/) มีตัวอย่างและบทช่วยสอนมากมาย

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}