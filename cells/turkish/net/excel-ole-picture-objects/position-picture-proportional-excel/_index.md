---
title: Excel'de Resim Konumlandırma (Orantılı)
linktitle: Excel'de Resim Konumlandırma (Orantılı)
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Aspose.Cells for .NET kullanarak Excel'de görselleri orantılı olarak nasıl konumlandıracağınızı öğrenin. Elektronik tablolarınızı görsel olarak daha çekici hale getirin.
weight: 14
url: /tr/net/excel-ole-picture-objects/position-picture-proportional-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Resim Konumlandırma (Orantılı)

## giriiş
Excel elektronik tablolarınıza asla tam olarak uymayan pikselli resimlerden bıktınız mı? Şunu hayal edin: Excel sayfanızda belirgin bir şekilde görüntülenmesi gereken güzel bir logonuz var, ancak sonunda sıkıştırılmış, gerilmiş veya kötü yerleştirilmiş oluyor. Bunu kimse istemez! Hadi, yerlerinize sıkı tutunun çünkü bugün .NET için Aspose.Cells kitaplığını kullanarak Excel'de resimleri orantılı olarak nasıl konumlandıracağınızı öğreneceksiniz. Bu güçlü kitaplık, raporlama, veri analizi veya sadece sunumlarınızı süslemek için olsun, Excel dosyalarını düzenlemeyi çocuk oyuncağı haline getiriyor. Resimlerinizi mükemmel şekilde hizalamanın inceliklerine dalalım!
## Ön koşullar
Gerçek kodlamaya dalmadan önce, makinenizde ayarlamanız gereken birkaç şey var:
1. Visual Studio: .NET projeniz için kullanışlı bir ortam sağlayacağından Visual Studio'nun yüklü olduğundan emin olun.
2.  Aspose.Cells Kütüphanesi: Aspose.Cells kütüphanesine ihtiyacınız olacak. Ücretsiz deneme sürümünü edinebilir veya şuradan satın alabilirsiniz:[Aspose web sitesi](https://purchase.aspose.com/buy).
3. Temel C# Bilgisi: C# programlamaya dair biraz bilgi sahibi olmak, tartışacağımız örnekleri anlamanıza yardımcı olacaktır.
4. Resim Dosyası: Excel dosyasına eklemek istediğiniz hazır bir resminiz (logonuz gibi) olsun.
Artık her şey yerli yerinde olduğuna göre kodlamaya geçebiliriz!
## Paketleri İçe Aktar
Projenizde Aspose.Cells kullanmaya başlamak için belirli ad alanlarını içe aktarmanız gerekir. Bunu nasıl yapacağınız aşağıda açıklanmıştır:
### Yeni Bir Proje Oluştur
Visual Studio'da yeni bir proje oluşturun:
- Visual Studio’yu açın.
- "Yeni proje oluştur"a tıklayın.
- Tercihinize bağlı olarak "Sınıf Kütüphanesi (.NET Framework)" veya "Konsol Uygulaması"nı seçin.
### Aspose.Cells'i yükleyin
Aspose.Cells paketini NuGet aracılığıyla projenize ekleyebilirsiniz. İşte nasıl:
- Çözüm Gezgini’nde projenizin üzerine sağ tıklayın.
- "NuGet Paketlerini Yönet" seçeneğini seçin.
- "Aspose.Cells" ifadesini arayın ve "Yükle"ye tıklayın.
### Yönergeleri Kullanarak Ekle
Kod dosyanızın en üstüne aşağıdaki yönergeleri ekleyin:
```csharp
using System.IO;
using Aspose.Cells;
```
Bu yönergeler Excel dosyalarınızı düzenlemek için ihtiyaç duyacağınız sınıflara erişmenizi sağlayacaktır.
Şimdi, Excel'de bir resmi orantılı bir şekilde başarılı bir şekilde konumlandırmak için bunu ayrıntılı adımlara ayıralım.
## Adım 1: Dizininizi Ayarlayın
İlk önce, belgeleriniz için belirlenmiş bir klasörünüz olduğundan emin olun. Eğer yoksa, bir dizin nasıl oluşturulur:
```csharp
string dataDir = "Your Document Directory";
// Eğer mevcut değilse dizin oluşturun.
bool isExists = System.IO.Directory.Exists(dataDir);
if (!isExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
 Bu kod parçası Excel dosyalarınızı depolamak için yeni bir dizin oluşturur (eğer yoksa). Sadece değiştirin`"Your Document Directory"` dosyalarınızın kaydedilmesini istediğiniz gerçek yol ile.
## Adım 2: Bir Çalışma Kitabı Oluşturun
Şimdi yeni bir çalışma kitabı oluşturalım:
```csharp
Workbook workbook = new Workbook();
```
Bu satır yeni bir çalışma kitabı nesnesi başlatır ve üzerinde çalışmanız için size boş bir alan sağlar.
## Adım 3: Yeni bir Çalışma Sayfası Ekleyin
Artık çalışma kitabımız hazır olduğuna göre, ona yeni bir çalışma sayfası ekleyelim:
```csharp
int sheetIndex = workbook.Worksheets.Add();
```
Bu, yeni bir çalışma sayfası ekleyecek ve daha sonra üzerinde değişiklik yapmak için kullanabileceğimiz o sayfanın dizinini döndürecektir.
## Adım 4: Yeni Çalışma Sayfasına Erişim
Yeni eklenen çalışma sayfasını düzenlemek için, ona erişmeniz gerekir:
```csharp
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
 Şimdi,`worksheet` belirli sayfaya içerik ve resim eklememize olanak tanıyacaktır.
## Adım 5: Resmi Ekle
Şimdi heyecan verici kısım geliyor! Güzel resminizi ekleyelim. Değiştir`"logo.jpg"` resim dosyanızın adıyla:
```csharp
int pictureIndex = worksheet.Pictures.Add(5, 5, dataDir + "logo.jpg");
```
 Bu satır, F6 hücresine resim ekler (satırlar ve sütunlar sıfır indeksli olduğundan,`5` (altıncı hücreye atıfta bulunur).
## Adım 6: Eklenen Resme Erişim
Resim eklendikten sonra şu şekilde erişebilirsiniz:
```csharp
Aspose.Cells.Drawing.Picture picture = worksheet.Pictures[pictureIndex];
```
Bu, resim özelliklerini değiştirmenizi sağlar.
## Adım 7: Resmi Orantılı Olarak Konumlandırın
Şimdi resmi orantılı olarak konumlandıralım:
```csharp
picture.UpperDeltaX = 200;
picture.UpperDeltaY = 200;
```
 Burada,`UpperDeltaX` Ve`UpperDeltaY` Görüntünün konumunu hücrenin boyutlarına göre ayarlayın. Görüntünüzü tam olarak doğru hale getirmek için bu değerleri ayarlayabilirsiniz.
## Adım 8: Değişikliklerinizi Kaydedin
Son olarak, tüm değişiklikleri korumak için çalışma kitabınızı kaydedin:
```csharp
workbook.Save(dataDir + "book1.out.xls");
```
 Bu satır çalışma kitabınızı şu şekilde kaydeder:`book1.out.xls` belirtilen dizinde.
## Çözüm
Ve işte oldu! Aspose.Cells for .NET kullanarak Excel'de resimleri orantılı olarak nasıl konumlandıracağınızı öğrendiniz. Sadece resim eklemekle ilgili değil; onları elektronik tablolarınızda mükemmel göstermekle ilgili. Sadece şunu unutmayın: İyi yerleştirilmiş bir resim, veri sunumunuzu önemli ölçüde yükseltebilir.
Farklı görseller ve yerleşimlerle deney yapmanın tadını çıkarın ve Aspose.Cells'in sunduğu zengin özelliklerin derinliklerine dalmaktan çekinmeyin. Excel sayfalarınız ciddi bir makyajdan geçecek!
## SSS
### Aspose.Cells Nedir?
Aspose.Cells, kullanıcıların Microsoft Excel'in kurulumuna ihtiyaç duymadan Excel dosyaları oluşturmalarına, düzenlemelerine ve dönüştürmelerine olanak tanıyan güçlü bir .NET kütüphanesidir.
### Aspose.Cells'i ücretsiz kullanabilir miyim?
 Evet, Aspose.Cells indirebileceğiniz ücretsiz bir deneme sürümü sunuyor[Burada](https://releases.aspose.com/).
### Dokümantasyonu nerede bulabilirim?
 Kapsamlı içeriğe erişebilirsiniz[belgeleme](https://reference.aspose.com/cells/net/) Aspose.Cells için.
### Aspose.Cells tüm resim formatlarını destekliyor mu?
Aspose.Cells JPEG, PNG, BMP, GIF ve TIFF gibi çeşitli formatları destekler.
### Aspose.Cells için nasıl destek alabilirim?
 Herhangi bir sorunuz varsa, lütfen şu adresi ziyaret edin:[destek forumu](https://forum.aspose.com/c/cells/9)Sorularınızı sorabileceğiniz yer.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
