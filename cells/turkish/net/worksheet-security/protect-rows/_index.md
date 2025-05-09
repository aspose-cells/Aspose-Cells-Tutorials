---
"description": "Aspose.Cells for .NET kullanarak bir Excel çalışma sayfasındaki satırları nasıl koruyacağınızı öğrenin. Verilerinizi satır düzeyinde korumayla güvence altına alın ve yanlışlıkla yapılan değişiklikleri önleyin."
"linktitle": "Aspose.Cells kullanarak Çalışma Sayfasındaki Satırları Koruyun"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": "Aspose.Cells kullanarak Çalışma Sayfasındaki Satırları Koruyun"
"url": "/tr/net/worksheet-security/protect-rows/"
"weight": 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells kullanarak Çalışma Sayfasındaki Satırları Koruyun

## giriiş
Excel dosyalarıyla programatik olarak çalışmak genellikle yalnızca veri manipülasyonu değil aynı zamanda veri koruması da gerektiren bir görevdir. Hassas verileri korumanız veya yanlışlıkla düzenlemeyi önlemeniz gerekip gerekmediğine bakılmaksızın, bir çalışma sayfasındaki satırları korumak önemli bir adım olabilir. Bu eğitimde, .NET için Aspose.Cells kullanarak bir Excel çalışma sayfasındaki belirli satırları nasıl koruyacağımızı ele alacağız. Ortamınızı hazırlamaktan koruma özelliklerini basit ve takip etmesi kolay bir şekilde uygulamaya kadar gerekli tüm adımları ele alacağız.
## Ön koşullar
Bir çalışma sayfasındaki satırları korumaya başlamadan önce, yerinde olması gereken birkaç şey vardır:
1. Aspose.Cells for .NET: Geliştirme makinenizde Aspose.Cells for .NET'in yüklü olduğundan emin olun. Bunu henüz yapmadıysanız, şuradan kolayca indirebilirsiniz: [Aspose Hücreleri indirme sayfası](https://releases.aspose.com/cells/net/).
2. Visual Studio veya Herhangi Bir .NET IDE: Çözümü uygulamak için bir geliştirme ortamı kurmanız gerekir. Visual Studio harika bir seçenektir, ancak herhangi bir .NET uyumlu IDE işe yarayacaktır.
3. Temel C# Bilgisi: C# programlamanın temellerini anlamak, eğitimi takip etmenize ve örnek kodu ihtiyaçlarınıza uyacak şekilde değiştirmenize yardımcı olacaktır.
4. Aspose.Cells API Belgeleri: Aşağıdakilerle tanışın: [Aspose.Cells for .NET belgeleri](https://reference.aspose.com/cells/net/) Kütüphanede kullanılan sınıf yapısı ve yöntemler hakkında genel bir bakış elde etmek için.
Eğer ön koşullar tamamlanmışsa, hemen uygulamaya geçebiliriz.
## Paketleri İçe Aktar
Başlamak için gerekli paketleri içe aktarmanız gerekir. Bu kütüphaneler, C# projenizdeki Excel dosyalarıyla etkileşim kurmak için çok önemlidir.
```csharp
using System.IO;
using Aspose.Cells;
```
Gerekli paketleri içe aktardıktan sonra kodlamaya başlayabilirsiniz. 
Şimdi, süreci sizin için takip etmesi çok kolay olacak şekilde daha küçük adımlara bölelim. Her adım, uygulamanın belirli bir kısmına odaklanacak ve bunu hızlı bir şekilde anlayıp uygulayabilmenizi sağlayacaktır. 
## Adım 1: Yeni bir Çalışma Kitabı ve Çalışma Sayfası Oluşturun
Herhangi bir koruma ayarını uygulayabilmeniz için yeni bir çalışma kitabı oluşturmanız ve üzerinde çalışmak istediğiniz çalışma sayfasını seçmeniz gerekir. Bu sizin çalışma belgeniz olacaktır.
```csharp
// Belgeler dizinine giden yol.
string dataDir = "Your Document Directory";
// Eğer mevcut değilse dizin oluşturun.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Yeni bir çalışma kitabı oluşturun.
Workbook wb = new Workbook();
// Bir çalışma sayfası nesnesi oluşturun ve ilk sayfayı elde edin.
Worksheet sheet = wb.Worksheets[0];
```
Bu örnekte, tek bir çalışma sayfasıyla yeni bir çalışma kitabı oluşturuyoruz (bu, Aspose.Cells kullanarak yeni bir çalışma kitabı oluşturduğunuzda varsayılan kurulumdur). Daha sonra, satır korumamızın hedefi olacak olan çalışma kitabındaki ilk çalışma sayfasını alıyoruz.
## Adım 2: Style ve StyleFlag Nesnelerini Tanımlayın
Bir sonraki adım stil ve stil bayrağı nesnelerini tanımlamaktır. Bu nesneler hücrenin özelliklerini, örneğin kilitli mi yoksa kilidi açılmış mı olduğunu değiştirmenize olanak tanır.
```csharp
// Stil nesnesini tanımlayın.
Style style;
// Styleflag nesnesini tanımlayın.
StyleFlag flag;
```
Bu nesneleri daha sonraki adımlarda hücre özelliklerini özelleştirmek ve çalışma sayfanıza uygulamak için kullanacaksınız.
## Adım 3: Çalışma Sayfasındaki Tüm Sütunların Kilidini Açın
Varsayılan olarak, bir Excel çalışma sayfasındaki tüm hücreler kilitlidir. Ancak, bir çalışma sayfasını koruduğunuzda, kilitli durumu zorunlu hale getirilir. Yalnızca belirli satırların veya hücrelerin korunduğundan emin olmak için önce tüm sütunların kilidini açabilirsiniz. Yalnızca belirli satırları korumak istiyorsanız bu adım önemlidir.
```csharp
// Çalışma sayfasındaki tüm sütunları dolaşın ve kilidini açın.
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    flag = new StyleFlag();
    flag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, flag);
}
```
Bu kodda, çalışma sayfasındaki 256 sütunun tamamında döngü oluşturuyoruz (Excel çalışma sayfalarında 0'dan 255'e kadar indekslenen maksimum 256 sütun bulunur) ve bunları ayarlıyoruz. `IsLocked` mülk `false`Bu eylem tüm sütunların kilidinin açılmasını sağlar, ancak daha sonra belirli satırları yine de kilitleyeceğiz.
## Adım 4: İlk Satırı Kilitleyin
Sütunların kilidini açtıktan sonraki adım, korumak istediğiniz belirli satırları kilitlemektir. Bu örnekte, ilk satırı kilitleyeceğiz. Bu, diğer satırlar kilitsiz bırakılırken kullanıcıların bunu değiştirememesini sağlar.
```csharp
// İlk sıra stilini al.
style = sheet.Cells.Rows[0].Style;
// Kilitle onu.
style.IsLocked = true;
// Bayrağı örneklendir.
flag = new StyleFlag();
// Kilit ayarını yapın.
flag.Locked = true;
// Stili ilk satıra uygulayın.
sheet.Cells.ApplyRowStyle(0, style, flag);
```
Burada ilk satırın stiline erişiyoruz ve onu ayarlıyoruz `IsLocked` mülk `true`. Bundan sonra şunu kullanırız: `ApplyRowStyle()` Kilit stilini tüm satıra uygulamak için yöntem. Korumak istediğiniz diğer satırları kilitlemek için bu adımı tekrarlayabilirsiniz.
## Adım 5: Sayfayı Koruyun
Artık gerekli satırları kilitleyip açtığımıza göre, çalışma sayfasını koruma zamanı geldi. Koruma, koruma parolasını (sağlanmışsa) kaldırmadıkları sürece hiç kimsenin kilitli satırları veya hücreleri değiştiremeyeceğini garanti eder.
```csharp
// Sayfayı koruyun.
sheet.Protect(ProtectionType.All);
```
Bu adımda, tüm sayfaya koruma uygularız `ProtectionType.All`Bu tür koruma, kilitli satırlar ve hücreler dahil olmak üzere sayfanın tüm yönlerinin korunduğu anlamına gelir. Ayrıca, gerekirse farklı koruma türleri belirterek bu korumayı özelleştirebilirsiniz.
## Adım 6: Çalışma Kitabını Kaydedin
Son olarak, gerekli stilleri ve korumayı uyguladıktan sonra çalışma kitabını kaydetmemiz gerekir. Çalışma kitabı Excel 97-2003, Excel 2010 vb. gibi çeşitli biçimlerde kaydedilebilir.
```csharp
// Excel dosyasını kaydedin.
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
Bu kod satırı, çalışma kitabını uygulanan değişikliklerle Excel 97-2003 biçiminde kaydeder. Çeşitli seçenekler arasından seçim yaparak dosya biçimini ihtiyaçlarınıza göre değiştirebilirsiniz. `SaveFormat` seçenekler.
## Çözüm
İşte oldu! Aspose.Cells for .NET kullanarak bir çalışma sayfasındaki satırları nasıl koruyacağınızı başarıyla öğrendiniz. Yukarıdaki adımları izleyerek, istediğiniz satır veya sütunun kilidini açabilir veya kilitleyebilir ve verilerinizin bütünlüğünü sağlamak için koruma uygulayabilirsiniz.
## SSS
### Birden fazla satırı aynı anda nasıl koruyabilirim?  
Birden fazla satır arasında geçiş yapabilir ve kilitleme stilini her birine ayrı ayrı uygulayabilirsiniz. Basitçe değiştirin `0` kilitlemek istediğiniz satır indeksi ile.
### Sayfa koruması için şifre belirleyebilir miyim?  
Evet! Bir şifreyi şuraya geçirebilirsiniz: `sheet.Protect()` Şifre korumasını zorunlu kılma yöntemi.
### Tüm sütunlar yerine hücrelerin kilidini açabilir miyim?  
Evet! Sütunların kilidini açmak yerine, stil özelliklerini değiştirerek tek tek hücrelerin kilidini açabilirsiniz.
### Korunan bir satırı düzenlemeye çalışırsam ne olur?  
Bir satır korunduğunda, sayfanın korumasını kaldırmadığınız sürece Excel kilitli hücrelerde herhangi bir düzenleme yapılmasını engeller.
### Belirli aralıkları bir satırda koruyabilir miyim?  
Evet! Tek tek aralıkları bir satırda, şunu ayarlayarak kilitleyebilirsiniz: `IsLocked` Aralıktaki belirli hücrelere ait özellik.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}