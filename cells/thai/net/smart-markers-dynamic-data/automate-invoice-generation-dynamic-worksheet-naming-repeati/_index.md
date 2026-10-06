---
category: general
date: 2026-02-14
description: 'อัตโนมัติการสร้างใบแจ้งหนี้ด้วย SmartMarker: เรียนรู้วิธีทำซ้ำแผ่นงาน,
  ตั้งชื่อแบบไดนามิก, และเชี่ยวชาญการตั้งชื่อแผ่นงานแบบไดนามิกในเวลาไม่กี่นาที.'
draft: false
keywords:
- automate invoice generation
- how to name worksheets
- how to repeat worksheet
- dynamic worksheet naming
language: th
og_description: อัตโนมัติการสร้างใบแจ้งหนี้ด้วย SmartMarker. คู่มือนี้แสดงวิธีทำซ้ำแผ่นงาน,
  ตั้งชื่อแผ่นงานแบบไดนามิก, และเชี่ยวชาญการตั้งชื่อแผ่นงานแบบไดนามิก.
og_title: อัตโนมัติการสร้างใบแจ้งหนี้ – การตั้งชื่อแผ่นงานแบบไดนามิกและการทำซ้ำ
tags:
- C#
- SmartMarker
- Excel Automation
title: อัตโนมัติการสร้างใบแจ้งหนี้ – การตั้งชื่อแผ่นงานแบบไดนามิกและการทำซ้ำใน C#
url: /th/net/smart-markers-dynamic-data/automate-invoice-generation-dynamic-worksheet-naming-repeati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การสร้างใบแจ้งหนี้อัตโนมัติ – การตั้งชื่อ Worksheet แบบไดนามิกและการทำซ้ำใน C#

เคยสงสัยไหมว่า **การสร้างใบแจ้งหนี้อัตโนมัติ** จะทำอย่างไรโดยไม่ต้องคัดลอกแผ่นงานด้วยตนเองสำหรับแต่ละคำสั่งซื้อ? คุณไม่ได้อยู่คนเดียว นักพัฒนาหลายคนเจออุปสรรคเมื่อต้องการ Worksheet แยกสำหรับแต่ละใบแจ้งหนี้พร้อมกับให้ชื่อแผ่นงานสะท้อนหมายเลขคำสั่งซื้อ ในบทเรียนนี้เราจะใช้ `SmartMarkerProcessor` ของ SmartMarker เพื่อแก้ปัญหานั้นและแสดงให้คุณ **วิธีตั้งชื่อ Worksheet** อย่างไดนามิก พร้อมกับ **วิธีทำซ้ำ Worksheet** สำหรับแต่ละระเบียน สุดท้ายคุณจะได้ตัวอย่าง C# ที่พร้อมรันซึ่งสร้างเวิร์กบุ๊กที่แต่ละใบแจ้งหนี้อยู่บนแท็บที่ตั้งชื่ออย่างสวยงาม

เราจะเดินผ่านทุกขั้นตอน—from การดึงคำสั่งซื้อจากแหล่งข้อมูลไปจนถึงการกำหนดค่า `SmartMarkerOptions` เพื่อการตั้งชื่อ Worksheet แบบไดนามิก ไม่ต้องอ้างอิงเอกสารภายนอก; ทุกอย่างที่คุณต้องการอยู่ที่นี่ ความรู้พื้นฐานเล็กน้อยเกี่ยวกับ C# และการอ้างอิงไลบรารี Aspose.Cells (หรือเอนจินที่รองรับ SmartMarker) ก็เพียงพอ

---

## สิ่งที่คุณจะสร้าง

