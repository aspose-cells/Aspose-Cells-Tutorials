---
category: general
date: 2026-07-03
description: SmartMarkerProcessor kullanarak çalışma sayfalarını nasıl tekrarlayacağınızı
  ve dinamik Excel dosyaları oluşturacağınızı öğrenin. .NET geliştiricileri için adım
  adım kod örneği.
draft: false
keywords:
- how to repeat worksheets
- generate dynamic excel sheets
- SmartMarkerProcessor Excel
- repeat sheet template C#
- dynamic workbook generation
language: tr
og_description: SmartMarkerProcessor kullanarak tam, çalıştırılabilir bir C# örneğiyle
  çalışma sayfalarını nasıl tekrarlayacağınızı ve dinamik Excel dosyaları oluşturacağınızı
  keşfedin.
og_title: Çalışma Sayfalarını Tekrarlama – Tam .NET Öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to repeat worksheets and generate dynamic Excel sheets using
    SmartMarkerProcessor. Step‑by‑step code example for .NET developers.
  headline: How to Repeat Worksheets – Complete Guide for Excel Automation
  type: TechArticle
- description: Learn how to repeat worksheets and generate dynamic Excel sheets using
    SmartMarkerProcessor. Step‑by‑step code example for .NET developers.
  name: How to Repeat Worksheets – Complete Guide for Excel Automation
  steps:
  - name: Scans every worksheet for markers that match the provided object’s property
      names.
    text: Scans every worksheet for markers that match the provided object’s property
      names.
  - name: Detects the `{0}` placeholder in the sheet name and creates a new sheet
      for each data row.
    text: Detects the `{0}` placeholder in the sheet name and creates a new sheet
      for each data row.
  - name: Replaces any cell markers like `&=Sheet.Title` with the actual title value.
    text: Replaces any cell markers like `&=Sheet.Title` with the actual title value.
  - name: '**Keep the template minimal.** Only include elements that truly need to
      be duplicated; static helper sheets can stay outside the `Sheet_{0}` pattern.'
    text: '**Keep the template minimal.** Only include elements that truly need to
      be duplicated; static helper sheets can stay outside the `Sheet_{0}` pattern.'
  - name: '**Validate input data** before processing to avoid runtime marker errors.'
    text: '**Validate input data** before processing to avoid runtime marker errors.'
  - name: '**Dispose of the Workbook** (`wb.Dispose()`) when dealing with many files
      to free unmanaged resources.'
    text: '**Dispose of the Workbook** (`wb.Dispose()`) when dealing with many files
      to free unmanaged resources.'
  - name: '**Leverage SmartMarker expressions** (`&=Sheet.Title`, `&=Sheet.Total`)
      to inject more complex data without extra code.'
    text: '**Leverage SmartMarker expressions** (`&=Sheet.Title`, `&=Sheet.Total`)
      to inject more complex data without extra code.'
  - name: '**Version your templates.** Store them alongside your source code so CI
      pipelines can copy them automatically.'
    text: '**Version your templates.** Store them alongside your source code so CI
      pipelines can copy them automatically.'
  type: HowTo
- questions:
  - answer: Absolutely. Just pass the DataTable as the value of the `Sheet` marker
      (`new { Sheet = dataTable }`).
    question: Can I repeat worksheets based on a DataTable?
  - answer: Formulas are preserved because we clone the entire worksheet, including
      its calculation engine.
    question: What if my template has formulas referencing other sheets?
  - answer: Yes—use a sheet‑name marker such as `Sheet_{0}_&=Sheet.Title` inside the
      template.
    question: Is it possible to rename the duplicated sheets?
  - answer: The free evaluation works, but it adds watermarks. For production use,
      obtain a proper license to remove them.
    question: Do I need a license for Aspose.Cells?
  type: FAQPage
