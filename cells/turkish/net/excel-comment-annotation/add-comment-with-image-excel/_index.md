---
title: Excel'de Resimli Yorum Ekle
linktitle: Excel'de Resimli Yorum Ekle
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Aspose.Cells for .NET kullanarak Excel'de resimlerle yorum eklemeyi öğrenin. Kişiselleştirilmiş açıklamalarla elektronik tablolarınızı geliştirin.
weight: 10
url: /tr/net/excel-comment-annotation/add-comment-with-image-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Resimli Yorum Ekle

## giriiş
Excel, veri yönetimi ve analizi için güçlü bir araçtır, ancak bazen elektronik tablolarınıza kişisel bir dokunuş eklemeniz gerekir, değil mi? Belki de verileri açıklama, geri bildirim sağlama veya hatta resimlerle biraz gösteriş katmak istersiniz. İşte yorumlar tam da bu noktada işe yarar! Bu eğitimde, .NET için Aspose.Cells kitaplığını kullanarak Excel'de bir resimle yorum eklemeyi keşfedeceğiz. Bu yaklaşım, daha etkileşimli ve görsel olarak çekici elektronik tablolar oluşturmak için özellikle yararlı olabilir.
## Ön koşullar
Excel'de resimlere yorum eklemenin inceliklerine dalmadan önce, başlamak için ihtiyacınız olan her şeye sahip olduğunuzdan emin olalım:
1. Visual Studio: Bilgisayarınızda Visual Studio'nun yüklü olduğundan emin olun. Kodunuzu burada yazacak ve çalıştıracaksınız.
2.  .NET için Aspose.Cells: Aspose.Cells kütüphanesine sahip olmanız gerekir. Henüz yüklemediyseniz, şuradan indirebilirsiniz:[Burada](https://releases.aspose.com/cells/net/).
3. Temel C# Bilgisi: C# programlamaya aşina olmak, kod parçacıklarını daha iyi anlamanıza yardımcı olacaktır.
4. Bir Resim Dosyası: Excel yorumunuza yerleştirmek istediğiniz hazır bir resim dosyanız (logo gibi) olsun. Bu eğitim için, adında bir dosyanız olduğunu varsayacağız`logo.jpg`.
5. .NET Framework: Aspose.Cells'in düzgün çalışması için .NET Framework'ün yüklü olduğundan emin olun.
Artık ön koşullarımızı tamamladığımıza göre, gerçek kodlamaya geçebiliriz!
## Paketleri İçe Aktar
İlk önce gerekli paketleri içe aktarmamız gerekiyor. C# projenizde Aspose.Cells kütüphanesine bir referans eklediğinizden emin olun. Bunu Visual Studio'daki NuGet Paket Yöneticisi'ni kullanarak yapabilirsiniz. İşte nasıl:
1. Visual Studio’yu açın.
2. Yeni bir proje oluşturun veya mevcut bir projeyi açın.
3. Çözüm Gezgini’nde projenizin üzerine sağ tıklayın.
4. NuGet Paketlerini Yönet'i seçin.
5. Aspose.Cells'i arayın ve yükleyin.

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Kütüphaneyi kurduktan sonra kodunuzu yazmaya başlayabilirsiniz. İşte adım adım nasıl yapacağınız.
## Adım 1: Belge Dizininizi Ayarlayın
Başlamak için Excel dosyalarımızı kaydedebileceğimiz bir dizin ayarlamamız gerekiyor. Bu çok önemli bir adım çünkü işimizi düzenli tutmak istiyoruz.
```csharp
// Belgeler dizinine giden yol.
string dataDir = "Your Document Directory";
// Eğer mevcut değilse dizin oluşturun.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- dataDir: Bu değişken, belgeler dizininize giden yolu tutar. Değiştir`"Your Document Directory"` Excel dosyanızı kaydetmek istediğiniz gerçek yol ile.
- Directory.Exists: Bu, dizinin zaten var olup olmadığını kontrol eder.
- Directory.CreateDirectory: Eğer dizin mevcut değilse, bu onu oluşturur.
## Adım 2: Bir Çalışma Kitabı Oluşturun
 Daha sonra, bir örnek oluşturmamız gerekiyor`Workbook` sınıf. Bu sınıf bellekteki bir Excel çalışma kitabını temsil eder.
```csharp
//Bir Çalışma Kitabını Örneklendirin
Workbook workbook = new Workbook();
```
- Çalışma Kitabı: Bu, Excel dosyaları oluşturmanıza ve düzenlemenize olanak tanıyan Aspose.Cells'deki ana sınıftır. Bunu örnekleyerek, esasen yeni bir Excel çalışma kitabı oluşturuyorsunuz.
## Adım 3: Yorum Koleksiyonunu Edinin
Artık çalışma kitabımız hazır olduğuna göre, ilk çalışma sayfasının yorum koleksiyonuna erişelim.
```csharp
// İlk sayfadaki yorum koleksiyonunun referansını alın
CommentCollection comments = workbook.Worksheets[0].Comments;
```
- Çalışma sayfaları[ 0]: Bu, çalışma kitabındaki ilk çalışma sayfasına erişim sağlar. Unutmayın, dizin sıfır tabanlıdır, bu nedenle`[0]` ilk sayfaya atıfta bulunur.
- Yorumlar: Bu özellik bize o çalışma sayfasındaki yorumlar koleksiyonuna erişim sağlar.
## Adım 4: Bir Hücreye Yorum Ekleyin
Belirli bir hücreye bir yorum ekleyelim. Bu durumda, A1 hücresine bir yorum ekleyeceğiz.
```csharp
// A1 hücresine bir yorum ekleyin
int commentIndex = comments.Add(0, 0);
Comment comment = comments[commentIndex];
comment.Note = "First note.";
comment.Font.Name = "Times New Roman";
```
- comments.Add(0, 0): Bu yöntem, A1 hücresine (satır 0, sütun 0) bir yorum ekler.
- yorum.Not: Burada yorumun metnini belirliyoruz.
- comment.Font.Name: Bu, yorum metninin yazı tipini ayarlar.
## Adım 5: Bir Görüntüyü Akışa Yükleyin
 Şimdi yorumumuza yerleştirmek istediğimiz resmi yükleme zamanı. Bir`MemoryStream` görüntü verilerini tutmak için.
```csharp
// Akışa bir görüntü yükleyin
Bitmap bmp = new Bitmap(dataDir + "logo.jpg");
MemoryStream ms = new MemoryStream();
bmp.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
```
- Bitmap: Bu sınıf resim dosyasını yüklemek için kullanılır. Yolun doğru olduğundan emin olun.
- MemoryStream: Bu, görüntüyü belleğe kaydetmek için kullanacağımız akıştır.
- bmp.Save: Bu, bitmap görüntüsünü bellek akışına PNG formatında kaydeder.
## Adım 6: Görüntü Verilerini Yorum Şekline Ayarlayın
Şimdi resim verisini daha önce oluşturduğumuz yorumla ilişkili şekle ayarlamamız gerekiyor.
```csharp
// Resim verilerini yorumla ilişkili şekle ayarlayın
comment.CommentShape.Fill.ImageData = ms.ToArray();
```
- comment.CommentShape.Fill.ImageData: Bu özellik, yorum şekli için resmi ayarlamanıza olanak tanır.`MemoryStream` bir bayt dizisine kullanarak`ms.ToArray()`.
## Adım 7: Çalışma Kitabını Kaydedin
Son olarak çalışma kitabımızı yorum ve resim ekleyerek kaydedelim.
```csharp
// Çalışma kitabını kaydet
workbook.Save(dataDir + "book1.out.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```
- workbook.Save: Bu yöntem çalışma kitabını belirtilen yola kaydeder. Bunu bir XLSX dosyası olarak kaydediyoruz.
## Çözüm
İşte oldu! Aspose.Cells for .NET kullanarak bir Excel dosyasına resimli bir yorum eklemeyi başardınız. Bu özellik, elektronik tablolarınızı daha bilgilendirici ve görsel olarak çekici hale getirebilir. Verilere açıklama ekliyor, geri bildirim sağlıyor veya sadece kişisel bir dokunuş katıyor olun, resimli yorumlar kullanıcı deneyimini önemli ölçüde iyileştirebilir.
## SSS
### Aynı hücreye birden fazla yorum ekleyebilir miyim?
Hayır, Excel aynı hücrede birden fazla yoruma izin vermez. Hücre başına yalnızca bir yorumunuz olabilir.
### Hangi resim formatları destekleniyor?
Aspose.Cells PNG, JPEG ve BMP dahil olmak üzere çeşitli resim formatlarını destekler.
### Aspose.Cells'i kullanmak için lisansa ihtiyacım var mı?
Aspose.Cells ücretsiz deneme sürümü sunuyor, ancak tüm işlevlerden yararlanmak için lisans satın almanız gerekiyor.
### Yorumun görünümünü özelleştirebilir miyim?
Evet, yorum metninin yazı tipini, boyutunu ve rengini özelleştirebilir, ayrıca yorumun şeklini ve boyutunu da değiştirebilirsiniz.
### Aspose.Cells hakkında daha fazla dokümanı nerede bulabilirim?
 Aspose.Cells'te kapsamlı belgeler bulabilirsiniz[Burada](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
