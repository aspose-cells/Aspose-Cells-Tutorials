---
title: .NET'te JSON'u CSV'ye Programatik Olarak Dönüştürme
linktitle: .NET'te JSON'u CSV'ye Programatik Olarak Dönüştürme
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Aspose.Cells kullanarak .NET'te JSON'u programatik olarak CSV'ye nasıl dönüştüreceğinizi öğrenin. Sorunsuz veri dönüşümünü sağlamak için adım adım kılavuzumuzu izleyin.
weight: 15
url: /tr/net/converting-excel-files-to-other-formats/converting-json-to-csv/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET'te JSON'u CSV'ye Programatik Olarak Dönüştürme

## giriiş
Günümüzün dijital dünyasında, verileri birden fazla biçimde işlemek sıradan hale geldi ve JSON (JavaScript Nesne Gösterimi), veri alışverişi için en yaygın kullanılan biçimlerden biridir. Peki, bu JSON'u CSV (Virgülle Ayrılmış Değerler) gibi analiz için daha erişilebilir bir biçime dönüştürmeniz gerektiğinde ne olur? Bu eğitim, kullanımı kolay ancak güçlü bir elektronik tablo düzenleme API'si olan Aspose.Cells for .NET'i kullanarak JSON'u programatik olarak CSV'ye dönüştürme sürecini size gösterecektir. 
## Ön koşullar
Koda dalmadan önce, gerekli tüm bileşenlere ve kullanacağımız araçlar hakkında temel bir anlayışa sahip olduğunuzdan emin olmanız önemlidir. İhtiyacınız olan şeyleri ana hatlarıyla açıklayalım:
-  Aspose.Cells for .NET: Bu, JSON'u CSV'ye dönüştürmek için kullanacağımız birincil kütüphanedir.[buradan indirin](https://releases.aspose.com/cells/net/).
- Visual Studio: .NET kodunu yazmak ve çalıştırmak için Visual Studio gibi bir entegre geliştirme ortamına (IDE) ihtiyacınız olacak.
- .NET Framework: .NET Framework'ün yüklü olduğundan emin olun. Aspose.Cells hem .NET Core hem de .NET Framework ile uyumludur.
- C# Temel Bilgileri: Bu kılavuz kodun her bir bölümünü parçalara ayıracak olsa da, C# ile ilgili bir miktar bilginiz olması faydalı olacaktır.
## Paketleri İçe Aktar
.NET projenizde Aspose.Cells'i kullanmak için öncelikle kütüphaneyi yüklemeniz gerekir. Bunu NuGet Paket Yöneticisi aracılığıyla yapabilirsiniz:
1. Visual Studio’yu açın.
2. Araçlar > NuGet Paket Yöneticisi > Çözüm için NuGet Paketlerini Yönet'e gidin.
3. Aspose.Cells'i arayın ve en son sürümü yükleyin.
Kurulum tamamlandıktan sonra kodunuza aşağıdaki ad alanlarını eklediğinizden emin olun:
```csharp
using Aspose.Cells.Utility;
using System;
using System.IO;
```
Artık her şey ayarlandığına göre, Aspose.Cells kullanarak bir JSON dosyasını CSV'ye dönüştürmenin ne kadar kolay olduğunu görebilmeniz için kodu adım adım parçalayalım.
## Adım 1: JSON Dosyasını Okuyun
 Yapmamız gereken ilk şey bir dosyadan JSON verilerini okumaktır. Zaten bir JSON dosyanız olduğunu varsayalım (adını koyalım)`SampleJson.json`) sisteminizdeki bir dizinde saklanır.
Kullanabilirsiniz`File.ReadAllText()` C# dilinde JSON dosyasının içeriğini bir dizeye okumak için kullanılan yöntem.
```csharp
// Kaynak dizini
string sourceDir = "Your Document Directory";
// JSON dosyasını oku
string str = File.ReadAllText(sourceDir + "SampleJson.json");
```

Bu adım çok önemlidir çünkü dönüştürme işlemini başlatmak için ham JSON verilerine ihtiyacınız vardır. Bunu bir dize olarak okuyarak, Aspose.Cells tarafından işlenmeye hazırlıyorsunuz.
## Adım 2: Boş bir Çalışma Kitabı Oluşturun
Aspose.Cells öncelikle çalışma kitaplarında (Excel dosyaları) çalışır. JSON verilerini içe aktarmaya başlamak için, öncelikle bu verilerin ekleneceği boş bir çalışma kitabı oluşturmanız gerekir.
```csharp
// Boş çalışma kitabı oluştur
Workbook workbook = new Workbook();
```
Burada, sonunda CSV biçimli verileri tutacak boş bir çalışma kitabı başlatıyorsunuz. Bunu, yakında JSON verilerinizle doldurulacak olan Excel'de boş bir elektronik tablo oluşturmak olarak düşünün.
## Adım 3: Çalışma Kitabındaki Hücrelere Erişim
 Şimdi boş bir çalışma kitabımız olduğuna göre, hücrelerine erişmemiz gerekiyor.`Cells` Aspose.Cells'deki koleksiyon, JSON verilerinizi yerleştireceğiniz çalışma sayfasındaki tüm hücreleri temsil eder.
