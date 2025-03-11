---
title: Yalnızca Excel Dosyasından Görünür Sayfaları Yükle
linktitle: Yalnızca Excel Dosyasından Görünür Sayfaları Yükle
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Bu adım adım kılavuzda, Aspose.Cells for .NET kullanarak Excel dosyalarından yalnızca görünür sayfaların nasıl yükleneceğini öğrenin.
weight: 12
url: /tr/net/excel-file-handling/load-visible-sheets-only/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Yalnızca Excel Dosyasından Görünür Sayfaları Yükle

## giriiş
.NET uygulamalarınızda Excel dosyalarıyla çalışırken, özellikle bazıları gizli veya operasyonunuzla ilgili olmadığında, birden fazla çalışma sayfasını yönetme zorluğu belirginleşir. .NET için Aspose.Cells, Excel dosyalarını verimli bir şekilde yönetmenize yardımcı olan güçlü bir kütüphanedir. Bu makalede, bir Excel dosyasından yalnızca görünür sayfaları nasıl yükleyeceğinizi ve gizli verileri nasıl filtreleyeceğinizi inceleyeceğiz. Excel verilerinizde gezinirken kendinizi bunalmış hissettiyseniz, bu kılavuz tam size göre!
## Ön koşullar
Eğitime başlamadan önce, takip etmeniz gereken her şeye sahip olduğunuzdan emin olalım:
1. C# Temel Anlayışı: Bu eğitim, C# programlama diline aşina olan geliştiriciler için tasarlanmıştır.
2.  Aspose.Cells for .NET: Aspose.Cells for .NET kitaplığını indirmiş ve kurmuş olmanız gerekir.[kütüphaneyi buradan indirin](https://releases.aspose.com/cells/net/).
3. Visual Studio veya Herhangi Bir IDE: C# kodlarınızı yazıp test edebileceğiniz bir IDE'niz olmalı.
4. .NET Framework: Uygulamalarınızı çalıştırmak için gerekli .NET Framework'ün yüklü olduğundan emin olun.
5. Örnek Excel Dosyası: Uygulama için örnek bir Excel dosyası oluşturun veya verilen kodu takip edin.
Her şey hazır mı? Harika! Hadi başlayalım!
## Paketleri İçe Aktar
Aspose.Cells ile çalışan herhangi bir C# projesinin ilk adımlarından biri gerekli paketleri içe aktarmaktır. Bu, kütüphanenin sağladığı tüm işlevlere erişmenizi sağlar. İşte nasıl yapılacağı:
1. Projenizi Açın: Öncelikle C# projenizi Visual Studio'da veya tercih ettiğiniz herhangi bir IDE'de açın.
2. Referans Ekleme: Çözüm Gezgini'nde projenize sağ tıklayın, "Ekle"yi ve ardından "Referans"ı seçin. 
3. Aspose.Cells'i arayın: Daha önce indirdiğiniz Aspose.Cells.dll dosyasını bulun ve proje referanslarınıza ekleyin.
Bu adım, Aspose.Cells işlevselliğini projenize bağladığı için önemlidir. 
```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Artık gerekli paketleri içe aktardığınıza göre, örnek bir Excel çalışma kitabı oluşturacağız. Bu çalışma kitabında birden fazla sayfamız olacak ve bunlardan biri bu eğitim için gizlenecek.
## Adım 1: Ortamınızı Kurun
Öncelikle ortamı ayarlayalım ve örnek dosya için yolları belirleyelim.
```csharp
// Belgeler dizinine giden yol.
string dataDir = "Your Document Directory";
string sampleFile = "output.xlsx";
string samplePath = dataDir + sampleFile;
```
 Bu kod parçacığında şunu değiştirin:`"Your Document Directory"` çalışma kitabınızı kaydetmek istediğiniz gerçek yol ile. 
## Adım 2: Çalışma Kitabını Oluşturun
Şimdi çalışma kitabını oluşturalım ve biraz veri ekleyelim.
```csharp
// Örnek bir çalışma kitabı oluşturun
Workbook createWorkbook = new Workbook();
createWorkbook.Worksheets["Sheet1"].Cells["A1"].Value = "Aspose";
createWorkbook.Worksheets.Add("Sheet2").Cells["A1"].Value = "Aspose";
createWorkbook.Worksheets.Add("Sheet3").Cells["A1"].Value = "Aspose";
createWorkbook.Worksheets["Sheet3"].IsVisible = false; // Sheet3'ü gizli yap
createWorkbook.Save(samplePath);
```
İşte olup bitenlerin özeti:
- Yeni bir çalışma kitabı oluşturuyoruz ve üç sayfa ekliyoruz.
- “Sheet1” ve “Sheet2” görünür olacak, “Sheet3” ise gizlenecek.
- Daha sonra çalışma kitabını belirtilen yola kaydediyoruz.
## Adım 3: Örnek Çalışma Kitabını Yükleme Seçenekleriyle Yükleyin
Artık görünür ve gizli sayfaların olduğu bir çalışma kitabımız olduğuna göre, yalnızca görünür sayfalara eriştiğimizden emin olarak çalışma kitabını yüklemenin zamanı geldi.
```csharp
LoadOptions loadOptions = new LoadOptions();
loadOptions.LoadFilter = new CustomLoad();
```
Bu kod parçacığı, gizli sayfaları filtrelemek için özelleştireceğimiz çalışma kitabı için yükleme seçeneklerini ayarlar.
## Adım 4: Özel Yük Filtresini Tanımlayın
Yalnızca görünür sayfaları yüklemek için özel bir yükleme filtresi oluşturmamız gerekir. Bunu nasıl tanımlayacağımız aşağıda açıklanmıştır:
```csharp
class CustomLoad : LoadFilter
{
    public override void StartSheet(Worksheet sheet)
    {
        if (sheet.IsVisible)
        {
            this.LoadDataFilterOptions = LoadDataFilterOptions.All;
        }
        else
        {
            this.LoadDataFilterOptions = LoadDataFilterOptions.Structure;
        }
    }
}
```
-  The`StartSheet` yöntem her sayfanın görünür olup olmadığını kontrol eder.
- Eğer görünür durumdaysa, o sayfadaki tüm verileri yükler.
- Görünmüyorsa, o sayfadan herhangi bir veri yüklemeyi atlar.
## Adım 5: Yükleme Seçeneklerini Kullanarak Çalışma Kitabını Yükleyin
Şimdi çalışma kitabını yükleyelim ve görünen sayfalardaki verileri görüntüleyelim.
```csharp
Workbook loadWorkbook = new Workbook(samplePath, loadOptions);
Console.WriteLine("Sheet1: A1: {0}", loadWorkbook.Worksheets["Sheet1"].Cells["A1"].Value);
Console.WriteLine("Sheet2: A1: {0}", loadWorkbook.Worksheets["Sheet2"].Cells["A1"].Value);
```
 Bu kod parçacığı şunu kullanır:`loadOptions` yalnızca görünür sayfalardan veri içe aktarmak ve “Sayfa1” ve “Sayfa2”deki A1 hücresinin içeriğini görüntülemek için. 
## Çözüm
Ve işte oldu! Aspose.Cells for .NET kullanarak bir Excel dosyasından yalnızca görünür sayfaları yüklemeyi başarıyla öğrendiniz. Aldığınız verileri nasıl sınırlayacağınızı ve yalnızca ihtiyacınız olanla nasıl çalışacağınızı bildiğinizde Excel çalışma sayfalarınızı yönetmek çok kolay olabilir. Bu yalnızca uygulamalarınızın verimliliğini artırmakla kalmaz, aynı zamanda kodunuzu daha temiz ve yönetilmesi daha kolay hale getirir. 
## SSS
### Gerektiğinde gizli sayfalar yükleyebilir miyim?
Evet, gizli sayfaları da içerecek şekilde özel yükleme filtresindeki koşulları kolayca ayarlayabilirsiniz.
### Aspose.Cells ne için kullanılır?
Aspose.Cells, Microsoft Excel'in kurulu olmasına gerek kalmadan Excel dosyalarını düzenlemek için kullanılır ve Excel çalışma sayfalarını okuma, yazma ve yönetme gibi işlevler sunar.
### Aspose.Cells'in deneme sürümü var mı?
 Evet yapabilirsin[ücretsiz deneme sürümünü indirin](https://releases.aspose.com/) Özelliklerini test etmek için.
### Aspose.Cells için dokümanları nerede bulabilirim?
 The[belgeleme](https://reference.aspose.com/cells/net/) tüm özellikler hakkında kapsamlı bilgi sağlar.
### Aspose.Cells'i nasıl satın alabilirim?
 Kolayca yapabilirsiniz[Aspose.Cells'i satın al](https://purchase.aspose.com/buy) satın alma sayfalarından.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
