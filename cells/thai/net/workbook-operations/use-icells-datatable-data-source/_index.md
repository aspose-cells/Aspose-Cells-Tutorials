---
title: ใช้ ICellsDataTableDataSource สำหรับ Workbook Designer
linktitle: ใช้ ICellsDataTableDataSource สำหรับ Workbook Designer
second_title: API การประมวลผล Excel ของ Aspose.Cells .NET
description: เรียนรู้การใช้ ICellsDataTableDataSource กับ Aspose.Cells สำหรับ .NET เพื่อเติมข้อมูลในแผ่นงาน Excel แบบไดนามิก เหมาะอย่างยิ่งสำหรับการทำให้ข้อมูลลูกค้าในสมุดงานเป็นแบบอัตโนมัติ
weight: 21
url: /th/net/workbook-operations/use-icells-datatable-data-source/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ใช้ ICellsDataTableDataSource สำหรับ Workbook Designer

## การแนะนำ
 การสร้างสเปรดชีตขั้นสูงพร้อมการรวมข้อมูลอัตโนมัติสามารถเปลี่ยนแปลงเกมได้ โดยเฉพาะในแอปพลิเคชันทางธุรกิจ ในบทช่วยสอนนี้ เราจะเจาะลึกวิธีใช้`ICellsDataTableDataSource`สำหรับนักออกแบบเวิร์กบุ๊กใน Aspose.Cells สำหรับ .NET เราจะแนะนำคุณเกี่ยวกับการสร้างโซลูชันที่เรียบง่ายและอ่านได้โดยมนุษย์เพื่อโหลดข้อมูลที่กำหนดเองลงในไฟล์ Excel แบบไดนามิก ดังนั้น หากคุณกำลังทำงานกับรายชื่อลูกค้า ข้อมูลการขาย หรือสิ่งที่คล้ายกัน คู่มือนี้เหมาะสำหรับคุณ!