tags:
- Excel
- C#
- Aspose.Cells
- Automation
title: Çalışma Sayfalarını Tekrarlama – Excel Otomasyonu İçin Tam Rehber
url: /tr/net/smart-markers-dynamic-data/how-to-repeat-worksheets-complete-guide-for-excel-automation/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Çalışma Sayfalarını Tekrarlama – Excel Otomasyonu için Tam Kılavuz

Excel dosyasında **çalışma sayfalarını nasıl tekrar edeceğinizi** manuel olarak tek tek kopyalamadan hiç merak ettiniz mi? Tek başınıza değilsiniz. Birçok raporlama senaryosunda, her ay, departman veya başka bir veri dilimi için çoğaltmanız gereken bir şablon sayfanız olur. İyi haber? Birkaç C# satırıyla **dinamik Excel sayfaları oluşturabilir** ve çalışma kitabının verilerinizle birlikte büyümesini sağlayabilirsiniz.

Bu öğreticide, bir şablon çalışma kitabını yükleyen, Aspose.Cells'in SmartMarkerProcessor'ını başlıklar dizisine bağlayan ve sonunda her veri öğesi için sayfayı tekrarlayan yeni bir dosya kaydeden uygulamalı bir çözümü adım adım inceleyeceğiz. Sonunda, herhangi bir .NET projesine ekleyebileceğiniz ve anında dinamik Excel sayfaları oluşturmaya başlayabileceğiniz yeniden kullanılabilir bir kod parçacığına sahip olacaksınız.

## Önkoşullar

- **.NET 6+** (veya .NET Framework 4.6.2+).  
- **Aspose.Cells for .NET** NuGet paketi (`Aspose.Cells`) yüklü.  
- `template.xlsx` adlı bir şablon çalışma kitabı, içinde `Sheet_{0}` adlı bir sayfa bulunur; `{0}` sayfa indeksinin SmartMarker yer tutucusudur.  
- C# ve nesne başlatıcıları hakkında temel bir anlayış.

Ek bir yapılandırma gerekmez—Aspose.Cells içsel olarak ağır işi halleder.

## Adım 1: Şablon Çalışma Kitabını Yükleme (Çalışma Sayfalarını Tekrarlama – Yükleme Aşaması)

İlk ihtiyacımız, şablonumuza işaret eden bir workbook nesnesidir. Bunu, veri koleksiyonumuzdaki her giriş için klonlanacak bir tuval olarak düşünün.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

...

// Load the template workbook that contains a sheet named "Sheet_{0}"
Workbook wb = new Workbook(@"C:\ExcelTemplates\template.xlsx");
```

> **Neden önemli:** `Workbook` sınıfı tüm Excel dosyasını temsil eder. Önceden tasarlanmış bir şablon yükleyerek, yalnızca sayfa yapısını çoğaltırken biçimlendirme, formüller ve tüm statik içeriği aynı tutarsınız.

## Adım 2: SmartMarkerProcessor'ı Oluşturma ve Yapılandırma

SmartMarkerProcessor, workbook'ta işaretçileri (yer tutucuları) tarayan ve bunları veri ile değiştiren motorudur. **Dinamik Excel sayfaları oluşturmak** için mükemmeldir çünkü yeni çalışma sayfalarını anında oluşturabilir.

```csharp
// Instantiate the processor – it will handle the marker substitution
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

> **Pro ipucu:** Özel veri dönüşümüne (ör. tarihleri belirli formatlara) ihtiyacınız varsa, `Process` metodunu çağırmadan önce bir `SmartMarkerProcessor` olay işleyicisi ekleyebilirsiniz.

## Adım 3: Veri Kaynağını Hazırlama – Sayfa Başlıkları Dizisi

Amacımız her ay için bir sayfayı tekrarlamaktır, bu yüzden her öğe bir `Title` tutan basit bir dizi oluşturuyoruz. Bu dizi, veritabanları, CSV dosyaları veya API yanıtları gibi herhangi bir koleksiyonla değiştirilebilir.

```csharp
// Define the data that drives the repetition
var sheetData = new[]
{
    new { Title = "Jan" },
    new { Title = "Feb" },
    new { Title = "Mar" } // Add more months as needed
};
```

