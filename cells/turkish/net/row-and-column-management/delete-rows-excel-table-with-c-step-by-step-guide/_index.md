---
category: general
date: 2026-02-28
description: C#'ta Excel tablosundaki satırları hızlıca sil. Adlandırılmış aralık
  eklemeyi, çalışma sayfasına adla erişmeyi ve yinelenen ad hatalarından kaçınmayı
  öğrenin.
draft: false
keywords:
- delete rows excel table
- add named range excel
- access worksheet by name
- how to add defined name
- named range on another sheet
language: tr
og_description: C# kullanarak Excel tablosundaki satırları sil. Bu öğreticide ayrıca
  adlandırılmış bir aralık ekleme ve çalışma sayfasına adla erişme gösterilmektedir.
og_title: C# ile Excel Tablosundan Satırları Sil – Tam Rehber
tags:
- C#
- Excel
- DevExpress Spreadsheet
title: C# ile Excel Tablosundaki Satırları Sil – Adım Adım Rehber
url: /tr/net/row-and-column-management/delete-rows-excel-table-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile Excel Tablosundan Satır Silme – Tam Programlama Öğreticisi

Bir çalışma kitabından **delete rows excel table** işlemini yapmak istediğinizde hangi API çağrısını kullanacağınızdan emin olmadınız mı? Tek başınıza değilsiniz—çoğu geliştirici, bir tabloyu programlı olarak küçültmeye ilk kez çalıştıklarında aynı duvara çarpar.  

Bu rehberde, yalnızca bir Excel tablosundan satırları kaldırmakla kalmayıp aynı zamanda **how to add defined name** (diğer adıyla *named range*) gösteren, **access worksheet by name** ve başka bir sayfada aynı adı eklemenin neden `InvalidOperationException` hatası verdiğini gösteren tam, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz.  

Makalenin sonunda şunları yapabilecek duruma geleceksiniz:

* Sekme adını kullanarak bir çalışma sayfasını alın.  
* O sayfadaki ilk tablodan veri satırlarını güvenli bir şekilde silin.  
* Belirli bir adrese işaret eden bir adlandırılmış aralık (named range) oluşturun.  
* Farklı sayfalarda aynı adın tekrarlanmasının yol açtığı sorunları anlayın.

Harici bir dokümantasyona gerek yok—gereken her şey burada.

---

## Gereksinimler

* **DevExpress Spreadsheet** (veya `Workbook`, `Worksheet`, `ListObject` ve `Names` nesnelerini sunan herhangi bir kütüphane).  
* **.NET 6** veya daha yeni bir hedefleyen bir .NET projesi (kod .NET Framework 4.8 ile de derlenebilir).  
* C# temellerine aşina olmak—eğer bir `foreach` döngüsü yazabiliyorsanız hazırsınız.

> **Pro ipucu:** DevExpress’in ücretsiz Community Edition’ını kullanıyorsanız, aşağıda kullanılan API’ler ticari sürümle aynı işlevselliğe sahiptir.

## Step 1 – Access Worksheet by Name

İlk yapmanız gereken, değiştirmek istediğiniz tabloyu içeren sayfayı bulmaktır.  
Çoğu geliştirici alışkanlıkla `Worksheets[0]` kullanır, ancak bu yaklaşım kodunuzu sayfa sırasına bağlar ve bir sekmenin adı değiştiğinde kırılır.

```csharp
using DevExpress.Spreadsheet;

// Assume 'workbook' is an already‑loaded Workbook instance
Worksheet worksheet = workbook.Worksheets["Sheet1"];   // <-- access worksheet by name
```

*Bu neden önemlidir:* Sayfanın **adını** indeks yerine kullanarak, çalışma kitabı değiştiğinde yanlış sayfada istenmeyen değişiklikler yapma riskinden kaçınırsınız.  

