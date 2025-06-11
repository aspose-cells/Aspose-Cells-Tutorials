---
"description": "Aspose.Cells for .NET kullanarak Excel'deki Power Query formül öğelerini kolayca güncelleyin. Veri işleme süreçlerinizi kolaylaştırmak için adım adım kılavuz."
"linktitle": "Power Query Formül Öğesini Güncelle"
"second_title": "Aspose.Cells for .NET API Başvurusu"
"title": "Power Query Formül Öğesini Güncelle"
"url": "/tr/net/excel-workbook/update-power-query-formula-item/"
"weight": 160
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Power Query Formül Öğesini Güncelle

## giriiş

Excel ile daha önce çalıştıysanız, ne kadar güçlü olabileceğini biliyorsunuzdur; özellikle Power Queries'e dalmaya başladığınızda. Bunlar, verilerinizi zahmetsizce dönüştürmenize, temizlemenize ve analiz etmenize olanak tanıyan gizli soslardır. Excel'deki Power Query formüllerinizi düzenlemenin akıllıca bir yolu da .NET için Aspose.Cells'dir. Bugün, Power Query formül öğelerini adım adım güncelleme konusunda size rehberlik edeceğiz. O halde, kodlama şapkanızı alın ve başlayalım!

## Ön koşullar

Koda dalmadan önce, ayarlamanız gereken birkaç şey var:

1. Visual Studio: .NET kodunuzu yazmak ve çalıştırmak için entegre bir geliştirme ortamına (IDE) ihtiyacınız olacak. Visual Studio bunun için en iyi seçimdir.
2. Aspose.Cells Kütüphanesi: Projenizde Aspose.Cells kütüphanesinin mevcut olduğundan emin olun. Bunu şuradan indirebilirsiniz: [alan](https://releases.aspose.com/cells/net/).
3. C# Hakkında Temel Bilgiler: Bunu birlikte ele alacağız ancak C# hakkında temel bilgilere sahip olmak, özellikle farklı sınıflar ve yöntemler arasında gezinirken kesinlikle yardımcı olacaktır.
4. Örnek Excel Dosyaları: Kod parçacığında belirtilen Excel dosyalarına ihtiyacınız olacak. Şunlara sahip olduğunuzdan emin olun:
   - `SamplePowerQueryFormula.xlsx`
   - `SamplePowerQueryFormulaSource.xlsx`

5. .NET Framework: Projenizin .NET Framework'ün uyumlu bir sürümünü hedeflediğinden emin olun.

Artık setimiz hazır olduğuna göre, eğlenceli kısma geçebiliriz: Kod yazmaya!

## Paketleri İçe Aktar

İlk önce, gerekli ad alanlarını içe aktarmak isteyeceksiniz. Bunu nasıl yapacağınız aşağıda açıklanmıştır:

```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```

Bu ad alanlarını ekleyerek, derleyiciye Aspose.Cells kütüphanesindeki sınıfları ve yöntemleri kullanmayı planladığınızı bildiriyorsunuz. Bu adım, takip eden kod için temel oluşturduğu için önemlidir.

Sağladığınız kod parçacığını parçalara ayıralım. Bu eğitim, her bir bölümde size yol gösterecek ve neler olup bittiğini anlamanızı sağlayacaktır.

## Adım 1: Çalışma Dizinlerini Ayarlayın

Bu adımda, kaynak ve çıktı dosyalarımızın nerede bulunduğunu tanımlayacağız. Bu, Aspose'un Excel dosyalarınızı nerede arayacağını bilmesini sağlar.

```csharp
// Çalışma dizinleri
string SourceDir = "Your Document Directory";
string outputDir = "Your Output Directory";
```

## Adım 2: Çalışma Kitabını Yükleyin

Şimdi Power Query'nin bulunduğu Excel dosyasını yükleyelim.

```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
The `Workbook` sınıf, Excel dosyasına giriş noktanızdır. Kaynak dosyamızın yolunu geçirerek, onu düzenlememize izin veren bir örnek oluşturuyoruz. Bunu bir kitabı açmak gibi düşünebilirsiniz; içeriğini okumaya (veya düzenlemeye) hazırlanıyorsunuz.

## Adım 3: Veri Mashup'ına erişin

Daha sonra çalışma kitabının Veri Mashup'ında saklanan Power Query formüllerine erişeceğiz.

```csharp
DataMashup mashupData = workbook.DataMashup;
```
The `DataMashup` sınıfı, çalışma kitabınızla ilişkili tüm Power Query formüllerini içerir. Burası, onarımlar için bir alet kutusu açtığınızda olduğu gibi, ağır işlerimizi yapacağımız yerdir.

## Adım 4: Power Query Formüllerinde Döngü

Şimdi güncellemek istediğimiz belirli formülü bulmak için Power Query formüllerini yineleyeceğimiz kısma geliyoruz.

```csharp
foreach (PowerQueryFormula formula in mashupData.PowerQueryFormulas)
{
    foreach (PowerQueryFormulaItem item in formula.PowerQueryFormulaItems)
    {
        if (item.Name == "Source")
        {
            item.Value = "Excel.Workbook(File.Contents(\"" + SourceDir + "SamplePowerQueryFormulaSource.xlsx\"), null, true)";
        }
    }
}
```

- Her bir döngüde `PowerQueryFormula` içinde `mashupData`.
- Bu döngü içerisinde her birimizin içine dalıyoruz `PowerQueryFormulaItem`.
- Öğenin adının "Kaynak" ile eşleşip eşleşmediğini kontrol ediyoruz. Eşleşiyorsa, değerini yeni kaynak dosyamıza bağlayacak şekilde güncelliyoruz.

Bu, bir kılavuzda doğru sayfayı bulup ardından gerekli güncellemeleri yapmaya benzer; basit ve titiz bir süreçtir.

## Adım 5: Güncellenen Çalışma Kitabını Kaydedin

Güncellemeleri yaptıktan sonra değişikliklerimizi kaydetmenin zamanı geldi.

```csharp
// Çıktı çalışma kitabını kaydedin.
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
The `Save` method güncellenen çalışma kitabını belirtilen çıktı dizinine yazar. Bu, düzenlemelerinizi kılavuzun yeni bir sürümünde mühürlemek ve başkalarının kullanımına hazır hale getirmek gibidir!

## Çözüm

Tebrikler! Aspose.Cells for .NET kullanarak bir Power Query formül öğesini başarıyla güncellediniz. Bu yöntemle, Excel dosyalarınızdaki Power Query formüllerinin değiştirilmesini otomatikleştirebilir, böylece değerli zaman ve emekten tasarruf edebilirsiniz.

## SSS

### Aspose.Cells Nedir?
Aspose.Cells, Microsoft Excel'in kurulmasına gerek kalmadan .NET uygulamalarında Excel dosyalarını düzenlemek için güçlü bir kütüphanedir.

### Aspose.Cells'i çalıştırmak için Microsoft Excel'e ihtiyacım var mı?
Hayır, Aspose.Cells, sunucunuzda veya geliştirme makinenizde Excel'e ihtiyaç duymadan Excel dosyalarını program aracılığıyla oluşturmanıza ve düzenlemenize olanak tanır.

### Aspose.Cells'i kullanarak hangi tür Excel dosyalarıyla çalışabilirim?
Aspose.Cells'i kullanarak .xlsx, .xls, .xlsm ve diğer birçok Excel formatıyla çalışabilirsiniz.

### Aspose.Cells için deneme sürümü mevcut mu?
Evet, ücretsiz deneme sürümünü şu adresten indirebilirsiniz: [Aspose Cells sürüm sayfası](https://releases.aspose.com/).

### Aspose.Cells için nasıl destek alabilirim?
Desteğe şu şekilde erişebilirsiniz: [Aspose forumu](https://forum.aspose.com/c/cells/9)Topluluk ve Aspose ekibinden sorular sorabileceğiniz ve yanıtlar bulabileceğiniz yer.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}