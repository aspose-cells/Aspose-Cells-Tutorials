---
"description": "Aspose.Cells for .NET kullanarak Excel çalışma sayfalarında düzenlenebilir aralıklar oluşturmayı öğrenin; böylece belirli hücrelerin düzenlenebilir olmasına izin verirken geri kalanını çalışma sayfası korumasıyla güvence altına alın."
"linktitle": "Kullanıcıların Aspose.Cells kullanarak Çalışma Sayfasındaki Aralıkları Düzenlemesine İzin Ver"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": "Kullanıcıların Aspose.Cells kullanarak Çalışma Sayfasındaki Aralıkları Düzenlemesine İzin Ver"
"url": "/tr/net/worksheet-security/allow-edit-ranges/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Kullanıcıların Aspose.Cells kullanarak Çalışma Sayfasındaki Aralıkları Düzenlemesine İzin Ver

## giriiş
Excel belgeleri genellikle istenmeyen düzenlemelerden korumak istediğiniz hassas veriler veya yapılandırılmış içerikler içerir. Ancak, belirli kullanıcılar için düzenlenebilir hale getirmek istediğiniz belirli hücreler veya aralıklar olabilir. İşte tam bu noktada, .NET için Aspose.Cells, belirlenmiş aralıklara düzenleme izinleri verirken tüm bir çalışma sayfasını korumanıza olanak tanıyan güçlü bir araç olarak devreye girer. Yalnızca belirli hücrelerin düzenlenebilir olduğu ve diğerlerinin güvenli kaldığı bir bütçe elektronik tablosunu paylaştığınızı düşünün; Aspose.Cells bunu kolay ve verimli hale getirir.
## Ön koşullar
Kodlama kısmına geçmeden önce ihtiyacınız olan her şeye sahip olduğunuzdan emin olalım:
- Aspose.Cells for .NET: Aspose.Cells for .NET kitaplığını yüklediğinizden emin olun. İndirebilirsiniz [Burada](https://releases.aspose.com/cells/net/).
- Geliştirme Ortamı: Visual Studio veya herhangi bir C# uyumlu IDE.
- .NET Framework: Sürüm 4.0 veya üzeri.
- Lisans: Deneme sınırlamalarından kaçınmak için bir lisans almayı düşünün. Bir lisans alabilirsiniz. [burada geçici lisans](https://purchase.aspose.com/temporary-license/).
## Paketleri İçe Aktar
Kodunuzun başına gerekli Aspose.Cells ad alanını eklediğinizden emin olun:
```csharp
using System.IO;
using Aspose.Cells;
```
Bu, Excel dosyalarında korumalı aralıkları ayarlamak için gereken tüm sınıflara ve yöntemlere erişebilmenizi sağlayacaktır.
Artık temeller hazır olduğuna göre, kodu adım adım ayrıntılı olarak inceleyelim.
## Adım 1: Dizini Ayarlayın
Dosyalarla çalışmaya başlamadan önce, Excel dosyasını kaydedeceğiniz dizini ayarlamanız gerekir. Bu, dosyalarınızın iyi organize edilmesini ve güvenli bir şekilde saklanmasını sağlar.
```csharp
// Belgelerinizin dizinine giden yolu tanımlayın
string dataDir = "Your Document Directory";
// Dizinin var olup olmadığını kontrol edin, yoksa oluşturun
bool isExists = Directory.Exists(dataDir);
if (!isExists)
{
    Directory.CreateDirectory(dataDir);
}
```
Kodun bu kısmı dizininizin dosya işlemleri için hazır olduğundan emin olur. Bunu, takip eden her şeyin temelini atmak olarak düşünün.
## Adım 2: Çalışma Kitabını ve Çalışma Sayfasını Başlatın
Şimdi yeni bir çalışma kitabı oluşturup, onun varsayılan çalışma sayfasına erişerek ilerleyelim.
```csharp
// Yeni bir Çalışma Kitabı Başlat
Workbook book = new Workbook();
// Çalışma kitabındaki ilk çalışma sayfasına erişin
Worksheet sheet = book.Worksheets[0];
```
Burada, bir Excel çalışma kitabını başlatıyoruz ve içindeki ilk çalışma sayfasını seçiyoruz. Bu çalışma sayfası, koruma ayarlarımızı uygulayacağımız ve düzenlenebilir aralıkları tanımlayacağımız tuval olacak.
## Adım 3: Düzenleme Aralıklarına İzin Ver Koleksiyonuna erişin
Aspose.Cells adlı bir özelliğe sahiptir `AllowEditRanges`, çalışma sayfası korunduğunda bile düzenlenebilen aralıkların bir koleksiyonudur.
```csharp
// Düzenleme Aralıklarına İzin Ver koleksiyonuna erişin
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```
Bu satır, düzenlenebilir özel bir aralık koleksiyonuna erişim ayarlar. Bunu, çalışma sayfanızda yalnızca belirli aralıkların korumayı aşmasına izin verilen bir "VIP" alanı olarak düşünün.
## Adım 4: Korunan Bir Aralık Tanımlayın ve Oluşturun
Şimdi çalışma sayfamızda korumalı bir aralık tanımlayıp oluşturalım. Bu aralık için başlangıç ve bitiş hücrelerini belirteceğiz.
```csharp
// Bir ProtectedRange değişkeni tanımlayın
ProtectedRange protectedRange;
// Koleksiyona belirli bir ad ve hücre konumları ile yeni bir aralık ekleyin
int idx = allowRanges.Add("EditableRange", 1, 1, 3, 3);
protectedRange = allowRanges[idx];
```
Bu kod bloğunda:
- `EditableRange` Aralığa atanan isimdir.
- (1, 1, 3, 3) sayıları aralık koordinatlarını tanımlar, yani B2 hücresinden (satır 1, sütun 1) başlayıp D4 hücresine (satır 3, sütun 3) kadar gider.
## Adım 5: Korunan Aralık için bir Parola Ayarlayın
Ek güvenlik için, korunan aralık için bir parola ayarlayabilirsiniz. Bu adım, yalnızca yetkili kullanıcıların aralığı düzenleyebildiğinden emin olmak için ekstra bir koruma katmanı ekler.
```csharp
// Düzenlenebilir aralık için bir parola belirleyin
protectedRange.Password = "123";
```
Burada bir şifre ekledik (`"123"`) korunan aralığa. Bu parola gereksinimi, kimin değişiklik yapabileceği konusunda ekstra bir kontrol düzeyi sağlar.
## Adım 6: Çalışma Sayfasını Koruyun
Düzenlenebilir aralığımız belirlendikten sonraki adım tüm çalışma sayfasını korumaktır. Bu koruma ayarı, tanımlanmış aralığın dışındaki tüm hücrelerin kilitli ve düzenlenemez olmasını sağlayacaktır.
```csharp
// Çalışma sayfasına koruma uygulayın ve diğer tüm hücreleri düzenlenemez hale getirin
sheet.Protect(ProtectionType.All);
```
The `Protect` yöntem, düzenlenebilir olarak tanımladığımız aralıklar hariç tüm çalışma sayfasını kilitler. Bu adım esasen, gerektiğinde belirli hücrelere erişimle güvenli bir "salt okunur" ortam yaratır.
## Adım 7: Çalışma Kitabını Kaydedin
Son adım çalışma kitabını kaydetmektir, böylece ayarlarınız uygulanır ve saklanır.
```csharp
// Excel dosyasını belirtilen dizine kaydedin
book.Save(dataDir + "protectedrange.out.xls");
```
Bu adımda, çalışma kitabımızı 1. Adımda kurduğumuz dizine “protectedrange.out.xls” olarak kaydediyoruz. Artık yalnızca belirli aralıkların düzenlenebildiği, tamamen işlevsel ve güvenli bir Excel dosyanız var!
## Çözüm
.NET için Aspose.Cells, Excel dosyalarınızdaki koruma ve izinleri yönetmek için mükemmel bir yol sunar. Düzenlenebilir aralıklar oluşturarak, belirli alanların erişilebilir kalmasına izin verirken çalışma sayfalarınızı güvence altına alabilirsiniz. Bu işlevsellik, yalnızca birkaç hücrenin düzenleme için açık olması ve diğerlerinin kilitli kalması gereken işbirlikçi belgeler için özellikle yararlıdır.
## SSS
### Bir çalışma sayfasına birden fazla düzenlenebilir aralık ekleyebilir miyim?
Evet, yalnızca tekrarlayarak birden fazla aralık ekleyebilirsiniz. `allowRanges.Add()` Her yeni aralık için bir yöntem.
### Daha sonra korunan bir aralığı kaldırmak istersem ne olur?
Kullanın `allowRanges.RemoveAt()` Kaldırmak istediğiniz aralığın indeksini içeren yöntem.
### Her aralık için farklı şifre belirleyebilir miyim?
Kesinlikle. Her biri `ProtectedRange` kendine özgü bir şifreye sahip olabilir ve bu sayede ayrıntılı kontrol sahibi olabilirsiniz.
### Düzenlenebilir aralıklar olmadan çalışma sayfasını korursam ne olur?
Düzenlenebilir aralıklar tanımlamazsanız, korunduktan sonra tüm çalışma sayfası düzenlenemez hale gelir.
### Korunan aralık diğer kullanıcılar tarafından görülebiliyor mu?
Hayır, koruma dahilidir. Kullanıcılar yalnızca korunan alanı düzenlemeye çalıştıklarında bir parola girmeleri istenecektir.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}