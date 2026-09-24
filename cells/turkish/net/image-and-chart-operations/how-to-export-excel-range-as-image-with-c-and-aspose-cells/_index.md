---
category: general
date: 2026-09-24
description: C# ile Aspose.Cells kullanarak Excel aralığını resim olarak dışa aktar
  – bir çalışma sayfası alanını PNG veya JPEG olarak kaydetmek için adım adım rehber.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel range as image
- Aspose.Cells export range
- C# Excel to PNG
- ImageOrPrintOptions usage
- export pivot table as image
language: tr
lastmod: 2026-09-24
og_description: Aspose.Cells ile C#'ta Excel aralığını görüntü olarak dışa aktarın.
  Pivot tablolar dahil herhangi bir çalışma sayfası alanını dakikalar içinde PNG veya
  JPEG'e nasıl dönüştüreceğinizi öğrenin.
og_image_alt: Screenshot of a C# program exporting an Excel range to a PNG image
og_title: C# ile Excel aralığını resim olarak dışa aktar – kapsamlı Aspose.Cells rehberi
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Export excel range as image in C# using Aspose.Cells – step‑by‑step
    guide to save a worksheet area as PNG or JPEG.
  headline: How to export excel range as image with C# and Aspose.Cells
  type: TechArticle
- description: Export excel range as image in C# using Aspose.Cells – step‑by‑step
    guide to save a worksheet area as PNG or JPEG.
  name: How to export excel range as image with C# and Aspose.Cells
  steps:
  - name: '**Load** the workbook from disk.'
    text: '**Load** the workbook from disk.'
  - name: '**Define** the cell area that will become the image (the *print area*).'
    text: '**Define** the cell area that will become the image (the *print area*).'
  - name: '**Export** the area using `ImageOrPrintOptions` and write the file.'
    text: '**Export** the area using `ImageOrPrintOptions` and write the file.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Image export
title: C# ve Aspose.Cells ile Excel aralığını resim olarak nasıl dışa aktarılır
url: /tr/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ve Aspose.Cells ile Excel aralığını görüntü olarak dışa aktarma

Bir .NET uygulamasında **excel aralığını görüntü olarak dışa aktarmanız** gerekiyorsa, bu rehber size eksiksiz, doğrudan çalıştırılabilir bir çözüm sunar. İster bir gösterge tablosu yayınlıyor olun, ister bir pivot tabloyu bir web sayfasına gömüyor olun, ister bir rapor küçük resmi oluşturuyor olun, birkaç satır C# kodu ile herhangi bir çalışma sayfası alanını PNG (veya JPEG) formatına dönüştürebilirsiniz.

Bu öğreticide şunları öğreneceksiniz:

* Mevcut bir çalışma kitabını (`Workbook` sınıfı) yükleyin  
* Yakalamak istediğiniz tam hücre aralığını (`PrintArea`) tanımlayın  
* `ImageOrPrintOptions` ile görüntü dışa aktarma seçeneklerini yapılandırın  
* Oluşan resmi diske kaydedin  

Tüm ön koşullar, uç durumlar ve yaygın tuzaklar ele alınmıştır, böylece kodu kendi projelerinize sorunsuz bir şekilde uyarlayabilirsiniz.

## Ön Koşullar

Başlamadan önce şunlara sahip olduğunuzdan emin olun:

| Gereksinim | Sebep |
|-------------|--------|
| **Aspose.Cells for .NET** (latest version) | Örnekte kullanılan `Workbook`, `Worksheet` ve `ImageOrPrintOptions` API'lerini sağlar. |
| **.NET 6.0 or later** | Örnek .NET 6 hedeflemektedir, ancak Aspose.Cells'i destekleyen herhangi bir .NET Core/Framework sürümü çalışır. |
| **A valid Excel file** (e.g., `input.xlsx`) | Dönüştürmek istediğiniz çalışma kitabı. |
| **Write permission to the output folder** | `Save` işleminin başarılı olması için gereklidir. |

Aspose.Cells'i NuGet üzerinden kurabilirsiniz:

```bash
dotnet add package Aspose.Cells
```

## Excel aralığını görüntü olarak dışa aktarma – sürecin genel görünümü

İşlem üç mantıksal aşamadan oluşur:

1. **Load**: Çalışma kitabını diskteki dosyadan yükleyin.  
2. **Define**: Görüntü haline gelecek hücre alanını ( *print area* ) tanımlayın.  
3. **Export**: Alanı `ImageOrPrintOptions` kullanarak dışa aktarın ve dosyayı yazın.

