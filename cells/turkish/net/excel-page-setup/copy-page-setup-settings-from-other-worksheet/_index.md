---
title: Sayfa Kurulum Ayarlarını Diğer Çalışma Sayfasından Kopyala
linktitle: Sayfa Kurulum Ayarlarını Diğer Çalışma Sayfasından Kopyala
second_title: Aspose.Cells for .NET API Başvurusu
description: Bu adım adım kılavuzla, elektronik tablo yönetiminizi geliştirmek için mükemmel olan Aspose.Cells for .NET'i kullanarak çalışma sayfaları arasında sayfa düzeni ayarlarını kopyalamayı öğrenin.
weight: 10
url: /tr/net/excel-page-setup/copy-page-setup-settings-from-other-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sayfa Kurulum Ayarlarını Diğer Çalışma Sayfasından Kopyala

## giriiş

Hiç kendinizi bir çalışma sayfasından diğerine sayfa ayarlarını kopyalamanız gereken bir durumda buldunuz mu? İster finansal raporlarla ister proje zaman çizelgeleriyle çalışıyor olun, sunumda tekdüzelik esastır. .NET için Aspose.Cells ile sayfa düzeni ayarlarını çalışma sayfaları arasında kolayca kopyalayabilirsiniz. Bu kılavuz, .NET veya Aspose.Cells ile yeni başlıyor olsanız bile, süreci adım adım basit ve anlaşılır hale getirerek size yol gösterecektir. Başlamaya hazır mısınız? Hadi başlayalım!

## Ön koşullar

Koda geçmeden önce, yerinde olması gereken birkaç temel öğe vardır:

1. .NET Geliştirme Ortamı: Visual Studio veya tercih ettiğiniz herhangi bir IDE gibi .NET uyumlu bir ortamınızın olduğundan emin olun.
2.  Aspose.Cells Kütüphanesi: Aspose.Cells kütüphanesine ihtiyacınız olacak.[buradan indirin](https://releases.aspose.com/cells/net/).
3. C# Temel Anlayışı: C# temellerini bilmek, kavramları daha iyi kavramanıza kesinlikle yardımcı olacaktır.
4.  Aspose.Cells Belgeleri: Kendinizi şu konularda bilgilendirin:[belgeleme](https://reference.aspose.com/cells/net/) Daha sonra işinize yarayabilecek gelişmiş yapılandırmalar veya ek özellikler için.

Artık ön koşullarımız tamam olduğuna göre, gerekli paketleri içe aktaralım!

## Paketleri İçe Aktar

Projenizde Aspose.Cells kullanmaya başlamak için, kodunuza aşağıdaki paketi aktarmanız gerekir:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Bu tek satır, Aspose.Cells kütüphanesinin tüm güçlü bileşenlerine erişmenizi sağlar.

Her bir bölümü tam olarak anlamanızı sağlamak için tüm süreci yönetilebilir adımlara bölelim. Bir çalışma kitabı oluşturacağız, iki çalışma sayfası ekleyeceğiz, birinin sayfa düzenini değiştireceğiz ve sonra bu ayarları diğerine kopyalayacağız.

## Adım 1: Bir Çalışma Kitabı Oluşturun

Çalışma Kitabınızı Oluşturun:
 İlk olarak, bir örnek oluşturmanız gerekir`Workbook` sınıf. Bu esasen sizin başlangıç noktanızdır. 

```csharp
Workbook wb = new Workbook();
```

Bu satır, çalışma sayfalarınızı saklayacağınız çalışma kitabını başlatır.

## Adım 2: Çalışma Sayfaları Ekleyin

Çalışma Kitabınıza Çalışma Sayfaları Ekleyin:
Artık çalışma kitabınız hazır, şimdi birkaç çalışma sayfası eklemenin zamanı geldi.

```csharp
wb.Worksheets.Add("TestSheet1");
wb.Worksheets.Add("TestSheet2");
```

Burada, "TestSheet1" ve "TestSheet2" adlı iki çalışma sayfası ekledik. Bu, çalışma kitabınızda içeriği bağımsız olarak yönetebileceğiniz iki farklı sayfa oluşturmak gibidir.

## Adım 3: Çalışma Sayfalarına Erişim

Çalışma Sayfalarınıza Erişim:
Daha sonra, değişiklik yapmak için yeni oluşturduğunuz çalışma sayfalarına erişmeniz gerekecektir.

```csharp
Worksheet TestSheet1 = wb.Worksheets["TestSheet1"];
Worksheet TestSheet2 = wb.Worksheets["TestSheet2"];
```

Artık her iki çalışma sayfasına da referanslarınız var, böylece özelliklerini kolayca ayarlayabilirsiniz.

## Adım 4: TestSheet1 için Kağıt Boyutunu Ayarlayın

Sayfa Ayarını Değiştir:
 "TestSheet1"in kağıt boyutunu şu şekilde ayarlayalım:`PaperA3ExtraTransverse`.

```csharp
TestSheet1.PageSetup.PaperSize = PaperSizeType.PaperA3ExtraTransverse;
```

Belgeniz belirli bir baskı düzeni için tasarlanmışsa bu adım çok önemlidir. Sanat eseriniz için bir tuval boyutu seçmek gibidir.

## Adım 5: Mevcut Kağıt Boyutlarını Yazdırın

Mevcut Kağıt Boyutunu Kontrol Edin:
Şimdi kopyalama işleminden önce mevcut kağıt boyutlarının ne olduğuna bakalım.

```csharp
Console.WriteLine("Before Paper Size: " + TestSheet1.PageSetup.PaperSize);
Console.WriteLine("Before Paper Size: " + TestSheet2.PageSetup.PaperSize);
```

Bu, her iki çalışma sayfası için geçerli sayfa düzenini konsola çıktı olarak verecektir. Değişiklik yapmadan önce neye sahip olduğunuzu doğrulamak her zaman iyidir, değil mi?

## Adım 6: Sayfa Düzenini TestSheet1'den TestSheet2'ye Kopyala

Sayfa Yapısı Ayarlarını Kopyalayın:
İşte heyecan verici kısım geldi! Tüm sayfa düzeni ayarlarını "TestSheet1"den "TestSheet2"ye kopyalayabilirsiniz.

```csharp
TestSheet2.PageSetup.Copy(TestSheet1.PageSetup, new CopyOptions());
```

Bu kod satırı esasen "TestSheet1"in tüm biçimlendirmesini alır ve "TestSheet2"ye uygular. Bir sayfanın anlık görüntüsünü alıp başka bir sayfaya yapıştırmak gibidir!

## Adım 7: Güncellenmiş Kağıt Boyutlarını Yazdırın

Kağıt Boyutlarını Tekrar Kontrol Edin:
Son olarak ayarların başarıyla kopyalandığını doğrulayalım.

```csharp
Console.WriteLine("After Paper Size: " + TestSheet1.PageSetup.PaperSize);
Console.WriteLine("After Paper Size: " + TestSheet2.PageSetup.PaperSize);
Console.WriteLine();
Console.WriteLine("CopyPageSetupSettingsFromSourceWorksheetToDestinationWorksheet executed successfully.\r\n");
```

Kopyalama işleminden sonra her iki çalışma sayfasının sayfa boyutlarının eşleştiğini görmelisiniz. İşte bu kadar! Ayarlar sorunsuz bir şekilde aktarıldı.

## Adım 8: Çalışma Kitabınızı Kaydedin

Değişikliklerinizi Kaydedin:
Bütün bu sıkı çalışmalardan sonra çalışma kitabınızı kaydetmeyi unutmayın!

```csharp
wb.Save("CopiedPageSetupExample.xlsx");
```

Çalışma kitabını kaydetmek, tüm değişikliklerinizin kalıcı olduğundan emin olmak için önemlidir. Bu adımı, bir belgeyi bitirdikten sonra "kaydet" tuşuna basmak olarak düşünün — hiçbir ilerlemeyi kaybetmemek için çok önemlidir!

## Çözüm

.NET için Aspose.Cells'i kullanmak çalışma sayfalarını yönetmeyi çocuk oyuncağı haline getirir. Sayfa düzenlerini bir çalışma sayfasından diğerine kolayca kopyalayabilir, belgeleriniz boyunca tutarlılığı korumanıza yardımcı olur. Bu kılavuzda özetlenen ayrıntılı adımlarla çalışma kitabınızın sayfa ayarlarını güvenle değiştirebilir ve biçimlendirmede zamandan tasarruf edebilirsiniz. 

## SSS

### Aspose.Cells Nedir?  
Aspose.Cells, .NET uygulamalarında elektronik tablolarla çalışmak için güçlü bir kütüphanedir.

### Aspose.Cells'i diğer programlama dilleriyle birlikte kullanabilir miyim?  
Aspose.Cells öncelikli olarak .NET dillerini destekler, ancak farklı diller için başka Aspose kütüphaneleri de vardır.

### Aspose.Cells için ücretsiz deneme sürümü mevcut mu?  
 Evet, indirebilirsiniz[ücretsiz deneme](https://releases.aspose.com/) Aspose.Cells'in.

### Aspose.Cells için desteği nasıl alabilirim?  
 Desteğe şu şekilde erişebilirsiniz:[Aspose forumu](https://forum.aspose.com/c/cells/9).

### Aspose.Cells için geçici lisans alabilir miyim?  
Kesinlikle! Bir tane talep edebilirsiniz[geçici lisans](https://purchase.aspose.com/temporary-license/) Ürünü değerlendirmek için.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
