---
title: Excel Sayfasına Veri Aktarırken Formül Alanlarını Belirleyin
linktitle: Excel Sayfasına Veri Aktarırken Formül Alanlarını Belirleyin
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Bu detaylı eğitimde, Aspose.Cells for .NET kullanarak belirtilen formül alanlarına sahip Excel sayfalarına veri aktarmayı öğrenin.
weight: 11
url: /tr/net/excel-custom-number-date-formatting/specify-formula-fields-while-importing-data-to-worksheet-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel Sayfasına Veri Aktarırken Formül Alanlarını Belirleyin

## giriiş

Excel dosyalarını programatik olarak işlemek söz konusu olduğunda, Aspose.Cells for .NET paha biçilmez bir araçtır. Excel elektronik tablolarını kolaylıkla oluşturmak, değiştirmek ve düzenlemek için sağlam işlevsellik sağlar. Sunduğu ilginç özelliklerden biri de verileri bir Excel sayfasına aktarırken formül alanlarını belirtme yeteneğidir. Bir finansal rapor üzerinde çalıştığınızı ve kullanıcı girdisine göre toplamları otomatik olarak hesaplamanız gerektiğini düşünün. Bu eğitim, temiz ve anlaşılır bir yaklaşımla tam olarak bunu başarmanız için size adım adım rehberlik edecektir.

## Ön koşullar

Koda dalmadan önce ihtiyacınız olan her şeye sahip olduğunuzdan emin olalım. 

