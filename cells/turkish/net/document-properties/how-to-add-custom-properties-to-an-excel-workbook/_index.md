---
category: general
date: 2026-10-01
description: Aspose.Cells kullanarak bir Excel çalışma kitabına özel özellikler eklemeyi
  öğrenin. Bu kılavuz ayrıca proje kimliğini eklemeyi ve özel özellikleri okumayı
  gösterir.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add custom properties
- how to add custom
- excel custom properties
- add project id
- read custom properties
language: tr
lastmod: 2026-10-01
og_description: Aspose.Cells ile bir Excel çalışma kitabına özel özellikler ekleyin.
  Proje kimliği eklemek, inceleyen bilgilerini ayarlamak ve özel özellikleri programlı
  olarak okumak için bu kapsamlı öğreticiyi izleyin.
og_image_alt: Screenshot of an Excel worksheet displaying custom properties added
  via Aspose.Cells
og_title: Excel çalışma kitabına özel özellikler ekleyin – adım adım rehber
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  headline: How to add custom properties to an Excel workbook
  type: TechArticle
- description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  name: How to add custom properties to an Excel workbook
  steps:
  - name: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
    text: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
  - name: Go to **File → Info → Properties → Advanced Properties**.
    text: Go to **File → Info → Properties → Advanced Properties**.
  - name: Select the **Custom** tab.
    text: Select the **Custom** tab.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Excel çalışma kitabına özel özellikler nasıl eklenir
url: /tr/net/document-properties/how-to-add-custom-properties-to-an-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel çalışma kitabına özel özellikler ekleme

Excel çalışma kitabına **özel özellikler eklemeniz** gerekiyorsa, bu kılavuz Aspose.Cells for .NET ile bunu tam olarak nasıl yapacağınızı gösterir. Ayrıca bir proje kimliği eklemeyi, bir inceleyen adı ayarlamayı ve daha sonra dosyadan **özel özellikleri okuma** yöntemini öğreneceksiniz.

Özel meta verilerle çalışmak, iş‑özel bilgileri doğrudan elektronik tabloya yerleştirmenizi sağlar; böylece sahipliği, sürümü veya başka herhangi bir bağlamı ayrı bir veritabanı tutmadan izlemek kolaylaşır. Aşağıdaki adımlar, çalışma kitabını oluşturmaktan yeni özellikleri kalıcı hale getirmeye kadar tam uçtan uca iş akışını kapsar.

## Önkoşullar

* .NET 6.0 veya daha yeni bir sürüm yüklü  
* Geçerli bir Aspose.Cells for .NET lisansı (veya ücretsiz deneme)  
* Visual Studio 2022 (veya herhangi bir C# IDE)  

`Aspose.Cells` dışındaki ek NuGet paketlerine gerek yok.

## Adım 1: Projeyi kurun ve ad alanlarını içe aktarın

Yeni bir konsol uygulaması oluşturun ve Aspose.Cells referansını ekleyin:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // The rest of the code lives here
        }
    }
}
```

`Aspose.Cells` ad alanı, kullanacağımız `Workbook`, `Worksheet` ve `CustomPropertyCollection` sınıflarını içerir.

## Adım 2: Mevcut bir çalışma kitabını yükleyin (veya yeni bir tane oluşturun)

Mevcut bir `.xlsb` dosyasıyla başlayabilir veya yeni bir çalışma kitabı oluşturabilirsiniz. Aşağıdaki örnek, `YOUR_DIRECTORY` adlı klasörde bulunan **Data.xlsb** dosyasını yükler.

```csharp
// Load the existing workbook
var workbookPath = @"YOUR_DIRECTORY\Data.xlsb";
var workbook = new Workbook(workbookPath);
```

Dosya mevcut değilse, kodu `new Workbook();` ile değiştirerek boş bir çalışma kitabı oluşturun.

## Adım 3: İlk çalışma sayfasına özel özellikler ekleyin

Temel işlem, bir çalışma sayfasına **özel özellikler eklemektir**. Aspose.Cells, özel özellikleri bir sözlük gibi davranan bir koleksiyonda saklar.

```csharp
// Get the first worksheet (index 0)
var worksheet = workbook.Worksheets[0];

