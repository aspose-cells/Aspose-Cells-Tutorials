---
"description": "Aspose.Cells for .NET kullanarak Excel çalışma kitabından gömülü MOL dosyalarının nasıl kolayca çıkarılacağını öğrenin."
"linktitle": "Gömülü Mol Dosyasını Çıkar"
"second_title": "Aspose.Cells for .NET API Başvurusu"
"title": "Gömülü Mol Dosyasını Çıkar"
"url": "/tr/net/excel-workbook/extract-embedded-mol-file/"
"weight": 90
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Gömülü Mol Dosyasını Çıkar

## giriiş

Hiç gömülü dosyaları, özellikle de MOL dosyalarını bir Excel elektronik tablosundan çıkarmanız gerektiğini fark ettiniz mi? Bu zor bir iş, değil mi? Ama endişelenmeyin! .NET için Aspose.Cells'in yardımıyla, bu görünüşte karmaşık görevi parkta yürüyüşe dönüştürebiliriz. Bu eğitimde, güçlü Aspose.Cells kitaplığını kullanarak bir Excel dosyasından MOL dosyalarını nasıl çıkaracağınız konusunda adım adım size rehberlik edeceğiz.

## Ön koşullar

Çıkarma sürecine dalmadan önce, takip etmek için tam donanımlı olduğunuzdan emin olalım. İhtiyacınız olanlar şunlardır:

