---
category: general
date: 2026-07-13
description: C# ile Excel Çalışma Kitabı oluşturun ve adlandırılmış aralık eklemeyi,
  tabloya isim atamayı ve adlandırma çakışmalarını nasıl yöneteceğinizi tek bir net
  örnekle öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- add named range
- assign name to table
- set table name
- how to add range
language: tr
lastmod: 2026-07-13
og_description: Aspose.Cells ile C#'ta Excel Çalışma Kitabı Oluşturun. Adlandırılmış
  aralık eklemeyi, tablo adını ayarlamayı ve adlandırma çakışmalarını çözmeyi kısa
  ve çalıştırılabilir bir rehberde öğrenin.
og_image_alt: Screenshot showing an Excel workbook with a named range and a table
  name set using C# code
og_title: C# ile Excel Çalışma Kitabı Oluştur – Adlandırılmış Aralık Ekle ve Tablo
  Adını Belirle
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Create Excel Workbook in C# and learn how to add named range, assign
    name to table, and handle naming conflicts—all in one clear example.
  headline: Create Excel Workbook in C# – Add Named Range & Set Table Name
  type: TechArticle
- description: Create Excel Workbook in C# and learn how to add named range, assign
    name to table, and handle naming conflicts—all in one clear example.
  name: Create Excel Workbook in C# – Add Named Range & Set Table Name
  steps:
  - name: '**Use a consistent prefix** (`tbl_`, `rng_`, etc.) – it instantly tells
      you what the object is.'
    text: '**Use a consistent prefix** (`tbl_`, `rng_`, etc.) – it instantly tells
      you what the object is.'
  - name: '**Stay within 255 characters** – Excel’s limit for names.'
    text: '**Stay within 255 characters** – Excel’s limit for names.'
  - name: '**Avoid spaces and special characters** – only letters, numbers, and underscores
      are safe.'
    text: '**Avoid spaces and special characters** – only letters, numbers, and underscores
      are safe.'
  - name: '**Validate before assigning** – a quick `if (!sheet.Names.Contains(name))`
      check prevents the clash we demonstrated.'
    text: '**Validate before assigning** – a quick `if (!sheet.Names.Contains(name))`
      check prevents the clash we demonstrated.'
  type: HowTo
