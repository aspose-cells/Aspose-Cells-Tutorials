---
title: Aspose.Cells kullanarak Çalışma Kitabı İçindeki Verileri Kopyalama
linktitle: Aspose.Cells kullanarak Çalışma Kitabı İçindeki Verileri Kopyalama
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Aspose.Cells for .NET'i kullanarak Excel çalışma kitabındaki verileri adım adım kılavuz, kod örnekleri ve faydalı ipuçlarıyla etkili bir şekilde kopyalamayı öğrenin.
weight: 12
url: /tr/net/worksheet-value-operations/copy-data-within-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells kullanarak Çalışma Kitabı İçindeki Verileri Kopyalama

## giriiş
Excel çalışma kitaplarındaki verileri yönetmek birçok uygulamanın temel bir parçasıdır. Temel verilerle dolu bir şablonunuz veya sayfanız olduğunu ve bunları daha sonra kullanmak üzere aynı çalışma kitabına kopyalamak istediğinizi düşünün. İşte .NET için Aspose.Cells'in parladığı yer burası! Bu kılavuzda, kullanıcı dostu ve anlaşılır bir adım adım eğitimle Aspose.Cells'i kullanarak aynı çalışma kitabındaki verileri kopyalama konusunda size yol göstereceğiz.
## Ön koşullar
Kodlamaya başlamadan önce, bu görevi tamamlamak için ihtiyacımız olan her şeye sahip olduğumuzdan emin olalım:
1.  Aspose.Cells for .NET Kütüphanesi – En son sürümü şu adresten indirin:[Aspose.Cells for .NET indirme sayfası](https://releases.aspose.com/cells/net/).
2. Geliştirme Ortamı – Visual Studio gibi .NET uyumlu bir IDE'ye ihtiyacınız olacak.
3.  Lisans – Aspose.Cells için ücretsiz deneme veya satın alınmış lisans kullanma. Geçici bir lisans alabilirsiniz[Burada](https://purchase.aspose.com/temporary-license/) veya satın alma seçeneklerini keşfedin[Burada](https://purchase.aspose.com/buy).
## Paketleri İçe Aktar
Kodunuzda, sınıflarını ve metotlarını kullanabilmek için Aspose.Cells'i içe aktarmanız gerekecektir:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Koda dalalım! Aspose.Cells for .NET kullanarak bir çalışma kitabındaki verileri kopyalama görevini kolay takip edilebilir adımlara ayıracağız.
## Adım 1: Dizin Yollarınızı Ayarlayın
Çalışma kitabını işlemeye başlamadan önce, dosyalarımızın nerede olduğunu ve çıktıyı nereye kaydetmek istediğimizi tanımlayalım. Bir dizin yolu ayarlamak, her şeyi düzenli tutar.
```csharp
// Belgeler için dizin yolunu ayarlayın.
string dataDir = "Your Document Directory";
string inputPath = dataDir + "book1.xls";
```
 Burada, değiştirin`"Your Document Directory"` çalışma kitabınızın saklandığı gerçek yol ile. Bu yol değişkeni, giriş ve çıkış dosyalarınıza başvurmanızı kolaylaştıracaktır.
## Adım 2: Mevcut Excel Dosyasını Açın
Bir Excel dosyasıyla çalışmak için, onu Aspose.Cells'deki çalışma kitabı nesnesine yüklememiz gerekir. Bu adım, veri kopyalamak istediğiniz dosyayı açar.
```csharp
// Mevcut bir Excel dosyasını açın.
Workbook wb = new Workbook(inputPath);
```
 Bununla birlikte, bizim`Workbook` nesne`wb` artık içeriklerle etkileşime girmeye hazır`book1.xls`.
## Adım 3: Çalışma Sayfaları Koleksiyonuna Erişim
 Artık çalışma kitabı açık olduğuna göre, çalışma sayfaları koleksiyonuna erişeceğiz.`WorksheetCollection` sınıf, çalışma kitabındaki birden fazla sayfayla çalışmamıza yardımcı olur.
```csharp
// Çalışma kitabındaki tüm sayfalara başvuran bir Çalışma Sayfaları nesnesi oluşturun.
WorksheetCollection sheets = wb.Worksheets;
```
 Burada,`sheets` çalışma kitabındaki her sayfayı düzenlememize, var olan bir sayfanın kopyasını eklememize olanak tanır.
## Adım 4: Verileri Yeni Bir Sayfaya Kopyala
Görevimizin ana kısmı, aynı çalışma kitabındaki bir sayfanın içeriklerini yeni bir sayfaya kopyalamaktır. Bu örnekte, "Sheet1"deki verileri yeni bir sayfaya kopyalayacağız.
```csharp
// Çalışma kitabındaki "Sayfa1"deki verileri yeni bir sayfaya kopyalayın.
sheets.AddCopy("Sheet1");
```
 The`AddCopy`method belirtilen sayfanın tam bir kopyasını oluşturur ve bunu çalışma kitabına ekler. Burada "Sheet1"i çoğaltıyoruz. Kopyalamak istediğiniz herhangi bir sayfanın adını belirtebilirsiniz.
## Adım 5: Çalışma Kitabını Yeni Sayfayla Kaydedin
Sayfayı kopyaladıktan sonra, değişiklikleri korumak için çalışma kitabını yeni bir adla veya yeni bir konuma kaydedin.
```csharp
// Kopyalanan verilerle çalışma kitabını kaydedin.
wb.Save(dataDir + "CopyWithinWorkbook_out.xls");
```
 Bu satır, değiştirilen çalışma kitabını şu şekilde kaydeder:`CopyWithinWorkbook_out.xls` belirtilen dizinde.
## Çözüm
İşte karşınızda! Aspose.Cells for .NET kullanarak bir çalışma kitabındaki verileri kopyalamak çocuk oyuncağı. Aspose.Cells, Excel dosyalarını yönetmeyi kolaylaştırır ve karmaşık veri yönetimi görevlerini kolaylıkla gerçekleştirmenizi sağlar. Şablon kullanımı, yedeklemeler veya yeni sürümler oluşturmak için sayfaları çoğaltmanız gerekip gerekmediğine bakılmaksızın, ele aldığımız adımlar hedeflerinize ulaşmanıza yardımcı olacaktır.
 Daha fazlasını keşfetmeye hevesliyseniz, şuraya göz atın:[Aspose.Cells belgeleri](https://reference.aspose.com/cells/net/) Gelişmiş özellikler ve yetenekler için.
## SSS
### Birden fazla sayfayı aynı anda kopyalayabilir miyim?
Aspose.Cells tek bir çağrıda birden fazla sayfanın kopyalanmasını desteklemez, ancak çoğaltmak istediğiniz sayfalar arasında dolaşabilir ve bunları tek tek kopyalayabilirsiniz.
### Kopyalanan sayfanın adını değiştirebilir miyim?
 Evet, sayfayı kopyaladıktan sonra, onu kullanarak yeniden adlandırabilirsiniz.`sheets[sheets.Count - 1].Name = "NewSheetName";`.
### Aspose.Cells .NET Core ile uyumlu mu?
Kesinlikle! Aspose.Cells hem .NET Framework hem de .NET Core ortamlarını destekler.
### Sayfaları kopyalarken biçimlendirmeyi nasıl hallederim?
 The`AddCopy` Bu yöntem tüm içeriği ve biçimlendirmeyi koruduğu için kopyaladığınız sayfa tıpkı orijinali gibi görünecektir.
### Ya bir sayfayı farklı bir çalışma kitabına kopyalamak istersem?
Kullanabilirsiniz`Copy` başka bir çalışma kitabına referansı olan yöntem, örneğin`sheets.Add().Copy(wb.Worksheets["Sheet1"]);`.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
