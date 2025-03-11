---
title: Çalışma Sayfası Yazdırma için Kağıt Genişliğini ve Yüksekliğini Alın
linktitle: Çalışma Sayfası Yazdırma için Kağıt Genişliğini ve Yüksekliğini Alın
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Bu adım adım kılavuzla Aspose.Cells for .NET'te çalışma sayfası yazdırmak için kağıt genişliğini ve yüksekliğini nasıl alacağınızı öğrenin.
weight: 16
url: /tr/net/worksheet-display/get-paper-width-height/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Çalışma Sayfası Yazdırma için Kağıt Genişliğini ve Yüksekliğini Alın

## giriiş
Belgeleri doğru bir şekilde yazdırmak için kağıdın boyutları hakkında bilgi sahibi olmak gerekir. Bir geliştiriciyseniz veya Excel dosyalarıyla ilgilenen bir uygulama üzerinde çalışıyorsanız, çalışma sayfalarını yazdırırken kağıt genişliğini ve yüksekliğini nasıl alacağınızı bilmeniz gerekebilir. Neyse ki, .NET için Aspose.Cells Excel belgelerini programatik olarak yönetmek için sağlam bir yol sağlar. Bu makalede, temel kavramları göstermek için basit örnekler kullanarak kağıt boyutu özelliklerini belirleme sürecinde size rehberlik edeceğiz. 
## Ön koşullar
Teknik detaylara dalmadan önce, biraz temel çalışma yapalım. Bu öğreticiyi başarıyla takip etmek için şunlara ihtiyacınız olacak:
### 1. C#'ın Temel Bilgileri
.NET ortamında çalışacağımız için C# programlamaya iyi hakim olmanız gerekiyor.
### 2. Aspose.Cells Kütüphanesi
Projenizde Aspose.Cells kütüphanesinin yüklü olduğundan emin olun. Henüz yapmadıysanız, en son sürümü şu adresten indirebilirsiniz:[Aspose.Cells indirme sayfası](https://releases.aspose.com/cells/net/).
### 3. Visual Studio IDE
C# projelerinizi çalıştırmak ve yönetmek için Visual Studio'ya sahip olmak faydalıdır. .NET'i destekleyen herhangi bir sürüm harika çalışmalıdır.
### 4. Geçerli Bir Aspose Lisansı
 Aspose.Cells denenebilirken, uzun vadeli projeler için kullanıyorsanız bir lisans satın almayı düşünün. Bunu şuradan satın alabilirsiniz:[bu bağlantı](https://purchase.aspose.com/buy) veya keşfet[geçici lisans](https://purchase.aspose.com/temporary-license/) kısa test aşamaları için.
Her şey tamamsa, koda geçelim!
## Paketleri İçe Aktarma
Yolculuğumuzun ilk adımı temel ad alanlarını içe aktarmayı içerir. Bu önemlidir, çünkü Excel dosyalarını düzenlemek için kullanacağımız sınıflara ve yöntemlere erişmemizi sağlar. İşte bunu nasıl yapacağınız:
```csharp
using System;
using System.IO;
using Aspose.Cells;
```
Bu satırı .cs dosyanızın en üstüne eklediğinizden emin olun. Artık içe aktarımlar hazır olduğuna göre, çalışma kitabımızı oluşturmaya ve çalışma sayfasına erişmeye devam edelim.
## Adım 1: Çalışma Kitabınızı Oluşturun
Bir örnek oluşturarak başlıyoruz`Workbook` sınıf. Bu, Excel dosya düzenlememizin temelini oluşturur.
```csharp
Workbook wb = new Workbook();
```
Bu satır, programa yeni bir çalışma kitabı başlatmasını ve çalışma sayfalarımıza dalmaya başlamamızı söyler.
## Adım 2: İlk Çalışma Sayfasına Erişim
Sonra, yeni oluşturduğumuz çalışma kitabımızdaki ilk çalışma sayfasına erişeceğiz. Oldukça basit:
```csharp
Worksheet ws = wb.Worksheets[0];
```
Burada, çalışma kitabımızdaki ilk sayfaya (0'da indekslenmiş) erişiyoruz. Burada kağıt boyutlarını ayarlayacağız.
## Kağıt Boyutunu Ayarlama ve Boyutları Alma
Şimdi operasyonun özüne giriyoruz: kağıt boyutunu ayarlama ve boyutlarını alma! Bunu adım adım parçalayalım.
## Adım 3: Kağıt Boyutunu A2 Olarak Ayarlayın
Öncelikle kağıt ebatımızı A2 olarak ayarlayalım ve ölçülerini yazdıralım.
```csharp
ws.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```
 Bu kurulumdan sonra şunu kullanırız:`Console.WriteLine` boyutları görüntülemek için. Bunu çalıştırdığınızda, A2 kağıt boyutu için inç cinsinden genişlik ve yüksekliği göreceksiniz.
## Adım 4: Kağıt Boyutunu A3 Olarak Ayarlayın
Şimdi A3 zamanı! İşlemi basitçe tekrarlıyoruz:
```csharp
ws.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```
İşte! Beyanname A3 kağıdı için belirli yükseklik ve genişliği yazdıracaktır.
## Adım 5: Kağıt Boyutunu A4 Olarak Ayarlayın
Aynı kalıbı takip ederek A4'ün nasıl ölçüldüğünü kontrol edelim:
```csharp
ws.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```
Bu bize en yaygın kullanılan kağıt boyutlarından biri olan A4'ün boyutlarını verir.
## Adım 6: Kağıt Boyutunu Letter Olarak Ayarlayın
Kağıt boyutu keşfimizi tamamlamak için, boyutu Letter olarak ayarlayalım:
```csharp
ws.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```
Yine Letter boyutu için belirli genişlik ve yüksekliği göreceğiz.
## Çözüm
İşte bu kadar! Aspose.Cells for .NET kullanarak yazdırma için çalışma sayfaları hazırlarken çeşitli boyutlar için kağıt genişliğini ve yüksekliğini nasıl elde edeceğinizi öğrendiniz. Bu yardımcı program, özellikle yazdırma düzenlerinizi planlarken veya yazdırma ayarlarını programatik olarak yönetirken inanılmaz derecede yardımcı olabilir. Tam boyutları inç olarak bilerek, yaygın tuzaklardan kaçınabilir ve belgelerinizin amaçlandığı gibi yazdırılmasını sağlayabilirsiniz.
## SSS
### Aspose.Cells Nedir?
Aspose.Cells, Excel dosyalarıyla programlı olarak çalışmak için çeşitli özellikler sağlayan bir .NET kütüphanesidir.
### Aspose.Cells'i kullanmaya nasıl başlayabilirim?
Kütüphaneyi şu adresten indirerek başlayın:[Aspose web sitesi](https://releases.aspose.com/cells/net/) ve projenizde kurulumunu yapmak için dokümantasyonu takip edin.
### Aspose.Cells'i ücretsiz kullanabilir miyim?
Aspose.Cells, özelliklerini keşfetmek için kullanabileceğiniz bir deneme sürümü sunar. Uzun süreli kullanım için bir lisans satın almanız gerekir.
### Aspose.Cells hangi kağıt boyutlarını destekliyor?
Aspose.Cells, A2, A3, A4, Letter ve daha birçok farklı kağıt boyutunu destekler.
### Aspose.Cells için daha fazla kaynak veya desteği nerede bulabilirim?
 Kontrol edebilirsiniz[Aspose forumu](https://forum.aspose.com/c/cells/9) toplum yardımı ve[belgeleme](https://reference.aspose.com/cells/net/) öğretici materyaller ve referans materyalleri için.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
