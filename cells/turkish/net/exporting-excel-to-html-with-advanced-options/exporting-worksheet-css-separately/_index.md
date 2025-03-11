---
title: Çalışma Sayfası CSS'sini Çıktı HTML'de Ayrı Ayrı Dışa Aktarma
linktitle: Çalışma Sayfası CSS'sini Çıktı HTML'de Ayrı Ayrı Dışa Aktarma
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Bu kapsamlı adım adım eğitimde, Aspose.Cells for .NET kullanarak Excel çalışma sayfalarını ayrı CSS ile HTML'ye etkili bir şekilde nasıl aktaracağınızı öğrenin.
weight: 14
url: /tr/net/exporting-excel-to-html-with-advanced-options/exporting-worksheet-css-separately/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Çalışma Sayfası CSS'sini Çıktı HTML'de Ayrı Ayrı Dışa Aktarma

## giriiş
Bu kılavuzda, CSS'yi ayrı olarak dışa aktarmaya özel bir vurgu yaparak bir Excel çalışma sayfasını HTML'ye nasıl aktaracağınızı öğreneceksiniz. Bu yalnızca stillerinizin sürdürülebilirliğini iyileştirmekle kalmaz, aynı zamanda iş akışı verimliliğinizi de artırır. Şimdi, ön koşullara dalalım ve ellerimizi kirletelim!
## Ön koşullar
Koda geçmeden önce, bu eğitimi sorunsuz bir şekilde yürütmek için ihtiyacınız olanlar şunlardır:
1. Aspose.Cells for .NET Lisansı: Aspose.Cells'in özelliklerini tam olarak kullanmak için bir lisansa ihtiyacınız olacak.[en son sürümü indirin](https://releases.aspose.com/cells/net/)veya bir tane al[geçici lisans](https://purchase.aspose.com/temporary-license/) eğer sadece suyu test ediyorsan.
2. Geliştirme Ortamı: .NET projelerinizi sorunsuz bir şekilde çalıştırmak için Visual Studio'nun yüklü olması gerekir.
3. Temel C# Bilgisi: C# programlamada biraz temel bilgi sahibi olmak, kod parçacıklarını daha iyi anlamanıza yardımcı olacaktır.
4.  Referans Belgeleri: Kendinizi şu konularda bilgilendirin:[Aspose.Cells belgeleri](https://reference.aspose.com/cells/net/) ek özellikler ve yetenekler için.
Bu ön koşulları listeden çıkardıktan sonra, heyecan verici kısma geçmeye hazırız!
## Paketleri İçe Aktar
Başlamak için, ilgili ad alanlarını Aspose.Cells'den içe aktarmanız gerekir. Bunu nasıl kurabileceğiniz aşağıda açıklanmıştır:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Drawing;
```
Bu kurulum size çalışma kitapları oluşturmak, çalışma sayfalarını düzenlemek ve stilleri yönetmek için gerekli tüm araçları sağlayacaktır.

Bunu yönetilebilir parçalara bölelim, her adım sizi o canlı Excel çalışma sayfasını tüm CSS içeriğiyle birlikte doğrudan bir HTML dosyasına aktarma hedefinize biraz daha yaklaştıracak!
## Adım 1: Çıktı Dizinini Ayarlayın
Yapmanız gereken ilk şey, dışa aktarılan HTML dosyanızı nereye kaydetmek istediğinize karar vermektir. Bu çok önemlidir çünkü bunu yanlış yaparsanız, belgenizi her yerde aramak zorunda kalabilirsiniz!
```csharp
string outputDir = "Your Document Directory";
```
 Basitçe değiştirin`"Your Document Directory"` dosyanın kaydedilmesini istediğiniz yol ile. Örneğin:`string outputDir = @"C:\MyExports\";`.
## Adım 2: Bir Çalışma Kitabı Nesnesi Oluşturun
Sonra, yeni bir çalışma kitabı nesnesi oluşturmamız gerekiyor. Çalışma kitabını, tüm sihrin gerçekleştiği boş tuvaliniz olarak düşünün!
```csharp
Workbook wb = new Workbook();
```
 Bunu yaparak Workbook sınıfının yeni bir örneğini başlattık. Bu değişken`wb` artık tüm Excel çalışma sayfamızı tutacaktır.
## Adım 3: İlk Çalışma Sayfasına Erişim
Şimdi tuvalinize dalıp ilk çalışma kağıdını alma zamanı. Bu kısım basit, çünkü bu eğitim için yalnızca ilk kağıda ihtiyacımız var.
```csharp
Worksheet ws = wb.Worksheets[0];
```
Bu satır, çalışma kitabınızdaki ilk çalışma sayfasını düzenlemeye hazır hale getirir.
## Adım 4: Bir Hücrenin Değerini Değiştirin
Şimdi eğlenceli kısma geçelim—bir hücreye biraz veri koyalım! Herhangi bir hücreyi seçebilirsiniz, ancak bu örnek için "B5" hücresini kullanacağız.
```csharp
Cell cell = ws.Cells["B5"];
cell.PutValue("This is some text.");
```
Bu satırla, B5 hücresine "Bu bir metindir." metnini ekledik. Basit, değil mi? 
## Adım 5: Hücre Stilini Ayarlayın
Biraz gösteriş katalım! Metnimizi, yazı rengini kırmızıya değiştirerek biçimlendireceğiz. 
```csharp
Style st = cell.GetStyle();
st.Font.Color = Color.Red;
cell.SetStyle(st);
```
Bu adım, B5 hücresinin mevcut stilini alır, yazı tipi rengini kırmızıya değiştirir ve ardından yeni stili yeniden uygular. Artık hücreniz sadece başka bir düz metin kutusu değil!
## Adım 6: HTML Kaydetme Seçeneklerini Belirleyin
Bu aşamada HTML kaydetme seçeneklerini hazırlayacağız. Bu, CSS'nizin ayrı olarak dışa aktarılmasını sağlamak için önemlidir.
```csharp
HtmlSaveOptions opts = new HtmlSaveOptions();
opts.ExportWorksheetCSSSeparately = true;
```
 İle`ExportWorksheetCSSSeparately` seçeneği true olarak ayarlandığında, CSS stillerini doğrudan HTML dosyasına yerleştirmek yerine kütüphaneye bunları ayrı ayrı ele almasını söylüyorsunuz.
## Adım 7: Çalışma Kitabını HTML Olarak Kaydedin
Son olarak, tüm zor işi kaydetme zamanı! Bu satır çalışma kitabınızı belirtilen çıktı dizinine bir HTML dosyası olarak kaydeder.
```csharp
wb.Save(outputDir + "outputExportWorksheetCSSSeparately.html", opts);
```
Burada çıktı dosyamıza isim veriyoruz`outputExportWorksheetCSSSeparately.html`Ve işte başardınız!
## Adım 8: Uygulamayı Onaylayın
Her şeyin yolunda gittiğini bilmek için, bir onay mesajı çıktısı almak her zaman iyi bir uygulamadır.
```csharp
Console.WriteLine("ExportWorksheetCSSSeparatelyInOutputHTML executed successfully.");
```
Artık kodunuzu çalıştırabilirsiniz ve bu onay mesajını görüyorsanız tebrikler! Excel çalışma sayfanızı ayrı CSS ile başarıyla dışa aktardınız!
## Çözüm
Ve işte karşınızda—Aspose.Cells for .NET sayesinde, CSS'yi ayrı tutarken bir Excel çalışma sayfasını HTML'ye aktarmaya yönelik kendi kılavuzunuz. Bu, yalnızca stilinizi düzenli tutmakla kalmaz, aynı zamanda gelecekte değişiklik yapmanız gerektiğinde size daha fazla esneklik sağlar. 
## SSS
### Aspose.Cells Nedir?
Aspose.Cells, Microsoft Excel'e ihtiyaç duymadan Excel elektronik tabloları oluşturmanıza, değiştirmenize ve dönüştürmenize olanak tanıyan güçlü bir .NET kütüphanesidir.
### Aspose.Cells'in ücretsiz deneme sürümünü nasıl edinebilirim?
 Ücretsiz deneme sürümünü şuradan indirebilirsiniz:[Aspose.Cells sürüm sayfası](https://releases.aspose.com/).
### HTML çıktısını daha fazla özelleştirebilir miyim?
Evet, Aspose.Cells ihtiyaçlarınıza göre HTML çıktısını özelleştirmek için çeşitli seçenekler sunar.
### Aspose.Cells kullanarak diğer sayfa elemanlarını düzenlemek mümkün müdür?
Kesinlikle! Aspose.Cells, bir elektronik tablodaki grafikleri, görüntüleri ve diğer birçok öğeyi düzenlemenize olanak tanır.
### Ek kaynakları nerede bulabilirim?
 Şuna bir göz atın:[Aspose.Cells belgeleri](https://reference.aspose.com/cells/net/) Ayrıntılı kılavuzlar ve API referansları için.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
