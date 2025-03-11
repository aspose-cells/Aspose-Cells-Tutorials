---
title: Excel'de Eklentiden Fonksiyon Kaydetme ve Çağırma
linktitle: Excel'de Eklentiden Fonksiyon Kaydetme ve Çağırma
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Aspose.Cells for .NET kullanarak Excel'de eklentilerden fonksiyonları nasıl kaydedeceğinizi ve çağıracağınızı kolay adım adım eğitimimiz ile öğrenin.
weight: 20
url: /tr/net/excel-formulas-and-calculation-options/registering-and-calling-function-from-add-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Eklentiden Fonksiyon Kaydetme ve Çağırma

## giriiş
Bir eklentiden işlevleri çağırarak Excel deneyiminizi geliştirmek ister misiniz? Cevabınız evetse, doğru yerdesiniz! Excel eklentileri, elektronik tabloların peri anneleri gibidir; işlevselliği sihirli bir şekilde genişleterek parmaklarınızın ucunda bir sürü yeni araç sunar. Ve .NET için Aspose.Cells ile bu eklenti işlevlerini kaydetmek ve kullanmak her zamankinden daha kolay. 
Bu kılavuzda, Aspose.Cells for .NET kullanarak bir Excel eklentisinden bir fonksiyonu kaydetme ve çağırma sürecini adım adım anlatacağım. Her şeyi adım adım açıklayacağız, böylece kısa sürede kendinizi bir profesyonel gibi hissedeceksiniz!
## Ön koşullar
Kodlama sihirbazlığına dalmadan önce, neye ihtiyacınız olduğunu ele alalım:
1. Visual Studio: Makinenizde Visual Studio'nun kurulu olduğundan emin olun. Kodumuzu burada yazıp çalıştıracağız.
2.  Aspose.Cells Kütüphanesi: Aspose.Cells kütüphanesinin kurulu olması gerekir. Bunu şu adresten alabilirsiniz:[indirme sayfası](https://releases.aspose.com/cells/net/).
3. Temel C# Bilgisi: C# hakkında biraz bilgi sahibi olmak çok işinize yarayacak; konuyu sorunsuz bir şekilde takip etmenize yardımcı olacaktır.
4.  Excel Eklentileri: Bir eklenti dosyanız (örneğin) olmalıdır.`.xlam`) kaydetmek ve kullanmak istediğiniz fonksiyonları içeren.
5.  Örnek Bir Excel Eklentisi: Bu eğitim için, adında bir Excel eklentisi kullanacağız.`TESTUDF.xlam`O yüzden bunu mutlaka elinizin altında bulundurun!
Artık kurulumunuz tamamlandığına göre kolları sıvayıp kodlamaya başlayabiliriz!
## Paketleri İçe Aktarma
Başlamak için, C# dosyanızın en üstüne bazı temel ad alanlarını içe aktarmanız gerekir. İşte eklemeniz gerekenler:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Bu ad alanları, bu eğitimde kullanacağımız sınıflara ve metotlara erişmenizi sağlayacak.
Bunu yönetilebilir adımlara bölelim. Bu kılavuzun sonunda, eklenti işlevlerini nasıl kaydedeceğiniz ve bunları Excel çalışma kitaplarınızda nasıl kullanacağınız konusunda sağlam bir anlayışa sahip olacaksınız.
## Adım 1: Kaynak ve Çıktı Dizinlerinizi Ayarlayın
Eklentinizi kaydedebilmeniz için eklentinizin ve çıktı dosyalarınızın nerede bulunacağını tanımlamanız gerekir.
```csharp
// Kaynak dizini
string sourceDir = "Your Document Directory";
// Çıktı dizini
string outputDir = "Your Document Directory";
```
 Yer değiştirmek`"Your Document Directory"` gerçek yolunuzla`.xlam` dosya ve çıktı dosyaları kaydedilecektir. Bu, gösteri başlamadan önce sahneyi hazırlamak gibidir.
## Adım 2: Boş bir Çalışma Kitabı Oluşturun
Daha sonra eklenti fonksiyonlarıyla oynayabileceğimiz boş bir çalışma kitabı oluşturmak isteyeceksiniz.
```csharp
// Boş çalışma kitabı oluştur
Workbook workbook = new Workbook();
```
Bu kod satırı oyun alanımız olarak hizmet edecek yeni bir çalışma kitabı oluşturur. Bunu yaratıcı vuruşlarınız için hazır, taze bir tuval olarak düşünün.
## Adım 3: Eklenti İşlevini Kaydedin
Şimdi, meselenin özüne gelelim! Eklenti işlevinizi kaydetmenin zamanı geldi. İşte bunu nasıl yapacağınız:
```csharp
// Makro etkinleştirilmiş eklentiyi fonksiyon adıyla birlikte kaydedin
int id = workbook.Worksheets.RegisterAddInFunction(sourceDir + @"TESTUDF.xlam", "TEST_UDF", false);
```
 Bu satır, eklentinin şu adlı işlevini kaydeder:`TEST_UDF` içinde bulundu`TESTUDF.xlam` eklenti dosyası.`false`parametresi eklentinin 'izole' modda yüklenmediği anlamına gelir. 
