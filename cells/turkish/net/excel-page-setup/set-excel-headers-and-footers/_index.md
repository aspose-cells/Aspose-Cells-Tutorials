---
title: Excel Başlıklarını ve Altbilgilerini Ayarla
linktitle: Excel Başlıklarını ve Altbilgilerini Ayarla
second_title: Aspose.Cells for .NET API Başvurusu
description: Aspose.Cells for .NET'i kullanarak Excel başlıklarını ve altbilgilerini adım adım kılavuzumuzla kolayca nasıl ayarlayacağınızı öğrenin. Profesyonel belgeler için mükemmeldir.
weight: 100
url: /tr/net/excel-page-setup/set-excel-headers-and-footers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel Başlıklarını ve Altbilgilerini Ayarla

## giriiş

E-tablo belgelerini yönetmeye gelince, başlıklar ve altbilgiler bağlam sağlamada önemli bir rol oynar. Bir Excel dosyasını açtığınızı ve en üstte çalışma sayfasının adını, tarihi ve hatta belki de dosya adını gördüğünüzü hayal edin. Belgenize profesyonel bir dokunuş katar ve önemli ayrıntıları tek bakışta iletmenize yardımcı olur. .NET için Aspose.Cells kullanarak Excel sayfalarınızın profesyonelliğini artırmak istiyorsanız, doğru yerdesiniz! Bu kılavuzda, Excel e-tablolarınıza zahmetsizce başlıklar ve altbilgiler ayarlama adımlarında size yol göstereceğiz. 

## Ön koşullar

Ayrıntılara dalmadan önce, başlamak için ihtiyacınız olan her şeye sahip olduğunuzdan emin olalım. İlk olarak, şunlara ihtiyacınız olacak:

1. Visual Studio: Makinenizde Visual Studio'nun yüklü olduğundan emin olun. C# kodunuzu burada yazıp çalıştıracaksınız.
2.  Aspose.Cells for .NET Kütüphanesi: Aspose.Cells kütüphanesine sahip olmanız gerekir. Eğer henüz yapmadıysanız, şuradan indirebilirsiniz:[Burada](https://releases.aspose.com/cells/net/).
3. C# Hakkında Temel Bilgi: Tüm kod örnekleri bu dilde olacağından, C# programlamaya aşinalık çok önemlidir.
4. Proje Kurulumu: Excel başlık/altbilgi mantığımızı uygulayacağımız Visual Studio'da yeni bir C# projesi oluşturun.

Yukarıdaki ön koşullara sahip olduğunuzu doğruladıktan sonra, ellerimizi kirletmenin zamanı geldi!

## Paketleri İçe Aktar

Aspose.Cells ile çalışmaya başlamak için, C# kodunuza uygun ad alanlarını içe aktarmanız gerekir.

### C# Projenizi Açın

Başlık ve altbilgi ayarlarını uygulamak istediğiniz projenizi Visual Studio'da açın. Kodunuzu barındırabilecek net bir yapıya sahip olduğunuzdan emin olun.

### Aspose.Cells'e Referans Ekle

Projenizi oluşturduktan veya açtıktan sonra, Aspose.Cells kütüphanesine bir referans eklemeniz gerekir. Solution Explorer'da projenize sağ tıklayın, "Manage NuGet Packages"ı seçin ve 'Aspose.Cells'i arayın. Bunu projenize yükleyin.

### Ad Alanını İçe Aktar

C# dosyanızın en üstüne Aspose.Cells ad alanını içe aktarmak için aşağıdaki satırı ekleyin:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Bu namespace'i içe aktararak Aspose.Cells kütüphanesinin sağladığı işlevsellikleri hiçbir engele takılmadan kullanabilirsiniz.

Harika! Artık ortamınız kuruldu ve paketleriniz içe aktarıldı, şimdi Excel'de başlık ve altbilgi ayarlama sürecini adım adım inceleyelim.

## Adım 1: Çalışma Kitabını Başlatın

Öncelikle hafızamızdaki Excel dosyamızı temsil eden bir Çalışma Kitabı nesnesi oluşturmamız gerekiyor.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Workbook excel = new Workbook();
```

 Açıklama: Burada, şunu değiştirin`YOUR DOCUMENT DIRECTORY` Excel dosyanızı kaydetmek istediğiniz gerçek yol ile.`Workbook` nesnesi Excel dosyaları oluşturmak ve düzenlemek için ana giriş noktanızdır.

## Adım 2: PageSetup Referansını Edinin

 Daha sonra, şuraya erişmemiz gerekiyor:`PageSetup` Başlık ve altbilgileri ayarlamak istediğimiz çalışma sayfasının özelliği.

```csharp
PageSetup pageSetup = excel.Worksheets[0].PageSetup;
```

 Açıklama: İlk çalışma sayfasına (indeks) erişiyoruz`0` ) çalışma kitabımızın`PageSetup` sınıf, üstbilgiler ve altbilgiler dahil olmak üzere sayfanın yazdırıldığında nasıl görüneceğini özelleştirmek için özellikler ve yöntemler sağlar.

## Adım 3: Başlığı Ayarlayın

Şimdi başlığı ayarlamaya başlayalım. Sol bölümle başlayacağız:

```csharp
pageSetup.SetHeader(0, "&A");
```

 Açıklama:`SetHeader` yöntem, başlığın içeriğini tanımlamamıza olanak tanır. Burada,`&A` başlığın sol tarafında görünecek olan çalışma sayfasının adını belirtir.

## Adım 4: Merkezi Başlığı Özelleştirin

Daha sonra, merkezi başlığı özelleştirerek geçerli tarih ve saati belirli bir yazı tipinde göstereceğiz.

```csharp
pageSetup.SetHeader(1, "&\"Times New Roman,Bold\"&D-&T");
```

 Açıklama:`&D` Ve`&T` kodlar otomatik olarak kendilerini sırasıyla geçerli tarih ve saatle değiştirecektir. Ayrıca bu başlığın yazı tipinin "Times New Roman" ve kalın olması gerektiğini belirtiyoruz.

## Adım 5: Doğru Başlığı Ayarlayın

Şimdi başlığın sağ kısmını dosyanın ismini gösterecek şekilde ayarlayalım.

```csharp
pageSetup.SetHeader(2, "&\"Times New Roman,Bold\"&12&F");
```

 Açıklama: Burada,`&F` dosya adıyla değiştirilecektir. Tutarlı bir görünüm sağlamak için merkezi başlıkta kullandığımız yazı tipini kullanırız.

## Adım 6: Altbilgiyi Yapılandırın

Artık başlıklarımız şık göründüğüne göre, dikkatimizi altbilgilere çevirelim. Sol altbilgiyle başlayalım:

```csharp
pageSetup.SetFooter(0, "Hello World! &\"Courier New\"&14 123");
```

Açıklama: Sol alt bilgiye "Merhaba Dünya!" metninin yanında özel bir mesaj ekliyoruz.`123` farklı bir yazı tipinde—Courier New.

## Adım 7: Orta Alt Bilgi Yapılandırması

Daha sonra, ortadaki altbilgiyi geçerli sayfa numarasını gösterecek şekilde ayarlıyoruz:

```csharp
pageSetup.SetFooter(1, "&P");
```

 Açıklama:`&P` Kod, sayfa numarasını otomatik olarak altbilginin ortasına ekler; bu, sayfaları takip etmenin kullanışlı bir yoludur.

## Adım 8: Sağ Alt Bilgi Yapılandırması

Altbilgi ayarlarımızı tamamlamak için, sağ altbilgiyi belgedeki toplam sayfa sayısını gösterecek şekilde ayarlayalım.

```csharp
pageSetup.SetFooter(2, "&N");
```

 Açıklama: Burada,`&N` toplam sayfa sayısıyla değiştirilecektir. Özellikle uzun belgeler için profesyonel bir dokunuş katar.

## Adım 9: Çalışma Kitabını Kaydedin

Artık her şey hazır, emeğinizin meyvelerini görmek için çalışma kitabını kaydetmeniz yeterli.

```csharp
excel.Save(dataDir + "SetHeadersAndFooters_out.xls");
```

 Açıklama: Değiştir`"SetHeadersAndFooters_out.xls"` İstediğiniz dosya adıyla. Çalışma kitabınızı kaydedin ve işte tamam!

## Çözüm

İşte karşınızda! Aspose.Cells for .NET kullanarak Excel'de başlık ve altbilgi ayarlamak, bu adımları izlerseniz basittir. Belgenizin görünümünü iyileştirmekle kalmayıp, önemli bağlam sağlayarak işlevselliğini de iyileştirmiş olursunuz. İster raporlar hazırlayın, ister şablonlar paylaşın veya sadece verilerinizi düzenleyin, başlıklar ve altbilgiler rakipsiz bir profesyonellik katar. O halde deneyin ve bu güçlü kitaplıkla Excel belgelerinizi yönetmenin ne kadar kolay olduğunu görün!

## SSS

### Aspose.Cells Nedir?
Aspose.Cells, Excel dosyalarını program aracılığıyla oluşturmak, düzenlemek ve işlemek için kullanılan bir .NET kütüphanesidir.

### Aspose.Cells'i ücretsiz deneyebilir miyim?
 Evet! Ücretsiz deneme sürümünü şuradan indirebilirsiniz:[Burada](https://releases.aspose.com/).

### Aspose.Cells eski Excel formatlarıyla uyumlu mu?
Kesinlikle! Aspose.Cells hem eski hem de yeni Excel dosya formatlarını destekler.

### Daha fazla dokümanı nerede bulabilirim?
 Ayrıntılı dokümantasyonu şu adresten kontrol edebilirsiniz:[Aspose.Cells Belgeleri](https://reference.aspose.com/cells/net/).

### Aspose.Cells için desteği nasıl alabilirim?
 Destek için şu adresi ziyaret edin:[Aspose Destek Forumu](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