// Add a numeric ProjectId property
worksheet.CustomProperties.Add("ProjectId", 12345);

// Add a string Reviewer property
worksheet.CustomProperties.Add("Reviewer", "John Doe");

// Optional: add a DateTime property for the creation timestamp
worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);
```

`CustomProperties.Add` kullanmamızın, `CustomProperties["Name"] = value` yerine tercih edilmesinin nedeni, `Add` metodunun giriş mevcut değilse oluşturması ve doğru veri tipinin saklanmasını garanti etmesidir. Bu yaklaşım, daha sonra değerleri okurken oluşabilecek tip uyumsuzluklarından kaynaklanan çalışma zamanı hatalarını önler.

## Adım 4: Çalışma kitabını yeni özelliklerle kaydedin

Meta verileri ekledikten sonra, değişiklikleri yeni bir dosyaya kaydedin; böylece orijinali dokunulmaz kalır.

```csharp
// Save the workbook with the custom properties
var outputPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Bu noktada Excel dosyası, tanımladığınız özel meta verileri içerir. Özellikleri, bir sonraki bölümdeki adımları izleyerek doğrulayabilirsiniz.

## Adım 5: Bir çalışma kitabından özel özellikleri okuyun

**excel özel özelliklerini** okumak aynı koleksiyon desenini izler. Bu kod parçacığı, az önce sakladığımız değerleri nasıl alacağınızı gösterir.

```csharp
// Load the workbook that contains custom properties
var loadedWorkbook = new Workbook(outputPath);
var loadedWorksheet = loadedWorkbook.Worksheets[0];
var props = loadedWorksheet.CustomProperties;

// Retrieve each property safely
int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

Console.WriteLine($"ProjectId: {projectId}");
Console.WriteLine($"Reviewer: {reviewer}");
Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
```

`CustomPropertyCollection` indisleyicisi bir `CustomProperty` nesnesi döndürür; `Value` özelliğine erişmek, saklanan veriyi orijinal tipinde almanızı sağlar. Dönüştürmeden önce `null` kontrolü yapmak, bir özellik eksik olduğunda `NullReferenceException` oluşmasını önler.

### Beklenen konsol çıktısı

```
ProjectId: 12345
Reviewer: John Doe
CreatedOn (UTC): 2026-10-01 12:34:56Z
```

Zaman damgası, adım 3'te `Add` metodunu çağırdığınız tam anı yansıtacaktır.

## Pro ipucu: Mevcut bir özel özelliği güncelleme

Daha sonra **özel bilgi ekleme** (örneğin, inceleyen kişiyi değiştirme) ihtiyacınız varsa, `CustomPropertyCollection` ayarlayıcısını kullanın:

```csharp
// Change the reviewer name
if (props["Reviewer"] != null)
{
    props["Reviewer"].Value = "Jane Smith";
}
else
{
    // Property does not exist; add it
    props.Add("Reviewer", "Jane Smith");
}
```

Bu desen, özelliğin ya güncellenmesini ya da oluşturulmasını sağlar; bu da otomatik rapor oluşturma gibi yinelemeli iş akışları için faydalıdır.

## Adım 6: Excel içinde özellikleri doğrulayın (isteğe bağlı)

Özel özellikleri doğrudan Excel'de de görüntüleyebilirsiniz:

1. Kaydedilen `DataWithProps.xlsb` dosyasını Microsoft Excel'de açın.  
2. **File → Info → Properties → Advanced Properties** menüsüne gidin.  
3. **Custom** sekmesini seçin.  

`ProjectId`, `Reviewer` ve `CreatedOn` girişlerinin ilgili değerleriyle listelendiğini göreceksiniz.