Aşağıda her aşama, tam kaynak kodu ve açıklama içeren ayrı bir adıma bölünmüştür.

## Adım 1: Çalışma kitabını yükleme

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Path to the source Excel file
string inputPath = @"YOUR_DIRECTORY\input.xlsx";

// Create a Workbook object – this reads the file into memory
Workbook workbook = new Workbook(inputPath);
```

**Neden Önemlidir:**  
`Workbook`, tüm Excel işlemlerinin giriş noktasıdır. Dosyayı bir kez yüklemek bellek kullanımını düşük tutar ve daha sonra herhangi bir çalışma sayfasına erişmenizi sağlar.

## Adım 2: Hedef çalışma sayfasına erişim

```csharp
// Get the first worksheet (index 0). Change the index or use the sheet name as needed.
Worksheet sheet = workbook.Worksheets[0];
```

**İpucu:** Belirli bir sayfaya isimle ihtiyacınız varsa, indeksi `workbook.Worksheets["SheetName"]` ile değiştirin. Bu, çalışma kitabı düzeni değiştiğinde hataları önler.

## Adım 3: Dışa aktarmak istediğiniz aralığı tanımlama

```csharp
// Define the cell range that will be exported.
// Example: A1:G20 captures a typical pivot‑table area.
sheet.PageSetup.PrintArea = "A1:G20";
```

**Neden `PrintArea` ayarlanır?**  
Aspose.Cells, bir görüntü oluştururken *print area*'yı işler. Bunu tam aralığa sınırlayarak gereksiz boşlukları önler ve performansı artırırsınız.

### Alternatif: Tüm sayfayı dışa aktarma

Tüm çalışma sayfasını dışa aktarmak istiyorsanız, sadece `PrintArea` atamasını atlayın. Aspose.Cells varsayılan olarak sayfanın kullanılan aralığını kullanacaktır.

## Adım 4: Görüntü dışa aktarma seçeneklerini yapılandırma

```csharp
// Create an ImageOrPrintOptions object to control the output format.
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    // Choose PNG for lossless quality; change to Jpeg for smaller files.
    ImageFormat = ImageFormat.Png,

    // Optional: set the resolution (DPI). Higher DPI yields sharper images.
    HorizontalResolution = 300,
    VerticalResolution = 300,

    // Optional: set the page orientation if the range is wide.
    PageOrientation = PageOrientationType.Landscape
};
```

**Ana özelliklerin açıklaması:**

* `ImageFormat` – Dosya tipini belirler (`Png`, `Jpeg`, `Bmp`, vb.). PNG, keskin kenarları koruduğu için grafikler ve metinler için idealdir.  
* `HorizontalResolution` / `VerticalResolution` – Piksel yoğunluğunu kontrol eder. Web küçük resimleri için 96 DPI yeterlidir; baskıya hazır grafikler için 300 DPI önerilir.  
* `PageOrientation` – Seçilen aralık yüksekliğinden daha geniş olduğunda yardımcı olur.

## Adım 5: Aralığı bir görüntü dosyasına dışa aktarma

```csharp
// Define the output path for the image
string outputPath = @"YOUR_DIRECTORY\range.png";

// Save the first picture on the worksheet as an image.
// The Pictures collection is automatically populated after setting PrintArea.
sheet.Pictures[0].Save(outputPath, imgOptions);
```

**Arka planda ne olur:**  
`PrintArea` ayarlandığında, Aspose.Cells o alanı temsil eden geçici bir resim oluşturur. `Pictures[0]` nesnesi daha sonra sağladığınız seçeneklerle kaydedilir.

### Resmi olmayan çalışma sayfalarını işleme

Çalışma sayfası zaten bir resim içermiyorsa (ör. yeni bir dosya), anında bir tane oluşturabilirsiniz:

```csharp
// Create a picture from the defined range and add it to the sheet
Picture pic = sheet.Pictures[sheet.Pictures.Add(0, 0, sheet.PageSetup.PrintArea)];
pic.Save(outputPath, imgOptions);
```

## Tam, çalıştırılabilir örnek

Her şeyi bir araya getirerek, kopyalayıp yapıştırıp çalıştırabileceğiniz bağımsız bir konsol uygulaması aşağıdadır:

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // 2️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Define the range to export (e.g., a pivot table)
        sheet.PageSetup.PrintArea = "A1:G20";

        // 4️⃣ Set image export options (PNG, 300 DPI, landscape)
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300,
            PageOrientation = PageOrientationType.Landscape
        };

        // 5️⃣ Save the picture as an image file
        string outputPath = @"YOUR_DIRECTORY\range.png";

        // Ensure a picture exists; create one if necessary
        Picture pic;
        if (sheet.Pictures.Count == 0)
        {
            pic = sheet.Pictures[sheet.Pictures.Add(0, 0, sheet.PageSetup.PrintArea)];
        }
        else
        {
            pic = sheet.Pictures[0];
        }

        pic.Save(outputPath, imgOptions);

        System.Console.WriteLine($"Export completed: {outputPath}");
    }
}
```