- questions:
  - answer: Yes, but you must qualify the address with the sheet name, e.g., `"Sheet1!A1:B5"`.
      The `Names.Add` method accepts that format.
    question: Can I add a named range that spans multiple worksheets?
  - answer: Absolutely. You can pass a formula string instead of a static address,
      such as `"=OFFSET(Sheet1!$A$1,0,0,COUNT(Sheet1!$A:$A),2)"`.
    question: Does Aspose.Cells support dynamic named ranges (like OFFSET formulas)?
  - answer: 'Just set `table.Name = " ## What Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
      - [How to Implement a Named Range with Workbook Scope in Aspose.Cells Java for
      Enhanced Excel Data Management](/cells/english/java/tables-structured-references/implement-named-range-workbook-scope-aspose-cells-java/)
      - [Excel Automation&#58; Create a Workbook and Add a ListBox Using Aspose.Cells
      for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
    question: What if I need to rename an existing table?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- Excel Automation
- .NET
title: C# ile Excel Çalışma Kitabı Oluştur – Adlandırılmış Aralık Ekle ve Tablo Adını
  Belirle
url: /tr/net/excel-advanced-named-ranges/create-excel-workbook-in-c-add-named-range-set-table-name/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile Excel Çalışma Kitabı Oluşturma – Adlandırılmış Aralıklar Eklemek ve Tablo İsimlerini Ayarlamak İçin Tam Kılavuz

Sıfırdan **Excel çalışma kitabı** oluşturmanız gerektiğinde ve bir adlandırılmış aralığı nereye koyacağınızı ya da bir tabloya kendi tanımlayıcısını nasıl vereceğinizi merak ettiğiniz oldu mu? Tek başınıza değilsiniz. Birçok raporlama veya veri‑dışa aktarma senaryosunda, aralıklar, tablolar ve zaman zaman ortaya çıkan adlandırma çakışmalarıyla uğraşacağınızı göreceksiniz.  

Bu öğreticide **Excel çalışma kitabı** oluşturan, **adlandırılmış bir aralık** ekleyen ve ardından **bir tabloya isim atayan** tam çalıştırılabilir bir örnek üzerinden ilerleyeceğiz—isimler çakıştığında tam olarak ne yapmanız gerektiğini göstereceğiz. Sonunda her adımın “nasıl” ve “neden”ini öğrenecek, kodunuzu temiz tutmak için birkaç ipucu da edineceksiniz.

> **Hızlı kazanç:** Kod, **Aspose.Cells** kütüphanesini kullanır; .NET 6+ ile çalışır ve sunucuda Excel kurulumu gerektirmez.

---

## What You’ll Need

- **.NET 6 SDK** (veya herhangi bir yeni .NET sürümü)  
- **Aspose.Cells for .NET** NuGet paketi  
- İyi bir IDE (Visual Studio, Rider veya VS Code)  
- Temel C# bilgisi—fancy bir şey yok, sadece standart `using` ifadeleri

Bu gereksinimlere sahipseniz, **create excel workbook** sürecine doğrudan atlayabiliriz.

---

## ## Create Excel Workbook – Step‑by‑Step Overview

Aşağıda tamamen kopyala‑yapıştır‑hazır program yer alıyor. Çalışma kitabı oluşturulmasından **tabloya isim atama** sırasında oluşabilecek adlandırma çakışmasının nasıl ele alınacağını gösteriyor.

```csharp
using System;
using Aspose.Cells;

namespace ExcelNamingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook
            Workbook workbook = new Workbook();

            // Step 2: Add some sample data so we have a table to work with
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells["A1"].PutValue("Product");
            sheet.Cells["B1"].PutValue("Price");
            sheet.Cells["A2"].PutValue("Apple");
            sheet.Cells["B2"].PutValue(0.99);
            sheet.Cells["A3"].PutValue("Banana");
            sheet.Cells["B3"].PutValue(0.59);
            sheet.Cells["A4"].PutValue("Cherry");
            sheet.Cells["B4"].PutValue(2.99);
            sheet.Cells["A5"].PutValue("Date");
            sheet.Cells["B5"].PutValue(3.49);

            // Step 3: Convert the data range into a table (default name Table1)
            int tableIndex = sheet.Tables.Add(sheet.Cells.CreateRange("A1:B5"), true);
            ListObject table = sheet.Tables[tableIndex];
            // At this point the table name is "Table1"

            // Step 4: Add a named range that covers the same cells
            // This is the "add named range" part of the tutorial
            sheet.Names.Add("MyRange", "A1:B5");

            // Step 5: Try to give the table the same name – this will cause a conflict
            try
            {
                table.Name = "MyRange"; // <-- assign name to table
            }
            catch (Exception ex)
            {
                // Step 6: Handle the naming conflict by outputting the error message
                Console.WriteLine("Naming conflict detected:");
                Console.WriteLine(ex.Message);
            }

            // Optional: Save the workbook to verify everything works
            workbook.Save("DemoWorkbook.xlsx");
        }
    }
}
```

**Beklenen çıktı** programı çalıştırdığınızda:

```
Naming conflict detected:
A name with the same text already exists.
```

Ve *DemoWorkbook.xlsx* dosyasını açtığınızda **Table1** adlı bir tablo ve **MyRange** adlı bir adlandırılmış aralık göreceksiniz—tam da istediğimiz gibi, çakışma olmadan.

---

## ## Add Named Range – Why It Matters

Bir **named range**, temelde bir hücre bloğu için bir takma addır. Sürekli `A1:B5` yazmak yerine formüllerde, veri doğrulamalarda ya da kod içinde `MyRange` yazabilirsiniz. Bu, okunabilirliği artırır ve yazım hatalarından kaynaklanan hataları azaltır.

Yukarıdaki snippet'te şu kodu çağırıyoruz:

```csharp
sheet.Names.Add("MyRange", "A1:B5");
```

- İlk argüman, daha sonra kullanacağınız **name** (isim) dir.  
- İkinci argüman ise **address** (adres) dir (çalışma sayfasına göre göreceli).

Eğer **how to add range** dinamik olarak eklemeniz gerekirse, adres dizesini `Cell.GetRefersTo()` ile oluşturabilir ya da `Range refRange = sheet.Cells.CreateRange(startRow, startCol, totalRows, totalCols)` kullanabilirsiniz.

---

## ## Assign Name to Table – Handling Conflicts

Tablolar (aynı zamanda *list objects* olarak da adlandırılır) zaten yerleşik bir name (isim) özelliğine sahiptir. Varsayılan olarak Aspose.Cells, onları `Table1`, `Table2` vb. olarak adlandırır. Bir tabloya mevcut bir adlandırılmış aralıkla aynı tanımlayıcıyı vermeye çalıştığınızda, kütüphane bir istisna fırlatır—tıpkı Excel'in yaptığı gibi.

Bu neden olur?

- Excel’in adlandırma kapsamı, hem aralıklar hem de tablolar için **workbook‑wide** (çalışma kitabı genelinde) geçerlidir.  
- Çift isimler formülleri belirsiz kılar, bu yüzden motor çakışmayı engeller.

### Pro tip

Bir tablonun bir aralıkla aynı mantıksal ismi paylaşması gerçekten gerekiyorsa, bunlardan birine **prefix** (ön ek) eklemeyi düşünün, örneğin:

```csharp
table.Name = "tbl_MyRange";   // safe, no conflict
```

Veya önce aralığın ismini değiştirin:

```csharp
sheet.Names["MyRange"].Name = "DataRange";
```

Her iki yaklaşım da ad alanını düzenli tutar ve çalışma zamanı hatalarını önler.

---

## ## Set Table Name – Best Practices

Programatik olarak **set table name** (tablo ismi ayarlama) yaparken şu yönergeleri aklınızda bulundurun:

1. **Tutarlı bir ön ek kullanın** (`tbl_`, `rng_` vb.) – nesnenin ne olduğunu anında gösterir.  
2. **255 karakteri aşmayın** – Excel’in isim uzunluğu sınırı budur.  
3. **Boşluk ve özel karakterlerden kaçının** – sadece harf, sayı ve alt çizgi güvenlidir.  
4. **Atamadan önce doğrulayın** – `if (!sheet.Names.Contains(name))` gibi basit bir kontrol, gösterdiğimiz çakışmayı önler.

İşte herhangi bir projeye ekleyebileceğiniz yardımcı bir metod:

```csharp
static void SafeSetTableName(Worksheet sheet, ListObject table, string desiredName)
{
    string finalName = desiredName;
    int suffix = 1;
    while (sheet.Names.Contains(finalName) || sheet.Tables.Contains(finalName))
    {
        finalName = $"{desiredName}_{suffix}";
        suffix++;
    }
    table.Name = finalName;
}
```

`SafeSetTableName(sheet, table, "MyRange")` çağrısı, bir çakışma varsa `MyRange` değerini otomatik olarak `MyRange_1` yapar ve **create excel workbook** işleminin beklenmedik bir şekilde durmasını engeller.

---

## ## Full Working Example – Putting It All Together

Aşağıda, bir console uygulamasına doğrudan kopyalayabileceğiniz kompakt bir sürüm bulunuyor. Güvenlik rutinini içerir ve uçtan uca akışı gösterir.

```csharp
using System;
using Aspose.Cells;

namespace ExcelNamingDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the workbook
            Workbook wb = new Workbook();
            Worksheet ws = wb.Worksheets[0];

            // Populate a simple dataset
            ws.Cells["A1"].PutValue("Item");
            ws.Cells["B1"].PutValue("Quantity");
            ws.Cells["A2"].PutValue("Pen");
            ws.Cells["B2"].PutValue(10);
            ws.Cells["A3"].PutValue("Notebook");
            ws.Cells["B3"].PutValue(5);

            // Turn data into a table
            int tblIdx = ws.Tables.Add(ws.Cells.CreateRange("A1:B3"), true);
            ListObject tbl = ws.Tables[tblIdx];

            // Add a named range covering the same cells
            ws.Names.Add("MyRange", "A1:B3");

            // Safely assign a name to the table
            SafeSetTableName(ws, tbl, "MyRange");

            // Save to verify
            wb.Save("FinalDemo.xlsx");
            Console.WriteLine($"Table name set to: {tbl.Name}");
        }

        static void SafeSetTableName(Worksheet sheet, ListObject table, string desiredName)
        {
            string candidate = desiredName;
            int i = 1;
            while (sheet.Names.Contains(candidate) || sheet.Tables.Contains(candidate))
            {
                candidate = $"{desiredName}_{i}";
                i++;
            }
            table.Name = candidate;
        }
    }
}
```

Bu betiği çalıştırdığınızda `FinalDemo.xlsx` oluşturulur; tabloda `MyRange_1` (veya başka bir benzersiz ek) adı bulunur, aralık ise `MyRange` olarak kalır. İstisna yok, gizem yok—sadece temiz, deterministik adlandırma.

---

## ## Frequently Asked Questions (FAQ)

**S: Birden fazla çalışma sayfasını kapsayan bir adlandırılmış aralık ekleyebilir miyim?**  
C: Evet, ancak adresi sayfa adıyla nitelendirmeniz gerekir, örneğin `"Sheet1!A1:B5"`. `Names.Add` metodu bu formatı kabul eder.

**S: Aspose.Cells dinamik adlandırılmış aralıkları (OFFSET formülleri gibi) destekliyor mu?**  
C: Kesinlikle. Statik bir adres yerine bir formül dizesi geçirebilirsiniz; örnek: `"=OFFSET(Sheet1!$A$1,0,0,COUNT(Sheet1!$A:$A),2)"`.

**S: Mevcut bir tabloyu yeniden adlandırmam gerekirse ne yapmalıyım?**  
C: Sadece `table.Name = "

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}