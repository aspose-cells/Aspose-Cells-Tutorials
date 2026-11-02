---
category: general
date: 2026-06-30
description: Aspose.Cells kullanarak bir Excel çalışma kitabında koşullu biçimlendirme
  oluşturun. Hücre arka planını nasıl ayarlayacağınızı, hücreleri nasıl sıralayacağınızı
  ve dosyayı programlı olarak nasıl oluşturacağınızı öğrenin.
draft: false
keywords:
- create conditional formatting
- create excel workbook
- set cell background
- how to rank cells
- how to use aspose
language: tr
og_description: Aspose.Cells kullanarak bir Excel çalışma kitabında koşullu biçimlendirme
  oluşturun. Hücre arka planını ayarlamak, hücreleri sıralamak ve Excel'i otomatikleştirmek
  için bu kapsamlı öğreticiyi izleyin.
og_title: Aspose.Cells ile Excel'de Koşullu Biçimlendirme Oluşturun
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create conditional formatting in an Excel workbook using Aspose.Cells.
    Learn how to set cell background, rank cells, and build the file programmatically.
  headline: Create Conditional Formatting in Excel with Aspose.Cells – Step‑by‑Step
    Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Aspose.Cells ile Excel'de Koşullu Biçimlendirme Oluşturma – Adım Adım Rehber
url: /tr/net/excel-conditional-formatting/create-conditional-formatting-in-excel-with-aspose-cells-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells ile Excel'de Koşullu Biçimlendirme Oluşturma – Adım Adım Kılavuz

Excel dosyasını UI'ı açmadan **koşullu biçimlendirme oluşturmayı** hiç merak ettiniz mi? Tek başınıza değilsiniz. Birçok geliştirici, **excel workbook** dosyalarını anında oluşturmak zorunda ve bunu programatik olarak yapmak saatler süren manuel işi tasarruf ettiriyor. Bu öğreticide **koşullu biçimlendirme oluşturmayı**, hücreleri stillendirmeyi ve en yüksek değerleri sıralamayı, .NET için güçlü Aspose.Cells kütüphanesiyle nasıl yapacağınızı göstereceğiz.

Gerçek bir senaryo üzerinden ilerleyeceğiz: bir puan tablosu oluşturma, yüksek puanları açık‑yeşil renkle vurgulama ve ilk‑3 performans sahibine altın arka plan uygulama. Sonunda **hücre arka planını nasıl ayarlayacağınızı**, **hücreleri nasıl sıralayacağınızı** ve **Aspose** ile gelişmiş Excel otomasyonu nasıl yapılacağını öğreneceksiniz. Gereksiz ayrıntı yok, doğrudan herhangi bir C# projesine ekleyebileceğiniz çalıştırılabilir bir çözüm.

## Öğrenecekleriniz

- Aspose.Cells kullanarak **excel workbook** oluşturma  
- Bir aralığı rastgele veri (puanlar) ile doldurma  
- **hücre arka planını** katı renklerle ayarlama  
- Formül tabanlı bir kural uygulayarak **hücreleri sıralama** ve en iyi üçü vurgulama  
- Sonucu .xlsx dosyası olarak kaydetme  