> **Neden anonim tip?** Örneği hafif tutar. Gerçek projelerde muhtemelen toplamları, tarihleri vb. taşıyan güçlü tipli bir sınıf (ör. `MonthInfo`) kullanırsınız.

## Adım 4: Smart‑Marker İşlemini Çalıştırma

Şimdi veriyi `Sheet` adlı işaretçiye bağlıyoruz. Şablondaki yer tutucu (`Sheet_{0}`) Aspose.Cells'e `sheetData` içindeki her öğe için sayfayı çoğaltmasını söyler.

```csharp
// Bind the data to the "Sheet" marker – this triggers sheet duplication
processor.Process(wb, new { Sheet = sheetData });
```

SmartMarkerProcessor, arka planda şu işlemleri yapar:

1. Sağlanan nesnenin özellik adlarıyla eşleşen işaretçileri her çalışma sayfasında tarar.  
2. Sayfa adındaki `{0}` yer tutucusunu algılar ve her veri satırı için yeni bir sayfa oluşturur.  
3. `&=Sheet.Title` gibi hücre işaretçilerini gerçek başlık değeriyle değiştirir.

### Kenar Durumları ve İpuçları

- **Şablon Sayfası Eksik:** `Sheet_{0}` bulunmazsa, işlemci bir `MarkerException` fırlatır. Şablon sayfa adının tam olarak eşleştiğinden emin olun.  
- **Büyük Veri Setleri:** Binlerce satır için, bellek kullanımını azaltmak amacıyla çalışma kitabını akış olarak kaydetmeyi düşünün (`Workbook.Save(..., SaveFormat.Xlsx, new SaveOptions { MemorySetting = MemorySetting.MemoryPreference })`).  
- **Özel Sayfa İsimleri:** Sayfa adında ek işaretçiler ekleyebilirsiniz, ör. `Sheet_{0}_&=Sheet.Title`, böylece `Sheet_1_Jan`, `Sheet_2_Feb` gibi isimler elde edersiniz.

## Adım 5: Oluşturulan Çalışma Kitabını Kaydetme

Son olarak, değiştirilmiş çalışma kitabını diske yazın. Çıktı dosyası artık `sheetData` içindeki her başlık için ayrı bir çalışma sayfası içeriyor.

```csharp
// Persist the workbook with repeated sheets
wb.Save(@"C:\ExcelOutputs\RepeatingSheets.xlsx");
```

Kaydedilen dosyayı açtığınızda üç sayfa göreceksiniz: `Sheet_1`, `Sheet_2` ve `Sheet_3`; her biri ilgili ay başlığıyla doldurulmuş.

## Tam Çalışan Örnek

Hepsini bir araya getirerek, hemen çalıştırabileceğiniz tek bir kopyala‑yapıştır hazır program aşağıdadır.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace ExcelWorksheetRepeater
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the template workbook (must contain a sheet named "Sheet_{0}")
            string templatePath = @"C:\ExcelTemplates\template.xlsx";
            Workbook wb = new Workbook(templatePath);

            // 2️⃣ Create the SmartMarkerProcessor
            SmartMarkerProcessor processor = new SmartMarkerProcessor();

            // 3️⃣ Prepare the data – each object will generate a new worksheet
            var sheetData = new[]
            {
                new { Title = "Jan" },
                new { Title = "Feb" },
                new { Title = "Mar" }
            };

            // 4️⃣ Process the workbook – bind the data to the "Sheet" marker
            processor.Process(wb, new { Sheet = sheetData });

            // 5️⃣ Save the workbook with repeated sheets
            string outputPath = @"C:\ExcelOutputs\RepeatingSheets.xlsx";
            wb.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Beklenen çıktı:** `RepeatingSheets.xlsx` dosyasını açın ve üç çalışma sayfası (`Sheet_1`, `Sheet_2`, `Sheet_3`) göreceksiniz. Her sayfa, `template.xlsx`'den gelen statik içeriğin yanı sıra, `&=Sheet.Title` gibi bir SmartMarker yerleştirdiğiniz yerde başlığı (`Jan`, `Feb`, `Mar`) içerir.