## Tam çalışan örnek

Aşağıda, önceki tüm kod parçacıklarını birleştiren eksiksiz, bağımsız program yer almaktadır. `Program.cs` dosyasına kopyalayıp çalıştırın; konsol alınan değerleri gösterecektir.

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // Paths (adjust to your environment)
            var sourcePath = @"YOUR_DIRECTORY\Data.xlsb";
            var resultPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";

            // Load or create workbook
            var workbook = new Workbook(sourcePath);
            var worksheet = workbook.Worksheets[0];

            // Add custom properties
            worksheet.CustomProperties.Add("ProjectId", 12345);
            worksheet.CustomProperties.Add("Reviewer", "John Doe");
            worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);

            // Save the workbook
            workbook.Save(resultPath);
            Console.WriteLine($"Saved workbook with custom properties to {resultPath}");

            // Load the saved workbook to read properties
            var loadedWorkbook = new Workbook(resultPath);
            var loadedWorksheet = loadedWorkbook.Worksheets[0];
            var props = loadedWorksheet.CustomProperties;

            // Read properties
            int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
            string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
            DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

            Console.WriteLine($"ProjectId: {projectId}");
            Console.WriteLine($"Reviewer: {reviewer}");
            Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
        }
    }
}
```

Bu programı çalıştırmak, önceki konsol çıktısını üretir ve gömülü meta verileri içeren `DataWithProps.xlsb` dosyasını oluşturur.

## Yaygın sorular ve kenar durumları

| Soru | Cevap |
|---|---|
| **İlkel olmayan tipleri depolayabilir miyim?** | Aspose.Cells `string`, `int`, `double`, `DateTime` ve `bool` tiplerini destekler. Karmaşık nesneler için önce JSON veya XML'e serileştirip dize olarak saklayın. |
| **Çalışma kitabı şifre korumalıysa ne olur?** | `CustomProperties`'a erişmeden önce çalışma kitabını bir şifreyle açın (`new Workbook(path, password)`). Şifre çözme işleminden sonra özelliklere hâlâ erişilebilir. |
| **Özel özellikler format dönüşümünden sonra korunur mu?** | Farklı bir formata (ör. `.xlsx`) kaydederken, hedef format desteklediği sürece Aspose.Cells özel özellikleri korur. |
| **Bir özel özelliği nasıl silerim?** | `worksheet.CustomProperties.Remove("PropertyName");` kullanın. Bu, koleksiyondan ilgili girişi kaldırır. |

## Sonraki adımlar

Artık **özel özellik ekleme** konusunda bilgi sahibi olduğunuza göre, aşağıdaki ilgili konuları keşfedebilirsiniz:

* **excel custom properties** belge sürümleme için  
* Tek bir çalışma kitabındaki birden fazla çalışma sayfasından **read custom properties**  
* **Aspose.Cells** kullanarak özel meta verilere referans veren pivot tablolar oluşturma  
* Çalışma kitabını PDF'ye dışa aktarırken özel özellikleri koruma  

Farklı veri tipleriyle deney yapın, özel özellikleri hücre yorumlarıyla birleştirin veya meta verileri daha büyük bir belge‑yönetim sistemine entegre edin.

---

**Excel raporlamanızı otomatikleştirmeye hazır mısınız?** Yukarıdaki kodu projenize ekleyin, özellik adlarını iş ihtiyaçlarınıza göre ayarlayın ve ardından aşağı akış işlemleri için hazır, kendini tanımlayan bir elektronik tabloya sahip olacaksınız.

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Create Excel Workbook – Add Custom Properties and Save as XLSB](/cells/english/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/)
- [How to Access Custom Document Properties in Excel Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/access-custom-excel-properties-aspose-cells-net/)
- [Master Excel Custom Properties Using Aspose.Cells .NET for Enhanced Data Management](/cells/english/net/data-manipulation/excel-custom-properties-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}