## Adım 4: Ek Fonksiyonları Kaydedin (Eğer Varsa)
Aynı eklenti dosyasında kayıtlı daha fazla fonksiyonunuz varsa, onları da kaydedebilirsiniz!
```csharp
// Dosyaya daha fazla işlev kaydedin (eğer varsa)
workbook.Worksheets.RegisterAddInFunction(id, "TEST_UDF1");
```
Burada, aynı eklentiden daha fazla işlev eklemenin ne kadar kolay olduğunu görebilirsiniz. Sadece onları yapı taşları gibi istiflemeye devam edin!
## Adım 5: Çalışma Sayfasına Erişim
Şimdi devam edelim ve fonksiyonumuzu kullanacağımız çalışma kağıdına geçelim. 
```csharp
// İlk çalışma sayfasına erişin
Worksheet worksheet = workbook.Worksheets[0];
```
Formülümüzü yerleştirmek için çalışma kitabındaki ilk çalışma sayfasına erişiyoruz. Eğlencenin yaşandığı odanın kapısını açmak gibi.
## Adım 6: Belirli Bir Hücreye Erişim
Şimdi formülümüz için hangi hücreyi kullanmak istediğimizi seçmemiz gerekiyor. 
```csharp
// İlk hücreye erişim
var cell = worksheet.Cells["A1"];
```
Burada A1 hücresini işaret ediyoruz. Sihirli formülümüzü buraya bırakacağız. Bunu hazine haritanıza bir hedef sabitlemek olarak düşünebilirsiniz!
## Adım 7: Formülü Ayarlayın
Şimdi büyük açıklamanın zamanı geldi! Kayıtlı fonksiyonumuzu çağıran formülü ayarlayalım.
```csharp
// Eklentide bulunan formül adını ayarlayın
cell.Formula = "=TEST_UDF()";
```
Bu satırla Excel'e A1 hücresindeki fonksiyonumuzu kullanmasını söylüyoruz. Excel'e bir komut verip "Hey, bunu yap!" demek gibi.
## Adım 8: Çalışma Kitabını Kaydedin
Son olarak, şaheserimizi kurtarmanın zamanı geldi.
```csharp
// Çalışma kitabını XLSX formatında çıktı olarak kaydedin.
workbook.Save(outputDir + @"test_udf.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```
Burada, çalışma kitabımızı XLSX dosyası olarak kaydediyoruz. Bu son adım, resminizi bir çerçeveye koyup sergilemeye hazırlanmak gibidir!
## Adım 9: Yürütmeyi Onaylayın
Son olarak konsola bir başarı mesajı yazdırarak işi bitirelim.
```csharp
Console.WriteLine("RegisterAndCallFuncFromAddIn executed successfully.");
```
Bu çizgi bizim zafer bayrağımız olarak işlev görüyor. Her şeyin yolunda gittiğini teyit etmek için hoş bir dokunuş.
## Çözüm 
Ve işte karşınızda! Sadece .NET için Aspose.Cells kullanarak Excel eklentilerinden işlevleri nasıl kaydedeceğinizi ve çağıracağınızı öğrenmekle kalmadınız, aynı zamanda dahil olan her adım hakkında daha derin bir anlayış da kazandınız. Hayat şimdi biraz daha kolay, değil mi? Öyleyse neden kendiniz denemiyorsunuz? Bu Excel eklentilerine dalın ve elektronik tablolarınıza yeni bir etkileşim ve işlevsellik düzeyi kazandırın.
## SSS
### Excel Eklentisi Nedir?  
Excel Eklentisi, Excel'e özel özellikler, işlevler veya komutlar ekleyerek kullanıcıların yeteneklerini genişletmesine olanak tanıyan bir programdır.
### Aspose.Cells'i yerel olarak yüklemeden kullanabilir miyim?  
Hayır, .NET uygulamalarınızda kullanmak için Aspose.Cells kütüphanesini yüklemeniz gerekir.
### Aspose.Cells için geçici lisansı nasıl alabilirim?  
 Onları ziyaret edebilirsiniz[geçici lisans sayfası](https://purchase.aspose.com/temporary-license/) Daha fazla bilgi için.
### Tek bir eklentiden birden fazla fonksiyonu çağırmak mümkün müdür?  
 Evet! Aynı eklenti dosyasından birden fazla işlevi kaydedebilirsiniz.`RegisterAddInFunction` yöntem.
### Aspose.Cells hakkında daha fazla dokümanı nerede bulabilirim?  
 Sitede kapsamlı dokümantasyonlarını inceleyebilirsiniz[Burada](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