**Beklenen çıktı:**  
`range.png` adlı bir dosya `YOUR_DIRECTORY` içinde ortaya çıkar. Açtığınızda **A1 ile G20** arasındaki tam hücrelerin keskin bir PNG görüntüsü olarak render edildiğini görürsünüz.

## Yaygın varyasyonlar ve uç‑durum yönetimi

| Senaryo | Ayar |
|----------|------------|
| **JPEG olarak dışa aktar** | `ImageFormat = ImageFormat.Jpeg` olarak değiştirin ve isteğe bağlı olarak `Quality = 90` (0‑100 aralığında) ayarlayın. |
| **Birden fazla aralık** | Her aralık için `sheet.Pictures.Add` çağırın ve her resmi ayrı bir dosya adıyla kaydedin. |
| **Büyük çalışma sayfaları** | Bellek artışlarını önlemek için sadece ihtiyaç duyulan aralıkta `HorizontalResolution`/`VerticalResolution` değerlerini artırın. |
| **Resim oluşturulmadı** | `PrintArea`'nın doğru biçimlendirildiğini (`"A1:G20"`) doğrulayın. Geçersiz bir adres, boş bir `Pictures` koleksiyonuna yol açar. |
| **Akıma kaydetme** | Görüntüyü bellek içinde gerektiğinde (ör. bir ASP.NET yanıtı için) `pic.Save(Stream, imgOptions)` kullanın. |

## Güvenilir görüntü dışa aktarma için uzman ipuçları

* **Print area'yı doğrulayın** – `CellArea` ayrıştırmasını (`CellArea area = CellArea.CreateCellArea("A1", "G20")`) kullanarak aralıkları programatik olarak oluşturun ve yazım hatalarından kaçının.  
* **Kaynakları serbest bırakın** – Birçok dosya işliyorsanız `Workbook`'u bir `using` bloğu içinde sararak yerel kaynakları hızlıca serbest bırakın.  
* **Toplu işleme** – Onlarca aralık dışa aktarırken, nesne tahsis yükünü azaltmak için tek bir `ImageOrPrintOptions` örneğini yeniden kullanın.  
* **İş parçacığı güvenliği** – Aspose.Cells nesneleri **iş parçacığı güvenli değildir**. Her iş parçacığı için ayrı bir `Workbook` oluşturun veya erişimi senkronize edin.

## Sonuç

Artık C# ve Aspose.Cells kullanarak **excel aralığını görüntü olarak dışa aktarma** için eksiksiz, üretim‑hazır bir yönteme sahipsiniz. Çalışma kitabını yükleme, print area'yı ayarlama, `ImageOrPrintOptions` yapılandırma ve resmi kaydetme adımları, “nasıl” ve “neden” yönlerini kapsar ve kodu pivot tablolar, grafikler veya herhangi bir özel hücre bloğuna uyarlamanızı sağlar.

Sonraki adımda şunları keşfedebilirsiniz:

* **Excel aralığını görüntü olarak dışa aktarma** diğer formatlarda (SVG, BMP) – denemeniz için başka bir ikincil anahtar kelime.  
* **Aspose.PDF** kullanarak PNG'yi bir PDF'ye gömme – uçtan uca rapor üretimi için.  
* **Basit bir konsol döngüsüyle** birden çok çalışma kitabı arasında toplu dışa aktarmayı otomatikleştirme.

Farklı çözünürlükler, yönlendirmeler ve çıktı dizinleriyle denemeler yapmaktan çekinmeyin. Kodlamanın tadını çıkarın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren eksiksiz çalışan kod örnekleri sunar.

- [Aspose.Cells .NET Kullanarak Excel Hücrelerini Görüntü Olarak Dışa Aktarma: Adım Adım Kılavuz](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)
- [Aspose.Cells for Java Kullanarak Excel Çalışma Kitabını Görüntü Olarak Dışa Aktarma](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Aspose.Cells Java Kullanarak Excel Çalışma Sayfasını PNG Olarak Dışa Aktarma](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}