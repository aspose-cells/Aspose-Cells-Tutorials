---
"description": "Bu adım adım eğitimde Aspose.Cells for .NET kullanarak Excel çalışma sayfasına Spinner denetiminin nasıl ekleneceğini öğrenin."
"linktitle": "Excel'de Çalışma Sayfasına Spinner Denetimi Ekleme"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": "Excel'de Çalışma Sayfasına Spinner Denetimi Ekleme"
"url": "/tr/net/excel-shapes-controls/add-spinner-control-to-worksheet-excel/"
"weight": 23
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Çalışma Sayfasına Spinner Denetimi Ekleme

## giriiş
.NET kullanarak Excel otomasyon dünyasına dalıyorsanız, muhtemelen elektronik tablolarınızda daha etkileşimli denetimlere ihtiyaç duyduğunuzu fark etmişsinizdir. Bu denetimlerden biri de kullanıcıların bir değeri kolayca artırmasına veya azaltmasına olanak tanıyan Spinner'dır. Bu eğitimde, .NET için Aspose.Cells kullanarak bir Excel çalışma sayfasına Spinner denetiminin nasıl ekleneceğini inceleyeceğiz. Bunu, sorunsuz bir şekilde takip edebilmeniz için sindirilebilir adımlara böleceğiz. 
## Ön koşullar
Koda geçmeden önce, sorunsuz bir deneyim için her şeyin ayarlandığından emin olalım:
1. .NET için Aspose.Cells: Aspose.Cells kütüphanesine sahip olduğunuzdan emin olun. Henüz yüklemediyseniz, en son sürümü şu adresten alabilirsiniz: [indirme bağlantısı](https://releases.aspose.com/cells/net/).
2. Visual Studio: Visual Studio'nun veya tercih ettiğiniz herhangi bir .NET IDE'nin çalışan bir kurulumuna sahip olmalısınız.
3. C# Temel Bilgisi: C# programlamaya aşinalık kod parçacıklarını kolayca anlamanıza yardımcı olacaktır. Eğer yeni başlıyorsanız endişelenmeyin! Her bir bölümde size yol göstereceğim.
## Paketleri İçe Aktar
Projenizde Aspose.Cells kullanmak için gerekli ad alanlarını içe aktarmanız gerekir. Ortamınızı şu şekilde ayarlayabilirsiniz:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Bu ad alanları, Spinner gibi şekiller için çalışma kitabı düzenleme ve çizim yetenekleri de dahil olmak üzere Aspose.Cells'in temel işlevlerine erişmenizi sağlar.
Artık ön koşulları ele aldığımıza ve gerekli paketleri içe aktardığımıza göre, adım adım kılavuza geçelim. Her adım, kolayca uygulayabilmeniz için açık ve öz olacak şekilde tasarlanmıştır.
## Adım 1: Proje Dizininizi Ayarlayın
Kodlamaya başlamadan önce dosyalarınızı organize etmek iyi bir uygulamadır. Excel dosyalarımız için bir dizin oluşturalım.
```csharp
// Belgeler dizinine giden yol.
string dataDir = "Your Document Directory";
// Eğer mevcut değilse dizin oluşturun.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Burada, belge dizinimiz için bir yol belirtiyoruz. Dizin yoksa, onu oluşturuyoruz. Bu, oluşturulan tüm dosyalarımızın belirlenmiş bir ana dizine sahip olmasını sağlar.
## Adım 2: Yeni Bir Çalışma Kitabı Oluşturun
Şimdi Spinner kontrolümüzü ekleyeceğimiz Excel çalışma kitabını oluşturmanın zamanı geldi.
```csharp
// Yeni bir Çalışma Kitabı örneği oluşturun.
Workbook excelbook = new Workbook();
```
The `Workbook` sınıfı bir Excel dosyasını temsil eder. Bunu örnekleyerek, değişikliklere hazır yeni bir çalışma kitabı oluştururuz.
## Adım 3: İlk Çalışma Sayfasına Erişim
Spinner'ımızı çalışma kitabındaki ilk çalışma sayfasına ekleyeceğiz.
```csharp
// İlk çalışma kağıdını al.
Worksheet worksheet = excelbook.Worksheets[0];
```
Bu satır çalışma kitabımızdan ilk çalışma sayfasına (indeks 0) erişir. Birden fazla çalışma sayfanız olabilir, ancak bu örnek için bunu basit tutacağız.
## Adım 4: Hücrelerle Çalışın
Şimdi, çalışma sayfamızdaki hücrelerle çalışalım. Bazı değerler ve stiller belirleyeceğiz.
```csharp
// Çalışma sayfası hücrelerini alın.
Cells cells = worksheet.Cells;
// A1 hücresine bir dize değeri girin.
cells["A1"].PutValue("Select Value:");
// Hücrenin yazı rengini ayarlayın.
cells["A1"].GetStyle().Font.Color = Color.Red;
// Yazı tipini kalın olarak ayarlayın.
cells["A1"].GetStyle().Font.IsBold = true;
// A2 hücresine değer girin.
cells["A2"].PutValue(0);
```
Burada, A1 hücresini bir istemle dolduruyoruz, kırmızı bir renk uyguluyoruz ve metni kalınlaştırıyoruz. Ayrıca A2 hücresini Spinner'ımıza bağlanacak olan 0 başlangıç değerine ayarlıyoruz.
## Adım 5: A2 Hücresini Şekillendirin
Şimdi A2 hücresine görsel olarak daha çekici hale getirmek için bazı stiller uygulayalım.
```csharp
// Gölgelendirme rengini siyah, arka planı ise düz olarak ayarlayın.
cells["A2"].GetStyle().ForegroundColor = Color.Black;
cells["A2"].GetStyle().Pattern = BackgroundType.Solid;
// Hücrenin yazı rengini ayarlayın.
cells["A2"].GetStyle().Font.Color = Color.White;
// Yazı tipini kalın olarak ayarlayın.
cells["A2"].GetStyle().Font.IsBold = true;
```
A2 hücresine düz desenli siyah bir arka plan ekliyoruz ve yazı tipi rengini beyaz olarak ayarlıyoruz. Bu kontrast, çalışma sayfasında öne çıkmasını sağlayacaktır.
## Adım 6: Spinner Kontrolünü Ekleyin
Artık Spinner denetimini çalışma sayfamıza eklemeye hazırız.
```csharp
// Bir spinner kontrolü ekleyin.
Aspose.Cells.Drawing.Spinner spinner = excelbook.Worksheets[0].Shapes.AddSpinner(1, 0, 1, 0, 20, 18);
```
Bu satır çalışma sayfasına bir Spinner denetimi ekler. Parametreler Spinner'ın konumunu ve boyutunu belirtir (satır, sütun, genişlik, yükseklik).
## Adım 7: Spinner Özelliklerini Yapılandırın
Spinner'ın davranışını ihtiyaçlarımıza uyacak şekilde özelleştirelim.
```csharp
// Spinner'ın yerleşim türünü ayarlayın.
spinner.Placement = PlacementType.FreeFloating;
// Kontrol için bağlantılı hücreyi ayarlayın.
spinner.LinkedCell = "A2";
// Maksimum değeri ayarlayın.
spinner.Max = 10;
// Minimum değeri ayarlayın.
spinner.Min = 0;
// Kontrol için artış değişikliğini ayarlayın.
spinner.IncrementalChange = 2;
// 3 boyutlu gölgelendirmeyi ayarlayın.
spinner.Shadow = true;
```
Burada, Spinner'ın özelliklerini ayarlıyoruz. Bunu A2 hücresine bağlıyoruz ve orada görüntülenen değeri kontrol etmesini sağlıyoruz. Minimum ve maksimum değerler, Spinner'ın içinde çalışabileceği aralığı tanımlarken, artımlı değişiklik, değerin her tıklamayla ne kadar değiştiğini ayarlar. 3 boyutlu gölgelendirme eklemek ona cilalı bir görünüm kazandırır.
## Adım 8: Excel Dosyasını Kaydedin
Son olarak Spinner'ı da içeren Excel çalışma kitabımızı kaydedelim.
```csharp
// Excel dosyasını kaydedin.
excelbook.Save(dataDir + "book1.out.xls");
```
Bu komut çalışma kitabını belirtilen dizine kaydeder. Dosya adını gerektiği gibi değiştirebilirsiniz.
## Çözüm
İşte oldu! Aspose.Cells for .NET kullanarak bir Excel çalışma sayfasına Spinner denetimini başarıyla eklediniz. Bu etkileşimli öğe, değerlerde hızlı ayarlamalar yapılmasına izin vererek kullanıcı deneyimini geliştirir. Dinamik bir raporlama aracı veya bir veri girişi formu oluşturuyor olun, Spinner denetimi değerli bir ekleme olabilir. 
## SSS
### Excel'de Spinner denetimi nedir?
Spinner denetimi, kullanıcıların sayısal bir değeri kolayca artırmasına veya azaltmasına olanak tanır ve seçimler yapmak için sezgisel bir yol sağlar.
### Spinner'ın görünümünü özelleştirebilir miyim?
Evet, daha cilalı bir görünüm için boyutunu, konumunu ve hatta 3 boyutlu gölgelendirmesini değiştirebilirsiniz.
### Aspose.Cells'i kullanmak için lisansa ihtiyacım var mı?
Aspose.Cells ücretsiz deneme sunuyor ancak üretim kullanımı için ücretli bir lisans gerekiyor. Şuraya göz atın: [satın alma seçenekleri](https://purchase.aspose.com/buy).
### Aspose.Cells konusunda nasıl yardım alabilirim?
Destek için şu adresi ziyaret edin: [Aspose forumu](https://forum.aspose.com/c/cells/9) Sorularınızı sorabileceğiniz ve cevap bulabileceğiniz yer.
### Aynı çalışma sayfasına birden fazla Spinner eklemek mümkün müdür?
Kesinlikle! Her kontrol için aynı adımları izleyerek ihtiyacınız kadar Spinner ekleyebilirsiniz.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}