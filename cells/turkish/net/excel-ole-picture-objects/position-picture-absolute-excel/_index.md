---
"description": "Bu kapsamlı adım adım eğitimle Aspose.Cells for .NET kullanarak Excel'de görsellerin nasıl mutlak şekilde konumlandırılacağını öğrenin."
"linktitle": "Excel'de Pozisyon Resmi (Mutlak)"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": "Excel'de Pozisyon Resmi (Mutlak)"
"url": "/tr/net/excel-ole-picture-objects/position-picture-absolute-excel/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Pozisyon Resmi (Mutlak)

## giriiş
Kendinizi hiç Excel elektronik tablosunda resimleri doğru şekilde konumlandırmakta zorlanırken buldunuz mu? Yalnız değilsiniz! Birçok kullanıcı, özellikle veri görselleştirme ihtiyaçları daha iyi estetik veya netlik için mutlak konumlandırma gerektirdiğinde bu zorlukla karşı karşıyadır. Daha fazla aramayın; bu kılavuz, Aspose.Cells for .NET kullanarak resimleri bir Excel çalışma sayfasında mutlak olarak konumlandırmanın basit sürecinde size yol gösterecektir. İster Excel manipülasyonu üzerinde çalışan bir geliştirici olun, ister raporlarınızı geliştirmek isteyen bir veri analisti olun, adım adım eğitimimiz resimlerle Excel deneyimlerinizi basitleştirmek için burada!
## Ön koşullar
Koda ve ayrıntılara dalmadan önce hazır bulundurmanız gereken birkaç şey var:
1. Aspose.Cells kütüphanesi: Aspose.Cells for .NET kütüphanesinin en son sürümüne sahip olduğunuzdan emin olun. Bunu şuradan indirebilirsiniz: [sürüm sayfası](https://releases.aspose.com/cells/net/).
2. Geliştirme Ortamı: Çalışan bir .NET geliştirme ortamı kurduğunuzdan emin olun. Visual Studio veya seçtiğiniz herhangi bir IDE'yi kullanabilirsiniz.
3. Temel C# Bilgisi: Kod parçacıklarını anlamak için C# programlama diline aşina olmak faydalı olacaktır.
4. Resim Dosyası: Excel sayfanıza eklemeyi planladığınız belirlenmiş belge dizininde kayıtlı bir resim dosyanız (örneğin, “logo.jpg”) olsun.

## Paketleri İçe Aktar
Başlamak için, projemiz için gerekli paketleri içe aktardığımızdan emin olalım. Proje dosyanız aşağıdaki ad alanlarını içermelidir:
```csharp
using System.IO;
using Aspose.Cells;
```
Bu ad alanlarını içe aktararak programımızın Aspose.Cells tarafından sağlanan özelliklerden yararlanabilmesini sağlıyoruz.
Daha anlaşılır olması için bunu yönetilebilir adımlara bölelim.
## Adım 1: Belge Dizininizi Ayarlayın
Bu ilk adımda, belgelerinizin bulunduğu dizini tanımlamanız gerekir. Bu, programın dosyaları nereye kaydedeceğini veya getireceğini bilmesi için önemlidir. Bunu nasıl ayarlayabileceğiniz aşağıda açıklanmıştır:
```csharp
string dataDir = "Your Document Directory";
```
Basitçe değiştirin `"Your Document Directory"` görüntü dosyanızın bulunduğu gerçek yol ile. Bu, aşağıdaki gibi bir şey olabilir `"C:\\Users\\YourUsername\\Documents\\"`.
## Adım 2: Bir Çalışma Kitabı Nesnesi Oluşturma
Daha sonra, yeni bir örnek oluşturmanız gerekir `Workbook` sınıf. Bu nesne Excel dosyanızı temsil eder:
```csharp
Workbook workbook = new Workbook();
```
Bu noktada elinizde veri ve görsellerle doldurulmaya hazır bir çalışma kitabı var.
## Adım 3: Yeni Bir Çalışma Sayfası Ekleme
Artık çalışma kitabınız olduğuna göre, ona bir çalışma sayfası eklemeniz gerekiyor. Resimleri ekleme ve konumlandırmanın sihrinin gerçekleşeceği yer burasıdır:
```csharp
int sheetIndex = workbook.Worksheets.Add();
```
Bu satır, çalışma kitabınız içinde yeni bir çalışma sayfası oluşturur ve değişkende sakladığımız dizinini döndürür. `sheetIndex`.
## Adım 4: Yeni Çalışma Sayfasını Elde Etme
Yeni oluşturulan çalışma sayfasına başvuralım. Az önce aldığımız dizini kullanarak çalışma sayfasına erişebilir ve onu düzenleyebiliriz:
```csharp
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
Artık bununla çalışabilirsiniz `worksheet` Resim dahil içerik ekleme nesnesi.
## Adım 5: Resim Ekleme
Şimdi heyecan verici kısma geçelim! Resmi çalışma sayfamıza ekleyeceğimiz yer burası. Resmin sabitlenmesini istediğimiz satır ve sütun dizinlerini belirtiyoruz (bu durumda, satır 5 ve sütun 5 olan "F6" hücresinde):
```csharp
int pictureIndex = worksheet.Pictures.Add(5, 5, dataDir + "logo.jpg");
```
Bu satır, resmi tüm çalışma sayfasına göre belirtilen konumda etkili bir şekilde kilitler. Ancak, şu anda, hücrelerle birlikte yeniden boyutlandırmaya tabidir.
## Adım 6: Yeni Eklenen Resme Erişim
Resmi daha fazla düzenleyebilmek için özelliklerine erişmeniz gerekir:
```csharp
Aspose.Cells.Drawing.Picture picture = worksheet.Pictures[pictureIndex];
```
Bununla birlikte, az önce eklediğimiz görselin özelliklerine erişim kazanacaksınız!
## Adım 7: Resim için Mutlak Konumlandırmayı Ayarlama
Resmi mutlak olarak (piksel olarak) konumlandırmak için, konumunu kullanarak tanımlamanız gerekecektir. `Left` Ve `Top` özellikleri. Görüntünün nerede görüneceği üzerinde kontrol sahibi olacağınız yer burasıdır:
```csharp
picture.Left = 60;
picture.Top = 10;
```
Her iki değeri de ihtiyacınıza göre ayarlayabilirsiniz; bunlar sırasıyla görüntünün yatay ve dikey konumunu temsil eder.
## Adım 8: Excel Dosyasını Kaydetme
Son olarak, tüm değişikliklerinizi yaptıktan sonra çalışma kitabını kaydetme zamanı geldi:
```csharp
workbook.Save(dataDir + "book1.out.xls");
```
Bu, adında bir Excel dosyası oluşturacaktır. `book1.out.xls` Daha önce tanımladığınız belge dizininde, resmin yerleştirildiği çalışma sayfanızı mutlaka bulun.

## Çözüm
İşte karşınızda! Aspose.Cells for .NET kullanarak bir resmi Excel sayfasında mutlak konumlandırmayla başarıyla konumlandırdınız. Bu basit işlem yalnızca Excel belgelerinizin görsel sunumunu geliştirmekle kalmaz, aynı zamanda resimlerin hücre boyutlarında ve satır yüksekliklerinde yapılan değişikliklerden bağımsız olarak tam olarak istediğiniz yerde kalmasını sağlar. Artık bir rapor hazırlıyor veya bir pano oluşturuyor olun, resimlerinizin her seferinde mükemmel bir şekilde yerleştirildiğinden emin olabilirsiniz.
## SSS
### Aspose.Cells for .NET nedir?
Aspose.Cells for .NET, geliştiricilerin Microsoft Excel'e ihtiyaç duymadan Excel elektronik tablolarını programlı bir şekilde oluşturmalarına, düzenlemelerine ve dönüştürmelerine olanak tanıyan bir .NET kütüphanesidir.
### Aspose.Cells'i kullanarak başka görüntü düzenlemeleri yapabilir miyim?
Evet, konumlandırmanın ötesinde, Aspose.Cells kitaplığını kullanarak Excel elektronik tablolarındaki resimleri yeniden boyutlandırabilir, döndürebilir ve değiştirebilirsiniz.
### Aspose.Cells'i kullanmak ücretsiz mi?
Aspose.Cells ticari bir üründür, ancak kendi sitelerinde mevcut olan ücretsiz deneme sürümüyle başlayabilirsiniz. [ücretsiz deneme sayfası](https://releases.aspose.com/).
### Aspose.Cells için geçici lisansı nasıl alabilirim?
Geçici lisans için başvurunuzu şu şekilde yapabilirsiniz: [geçici lisans sayfası](https://purchase.aspose.com/temporary-license/) Aspose tarafından sağlanmıştır.
### Daha fazla örnek ve dokümanı nerede bulabilirim?
The [Aspose.Cells belgeleri](https://reference.aspose.com/cells/net/) kod örnekleri ve daha detaylı özellikler de dahil olmak üzere kapsamlı kaynaklar içerir.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}