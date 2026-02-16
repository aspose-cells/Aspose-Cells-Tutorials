---
category: general
date: 2026-02-15
description: WRAPCOLS'i kullanarak iki sütunlu bir düzen oluşturma, bir formül ekleme
  ve C# çalışma sayfalarında bir dizi oluşturma – adım adım rehber.
draft: false
keywords:
- how to use wrapcols
- create two column layout
- how to add formula
- how to create columns
- generate sequence array
language: tr
og_description: WRAPCOLS'i kullanarak iki sütunlu bir düzen oluşturma, formüller ekleme
  ve C# çalışma sayfasında bir dizi oluşturma – kapsamlı rehber.
og_title: 'WRAPCOLS Nasıl Kullanılır: C#''ta İki Sütunlu Düzen'
tags:
- CSharp
- ExcelAutomation
- WorksheetFormula
title: 'WRAPCOLS Nasıl Kullanılır: C#''ta İki Sütunlu Düzen Oluşturma'
url: /tr/net/row-and-column-management/how-to-use-wrapcols-create-a-two-column-layout-in-c/
---

produce final output with all translated content.

Check for any URLs: none.

Check for any file paths: WrapColsDemo.xlsx is a filename; we should not translate that. We kept it unchanged.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# WRAPCOLS Nasıl Kullanılır: C#'ta İki Sütunlu Düzen Oluşturma

Ever wondered **how to use WRAPCOLS** when you need a quick two‑column view inside an Excel‑style worksheet? You’re not alone. Many developers hit a wall when they try to split a generated list into neat columns without writing a loop for each cell. The good news? With the `WRAPCOLS` function you can drop a single formula into `A1` and let Excel (or a compatible engine) do the heavy lifting.

Bu öğreticide, **how to add formula** ile **create two column layout** oluşturan, **how to create columns** dinamik olarak gösteren ve hatta **generate sequence array** değerlerini anında üreten bir süreci adım adım anlatacağız. Sonunda, projenize yapıştırıp çalıştırabileceğiniz ve anında düzenli bir iki sütunlu blok görebileceğiniz tamamen çalışabilir bir C# kod parçacığına sahip olacaksınız.

## Öğrenecekleriniz

- `WRAPCOLS`'un amacı ve neden manuel döngüye göre daha iyi bir alternatif olduğu.  
- C# kullanarak bir çalışma sayfası hücresine **add a formula** ekleme.  
- `SEQUENCE` ile bir dizi dizisi (sequence array) oluşturma ve bunu `WRAPCOLS` içine besleme.  
- Formülün hemen çözülmesi için sayfayı yeniden hesaplama ipuçları.  
- Köşe‑durum (edge‑case) yönetimi (ör. boş çalışma sayfaları, özel sütun sayıları).

Standart bir Excel işleme paketi dışındaki harici kütüphanelere ihtiyaç yok – **ClosedXML**'i basit API'si nedeniyle kullanacağız, ancak kavramlar EPPlus, SpreadsheetGear veya hatta Google Sheets'in API'si üzerinden de geçerlidir.

---

## Önkoşullar

- .NET 6.0 veya daha yenisi (kod .NET Core ve .NET Framework üzerinde derlenir).  
- **ClosedXML** referansı (`dotnet add package ClosedXML`).  
- Temel C# bilgisi – `using` ifadeleri ve nesne başlatma konusunda rahat olmalısınız.  

Zaten açık bir çalışma kitabınız varsa, dosya oluşturma kısmını atlayabilir ve doğrudan formül bölümüne geçebilirsiniz.

## Adım 1: Çalışma Sayfasını Hazırlama (Sütunları Nasıl Oluşturursunuz)

İlk olarak, üzerinde çalışacağımız bir `Worksheet` nesnesine ihtiyacımız var. ClosedXML'de bu nesneyi bir `XLWorkbook`'tan elde edersiniz. Aşağıdaki kod parçacığı yeni bir çalışma kitabı oluşturur, *Demo* adlı bir sayfa ekler ve açıklık sağlamak için `worksheet` adında bir referans alır.

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // Create a fresh workbook and add a worksheet named "Demo"
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");

            // Rename for clarity – this is the worksheet we’ll manipulate
            var worksheet = ws;   // <-- same object, just a clearer name

            // --------------------------------------------------------------
            // Next step: write the WRAPCOLS formula
            // --------------------------------------------------------------
```

> **Neden yeniden adlandırılıyor?**  
> Değişken adını kısa tutmak (`worksheet`) sonraki kodun okunmasını kolaylaştırır, özellikle birden fazla işlemi zincirlediğinizde. Ayrıca çoğu belgede gördüğünüz adlandırma stilini yansıtarak zihinsel yükü azaltır.

## Adım 2: Formülü Yazma (Formül Ekleme + Dizi Dizisi Oluşturma)

Şimdi sihirli satır geliyor. **A1** hücresine iki şey yapan bir formül yerleştireceğiz:

1. **Generate a sequence array** altı sayıdan oluşan bir dizi (`SEQUENCE(6)` → 1,2,3,4,5,6).  
2. **Wrap those numbers into two columns** (`WRAPCOLS(..., 2)`) iki sütuna sarar.

```csharp
            // Write the WRAPCOLS formula into A1
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // --------------------------------------------------------------
            // Finally, force the engine to evaluate the formula
            // --------------------------------------------------------------
