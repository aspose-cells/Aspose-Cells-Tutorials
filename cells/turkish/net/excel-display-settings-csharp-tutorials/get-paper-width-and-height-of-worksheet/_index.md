---
title: Çalışma Sayfasının Kağıt Genişliğini ve Yüksekliğini Alın
linktitle: Çalışma Sayfasının Kağıt Genişliğini ve Yüksekliğini Alın
second_title: Aspose.Cells for .NET API Başvurusu
description: Aspose.Cells for .NET'te çalışma sayfalarının genişliğini ve yüksekliğini nasıl ayarlayacağınızı basit adım adım bir kılavuzla öğrenin.
weight: 80
url: /tr/net/excel-display-settings-csharp-tutorials/get-paper-width-and-height-of-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Çalışma Sayfasının Kağıt Genişliğini ve Yüksekliğini Alın

## giriiş

Hiç bir Excel sayfasını yazdırmayı denediniz ve çeşitli kağıt boyutlarının kafa karıştırıcı boyutlarıyla uğraştınız mı? Eğer benim gibiyseniz, hiçbir şeyin doğru çıkmayan bir düzen kadar gününüzü mahvedemeyeceğini bilirsiniz! İster raporlar, ister faturalar veya sadece basit bir liste yazdırıyor olun, kağıt boyutlarını programatik olarak nasıl ayarlayacağınızı anlamak sizi bir sürü dertten kurtarabilir. Bugün, uygulamanızda doğrudan kağıt boyutlarını nasıl alacağınızı ve ayarlayacağınızı incelemek için Aspose.Cells for .NET dünyasına dalacağız. Kollarımızı sıvayalım ve bu kağıt boyutlarını yönetmenin inceliklerine inelim!

## Ön koşullar 

Kodlamanın büyüsüne dalmadan önce, başlamak için ihtiyacınız olan şeyleri bir araya getirelim:

1. C#'ın Temel Anlayışı: C#'a giriş seviyesinde hakim olmalısınız. Programlamaya yeni başladıysanız endişelenmeyin! Basit tutacağız.
2.  Aspose.Cells Kütüphanesi: Makinenizde .NET için Aspose.Cells kütüphanesinin yüklü olduğundan emin olun. Bunu şu adresten indirebilirsiniz:[bu bağlantı](https://releases.aspose.com/cells/net/).
3. .NET Geliştirme Ortamı: C# kodunuzu yazmak ve yürütmek için Visual Studio'yu veya seçtiğiniz herhangi bir IDE'yi kurun. Nereden başlayacağınızdan emin değilseniz, Visual Studio Community Edition sağlam bir seçimdir.
4.  Referanslar ve Belgeler: Daha derin içgörüler için Aspose.Cells belgelerine aşina olun. Bunu bulabilirsiniz[Burada](https://reference.aspose.com/cells/net/).
5. Temel Excel Dosya Bilgisi: Excel dosyalarının nasıl yapılandırıldığını (çalışma sayfaları, satırlar ve sütunlar) anlamak çok faydalı olacaktır.

Harika! Artık temelleri işaretlediğimize göre, gerekli paketleri içe aktarmaya geçebiliriz.

## Paketleri İçe Aktar

 Hayatımızı kolaylaştırmak ve Aspose.Cells'in tüm gücünden yararlanmak için birkaç paketi içe aktarmamız gerekiyor. Bir tane eklemek kadar basit`using` Kod dosyanızın en üstündeki ifade. İçe aktarmanız gerekenler şunlardır:

```csharp
using System;
using System.IO;
```

Bu satır, Aspose.Cells kütüphanesindeki tüm sınıflara ve yöntemlere erişmemizi sağlayarak Excel dosyalarını yönetmeyi kolaylaştırır. Şimdi, çeşitli kağıt boyutları için kağıt genişliğini ve yüksekliğini alma konusunda adım adım kılavuzumuza geçelim.

## Adım 1: Yeni bir Çalışma Kitabı Oluşturun

Aspose.Cells ile çalışmanın ilk adımı yeni bir çalışma kitabı oluşturmaktır. Çalışma kitabını, çalışma sayfaları, hücreler ekleyebileceğiniz ve bizim durumumuzda kağıt boyutlarını tanımlayabileceğiniz boş bir tuval olarak düşünün.

```csharp
//Çalışma kitabı oluştur
Workbook wb = new Workbook();
```

Bu satır, bizim işlememiz için hazır olan yeni bir çalışma kitabı nesnesi örneği oluşturur. Henüz hiçbir şey görmeyeceksiniz, ancak tuvalimiz ayarlandı!

## Adım 2: İlk Çalışma Sayfasına Erişim

Artık çalışma kitabımız olduğuna göre, içindeki belirli bir çalışma sayfasına erişmemiz gerekiyor. Bir çalışma sayfası, çalışma kitabınızdaki tek bir sayfa gibidir ve tüm eylemin gerçekleştiği yerdir.

```csharp
//İlk çalışma sayfasına erişin
Worksheet ws = wb.Worksheets[0];
```

Burada, çalışma kitabımızdan ilk çalışma sayfasını (indeks 0) alıyoruz. Bunu bir kitabın ilk sayfasına geçmek gibi düşünebilirsiniz. 

## Adım 3: Kağıt Boyutunu Ayarlayın ve Ölçüleri Alın

Şimdi heyecan verici kısım geliyor! Farklı kağıt boyutları ayarlayıp boyutlarını tek tek alacağız. Bu adım, farklı boyutların düzeni nasıl etkilediğini görmemizi sağladığı için önemlidir.

```csharp
//Kağıt boyutunu A2 olarak ayarlayın ve kağıt genişliğini ve yüksekliğini inç olarak yazdırın
ws.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```

 Bu blokta, kağıt boyutunu A2 olarak ayarlıyoruz ve ardından genişliğini ve yüksekliğini alıyoruz.`PaperWidth` Ve`PaperHeight` özellikler boyutları inç cinsinden sağlar. Bu, bir çerçeveye resim koymadan önce boyutunu kontrol etmeye benzer.

## Adım 4: Diğer Kağıt Boyutları İçin Tekrarlayın

Diğer yaygın kağıt boyutları için işlemi tekrarlayalım. A3, A4 ve Letter boyutlarını kontrol edeceğiz. Bu tekrar, her boyutun Aspose.Cells çerçevesi içinde nasıl tanımlandığını anlamak için önemlidir.

```csharp
//Kağıt boyutunu A3 olarak ayarlayın ve kağıt genişliğini ve yüksekliğini inç olarak yazdırın
ws.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
//Kağıt boyutunu A4 olarak ayarlayın ve kağıt genişliğini ve yüksekliğini inç olarak yazdırın
ws.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
//Kağıt boyutunu Letter olarak ayarlayın ve kağıt genişliğini ve yüksekliğini inç cinsinden yazdırın
ws.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```

 Bu blokların her biri bir önceki adımı taklit eder ancak`PaperSize`mülkü buna göre ayarlayın. Sadece boyut göstergesini değiştirerek, zahmetsizce farklı kağıt boyutları elde edersiniz. Bu, depolamanız gereken şeye göre bir kutunun boyutunu değiştirmek gibidir!

## Çözüm

İşte bu kadar! Bu adımları izleyerek, Aspose.Cells for .NET'te çeşitli kağıt boyutlarının boyutlarını kolayca ayarlayabilir ve alabilirsiniz. Bu özellik size yalnızca zaman kazandırmakla kalmaz, aynı zamanda yanlış yapılandırılmış sayfa ayarları nedeniyle oluşabilecek yazdırma kazalarını da önler. Bu nedenle, bir sonraki sefere bir Excel sayfası yazdırmanız veya bir rapor oluşturmanız gerektiğinde, boyutların elinizde olduğunu bilerek bunu güvenle yapabilirsiniz. 

## SSS

### Aspose.Cells Nedir?
Aspose.Cells, Excel'in kurulu olmasına gerek kalmadan Excel dosyalarını işlemek için tasarlanmış bir .NET kütüphanesidir.

### Aspose.Cells'i ücretsiz kullanabilir miyim?
 Evet! Ücretsiz denemeye şu adresten başlayabilirsiniz:[bu bağlantı](https://releases.aspose.com/).

### Özel kağıt boyutlarını nasıl ayarlayabilirim?
 Aspose.Cells, özel kağıt boyutlarını ayarlamak için seçenekler sunar`PageSetup` sınıf.

### Aspose.Cells'i kullanmak için kodlama bilgisi gerekli mi?
Temel kodlama bilgisi yardımcı olur, ancak daha kolay anlamak için eğitimleri takip edebilirsiniz!

### Daha fazla örneği nerede bulabilirim?
 The[Aspose.Cells belgeleri](https://reference.aspose.com/cells/net/) zengin örnekler ve öğretici materyaller sunmaktadır.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