Önkoşullar: .NET 6+ (veya .NET Framework 4.6+), Visual Studio (veya herhangi bir C# IDE) ve Aspose.Cells NuGet paketine referans. Aspose ile hiç çalışmadıysanız endişelenmeyin—**Aspose nasıl kullanılır** konusunu sıfırdan ele alacağız.

---

![Create conditional formatting example](https://example.com/images/create-conditional-formatting.png "Koşullu biçimlendirmeyi gösteren ekran görüntüsü, oluşturulan Excel dosyasında")

*Image alt text: Aspose.Cells ile oluşturulmuş bir Excel çalışma kitabında koşullu biçimlendirme örneği.*

## Aspose.Cells ile Excel Workbook Nasıl Oluşturulur

İlk olarak bir workbook nesnesine ihtiyacınız var. Aspose.Cells bunu tek satırda halleder.

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Instantiate a new workbook and give the first sheet a friendly name
    Workbook workbook = new Workbook();                 // creates an empty workbook
    Worksheet sheet = workbook.Worksheets[0];           // grab the default worksheet
    sheet.Name = "Scores";                              // rename it to something meaningful
```

Sayfayı neden yeniden adlandırıyoruz? **Scores** gibi net bir ad, dosyayı teknik olmayan kullanıcılarla paylaştığınızda daha sonra referans almayı kolaylaştırır.  

Workbook oluşturulduğuna göre, A sütununu rastgele puanlarla dolduralım.

## Verileri Doldurma – Rastgele Puanlar Oluşturma

```csharp
    // Step 2: Populate A2:A21 with random values between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)               // 20 rows of data
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }
```

Kısa bir not: `PutValue` veri tipini otomatik algılar, bu yüzden `int`'e dönüştürmeye gerek yok. Döngü `i = 0`'dan başlar ancak satır `i + 1`'e yazar çünkü Excel satırları 1‑tabanlı iken `Cells` koleksiyonu 0‑tabanlıdır.

## Yüksek Puanlar İçin Hücre Arka Planı Nasıl Ayarlanır

Şimdi **koşullu biçimlendirme** oluşturacağız; 80 ve üzeri puanları açık‑yeşil bir renkle boyayacak.

```csharp
    // Step 3: Define a conditional formatting range (A2:A21)
    int firstRow = 1, lastRow = 20;                     // zero‑based indices for rows 2‑21
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];

    // Add a rule: cell value >= 80 → light‑green background
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");

    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;
```

`ForegroundColor` özelliği doldurma rengini kontrol eder, `Pattern = BackgroundType.Solid` ise Excel'e bir degrade veya desen yerine katı bir dolgu kullanmasını söyler. Bu, sayısal bir eşik değerine dayalı **hücre arka planını nasıl ayarlayacağınızın** temelidir.

## Hücreleri Sıralama ve İlk‑3'ü Vurgulama

Sıralama biraz daha karmaşık çünkü her hücreyi tüm aralığa karşı değerlendiren bir formüle ihtiyacımız var. Aspose.Cells, UI'da yazacağınız aynı Excel formül sözdizimini kullanmanıza izin verir.

```csharp
    // Step 4: Add a formula‑based rule to color the top‑3 scores gold
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);

    // The formula uses the RANK function; note the absolute references ($) lock the range
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";

    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;
```

Formülde neden `A2`? Aspose, formülü aralıktaki her hücreye göre göreceli olarak değerlendirir, bu yüzden `A2` otomatik olarak `A3`, `A4` vb. olarak kayar. `RANK` işlevi, bir değerin belirtilen aralıktaki konumunu döndürür ve `<=3` kısmı sadece en yüksek üç puanın altın dolgu almasını sağlar.

## Workbook Nasıl Kaydedilir

```csharp
    // Step 5: Persist the workbook to disk
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

`YOUR_DIRECTORY` kısmını uygulamanızın yazma izni olan mutlak ya da göreli bir yol ile değiştirin. Metodu çalıştırdıktan sonra dosyayı Excel'de açtığınızda şunları göreceksiniz:

- 80 ve üzeri puanlar için açık‑yeşil hücreler  
- En yüksek üç puan için altın hücreler, bu puanlar 80'in altında olsa bile  

Bu, **koşullu biçimlendirme oluşturma** sürecinin tam halidir.

---

## Tam, Çalıştırılabilir Örnek

Aşağıda tüm metodu tekrar paylaşıyoruz; bir console uygulamasına ya da herhangi bir C# sınıfına kopyalayıp yapıştırabilirsiniz:

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Create a new workbook and name the first worksheet
    Workbook workbook = new Workbook();
    Worksheet sheet = workbook.Worksheets[0];
    sheet.Name = "Scores";

    // Step 2: Fill column A (A2:A21) with random scores between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }

    // Step 3: Highlight scores >= 80 with a light‑green background
    int firstRow = 1, lastRow = 20;
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");
    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;

    // Step 4: Color the top‑3 scores with a gold background using a formula rule
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";
    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;

    // Step 5: Save the workbook
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

