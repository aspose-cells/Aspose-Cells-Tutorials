---
"description": "Bu kapsamlı adım adım kılavuzla .NET'te Aspose.Cells kullanarak Excel satırlarını nasıl otomatik filtreleyeceğinizi zahmetsizce öğrenin."
"linktitle": "Excel'de Otomatik Filtre Şu Şekilde Başlar"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": "Excel'de Otomatik Filtre Şu Şekilde Başlar"
"url": "/tr/net/excel-autofilter-validation/autofilter-begins-with-in-excel/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Otomatik Filtre Şu Şekilde Başlar

## giriiş

Verilerle çalışmaya gelince, Excel sayısız sektör ve amaç için başvurulacak bir uygulama olarak kendini kanıtlamıştır. En güçlü özelliklerinden biri, kapsamlı veri kümelerini elemeyi çocuk oyuncağı haline getiren AutoFilter'dır. .NET için Aspose.Cells kullanıyorsanız, bu işlevsellikten programatik olarak yararlanabilir ve veri yönetimi görevlerinizi önemli ölçüde geliştirebilirsiniz. Bu kılavuzda, Excel satırlarını belirli bir dizeyle başlayıp başlamadıklarına göre filtreleyen bir özelliği uygulama sürecinde size yol göstereceğiz.

## Ön koşullar

Başlamadan önce aşağıdaki ön koşulların mevcut olduğundan emin olun:

1. Geliştirme Ortamı: .NET geliştirme ortamına aşina olun. Bu, Visual Studio veya seçtiğiniz herhangi bir IDE olabilir.
2. Aspose.Cells for .NET: Aspose.Cells for .NET'in yüklü olması gerekir. Bunu henüz yapmadıysanız, rahatlıkla indirebilirsiniz [Burada](https://releases.aspose.com/cells/net/).
3. Temel C# Bilgisi: C# hakkında temel bir anlayışa sahip olmak ve .NET kütüphaneleriyle nasıl çalışılacağını bilmek, sorunsuz bir şekilde ilerlemenize yardımcı olacaktır.
4. Örnek Veriler: Tercihen şu isimde bir Excel dosyanız olmalıdır: `sourseSampleCountryNames.xlsx`, belirlediğiniz kaynak dizininde bulunur. Bu dosya filtreleyeceğimiz verileri içerecektir.
5. Lisanslama: Tam işlevsellik için, bu yolla bir lisans edinmeyi düşünün [bağlantı](https://purchase.aspose.com/buy)Özellikleri test etmek istiyorsanız, bir talepte bulunabilirsiniz. [geçici lisans](https://purchase.aspose.com/temporary-license/).

Her şey hazır mı? Hadi gidelim!

## Paketleri İçe Aktar

Başlamak için, gerekli ad alanlarını C# dosyanızın en üstüne aktarın:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Bu, konsol etkileşimi için güveneceğimiz temel sistem özelliklerinin yanı sıra temel Aspose.Cells işlevselliğini içe aktarır.

Artık ortamınız kurulu ve gerekli paketler içe aktarılmış durumda, Autofilter özelliğini yönetilebilir adımlara bölelim. "Ba" ile başlayan satırları çıkaran bir filtre uygulayacağız.

## Adım 1: Kaynak ve Çıktı Dizinlerini Tanımlayın

Öncelikle, giriş Excel dosyamızın nerede bulunacağını ve filtrelenmiş çıktımızı nereye kaydetmek istediğimizi tanımlayalım:

```csharp
// Kaynak dizini
string sourceDir = "Your Document Directory\\";

// Çıktı dizini
string outputDir = "Your Document Directory\\";
```

Açıklama: Burada, şunu değiştirin `"Your Document Directory\\"` dizinlerinize giden gerçek yol ile. Dizin yollarını çift ters eğik çizgi ( ile sonlandırdığınızdan emin olun`\\`) herhangi bir yol sorununu önlemek için.

## Adım 2: Çalışma Kitabı Nesnesini Örneklendirin

Daha sonra Excel dosyamıza işaret eden bir Çalışma Kitabı nesnesi oluşturacağız:

```csharp
// Örnek verileri içeren bir Çalışma Kitabı nesnesini örnekleme
Workbook workbook = new Workbook(sourceDir + "sourseSampleCountryNames.xlsx");
```

Açıklama: Bu satır belirtilen dosya yolunu kullanarak yeni bir Çalışma Kitabı örneği başlatır. `Workbook` sınıf, Excel dosyasının tamamını temsil ettiği için temeldir.

## Adım 3: İlk Çalışma Sayfasına Erişim

Şimdi, üzerinde çalışmak istediğimiz belirli çalışma sayfasına erişmemiz gerekiyor:

```csharp
// Excel dosyasındaki ilk çalışma sayfasına erişim
Worksheet worksheet = workbook.Worksheets[0];
```

Açıklama: `Worksheets` koleksiyon bize bireysel sayfalara erişmemizi sağlar. `[0]` Excel dosyanızdaki ilk çalışma sayfasına başvurur; bu, genellikle tek sayfalık bir dosyayla çalışırken yaygın bir uygulamadır.

## Adım 4: Otomatik Filtreyi Ayarlama

İşte sihir burada başlıyor! Verilerimiz için bir AutoFilter aralığı oluşturacağız:

```csharp
// Hücrelere aralık vererek Otomatik Filtre oluşturma
worksheet.AutoFilter.Range = "A1:A18";
```

Açıklama: `AutoFilter.Range` özelliği, hangi satırların filtreleneceğini belirtmenize olanak tanır. Bu durumda, verilerimizi tuttuğu varsayılan A1 ila A18 aralığındaki satırları filtreliyoruz.

## Adım 5: Filtre Koşulunu Uygula

Bir sonraki adım filtre koşulunu tanımlamaktır. Sadece ilk sütun değerleri "Ba" ile başlayan satırları görüntülemek istiyoruz:

```csharp
// "Ba" dizesiyle başlayan satırlar için filtreyi başlat
worksheet.AutoFilter.Custom(0, FilterOperatorType.BeginsWith, "Ba");
```

Açıklama: `Custom` yöntem filtreleme mantığımızı tanımlar. İlk argüman (`0`) ilk sütuna (A) göre filtreleme yaptığımızı gösterir ve `FilterOperatorType.BeginsWith` "Ba" ile başlayan satırları arama koşulumuzu belirtir.

## Adım 6: Filtreyi Yenileyin

Filtre koşulumuzu uyguladıktan sonra, Excel'in değişiklikleri yansıtacak şekilde yenilendiğinden emin olmamız gerekir:

```csharp
// Filtrelenen satırları göstermek/gizlemek için filtreyi yenileyin
worksheet.AutoFilter.Refresh();
```

Açıklama: Bu satır, görünür satırların uygulanan filtre ölçütlerine karşılık geldiğinden emin olmak için AutoFilter'da bir yenilemeyi çağırır. Excel'deki yenileme düğmesine basmaya benzer.

## Adım 7: Değiştirilen Excel Dosyasını Kaydedin

Şimdi yaptığımız değişiklikleri kaydetme zamanı:

```csharp
// Değiştirilen Excel dosyasını kaydetme
workbook.Save(outputDir + "outSourseSampleCountryNames.xlsx");
```

Açıklama: `Save` method, değiştirilen Çalışma Kitabını belirtilen çıktı yoluna geri yazar. Bu, özgün verilerinizin bozulmadan kalması için tanımlı filtrelerinizi yeni bir dosyaya yazma kapsamına girer.

## Adım 8: Çıktı Onayı

Son olarak işlemimizin başarılı olduğunu teyit edelim:

```csharp
Console.WriteLine("AutofilterBeginsWith executed successfully.\r\n");
```

Açıklama: Bu basit satır, filtreleme işleminin hatasız tamamlandığını konsola bildiren bir onay mesajı çıkarır.

## Çözüm

Veri yönetiminin bunaltıcı hissettirebildiği bir dünyada, Excel'de Aspose.Cells for .NET aracılığıyla AutoFilter gibi özelliklerde ustalaşmak, verileri etkili ve verimli bir şekilde yönetmenizi sağlar. "Ba" ile başlayan Excel satırlarını nasıl filtreleyeceğinizi öğrendiniz ve yöntemi adım adım uyguladınız. Pratik yaparak, bu yöntemi devam eden projelerinizdeki çeşitli veri filtreleme ihtiyaçlarınıza uyarlayabileceksiniz.

## SSS

### Excel'de AutoFilter'ın amacı nedir?  
AutoFilter, kullanıcıların bir elektronik tablodaki verileri hızla sıralamasına ve filtrelemesine olanak tanır ve böylece belirli veri kümelerine odaklanmayı kolaylaştırır.

### Aspose.Cells ile birden fazla kritere göre filtreleme yapabilir miyim?  
Evet, Aspose.Cells birden fazla kriter belirlemenize olanak tanıyan gelişmiş filtreleme seçeneklerini destekler.

### Aspose.Cells'i kullanabilmek için lisansa ihtiyacım var mı?  
Ücretsiz deneme sürümüyle başlayabilirsiniz ancak tüm işlevlerin kullanılabilmesi ve deneme sürümü sınırlamalarının kaldırılabilmesi için lisans gereklidir.

### Aspose.Cells kullanarak hangi filtreleme türlerini gerçekleştirebilirim?  
Verileri değere, koşula (örneğin şununla başlar veya şununla biter) göre filtreleyebilir ve özel gereksinimlerinizi karşılamak için özel filtreleme yapabilirsiniz.

### Aspose.Cells for .NET hakkında daha fazla bilgiyi nerede bulabilirim?  
Belgeleri kontrol edebilirsiniz [Burada](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}