Sağladığınız ad mevcut değilse, kütüphane bir `KeyNotFoundException` fırlatır; bu hatayı yakalayarak kullanıcı dostu bir hata mesajı gösterebilirsiniz.

## Step 2 – Delete Rows Excel Table (The Safe Way)

Doğru çalışma sayfasına sahip olduğumuza göre, ilk tablodan veri satırlarını kaldıralım.  
Yaygın bir hata, `DeleteRows(1, rowCount‑1)` çağrısı yapmaktır. **DevExpress 22.2** itibarıyla bu aşırı yükleme **yasaklanmıştır** ve bir `InvalidOperationException` fırlatır. Kütüphane, satırları **tablonun veri aralığı içinde** silmenizi bekler, başlık satırını değil.

```csharp
// Grab the first table (ListObject) on the sheet
var table = worksheet.ListObjects[0];

// Calculate how many data rows we actually have (excluding the header)
int dataRowCount = table.DataRange.RowCount;

// Delete only the data rows – keep the header intact
if (dataRowCount > 0)
{
    // DeleteRows(startRow, rowCount) – startRow is zero‑based within the table
    table.DeleteRows(0, dataRowCount);
}
```

> **Tablo boş olsaydı ne olur?** `if` koruması, `rowCount = 0` olduğunda bir çağrı yapılmasını engeller; aksi takdirde bir istisna ortaya çıkar.

### Görsel Genel Bakış  

![delete rows excel table örneği](image.png "Excel tablosundan satırların kaldırıldığını gösteren ekran görüntüsü")  

*Alt metin: C# kodunda delete rows excel table örneği*

## Step 3 – How to Add Defined Name (Create a Named Range)

Tabloyu temizledikten sonra, daha sonra bir grafik ya da veri doğrulama listesi için belirli bir aralığa başvurmak isteyebilirsiniz. İşte **add named range excel** burada devreye girer.

```csharp
// Define a name that points to A1:C5 on Sheet1
workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

// Verify that the name exists
Name definedName = workbook.Names["MyTable"];
Console.WriteLine($"Defined name '{definedName.Name}' points to {definedName.RefersTo}");
```

`Names.Add` yöntemi iki parametre alır: tanımlayıcı ve A1‑stili adres.  
Daha önce **access worksheet by name** kullandığımız için, adres dizesi indeks değişikliklerinden endişe duymadan herhangi bir sayfaya güvenle referans verebilir.

## Step 4 – Named Range on Another Sheet – Avoid Duplicate Name Errors

Aynı tanımlayıcıyı farklı bir sayfada tekrar kullanabileceğinizi düşünebilirsiniz, şöyle:

```csharp
// Attempt to add the same name on Sheet2 – this will throw
workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

Ne yazık ki, Excel’in adlandırma kapsamı **çalışma kitabı genelinde** olup, sayfa bazlı değildir. Yukarıdaki çağrı, *“A name with the same identifier already exists.”* mesajı ile bir `InvalidOperationException` oluşturur.  

### Çözüm Yöntemi

1. **Benzersiz bir ad seçin** (`MyTable_Sheet2`).  
2. **Mevcut adı silin** ve ardından yeniden ekleyin (yalnızca gerçekten değiştirmek istiyorsanız).  

```csharp
// Option A – use a unique name
workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");

// Option B – replace the existing name (use with caution)
if (workbook.Names.Contains("MyTable"))
    workbook.Names.Remove("MyTable");

workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

## Full, Runnable Example

Her şeyi bir araya getirerek, Visual Studio’ya bırakıp `sample.xlsx` örnek dosyası üzerinde çalıştırabileceğiniz bağımsız bir konsol uygulaması sunuyoruz.