## Sık Sorulan Sorular

- **DataTable temelinde çalışma sayfalarını tekrar edebilir miyim?** Kesinlikle. `Sheet` işaretçisinin değeri olarak DataTable'ı (`new { Sheet = dataTable }`) geçmeniz yeterlidir.  
- **Şablonumda diğer sayfalara referans veren formüller varsa ne olur?** Formüller korunur çünkü tüm çalışma sayfasını, hesaplama motoru dahil, klonlarız.  
- **Kopyalanan sayfaların adını değiştirmek mümkün mü?** Evet—şablon içinde `Sheet_{0}_&=Sheet.Title` gibi bir sayfa‑adı işaretçisi kullanabilirsiniz.  
- **Aspose.Cells için lisansa ihtiyacım var mı?** Ücretsiz deneme çalışır, ancak filigran ekler. Üretim kullanımında, bunları kaldırmak için geçerli bir lisans alın.

## Dinamik Excel Sayfaları Oluşturmak İçin En İyi Uygulamalar

1. **Şablonu minimal tutun.** Yalnızca gerçekten çoğaltılması gereken öğeleri ekleyin; statik yardımcı sayfalar `Sheet_{0}` deseninin dışında kalabilir.  
2. **İşleme başlamadan önce giriş verilerini doğrulayın**; böylece çalışma zamanı işaretçi hatalarından kaçınırsınız.  
3. **Workbook'ı serbest bırakın** (`wb.Dispose()`) çok sayıda dosyayla çalışırken yönetilmeyen kaynakları serbest bırakmak için.  
4. **SmartMarker ifadelerinden** (`&=Sheet.Title`, `&=Sheet.Total`) yararlanarak ekstra kod olmadan daha karmaşık verileri enjekte edin.  
5. **Şablonlarınızı sürümleyin.** Kaynak kodunuzla birlikte saklayın, böylece CI pipeline'ları otomatik olarak kopyalayabilir.

## Sonuç

Excel çalışma kitabında **çalışma sayfalarını nasıl tekrar edeceğinizi** ele aldık ve bu süreçte Aspose.Cells ile **dinamik Excel sayfaları oluşturmak** için sağlam bir desen gösterdik. Bir şablon yükleyerek, başlıklar dizisini besleyerek ve çoğaltmayı SmartMarkerProcessor'a bırakarak, birkaç aydan binlerce veri bölümüyle ölçeklenebilen temiz, sürdürülebilir bir çözüm elde edersiniz.

Bir sonraki adıma hazır mısınız? Her sayfaya daha fazla işaretçi ekleyin—örneğin ay bazında satış rakamları tablosu—veya sayfalara göre uyum sağlayan koşullu biçimlendirmelerle deney yapın. Aynı yaklaşım faturalar, proje raporları veya bir sayfa şablonunun programlı olarak çoğaltılması gereken her senaryo için çalışır.

Bu kılavuzu faydalı bulduysanız, bir yıldız verin, ekip arkadaşlarınızla paylaşın veya kendi kullanım senaryonuzla ilgili bir yorum bırakın. Kodlamanın tadını çıkarın ve dinamik Excel oluşturmanın gücünün keyfini çıkarın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose.Cells .NET Smart Markers Kullanarak Dinamik Excel Raporları Oluşturma](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Aspose.Cells for .NET Kullanarak Excel Sayfalarını Birleştirme ve Yeniden Adlandırma: Adım Adım Kılavuz](/cells/english/net/worksheet-management/merge-rename-excel-sheets-aspose-cells-net/)
- [Aspose.Cells for .NET Kullanarak Excel'de Çalışma Sayfalarını Birleştirme: Kapsamlı Kılavuz](/cells/english/net/worksheet-management/merge-spreadsheets-with-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}