```csharp
// Hücreleri Al
Cells cells = workbook.Worksheets[0].Cells;
```
Bu kod parçacığı ilk çalışma sayfasını (0 dizinindeki çalışma sayfası) seçer ve`Cells` koleksiyon. Bu hücreler, verilerin ekleneceği bir elektronik tablonun ızgarası gibidir.
## Adım 4: JsonLayoutOptions'ı ayarlayın
 Aspose.Cells, JSON verilerinizin nasıl içe aktarılacağına ilişkin çeşitli özelleştirme seçenekleri sunar. Burada,`JsonLayoutOptions` Aspose'un dizileri, sayısal verileri ve nesne başlıklarını nasıl işleyeceğini belirtmek için.
```csharp
// JsonLayoutOptions'ı Ayarla
JsonLayoutOptions importOptions = new JsonLayoutOptions();
importOptions.ConvertNumericOrDate = true;
importOptions.ArrayAsTable = true;
importOptions.IgnoreArrayTitle = true;
importOptions.IgnoreObjectTitle = true;
```

- ConvertNumericOrDate: Sayısal veya tarih değerleri olan dize değerlerini otomatik olarak dönüştürür.
- ArrayAsTable: JSON'daki dizileri çalışma kitabındaki tablolar olarak ele al.
- IgnoreArrayTitle ve IgnoreObjectTitle: Bu seçenekler diziler ve nesneler için başlıkları yok sayarak yalnızca ham verilerin içe aktarılmasını sağlar.
## Adım 5: JSON Verilerini İçe Aktarın
 Düzen seçenekleri ayarlandıktan sonra, JSON verilerini getirmenin zamanı geldi.`JsonUtility.ImportData()` method burada ağır işi yapar ve JSON verilerini çalışma kitabının hücrelerine ekler.
```csharp
JsonUtility.ImportData(str, cells, 0, 0, importOptions);
```
Bu yöntem birkaç parametre alır:
- `str`1. Adımda okuduğumuz JSON dizisi.
- `cells`: Verilerin yerleştirileceği hücre koleksiyonu.
- `0, 0`: Bunlar, verilerin nereden başlayacağını (yani sol üst köşeden) belirten satır ve sütun dizinleridir.
- `importOptions`: 4. Adımda belirlediğimiz düzen seçenekleri.
## Adım 6: Çalışma Kitabını CSV Olarak Kaydedin
Artık JSON verileri çalışma kitabında olduğuna göre, çalışma kitabını kolayca bir CSV dosyası olarak kaydedebiliriz. CSV, tablo verilerini depolamak için basit ve hafif bir biçimdir ve bu da onu veri analizi için mükemmel kılar.
```csharp
// Çıktı dizini
string outputDir = "Your Document Directory";
// Çalışma Kitabını Kaydet
workbook.Save(outputDir + @"SampleJson_out.csv");
```
Bu adımda çalışma kitabını CSV dosyası olarak kaydediyoruz. Yolu ve dosya adını belirtirsiniz (`SampleJson_out.csv`) CSV'nin kaydedileceği yer.
## Adım 7: İşlemi Onaylayın
Her şeyin beklendiği gibi çalıştığından emin olmak için konsolda bir onay mesajı yazdırabiliriz.
```csharp
Console.WriteLine("ConvertJsonToCsv executed successfully.");
```
Basit bir başarı mesajı, sürecin sorunsuz bir şekilde ilerlediğini doğrulamaya yardımcı olur.
## Çözüm
JSON'u .NET için Aspose.Cells kullanarak CSV'ye dönüştürmek basit ama güçlü bir işlemdir. Sadece birkaç satır kodla karmaşık JSON verilerini daha erişilebilir bir CSV biçimine dönüştürebilirsiniz. İster dizilerle, ister nesnelerle veya sayısal verilerle uğraşıyor olun, Aspose.Cells dönüştürme sürecini ihtiyaçlarınıza uyacak şekilde yapılandırmayı kolaylaştırır.
## SSS
### Aspose.Cells büyük JSON dosyalarını işleyebilir mi?
Evet, Aspose.Cells büyük veri kümelerini verimli bir şekilde işleyecek şekilde tasarlanmıştır ve bu sayede büyük JSON dosyalarını performans sorunları yaşamadan işlemek için uygundur.
### CSV çıktısını nasıl özelleştirebilirim?
 CSV çıktısını ayarlayarak özelleştirebilirsiniz.`JsonLayoutOptions` veya CSV olarak kaydetmeden önce çalışma kitabının biçimlendirmesini değiştirmek.
### Dönüştürme sırasında JSON'dan belirli verileri hariç tutmanın bir yolu var mı?
Evet, içe aktarmadan önce JSON'u düzenleyerek veya özel kod mantığını kullanarak belirli veri alanlarını hariç tutabilir veya filtreleyebilirsiniz.
### Aspose.Cells CSV dışında başka dosya formatlarını da destekliyor mu?
Kesinlikle! Aspose.Cells, Excel (XLS, XLSX), PDF, HTML ve daha birçok formatı destekler.
### Aspose.Cells'i ücretsiz olarak nasıl deneyebilirim?
 Yapabilirsiniz[buradan ücretsiz deneme sürümünü indirin](https://releases.aspose.com/) satın almadan önce tüm özelliklerini test edin.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
