---
"date": "2025-04-05"
"description": "Aspose.Cells for .NET kullanarak Excel sayfalarına filigran eklemeyi ve özelleştirmeyi öğrenin. Bu kılavuz kurulum, uygulama ve güvenlik özelliklerini kapsar."
"title": "Aspose.Cells .NET&#58; Kullanarak Excel'de Filigran Nasıl Eklenir Kapsamlı Bir Kılavuz"
"url": "/tr/net/headers-footers/excel-watermark-aspose-cells-net-tutorial/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Aspose.Cells .NET Kullanarak Excel'e Filigran Nasıl Eklenir

Günümüzün dijital dünyasında, elektronik tablolar gibi belgeleri paylaşırken hassas verilerinizi korumak hayati önem taşır. Filigran eklemek (incelikli ama güçlü bir görsel ipucu) gizliliği veya sahipliği gösterebilir. Bu kapsamlı kılavuz, Excel sayfalarında filigran metin efektleri eklemek ve özelleştirmek için Aspose.Cells for .NET'i kullanma konusunda size yol gösterir.

## Ne Öğreneceksiniz
- Geliştirme ortamınızda .NET için Aspose.Cells'i kurma.
- Excel dosyasına C# ile filigran ekleme.
- Filigranların görünümünü, renk ve şeffaflık ayarları dahil olmak üzere özelleştirme.
- Yetkisiz değişiklikleri önlemek için Excel içindeki şekilleri kilitleme.
- Belge güvenliğini artırmaya yönelik pratik uygulamalar.

Bu işlevleri projelerinize nasıl uygulayabileceğinizi inceleyelim.

## Ön koşullar
Başlamadan önce şunlara sahip olduğunuzdan emin olun:
- **Görsel Stüdyo** Bilgisayarınıza kurulu (2017 ve sonrası herhangi bir sürüm).
- C# ve .NET geliştirme konusunda temel bilgi.
- API'leri kullanarak Excel dosya yönetimine ilişkin genel bir anlayış.

Ek olarak, NuGet Paket Yöneticisi Konsolu veya .NET CLI aracılığıyla .NET için Aspose.Cells'i yükleyin:

**NuGet Paket Yöneticisi**
```bash
PM> Install-Package Aspose.Cells
```

**.NET Komut Satırı Arayüzü**
```bash
dotnet add package Aspose.Cells
```

