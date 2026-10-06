---
category: general
date: 2026-02-28
description: C#'ta ana‑detay raporu oluşturun ve Excel şablonunu doldurmayı, verileri
  Excel'e birleştirmeyi ve Excel çalışma kitabını C#'ta birkaç adımda yüklemeyi öğrenin.
draft: false
keywords:
- create master detail report
- populate excel template
- merge data into excel
- load excel workbook c#
- how to create master detail
language: tr
og_description: Aspose.Cells SmartMarker kullanarak C#'te ana‑detay raporu oluşturun.
  Excel çalışma kitabını C#'te nasıl yükleyeceğinizi, verileri Excel'e nasıl birleştireceğinizi
  ve bir Excel şablonunu nasıl dolduracağınızı öğrenin.
og_title: C#'ta master-detail raporu oluştur – Excel şablonunu doldur
tags:
- C#
- Aspose.Cells
- Excel automation
- SmartMarker
title: C#'ta master-detail raporu oluştur – SmartMarker ile Excel şablonunu doldur
url: /tr/net/smart-markers-dynamic-data/create-master-detail-report-in-c-populate-excel-template-wit/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#’ta master‑detail raporu oluşturma – SmartMarker ile Excel şablonunu doldurma

C#’ta **master detail raporu oluşturma** ihtiyacı hiç duydunuz mu, ancak verileri bir Excel dosyasına nasıl aktaracağınızdan emin değildiniz mi? Tek başınıza değilsiniz. Bu rehberde **Excel şablonunu doldurma**, **verileri Excel’e birleştirme** ve **C# tarzında Excel çalışma kitabını yükleme** adımlarını adım adım göstereceğiz, böylece dağıtıma hazır, cilalı bir master‑detail raporuna sahip olacaksınız.

Aspose.Cells SmartMarker'ı kullanacağız, kutudan çıkar çıkmaz master‑detail ilişkilerini anlayan güçlü bir motor. Öğreticinin sonunda, herhangi bir .NET projesine ekleyebileceğiniz tam, çalıştırılabilir bir örnek elde edeceksiniz. Belirsiz “belgelere bak” kısayolları yok—sadece kopyala‑yapıştır yapıp çalıştırabileceğiniz bağımsız bir çözüm.

## Öğrenecekleriniz

- C#’ta **master detail** veri yapılarını nasıl oluşturacağınızı ve bunların doğrudan bir Excel şablonuna nasıl eşleneceğini.
- SmartMarker etiketleri içeren bir `.xlsx` dosyasını açan **C# tarzında Excel çalışma kitabını yükleme** kodunun tam şeklini.
- `SmartMarkerProcessor` çalıştırarak **Excel şablonunu doldurma** sürecini.
- Eksik etiketler veya büyük veri setleri gibi kenar durumlarını ele almanın ipuçları.
- Sonucu nasıl doğrulayacağınızı ve nihai **master detail raporunun** nasıl göründüğünü.

### Önkoşullar

- .NET 6.0 veya daha yenisi (kod ayrıca .NET Framework 4.8’de de çalışır).
- Aspose.Cells for .NET (ücretsiz deneme NuGet paketini alabilirsiniz: `Install-Package Aspose.Cells`).
- SmartMarker etiketleri içeren temel bir Excel dosyası (`template.xlsx`) (gereken minimum işaretlemeyi göstereceğiz).

Bunlar hazırsa, başlayalım.

## Adım 1 – Master‑detail veri kaynağını oluşturma *(master detail nasıl oluşturulur)*

İhtiyacınız olan ilk şey, master satırları (siparişler) ve bunların alt satırlarını (sipariş kalemleri) temsil eden bir C# nesnesidir. `MasterDetail` `true` olarak ayarlandığında SmartMarker bu hiyerarşiyi otomatik olarak okuyacaktır.

```csharp
using System;

// Step 1: Build the master‑detail data object
var orderData = new
{
    // Master collection – each order is a row in the master table
    Orders = new[]
    {
        new
        {
            Id = 1,
            // Detail collection – items belonging to order 1
            Items = new[] { new { Sku = 101, Qty = 2 }, new { Sku = 102, Qty = 1 } }
        },
        new
        {
            Id = 2,
            Items = new[] { new { Sku = 202, Qty = 1 } }
        }
    }
};
```

