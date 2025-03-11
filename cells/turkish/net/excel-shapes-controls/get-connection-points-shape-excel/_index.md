---
title: Excel'de Şekillerin Bağlantı Noktalarını Alın
linktitle: Excel'de Şekillerin Bağlantı Noktalarını Alın
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Aspose.Cells for .NET ile Excel'de şekil bağlantı noktalarının nasıl alınacağını öğrenin. Şekil noktalarını programatik olarak kolayca çıkarmak ve görüntülemek için adım adım kılavuzumuzu izleyin.
weight: 11
url: /tr/net/excel-shapes-controls/get-connection-points-shape-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Şekillerin Bağlantı Noktalarını Alın

## giriiş
Excel dosyalarıyla programatik olarak çalışırken, genellikle sayfalara gömülü şekillerle etkileşime girmemiz gerekir. Gerçekleştirebileceğiniz daha gelişmiş görevlerden biri, bir şekilden bağlantı noktalarını çıkarmaktır. Bağlantı noktaları, şekilleri bağlayıcılarla birleştirmek ve düzenlerini daha hassas bir şekilde yönetmek için kullanılır. Excel'de bir şeklin bağlantı noktalarını almak istiyorsanız, Aspose.Cells for .NET ihtiyacınız olan araçtır. Bu eğitimde, bunu başarmak için adım adım bir süreçten geçeceğiz.
## Ön koşullar
Koda dalmadan önce aşağıdaki ön koşullara sahip olduğunuzdan emin olun:
- .NET için Aspose.Cells: Geliştirme ortamınızda Aspose.Cells'in yüklü olması gerekir. Henüz yüklü değilse,[en son sürümü buradan indirin](https://releases.aspose.com/cells/net/).
- Geliştirme Ortamı: Visual Studio'nun veya herhangi bir .NET uyumlu IDE'nin çalışan bir kurulumuna sahip olduğunuzdan emin olun.
- Temel C# Bilgisi: Bu eğitim, C# programlama ve nesne yönelimli prensipler hakkında temel bir anlayışa sahip olduğunuzu varsayar.
 Ayrıca bir kayıt yaptırabilirsiniz[Aspose.Cells'in ücretsiz denemesi](https://releases.aspose.com/) Eğer henüz yapmadıysanız. Bu, bu kılavuz için gereken tüm özelliklere erişmenizi sağlayacaktır.

## Paketleri İçe Aktar
Projenizde Aspose.Cells ile çalışmak için gerekli ad alanlarını eklemeniz gerekir. Aşağıdaki içe aktarma ifadeleri kodunuzun en üstüne yerleştirilmelidir:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Bu ad alanları, Aspose.Cells'in temel işlevlerine erişmenizi ve çalışma sayfalarını ve şekilleri değiştirmenizi sağlar.

## Bir Şeklin Bağlantı Noktalarını Elde Etmek İçin Adım Adım Kılavuz
Bu bölümde, bir Excel çalışma sayfasındaki bir şeklin bağlantı noktalarını nasıl çıkaracağınızı göstereceğiz. Net bir anlayış için her adımı dikkatlice izleyin.
## Adım 1: Yeni Bir Çalışma Kitabı Oluşturun
 İlk önce, bir örnek oluşturmamız gerekiyor`Workbook` sınıf. Bu, Aspose.Cells'deki bir Excel dosyasını temsil eder. Mevcut bir dosyanız yoksa sorun değil—boş bir çalışma kitabıyla başlayabilirsiniz.
```csharp
// Yeni bir Çalışma Kitabı örneği oluşturun
Workbook workbook = new Workbook();
```
 Bu adımda boş bir Excel çalışma kitabı oluşturduk, ancak dosya yolunu Excel'e geçirerek mevcut bir çalışma kitabını da yükleyebilirsiniz.`Workbook` inşaatçı.
## Adım 2: İlk Çalışma Sayfasına Erişim
Sonra, şekillerle çalışmak istediğimiz çalışma sayfasına erişmemiz gerekiyor. Bu durumda, çalışma kitabının ilk çalışma sayfasını kullanacağız.
```csharp
// Çalışma kitabındaki ilk çalışma sayfasını alın
Worksheet worksheet = workbook.Worksheets[0];
```
 Bu satır, çalışma kitabındaki çalışma sayfaları koleksiyonundan ilk çalışma sayfasına erişir. Belirli bir sayfayla çalışıyorsanız, dizini değiştirebilirsiniz`0` istenilen indeksle.
## Adım 3: Yeni Bir Metin Kutusu (Şekil) Ekleyin
Şimdi çalışma sayfasına yeni bir şekil ekleyelim. Bir şekil türü olan bir metin kutusu oluşturacağız. Başka türde şekiller de ekleyebilirsiniz ancak basitlik adına bu eğitimde bir metin kutusuyla devam edeceğiz.
```csharp
// Koleksiyona yeni bir metin kutusu ekleyin
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
İşte yaptıklarımız:
-  Satıra bir metin kutusu eklendi`2` , kolon`1`.
-  Metin kutusunun boyutlarını ayarlayın`160` genişlikteki birimler ve`200` yükseklikteki birimler.
## Adım 4: Şekiller Koleksiyonundan Şekle Erişim
 Metin kutusunu eklediğimizde, çalışma sayfasının şekil koleksiyonunun bir parçası haline gelir. Şimdi bu şekle şu şekilde erişeceğiz:`Shapes`koleksiyon.
```csharp
// Şekil koleksiyonundan şekle (metin kutusu) erişin
Shape shape = workbook.Worksheets[0].Shapes[0];
```
Bu adımda, koleksiyondan ilk şekli (metin kutumuzu) alırız. Birden fazla şekliniz varsa, dizini belirtebilir veya şekli ismine göre bile bulabilirsiniz.
## Adım 5: Bağlantı Noktalarını Alın
Şimdi şeklimiz olduğuna göre, bağlantı noktalarını çıkaralım. Bu noktalar, şekle bağlayıcılar takmak için kullanılır.`ConnectionPoints` şeklin özelliği mevcut tüm bağlantı noktalarını döndürür.
```csharp
// Bu şekildeki tüm bağlantı noktalarını alın
var connectionPoints = shape.ConnectionPoints;
```
Bu bize o şekil için mevcut tüm bağlantı noktalarının bir koleksiyonunu verir.
## Adım 6: Bağlantı Noktalarını Göster
Son olarak, her bağlantı noktasının koordinatlarını görüntülemek istiyoruz. Bağlantı noktaları arasında döngü kurduğumuz ve bunları konsola yazdırdığımız yer burasıdır.
```csharp
// Tüm şekil noktalarını görüntüle
foreach (var pt in connectionPoints)
{
    System.Console.WriteLine(string.Format("X = {0}, Y = {1}", pt.X, pt.Y));
}
```
 Bu döngü her bağlantı noktası üzerinde yineleme yapar ve şunu yazdırır:`X` Ve`Y` koordinatlar. Bu, bir şeklin bağlantı noktalarını hata ayıklamak veya görsel olarak doğrulamak için yararlı olabilir.
## Adım 7: Uygula ve Tamamla
Yukarıdaki tüm adımları kurduğunuzda, kodu çalıştırabilirsiniz. İşte işlemin başarıyla tamamlanmasını sağlayan son satır:
```csharp
System.Console.WriteLine("GetShapeConnectionPoints executed successfully.");
```
Bu satır, işlemin tamamlandığını belirten bir mesajı konsola kaydeder.

## Çözüm
Bu eğitimde, .NET için Aspose.Cells kullanarak Excel'de bir şeklin bağlantı noktalarının nasıl alınacağını ele aldık. Görevi küçük, sindirilebilir adımlara bölerek, bir çalışma kitabı oluşturma, bir şekil ekleme ve bağlantı noktalarını çıkarma sürecini inceledik.
Şekilleri programatik olarak nasıl işleyeceğinizi anlayarak, dinamik ve etkileşimli Excel sayfaları oluşturmak için bir olasılıklar dünyasının kilidini açarsınız. İster raporlar oluşturun, ister panolar tasarlayın veya diyagramlar oluşturun, bu bilgi işe yarayacaktır.
## SSS
### Bir şeklin bağlantı noktası nedir?
Bağlantı noktası, bir şeklin üzerinde bağlayıcılar takabileceğiniz veya şekli diğer şekillere bağlayabileceğiniz belirli bir noktadır.
### Bir çalışma sayfasındaki tüm şekillerin bağlantı noktalarını alabilir miyim?
Evet, Aspose.Cells, bunları destekleyen herhangi bir şekil için bağlantı noktalarını almanıza olanak tanır. Çalışma sayfasındaki şekiller koleksiyonunda basitçe döngü yapın.
### Aspose.Cells'i kullanmak için lisansa ihtiyacım var mı?
Evet, ücretsiz deneyebilirsiniz ancak tüm özellikler için lisans gereklidir.[buradan lisans satın alın](https://purchase.aspose.com/buy)veya bir tane al[geçici lisans](https://purchase.aspose.com/temporary-license/).
### Aspose.Cells'e farklı şekil türlerini nasıl ekleyebilirim?
Kullanabilirsiniz`Add` dikdörtgenler, elipsler ve daha fazlası gibi şekiller için yöntem. Her şeklin özelleştirebileceğiniz belirli parametreleri vardır.
### Yeni bir Excel dosyası oluşturmak yerine mevcut bir Excel dosyasını nasıl yüklerim?
 Mevcut bir dosyayı yüklemek için dosya yolunu şuraya iletin:`Workbook` yapıcı, şu şekilde:  
```csharp
Workbook workbook = new Workbook("path_to_file.xlsx");
```
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