### Lisans Edinimi
Aspose.Cells for .NET'i kullanmak için, yeteneklerini keşfetmek üzere ücretsiz deneme lisansıyla başlayabilirsiniz:
1. **Ücretsiz Deneme:** Ziyaret edin [Aspose geçici lisans sayfası](https://purchase.aspose.com/temporary-license/) ve geçici lisans talebinde bulunabilirsiniz.
2. **Satın almak:** Uzun vadeli kullanım için, şu adresten lisans satın alın: [Aspose Satın Alma Sayfası](https://purchase.aspose.com/buy).

### Temel Kurulum
Aspose.Cells'i NuGet veya CLI aracılığıyla edindikten sonra, onu C# projenizde başlatın:
```csharp
using Aspose.Cells;
```

## Aspose.Cells'i .NET için Kurma
Aspose.Cells'in kurulumu ve başlatılmasına ilişkin kısa bir genel bakış:
1. **Düzenlemek** Yukarıda gösterildiği gibi Paket Yöneticisi Konsolu veya .NET CLI'yi kullanarak Aspose.Cells.
2. **Başlat:** Bir tane oluşturarak başlayın `Workbook` Excel dosyasını temsil eden nesne.

```csharp
Workbook workbook = new Workbook();
```
3. **Lisans Başvurusu:** Lisansınız varsa, tüm özelliklerin kilidini açmak için bunu kullanın.

## Uygulama Kılavuzu

### Özellik 1: Excel Sayfasına Filigran Ekleme
#### Genel bakış
Filigran eklemek, verilerinizin üzerine gizlice yerleştirilen ve "GİZLİ" gibi belge durumunu belirten metin efektleri oluşturmayı içerir.

#### Adım Adım Uygulama
##### Bir Çalışma Kitabı ve Çalışma Sayfası Oluşturun
```csharp
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

##### Filigran Olarak Metin Efekti Ekle
Yazı tipi stili, boyutu, konumu ve görünümü gibi belirli niteliklerle metin efekti şeklini oluşturun.

```csharp
Shape wordart = sheet.Shapes.AddTextEffect(
    MsoPresetTextEffect.TextEffect1,
    "CONFIDENTIAL", 
    "Arial Black",
    50,   // Yazı tipi boyutu
    false, // italik mi
    true, // Cesur
    18,   // Sol pozisyon
    8,    // En üst pozisyon
    1,    // Genişlik
    1,    // Yükseklik
    130,  // Dönme açısı
    800   // Ölçek faktörü
);
```

##### Görünümü Özelleştir
Daha şık bir görünüm için degrade rengini ve şeffaflığı ayarlayın.
```csharp
FillFormat wordArtFormat = wordart.Fill;
wordArtFormat.SetOneColorGradient(Color.Red, 0.2, GradientStyleType.Horizontal, 2); 
wordArtFormat.Transparency = 0.9; // Biraz şeffaf hale getirin

wordart.HasLine = false; // Daha temiz bir görünüm için sınır çizgisini kaldırın
```

##### Çalışma Kitabınızı Kaydedin
```csharp
workbook.Save("YOUR_OUTPUT_DIRECTORY\output_out.xlsx");
```

### Özellik 2: Excel Sayfasında Şekil Görünümlerini Kilitle
#### Genel bakış
Şekillerin kilitlenmesi, yetkisiz kullanıcıların filigranı veya diğer şekilleri değiştirmesini önleyerek belge bütünlüğünü korur.

#### Adım Adım Uygulama
##### Filigranın Çeşitli Özelliklerini Kilitle
Filigranınızı yönlerini kilitleyerek güvence altına alın.
```csharp
wordart.IsLocked = true;
wordart.SetLockedProperty(ShapeLockType.Selection, true);
wordart.SetLockedProperty(ShapeLockType.ShapeType, true);
wordart.SetLockedProperty(ShapeLockType.Move, true);
wordart.SetLockedProperty(ShapeLockType.Resize, true);
wordart.SetLockedProperty(ShapeLockType.Text, true);
```

##### Değişiklikleri Kaydet
Değişikliklerin çalışma kitabınıza kaydedildiğinden emin olun.
```csharp
workbook.Save("YOUR_OUTPUT_DIRECTORY\output_out.xlsx");
```

## Pratik Uygulamalar
1. **Gizli Raporlar:** Hassas bilgiler içeren dahili raporlarda filigran kullanın.
2. **Telif Hakkı Bildirimleri:** Müşterilere dağıtılan şablonlara telif hakkı bildirimlerini yerleştirin.
3. **Sürüm Kontrolü:** Belgelerin taslak veya son halini ilgili filigran metniyle belirtin.

## Performans Hususları
- **Kaynakları Optimize Edin:** Yalnızca gerekli çalışma sayfalarını ve şekilleri yükleyerek kaynak kullanımını en aza indirin.
- **Bellek Yönetimi:** Nesneleri uygun şekilde kullanarak atın `Dispose()` Uygulanabilir olduğu durumlarda, .NET uygulamalarında verimli bellek yönetiminin sağlanması için yöntemler.

## Çözüm
Excel sayfalarında filigran eklemek ve şekilleri kilitlemek için Aspose.Cells for .NET'i kullanmada ustalaşarak, belge güvenliğini artırabilir ve kritik bilgileri tek bakışta iletebilirsiniz. Bu kılavuz, bu özellikleri etkili bir şekilde uygulamak için gerekli becerileri size kazandırdı.

### Sonraki Adımlar
Daha fazla özelleştirme seçeneğini keşfedin [Aspose.Cells belgeleri](https://reference.aspose.com/cells/net/) veya bu işlevleri, güçlü belge yönetimi gerektiren daha büyük sistemlere entegre etmeyi deneyin.

## SSS Bölümü
1. **Filigran metnini nasıl değiştirebilirim?**
   - İkinci parametreyi değiştirin `AddTextEffect()` İstediğiniz metinle yöntemi kullanın.
2. **Filigranımda farklı yazı tipleri kullanabilir miyim?**
   - Evet, üçüncü parametreyi değiştirerek herhangi bir yazı tipini belirtin `AddTextEffect()`.
3. **Excel dosyam büyükse ve yüklemesi yavaşsa ne yapmalıyım?**
   - Kodunuzu yalnızca çalışma kitabının gerekli kısımlarını yükleyecek şekilde optimize etmeyi veya Aspose.Cells'te bulunan performans ayarlama seçeneklerini kullanmayı düşünün.
4. **Filigranı sonradan kaldırmak mümkün müdür?**
   - Evet, şekilleri bulundukları çalışma sayfası koleksiyonundan silebilirsiniz.
5. **Bu çözümü toplu işlemede nasıl uygularım?**
   - Verimlilik için benzer mantığı döngüler veya eşzamansız görevler içerisinde uygulayarak birden fazla çalışma kitabı üzerinde yineleme yapın.

## Kaynaklar
- [Aspose.Cells Belgeleri](https://reference.aspose.com/cells/net/)
- [Aspose.Cells'i indirin](https://releases.aspose.com/cells/net/)
- [Lisans Satın Alın](https://purchase.aspose.com/buy)
- [Ücretsiz Deneme Alın](https://releases.aspose.com/cells/net/)
- [Geçici Lisans Talebinde Bulunun](https://purchase.aspose.com/temporary-license/)
- [Aspose Destek Forumu](https://forum.aspose.com/c/cells/9)

Artık bilgi sahibi olduğunuza göre, bu teknikleri pratiğe dökmenin ve Excel belgelerinizi etkili bir şekilde güvence altına almanın zamanı geldi!


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}