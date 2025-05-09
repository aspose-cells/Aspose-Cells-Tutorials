---
"description": "Bu kolay takip edilebilir eğitimde, Aspose.Cells for .NET kullanarak özel DB Num biçimlendirmesiyle verileri Excel'e nasıl aktaracağınızı öğrenin."
"linktitle": "Özel DB Num Desen Biçimlendirmesi ile Verileri Excel'e Aktarın"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": "Özel DB Num Desen Biçimlendirmesi ile Verileri Excel'e Aktarın"
"url": "/tr/net/excel-data-import-export/import-data-to-worksheet-in-excel-with-specified-db-num-custom-pattern-formatting/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Özel DB Num Desen Biçimlendirmesi ile Verileri Excel'e Aktarın

## giriiş

E-tablo düzenleme söz konusu olduğunda, verileri Excel'e aktarmak ve doğru şekilde biçimlendirmek, özellikle DB Num desenleri gibi belirli kültür tabanlı biçimleri kullanmak istediğinizde, bunaltıcı bir görev gibi gelebilir. Excel biçimlendirmesinin teknik ayrıntılarıyla boğuştuğunuzu hissettiyseniz, doğru yerdesiniz! Bu kılavuzda, .NET için Aspose.Cells'i kullanarak işleri basit adımlara böleceğiz ve veri içe aktarımlarınızı yalnızca basit değil, aynı zamanda estetik açıdan da hoş hale getireceğiz. O halde sıkı tutunun çünkü .NET programlama, biçimlendirme ve Excel dosyalarını kolayca dışa aktarma dünyasına dalıyoruz!

## Ön koşullar

Ayrıntılara girmeden önce, ihtiyacınız olan her şeye sahip olduğunuzdan emin olalım. İşte sizi başarıya hazırlayacak ön koşulların hızlı bir kontrol listesi:

