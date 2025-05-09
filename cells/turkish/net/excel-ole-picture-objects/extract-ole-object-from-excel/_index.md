---
"description": "Aspose.Cells for .NET kullanarak Excel dosyalarından OLE nesnelerinin nasıl çıkarılacağını öğrenin. Kolay çıkarma için adım adım kılavuz."
"linktitle": "Excel'den OLE Nesnesini Çıkar"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": "Excel'den OLE Nesnesini Çıkar"
"url": "/tr/net/excel-ole-picture-objects/extract-ole-object-from-excel/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel'den OLE Nesnesini Çıkar

## giriiş
Günümüzün teknoloji meraklısı dünyasında, Excel dosyalarıyla uğraşmak, özellikle veri analizi, finans ve proje yönetimi alanında çalışanlar için yaygın bir görevdir. Genellikle göz ardı edilen bir husus, Excel elektronik tablolarındaki OLE (Nesne Bağlama ve Gömme) nesnelerinin işlenmesidir. Bunlar, Excel dosyalarınızın işlevselliğini ve zenginliğini artırmada önemli bir rol oynayan gömülü belgeler, resimler veya hatta karmaşık veri türleri olabilir. .NET kullanarak bu OLE nesnelerini programlı olarak çıkarmak isteyen bir Aspose.Cells kullanıcısıysanız, doğru yerdesiniz! Bu kılavuz, yalnızca nasıl yapılacağını değil, aynı zamanda sürecin her bir bölümünün neden önemli olduğunu da anlamanızı sağlayarak sizi adım adım süreçte yönlendirecektir.
## Ön koşullar
OLE nesnelerini çıkarma işleminin ince ayrıntılarına dalmadan önce, yerinde olması gereken birkaç şey vardır:
1. C# Temel Bilgisi: C#'a aşinaysanız, doğru yoldasınız demektir. Değilseniz, endişelenmeyin! İşleri basit tutacağız.
2. Aspose.Cells Kurulu: Aspose.Cells kütüphanesine ihtiyacınız olacak. Bunu siteden indirebilirsiniz [Burada](https://releases.aspose.com/cells/net/).
3. Uyumlu Bir Geliştirme Ortamı: Visual Studio gibi, kullanıma hazır bir .NET geliştirme ortamınızın olduğundan emin olun.
4. Örnek Excel Dosyası: Test için OLE nesnelerinin gömülü olduğu bir Excel dosyasına ihtiyacınız olacak. 
Bu ön koşullar sağlandıktan sonra, OLE nesne çıkarma dünyasına yolculuğumuza başlayabiliriz.
## Paketleri İçe Aktar
Öncelikle, eğitimimizde kullanacağımız gerekli paketleri içe aktaralım. C# projenizde, Aspose.Cells ad alanını eklemeniz gerekecek. Bunu nasıl yapabileceğiniz aşağıda açıklanmıştır:
```csharp
using System.IO;
using Aspose.Cells;
```
## Adım 1: Belge Dizinini Ayarlayın
Bu adımda, Excel dosyamızın bulunduğu yolu tanımlayacağız. Bunun neden önemli olduğunu merak ediyor olabilirsiniz. Bir performans için sahneyi hazırlamak gibidir; senaryonun aktörleri nerede bulacağını bilmesine yardımcı olur (bizim durumumuzda, Excel dosyası).
```csharp
string dataDir = "Your Document Directory";
```
Yer değiştirmek `"Your Document Directory"` Excel dosyanızın gerçek yolu ile (`book1.xls`) saklanır.
## Adım 2: Excel Dosyasını Açın
Artık belge dizinimizi kurduğumuza göre, bir sonraki adım Excel dosyasını açmaktır. Bunu okumaya başlamadan önce bir kitap açmak gibi düşünün; içinde ne olduğunu görmek önemlidir.
```csharp
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
## Adım 3: OLE Nesne Koleksiyonuna Erişim
Bir Excel çalışma kitabındaki her çalışma sayfası, OLE nesneleri de dahil olmak üzere çeşitli nesneler içerebilir. Burada, ilk çalışma sayfasının OLE nesne koleksiyonuna erişiyoruz. Bu, gömülü resimleri ve belgeleri kontrol etmek için bir sayfa seçmeye benzer.
```csharp
Aspose.Cells.Drawing.OleObjectCollection oles = workbook.Worksheets[0].OleObjects;
```
## Adım 4: OLE Nesneleri Arasında Döngü
Şimdi eğlenceli kısma geliyoruz: koleksiyonumuzdaki tüm OLE nesneleri arasında döngü. Bu adım çok önemlidir çünkü birden fazla OLE nesnesini verimli bir şekilde ele almamızı sağlar. Değerli eşyalar bulmak için bir hazine sandığının içinden geçtiğinizi düşünün!
```csharp
for (int i = 0; i < oles.Count; i++)
{
    Aspose.Cells.Drawing.OleObject ole = oles[i];
    // Her nesneyi işlemek için daha fazla mantık
}
```
## Adım 5: Çıktı Dosya Adını Belirleyin
Her bir OLE nesnesini daha derinlemesine incelediğimizde, çıkarılan nesneler için bir dosya adı bulmamız gerekir. Neden? Çünkü onları çıkardığımızda, hazinelerimizi daha sonra kolayca bulabilmek için her şeyi düzenli tutmak isteriz.
```csharp
string fileName = dataDir + "ole_" + i + ".";
```
## Adım 6: Dosya Biçimi Türünü Belirleyin
Her OLE nesnesi farklı türlerde olabilir (örneğin, belgeler, elektronik tablolar, resimler). Biçim türünü belirlemek, onu doğru şekilde çıkarabilmeniz için çok önemlidir. Bir yemeğin tarifini bilmek gibidir; malzemeleri bilmeniz gerekir!
```csharp
switch (ole.FileFormatType)
{
    case FileFormatType.Doc:
        fileName += "doc";
        break;
    case FileFormatType.Xlsx:
        fileName += "xlsx";
        break;
    case FileFormatType.Ppt:
        fileName += "ppt";
        break;
    case FileFormatType.Pdf:
        fileName += "pdf";
        break;
    case FileFormatType.Unknown:
        fileName += "jpg";
        break;
    default:
        // Diğer dosya biçimlerini yönetin
        break;
}
```
## Adım 7: OLE Nesnesini Kaydedin
Şimdi OLE nesnesini kaydetmeye geçelim. Nesne bir Excel dosyasıysa, onu bir `MemoryStream` bu da verileri yazmadan önce bellekte işlememize olanak tanır. Bu adım, hazinenizi bir arkadaşınıza göndermeden önce paketlemeye benzer.
```csharp
if (ole.FileFormatType == FileFormatType.Xlsx)
{
    MemoryStream ms = new MemoryStream();
    ms.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    Workbook oleBook = new Workbook(ms);
    oleBook.Settings.IsHidden = false;
    oleBook.Save(dataDir + "Excel_File" + i + ".out.xlsx");
}
```
Diğer dosya türleri için şunu kullanacağız: `FileStream` dosyayı diskte oluşturmak için.
```csharp
else
{
    FileStream fs = File.Create(fileName);
    fs.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    fs.Close();
}
```

## Çözüm
Ve işte böyle, Aspose.Cells for .NET ile OLE nesne çıkarma sularında başarıyla yol aldınız! Bu adımları izleyerek, Excel dosyalarınızdan gömülü nesneleri kolayca çıkarabilir ve yönetebilirsiniz. Unutmayın, değerli herhangi bir beceri gibi, pratik mükemmelleştirir. Bu yüzden, farklı Excel dosyalarıyla denemeler yaparak zaman ayırın ve yakında bir OLE çıkarma uzmanı olacaksınız!
## SSS
### Excel'deki OLE nesneleri nelerdir?
OLE nesneleri, Excel çalışma sayfasındaki diğer uygulamalardaki belgeleri ve verileri yerleştirmeye ve bunlara bağlantı sağlamaya olanak tanıyan bir teknolojidir.
### OLE nesnelerini neden çıkarmam gerekir?
OLE nesnelerini çıkarmak, gömülü belgelere veya resimlere orijinal Excel dosyasından bağımsız olarak erişmenizi ve bunları düzenlemenizi sağlar.
### Aspose.Cells her türlü gömülü dosyayı işleyebilir mi?
Evet, Aspose.Cells Word belgeleri, Excel sayfaları, PowerPoint sunumları ve resimler dahil olmak üzere çeşitli OLE nesnelerini yönetebilir.
### Aspose.Cells for .NET'i nasıl kurarım?
Aspose.Cells'i şu adresten indirerek yükleyebilirsiniz: [yayın sayfası](https://releases.aspose.com/cells/net/).
### Aspose.Cells için desteği nereden bulabilirim?
Aspose.Cells için desteği şu adresten alabilirsiniz: [destek forumu](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}