---
"description": "Bu kolay adım adım eğitimle Aspose.Cells for .NET kullanarak Excel'de ara toplamların nasıl oluşturulacağını öğrenin."
"linktitle": "Excel'de Alt Toplamlar Oluşturma"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": "Excel'de Alt Toplamlar Oluşturma"
"url": "/tr/net/excel-subtotal-calculation/create-subtotals-in-excel/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Alt Toplamlar Oluşturma

## giriiş
Excel becerilerinizi geliştirmeye ve elektronik tablolarınızı daha dinamik hale getirmeye hazır mısınız? Excel'de alt toplamlar oluşturmak, verileri etkili bir şekilde kategorize etmenize ve özetlemenize yardımcı olarak daha iyi veri yorumlama ve raporlama olanağı sağlar. Kendinizi sık sık yığınla sayıyla boğuşurken bulan biriyseniz, yapılandırılmış özetler oluşturmak olmazsa olmazdır. Bugün, tüm Excel dosya işlemlerinizi yönetmek için tasarlanmış güçlü bir kitaplık olan Aspose.Cells for .NET kullanarak alt toplamları zahmetsizce nasıl oluşturacağınıza dalacağız.
## Ön koşullar
Excel'de ara toplamlar oluşturmanın inceliklerine dalmadan önce, yerine getirmeniz gereken birkaç ön koşul vardır:
1. .NET için Aspose.Cells Kurulu: Geliştirme ortamınızda Aspose.Cells kütüphanesinin kurulu olduğundan emin olun. Bunu henüz yapmadıysanız, kolayca yapabilirsiniz [buradan indirin](https://releases.aspose.com/cells/net/).
2. .NET Ortamı: Kütüphaneyle çalışabileceğimiz çalışan bir .NET ortamınız olmalı. Visual Studio veya başka bir IDE olsun, C#'ta kodlama konusunda rahat olduğunuzdan emin olun.
3. Temel C# Bilgisi: C#'a aşinalık faydalı olacaktır. Sağlayacağımız örnekler C# sözdizimindedir, bu nedenle bu konuda rahat olmanız süreci anlamanıza yardımcı olacaktır.
4. Excel Çalışma Sayfası: Üzerinde pratik yapmak için örnek bir Excel dosyası. Adlı bir dosya kullanacağız. `book1.xls` eğitimimizde.
5. Çevrimiçi Belgelere ve Desteğe Erişim: Kendinizi Çevrimiçi Belgelere ve Desteğe Tanıyın [Aspose.Cells belgeleri](https://reference.aspose.com/cells/net/) Kütüphaneyi kullanmada ilerledikçe inanılmaz derecede faydalı olabilir.
Artık temelleri attığımıza göre, teknik kısma geçebiliriz!
## Paketleri İçe Aktar
Gerçek koda başlamadan önce, gerekli tüm paketlere sahip olduğumuzdan emin olmamız gerekir. Aşağıda, projenize gerekli ad alanını nasıl içe aktarabileceğiniz gösterilmektedir:
```csharp
using System.IO;
using Aspose.Cells;
```
Bu, Excel dosyalarını düzenlemek için Aspose kütüphanesinden ihtiyacımız olan her şeyi içe aktarır. Şimdi, bir Excel çalışma sayfasında alt toplamlar oluşturmak için kodu adım adım parçalayalım.
## Adım 1: Dosya Yolunu Ayarlayın
Başlamak için Excel dosyamızın nerede bulunduğunu tanımlamamız gerekir. Bu, programa belge dizinimiz hakkında bilgi verdiğimiz yerdir.
```csharp
string dataDir = "Your Document Directory";
```
Yer değiştirmek `"Your Document Directory"` gerçek yolunuzla `book1.xls` saklanır. Bu, programa üzerinde işlem yapacağımız Excel dosyasının nerede bulunacağını söyler.
## Adım 2: Yeni Bir Çalışma Kitabı Oluşturun
Sırada, Workbook nesnesinin yeni bir örneğini oluşturacağız. Bu, Excel dosyamızı açmamıza ve düzenlememize olanak tanıyacak.
```csharp
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
Burada bir nesne yaratıyoruz `Workbook` ve onu belirtilen şekilde yüklüyoruz `book1.xls` dosya. Bu çalışma kitabı nesnesi artık Excel dosyasındaki tüm bilgileri içerir ve bunları değiştirmemize olanak tanır.
## Adım 3: Hücre Koleksiyonuna Erişim
Excel çalışma sayfasının içeriği üzerinde işlem yapabilmek için “Hücreler” koleksiyonuna erişmemiz gerekiyor.
```csharp
Cells cells = workbook.Worksheets[0].Cells;
```
Bu, çalışma kitabımızın ilk çalışma sayfasından (indeks 0) hücreleri alır. `cells` nesnesi, elektronik tablodaki bireysel hücrelerle etkileşime girmemizi sağlayacaktır.
## Adım 4: Alt Toplamlar için Hücre Alanını Tanımlayın
Şimdi ara toplamı uygulamak istediğimiz hücre aralığını belirtmenin zamanı geldi. 
```csharp
CellArea ca = new CellArea();
ca.StartRow = 2; // B3
ca.StartColumn = 1; 
ca.EndRow = 18; // 19. yüzyıl
ca.EndColumn = 2;
```
Burada bir tanım yapıyoruz `CellArea` ilgilendiğimiz aralığı belirten. Bu durumda, B3'ten (Satır 2, Sütun 1) C19'a (Satır 18, Sütun 2) kadar olan alanı seçtik. Alt toplamlarımızı burada hesaplayacağız.
## Adım 5: Alt Toplamları Uygula
Operasyonumuzun kalbi budur: Ara toplamın tanımlanan hücre alanına uygulanması.
```csharp
cells.Subtotal(ca, 0, ConsolidationFunction.Sum, new int[] { 1 });
```
Bu satırda şunu çağırıyoruz: `Subtotal` yöntem. Tanımlanan parametreler şunlardır:
- `ca`: Daha önce tanımladığımız hücre aralığı.
- `0`: Bu indeks, ara toplamı alınacak değerleri içeren sütunu ifade eder. 
- `ConsolidationFunction.Sum`: Bu, değerleri toplamak istediğimizi belirtir.
- `new int[] { 1 }`: Bu, ikinci sütundaki (Sütun C) değerleri topladığımızı gösterir.
## Adım 6: Değiştirilen Excel Dosyasını Kaydedin
Son olarak değişikliklerimizi yeni bir Excel dosyasına kaydetmemiz gerekiyor. 
```csharp
workbook.Save(dataDir + "output.out.xls");
```
The `Save` yöntem değişiklikleri adlı yeni bir dosyaya yazar `output.out.xls`İhtiyaçlarınıza göre çıktı dosyası için herhangi bir isim belirtebilirsiniz.
## Çözüm
Bu basit adımlarla, Aspose.Cells for .NET kullanarak Excel çalışma sayfanızda alt toplamları başarıyla oluşturdunuz! Bir çalışma kitabı örneği oluşturmaktan alt toplamları uygulamaya ve sonuçları kaydetmeye kadar tüm temelleri ele aldık. Bu kitaplık yalnızca Excel işlemlerinizi basitleştirmekle kalmaz, aynı zamanda verileri daha etkili bir şekilde işlemenizi sağlar.
Şimdi, devam edin ve deneyin! Doğru araçları nasıl kullanacağınızı bildiğinizde, elektronik tablolardaki verileri yönetmenin ne kadar kolaylaştığına şaşıracaksınız. 
## SSS
### Aspose.Cells for .NET nedir?
Aspose.Cells for .NET, geliştiricilerin .NET uygulamalarında Excel dosyalarını program aracılığıyla düzenlemelerine olanak tanıyan güçlü bir kütüphanedir.
### Aspose.Cells'i kullanmak için özel bir şey yüklemem gerekiyor mu?
Evet, Aspose.Cells kütüphanesini indirip .NET projenize eklemeniz gerekiyor. [Buradan indirin](https://releases.aspose.com/cells/net/).
### Aspose.Cells kullanarak başka türde Excel özellikleri oluşturmak mümkün müdür?
Kesinlikle! Aspose.Cells, grafikler oluşturma, çalışma sayfalarını yönetme ve hücre biçimlerini değiştirme gibi birçok Excel işlemini gerçekleştirmenizi sağlar.
### Aspose.Cells'i ücretsiz kullanabilir miyim?
Yapabilirsiniz [ücretsiz denemeyi deneyin](https://releases.aspose.com/) Satın almaya karar vermeden önce özelliklerini keşfetmek için Aspose.Cells'i inceleyin.
### Hangi destek seçenekleri mevcut?
Herhangi bir sorun için şu adresi ziyaret edebilirsiniz: [Aspose destek forumu](https://forum.aspose.com/c/cells/9) Kullanıcı ve geliştiricilerden oluşan bir toplulukla yardım almak ve fikirlerinizi paylaşmak.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}