- C# Temel Bilgisi: C# ile ilgili biraz bilgi sahibi olmak çok işe yarayacaktır. Yeni başlıyor olsanız bile, hızınızı koruyabilmelisiniz.
- Visual Studio: Sisteminizde Visual Studio'nun yüklü olması gerekir. C# kodunuzu yazmak ve çalıştırmak için gereklidir.
- Aspose.Cells for .NET: Henüz indirmediyseniz şuraya gidin: [Aspose.Cells indirme sayfası](https://releases.aspose.com/cells/net/) ve en son sürümü edinin.
- .NET Framework: Uyumlu bir .NET Framework sürümünün yüklü olduğundan emin olun.
- Gömülü MOL Nesneleri İçeren Bir Excel Dosyası: Örneğimiz için şunu kullanacağız: `EmbeddedMolSample.xlsx`Bu dosyanın çıkarılmaya hazır olduğundan emin olun.

## Paketleri İçe Aktar

Artık ihtiyacımız olan her şeye sahip olduğumuza göre, projemizi kurmanın zamanı geldi. İşte C# projenize gerekli paketleri nasıl içe aktaracağınız:

### Yeni Bir Proje Oluştur

Visual Studio'yu açın ve yeni bir C# Konsol Uygulaması oluşturmayı seçin.

### Aspose.Cells için NuGet Paketini Ekleyin

Yeni oluşturduğunuz projede Aspose.Cells paketini eklemeniz gerekecek. Bunu NuGet Paket Yöneticisi aracılığıyla yapabilirsiniz:

1. Çözüm Gezgini’nde projenizin üzerine sağ tıklayın.
2. "NuGet Paketlerini Yönet" seçeneğini seçin.
3. "Aspose.Cells" ifadesini arayın ve "Yükle"ye tıklayın.

### Aspose.Cells Ad Alanını İçe Aktar

```csharp
using Aspose.Cells.Drawing;
using Aspose.Cells.WebExtensions;
using System;
using System.IO;
```

Artık projeniz Aspose.Cells kütüphanesinin işlevlerini kullanabilir durumda olmalı.

## Adım 1: Ortamı Kurma

Artık gerekli paketleri içe aktardığımıza göre, MOL dosyalarını çıkarmak için ortamımızı ayarlayalım.

```csharp
//dizinler
string SourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";

```

Bu, gömülü MOL dosyalarınızı içeren Excel dosyasını kullanarak çalışma kitabını başlatır.


Çıkarma sürecini kolay takip edilebilir adımlara bölelim.

## Adım 2: Çalışma Kitabını Yükleyin

Bir kez sahip olduğunuzda `workbook` Örnek Excel dosyamızı kurduktan sonraki adım çalışma kitabını yüklemek ve çıkartmaya hazırlanmak:

```csharp
Workbook workbook = new Workbook(SourceDir + "EmbeddedMolSample.xlsx");
```

Bu adımda, yeni bir örnek oluşturuyoruz `Workbook` Excel dosyanızın içeriğine bir köprü görevi gören sınıf. Dosya buraya yüklenir, böylece daha sonra sayfalar arasında yineleme yapabilir ve gömülü MOL nesnelerini bulabiliriz.

## Adım 3: Çalışma Sayfalarında Yineleme Yapın

Artık çalışma kitabımız yüklendiğine göre, daha derine inme zamanı. Gömülü nesneleri bulmak için çalışma kitabındaki her çalışma sayfasını dolaşmanız gerekir:

```csharp
foreach (Worksheet sheet in workbook.Worksheets)
{
    OleObjectCollection oles = sheet.OleObjects;
    // OLE nesnelerinin işlenmesine devam ediliyor...
}
```

Bu kod parçacığıyla, şunu kullanıyoruz: `foreach` çalışma kitabımızdaki her sayfayı dolaşacak döngü. Erişim yoluyla `OleObjects` koleksiyon, o belirli sayfadaki tüm gömülü nesnelere erişim sağlayabiliriz. 

## Adım 4: OLE Nesnelerini Çıkarın

İşte sihir burada gerçekleşiyor! MOL dosyalarını çıkarmak ve kaydetmek için her OLE nesnesinde döngü yapmanız gerekiyor:

```csharp
var index = 1;
foreach (OleObject ole in oles)
{
    string fileName = outputDir + "OleObject" + index + ".mol";
    FileStream fs = File.Create(fileName);
    fs.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    fs.Close();
    index++;
}
```

Bu yaklaşımda:
- Çıktı dosyalarını sıralı olarak adlandırmak için indeksi takip ediyoruz.
- Her OLE nesnesi için FileStream kullanarak yeni bir dosya oluşturuyoruz.
- Daha sonra gömülü veriyi bu dosyaya yazıp akışı kapatıyoruz.

## Adım 5: Uygulamayı Onaylayın

Çıkarım mantığınız tamamlandıktan sonra, çıkarma işleminizin başarılı bir şekilde yürütüldüğünü doğrulamak iyi bir uygulamadır:

```csharp
Console.WriteLine("ExtractEmbeddedMolFile executed successfully.");
```

Bu basit satır, tüm çıkarma işleminiz sorunsuz bir şekilde tamamlandığında konsola bir mesaj çıkışı verir. 

## Çözüm

Ve işte oldu! Aspose.Cells for .NET kullanarak gömülü MOL dosyalarını bir Excel dosyasından başarıyla çıkardınız. Şimdi yeni edindiğiniz becerilerinizi alıp Excel sayfalarından nesne dosyaları çıkarmanız gereken diğer senaryolara uygulayabilirsiniz. Bu yöntem yalnızca etkili olmakla kalmaz, aynı zamanda çeşitli Excel ile ilgili işlemleri zahmetsizce halletmenin kapılarını da açar.

## SSS

### Aspose.Cells for .NET nedir?  
Aspose.Cells for .NET, Excel dosyalarını .NET uygulamaları içerisinde düzenlemek ve yönetmek için tasarlanmış güçlü bir kütüphanedir.

### Aspose.Cells kullanarak farklı türdeki gömülü dosyaları çıkarabilir miyim?  
Kesinlikle! Aspose.Cells, yalnızca MOL dosyalarını değil, PDF'ler, resimler ve daha fazlası gibi çeşitli gömülü dosya biçimlerini çıkarmanıza olanak tanır.

### Aspose.Cells'i kullanmak için satın almam gerekiyor mu?  
Ücretsiz deneme sürümü mevcut olsa da, tüm özellikler için bir lisansa ihtiyaç vardır. [buradan satın alın](https://purchase.aspose.com/buy).

### Bu işlem için Visual Studio'ya ihtiyaç var mı?  
Biz Visual Studio kullanarak gösterdik ama siz projenizi çalıştırmak için herhangi bir C# uyumlu IDE'yi kullanabilirsiniz.

### Aspose.Cells için desteği nereden bulabilirim?  
Erişebilirsiniz [Aspose destek forumları](https://forum.aspose.com/c/cells/9) rehberlik ve sorun giderme için.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}