1. Visual Studio veya herhangi bir .NET entegre geliştirme ortamı (IDE): C# kodunuzu yazmak ve çalıştırmak için uygun bir IDE'niz olduğundan emin olun.
2.  .NET için Aspose.Cells: Projenizde Aspose.Cells kütüphanesini indirmeniz ve başvurmanız gerekecektir. Bunu şuradan indirebilirsiniz:[Aspose sürümleri](https://releases.aspose.com/cells/net/).
3. Temel C# bilgisi: C# ve nesne yönelimli programlama kavramlarına aşinalık, örnekleri daha iyi anlamanıza yardımcı olacaktır.
4. .NET Framework: Bu eğitimde .NET Framework 4.5 veya üzerini kullandığınız varsayılmaktadır.

Ön koşulları sağladıktan sonra, belirtilen formül alanlarına sahip bir Excel dosyasına bazı verileri aktaralım.

## Paketleri İçe Aktar

Kodunuzu yazmaya başlamadan önce, gerekli Aspose.Cells ad alanını içe aktarmanız gerekir. Bu genellikle C# dosyanızın en üstünde yapılır:

```csharp
using Aspose.Cells;
using System;
using System.Collections.Generic;
```

Bu, Aspose.Cells kütüphanesi tarafından sağlanan sınıfları ve yöntemleri her seferinde ad alanıyla önek eklemenize gerek kalmadan kullanmanıza olanak tanır.

Tüm süreci yönetilebilir adımlara bölelim:

## Adım 1: Çıktı Dizinini Tanımlayın

Öncelikle Excel dosyanızı nereye kaydetmek istediğinizi belirlemeniz gerekir. Bunu şu şekilde yapabilirsiniz:

```csharp
static string outputDir = "Your Document Directory"; // belge dizininizi burada belirtin
```

 Yer değiştirmek`"Your Document Directory"` gerçek dosya yolunuzla. Oluşturulan Excel dosyasının kaydedileceği yer burasıdır.

## Adım 2: Veri Öğeleri için Kullanıcı Tarafından Tanımlanan Bir Sınıf Oluşturun

Daha sonra içe aktarmayı planladığımız verileri yapılandıracak bir sınıf tanımlayacağız.

```csharp
class DataItems
{
    public int Number1 { get; set; }
    public int Number2 { get; set; }
    public string Formula1 { get; set; }
    public string Formula2 { get; set; }
}
```

 Bu`DataItems` Sınıf, Excel dosyasına yazacağımız ham tam sayıları ve formülleri tutacak. 

## Adım 3: Veri Öğelerini Tutmak İçin Bir Liste Başlatın

 Birden fazla örneğini tutmak için bir liste kullanacağız`DataItems` sınıf.

```csharp
List<DataItems> dis = new List<DataItems>();
```

## Adım 4: Listeye Veri Öğeleri Ekleyin

Şimdi listemize birkaç girdi ekleyelim. Her girdi iki sayı ve iki formül içerecek.

```csharp
// Her veri öğesini tanımlayın ve ekleyin
DataItems di = new DataItems();
di.Number1 = 2002;
di.Number2 = 3502;
di.Formula1 = "=SUM(A2,B2)";
di.Formula2 = "=HYPERLINK(\"https://www.aspose.com\",\"Aspose Web Sitesi\")";
dis.Add(di);

// Ek veri öğeleri için tekrarlayın
```

 Her birini özelleştirdiğinizden emin olun`DataItems` Benzersiz değerlere ve formüllere sahip örnek.

## Adım 5: Çalışma Kitabı Oluşturun ve Çalışma Sayfasına Erişin

Daha sonra çalışma kitabını oluşturup verileri içe aktaracağımız ilk çalışma sayfasına erişelim.

```csharp
Workbook wb = new Workbook(); // yeni bir çalışma kitabı oluştur
Worksheet ws = wb.Worksheets[0]; // ilk çalışma sayfasına erişin
```

## Adım 6: İçe Aktarma Tablosu Seçeneklerini Belirleyin

İşte sihir burada gerçekleşir. Verilerinizdeki hangi alanların formüllere karşılık geldiğini belirtmeniz gerekir. 

```csharp
ImportTableOptions opts = new ImportTableOptions();
opts.IsFormulas = new bool[] { false, false, true, true };
```

 Bu örnekte, son iki alan formülleri içerir ve bu da şu şekilde gösterilir:`true` , ilk iki alan ise`false`.

## Adım 7: Özel Nesneleri İçe Aktar

Artık her şey ayarlandığına göre, veri öğelerimizin listesini çalışma sayfasına aktaralım.

```csharp
ws.Cells.ImportCustomObjects(dis, 0, 0, opts);
```

Bu satır, verileri A1 hücresinden başlayarak etkili bir şekilde içe aktarır.

## Adım 8: Formülleri Hesaplayın

Bazı formülleri içe aktardığımız için bunları hesaplamak hayati önem taşıyor.

```csharp
wb.CalculateFormula();
```

Bu yöntem formüllerinizin bağımlılıklarına göre değerlendirilmesini sağlar.

## Adım 9: Sütunları Otomatik Olarak Sığdır

Verilerinizin görüntülenebilir olmasını sağlamak için, içeriğe göre sütunları otomatik olarak sığdırabilirsiniz.

```csharp
ws.AutoFitColumns();
```

Bu adım Excel dosyasının düzenini optimize eder. 

## Adım 10: Excel Dosyanızı Kaydedin

Son olarak yeni oluşturduğunuz Excel dosyanızı kaydetme zamanı geldi. 

```csharp
wb.Save(outputDir + "outputSpecifyFormulaFieldsWhileImportingDataToWorksheet.xlsx");
```

Çıktı dosyanızın adının konuyla ilgili ve açıklayıcı olduğundan emin olun!

## Adım 11: Uygulamayı Kontrol Etme

Her şeyin doğru şekilde çalıştığını doğrulamanın basit bir yolu olarak bir mesaj yazdırmak isteyebilirsiniz.

```csharp
Console.WriteLine("SpecifyFormulaFieldsWhileImportingDataToWorksheet executed successfully.");
```

Bu size kodun herhangi bir sorun olmadan çalıştığına dair anında geri bildirim sağlar.

## Çözüm

İşte karşınızda! Aspose.Cells for .NET ve belirtilen formül alanlarını kullanarak verileri bir Excel sayfasına başarıyla aktardınız. Bu adımları izleyerek, ihtiyaçlarınıza göre uyarlanmış veri işleme görevlerini otomatikleştirmek için benzer teknikleri uygulayabilirsiniz. İster raporlar için sayıları hesaplıyor olun, ister sadece verileri yönetiyor olun, Aspose ile Excel manipülasyon sanatında ustalaşmak sahip olunmaya değer bir beceridir.

## SSS

### Aspose.Cells Nedir?
Aspose.Cells, Excel dosyalarını program aracılığıyla oluşturmak, düzenlemek ve dönüştürmek için tasarlanmış bir .NET kütüphanesidir.

### Aspose.Cells for .NET'i nasıl kurarım?
 Bunu şuradan indirebilirsiniz:[Aspose sürümleri](https://releases.aspose.com/cells/net/) ve projenizde buna referans verin.

### Aspose.Cells'i ücretsiz kullanabilir miyim?
 Evet, Aspose şu adreste mevcut olan ücretsiz bir deneme sunuyor:[bu bağlantı](https://releases.aspose.com/).

### Daha fazla örneği nerede bulabilirim?
 Ek örnekler ve belgeler şu adreste bulunabilir:[Aspose dokümantasyon sayfası](https://reference.aspose.com/cells/net/).

### Aspose kullanırken sorunlarla karşılaşırsam ne olur?
 Aspose destek forumundan yardım alabilirsiniz[Burada](https://forum.aspose.com/c/cells/9).
 
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