## ข้อกำหนดเบื้องต้น
ในการเริ่มต้น ตรวจสอบให้แน่ใจว่าคุณมีสิ่งต่อไปนี้:
-  Aspose.Cells สำหรับไลบรารี .NET – คุณสามารถดาวน์โหลดได้จาก[ที่นี่](https://releases.aspose.com/cells/net/) หรือรับเวอร์ชันทดลองใช้งานฟรี
- สภาพแวดล้อมการพัฒนา .NET – Visual Studio เป็นตัวเลือกที่ยอดเยี่ยม
- ความเข้าใจพื้นฐานเกี่ยวกับ C# – ความคุ้นเคยกับคลาสและการจัดการข้อมูลจะช่วยให้คุณทำตามได้
ก่อนที่เราจะดำเนินการต่อ โปรดตรวจสอบให้แน่ใจว่าสภาพแวดล้อมการพัฒนาของคุณได้รับการตั้งค่าด้วยแพ็คเกจที่จำเป็น
## แพ็คเกจนำเข้า
หากต้องการใช้ Aspose.Cells อย่างมีประสิทธิภาพ คุณจำเป็นต้องนำเข้าแพ็คเกจที่จำเป็น ด้านล่างนี้เป็นข้อมูลอ้างอิงด่วนสำหรับเนมสเปซที่จำเป็น:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
using System.Collections;
```
## ขั้นตอนที่ 1: กำหนดคลาสข้อมูลลูกค้า
 ในการเริ่มต้น ให้สร้างสิ่งง่ายๆ`Customer` ชั้นเรียน ชั้นเรียนนี้จะมีรายละเอียดพื้นฐานของลูกค้า เช่น`FullName` และ`Address`ลองคิดดูว่าเป็นวิธีในการกำหนด "รูปร่าง" ของข้อมูลของคุณ
```csharp
public class Customer
{
    public Customer(string aFullName, string anAddress)
    {
        FullName = aFullName;
        Address = anAddress;
    }
    public string FullName { get; set; }
    public string Address { get; set; }
}
```
## ขั้นตอนที่ 2: ตั้งค่าคลาสรายชื่อลูกค้า
 ถัดไป ให้กำหนด`CustomerList` ชั้นเรียนที่ขยาย`ArrayList` รายการที่กำหนดเองนี้จะมีอินสแตนซ์ของ`Customer` และอนุญาติให้เข้าถึงรายการแต่ละรายการได้
```csharp
public class CustomerList : ArrayList
{
    public new Customer this[int index]
    {
        get { return (Customer)base[index]; }
        set { base[index] = value; }
    }
}
```
ในขั้นตอนนี้ เราจะห่อข้อมูลของเราในรูปแบบที่ Aspose.Cells สามารถจดจำและประมวลผลได้
## ขั้นตอนที่ 3: สร้างคลาสแหล่งข้อมูลลูกค้า
 นี่คือจุดที่สิ่งต่างๆ เริ่มน่าสนใจ เราจะสร้าง`CustomerDataSource` การดำเนินการชั้นเรียน`ICellsDataTable` เพื่อทำให้ข้อมูลของเรามีความเข้ากันได้กับโปรแกรมออกแบบเวิร์กบุ๊ก Aspose.Cells
```csharp
public class CustomerDataSource : ICellsDataTable
{
    internal string[] m_Columns;
    internal ICollection m_DataSource;
    private Hashtable m_PropHash;
    private IEnumerator m_IEnumerator;
    private PropertyInfo[] m_Properties;
    public CustomerDataSource(CustomerList customers)
    {
        this.m_DataSource = customers;
        this.m_Properties = customers[0].GetType().GetProperties();
        this.m_Columns = new string[this.m_Properties.Length];
        this.m_PropHash = new Hashtable(this.m_Properties.Length);
        for (int i = 0; i < m_Properties.Length; i++)
        {
            this.m_Columns[i] = m_Properties[i].Name;
            this.m_PropHash.Add(m_Properties[i].Name, m_Properties[i]);
        }
        this.m_IEnumerator = this.m_DataSource.GetEnumerator();
    }
    public string[] Columns => this.m_Columns;
    public int Count => this.m_DataSource.Count;
    public void BeforeFirst()
    {
        this.m_IEnumerator = this.m_DataSource.GetEnumerator();
    }
    public object this[int index] => this.m_Properties[index].GetValue(this.m_IEnumerator.Current, null);
    public object this[string columnName] => ((PropertyInfo)this.m_PropHash[columnName]).GetValue(this.m_IEnumerator.Current, null);
    public bool Next()
    {
        if (this.m_IEnumerator == null)
            return false;
        return this.m_IEnumerator.MoveNext();
    }
}
```
 ธรรมเนียมนี้`CustomerDataSource` คลาสทำให้ Aspose.Cells สามารถตีความแต่ละอันได้`Customer` วัตถุเป็นแถวในไฟล์ Excel
## ขั้นตอนที่ 4: เริ่มต้นข้อมูลลูกค้า
ตอนนี้เรามาเพิ่มลูกค้าเข้าในรายชื่อของเรากัน นี่คือที่ที่เราโหลดข้อมูลเพื่อเขียนลงในเวิร์กบุ๊ก คุณสามารถเพิ่มรายการอื่นๆ ได้ตามต้องการ
```csharp
CustomerList customers = new CustomerList();
customers.Add(new Customer("Thomas Hardy", "120 Hanover Sq., London"));
customers.Add(new Customer("Paolo Accorti", "Via Monte Bianco 34, Torino"));
```
ในตัวอย่างนี้ เรากำลังทำงานกับชุดข้อมูลขนาดเล็ก อย่างไรก็ตาม คุณสามารถขยายรายการนี้ได้อย่างง่ายดายโดยโหลดข้อมูลจากฐานข้อมูลหรือแหล่งอื่น
## ขั้นตอนที่ 5: โหลดเวิร์กบุ๊ก
ตอนนี้เรามาเปิดเวิร์กบุ๊ก Excel ที่มีอยู่ซึ่งมี Smart Markers ที่จำเป็น เวิร์กบุ๊กนี้จะทำหน้าที่เป็นเทมเพลตของเรา และ Aspose.Cells จะแทนที่ Smart Markers ด้วยข้อมูลลูกค้าแบบไดนามิก
```csharp
string sourceDir = "Your Document Directory";
Workbook workbook = new Workbook(sourceDir + "SmartMarker1.xlsx");
```
 ให้แน่ใจว่า`"SmartMarker1.xlsx"` มีตัวแทนเช่น`&=Customer.FullName` และ`&=Customer.Address` ซึ่งจะต้องกรอกข้อมูลลงไป
## ขั้นตอนที่ 6: ตั้งค่าตัวออกแบบเวิร์กบุ๊ก
ตอนนี้ มากำหนดค่าตัวออกแบบเวิร์กบุ๊กเพื่อเชื่อมโยงแหล่งข้อมูลลูกค้าของเรากับ Smart Markers ของเวิร์กบุ๊กกัน
```csharp
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.SetDataSource("Customer", new CustomerDataSource(customers));
```
 การ`SetDataSource` วิธีการผูกมัดของเรา`CustomerDataSource` ไปที่มาร์กเกอร์อัจฉริยะในสมุดงาน มาร์กเกอร์แต่ละตัวมีป้ายกำกับ`&=Customer` ใน Excel จะถูกแทนที่ด้วยข้อมูลลูกค้าที่สอดคล้องกัน
## ขั้นตอนที่ 7: ประมวลผลและบันทึกสมุดงาน
สุดท้ายเรามาประมวลผลสมุดงานเพื่อกรอกข้อมูลและบันทึกผลลัพธ์
```csharp
string outputDir = "Your Document Directory";
designer.Process();
workbook.Save(outputDir + "dest.xlsx");
```
โค้ดนี้จะกระตุ้นการประมวลผล Smart Marker แทนที่ตัวแทนทั้งหมดด้วยข้อมูล และบันทึกผลลัพธ์เป็น`dest.xlsx`.
## บทสรุป
 ขอแสดงความยินดี! คุณได้ดำเนินการสำเร็จแล้ว`ICellsDataTableDataSource` สำหรับนักออกแบบเวิร์กบุ๊กที่ใช้ Aspose.Cells สำหรับ .NET แนวทางนี้เหมาะอย่างยิ่งสำหรับการสร้างข้อมูลอัตโนมัติในสเปรดชีต โดยเฉพาะอย่างยิ่งเมื่อต้องจัดการกับข้อมูลแบบไดนามิก เช่น รายชื่อลูกค้าหรือสินค้าคงคลัง ด้วยทักษะเหล่านี้ คุณก็พร้อมที่จะสร้างแอปพลิเคชันที่ขับเคลื่อนด้วยข้อมูลซึ่งทำให้การรายงานที่ใช้ Excel เป็นเรื่องง่าย!
## คำถามที่พบบ่อย
###  อะไรคือ`ICellsDataTable` in Aspose.Cells?  
เป็นอินเทอร์เฟซที่อนุญาตให้เชื่อมโยงแหล่งข้อมูลที่กำหนดเองกับ Aspose.Cells Smart Markers เพื่อการเติมข้อมูลแบบไดนามิก
### ฉันจะปรับแต่งข้อมูลในเทมเพลตเวิร์กบุ๊กได้อย่างไร  
 ตัวแทนที่เรียกว่า Smart Markers เช่น`&=Customer.FullName`ถูกนำมาใช้ เครื่องหมายเหล่านี้จะถูกแทนที่ด้วยข้อมูลจริงในระหว่างการประมวลผล
### Aspose.Cells สำหรับ .NET ฟรีหรือไม่?  
 Aspose.Cells นำเสนอการทดลองใช้ฟรี แต่การเข้าใช้งานแบบเต็มรูปแบบต้องมีใบอนุญาตแบบชำระเงิน ตรวจสอบ[ทดลองใช้งานฟรี](https://releases.aspose.com/) หรือ[ซื้อ](https://purchase.aspose.com/buy) ตัวเลือก
### ฉันสามารถเพิ่มข้อมูลลูกค้าเพิ่มเติมแบบไดนามิกได้หรือไม่  
 แน่นอน! เพียงกรอก`CustomerList`พร้อมรายการเพิ่มเติมก่อนการรันโปรแกรม
### ฉันจะได้รับความช่วยเหลือหากติดขัดได้ที่ไหน?  
 แอสโพเซ่มี[ฟอรั่มสนับสนุน](https://forum.aspose.com/c/cells/9) โดยผู้ใช้สามารถถามคำถามและรับความช่วยเหลือจากชุมชนและทีมงาน Aspose ได้
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