```

> **Ne oluyor?**  
> `SEQUENCE(6)` dikey bir dizi `{1;2;3;4;5;6}` oluşturur. `WRAPCOLS` bu diziyi alıp belirtilen sütun sayısına “sarar”—bu örnekte **2**. Sonuç, şu şekilde görünen 3‑satır × 2‑sütunluk bir bloktur:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

İkinci argümanı **3** olarak değiştirirseniz, bunun yerine üç sütunlu bir düzen elde edersiniz. Bu, manuel döngüler olmadan **how to create columns** dinamik olarak oluşturmanın özüdür.

## Adım 3: Çalışma Sayfasını Yeniden Hesaplama (Formülün Değerlendirildiğinden Emin Olma)

ClosedXML, formülleri yazdığınızda otomatik olarak değerlendirmez. Değerlendirmeyi zorlamak için çalışma kitabı (veya belirli çalışma sayfası) üzerinde `Calculate()` çağırmanız gerekir.

```csharp
            // Recalculate so the formula is evaluated immediately
            worksheet.Calculate();

            // Optional: save the workbook to inspect the result
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

> **Pro tip:** Büyük çalışma kitaplarıyla çalışıyorsanız, yalnızca gerçekten değişen sayfalarda `Calculate()` çağırın. Bu bellek tasarrufu sağlar ve işleme hızını artırır.

`WrapColsDemo.xlsx` dosyasını açtığınızda iki sütunlu düzenin **A1:B3** içinde düzgün bir şekilde doldurulduğunu göreceksiniz. Satır veya sütunlar arasında döngü oluşturmak için ek bir koda gerek yok – `WRAPCOLS` her şeyi halletti.

## Adım 4: Çıktıyı Doğrulama (Ne Beklenir)

Programı çalıştırdıktan sonra oluşturulan dosyayı açın. Şu şekilde görmelisiniz:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

Sayılar dikey olarak (yani tümü A sütununda) görünüyorsa, formülü ayarladıktan **sonra** `worksheet.Calculate()` çağırdığınızdan emin olun. Bazı motorlar ayrıca `workbook.Calculate()` gerektirebilir; yukarıdaki kod parçacığı ClosedXML'in yerleşik değerlendiricisi için çalışır.

## Yaygın Varyasyonlar ve Kenar Durumları

### Sütun Sayısını Değiştirme

**create two column layout** farklı satır sayısıyla oluşturmak için, sadece `SEQUENCE` boyutunu veya `WRAPCOLS`'in ikinci argümanını ayarlayın:

```csharp
worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(12), 3)";
```

### Dinamik Sütun Sayısı Kullanma

Sütun sayısı bir değişkenden geliyorsa, dize yerleştirme (string interpolation) ile gömün:

```csharp
int colCount = 4;
worksheet.Cell("A1").FormulaA1 = $"=WRAPCOLS(SEQUENCE(8), {colCount})";
```

Artık çalışma zamanında uyum sağlayan **how to add formula**'a sahipsiniz.

### Boş Çalışma Sayfaları

Çalışma sayfası boşsa, `Calculate()` yine de çalışır – formül A1'den başlayarak hücreleri doldurur. Ancak, daha sonra çıktı aralığıyla kesişen satırları/sütunları silerseniz `#REF!` hataları görebilirsiniz. Bunu önlemek için önce hedef aralığı temizleyin:

```csharp
worksheet.Range("A1:Z100").Clear(); // wipes any leftovers
```

### Uyumluluk

`WRAPCOLS` ve `SEQUENCE`, Office 365'te tanıtılan Excel'in **Dynamic Array** fonksiyonlarının bir parçasıdır. Daha eski Excel sürümlerini hedefliyorsanız, bu fonksiyonlar mevcut olmayacak ve manuel bir döngüye ihtiyaç duyacaksınız. ClosedXML'in değerlendiricisi en yeni Excel davranışını yansıttığı için modern ortamlar için güvenlidir.

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook & worksheet
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");
            var worksheet = ws;   // clearer name

            // 2️⃣ Write WRAPCOLS formula that generates a sequence array
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // 3️⃣ Force calculation so the formula resolves immediately
            worksheet.Calculate();

            // 4️⃣ Save the file (optional, but handy for verification)
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

**Beklenen sonuç:** *WrapColsDemo.xlsx* dosyasını açtığınızda, daha önce açıklanan şekilde 1‑6 sayılarını içeren düzenli bir iki sütunlu düzen görürsünüz.

## Sonuç

**how to use WRAPCOLS** ile **create a two column layout** oluşturmayı ele aldık, programlı olarak **how to add formula** gösterdik ve `SEQUENCE`'in döngü olmadan **generate sequence array** değerleri üretmenizi sağladığını gördük. Excel'in dinamik dizi fonksiyonlarını C#'tan kullanarak kodunuzu öz, okunabilir ve sürdürülebilir tutabilirsiniz.

Sonraki adımda şunları keşfedebilirsiniz:

- `ROWS` veya `COUNTA` ile **dynamic row counts** oluşturma.  
- ClosedXML'in stil API'sını kullanarak **output**'u biçimlendirme (kenarlıklar, sayı biçimleri).  
- Düzen oluşturulduktan sonra **Exporting to CSV** yaparak sonraki işlem için dışa aktarma.

Deneyin, sütun sayısını ayarlayın ve karmaşık elektronik tabloları ne kadar hızlı prototipleyebileceğinizi görün. İyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}