```csharp
using System;
using DevExpress.Spreadsheet;

class Program
{
    static void Main()
    {
        // Load an existing workbook (replace with your file path)
        Workbook workbook = new Workbook();
        workbook.LoadDocument("sample.xlsx");

        // -------------------------------------------------
        // Step 1 – Access the worksheet by its tab name
        // -------------------------------------------------
        Worksheet worksheet = workbook.Worksheets["Sheet1"]; // primary sheet

        // -------------------------------------------------
        // Step 2 – Delete rows excel table (safe method)
        // -------------------------------------------------
        var table = worksheet.ListObjects[0];
        int dataRows = table.DataRange.RowCount;
        if (dataRows > 0)
            table.DeleteRows(0, dataRows); // removes only data rows

        // -------------------------------------------------
        // Step 3 – Add a defined name (named range) on Sheet1
        // -------------------------------------------------
        workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

        // -------------------------------------------------
        // Step 4 – Demonstrate duplicate‑name handling
        // -------------------------------------------------
        try
        {
            workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
        }
        catch (InvalidOperationException ex)
        {
            Console.WriteLine("Duplicate name error: " + ex.Message);
            // Use a unique identifier instead
            workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");
        }

        // Save the modified workbook
        workbook.SaveDocument("sample_modified.xlsx");
        Console.WriteLine("Workbook updated successfully.");
    }
}
```

**Beklenen sonuç**

* **Sheet1** üzerindeki ilk tablonun tüm veri satırları kaybolur, sadece başlık satırı kalır.  
* **MyTable** adı artık `Sheet1!$A$1:$C$5` adresine işaret eder.  
* İkinci ad **MyTable_Sheet2**, **Sheet2** üzerindeki bir aralığa sorunsuz şekilde referans verir ve istisna fırlatmaz.

## Common Questions & Edge Cases

| Soru | Cevap |
|----------|--------|
| *Çalışma kitabında birden fazla tablo varsa ne yapılmalı?* | Doğru `ListObject`i indeks (`worksheet.ListObjects[1]`) ya da ad (`worksheet.ListObjects["MyTable"]`) ile alın. |
| *Bir tablo birden fazla çalışma sayfasına yayılmışsa satırları silebilir miyim?* | Hayır—tablolar tek bir sayfaya sınırlıdır. Silme mantığını her sayfa için tekrarlamanız gerekir. |
| *Sadece belirli bir satır alt kümesini silmek mümkün mü?* | Evet—`table.DeleteRows(startRow, count)` kullanın; `startRow` tablonun veri alanı içinde sıfır‑tabanlıdır. |
| *Kaydedildikten sonra adlandırılmış aralıklar korunur mu?* | Kesinlikle. `SaveDocument` çağrısı yapıldığında, adlar çalışma kitabının XML’ine eklenir. |
| *Çalışma kitabındaki tüm tanımlı adları nasıl listeleyebilirim?* | `foreach (var name in workbook.Names) Console.WriteLine(name.Name);` döngüsüyle gezinin. |

## Conclusion

**delete rows excel table** işlemini C# ile nasıl yapacağınızı, **add named range excel** kullanımını ve **access worksheet by name** yöntemini, tekrarlanan ad hatasından kaçınarak gösterdik.  

Tam çözüm yukarıdaki kod snippet’inde yer alıyor—kopyalayıp yapıştırın ve kendi dosyalarınızda çalıştırın. Buradan, birden fazla tabloyu işleme, dinamik aralık hesaplamaları ekleme ya da bir UI ile bütünleştirme gibi mantığı genişletebilirsiniz.

**İleri adımlar** olarak şunları keşfedebilirsiniz:

* **named range on another sheet** kullanarak grafik serilerini besleyin.  
* Silme mantığını **ExcelDataReader** ile birleştirerek temizlemeden önce veri içe aktarın.  
* Basit bir `foreach (var file in Directory.GetFiles(...))` döngüsüyle onlarca çalışma kitabında toplu güncellemeler otomatikleştirin.

C#’ta Excel otomasyonu hakkında daha fazla sorunuz mu var? Bir yorum bırakın, sohbeti sürdürelim. Mutlu kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}