**Neden önemli:**  
SmartMarker, `Orders` adlı bir özelliği (master) arar ve ardından her sipariş için `Items` adlı bir koleksiyon arar. Bu adları eşleştirerek, kendi döngülerinizi yazmadan otomatik olarak bir **master‑detail raporu** elde edersiniz.

> **Pro ipucu:** Özellik adlarını kısa ve anlamlı tutun; bunlar Excel şablonunuzdaki yer tutucular haline gelir.

## Adım 2 – Master‑detail işleme için SmartMarker seçeneklerini yapılandırma

Motoru bir master‑detail senaryosuyla çalıştığınızı belirtin ve alt satırları alacak detay sayfasının adını verin.

```csharp
using Aspose.Cells;

// Step 2: Set up SmartMarker options
SmartMarkerOptions options = new SmartMarkerOptions
{
    // Enables master‑detail processing
    MasterDetail = true,
    // The sheet in the template that holds the detail rows
    DetailSheetName = "OrderDetail"
};
```

**Neden önemli:**  
`MasterDetail = true` ifadesini atlamanız durumunda, SmartMarker verileri düz bir liste olarak kabul eder ve detay satırları hiç görünmez. `DetailSheetName` şablonda oluşturduğunuz sayfa adıyla (büyük/küçük harfe duyarlı) aynı olmalıdır.

## Adım 3 – C# tarzında Excel çalışma kitabını yükleme

Şimdi SmartMarker etiketlerini içeren şablonu açıyoruz. Bu, birçok geliştiricinin doğru dosya yolunu kullanmayı veya çalışma kitabını düzgün bir şekilde serbest bırakmayı unuttuğu için takıldığı **C# tarzında Excel çalışma kitabını yükleme** adımıdır.

```csharp
using System.IO;

// Step 3: Load the workbook that holds the SmartMarker tags
string templatePath = Path.Combine(Environment.CurrentDirectory, "template.xlsx");
Workbook workbook = new Workbook(templatePath);
```

**Neden önemli:**  
Aspose.Cells tüm çalışma kitabını belleğe okur, bu yüzden dosya disk üzerinde, bir kaynak olarak gömülü ya da bir web hizmetinden akış olarak gelebilir. Yalnızca yolun, bir sonraki bölümde tartışacağımız etiketleri içeren geçerli bir `.xlsx` dosyasına işaret ettiğinden emin olun.

## Adım 4 – Şablona SmartMarker etiketlerini ekleme (Excel şablonunu doldurma)

Eğer şimdi `template.xlsx` dosyasını açarsanız, iki sayfa göreceksiniz:

- **Orders** – `&=Orders.Id` gibi bir satıra sahip master sayfa.
- **OrderDetail** – `&=Items.Sku` ve `&=Items.Qty` gibi satırlara sahip detay sayfa.

İşte işaretlemenin minimal görünümü:

| Sayfa | Hücre A1 | Hücre B1 |
|-------|----------|----------|
| Orders | `&=Orders.Id` | *(boş)* |
| OrderDetail | `&=Items.Sku` | `&=Items.Qty` |

Etiketler için herhangi bir kod yazmanıza gerek yok—etiketler Excel dosyasında bulunur. **Excel şablonunu doldurma** adımı sadece işlemciyi çağırmaktır:

```csharp
// Step 4: Run SmartMarker to merge data into Excel
new SmartMarkerProcessor().Process(workbook, orderData, options);
```

**Neden önemli:**  
İşlemci her sayfayı tarar, `&=` yer tutucularını gerçek değerlerle değiştirir ve her master ve detail kaydı için satırları genişletir. `MasterDetail` etkin olduğu için, uygun siparişin altındaki her öğe için otomatik olarak yeni bir satır oluşturur.

## Adım 5 – Master detail raporunu kaydetme

Son olarak, doldurulmuş çalışma kitabını diske yazın. Bu, paylaşılmaya hazır bir **master detail raporu** elde ettiğiniz anıdır.

