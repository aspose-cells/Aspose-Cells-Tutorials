---
title: Excel'de Çalışma Zamanında Koşullu Biçimlendirme Uygulama
linktitle: Excel'de Çalışma Zamanında Koşullu Biçimlendirme Uygulama
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Bu kapsamlı, adım adım kılavuzda, Aspose.Cells for .NET ile Excel'de çalışma zamanında koşullu biçimlendirmenin nasıl uygulanacağını öğrenin.
weight: 11
url: /tr/net/excel-conditional-formatting/applying-conditional-formatting-at-runtime/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Çalışma Zamanında Koşullu Biçimlendirme Uygulama

## giriiş

veri analizi ve görselleştirme için güçlü araçlardır. Excel'in öne çıkan özelliklerinden biri, kullanıcıların hücrelere değerlerine göre belirli biçimlendirme stilleri uygulamasına olanak tanıyan koşullu biçimlendirmedir. Bu, eğilimleri belirlemeyi, önemli veri noktalarını vurgulamayı veya verileri daha okunabilir hale getirmeyi kolaylaştırabilir. Excel dosyalarınıza programatik olarak koşullu biçimlendirme uygulamak istiyorsanız, doğru yerdesiniz! Bu kılavuzda, .NET için Aspose.Cells kullanarak çalışma zamanında koşullu biçimlendirmenin nasıl uygulanacağını ele alacağız.

## Ön koşullar
Koda dalmadan önce, başlamak için ihtiyacınız olan her şeye sahip olduğunuzdan emin olalım:

1. Visual Studio: Makinenizde Visual Studio'nun yüklü olduğundan emin olun. .NET geliştirmeyi destekleyen herhangi bir sürümü kullanabilirsiniz.
2.  Aspose.Cells for .NET: Aspose.Cells for .NET'in yüklü olması gerekir. Bunu şuradan indirebilirsiniz:[Aspose web sitesi](https://releases.aspose.com/cells/net/).
3. Temel C# Bilgisi: C# programlamaya aşina olmak, kod parçacıklarını daha iyi anlamanıza yardımcı olacaktır.
4. .NET Framework: Projenizin .NET Framework'ün uyumlu bir sürümünü hedeflediğinden emin olun.

Artık ön koşulları tamamladığımıza göre, eğlenceli kısma geçebiliriz!

## Paketleri İçe Aktar
Aspose.Cells'e başlamak için, C# projenize gerekli ad alanlarını içe aktarmanız gerekir. Bunu şu şekilde yapabilirsiniz:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Bu ad alanları, Excel dosyalarını düzenlemek ve koşullu biçimlendirmeyi uygulamak için gereken sınıflara ve yöntemlere erişmenizi sağlayacaktır.

Şimdi koşullu biçimlendirmeyi uygulama sürecini yönetilebilir adımlara bölelim.

## Adım 1: Projenizi Kurun
İlk önce, Visual Studio'da yeni bir C# projesi oluşturmanız gerekiyor. İşte nasıl:

1. Visual Studio'yu açın ve Dosya > Yeni > Proje'yi seçin.
2. Konsol Uygulamasını (.NET Framework) seçin ve projenize bir isim verin.
3. Oluştur’a tıklayın.

## Adım 2: Aspose.Cells Referansını Ekleyin
Projeniz kurulduktan sonra Aspose.Cells kütüphanesine bir başvuru eklemeniz gerekir:

1. Çözüm Gezgini’nde projenizin üzerine sağ tıklayın.
2. NuGet Paketlerini Yönet'i seçin.
3. Aspose.Cells'i arayın ve yükleyin.

Bu, Aspose.Cells kütüphanesinin sağladığı tüm işlevleri kullanmanıza olanak tanıyacaktır.

## Adım 3: Bir Çalışma Kitabı Nesnesi Oluşturun
Şimdi yeni bir çalışma kitabı ve bir çalışma sayfası oluşturalım. Tüm sihir burada gerçekleşir:

```csharp
// Belgeler dizinine giden yol.
string dataDir = "Your Document Directory";
string filePath = dataDir + "Book1.xlsx";

// Bir Çalışma Kitabı nesnesini örnekleme
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

Bu adımda Excel dosyamızın kaydedileceği dizini tanımlıyoruz, yeni bir çalışma kitabı oluşturuyoruz ve ilk çalışma sayfasına erişiyoruz.

## Adım 4: Koşullu Biçimlendirmeyi Ekleyin
Şimdi biraz koşullu biçimlendirme ekleyelim. Boş bir koşullu biçimlendirme nesnesi oluşturarak başlayacağız:

```csharp
// Boş bir koşullu biçimlendirme ekler
int index = sheet.ConditionalFormattings.Add();
FormatConditionCollection fcs = sheet.ConditionalFormattings[index];
```

Burada, çalışma sayfamıza biçimlendirme kurallarımızı tutacak yeni bir koşullu biçimlendirme koleksiyonu ekliyoruz.

## Adım 5: Biçim Aralığını Tanımlayın
Sonra, koşullu biçimlendirmenin uygulanacağı hücre aralığını belirtmemiz gerekir. Diyelim ki ilk satırı ve ikinci sütunu biçimlendirmek istiyoruz:

```csharp
// Koşullu biçimlendirme aralığını ayarlar.
CellArea ca = new CellArea();
ca.StartRow =0;
ca.EndRow =0;
ca.StartColumn =0;
ca.EndColumn =0;
fcs.AddArea(ca);