- ดึงคอลเลกชันของอ็อบเจ็กต์ Order
- กำหนดค่า SmartMarker ให้ **ทำซ้ำ Worksheet** สำหรับแต่ละ Order
- ใช้ **การตั้งชื่อ Worksheet แบบไดนามิก** ด้วยตัวแปร `{OrderId}`
- สร้างไฟล์ Excel ที่แต่ละแท็บมีชื่อ `Invoice_12345`, `Invoice_67890` เป็นต้น
- ตรวจสอบผลลัพธ์โดยการเปิดเวิร์กบุ๊ก

---

## ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (โค้ดยังคอมไพล์ได้กับ .NET 5+ ด้วย)
- Aspose.Cells for .NET (หรือไลบรารีใด ๆ ที่รองรับ SmartMarker) ติดตั้งผ่าน NuGet:

```bash
dotnet add package Aspose.Cells
```

- คลาส `Order` เบื้องต้น (คุณสามารถแทนที่ด้วย DTO ของคุณเอง)

---

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และโมเดล

แรกเริ่มสร้างแอปคอนโซลใหม่และกำหนดโมเดลข้อมูลที่แทนคำสั่งซื้อ

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    // Simple POCO representing an order – replace fields as needed
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }
    }

    class Program
    {
        static void Main()
        {
            // Retrieve orders (in real life this could be a DB call)
            var orders = GetOrders();

            // The rest of the tutorial continues here...
        }

        // Mock method – in production pull from EF Core, Dapper, etc.
        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

> **เคล็ดลับ:** ทำโมเดลให้เบา ๆ สำหรับการสาธิต; คุณสามารถเพิ่มรายละเอียดเช่น รายการสินค้า รายละเอียดภาษี ฯลฯ ในภายหลังได้

---

## ขั้นตอนที่ 2: เตรียมเทมเพลต Excel

SmartMarker ทำงานกับเทมเพลตเวิร์กบุ๊ก สร้างไฟล์ชื่อ `InvoiceTemplate.xlsx` ที่มี Worksheet เดียวชื่อ `InvoiceTemplate` ในเซลล์ **A1** ใส่ตัวแปร SmartMarker เช่น:

```
{{OrderId}} – {{Customer}} – {{Date}} – ${{Total}}
```

คุณสามารถจัดรูปแบบเซลล์ตามต้องการ—หัวข้อหนา, การจัดรูปแบบสกุลเงิน ฯลฯ บันทึกไฟล์ไว้ที่โฟลเดอร์รากของโปรเจกต์

> **ทำไมต้องใช้เทมเพลต?** มันแยกการออกแบบจากโค้ด ทำให้ดีไซเนอร์ปรับรูปลักษณ์ได้โดยไม่ต้องแก้โค้ด

---

## ขั้นตอนที่ 3: กำหนดค่า SmartMarker Options – ทำซ้ำและตั้งชื่อ Worksheet

ต่อไปเราจะบอก SmartMarker ให้ *ทำซ้ำ* Worksheet เทมเพลตสำหรับทุก Order และให้แต่ละสำเนามีชื่อที่รวม Order ID นี่คือหัวใจของ **การตั้งชื่อ Worksheet แบบไดนามิก**

```csharp
// Inside Main() after retrieving orders
// Load the template workbook
Workbook wb = new Workbook("InvoiceTemplate.xlsx");

// Set up SmartMarker options
var smartMarkerOptions = new SmartMarkerOptions
{
    // Instructs SmartMarker to create a new worksheet per data item
    RepeatWorksheet = true,

    // Naming pattern – {OrderId} will be replaced with the actual value
    RepeatWorksheetName = "Invoice_{OrderId}"
};

// Run the processor
wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

// Save the result
string outputPath = "GeneratedInvoices.xlsx";
wb.Save(outputPath);

Console.WriteLine($"✅ Invoices generated: {outputPath}");
```

### วิธีการทำงาน

- **`RepeatWorksheet = true`** บอกเอนจินให้คัดลอกแผ่นงานต้นฉบับสำหรับแต่ละองค์ประกอบในคอลเลกชัน `orders` ซึ่งตอบโจทย์ **วิธีทำซ้ำ Worksheet**
- **`RepeatWorksheetName = "Invoice_{OrderId}"`** เป็นสตริงเทมเพลตที่ `{OrderId}` จะถูกแทนที่ด้วยค่า ID ของ Order ปัจจุบัน นี่คือคำตอบของ **วิธีตั้งชื่อ Worksheet** และ **การตั้งชื่อ Worksheet แบบไดนามิก**
- ตัวประมวลผลจะผสานฟิลด์ของแต่ละ Order (`{{OrderId}}`, `{{Customer}}` เป็นต้น) ลงในแผ่นงานที่คัดลอกใหม่ ทำให้ได้ใบแจ้งหนี้ที่เต็มรูปแบบ

---

## ขั้นตอนที่ 4: รันแอปพลิเคชันและตรวจสอบผลลัพธ์

คอมไพล์และรันแอปคอนโซล:

```bash
dotnet run
```

คุณควรเห็นข้อความแสดงความสำเร็จในคอนโซล เปิดไฟล์ `GeneratedInvoices.xlsx` แล้วคุณจะพบสามแท็บ:

- **Invoice_1001**
- **Invoice_1002**
- **Invoice_1003**

แต่ละแผ่นงานจะมีข้อมูลคำสั่งซื้อที่แทนที่ในตัวแปรตามที่ออกแบบไว้ในเทมเพลต แสดงให้เห็นว่า **การสร้างใบแจ้งหนี้อัตโนมัติ** ทำงานครบวงจร

### ภาพหน้าจอที่คาดหวัง (ข้อความแทนภาพสำหรับ SEO)

![ตัวอย่างการสร้างใบแจ้งหนี้อัตโนมัติที่แสดง Worksheet สามแผ่นที่ตั้งชื่อแบบไดนามิก](/images/invoice-automation.png)

> *ข้อความ alt ของภาพรวมถึงคีย์เวิร์ดหลักเพื่อสนับสนุน SEO*

---

## ขั้นตอนที่ 5: กรณีขอบและตัวแปรที่พบบ่อย

### ถ้า OrderId มีอักขระที่ไม่อนุญาต?

ชื่อแผ่นงานของ Excel ไม่สามารถมี `\ / ? * [ ] :` หาก ID ของคุณอาจมีอักขระเหล่านี้ ให้ทำการทำความสะอาดก่อน:

```csharp
RepeatWorksheetName = "Invoice_{SanitizedOrderId}"
```

เพิ่มคุณสมบัติคำนวณในคลาส `Order`:

```csharp
public string SanitizedOrderId => OrderId.ToString().Replace("/", "-").Replace("\\", "-");
```

### ต้องการเก็บแผ่นงานเทมเพลตไว้ด้วย?

ตั้งค่า `smartMarkerOptions.RemoveTemplate = false;` (ค่าเริ่มต้นคือ `true`) เพื่อให้แผ่นงาน `InvoiceTemplate` ยังคงอยู่เป็นอ้างอิง

### ต้องการจัดกลุ่มใบแจ้งหนี้ตามลูกค้า?

คุณสามารถทำ **repeat groups** ซ้อนกันได้ ก่อนทำซ้ำตามลูกค้า แล้วทำซ้ำตามคำสั่งซื้อภายในแต่ละแผ่นงานของลูกค้า ไวยากรณ์จะซับซ้อนขึ้นเล็กน้อย แต่หลักการยังคงเหมือนเดิม—ใช้ `RepeatWorksheet` และรูปแบบการตั้งชื่อที่สะท้อนโครงสร้างลำดับชั้น

---

## ตัวอย่างทำงานเต็มรูปแบบ (โค้ดทั้งหมดในไฟล์เดียว)

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }

        // Helper for safe sheet names
        public string SanitizedOrderId => OrderId.ToString();
    }

    class Program
    {
        static void Main()
        {
            var orders = GetOrders();

            // Load template
            Workbook wb = new Workbook("InvoiceTemplate.xlsx");

            // Configure SmartMarker for repeating and naming worksheets
            var smartMarkerOptions = new SmartMarkerOptions
            {
                RepeatWorksheet = true,
                RepeatWorksheetName = "Invoice_{OrderId}" // dynamic worksheet naming
                // RemoveTemplate = true; // default behavior
            };

            // Process the data
            wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

            // Save the final workbook
            string outputPath = "GeneratedInvoices.xlsx";
            wb.Save(outputPath);

            Console.WriteLine($"✅ Invoices generated: {outputPath}");
        }

        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

คัดลอก‑วางโค้ดนี้ลงใน `Program.cs` วางไฟล์ `InvoiceTemplate.xlsx` ข้าง ๆ แล้วคุณก็พร้อมใช้งาน

---

## คำถามที่พบบ่อย

**ถาม: วิธีนี้ทำงานกับชุดข้อมูลขนาดใหญ่ (หลายพันใบแจ้งหนี้) ได้หรือไม่?**  
ตอบ: ได้. SmartMarker สตรีมข้อมูลอย่างมีประสิทธิภาพ แต่ควรตรวจสอบการใช้หน่วยความจำ หากถึงขีดจำกัดให้พิจารณาประมวลผลเป็นชุดและบันทึกแต่ละชุดเป็นเวิร์กบุ๊กแยก

**ถาม: สามารถใส่โลโก้ในทุกใบแจ้งหนี้โดยอัตโนมัติได้หรือไม่?**  
ตอบ: แน่นอน. วางรูปโลโก้บนแผ่นงานเทมเพลต เนื่องจากแผ่นงานถูกคัดลอก โลโก้จะปรากฏในแต่ละใบแจ้งหนี้โดยไม่ต้องเขียนโค้ดเพิ่มเติม

**ถาม: ถ้าต้องการป้องกันแผ่นงานต้องทำอย่างไร?**  
ตอบ: หลังจากประมวลผลแล้ว ให้วนลูปผ่าน `wb.Worksheets` และเรียก `ws.Protect(Password, ProtectionType.All)`

---

## สรุป

เราได้ **ทำการสร้างใบแจ้งหนี้อัตโนมัติ** ด้วยการใช้ฟีเจอร์ repeat‑worksheet ของ SmartMarker และรูปแบบการตั้งชื่อที่ชาญฉลาด บทเรียนนี้ครอบคลุม **วิธีตั้งชื่อ Worksheet**, แสดง **วิธีทำซ้ำ Worksheet** สำหรับแต่ละคำสั่งซื้อ, และนำเสนอ **การตั้งชื่อ Worksheet แบบไดนามิก** ที่ทำให้เวิร์กบุ๊กของคุณเป็นระเบียบและค้นหาได้ง่าย

ตั้งแต่การดึงข้อมูล, การตั้งค่าเทมเพลต, การกำหนด `SmartMarkerOptions`, จนถึงการจัดการกรณีขอบ คุณมีโซลูชันที่สมบูรณ์และรันได้แล้ว ตอนต่อไปลองเพิ่มตารางรายการสินค้า, ใช้การจัดรูปแบบตามเงื่อนไข, หรือส่งออกข้อมูลเดียวกันเป็น PDF เพื่อสร้างกระบวนการบิลลิ่งอัตโนมัติเต็มรูปแบบ

พร้อมจะก้าวต่อ? สำรวจหัวข้อที่เกี่ยวข้องเช่น “การส่งออก Excel จำนวนมากด้วย Aspose.Cells”, “การแปลง Worksheet เป็น PDF”, หรือ “การส่งใบแจ้งหนี้ที่สร้างอัตโนมัติทางอีเมลจาก C#” ความเป็นไปได้ไม่มีที่สิ้นสุด—ขอให้สนุกกับการเขียนโค้ด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}