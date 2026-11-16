---
category: general
date: 2026-11-16
description: Aspose.Cells, dinamik dizi fonksiyonları ve bir lambda azaltıcı kullanarak
  Excel'de diziyi nasıl genişleteceğinizi öğrenin, ardından C# ile Excel dosyasını
  yazın.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- create excel workbook
- how to use lambda
- dynamic array functions
- write excel file
language: tr
lastmod: 2026-11-16
og_description: Aspose.Cells, dinamik dizi fonksiyonları ve bir lambda azaltıcı kullanarak
  Excel'de diziyi nasıl genişleteceğiniz. Excel dosyasını yazmak için tam C# örneğini
  izleyin.
og_image_alt: Diagram illustrating how to expand array in an Excel worksheet
og_title: Aspose.Cells ile Excel’de Dizi Nasıl Genişletilir – Adım Adım Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to expand array in Excel using Aspose.Cells, dynamic array
    functions, and a lambda reducer, then write the Excel file from C#.
  headline: How to expand array in Excel with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. `EXPAND` pads missing columns with blank cells. The same works for
      rows.
    question: Can I expand to more columns than the source provides?
  - answer: '`EXPAND` will treat the source as a single row; you can still specify
      rows and columns to reshape it.'
    question: What if the source array is horizontal (`{1,2,3,4,5}`)?
  - answer: The lambda must return a value compatible with the accumulator type. For
      text concatenation you could use `LAMBDA(acc, val, acc & val)`.
    question: Does `REDUCE` work with non‑numeric data?
  - answer: Only when you need the computed values before saving. Excel will recalculate
      on open if you skip it.
    question: Do I need to call `CalculateFormula` for every change?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Excel automation
title: Aspose.Cells ile Excel'de diziyi nasıl genişletilir
url: /tr/net/calculation-engine/how-to-expand-array-in-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Aspose.Cells ile dizi nasıl genişletilir

Eğer C# ile bir Excel çalışma sayfasında **diziyi nasıl genişletilir** ihtiyacınız varsa, bu öğretici tam adımları gösterir. Bir Excel çalışma kitabı oluşturacak, `EXPAND` ve `REDUCE` gibi dinamik dizi fonksiyonlarını kullanacak, bir **lambda** biriktirici uygulayacak ve sonunda **Excel dosyasını yaz**acaksınız. Yaklaşım Aspose.Cells 23.10 veya daha yeni sürümlerle çalışır ve manuel Excel kurulumu gerektirmez.

Bu rehberin sonunda, dinamik dizi formüllerinin programatik bağlamdaki gücünü gösteren tam işlevsel bir `ExpandReduceDemo.xlsx` dosyasına sahip olacaksınız.

## Gereksinimler

- .NET 6.0 (veya Aspose.Cells tarafından desteklenen herhangi bir .NET sürümü)
- Aspose.Cells for .NET paketi (`dotnet add package Aspose.Cells`)
- Bir kod editörü veya IDE (Visual Studio, VS Code, Rider, vb.)

Ek bir COM interop veya Office kurulumu gerekmez çünkü Aspose.Cells dosya formatını dahili olarak yönetir.

## Adım 1: Excel çalışma kitabı oluşturma

İlk görev, bellekte **excel çalışma kitabı oluşturmak**tır. Aspose.Cells, bir bütün XLSX dosyasını temsil eden `Workbook` sınıfını sağlar.

```csharp
using System;
using Aspose.Cells;

class ExpandReduceDemo
{
    static void Main()
    {
        // Step 1: instantiate a new workbook and get the default worksheet
        Workbook workbook = new Workbook();              // creates an empty .xlsx structure
        Worksheet sheet = workbook.Worksheets[0];        // the first (and only) sheet by default
```

> **Neden önemli:** Bir `Workbook` örneği oluşturmak size temiz bir tuval sağlar. Varsayılan çalışma sayfası zaten hazırlanmıştır, bu yüzden birden fazla sayfa istemediğiniz sürece elle eklemenize gerek yoktur.

## Adım 2: Dikey dizi sabiti ekleme

Excel'in dinamik dizi motoru, literal dizi sabitleriyle çalışabilir. Dikey dizi `{1;2;3;4;5}`'i **A1** hücresine yerleştireceğiz.

```csharp
        // Step 2: put a vertical array constant into A1
        sheet.Cells["A1"].PutValue("{1;2;3;4;5}");
```

> **İpucu:** Noktalı virgül (`;`) sabitte satırları ayırırken, virgül (`,`) sütunları ayırır. Bu, Excel'in kendi sözdizimini yansıtır.

## Adım 3: Diziyi bir matrise genişletme

Şimdi temel soruyu yanıtlıyoruz – **diziyi nasıl genişletilir** – `EXPAND` fonksiyonunu kullanarak. Formül, tek sütunluk diziyi **B1**'den başlayan 5 satır × 2 sütunluk bir matrise genişletir.

```csharp
        // Step 3: use EXPAND to create a 5‑row by 2‑column matrix
        sheet.Cells["B1"].Formula = "EXPAND(A1,5,2)";
```

> **Neden EXPAND?** `EXPAND(source, rows, cols)` kaynak aralığın belirtilen boyutu kaplamasını zorlar, gerekirse boşluklarla doldurur. Tek bir diziden daha büyük bir matris oluşturmanın en okunabilir yoludur.

