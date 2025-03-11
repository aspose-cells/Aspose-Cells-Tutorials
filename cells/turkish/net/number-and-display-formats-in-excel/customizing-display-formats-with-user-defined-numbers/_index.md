---
title: Kullanıcı Tarafından Tanımlanan Sayılarla Görüntüleme Biçimlerini Özelleştirme
linktitle: Kullanıcı Tarafından Tanımlanan Sayılarla Görüntüleme Biçimlerini Özelleştirme
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Aspose.Cells for .NET ile görüntüleme biçimlerini nasıl özelleştireceğinizi öğrenin. Bu adım adım kılavuzu kullanarak tarihleri, yüzdeleri ve para birimini biçimlendirin.
weight: 11
url: /tr/net/number-and-display-formats-in-excel/customizing-display-formats-with-user-defined-numbers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kullanıcı Tarafından Tanımlanan Sayılarla Görüntüleme Biçimlerini Özelleştirme

## giriiş
Excel dosyalarıyla çalışmak, verileri daha anlamlı ve kullanıcı dostu bir şekilde sunmak için hücrelerin özel biçimlendirilmesini gerektirir. Bir rapor için bir Excel dosyası oluşturduğunuzu düşünün. Sadece ham sayılar istemezsiniz. Tarihlerin, yüzdelerin ve para birimlerinin şık ve profesyonel görünmesini istersiniz, değil mi? İşte tam bu noktada özel görüntüleme biçimleri devreye girer. Bu eğitimde, kullanıcı tanımlı ayarları kullanarak sayıların görüntüleme biçimini nasıl özelleştireceğinizi göstermek için Aspose.Cells for .NET'e derinlemesine iniyoruz.
## Ön koşullar
Başlamadan önce, bu öğreticiyi takip etmek için her şeyin hazır olduğundan emin olun. İhtiyacınız olanlar şunlardır:
-  .NET için Aspose.Cells kuruldu.[Buradan indirin](https://releases.aspose.com/cells/net/).
- C# ve .NET framework hakkında temel bilgi.
-  Aspose.Cells için geçerli bir lisans. Eğer yoksa, bir tane edinin[ücretsiz deneme](https://releases.aspose.com/) veya bir talepte bulunun[geçici lisans](https://purchase.aspose.com/temporary-license/).
- Visual Studio benzeri bir IDE.
- .NET Framework 4.0 veya üzeri.
 Eğer bir şeyi kaçırıyorsanız endişelenmeyin. Gerekli dosyaları indirmek veya yardım almak için bu bağlantıları her zaman tekrar ziyaret edebilirsiniz.[Aspose destek forumu](https://forum.aspose.com/c/cells/9).
## Ad Alanlarını İçe Aktar
Koda geçmeden önce, gerekli tüm Aspose.Cells işlevlerine erişmek için gerekli ad alanlarını içe aktarmanız gerekir.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Bu iki ad alanı bu eğitimde temel araçlarınız olacak. Şimdi, eğlenceli kısma geçelim:
## Adım 1: Proje Dizininin Kurulması
Öncelikle dosyalarınızı depolayacak bir yere ihtiyacınız var, değil mi? Çıktı Excel dosyasını kaydetmek için bir dizin oluşturalım. Bu adımda, herhangi bir şeyi kaydetmeden önce dizinin var olduğundan da emin olacağız.
```csharp
// Belgeler dizinine giden yol.
string dataDir = "Your Document Directory";
// Eğer mevcut değilse dizin oluşturun.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
-  Bir tanım yapıyoruz`dataDir` Çıktı Excel dosyasının gideceği yolu saklayan değişken.
-  Daha sonra dizinin var olup olmadığını şu şekilde kontrol ederiz:`System.IO.Directory.Exists()`.
-  Dizin mevcut değilse, şu şekilde oluşturulacaktır:`System.IO.Directory.CreateDirectory()`.
## Adım 2: Yeni bir Çalışma Kitabı Oluşturun ve Bir Çalışma Sayfası Ekleyin
Artık dizinimiz hazır olduğuna göre, yeni bir Excel çalışma kitabı oluşturalım ve buna bir çalışma sayfası ekleyelim.
```csharp
// Bir Çalışma Kitabı nesnesini örnekleme
Workbook workbook = new Workbook();
// Excel nesnesine yeni bir çalışma sayfası ekleme
int i = workbook.Worksheets.Add();
// Yeni eklenen çalışma sayfasının referansını sayfa indeksini geçirerek elde etme
Worksheet worksheet = workbook.Worksheets[i];
```
-  İlk olarak yeni bir tane oluşturuyoruz`Workbook` nesne. Bunu Excel dosyanız olarak düşünün.
-  Bu çalışma kitabına yeni bir çalışma sayfası ekliyoruz`Add()`yöntem ve indeksi değişkende depolamak`i`.
-  Bu çalışma sayfasına şu şekilde başvuruyoruz:`workbook.Worksheets[i]`.
## Adım 3: Bir Hücreye Tarih Ekleme ve Biçimini Özelleştirme
 Şimdi, geçerli tarihi bir hücreye ekleyelim ve özel bir şekilde görüntülenecek şekilde biçimlendirelim. Varsayılan tarih biçimi yerine, aşağıdaki gibi özel bir biçim belirleyeceğiz:`d-mmm-yy`.
```csharp
// "A1" hücresine geçerli sistem tarihini ekleme
worksheet.Cells["A1"].PutValue(DateTime.Now);
// A1 hücresinin stilini elde etmek
Style style = worksheet.Cells["A1"].GetStyle();
// Özel görüntüleme biçimini tarihi "g-aaa-yy" olarak gösterecek şekilde ayarlama
style.Custom = "d-mmm-yy";
// Stili A1 hücresine uygulama
worksheet.Cells["A1"].SetStyle(style);
```
-  Hücreye geçerli sistem tarihini ekliyoruz`A1` kullanarak`PutValue(DateTime.Now)`.
-  Hücrenin geçerli stilini alıyoruz`A1` kullanarak`GetStyle()`.
-  Hücrenin stilini ayarlayarak değiştiriyoruz`style.Custom = "d-mmm-yy"`, tarihi gün, kısaltılmış ay ve yılı gösterecek şekilde biçimlendirir.
-  Son olarak yeni stili hücreye şu şekilde uygularız:`SetStyle()`.
## Adım 4: Bir Hücreyi Yüzde Olarak Biçimlendirme
 Şimdi sayılarla çalışalım. Başka bir hücreye sayısal bir değer ekleyelim, diyelim ki`A2`ve yüzde olarak biçimlendirin.
```csharp
//"A2" hücresine sayısal bir değer ekleme
worksheet.Cells["A2"].PutValue(20);
// A2 hücresinin stilini elde etmek
style = worksheet.Cells["A2"].GetStyle();
// Değeri yüzde olarak göstermek için özel görüntüleme biçimini ayarlama
style.Custom = "0.0%";
// Stilin A2 hücresine uygulanması
worksheet.Cells["A2"].SetStyle(style);
```
-  Değer katıyoruz`20` hücreye`A2`.
-  Hücre stilini alıyoruz`A2` ve özel formatı şu şekilde ayarlayın`0.0%` değeri yüzde olarak (yani %20) görüntülemek için.
-  Son olarak, stili hücreye şu şekilde uygularız:`SetStyle()`.
## Adım 5: Hücreyi Para Birimi Olarak Biçimlendirme
 Hücreye başka bir değer ekleyelim`A3`ve para birimi olarak görüntülenecek şekilde biçimlendirin. İşleri daha ilginç hale getirmek için, pozitif değerleri pound cinsinden ve negatif değerleri dolar cinsinden para birimi olarak görüntüleyen bir biçim kullanacağız.
```csharp
// "A3" hücresine sayısal bir değer ekleme
worksheet.Cells["A3"].PutValue(2546);
// A3 hücresinin stilini elde etmek
style = worksheet.Cells["A3"].GetStyle();
// Değeri para birimi olarak göstermek için özel görüntüleme biçimini ayarlama
style.Custom = "£#,##0;[Red]$-#,##0";
// Stilin A3 hücresine uygulanması
worksheet.Cells["A3"].SetStyle(style);
```
-  Değer katıyoruz`2546` hücreye`A3`.
-  Özel bir format belirledik`£#,##0;[Red]$-#,##0`Pozitif değerleri pound işaretiyle, negatif değerleri ise dolar işaretiyle kırmızıyla gösteren .
- Stili hücreye şu şekilde uygularız:`SetStyle()`.
## Adım 6: Çalışma Kitabını Kaydetme
Son adım çalışma kitabını bir Excel dosyası olarak kaydetmektir. Bu eğitim için Excel 97-2003 biçimini kullanacağız.
```csharp
// Excel dosyasını kaydetme
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
-  The`Save()` method çalışma kitabını belirtilen dizine kaydeder.
-  Biz seçiyoruz`SaveFormat.Excel97To2003` Excel'in eski sürümleriyle uyumluluğu sağlamak için.
## Çözüm
İşte bu kadar! Az önce bir Excel dosyası oluşturduk, Aspose.Cells for .NET kullanarak belirli hücrelere özel tarih, yüzde ve para birimi biçimleri ekledik ve dosyayı kaydettik. Özel biçimlendirme, Excel dosyalarınızı çok daha okunabilir ve profesyonel hale getirir. Verilerinizin nasıl göründüğü konusunda daha fazla kontrol sahibi olmak için Aspose.Cells'deki koşullu biçimlendirme gibi diğer biçimlendirme seçeneklerini keşfetmeyi unutmayın.
## SSS
### Aspose.Cells'te daha karmaşık biçimlendirme seçeneklerini nasıl uygulayabilirim?
Yazı tipi rengi, kenarlıklar ve arka plan renkleri gibi farklı biçimlendirme stillerini özel sayı biçimleriyle birleştirebilirsiniz.
### Bir hücre aralığına özel sayı biçimi uygulayabilir miyim?
Evet, Aspose.Cells, bir hücre aralığına bir stil uygulamanıza olanak tanır.`Range.SetStyle()` yöntem.
### Çalışma kitabını hangi diğer dosya biçimlerinde kaydedebilirim?
 Aspose.Cells, XLSX, CSV ve PDF dahil olmak üzere birçok formatı destekler. Basitçe`SaveFormat` içinde`Save()` yöntem.
### Negatif sayıları farklı şekilde biçimlendirebilir miyim?
Kesinlikle! Negatif sayıları farklı renkler veya sembollerle görüntülemek için özel sayı biçimlerini kullanabilirsiniz.
### Aspose.Cells for .NET ücretsiz mi?
 Aspose.Cells ücretsiz deneme sunuyor, ancak tam işlevsellik için geçerli bir lisansa ihtiyacınız olacak. Bir tane alabilirsiniz[burada geçici lisans](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
