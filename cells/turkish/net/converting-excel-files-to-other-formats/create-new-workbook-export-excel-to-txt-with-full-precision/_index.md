---
category: general
date: 2026-03-18
description: Yeni bir çalışma kitabı oluşturun ve sayısal hassasiyeti koruyarak Excel'i
  TXT'ye dışa aktarın. Çalışma sayfasını txt olarak kaydetmeyi ve çalışma sayfasını
  verimli bir şekilde txt'ye dönüştürmeyi öğrenin.
draft: false
keywords:
- create new workbook
- export excel to txt
- save excel as txt
- save worksheet as txt
- convert worksheet to txt
language: tr
og_description: Yeni bir çalışma kitabı oluşturun ve Excel'i hassas bir şekilde TXT'ye
  dışa aktarın. Bu öğretici, çalışma sayfasını txt olarak kaydetmeyi ve C# kullanarak
  çalışma sayfasını txt'ye dönüştürmeyi gösterir.
og_title: Yeni çalışma kitabı oluştur – Excel'i TXT'ye Dönüştürme Kılavuzu
tags:
- Aspose.Cells
- C#
- Excel automation
title: Yeni çalışma kitabı oluştur – Excel'i tam hassasiyetle TXT'ye dışa aktar
url: /tr/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Yeni çalışma kitabı oluştur – Excel'i Tam Hassasiyetle TXT'ye Dışa Aktar

Hiç C#'ta **create new workbook** yapıp bazı verileri düz metin dosyasına dökmek zorunda kaldınız mı? Belki eski bir sistemden rapor çekiyorsunuz ve aşağı akış aracı yalnızca `.txt` beslemesi kabul ediyor. İyi haber? Sayısal hassasiyeti feda etmenize gerek yok ve kesinlikle CSV dizelerini elle oluşturmanız da gerekmiyor.

Bu rehberde **export excel to txt** sürecinin tamamını adım adım inceleyeceğiz; çalışma kitabını başlatmaktan **save worksheet as txt** sırasında sondaki sıfırları korumaya kadar her şeyi kapsayacağız. Sonunda, herhangi bir .NET projesine ekleyebileceğiniz, çalıştırmaya hazır bir kod parçacığına sahip olacaksınız—ekstra araçlara gerek yok.

## Gerekenler

- **ASP.NET/ .NET 6+** (kod .NET Framework 4.6+ üzerinde de çalışır)  
- **Aspose.Cells for .NET** – `Workbook`, `Worksheet` ve `TxtSaveOptions` sınıflarını sağlayan kütüphane. NuGet üzerinden `Install-Package Aspose.Cells` ile edinebilirsiniz.  
- C#'a temel bir anlayış (eğer `using` ifadeleriyle rahat iseniz, hazırsınız).  

Hepsi bu—Excel interop yok, COM nesneleri yok ve kesinlikle manuel dize birleştirme yok.

---

## Adım 1: Yeni Bir Çalışma Kitabı Başlat (Primary Keyword)

İlk yapmanız gereken **create new workbook** işlemidir. Çalışma kitabını, daha sonra sayı, metin veya formüller yapıştıracağınız boş bir tuval olarak düşünün.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();                 // <‑‑ creates new workbook
            Worksheet worksheet = workbook.Worksheets[0];       // first sheet (index 0)
```

> **Why this matters:** `Workbook`'ı bir dosya yüklemeden örneklemek size temiz bir sayfa verir. Daha sonra verileri programatik olarak ekleyebilirsiniz; bu, mevcut bir `.xlsx`'iniz olmadığı **convert worksheet to txt** senaryoları için mükemmeldir.

---

## Adım 2: Hücreleri Doldur – Sondaki Sıfırları Koruyun

Sayıları metne dökerken sıkça karşılaşılan bir tuzak, sondaki sıfırların kaybolmasıdır (`123.45000` → `123.45`). Aşağı akış sistemleri sabit‑genişli alanlara dayanıyorsa, bu kayıp her şeyi bozabilir.

```csharp
            // Step 2: Write a numeric value that contains trailing zeros
            // PutValue respects the data type; we’ll later tell the saver to keep precision.
            worksheet.Cells[0, 0].PutValue(123.45000);
```

> **Pro tip:** `PutValue` otomatik olarak veri tipini belirler. Eğer bir sayıya benzeyen bir dizeye ihtiyacınız varsa, bunun yerine `PutValue("123.45000")` kullanın.

---

## Adım 3: TXT Kaydetme Seçeneklerini Yapılandır – Sayısal Hassasiyeti Koru

İşte sihrin gerçekleştiği yer. `PreserveNumericPrecision` özelliğini etkinleştirerek Aspose.Cells'e girdiğiniz tam değeri, önemsiz sondaki sıfırları da dahil olmak üzere, yazmasını söylersiniz.

```csharp
            // Step 3: Configure TXT save options to keep the original numeric precision
            TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                PreserveNumericPrecision = true   // retain all digits, even trailing zeros
            };