## Adım 4: Matrisi bir lambda biriktirici ile azaltma

`REDUCE` fonksiyonu bir aralık üzerinde yineleme yapar ve değerleri bir **lambda** ifadesi kullanarak biriktirir. Burada her sütun değerini tek bir sütunda toplar ve sonucu **D1** hücresine yerleştiririz.

```csharp
        // Step 4: REDUCE the expanded matrix using a lambda accumulator
        sheet.Cells["D1"].Formula = "REDUCE(A1, B1:E5, LAMBDA(acc, val, acc+val))";
```

> **Lambda nasıl kullanılır:** `LAMBDA(acc, val, acc+val)` mevcut biriktiriciyi (`acc`) ve bir sonraki hücre değerini (`val`) alır. Yeni biriktiriciyi döndürür, böylece çalışan bir toplam gerçekleştirir. Bu, koddan Excel formüllerinde **lambda nasıl kullanılır** gösterir.

## Adım 5: Formülleri hesaplayarak sonuçların görünmesini sağlama

Aspose.Cells, formülleri ayarladığınızda otomatik olarak değerlendirmez. `CalculateFormula` çağrısı, motoru çalışma kitabındaki tüm formülleri hesaplamaya zorlar.

```csharp
        // Step 5: recalculate all formulas so the results are materialized
        workbook.CalculateFormula();
```

> **Not:** Oluşturulan dosyayı Excel'de açarsanız, değerler zaten görünür olacaktır çünkü önceden hesaplanmışlardır.

## Adım 6: Excel dosyasını diske yazma

Son olarak, `Save` yöntemiyle **excel dosyasını yaz**ın. Yazma izniniz olan bir klasör seçin.

```csharp
        // Step 6: save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\ExpandReduceDemo.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Beklenen sonuç

| A | B | C | D |
|---|---|---|---|
| {1;2;3;4;5} | 1 |  | 15 |
|            | 2 |  |    |
|            | 3 |  |    |
|            | 4 |  |    |
|            | 5 |  |    |

- **B Sütunu** ve **C** `EXPAND` ile üretilen 5 × 2 matrisi içerir.
- **D1 Hücresi** `15` gösterir, bu `REDUCE` + **lambda** formülüyle hesaplanan tüm sayıların toplamıdır.

## Yaygın sorular ve kenar durumları

- **Kaynağın sağladığından daha fazla sütuna genişletebilir miyim?**  
  Evet. `EXPAND` eksik sütunları boş hücrelerle doldurur. Aynı şey satırlar için de geçerlidir.

- **Kaynak dizi yataysa (`{1,2,3,4,5}`) ne olur?**  
  `EXPAND` kaynağı tek bir satır olarak kabul eder; yine de satır ve sütunları belirleyerek yeniden şekillendirebilirsiniz.

- **`REDUCE` sayısal olmayan verilerle çalışır mı?**  
  Lambda, biriktirici türüyle uyumlu bir değer döndürmelidir. Metin birleştirme için `LAMBDA(acc, val, acc & val)` kullanabilirsiniz.

- **Her değişiklikte `CalculateFormula` çağırmam gerekiyor mu?**  
  Yalnızca kaydetmeden önce hesaplanmış değerlere ihtiyacınız olduğunda. Bunu atladığınızda Excel, dosya açıldığında yeniden hesaplar.

## Profesyonel ipuçları

- **Performans:** Büyük çalışma kitapları için, tüm formüller ayarlandıktan sonra `workbook.CalculateFormula`'u bir kez çağırın, her hücreden sonra değil.
- **Sürüm güvenliği:** `EXPAND` ve `REDUCE`, Excel 365 ve sonrası sürümlerde mevcuttur. Aspose.Cells, hedef Excel sürümünden bağımsız olarak bunları uygular çünkü hesaplama motoru dahili olarak bulunur.
- **Formülleri hata ayıklama:** Ayarladığınız tam dizeyi geri okumak için `sheet.Cells["B1"].Formula` kullanın; bu, formülleri dinamik olarak oluştururken yardımcı olur.

## Sonuç

Artık Aspose.Cells kullanarak Excel'de **diziyi nasıl genişletilir** bildiğinize, **dinamik dizi fonksiyonlarını** kullandığınıza, `REDUCE` ile bir **lambda** uyguladığınıza ve C#'tan **excel dosyasını yaz**dığınıza emin olabilirsiniz. Bu uçtan uca örnek, matris transpozisyonu, kümülatif toplamlar veya özel birikimler gibi daha karmaşık veri dönüşümlerine uyarlanabilir.

---

*Sonraki adımlar:*  
- `FILTER`, `SORT` ve `UNIQUE` gibi diğer dinamik fonksiyonları keşfedin.  
- Tekrar kullanılabilir kullanıcı tanımlı fonksiyonlar oluşturmak için birden fazla `LAMBDA` ifadesini birleştirin.  
- Çalışma kitabı oluşturmayı ASP.NET Core API'lerine entegre ederek anlık rapor oluşturun.

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Dinamik dizi formülüyle C# Excel çalışma kitabı nasıl oluşturulur](/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/)
- [Excel'de diziyi genişletme ve bir şablonu doldurma](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)
- [Aspose.Cells ile C#'ta Dizi Nasıl Genişletilir – Adım Adım Kılavuz](/cells/english/net/excel-formulas-and-calculation-options/how-to-expand-array-in-c-with-aspose-cells-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}