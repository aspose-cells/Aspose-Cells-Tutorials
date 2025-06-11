---
"description": "Aspose.Cells for .NET kullanarak Excel'deki hücrelere yorum eklemeyi öğrenin. Excel işlevselliğini geliştirmek için yeni başlayanlar için adım adım kılavuz."
"linktitle": "Excel'de Hücrelere veya Şekillere Yorum Ekleme"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": "Excel'de Hücrelere veya Şekillere Yorum Ekleme"
"url": "/tr/net/excel-comment-annotation/add-comments-to-cells-or-shapes-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Hücrelere veya Şekillere Yorum Ekleme

## giriiş
Hücrelere veya şekillere yorum ekleyerek Excel belgelerinizi geliştirmek mi istiyorsunuz? Doğru yerdesiniz! Bu makale, Excel dosyalarınıza yorumları etkili bir şekilde eklemek için Aspose.Cells for .NET'i kullanmanızda size rehberlik edecektir. Geri bildirim, açıklama veya sadece dostça bir not sağlamak isteyip istemediğinize bakılmaksızın, sorunsuz bir şekilde takip edebilmeniz için adım adım açıklayacağız. O halde sanal araç kutunuzu alın ve başlayalım!
## Ön koşullar
Excel sayfalarına yorum ekleme yolculuğumuza başlamadan önce, ihtiyacınız olan her şeye sahip olduğunuzdan emin olalım. İşte yerinde olması gerekenler:
- Visual Studio Kurulu: .NET uygulamalarınızı yazabileceğiniz ve derleyebileceğiniz bir IDE'ye ihtiyacınız olacak. Visual Studio birçok geliştirici için popüler bir seçimdir.
- Aspose.Cells Paketi: Aspose.Cells kütüphanesinin yüklü olduğundan emin olun. Excel dosyalarını düzenlemek için sağlam bir araçtır. Bunu şuradan indirebilirsiniz: [yayın sayfası](https://releases.aspose.com/cells/net/).
- Temel C# Bilgisi: Tüm örneklerde bu programlama dili kullanılacağından, C# programlamaya dair temel bir anlayışa sahip olmak faydalı olacaktır.
- Aspose.Cells Lisansı: Genişletilmiş özellikler için bir lisans satın almayı düşünebilirsiniz, ancak bir lisansla da başlayabilirsiniz. [ücretsiz deneme](https://releases.aspose.com/), sınırlamalarla birlikte gelir.
## Paketleri İçe Aktar
Aspose.Cells ile çalışmaya başlamak için yapmanız gereken ilk şey, C# projenize gerekli paketleri içe aktarmaktır. İşte nasıl yapacağınız:
### Projenizi Açın
Mevcut projenizi Visual Studio'da açın veya sıfırdan başlıyorsanız yeni bir proje oluşturun.
### Aspose.Cells'i yükleyin
Aspose.Cells paketini NuGet'ten kolayca yükleyebilirsiniz. İşte nasıl:
1. Çözüm Gezgini’nde projenizin üzerine sağ tıklayın.
2. "NuGet Paketlerini Yönet" seçeneğini seçin.
3. "Aspose.Cells" ifadesini arayın ve en son sürümü yükleyin.
### Using Statement'ı ekleyin
Kod dosyanızın en üstüne aşağıdaki using yönergesini ekleyin:
```csharp
using System.IO;
using Aspose.Cells;
```
Artık Aspose.Cells ile Excel dosyalarında işlem yapmaya hazırsınız. 

Ön koşullar halledildikten sonra, rehberin özüne geçelim: Excel dosyasındaki hücrelere veya şekillere yorum ekleme. Bunu adım adım ele alacağız.
## Adım 1: Belge Dizinini Ayarlama
Çalışma Kitabını düzenlemeye başlamadan önce, belgemizin nerede saklanacağını tanımlamamız gerekir. İşte belge dizininizi ayarlama yöntemi.
```csharp
// Belgeler dizinine giden yol.
string dataDir = "Your Document Directory";
// Eğer mevcut değilse dizin oluşturun.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Burada, dizinin var olup olmadığını kontrol ediyoruz. Yoksa, onu oluşturuyoruz. Mobilyalarınızı düzenlemeye başlamadan önce bir eviniz olduğundan emin olmak gibi!
## Adım 2: Bir Çalışma Kitabı Nesnesi Oluşturma
Şimdi tüm sihrimizi göstereceğimiz yeni bir Çalışma Kitabı örneği oluşturmamız gerekiyor.
```csharp
// Bir Çalışma Kitabı nesnesini örnekleme
Workbook workbook = new Workbook();
```
Çalışma Kitabını, Excel şaheserinizi çizebileceğiniz boş bir tuval olarak düşünün. 
## Adım 3: Yeni Bir Çalışma Sayfası Ekleme
Bir Excel dosyası birden fazla sayfa içerebilir. Çalışma kitabımıza yeni bir çalışma sayfası ekleyelim.
```csharp
// Çalışma Kitabı nesnesine yeni bir çalışma sayfası ekleme
int sheetIndex = workbook.Worksheets.Add();
```
Her büyük sanatçının boş bir tuvale ihtiyacı vardır. İşte, biz bir tane ekliyoruz!
## Adım 4: Yeni Çalışma Sayfasına Erişim
Daha sonra, değişiklik yapmaya başlamak için yeni çalışma sayfasına bir referans alın.
```csharp
// Yeni eklenen çalışma sayfasının referansını sayfa indeksini geçirerek elde etme
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
Bu adım, yeni eklediğiniz sayfayla doğrudan çalışmanıza, yani çalışma tezgahınıza erişmenize olanak sağladığı için önemlidir.
## Adım 5: F5 Hücresine Yorum Ekleme
Şimdi heyecan verici kısma geçelim — belirli bir hücreye yorum ekleme. Bu durumda, "F5" hücresine yorum yapacağız.
```csharp
// "F5" hücresine yorum ekleme
int commentIndex = worksheet.Comments.Add("F5");
```
Bunu, çalışmanızın belirli bir bölümüne yapışkan bir not iliştirmek gibi düşünün. Düşüncelerinizi hatırlamanıza yardımcı olur!
## Adım 6: Yeni Eklenen Yorumlara Erişim
Yorumumuzu özelleştirmek için, ekledikten hemen sonra yorumumuza erişmemiz gerekiyor.
```csharp
// Yeni eklenen yoruma erişim
Comment comment = worksheet.Comments[commentIndex];
```
Bu adımda yapışkan notumuzu alıp üzerine düşüncelerimizi yazacağız.
## Adım 7: Yorum Notunu Ayarlama
Şimdi notumuzu yazmanın zamanı geldi. Yoruma biraz metin ekleyelim.
```csharp
// Yorum notunu ayarlama
comment.Note = "Hello Aspose!";
```
Bunu yapışkan notunuza yazmak gibi düşünün. Düşüncelerinizi kelimelere döküyorsunuz!
## Adım 8: Excel Dosyasını Kaydetme
Son olarak, sıkı çalışmamızı kaydetmemiz gerekiyor. Bu, yorumumuzu da içeren çalışma kitabını kaydedecektir!
```csharp
// Excel dosyasını kaydetme
workbook.Save(dataDir + "book1.out.xls");
```
Bu adım, harika bir hikaye yazdıktan sonra kitabınızı kapatmaya benzer; hikayenizin kaydedildiğinden emin olmak istersiniz!
## Çözüm
İşte oldu! Aspose.Cells for .NET kullanarak bir Excel dosyasındaki hücrelere yorumları başarıyla eklediniz. Yorumlar, işbirlikli projeler için veya sadece kendinize hatırlatıcılar bırakmak için kullanışlı olabilir. Artık tüm süreci tamamladığınıza göre, Excel becerilerinizi bir üst seviyeye taşımaya hazırsınız.
## SSS
### Aspose.Cells kullanarak şekillere yorum ekleyebilir miyim?
Evet! Hücrelere yaptığınız gibi şekillere de yorum ekleyebilirsiniz.
### Aspose.Cells hangi dosya formatlarını destekler?
Aspose.Cells, XLS, XLSX, CSV ve daha fazlası dahil olmak üzere çeşitli formatları destekler.
### Aspose.Cells'i kullanmak ücretsiz mi?
Aspose.Cells ücretsiz deneme sürümü sunuyor, ancak tüm özelliklerden yararlanmak için lisans satın almanız gerekebilir.
### Aspose.Cells için desteği nereden bulabilirim?
Destek almak için şu adresi ziyaret edebilirsiniz: [Aspose forumu](https://forum.aspose.com/c/cells/9).
### Aspose.Cells için geçici lisansı nasıl alabilirim?
Geçici lisans, aşağıdaki kaynaklardan alınabilir: [Aspose lisans sayfası](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}