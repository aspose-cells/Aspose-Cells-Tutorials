---
"description": "Aspose.Cells for .NET kullanarak Excel'deki dairesel referansları kolayca tespit edin. E-tablolarınızda doğru hesaplamalar sağlamak için adım adım kılavuzumuzu izleyin."
"linktitle": "Excel'de Programatik Olarak Dairesel Referans Algılama"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": "Excel'de Programatik Olarak Dairesel Referans Algılama"
"url": "/tr/net/excel-formulas-and-calculation-options/detecting-circular-reference/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Programatik Olarak Dairesel Referans Algılama

## giriiş
Excel dosyalarıyla çalışırken karşılaşabileceğiniz en sinir bozucu sorunlardan biri dairesel referanstır. Bu, bir formülün doğrudan veya dolaylı olarak kendi hücresine geri referans vermesiyle olur ve Excel'in hesaplama motorunu şaşırtabilecek bir döngü oluşturur. Ancak korkmayın! .NET için Aspose.Cells ile bu sinir bozucu dairesel referansları programatik olarak tespit edebilir, elektronik tablolarınızın işlevsel ve doğru kalmasını sağlayabilirsiniz. Bu kılavuzda, sizi adım adım bu süreçte yönlendireceğiz ve bunu çocuk oyuncağı haline getireceğiz.
## Ön koşullar
Dairesel referansları tespit etmenin inceliklerine dalmadan önce, başlamak için ihtiyacınız olan her şeye sahip olduğunuzdan emin olalım:
1. Visual Studio: Makinenizde Visual Studio'nun yüklü olduğundan emin olun. Bu sizin geliştirme ortamınız olacak.
2. .NET Framework: .NET Framework'ün uyumlu bir sürümünü (en azından .NET Framework 4.0) kullandığınızdan emin olun.
3. Aspose.Cells Kütüphanesi: Aspose.Cells kütüphanesine sahip olmanız gerekir. Bunu şuradan indirebilirsiniz: [Aspose web sitesi](https://releases.aspose.com/cells/net/).
4. Temel C# Bilgisi: Bu dilde kod yazacağımız için C# programlamaya aşina olmanız faydalı olacaktır.
5. Excel Dosyası: Test için dairesel referanslar içeren bir Excel dosyası hazırlayın. Basit bir tane oluşturabilir veya bir örnek indirebilirsiniz.
Artık ön koşullarımız hazır olduğuna göre, eğlenceli kısma geçebiliriz!
## Paketleri İçe Aktar
Kodlamaya başlamadan önce gerekli paketleri içe aktarmanız gerekir. İşte nasıl yapacağınız:
### Yeni Bir Proje Oluştur
- Visual Studio'yu açın ve yeni bir C# Konsol Uygulaması projesi oluşturun.
### Aspose.Cells Referansını Ekle
- Çözüm Gezgini’nde projenizin üzerine sağ tıklayın.
- "NuGet Paketlerini Yönet" seçeneğini seçin.
- “Aspose.Cells”i arayın ve en son sürümü yükleyin.
### Gerekli Ad Alanlarını İçe Aktar
En üstte `Program.cs` dosyaya gerekli ad alanlarını içe aktarın:
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Artık her şeyi ayarladığımıza göre, bir Excel dosyasında dairesel referansları tespit etmek için koda dalalım.
## Adım 1: Giriş Dizinini Tanımlayın
Öncelikle Excel dosyanızın bulunduğu dizini belirtmeniz gerekir. Excel dosyanızı buraya yükleyeceksiniz.
```csharp
// Giriş dizini
string sourceDir = "Your Document Directory";
```
Yer değiştirmek `"Your Document Directory"` Excel dosyanızın gerçek yolunu belirtin.
## Adım 2: Çalışma Kitabını LoadOptions ile yükleyin
Sonra Excel çalışma kitabınızı yükleyeceksiniz. Sihir burada başlıyor!
```csharp
LoadOptions loadOptions = new LoadOptions();
var objWB = new Aspose.Cells.Workbook(sourceDir + "Circular Formulas.xls", loadOptions);
```
Burada, yeni bir örnek oluşturuyoruz `LoadOptions` ve belirtilen yoldan çalışma kitabını yükleyin. Excel dosya adınızın eşleştiğinden emin olun!
## Adım 3: Yineleme Ayarlarını Etkinleştir
Dairesel referanslara izin vermek için çalışma kitabında yineleme ayarlarını etkinleştirmeniz gerekir.
```csharp
objWB.Settings.Iteration = true;
```
Bu, Aspose.Cells'e hesaplama sırasında dairesel referanslara izin vermesini söyler.
## Adım 4: Hesaplama Seçenekleri ve Dairesel Monitör Oluşturun
Şimdi hesaplama seçeneklerini ve özel dairesel monitörümüzü oluşturalım.
```csharp
CalculationOptions copts = new CalculationOptions();
CircularMonitor cm = new CircularMonitor();
copts.CalculationMonitor = cm;
```
Burada, bir örnek oluşturuyoruz `CalculationOptions` ve bir gelenek `CircularMonitor`Bu monitör, hesaplamalar sırasında bulunan dairesel referansların izlenmesine yardımcı olacaktır.
## Adım 5: Formülleri Hesaplayın
Şimdi çalışma kitabınızdaki formülleri hesaplamanın zamanı geldi.
```csharp
objWB.CalculateFormula(copts);
```
Bu satır hesaplamayı gerçekleştirir ve dairesel referansları kontrol eder.
## Adım 6: Dairesel Referansları Say
Hesaplamadan sonra kaç adet dairesel referans bulunduğunu sayabilirsiniz.
```csharp
long lngCircularRef = cm.circulars.Count;
Console.WriteLine("Circular References found - " + lngCircularRef);
```
Bu, Excel dosyanızda tespit edilen dairesel referansların sayısını çıktı olarak verecektir.
## Adım 7: Sonuçları Görüntüle
Son olarak sonuçları görüntüleyelim ve metodumuzun başarıyla çalıştığını doğrulayalım.
```csharp
Console.WriteLine("DetectCircularReference executed successfully.\r\n");
```
## Adım 8: CircularMonitor Sınıfını Uygulayın
İşlemi tamamlamak için aşağıdakileri uygulamanız gerekir: `CircularMonitor` sınıf. Bu sınıf, şu sınıftan miras alacaktır: `AbstractCalculationMonitor` ve dairesel referansların tespitini gerçekleştirir.
```csharp
public class CircularMonitor : AbstractCalculationMonitor
{
    public ArrayList circulars = new ArrayList();
    public ArrayList Circulars { get { return circulars; } }
    public override bool OnCircular(IEnumerator circularCellsData)
    {
        CalculationCell cc = null;
        ArrayList cur = new ArrayList();
        while (circularCellsData.MoveNext())
        {
            cc = (CalculationCell)circularCellsData.Current;
            cur.Add(cc.Worksheet.Name + "!" + CellsHelper.CellIndexToName(cc.CellRow, cc.CellColumn));
        }
        circulars.Add(cur);
        return true;
    }
}
```
Bu sınıf, çalışma sayfası adı ve hücre dizini de dahil olmak üzere bulunan her dairesel referansın ayrıntılarını yakalar.
## Çözüm
Aspose.Cells for .NET kullanarak Excel'de dairesel referansları tespit etmek, yönetilebilir adımlara böldüğünüzde basit bir işlemdir. Bu kılavuzu izleyerek, elektronik tablolarınızdaki dairesel referansları kolayca belirleyebilir ve işleyebilir, hesaplamalarınızın doğru ve güvenilir kalmasını sağlayabilirsiniz. İster deneyimli bir geliştirici olun, ister yeni başlıyor olun, Aspose.Cells Excel düzenleme yeteneklerinizi geliştirmek için güçlü araçlar sunar. 
## SSS
### Excel'de dairesel başvuru nedir?
Döngüsel başvuru, bir formülün kendi hücresine geri dönmesiyle oluşur ve hesaplamalarda sonsuz bir döngüye neden olur.
### Dairesel referansları programatik olarak nasıl tespit edebilirim?
.NET'te Aspose.Cells kütüphanesini kullanarak özel bir hesaplama izleyicisi uygulayarak dairesel referansları programlı olarak algılayabilirsiniz.
### Aspose.Cells'i kullanmak için ön koşullar nelerdir?
Visual Studio, .NET Framework ve Aspose.Cells kütüphanesinin yüklü olması gerekiyor.
### Aspose.Cells'i ücretsiz kullanabilir miyim?
Evet, Aspose.Cells özelliklerini keşfetmeniz için kullanabileceğiniz ücretsiz bir deneme sürümü sunuyor.
### Aspose.Cells hakkında daha fazla bilgiyi nerede bulabilirim?
Ziyaret edebilirsiniz [Aspose.Cells belgeleri](https://reference.aspose.com/cells/net/) Detaylı bilgi ve örnekler için.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}