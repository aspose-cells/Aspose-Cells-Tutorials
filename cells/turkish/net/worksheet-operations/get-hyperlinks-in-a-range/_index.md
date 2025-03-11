---
title: .NET'te Bir Aralıktaki Hiper Bağlantıları Alın
linktitle: .NET'te Bir Aralıktaki Hiper Bağlantıları Alın
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Aspose.Cells for .NET ile Excel dosyalarından köprü metinlerini kolayca çıkarın ve yönetin. Adım adım kılavuz ve kod örnekleri dahildir.
weight: 10
url: /tr/net/worksheet-operations/get-hyperlinks-in-a-range/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET'te Bir Aralıktaki Hiper Bağlantıları Alın

## giriiş
Hiç kendinizi elektronik tabloların içinde boğulurken buldunuz mu, köprü metinlerini nasıl etkili bir şekilde çıkaracağınızı merak ettiniz mi? Eğer öyleyse, doğru yerdesiniz! Bu kılavuzda, .NET için Aspose.Cells kullanarak belirli bir aralıktaki köprü metinlerini alma sürecinde size yol göstereceğiz. Bu güçlü kitaplık, Excel dosyalarıyla çalışmanın sıkıcı görevini ortadan kaldırarak köprü metinlerini almanızı ve hatta silmenizi kolaylaştırır. O halde bir fincan kahve alın ve Aspose.Cells dünyasına dalalım!
## Ön koşullar
Kodlamanın inceliklerine dalmadan önce, yerine getirmeniz gereken birkaç ön koşul var. Endişelenmeyin; bu uzun bir liste değil!
### Geliştirme Ortamınızı Hazırlayın
1. .NET Framework: Makinenizde uyumlu bir .NET ortamının kurulu olduğundan emin olun. .NET Core veya tam .NET Framework olabilir. Sürümünüzün Aspose.Cells kitaplığını desteklediğinden emin olun.
2.  Aspose.Cells Kütüphanesi: Aspose.Cells kütüphanesine sahip olmanız gerekir. En son sürümü şu adresten indirebilirsiniz:[Burada](https://releases.aspose.com/cells/net/) . Eğer yeni başlıyorsanız, şunu kullanmayı düşünün:[ücretsiz deneme](https://releases.aspose.com/) suları test etmek için.
3. IDE: Visual Studio gibi iyi bir Entegre Geliştirme Ortamı (IDE) hayatınızı kolaylaştıracaktır. Kodunuzu sorunsuz bir şekilde yazmanıza, hata ayıklamanıza ve çalıştırmanıza olanak tanır.
4. Temel C# Bilgisi: C# programlamaya aşina olmak faydalıdır, ancak öğrenmeye istekliyseniz, sorun yok!
Bu ön koşullar yerine getirildiğinde, harekete geçmeye hazırız. Temel kodlamaya geçelim: Gerekli paketleri içe aktaralım ve örneğimizi adım adım parçalayalım.
## Paketleri İçe Aktar
Kodlamanın ilk adımlarından biri gerekli paketleri içe aktarmaktır. Projenize Aspose.Cells kütüphanesine bir referans eklemeniz gerekir. Bu genellikle NuGet Paket Yöneticisi aracılığıyla yapılabilir. İşte bunu nasıl yapacağınız:
1. Visual Studio’yu açın.
2. Çözüm Gezgini’nde Projenize tıklayın.
3. Sağ tıklayın ve NuGet Paketlerini Yönet'i seçin.
4. “Aspose.Cells”i arayın ve yükleyin.
```csharp
using System.IO;
using System;
using Aspose.Cells;
```
Kütüphane hazır olduğuna göre şimdi hiper bağlantıları çıkarmak için koda geçelim!
## Adım 1: Dizin Yollarınızı Ayarlayın
Belgelerinizin yolunu tanımlayarak başlayalım. Excel dosyanızın bulunduğu kaynak dizini ve işlenen dosyanın kaydedileceği çıktı dizinini ayarlamak istersiniz.
```csharp
// Belgeler dizinine giden yol.
string sourceDir = "Your Document Directory"; // Bunu Excel dosyanızın yoluna değiştirin
// Çıktı dizini
string outputDir = "Your Document Directory"; // Bu yöntemin geçerli bir çıktı yolu sağladığından emin olun
```
 Bu kod parçacığında şunu değiştirin:`"Your Document Directory"` Excel dosyasını içeren dizininize giden gerçek yol ile. Bu, performansınızdan önce sahneyi kurmak gibidir; materyallerinizin nerede olduğunu bilmek çok önemlidir.
## Adım 2: Çalışma Kitabı Nesnesini Örneklendirin
 Daha sonra bir tane oluşturacağız`Workbook` Çalıştığımız Excel dosyasını açmak için nesne.
```csharp
// Bir Çalışma Kitabı nesnesi örneği oluşturun
// Bir Excel dosyası açın
Workbook workbook = new Workbook(sourceDir + "HyperlinksSample.xlsx");
```
 Burada yeni bir şey yaratıyoruz`Workbook` örnek.`Workbook`sınıf, esasen bir Excel dosyasıyla ilgili tüm işlemlere açılan kapınızdır. Bunu, tüm içeriğinizi barındıran kitabı açmak olarak düşünebilirsiniz.
## Adım 3: Çalışma Sayfasına Erişim
Artık çalışma kitabımız hazır olduğuna göre, ilk çalışma sayfasını alalım. Excel'de çalışma sayfaları kitabınızdaki sayfalar gibidir ve hangi sayfada çalıştığımızı belirtmemiz gerekir.
```csharp
// İlk (varsayılan) çalışma sayfasını al
Worksheet worksheet = workbook.Worksheets[0];
```
 Erişerek`Worksheets[0]`, ilk çalışma sayfasını seçiyoruz. Çalışma sayfaları sıfırdan başlayarak indekslenir, bu yüzden doğru olanı seçtiğinizden emin olun.
## Adım 4: Bir Aralık Oluşturun
Şimdi köprü metinlerini aramak istediğimiz aralığı tanımlamanın zamanı geldi. Bizim durumumuzda, A2 ila B3 hücrelerinde arama yapmak istediğimizi varsayalım.
```csharp
// A2:B3 aralığını oluşturun
Range range = worksheet.Cells.CreateRange("A2", "B3");
```
 Arayarak`CreateRange`, başlangıç ve bitiş hücrelerini belirtiriz. Sihir burada gerçekleşir—daha sonra bu belirtilen aralıkta bulunan köprü metinlerini kontrol edeceğiz.
## Adım 5: Aralıktan Hiper Bağlantıları Alın
Bu adım aslında tanımladığımız aralıktaki hiperlinklere ulaştığımız adımdır.
```csharp
//Hiper Bağlantıları aralığa alın
Hyperlink[] hyperlinks = range.Hyperlinks;
```
 The`Hyperlinks` birinin mülkü`Range` nesne bir dizi döndürür`Hyperlink` aralıkta bulunan nesneler. Sayfanızdaki tüm önemli notları tek seferde almak gibi!
## Adım 6: Döngüye Girin ve Bağlantıları Görüntüleyin
Şimdi, alınan köprü metinleri arasında dolaşalım. Şimdilik konsolda adreslerini ve alanlarını yazdıracağız.
```csharp
foreach (Hyperlink link in hyperlinks)
{
    Console.WriteLine(link.Area + " : " + link.Address);
}
```
Burada, her bir köprü metni arasında dolaşıp alanını ve adresini gösteriyoruz. Bu, bulduğunuz her köprü metninin önemli ayrıntılarını yüksek sesle okumaya benzer. 
## Adım 7: İsteğe bağlı - Köprü Metinlerini Silme
Gerekirse, aralığınızdan hiper bağlantıları kolayca silebilirsiniz! Bu, elektronik tablonuzu temizlemek istiyorsanız çok kullanışlı olabilir.
```csharp
foreach (Hyperlink link in hyperlinks)
{
    // Bağlantıyı silmek için Hyperlink.Delete() metodunu kullanın.
    link.Delete();
}
```
 Kullanımı`Delete()` her köprü metnindeki yöntem, artık ihtiyacınız olmayabilecek köprü metinlerini kaldırmanıza olanak tanır. Bu, sayfanızdan artık ihtiyaç duymadığınız bir karalamayı silmek gibidir.
## Adım 8: Değişikliklerinizi Kaydedin
Son olarak çalışma kitabını yaptığımız tüm ayarlamalarla kaydedelim.
```csharp
workbook.Save(outputDir + "HyperlinksSample_out.xlsx");
```
Bu kod satırı, değiştirilen çalışma kitabınızı belirtilen çıktı dizinine kaydedecektir. Bu, yaptığınız değişiklikleri yayınlamanın bir yoludur, örneğin son düzenlemelerden sonra kitabı kapatmak gibi.
## Çözüm
Ve işte karşınızda—Aspose.Cells for .NET kullanarak bir Excel sayfasındaki belirli bir aralıktan köprü metinleri çıkarmak için kapsamlı bir adım adım kılavuz! Ortamınızı nasıl kuracağınızı, kodu nasıl yazacağınızı ve bir Excel çalışma kitabındaki köprü metinleri üzerinde nasıl işlem yapacağınızı öğrendiniz. İster iş ister kişisel projeler için veri yönetiyor olun, bu araç uzun vadede size muazzam miktarda zaman kazandırabilir.
## SSS
### Aspose.Cells Nedir?
Aspose.Cells, bilgisayarınızda Microsoft Excel'in kurulu olmasına gerek kalmadan Excel dosyalarını düzenlemenize olanak sağlayan bir .NET kütüphanesidir.
### Aspose.Cells'i ücretsiz kullanabilir miyim?
Evet, ücretsiz deneme sürümü mevcut olup, satın almadan önce özelliklerini keşfetmenize olanak tanır.
### Deneme sürümünde herhangi bir kısıtlama var mı?
Deneme sürümünde, kaydedilen dosyalarda filigran gibi bazı işlevsellik kısıtlamaları olabilir.
### Aspose.Cells'i kullanmak için programlama bilmem gerekir mi?
Kütüphaneyi etkin bir şekilde kullanabilmek için C# veya .NET'te temel programlama bilgisine sahip olmanız önerilir.
### Aspose.Cells ile ilgili sorun yaşarsam nasıl destek alabilirim?
 Destek forumuna erişebilirsiniz[Burada](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
