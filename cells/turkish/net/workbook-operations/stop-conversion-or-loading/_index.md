---
title: Interrupt Monitor'ı kullanarak Dönüştürmeyi veya Yüklemeyi Durdurun
linktitle: Interrupt Monitor'ı kullanarak Dönüştürmeyi veya Yüklemeyi Durdurun
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Ayrıntılı, adım adım eğitimle, Interrupt Monitor kullanarak Aspose.Cells for .NET'te çalışma kitabı dönüştürmeyi durdurmayı öğrenin.
weight: 26
url: /tr/net/workbook-operations/stop-conversion-or-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Interrupt Monitor'ı kullanarak Dönüştürmeyi veya Yüklemeyi Durdurun

## giriiş
Büyük Excel dosyalarıyla çalışmak genellikle zaman ve kaynak tüketebilen uzun süreçleri içerir. Peki ya bir şeyin değiştirilmesi gerektiğini fark ettiğinizde dönüştürme sürecini yarıda kesebilseydiniz? Aspose.Cells for .NET, bir çalışma kitabının PDF gibi başka bir biçime dönüştürülmesini kesmenize olanak tanıyan Interrupt Monitor adlı bir özelliğe sahiptir. Bu, özellikle önemli veri dosyalarıyla çalışırken hayat kurtarıcı olabilir. Bu kılavuzda, Aspose.Cells for .NET'te Interrupt Monitor'ü kullanarak dönüştürme sürecini nasıl keseceğinizi ele alacağız.
## Ön koşullar
Başlamadan önce aşağıdakilerin yerinde olduğundan emin olun:
1.  Aspose.Cells for .NET - İndirin[Burada](https://releases.aspose.com/cells/net/).
2. .NET Geliştirme Ortamı - Visual Studio gibi.
3. C# Programlamanın Temel Bilgileri - C# sözdizimine aşinalık, takip etmenize yardımcı olacaktır.
## Paketleri İçe Aktar
Başlamak için gerekli paketleri içe aktaralım. Bu içe aktarımlar şunları içerir:
- Aspose.Cells: Excel dosyalarını düzenlemek için kullanılan ana kütüphane.
- System.Threading: İş parçacıklarını yönetmek için kullanılır, çünkü bu örnekte iki paralel işlem çalıştırılacaktır.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.IO;
```
Süreci ayrıntılı adımlara bölelim. Her adım, Excel çalışma kitabı dönüşümünü yönetmek için Interrupt Monitor'ı kurmanın ve kullanmanın önemini anlamanıza yardımcı olacaktır.
## Adım 1: Sınıfı Oluşturun ve Çıktı Dizinini Ayarlayın
Öncelikle fonksiyonlarımızı kapsülleyecek bir sınıfa ve çıktı dosyasının kaydedileceği bir dizine ihtiyacımız var.
```csharp
class StopConversionOrLoadingUsingInterruptMonitor
{
    static string outputDir = "Your Document Directory";
}
```
 Yer değiştirmek`"Your Document Directory"` PDF dosyasının kaydedilmesini istediğiniz gerçek yol ile.
## Adım 2: Kesinti İzleyicisini Örneklendirin
Sonra, bir InterruptMonitor nesnesi oluşturun. Bu izleyici, herhangi bir noktada kesintiye uğratma yeteneğini ayarlayarak işlemi kontrol etmeye yardımcı olacaktır.
```csharp
InterruptMonitor im = new InterruptMonitor();
```
Bu kesme izleyicisi çalışma kitabımıza eklenecek ve dönüştürme sürecini yönetmemizi sağlayacak.
## Adım 3: Çalışma Kitabını Dönüştürme İçin Ayarlayın
Şimdi bir çalışma kitabı nesnesi oluşturalım, ona InterruptMonitor atayalım ve ardından ilk çalışma sayfasına erişerek örnek metin ekleyelim.
```csharp
void CreateWorkbookAndConvertItToPdfFormat()
{
    Workbook wb = new Workbook();
    wb.InterruptMonitor = im;
    Worksheet ws = wb.Worksheets[0];
    Cell cell = ws.Cells["J1000000"];
    cell.PutValue("This is text.");
}
```
Yukarıdaki kod bir çalışma kitabı oluşturur, bunun için InterruptMonitor'ı ayarlar ve metni uzak bir hücreye yerleştirir (`J1000000`). Metnin bu hücre konumuna yerleştirilmesi, çalışma kitabının işlenmesinin daha fazla zaman almasını sağlayarak InterruptMonitor'a müdahale etmek için yeterli zamanı verir.
## Adım 4: Çalışma Kitabını PDF Olarak Kaydedin ve Kesintiyi Yönetin
 Şimdi çalışma kitabını PDF olarak kaydetmeyi deneyelim. Bir`try-catch` Oluşabilecek herhangi bir kesintiyi engellemek için blok.
```csharp
try
{
    wb.Save(outputDir + "output_InterruptMonitor.pdf");
}
catch (Aspose.Cells.CellsException ex)
{
    Console.WriteLine("Process Interrupted - Message: " + ex.Message);
}
```
İşlem kesintiye uğrarsa, istisna bunu yakalayacak ve uygun bir mesaj görüntüleyecektir. Aksi takdirde, çalışma kitabı PDF olarak kaydedilecektir.
## Adım 5: Dönüştürme İşlemini Kesin
 Buradaki ana özellik, işlemi kesintiye uğratma yeteneğidir. Bir gecikme ekleyeceğiz`Thread.Sleep` ve sonra ara`Interrupt()` 10 saniye sonra dönüşümü durdurma yöntemi.
```csharp
void WaitForWhileAndThenInterrupt()
{
    Thread.Sleep(1000 * 10);
    im.Interrupt();
}
```
Bu gecikme, kesme sinyali gönderilmeden önce çalışma kitabının PDF'ye dönüştürülmeye başlaması için zaman sağlar.
## Adım 6: İş parçacıklarını eş zamanlı olarak yürütün
Her şeyi bir araya getirmek için, her iki işlevi ayrı iş parçacıklarında başlatmamız gerekir. Bu şekilde, çalışma kitabı dönüşümü ve kesme beklemesi aynı anda gerçekleşebilir.
```csharp
public void TestRun()
{
    ThreadStart ts1 = new ThreadStart(this.CreateWorkbookAndConvertItToPdfFormat);
    Thread t1 = new Thread(ts1);
    t1.Start();
    ThreadStart ts2 = new ThreadStart(this.WaitForWhileAndThenInterrupt);
    Thread t2 = new Thread(ts2);
    t2.Start();
    t1.Join();
    t2.Join();
}
```
 Yukarıdaki kod çalışır`CreateWorkbookAndConvertItToPdfFormat` Ve`WaitForWhileAndThenInterrupt` paralel iş parçacıklarında, her iki işlem de tamamlandıktan sonra bunları birleştirir.
## Adım 7: Son Uygulama
 Son olarak bir tane ekleyeceğiz`Run()` kodu çalıştırma yöntemi.
```csharp
public static void Run()
{
    new StopConversionOrLoadingUsingInterruptMonitor().TestRun();
    Console.WriteLine("StopConversionOrLoadingUsingInterruptMonitor executed successfully.");
}
```
 Bu`Run` Yöntem, eylemin kesintiye uğramasını başlatmak ve gözlemlemek için giriş noktasıdır.
## Çözüm
Bu eğitimde, Aspose.Cells for .NET'te dönüştürme sürecini nasıl keseceğinizi inceledik. Kesme İzleyicisi, büyük Excel dosyalarıyla çalışırken faydalı bir araçtır ve işlemlerin tamamlanmasını beklemeden durdurmanıza olanak tanır. Bu, özellikle zamanın ve kaynakların değerli olduğu ve hızlı geri bildirimin gerekli olduğu senaryolarda faydalıdır.
## SSS
### Aspose.Cells for .NET'te Kesinti İzleyicisi Nedir?  
Kesinti İzleyicisi, bir çalışma kitabı dönüştürme veya yükleme işlemini yarıda kesmenize olanak tanır.
### Interrupt Monitor'u PDF dışında başka formatlarda da kullanabilir miyim?  
Evet, desteklenen diğer formatlara dönüştürmeleri de kesebilirsiniz.
### Thread.Sleep() kesme zamanlamasını nasıl etkiler?  
Thread.Sleep(), kesmeyi tetiklemeden önce bir gecikme yaratır ve dönüşümün başlaması için zaman tanır.
### İşlemi 10 saniyeden önce kesebilir miyim?  
 Evet, gecikmeyi değiştirin`WaitForWhileAndThenInterrupt()` daha kısa bir zamana.
### Kesinti işlemi performansı etkiler mi?  
Etkisi minimaldir ve uzun soluklu süreçlerin yönetimi açısından oldukça faydalıdır.
 Daha fazla bilgi için şuraya bakın:[Aspose.Cells for .NET Belgeleri](https://reference.aspose.com/cells/net/) Yardıma ihtiyacınız varsa, şuraya göz atın:[Destek Forumu](https://forum.aspose.com/c/cells/9)veya bir tane al[Ücretsiz Deneme](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