ca = new CellArea();
ca.StartRow =1;
ca.EndRow =1;
ca.StartColumn =1;
ca.EndColumn =1;
fcs.AddArea(ca);
```

Bu kodda, koşullu biçimlendirme için iki alan tanımlıyoruz. İlk alan (0,0) hücresinde, ikincisi ise (1,1) hücresindedir. Bu aralıkları kendi özel ihtiyaçlarınıza göre ayarlamakta özgürsünüz!

## Adım 6: Koşullu Biçimlendirme Koşullarını Ekleyin
Şimdi biçimlendirmemiz için koşulları tanımlamanın zamanı geldi. Hücreleri değerlerine göre vurgulamak istediğimizi varsayalım:

```csharp
// Koşul ekler.
int conditionIndex = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "=A2", "100");

// Koşul ekler.
int conditionIndex2 = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "50", "100");
```

 Bu adımda iki koşul ekliyoruz: biri arasındaki değerler için`A2` Ve`100` ve bir diğeri ise arasındaki değerler için`50` Ve`100`. Bu, hücreleri değerlerine göre dinamik olarak vurgulamanıza olanak tanır.

## Adım 7: Biçimlendirme Stillerini Ayarlayın
Koşullarımız yerinde olduğuna göre artık biçimlendirme stillerini ayarlayabiliriz. Koşullarımız için arka plan rengini değiştirelim:

```csharp
// Arka plan rengini ayarlar.
FormatCondition fc = fcs[conditionIndex];
fc.Style.BackgroundColor = Color.Red;
```

Burada, ilk koşulun arka plan rengini kırmızıya ayarlıyoruz. Bunu, yazı tipi rengini, kenarlıkları ve diğer stilleri gerektiği gibi değiştirerek daha da özelleştirebilirsiniz!

## Adım 8: Excel Dosyasını Kaydedin
Son olarak çalışmamızı kaydetme zamanı geldi! Çalışma kitabını belirtilen dizine kaydedeceğiz:

```csharp
// Excel dosyasını kaydetme
workbook.Save(dataDir + "output.xls");
```

Bu kod satırı, koşullu biçimlendirme uygulanmış Excel dosyasını kaydeder. Çıktı dosyanız için belirtilen dizini kontrol ettiğinizden emin olun!

## Çözüm
İşte karşınızda! Aspose.Cells for .NET kullanarak Excel'de çalışma zamanında koşullu biçimlendirmeyi başarıyla uyguladınız. Bu güçlü kitaplık, Excel dosyalarını programatik olarak yönetmenizi kolaylaştırarak sıkıcı görevleri otomatikleştirmenize ve veri sunumlarınızı geliştirmenize olanak tanır. İster küçük bir projede ister büyük ölçekli bir uygulamada çalışıyor olun, Aspose.Cells iş akışınızı kolaylaştırmanıza ve üretkenliğinizi artırmanıza yardımcı olabilir.

## SSS

### Aspose.Cells Nedir?
Aspose.Cells, geliştiricilerin Excel dosyalarını program aracılığıyla oluşturmalarına, düzenlemelerine ve dönüştürmelerine olanak tanıyan bir .NET kütüphanesidir.

### Aspose.Cells'i diğer programlama dilleriyle birlikte kullanabilir miyim?
Evet, Aspose.Cells Java, Python ve daha fazlası dahil olmak üzere birden fazla programlama dili için kullanılabilir.

### Aspose.Cells için ücretsiz deneme sürümü mevcut mu?
 Evet, ücretsiz deneme sürümünü şu adresten indirebilirsiniz:[Aspose web sitesi](https://releases.aspose.com/).

### Aspose.Cells için nasıl destek alabilirim?
 Destek almak için şu adresi ziyaret edebilirsiniz:[Aspose destek forumu](https://forum.aspose.com/c/cells/9).

### Aspose.Cells'i kullanmak için lisansa ihtiyacım var mı?
 Evet, ticari kullanım için lisans gereklidir, ancak geçici bir lisans talep edebilirsiniz[Burada](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