### Beklenen Sonuç

`Scores_ConditionalFormatting.xlsx` dosyasını açtığınızda:

- Değeri **80** veya daha yüksek olan hücreler açık‑yeşil parlar.  
- En yüksek üç sayı (80'in altında olsa bile) **altın** arka plan alır.  
- Diğer tüm hücreler varsayılan beyaz arka planı korur.

Bu görsel ipucu, bir yöneticinin en iyi performans gösterenleri manuel sıralama yapmadan hemen görmesini sağlar.

---

## Yaygın Sorular & Kenar Durumları

**Üçten fazla üst puan gerektiğinde ne yapmalıyım?**  
Formüldeki `<=3` kısmını `<=5` (veya istediğiniz herhangi bir sayı) olarak değiştirin. Kural otomatik olarak uyum sağlar.

**Birden fazla biçimlendirme aralığı uygulayabilir miyim?**  
Kesinlikle. `sheet.ConditionalFormattings.Add` metodunu farklı bir aralıkla tekrar çağırın, ardından yeni `ConditionalFormatting` nesnesine koşullar ekleyin.

**Eski Excel sürümleriyle ne olacak?**  
Aspose.Cells varsayılan olarak modern `.xlsx` formatında kaydeder; bu, Excel 2007 ve sonrası ile uyumludur. `.xls` gerekiyorsa `Save` metoduna `SaveFormat.Excel97To2003` parametresini geçin.

**Büyük sayfalarda performans etkisi var mı?**  
Koşullu biçimlendirme meta veri olarak saklanır, bu yüzden dosya boyutunu önemli ölçüde etkilemez. Ancak yüzbinlerce satır üretmek bellek kullanımını artırabilir—işlemi partiler halinde yapmayı düşünün.

---

## Sonraki Adımlar

Artık **koşullu biçimlendirme nasıl oluşturulur** konusunu kavradığınıza göre, aşağıdaki konuları keşfetmek isteyebilirsiniz:

- **Aspose.Cells ile programatik olarak Excel grafiklerini oluşturma** (başka bir değerli özellik)  
- **Metin değerlerine göre hücre arka planı ayarlama** (ör. “Geçti/Kaldı”)  
- **Aspose.Cells ile veri doğrulama ve açılır listeler**  

Bu konular, az önce öğrendikleriniz üzerine inşa edildiği için rahatlıkla adapte olabilirsiniz.

---

## Özet

Aspose.Cells kullanarak bir Excel çalışma kitabında **koşullu biçimlendirme oluşturma** sürecinin baştan sona tüm adımlarını gözden geçirdik. Workbook oluşturma, veri doldurma, **hücre arka planını ayarlama**, en iyi performans sahiplerini sıralama ve dosyayı kaydetme gibi adımları **hücreleri nasıl sıralayacağınız** ve **Aspose nasıl kullanılır** odaklarıyla ele aldık.  

Kodu deneyin, eşik değerlerini ayarlayın ve iş senaryolarınız için hızlıca şık raporlar üretin. Paylaşmak istediğiniz bir farklılık var mı? Aşağıya yorum bırakın—mutlu kodlamalar!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere yakın konuları kapsar ve aynı temeller üzerine inşa edilir. Her kaynak, adım adım açıklamalarla tam çalışan kod örnekleri içerir; böylece API özelliklerini daha da pekiştirebilir ve projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [Automate Excel Conditional Formatting Using Aspose.Cells for Java: A Complete Guide](/cells/english/java/formatting/automate-conditional-formatting-excel-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Create an Excel Workbook using Aspose.Cells in Java: A Step‑By‑Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}