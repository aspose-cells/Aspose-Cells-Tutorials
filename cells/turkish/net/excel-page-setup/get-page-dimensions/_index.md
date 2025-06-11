---
"description": "Bu adım adım kılavuzda Aspose.Cells for .NET kullanarak sayfa boyutlarının nasıl alınacağını öğrenin. Excel dosyalarıyla çalışan geliştiriciler için mükemmeldir."
"linktitle": "Sayfa Boyutlarını Al"
"second_title": "Aspose.Cells for .NET API Başvurusu"
"title": "Sayfa Boyutlarını Al"
"url": "/tr/net/excel-page-setup/get-page-dimensions/"
"weight": 40
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Sayfa Boyutlarını Al

## giriiş

.NET uygulamalarında elektronik tabloları işlemek söz konusu olduğunda, Aspose.Cells kitaplığı geliştiricilerin Excel dosyalarını kolayca düzenlemelerine olanak tanıyan sağlam bir araç olarak öne çıkıyor. Peki bu güçlü kitaplıkla çeşitli kağıt boyutları için sayfa boyutlarını nasıl elde edersiniz? Bu eğitimde, yalnızca Aspose.Cells'in işleyişine dair içgörü kazanmanızı değil, aynı zamanda projelerinizde kullanma konusunda da ustalaşmanızı sağlayarak süreci adım adım ele alacağız. 

## Ön koşullar 

Kodlama kısmına geçmeden önce, etkili bir şekilde takip edebilmeniz için sahip olmanız gereken birkaç şey var:

### Görsel Stüdyo
Makinenizde Visual Studio'nun yüklü olduğundan emin olun. .NET kodunuzu burada yazıp çalıştıracaksınız.

### Aspose.Cells Kütüphanesi
Projenizde Aspose.Cells kütüphanesini indirmeniz ve referans vermeniz gerekecektir. Bunu şuradan edinebilirsiniz:
- İndirme Bağlantısı: [.NET için Aspose.Cells](https://releases.aspose.com/cells/net/)

### C# Temel Bilgisi
C# hakkında temel bir anlayışa sahip olmanız faydalı olacaktır. Bu eğitim, takip edilmesi kolay olması gereken temel programlama kavramlarını kullanacaktır.

Hazır mısınız? Hadi başlayalım!

## Paketleri İçe Aktarma

Yolculuğumuzun ilk adımı, gerekli Aspose.Cells paketlerini C# projemize aktarmaktır. Bunu nasıl yapabileceğiniz aşağıda açıklanmıştır:

### Yeni Bir Proje Oluştur

Visual Studio'yu açın ve yeni bir C# Konsol Uygulaması projesi oluşturun. İstediğiniz ismi verebilirsiniz, hadi başlayalım `GetPageDimensions`.

### Referans Ekle

Aspose.Cells'i kullanmak için kütüphaneye referanslar eklemeniz gerekir:
- Çözüm Gezgini’nde projenizin üzerine sağ tıklayın.
- “NuGet Paketlerini Yönet” seçeneğini seçin.
- “Aspose.Cells”i arayın ve yükleyin.

### Yönergeleri Kullanarak Ekle

En üstte `Program.cs` dosyasına, Aspose.Cells işlevselliğine erişmek için bu using yönergesini ekleyin:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Artık gerekli paketleri içe aktardığımıza göre doğru yoldasınız! 

Şimdi her adımı inceleyerek çeşitli kağıt boyutlarının boyutlarının nasıl alınacağını inceleyelim. 

## Adım 1: Çalışma Kitabı Sınıfının Bir Örneğini Oluşturun

Yapmanız gereken ilk şey Aspose.Cells'den Workbook sınıfının bir örneğini oluşturmaktır. Bu sınıf bir Excel dosyasını temsil eder.

```csharp
Workbook book = new Workbook();
```

Burada, elektronik tablo verilerimizi ve yapılandırmalarımızı tutacak yeni bir çalışma kitabı oluşturuyoruz.

## Adım 2: İlk Çalışma Sayfasına Erişim

Çalışma kitabının bir örneğini oluşturduktan sonra, ilk çalışma sayfasına erişmek isteyeceksiniz. Her çalışma kitabı birden fazla çalışma sayfası içerebilir, ancak bu gösteri için ilkine bağlı kalacağız.

```csharp
Worksheet sheet = book.Worksheets[0];
```

Bu satır ilk çalışma sayfasını getirir ve kağıt boyutlarını ayarlamamıza ve ilgili ölçülerini almamıza olanak tanır.

## Adım 3: Kağıt Boyutunu A2 Olarak Ayarlama ve Boyutları Alma

Şimdi kağıt boyutunu ayarlama ve boyutları alma zamanı! A2 kağıt boyutuyla başlıyoruz.

```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```

Bu kod kağıt boyutunu A2 olarak ayarlar ve hemen genişliği ve yüksekliği çıktı olarak verir. Aspose.Cells'in güzelliği basitliğindedir!

## Adım 4: Diğer Kağıt Boyutları İçin Tekrarlayın

Bu işlemi A3, A4 ve Letter gibi diğer kağıt boyutları için tekrarlamak isteyeceksiniz. Bunu nasıl yapabileceğiniz aşağıda açıklanmıştır:

A3 için:

```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```

A4 için:

```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```

Mektup İçin:

```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```

## Adım 5: Çıktının Sonucu

Son olarak, tüm işlemin başarıyla tamamlandığını onaylamak isteyeceksiniz. Bu durumu konsola kaydedebilirsiniz:

```csharp
Console.WriteLine("GetPageDimensions executed successfully.\r\n");
```

## Çözüm

Tebrikler! Artık Aspose.Cells for .NET kullanarak farklı kağıt boyutları için sayfa boyutlarını nasıl alacağınızı başarıyla öğrendiniz. İster raporlama araçları, ister otomatik elektronik tablolar veya veri analizi işlevleri geliştiriyor olun, çeşitli biçimler için sayfa boyutlarını çekebilmek paha biçilmez olabilir. 

## SSS

### Aspose.Cells Nedir?
Aspose.Cells, Microsoft Excel'e ihtiyaç duymadan Excel dosyaları oluşturmak, düzenlemek ve dönüştürmek için kullanılan bir .NET kütüphanesidir.

### Aspose.Cells'i kullanmak için Microsoft Excel'i yüklemem gerekiyor mu?
Hayır, Aspose.Cells bağımsız bir kütüphanedir ve Excel'in kurulu olmasını gerektirmez.

### Aspose.Cells için daha fazla örneği nerede bulabilirim?
Dokümantasyonu buradan inceleyebilirsiniz: [Aspose.Cells Belgeleri](https://reference.aspose.com/cells/net/).

### Aspose.Cells'in ücretsiz deneme sürümü var mı?
Evet! Ücretsiz deneme sürümünü şuradan edinebilirsiniz: [Aspose.Cells Ücretsiz Deneme](https://releases.aspose.com/).

### Aspose.Cells için nasıl destek alabilirim?
Aspose destek forumunu ziyaret ederek yardım alabilirsiniz: [Aspose.Cells Desteği](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}