```csharp
// Step 5: Save the populated workbook
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
workbook.Save(outputPath);

// Optional: open the file automatically (Windows only)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = outputPath,
    UseShellExecute = true
});
```

**Beklenen çıktı:**  

- **Orders** sayfası iki satır gösterir: `1` ve `2` (sipariş ID’leri).  
- **OrderDetail** sayfası üç satır gösterir:  
  - SKU 101 Qty 2  
  - SKU 102 Qty 1  
  - SKU 202 Qty 1  

Bu, e-posta ile gönderebileceğiniz, yazdırabileceğiniz veya başka bir sisteme besleyebileceğiniz tam işlevsel bir **master detail raporu oluşturma** örneğidir.

## Kenar durumları ve sık sorulan sorular

### Şablonda bir etiket eksikse ne olur?

SmartMarker bilinmeyen etiketleri sessizce yok sayar, ancak boş hücrelerle karşılaşırsınız. Etiket yazımını iki kez kontrol edin ve C# nesnenizdeki özellik adlarının tam olarak eşleştiğinden emin olun.

### Büyük veri setlerini nasıl yönetir?

İşlemci satırları akış olarak işler, bu yüzden binlerce detay kaydı bile belleği zorlamaz. Ancak, çok büyük dosyalar için `LoadOptions` içinde `MemorySetting` değerini artırmak isteyebilirsiniz.

```csharp
var loadOptions = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook largeWorkbook = new Workbook(templatePath, loadOptions);
```

### Master için farklı bir sayfa adı kullanabilir miyim?

Evet—şablondaki sayfanın adını değiştirin ve bir detay sayfanız varsa `DetailSheetName` değerini ayarlayın. Master sayfa adı yer tutucudan (`&=Orders.Id`) türetilir.

### Toplam satırı eklemem gerekirse ne yapmalıyım?

Şablona normal bir Excel formülü ekleyin (örneğin, `=SUM(B2:B{#})`). SmartMarker, veri eklemesinden sonra formülü korur.

## Tam çalıştırılabilir örnek

Aşağıda, bir konsol uygulamasına kopyala‑yapıştır yapabileceğiniz tam program bulunmaktadır. Tüm `using` yönergelerini, veri modelini, seçenekleri ve dosya işlemlerini içerir.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace MasterDetailReportDemo
{
    class Program
    {
        static void Main()
        {
            // ---------- Step 1: Create master‑detail data ----------
            var orderData = new
            {
                Orders = new[]
                {
                    new
                    {
                        Id = 1,
                        Items = new[]
                        {
                            new { Sku = 101, Qty = 2 },
                            new { Sku = 102, Qty = 1 }
                        }
                    },
                    new
                    {
                        Id = 2,
                        Items = new[]
                        {
                            new { Sku = 202, Qty = 1 }
                        }
                    }
                }
            };

            // ---------- Step 2: SmartMarker options ----------
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                MasterDetail = true,
                DetailSheetName = "OrderDetail"
            };

            // ---------- Step 3: Load the template ----------
            string templatePath = Path.Combine(Environment.CurrentDirectory, "template.xlsx");
            Workbook workbook = new Workbook(templatePath);

            // ---------- Step 4: Process the template ----------
            new SmartMarkerProcessor().Process(workbook, orderData, options);

            // ---------- Step 5: Save the result ----------
            string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
            workbook.Save(outputPath);

            Console.WriteLine($"Master detail report generated at: {outputPath}");
        }
    }
}
```

Programı çalıştırın, `output.xlsx` dosyasını açın ve master‑detail verilerinin güzel bir şekilde doldurulduğunu göreceksiniz.

## Görsel referans

![Master detail raporu çıktısı ekran görüntüsü](https://example.com/images/master-detail-report.png "Master detail raporu örneği")

*Görsel, ID’leri 1 ve 2 olan Orders sayfasını ve üç SKU‑Qty satırını içeren OrderDetail sayfasını göstermektedir.*

## Sonuç

Artık Aspose.Cells SmartMarker kullanarak C#’ta **master detail raporu nasıl oluşturulur** konusunu biliyorsunuz; veri kaynağını oluşturma, **C# tarzında Excel çalışma kitabını yükleme**, **Excel şablonunu doldurma** ve nihayetinde

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}