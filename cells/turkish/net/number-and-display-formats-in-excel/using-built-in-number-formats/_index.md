---
title: Excel'de Yerleşik Sayı Biçimlerini Programlama Yoluyla Kullanma
linktitle: Excel'de Yerleşik Sayı Biçimlerini Programlama Yoluyla Kullanma
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Aspose.Cells for .NET kullanarak Excel'de sayı biçimlendirmesini otomatikleştirin. Tarih, yüzde ve para birimi biçimlerini programlı olarak nasıl uygulayacağınızı öğrenin.
weight: 10
url: /tr/net/number-and-display-formats-in-excel/using-built-in-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Yerleşik Sayı Biçimlerini Programlama Yoluyla Kullanma

## giriiş
Bu eğitimde, .NET için Aspose.Cells kullanarak Excel'de yerleşik sayı biçimlerini nasıl kullanacağınızı göstereceğiz. Ortamınızı kurmaktan tarihler, yüzdeler ve para birimleri gibi farklı biçimleri uygulamaya kadar her şeyi ele alacağız. İster deneyimli bir profesyonel olun ister .NET ekosistemine yeni adım atıyor olun, bu kılavuz Excel hücrelerini kolayca biçimlendirmenizi sağlayacak.
## Ön koşullar
Başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:
-  Aspose.Cells for .NET kütüphanesi yüklendi. Şunları yapabilirsiniz:[buradan indirin](https://releases.aspose.com/cells/net/).
- C# ve temel .NET programlama bilgisi.
- Bilgisayarınızda Visual Studio veya herhangi bir .NET IDE yüklü olmalıdır.
-  Geçerli bir Aspose lisansı veya[geçici lisans](https://purchase.aspose.com/temporary-license/).
- .NET framework yüklü (sürüm 4.0 veya üzeri).
  
Yukarıdakilerden herhangi biri eksikse, her şeyi ayarlamak için verilen bağlantıları takip edin. Hazır mısınız? Hadi eğlenceli kısma geçelim!
## Paketleri İçe Aktar
Eğitime başlamadan önce, .NET için Aspose.Cells ile çalışmak için gerekli ad alanlarını içe aktardığınızdan emin olun:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Bunları içe aktardıktan sonra Excel dosyalarını programatik olarak düzenlemeye hazırsınız. Şimdi adım adım kılavuza geçelim!
## Adım 1: Excel Çalışma Kitabınızı Oluşturun veya Erişim Sağlayın
Bu adımda yeni bir çalışma kitabı oluşturacaksınız. Bunu yeni bir Excel dosyası açmak gibi düşünün, ancak bunu kod aracılığıyla yapıyorsunuz!
```csharp
// Belgeler dizinine giden yol.
string dataDir = "Your Document Directory";
// Eğer mevcut değilse dizin oluşturun.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Bir Çalışma Kitabı nesnesini örnekleme
Workbook workbook = new Workbook();
```
 Burada, yalnızca yeni bir örnek oluşturuyoruz`Workbook` nesne. Bu, veri işleme için hazır Excel dosyanız gibi davranır. Ayrıca, yolunu sağlayarak mevcut bir dosyayı da yükleyebilirsiniz.
## Adım 2: Çalışma Sayfasına Erişim
Excel çalışma kitapları birden fazla çalışma sayfası içerebilir. Bu adımda, çalışma kitabınızdaki ilk çalışma sayfasına erişeceğiz:
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Şimdi çalışma kitabındaki ilk çalışma sayfasına erişiyoruz. Ek sayfaları düzenlemeniz gerekirse, bunlara dizinlerini veya adlarını kullanarak başvurabilirsiniz.
## Adım 3: Hücrelere Veri Ekleme
Belirli hücrelere biraz veri eklemeye başlayalım. İlk olarak, geçerli sistem tarihini "A1" hücresine ekleyeceğiz:
```csharp
worksheet.Cells["A1"].PutValue(DateTime.Now);
```
Bu satır geçerli tarihi A1 hücresine ekler. Oldukça havalı, değil mi? Bunu yüzlerce hücre için manuel olarak yaptığınızı düşünün—bir kabus olurdu. Şimdi biçimlendirmeye geçelim!
## Adım 4: "A1" Hücresindeki Tarihi Biçimlendir
Sonra, bu tarihi daha okunabilir bir formata, örneğin "15-Ekim-24" olarak biçimlendirelim. Aspose.Cells'in gerçekten parladığı yer burası:
1. Hücrenin Stilini Al:
```csharp
Style style = worksheet.Cells["A1"].GetStyle();
```
Burada, A1 hücresinin stilini yakalıyoruz. Bunu, herhangi bir değişiklik yapmadan önce hücrenin "modası"nı yakalamak olarak düşünün.
2. Tarih Formatını Ayarlayın:
```csharp
style.Number = 15;
```
 Ayarlama`Number` 15'e özellik, istenen tarih biçimini uygular. Bu, tarihleri "g-aaa-yy" biçiminde görüntülemek için yerleşik bir sayı biçimi kodudur.
3. Stili Hücreye Uygula:
```csharp
worksheet.Cells["A1"].SetStyle(style);
```
Bu satır, hücreye stil değişikliklerini uygular. Şimdi, varsayılan tarih biçimi yerine, "15-Ekim-24" gibi çok daha kullanıcı dostu bir şey göreceksiniz.
## Adım 5: "A2" Hücresine Bir Yüzde Ekleyin ve Biçimlendirin
Yüzdeleri biçimlendirmeye geçelim. Bir değer eklemek ve bunu yüzde olarak görüntülemek istediğinizi düşünün. Bu adımda, "A2" hücresine sayısal bir değer ekleyeceğiz ve bunu yüzde olarak biçimlendireceğiz:
1. Sayısal Değer Girin:
```csharp
worksheet.Cells["A2"].PutValue(20);
```
Bu, 20 sayısını A2 hücresine ekler. "Bu sadece sıradan bir sayı—bunu yüzdeye nasıl dönüştürebilirim?" diye düşünüyor olabilirsiniz. İşte, buna gelmek üzereyiz.
2. Stili Alın ve Yüzde Biçimini Ayarlayın:
```csharp
style = worksheet.Cells["A2"].GetStyle();
style.Number = 9;  // Yüzde olarak biçimlendir
worksheet.Cells["A2"].SetStyle(style);
    ```
Setting the `Number` property to 9 applies the built-in percentage format. Now the value in A2 will be displayed as "2000%." (Yes, 20 is treated as 2000% in percentage formatting).
## Step 6: Add and Format Currency in Cell "A3"
Now, let’s add a numeric value in cell A3 and format it as currency. This is a common use case for financial reports.
1. Insert Numeric Value:
```csharp
worksheet.Cells["A3"].PutValue(2546);
```
Burada, A3 hücresine 2546 ekliyoruz. Sonra, bu sayıyı para birimi olarak görünecek şekilde biçimlendireceğiz.
2. Stili Alın ve Para Birimi Biçimini Ayarlayın:
```csharp
style = worksheet.Cells["A3"].GetStyle();
style.Number = 6;  // Para birimi olarak biçimlendir
worksheet.Cells["A3"].SetStyle(style);
```
 Ayarlama`Number` 6'ya özellik para birimi biçimini uygular. Şimdi A3 hücresindeki değer virgüller ve iki ondalık basamakla birlikte "2.546,00" olarak görüntülenecektir.
## Adım 7: Excel Dosyasını Kaydedin
Artık tüm biçimlendirme sihrini uyguladığımıza göre, dosyayı kaydetme zamanı geldi:
```csharp
// Excel dosyasını kaydetme
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
 Bu satır Excel dosyasını Excel 97-2003 biçiminde kaydeder. Değiştirebilirsiniz`SaveFormat`ihtiyaçlarınıza uyacak şekilde. Ve işte böylece, programatik olarak bir Excel dosyası oluşturup biçimlendirdiniz!
## Çözüm
Tebrikler! Excel dosyasındaki hücrelere yerleşik sayı biçimlerini uygulamak için Aspose.Cells for .NET'i nasıl kullanacağınızı başarıyla öğrendiniz. Tarihlerden yüzdelere ve para birimlerine kadar, Excel veri işleme için en yaygın biçimlendirme gereksinimlerinden bazılarını ele aldık. Artık hücreleri manuel olarak biçimlendirmek yerine, tüm süreci otomatikleştirebilir ve zamandan tasarruf edebilir ve hataları azaltabilirsiniz.
## SSS
### Aspose.Cells for .NET'i kullanarak özel sayı biçimleri uygulayabilir miyim?
 Evet! Aspose.Cells yerleşik biçimlere ek olarak özel sayı biçimlerini de destekler. Aşağıdakileri kullanarak oldukça özel biçimler oluşturabilirsiniz:`Custom` mülk`Style` sınıf.
### Bir hücreyi belirli bir sembole sahip para birimi olarak nasıl biçimlendirebilirim?
 Belirli bir para birimi sembolünü uygulamak için, şunu ayarlayarak özel biçimlendirmeyi kullanabilirsiniz:`Style.Custom` mülk.
### Tüm satırları veya sütunları biçimlendirebilir miyim?
 Kesinlikle! Stilleri tüm satırlara veya sütunlara uygulayabilirsiniz.`Rows` veya`Columns`koleksiyonlar`Worksheet` nesne.
### Birden fazla hücreyi aynı anda nasıl biçimlendirebilirim?
Kullanabilirsiniz`Range` birden fazla hücreyi seçip hepsine aynı anda stil uygulamak için nesne.
### Aspose.Cells'i kullanmak için Microsoft Excel'in yüklü olması gerekir mi?
Hayır, Aspose.Cells Microsoft Excel'den bağımsız olarak çalışır, dolayısıyla bilgisayarınızda Excel'in yüklü olmasına gerek yoktur.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
