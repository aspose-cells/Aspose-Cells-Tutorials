---
title: E-Tabloda Kullanılan Yazı Tiplerinin Listesini Alın
linktitle: E-Tabloda Kullanılan Yazı Tiplerinin Listesini Alın
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Bu kolay takip edilebilir eğitimle Aspose.Cells for .NET kullanarak Excel elektronik tablolarından yazı tiplerini nasıl getireceğinizi ve listeleyeceğinizi öğrenin.
weight: 10
url: /tr/net/working-with-fonts-in-spreadsheets/get-list-of-fonts-used-in-spreadsheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# E-Tabloda Kullanılan Yazı Tiplerinin Listesini Alın

## giriiş
Kendinizi hiç Excel elektronik tablosunda gezinirken, çeşitli hücrelerinde kullanılan yazı tiplerini merak ederken buldunuz mu? Belki eski bir belgeyle karşılaştınız ve hangi tipografi seçimlerinin yapıldığını bilmek istiyorsunuz? Şanslısınız! .NET için Aspose.Cells ile, elektronik tablolarınızda gizli olan yazı tipi sırlarını elemenize ve ortaya çıkarmanıza olanak tanıyan bir araç kutusuna sahip olmak gibi. Bu kılavuzda, bir Excel dosyasında kullanılan tüm yazı tiplerinin listesini kolayca nasıl alacağınızı göstereceğiz. Emniyet kemerlerinizi bağlayın ve elektronik tabloların dünyasına dalalım!
## Ön koşullar
Koda geçmeden önce, başlamak için ihtiyacınız olacak birkaç şey var. Endişelenmeyin, gerçekten basit. İşte ihtiyacınız olan şeylerin bir kontrol listesi:
1. Visual Studio: Makinenizde Visual Studio'nun bir sürümünün yüklü olduğundan emin olun. Kodumuzu burada yazacağız.
2. .NET için Aspose.Cells: Aspose.Cells kütüphanesinin mevcut olması gerekir. Henüz indirmediyseniz, şuradan alabilirsiniz:[alan](https://releases.aspose.com/cells/net/).
3. Temel C# Bilgisi: C# programlamaya dair biraz bilgi sahibi olmak, kodda kolayca gezinmenize kesinlikle yardımcı olacaktır.
4. Örnek Bir Excel Dosyası: Çalışmak için "sampleGetFonts.xlsx" gibi bir örnek Excel dosyasına ihtiyacınız olacak. Font keşfimizi burada uygulayacağız.
Her şeyi hallettikten sonra kodlamaya başlamaya hazırsınız!
## Paketleri İçe Aktar
Başlamak için gerekli ad alanlarını içe aktaralım. .NET'te paketleri içe aktarmak partinize doğru misafirleri davet etmeye benzer; onlar olmadan işler düzgün yürümez.
Aspose.Cells'i içe aktarmak için yapmanız gerekenler:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
Bu basit satırla, Aspose.Cells'in çekirdek işlevselliğini projemize davet ediyoruz. Şimdi, çalışma kitabını yüklemeye geçelim.
## Adım 1: Belge Dizinini Ayarlayın
İlk önce ilk şeyler—koda dalmadan önce, belge dizininize giden yolu ayarlamanız gerekir. Excel dosyanız burada bulunur. 
```csharp
string dataDir = "Your Document Directory";
```
"Belge Dizininiz"i Excel dosyanızın bulunduğu gerçek yolla değiştireceksiniz. Bunu programa "Hey, Excel dosyamı sakladığım yer burası; gidip kontrol et!" demek gibi düşünün.
## Adım 2: Kaynak Çalışma Kitabını Yükleyin
 Excel dosyasını yükleme zamanı geldi. Yeni bir örnek oluşturacağız.`Workbook` sınıf ve dosyanın yolunu girin. 
```csharp
Workbook wb = new Workbook(dataDir + "sampleGetFonts.xlsx");
```
 Burada neler oluyor? Temel olarak elektronik tablomuzun kapısını açıyoruz.`Workbook` sınıfı Excel dosyasının içeriğiyle etkileşime girmemizi sağlar. 
## Adım 3: Tüm Yazı Tiplerini Alın
 Şimdi sihirli an geldi: Hadi yazı tiplerini geri alalım!`GetFonts()` Yöntem bizim altın biletimizdir.
```csharp
Aspose.Cells.Font[] fnts = wb.GetFonts();
```
 Burada, çalışma kitabından içinde kullanılan tüm yazı tiplerini açıklamasını istiyoruz.`fnts` dizi hazinelerimizi saklayacak.
## Adım 4: Yazı Tiplerini Yazdırın
Son olarak, bu yazı tiplerini alıp yazdıralım. Bu, bulduğumuz şeyi doğrulamamıza yardımcı olacaktır.
```csharp
for (int i = 0; i < fnts.Length; i++)
{
	Console.WriteLine(fnts[i]);
}
```
 Bu döngü, her yazı tipinde çalışır`fnts` dizi, bunları tek tek konsola çıktı olarak verir. Excel dosyanızdaki tüm havalı tipografi seçimlerini göstermek gibidir!
## Çözüm
Ve işte karşınızda! Sadece birkaç satır kodla, .NET için Aspose.Cells kullanarak Excel elektronik tablonuzda kullanılan yazı tiplerinin listesini başarıyla aldınız ve yazdırdınız. Bu sadece yazı tipleriyle ilgili değil; belgelerinizin inceliklerini anlamak, sunumlarınızı geliştirmek ve elektronik tablolarınızdaki tipografi sanatında ustalaşmakla ilgilidir. İster bir geliştirici olun, ister Excel ile uğraşmayı seven biri olun, bu küçük kod parçası oyunun kurallarını değiştirebilir. 
## SSS
### Aspose.Cells'i ayrıca yüklemem gerekir mi?
Evet, projenizde kütüphaneyi indirip referans göstermeniz gerekiyor. 
### Aspose.Cells'i diğer formatlarda kullanabilir miyim?
Kesinlikle! Aspose.Cells, XLSX, XLS ve CSV gibi birden fazla Excel formatıyla çalışır.
### Ücretsiz deneme imkanı var mı?
 Evet, ücretsiz deneme sürümünü şu adresten alabilirsiniz:[indirme bağlantısı](https://releases.aspose.com/).
### Teknik destek nasıl alabilirim?
 Yardıma ihtiyacınız varsa,[Aspose destek forumu](https://forum.aspose.com/c/cells/9) harika bir kaynaktır.
### Aspose.Cells .NET Core ile uyumlu mu?
Evet, Aspose.Cells .NET Core projeleriyle de uyumludur.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