```

> **Why enable this?** **save excel as txt** yaptığınızda, varsayılan davranış gereksiz ondalıkları kırpar. `PreserveNumericPrecision = true` ayarı, çıktının hücrenin ekranda gösterilen değerini yansıtmasını garanti eder; bu, finansal raporlar veya bilimsel veriler için kritiktir.

---

## Adım 4: Çalışma Sayfasını TXT Olarak Kaydet – Son Dışa Aktarım

Şimdi gerçekten **save worksheet as txt** yapıyoruz. Yazma izniniz olan herhangi bir yola işaret edebilirsiniz; örnek, `output` adlı göreli bir klasör kullanıyor.

```csharp
            // Step 4: Save the worksheet as a TXT file using the configured options
            string outputPath = "output/num-preserve.txt";
            worksheet.Save(outputPath, txtSaveOptions);

            Console.WriteLine($"File saved to {outputPath}");
        }
    }
}
```

> **Expected output** (`num-preserve.txt`):

```
123.45000
```

Sondaki sıfırların yerinde olduğunu fark edin—tam da istediğiniz gibi.

---

## Adım 5: Sonucu Doğrula – Hızlı Kontrol

Program çalıştıktan sonra, `num-preserve.txt` dosyasını herhangi bir metin düzenleyicide açın. Tek satırda `123.45000` görmelisiniz. Eğer bunun yerine `123.45` görürseniz, `PreserveNumericPrecision`'ın `true` olarak ayarlandığını ve Aspose.Cells'in (v23.10+) güncel bir sürümünü kullandığınızı tekrar kontrol edin.

---

## Yaygın Varyasyonlar ve Kenar Durumları

### Birden Çok Hücre veya Aralık Dışa Aktarma

Bir bütün aralık için **export excel to txt** yapmanız gerekiyorsa, kaydetmeden önce daha fazla hücreyi doldurmanız yeterlidir:

```csharp
worksheet.Cells["A1"].PutValue(100);
worksheet.Cells["A2"].PutValue(200.500);
worksheet.Cells["A3"].PutValue(300.00);
```

Aspose varsayılan olarak her hücreyi yeni bir satıra yazar. Ayracı (`txtSaveOptions.Separator`) kullanarak sekme, virgül gibi bir ayırıcıya da değiştirebilirsiniz.

### Çalışma Sayfasını Farklı Kodlamalarla TXT'ye Dönüştürme

Bazen aşağı akış sistemleri UTF‑8 BOM veya ASCII ister. Kodlamayı şu şekilde ayarlayabilirsiniz:

```csharp
txtSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

### Büyük Çalışma Kitaplarını İşleme

Yüz binlerce satır gibi devasa sayfalarla çalışırken, çıktıyı akış olarak yazmayı düşünün:

```csharp
txtSaveOptions.EnableCache = true; // writes data in chunks to reduce memory footprint
```

---

## Pro İpuçları ve Dikkat Edilmesi Gerekenler

- **Don’t forget to create the output directory** `Save` çağrısı yapmadan önce çıktı klasörünü oluşturmayı unutmayın, aksi takdirde `DirectoryNotFoundException` alırsınız.  
- **Watch out for locale‑specific decimal separators**. Ortamınız virgül (`1,23`) kullanıyorsa, nokta zorlamak için `txtSaveOptions.DecimalSeparator = '.'` ayarlayın.  
- **Version compatibility**: `PreserveNumericPrecision` bayrağı Aspose.Cells 20.6'da tanıtıldı. Daha eski bir sürüm kullanıyorsanız, bu bayrak mevcut olmayacak ve kaydetmeden önce hücreyi metin olarak biçimlendirmeniz gerekecek.

![Yeni çalışma kitabı örneği](excel-to-txt.png "Yeni çalışma kitabı")

*Görsel alt metni: "Yeni bir çalışma kitabı oluştur ve Excel'i sayısal hassasiyet korunmuş şekilde TXT'ye dışa aktar"*

---

## Özet – Neler Kapsandı

- **Create new workbook** Aspose.Cells kullanarak.  
- Sondaki sıfırları içeren bir sayı ile bir hücreyi doldurun.  
- `TxtSaveOptions.PreserveNumericPrecision = true` ayarlayarak **save excel as txt** işlemini hassasiyeti kaybetmeden yapın.  
- Dosyayı diske yazın ve çıktının orijinal değerle eşleştiğini doğrulayın.  

Bu, 50 satırın altında C# ile tam **convert worksheet to txt** iş akışıdır.

---

## Sonraki Adımlar ve İlgili Konular

Artık **export excel to txt** işlemini mükemmel hassasiyetle yapabildiğinize göre, aşağıdakileri keşfetmek isteyebilirsiniz:

- **Exporting to CSV** özel ayırıcılarla (`TxtSaveOptions.Separator`).  
- **Saving as other plain‑text formats** TSV gibi (`SaveFormat.TabDelimited`).  
- **Batch processing** bir klasördeki birden çok çalışma kitabını `Directory.GetFiles` ile işlemek.  
- **Integrating with Azure Functions** bulutta isteğe bağlı dönüşüm için.

Bunların her biri aynı `Workbook` → `Worksheet` → `TxtSaveOptions` desenine dayanır, bu yüzden kendinizi rahat hissedeceksiniz.

---

### Son Düşünce

Eğer bu adımları izlediyseniz, artık **create new workbook** nasıl yapılacağını, nasıl doldurulacağını ve **save worksheet as txt** yaparken ihtiyacınız olan her ondalık basamağın korunacağını tam olarak biliyorsunuz. Bu küçük bir kod parçası, ancak eski veri hatları düz metin girdileri istediğinde şaşırtıcı derecede yaygın bir sorunu çözüyor.

Bir deneyin, seçenekleri ayarlayın ve verinin tam istediğiniz gibi akmasını sağlayın. Kodlamanın tadını çıkarın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}