1. .NET Framework: Makinenizde .NET Framework'ün yüklü olduğundan emin olun. Aspose.Cells çeşitli .NET sürümleriyle sorunsuz bir şekilde çalışır.
2. .NET için Aspose.Cells: Aspose.Cells kütüphanesini indirip yüklemeniz gerekecek. Bunu şuradan alabilirsiniz: [indirme bağlantısı](https://releases.aspose.com/cells/net/).
3. Entegre Geliştirme Ortamı (IDE): C# kodunuzu yazıp çalıştırabileceğiniz Visual Studio gibi bir IDE kullanın.
4. Temel C# Bilgisi: C# hakkında temel bir anlayışa sahip olmak, bu kılavuzda kullanacağımız kodlama uygulamalarını takip etmenize yardımcı olacaktır.

Her şeyi aldınız mı? Harika! Gerekli paketleri içe aktarmaya geçelim.

## Paketleri İçe Aktar

Aspose.Cells ile etkili bir şekilde çalışmak için, C# dosyanızın başına gerekli ad alanlarını içe aktarmanız gerekir. Bunu adım adım açıklayalım.

### C# Dosyanızı Oluşturun

IDE'nizi açın (Visual Studio önerilir) ve yeni bir C# projesi oluşturun. Buna şu şekilde alakalı bir isim verin: `ExcelDataImport`.

### Referans Aspose.Cells

Projenize Aspose.Cells kütüphanesini dahil etmelisiniz. Solution Explorer'da projenize sağ tıklayın ve 'Referans Ekle'yi seçin. Aspose.Cells'i yüklediğiniz yere gidin ve seçin.

### Gerekli Ad Alanlarını İçe Aktar

C# dosyanızın en üstüne aşağıdaki ad alanlarını içe aktarın:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Bu basit satır, Aspose.Cells'in sunduğu tüm işlevselliğe açılan kapınızdır. 

Artık tüm ön koşulları karşıladığımıza ve gerekli paketleri içe aktardığımıza göre, verileri Excel'e içe aktarma ve özel DB Num desen biçimlendirmesini uygulama adım adım sürecine dalalım. Netlik ve anlayışı garantilemek için bunu metodik olarak ele alacağız.

## Adım 1: Veri Dizinini Ayarlayın

İlk olarak, çıktının kaydedileceği belgeler dizininize giden yolu belirtmeniz gerekir. Bunu dosya yapınıza göre ayarlayın.

```csharp
string dataDir = "Your Document Directory";
```

Bu örnekte şunu değiştirin: `Your Document Directory` gerçek yolunuzla, örneğin `C:\\Users\\YourName\\Documents\\`.

## Adım 2: Bir Çalışma Kitabı Oluşturun

Daha sonra, esasen Excel dosyanız olan yeni bir çalışma kitabı oluşturacaksınız.

```csharp
Workbook wb = new Workbook();
```

Burada yeni bir örnek oluşturuyoruz `Workbook` nesne. Bu sizin boş tuvaliniz!

## Adım 3: İlk Çalışma Sayfasına Erişim

Her çalışma kitabı birden fazla çalışma sayfası içerir. Veri girmeye başlamak için ilk çalışma sayfasına erişmek isteyeceksiniz.

```csharp
Worksheet ws = wb.Worksheets[0];
```

Tıpkı bir kitabın ilk sayfasını açtığınız gibi, verilerinizi eklemek için ilk çalışma sayfasına erişiyorsunuz.

## Adım 4: Hücreye Veri Girin

Şimdi, bir hücreyi biraz veriyle dolduralım. Bu örnek için, değeri gireceğiz `123` A1 hücresine.

```csharp
Cell cell = ws.Cells["A1"];
cell.PutValue(123);
```

Burada doğrudan Excel ile konuşuyorsunuz; verileri doğrudan A1 hücresine koyuyorsunuz! 

## Adım 5: Hücre Stiline Erişim

Her hücrenin bir stili vardır ve nasıl görüneceğini özelleştirebilirsiniz. Özel bir biçim uygulamak için, önce hücrenin stiline erişmeniz gerekir.

```csharp
Style st = cell.GetStyle();
```

Hücrenin stilini yakalayarak, ona kendi özgün dokunuşunuzu katmaya hazırlanıyorsunuz!

## Adım 6: DBNum Özel Desen Biçimlendirmesini Belirleyin

İşte sihir burada gerçekleşir. DBNum biçimlendirme stilini kullanarak özel bir biçim deseni belirtebilirsiniz.

```csharp
st.Custom = "[DBNum2][$-804]General";
```

Bu satır Excel'e sayıyı biçimlendirmesini söyler `123` Çince diline karşılık gelen DBNum desenine göre. Oldukça hoş, değil mi?

## Adım 7: Güncellenen Hücre Stilini Ayarlayın

Artık özel stilinizi tanımladığınıza göre, onu hücreye uygulamanın zamanı geldi.

```csharp
cell.SetStyle(st);
```

Bu, hücrenizi şık bir kıyafetle giydirmek gibi bir şey!

## Adım 8: Sütun Genişliğini Ayarlayın

Her şeyin güzel ve düzenli göründüğünden emin olalım. Verilerinize daha iyi uyması için ilk sütunun genişliğini ayarlayabilirsiniz.

```csharp
ws.Cells.SetColumnWidth(0, 30);
```

Burada, sütun genişliğini genişletiyoruz, böylece verileriniz sıkışık hissettirmiyor. Bunu, verilerinize nefes alacak alan vermek gibi düşünün!

## Adım 9: Çalışma Kitabını Kaydedin

Son olarak bu şaheseri PDF formatına kaydedelim. İşte muhteşem final!

```csharp
wb.Save(dataDir + "outputDBNumCustomFormatting.pdf", SaveFormat.Pdf);
```

Tebrikler! DB Num stilleri ile biçimlendirilmiş numaranızı gösteren bir PDF dosyası oluşturdunuz.

## Çözüm

Ve işte oldu! Verileri Excel'e başarıyla aktardınız, özel DB Num biçimlendirmesini uyguladınız ve PDF biçiminde kaydettiniz. .NET için Aspose.Cells ile bu süreç yalnızca daha kolay olmakla kalmıyor, aynı zamanda çok daha esnek ve güçlü hale geliyor. Excel'in yerleşik biçimlendirme seçenekleriyle uğraşmanıza gerek yok; artık kod üzerinden doğrudan bir kontrol hattınız var!

İster veri raporları hazırlayın ister finansal tablolar oluşturun, Aspose.Cells'in gücünden yararlanmak, elektronik tablo oyununuzu yepyeni bir seviyeye taşıyacaktır. Öyleyse, daha ne bekliyorsunuz? Projelerinize güvenle dalın ve verilerinizin parlamasına izin verin!

## SSS

### Aspose.Cells Nedir?  
Aspose.Cells, geliştiricilerin Excel dosyalarını program aracılığıyla oluşturmalarına, düzenlemelerine ve dönüştürmelerine olanak tanıyan güçlü bir .NET kütüphanesidir.

### Diğer hücre türlerini biçimlendirebilir miyim?  
Evet! Çalışma sayfalarınızdaki herhangi bir hücreye farklı stiller, biçimler ve hatta formüller uygulayabilirsiniz.

### Ücretsiz deneme imkanı var mı?  
Kesinlikle! Ücretsiz deneme sürümünü kontrol edebilirsiniz [Burada](https://releases.aspose.com/).

### Excel dosyalarını hangi formatlarda kaydedebilirim?  
Aspose.Cells, XLSX, XLS, CSV, PDF ve daha birçok formatı destekler.

### Daha fazla desteği nereden bulabilirim?  
Yardıma ihtiyacınız varsa, onları ziyaret edin [destek forumu](https://forum.aspose.com/c/cells/9) Topluluktan ve uzmanlardan yardım isteyin.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}