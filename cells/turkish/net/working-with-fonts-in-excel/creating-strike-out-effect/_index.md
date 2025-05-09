---
"description": "Bu detaylı adım adım eğitimde, Aspose.Cells for .NET ile Excel'de metne üstü çizili efektin nasıl uygulanacağını öğrenin."
"linktitle": "Excel'de Metinde Üstü Çizili Efekt Oluşturma"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": "Excel'de Metinde Üstü Çizili Efekt Oluşturma"
"url": "/tr/net/working-with-fonts-in-excel/creating-strike-out-effect/"
"weight": 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Metinde Üstü Çizili Efekt Oluşturma

## giriiş
Excel söz konusu olduğunda, görsel öğeler verilerin kendisi kadar önemlidir. Önemli değişiklikleri vurguluyor veya artık alakalı olmayan öğeleri işaretliyor olun, metindeki üstü çizili efekt, elektronik tablolarda görsel temsili yönetmenin klasik bir yoludur. Bu kılavuzda, .NET için Aspose.Cells kullanarak Excel'de metinde üstü çizili efekt uygulama sürecini adım adım ele alacağız. Bu eğitim yalnızca gerekli ön koşulları kapsamayacak, aynı zamanda bu efekti kolayca kopyalayabilmenizi sağlamak için adım adım bir yaklaşım da sağlayacaktır.
## Ön koşullar
Eğitime başlamadan önce aşağıdaki ön koşulların karşılandığından emin olun:
1. Geliştirme Ortamı: Bir .NET geliştirme ortamı kurmuş olmalısınız. Bu, Visual Studio veya .NET geliştirmeyi destekleyen tercih ettiğiniz herhangi bir IDE olabilir.
2. .NET için Aspose.Cells: Projenizde Aspose.Cells'in yüklü olduğundan emin olun. Aşağıdaki bağlantıdan indirebilirsiniz: [Aspose.Cells'i indirin](https://releases.aspose.com/cells/net/).
3. Temel C# Bilgisi: Örnekler C# ile kodlanacağı için C# programlamaya dair temel bir anlayışa sahip olmak faydalı olacaktır.
4. .NET Framework: Projenizin uyumlu bir .NET Framework sürümünü (genellikle .NET Core veya .NET Framework 4.5 ve üzeri) hedeflediğinden emin olun.
## Paketleri İçe Aktar
Herhangi bir kod yazmadan önce, Aspose.Cells'den gerekli ad alanlarını içe aktarmanız gerekir. Bu, kütüphane tarafından sağlanan çeşitli özelliklere erişmek için önemlidir. Gerekli ad alanlarını nasıl içe aktarabileceğiniz aşağıda açıklanmıştır:
```csharp
using System.IO;
using Aspose.Cells;
```
Bu içe aktarmalarla, bu eğitim boyunca kullanılacak Çalışma Kitabı, Çalışma Sayfası ve Stil sınıflarına erişebileceksiniz.
Artık sahneyi hazırladığımıza göre, süreci yönetilebilir adımlara bölelim. Her adım, Excel'de metinde bir çizgi efekti oluşturmanıza yardımcı olacak net talimatlarla birlikte sunulacaktır.
## Adım 1: Belge Dizinini Tanımlayın
Excel belgelerinizin depolanacağı yolu tanımlayarak başlayın. Bu, çıktı dosyalarınızı kaydedeceğiniz konum olacaktır.
```csharp
// Belgeler dizinine giden yol.
string dataDir = "Your Document Directory";
```
Yer değiştirmek `"Your Document Directory"` Excel dosyanızı kaydetmek istediğiniz gerçek dizin yolu ile. Bu, çıktınız için dizini ayarlar.
## Adım 2: Dizini Oluşturun
Daha sonra, önceki adımda belirttiğiniz dizinin var olduğundan emin olmanız gerekir. Eğer yoksa, onu programatik olarak oluşturabilirsiniz.
```csharp
// Eğer mevcut değilse dizin oluşturun.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Bu kod dizinin var olup olmadığını kontrol eder ve yoksa oluşturur. Bu, dosyanızı daha sonra kaydetmeye çalıştığınızda hatalardan kaçınmanıza yardımcı olur.
## Adım 3: Bir Çalışma Kitabı Nesnesi Oluşturun
Şimdi yeni bir Çalışma Kitabı nesnesi oluşturma zamanı. Bu, veri ekleyeceğiniz ve biçimleri uygulayacağınız Excel dosyanızın temelidir.
```csharp
// Bir Çalışma Kitabı nesnesini örnekleme
Workbook workbook = new Workbook();
```
The `Workbook` sınıf bir Excel dosyasını temsil eder. Bu sınıfın bir örneğini oluşturarak, aslında yeni bir Excel belgesi oluşturuyorsunuz.
## Adım 4: Yeni Bir Çalışma Sayfası Ekleyin
Her çalışma kitabı birden fazla çalışma sayfası içerebilir. Hadi devam edelim ve çalışma kitabınızda yeni bir çalışma sayfası oluşturalım.
```csharp
// Excel nesnesine yeni bir çalışma sayfası ekleme
int i = workbook.Worksheets.Add();
```
The `Add` yöntemi `Worksheets` koleksiyon çalışma kitabına yeni bir çalışma sayfası ekler ve dizinini döndürür. 
## Adım 5: Yeni Çalışma Sayfasının Referansını Edinin
Çalışma sayfasını oluşturduktan sonra, ilerideki işlemlerinizde bu sayfaya başvurmanız gerekir.
```csharp
// Yeni eklenen çalışma sayfasının referansını sayfa indeksini geçirerek elde etme
Worksheet worksheet = workbook.Worksheets[i];
```
Burada, yeni oluşturulan çalışma sayfasını dizinini ( kullanarak getiriyorsunuz`i`). Bu size çalışma sayfasını düzenleme erişimi sağlar.
## Adım 6: Bir Hücreye Erişim
Çalışma sayfanızda üstü çizili biçimi uygulayacağınız belirli bir hücreye erişmek isteyeceksiniz. Bu örnekte, hücreyi kullanıyoruz `A1`.
```csharp
// Çalışma sayfasından "A1" hücresine erişim
Aspose.Cells.Cell cell = worksheet.Cells["A1"];
```
Excel'de hücrelere sütun ve satır tanımlayıcıları ile başvurulur (örneğin, "A1"). Hücreye bir başvuru alıyoruz `A1` daha fazla manipülasyon için.
## Adım 7: Hücreye Değer Ekleyin
Sonra, hücreye biraz metin ekleyelim. Hücreye “Merhaba Aspose!” yazacağız `A1`.
```csharp
// "A1" hücresine bir değer ekleniyor
cell.PutValue("Hello Aspose!");
```
The `PutValue` yöntemi hücreye bir dize değeri atamak için kullanılır. Bu dizeyi istediğiniz herhangi bir şeyle değiştirebilirsiniz.
## Adım 8: Hücre Stilini Edinin
Artık hücremizde metin olduğuna göre, istediğimiz biçimlendirmeyi (üstü çizili efekt dahil) uygulamak için hücrenin stiline erişmenin zamanı geldi.
```csharp
// Hücre stilinin elde edilmesi
Style style = cell.GetStyle();
```
The `GetStyle` yöntemi hücrenin geçerli stilini alır ve yazı tipi, boyutu ve efektler gibi özellikleri değiştirmenize olanak tanır.
## Adım 9: Üstü Çizili Etkiyi Ayarlayın
Hücredeki metne üstü çizili efekti uygulayalım. Hücrenin yazı tipi stilini değiştireceğiz.
```csharp
// ExStart:SetStrikeout
// Yazı tipinde çizgi efektini ayarlama
style.Font.IsStrikeout = true;
// ExEnd:SetÜzeriÇıkar
```
Ayarlayarak `IsStrikeout` doğruysa, Excel'e seçili hücredeki metni görsel olarak üstü çizili olarak çizmesini söylüyorsunuz; tıpkı bir şeyi listeden görsel olarak işaretlemek gibi.
## Adım 10: Stili Hücreye Uygula
Stili değiştirdikten sonra değişiklikleri yansıtmak için hücreye geri uygulamanız gerekir.
```csharp
// Stili hücreye uygulama
cell.SetStyle(style);
```
The `SetStyle` yöntemi, hücreyi artık üstü çizili biçimlendirmeyi de içeren yeni stille günceller.
## Adım 11: Excel Dosyasını Kaydedin
Son olarak, çalışma kitabınızı belirtilen dizine kaydetme zamanı geldi. Bu örnekte, dosyayı şu adla kaydediyoruz: `book1.out.xls`.
```csharp
// Excel dosyasını kaydetme
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
The `Save` method çalışma kitabını diske 97-2003 Excel biçiminde yazar. Gerekirse farklı biçimler belirtebilirsiniz.
## Çözüm
Aspose.Cells for .NET kullanarak Excel'de metinde bir çizgi efekti oluşturmak, adım adım parçalara ayırdığınızda basit bir işlemdir. Bu kılavuzu izleyerek, artık elektronik tablolarınızı görsel ipuçlarıyla zenginleştirme ve verilerinizi yalnızca bilgilendirici değil aynı zamanda görsel olarak ilgi çekici hale getirme becerisine sahipsiniz.
## SSS
### Aspose.Cells Nedir?
Aspose.Cells, .NET uygulamalarında Excel dosyalarını yönetmek için güçlü bir kütüphanedir ve Excel belgelerini programlı bir şekilde oluşturmanıza, düzenlemenize ve dönüştürmenize olanak tanır.
### Aspose.Cells'i ücretsiz kullanabilir miyim?
Evet, deneme süresi boyunca ücretsiz kullanabilirsiniz. Ücretsiz deneme şu adreste mevcuttur: [Aspose.Cells Ücretsiz Deneme](https://releases.aspose.com/).
### Aspose.Cells'i nasıl satın alabilirim?
Aspose.Cells için bir lisansı web siteleri üzerinden satın alabilirsiniz [Aspose.Cells'i satın alın](https://purchase.aspose.com/buy).
### Aspose.Cells kullanımına yönelik örnekler var mı?
Evet, burada bol miktarda örnek ve kod parçacığı bulabilirsiniz. [Aspose.Cells Belgeleri](https://reference.aspose.com/cells/net/).
### Aspose.Cells için desteği nereden alabilirim?
Topluluk desteği ve yardımı alabilirsiniz [Aspose Forum](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}