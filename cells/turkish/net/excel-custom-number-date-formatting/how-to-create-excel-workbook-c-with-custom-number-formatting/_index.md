---
category: general
date: 2026-10-01
description: Excel çalışma kitabını C# ile nasıl oluşturacağınızı, özel sayı biçimi
  uygulamayı, hücre ondalık basamaklarını ayarlamayı ve çalışma kitabını XLSX olarak
  kaydetmeyi adım adım eksiksiz bir rehberde öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- apply custom number format
- how to format numbers excel
- set cell decimal places
- save workbook as xlsx
language: tr
lastmod: 2026-10-01
og_description: C# ile özel sayı formatı kullanarak bir Excel çalışma kitabı oluşturun,
  hücre ondalık basamaklarını ayarlayın ve çalışma kitabını XLSX olarak kaydedin.
  Kesin sayısal çıktı için bu kapsamlı rehberi izleyin.
og_image_alt: Screenshot of an Excel sheet showing numbers rounded to four significant
  digits
og_title: C# ile Excel çalışma kitabı oluşturma – özel sayı formatı ve XLSX dışa aktarımı
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  headline: How to create Excel workbook C# with custom number formatting
  type: TechArticle
- description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  name: How to create Excel workbook C# with custom number formatting
  steps:
  - name: Run the program (`dotnet run`).
    text: Run the program (`dotnet run`).
  - name: Open `SigDigits.xlsx`.
    text: Open `SigDigits.xlsx`.
  - name: Confirm that **A1** reads `123.5`.
    text: Confirm that **A1** reads `123.5`.
  - name: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
    text: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: C# ile Özel Sayı Biçimlendirmeli Excel Çalışma Kitabı Nasıl Oluşturulur
url: /tr/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-c-with-custom-number-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel çalışma kitabı C# ile özel sayı biçimlendirme nasıl oluşturulur

Eğer **create excel workbook c#** ihtiyacınız varsa ve sayıları tam istediğiniz gibi göstermek istiyorsanız, bu rehber birkaç net adımda nasıl yapacağınızı gösterir. Özel bir sayı biçimi uygulamayı, hücre ondalık basamaklarını ayarlamayı ve sonunda **save workbook as xlsx** işlemini öğrenerek veriyi sonraki aşamalara hazır hâle getireceksiniz.

Sayısal verilerle çalışmak genellikle hassasiyet ile okunabilirlik arasında bir denge kurmayı gerektirir. Bu öğreticinin sonunda, görüntülenen basamakları belirli bir anlamlı basamak sayısıyla sınırlayan ve dosyada orijinal değeri koruyan yeniden kullanılabilir bir deseniniz olacak. Harici betikler gerekmez—sadece C# ve Aspose.Cells kütüphanesi yeterlidir.

## Prerequisites

Başlamadan önce şunların yüklü olduğundan emin olun:

* .NET 6.0 SDK veya daha yeni bir sürüm  
* Visual Studio 2022 (veya herhangi bir C# IDE)  
* **Aspose.Cells for .NET** NuGet paketi (`Install-Package Aspose.Cells`) – bu kütüphane örneklerde kullanılan `Workbook`, `Worksheet` ve `ExportTableOptions` sınıflarını sağlar.  

Bu gereksinimler minimum düzeydedir; aynı kod .NET Core, .NET Framework ve hatta Azure Functions içinde de çalışır.

## Step 1: Create Excel workbook C# – initialize the file

İlk işlem, yeni bir `Workbook` nesnesi oluşturmak. Bu nesne bellekte tüm Excel dosyasını temsil eder ve otomatik olarak bir varsayılan çalışma sayfası içerir.

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();               // creates an empty .xlsx container
            Worksheet sheet = workbook.Worksheets[0];         // reference to the default sheet
```

**Why this matters:**  
Çalışma kitabını önceden oluşturmak size temiz bir tuval sağlar. Varsayılan çalışma sayfası (`Worksheets[0]`) veri girişi için hazırdır; senaryonuz birden fazla sekme gerektirmedikçe yeni bir sayfa eklemenize gerek kalmaz.

## Step 2: Write a numeric value to a cell

Şimdi örnek bir sayıyı **A1** hücresine yerleştirin. Kullanacağımız değer (`123.456789`) görüntülemek istediğimizden daha fazla ondalık basamağa sahiptir; bu sayede daha sonra yuvarlamayı gösterebiliriz.

```csharp
            // Step 2: Write a numeric value to cell A1
            sheet.Cells[0, 0].PutValue(123.456789); // row 0, column 0 = A1
```

**Tip:** `PutValue` veri tipini otomatik algılar, bu yüzden sayıyı string’e dönüştürmek zorunda kalmazsınız.

## Step 3: Apply custom number format – limit visible decimals

Excel’in sayıyı nasıl göstereceğini kontrol etmek için **custom number format** içeren bir `Style` oluştururuz. `"0.######"` deseni, Excel’e en fazla altı ondalık basamak göster, ancak sondaki sıfırları atla, der.

```csharp
            // Step 3: Define a custom number format (up to 6 decimal places) and apply it
            Style customStyle = workbook.CreateStyle();
            customStyle.Custom = "0.######";               // up to 6 decimals, no trailing zeros
            sheet.Cells[0, 0].SetStyle(customStyle);
```

**How this works:**  
Biçim dizesi, Excel’in özel‑biçim sözdizimini izler. `0` bir rakamı zorunlu kılar, `#` ise yalnızca anlamlı olduğunda rakam gösterir. Bu iki karakteri birleştirerek, orijinal hassasiyeti koruyan esnek bir görüntü elde edersiniz.

## Step 4: Set cell decimal places – using ExportTableOptions

**set cell decimal places** ihtiyacınız varsa (ör. bir DataTable’a dönüştürürken), Aspose.Cells size **significant digits** sayısını belirleme imkanı tanır. Bu adım, dışa aktarılan CSV veya DataTable’ın çalışma kitabında uyguladığınız aynı yuvarlama kurallarına uymasını sağlar.

```csharp
            // Step 4: Configure export options to limit the output to 4 significant digits
            ExportTableOptions exportOptions = new ExportTableOptions();
            exportOptions.SignificantDigits = 4;           // round to 4 significant figures
```

**Why use `SignificantDigits`?**  
Sabit bir ondalık sayısı yerine, anlamlı basamaklar sayıyı ölçeğini korurken hassasiyeti sınırlar; bu da analistlerin veri özetlerinde sıkça beklediği davranıştır.

## Step 5: Export the worksheet data and **save workbook as xlsx**

Son olarak, veriyi dışa aktarın (eğer bir DataTable’a ihtiyacınız varsa) ve çalışma kitabını diske kaydedin. `ExportDataTable` çağrısı yapılandırdığımız `ExportTableOptions` ayarlarını dikkate alır, `workbook.Save` ise standart bir XLSX dosyası yazar.

```csharp
            // Step 5: Export the worksheet data using the configured options and save the workbook
            sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
            workbook.Save("SigDigits.xlsx");               // saves to the application’s working folder
        }
    }
}
```

**Expected result:**  
*SigDigits.xlsx* dosyasını Excel’de açtığınızda **A1** hücresi `123.5` gösterir. Altındaki gerçek değer hâlâ `123.456789` olur, ancak gösterilen sayı 4‑anlamlı‑basamak kuralına uyar. Sayfayı bir DataTable’a dışa aktarırsanız, tabloda da değer `123.5` olarak yuvarlanmış olur.

---

## Apply custom number format to additional cells

Bir tek hücre yerine bir aralığı biçimlendirmeniz gerekiyorsa, `Style` nesnesini yeniden kullanın:

```csharp
// Apply the same custom style to B2:C5
Range range = sheet.Cells.CreateRange("B2:C5");
range.ApplyStyle(customStyle, new StyleFlag { NumberFormat = true });
```

**Pro tip:** Stil nesnesini yeniden kullanmak bellek yükünü azaltır ve sayfa genelinde tutarlı biçimlendirme garantiler.

## How to format numbers Excel using C# – common variations

| Scenario | Format string | Result |
|----------|---------------|--------|
| İki ondalık basamak sabit | `"0.00"` | `123.46` |
| Para birimi (ABD) | `"$#,##0.00"` | `$123.46` |
| Bir ondalık basamaklı yüzde | `"0.0%"` | `12,346.0%` |
| Bilimsel gösterim | `"0.00E+00"` | `1.23E+02` |

Raporlama gereksinimlerinize uygun deseni seçin. Tüm desenler, daha önce gösterilen `Style.Custom` özelliğiyle uyumludur.

## Set cell decimal places dynamically based on user input

Bazen gereken hassasiyet derleme zamanında bilinmez. Biçim dizesini çalışma zamanında oluşturabilirsiniz:

```csharp
int decimals = 3; // could come from a UI textbox
string format = "0." + new string('#', decimals);
customStyle.Custom = format;
sheet.Cells["A2"].PutValue(987.654321);
sheet.Cells["A2"].SetStyle(customStyle);
```

**Köşe durumu:** `decimals` sıfır ise, format `"0"` (tam sayı gösterimi) olur. Kötü biçimlendirilmiş dize oluşmasını önlemek için kullanıcı girdisini daima doğrulayın.

## Save workbook as XLSX – best practices

* **Mutlak yollar** kullanın; bilinen bir klasöre yazarken (`Path.Combine(Environment.CurrentDirectory, "output.xlsx")`).  
* `Workbook` nesnesini bir `using` ifadesi içinde sararak **Dispose** edin; böylece yönetilmeyen kaynaklar hızlıca serbest bırakılır:

```csharp
using (Workbook wb = new Workbook())
{
    // ...populate workbook...
    wb.Save(Path.Combine(@"C:\Exports", "Report.xlsx"));
}
```

* **Sürüm uyumluluğu:** Aspose.Cells, Excel 2010‑2023 ile uyumlu dosyalar yazar; bu sayede downstream kullanıcılar format sorunlarıyla karşılaşmaz.

---

## Full working example

Aşağıda, hemen kopyalayıp çalıştırabileceğiniz tam program yer alıyor. Gerekli tüm `using` yönergeleri, yorumlar ve hata yönetimi dahildir.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // 1️⃣ Create workbook and get the first worksheet
                Workbook workbook = new Workbook();
                Worksheet sheet = workbook.Worksheets[0];

                // 2️⃣ Write a high‑precision number to A1
                sheet.Cells[0, 0].PutValue(123.456789);

                // 3️⃣ Apply a custom number format (up to 6 decimals)
                Style customStyle = workbook.CreateStyle();
                customStyle.Custom = "0.######";
                sheet.Cells[0, 0].SetStyle(customStyle);

                // 4️⃣ Configure export options for 4 significant digits
                ExportTableOptions exportOptions = new ExportTableOptions
                {
                    SignificantDigits = 4
                };

                // 5️⃣ Export data (optional) and save the workbook as XLSX
                sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
                string outputPath = Path.Combine(Environment.CurrentDirectory, "SigDigits.xlsx");
                workbook.Save(outputPath);

                Console.WriteLine($"Workbook saved successfully at: {outputPath}");
                Console.WriteLine("Cell A1 displays: " + sheet.Cells["A1"].StringValue);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error creating workbook: {ex.Message}");
            }
        }
    }
}
```

**Verification steps**

1. Programı çalıştırın (`dotnet run`).  
2. `SigDigits.xlsx` dosyasını açın.  
3. **A1** hücresinin `123.5` gösterdiğini doğrulayın.  
4. Dosyanın XML’ini (`.xlsx` bir zip arşividir) açarsanız, `<c>` elemanının `s` özniteliğinde `"0.######"` özel formatının saklandığını göreceksiniz.

---

## Conclusion

Bu öğreticide **create excel workbook c#**, **apply custom number format**, **set cell decimal places** ve **save workbook as xlsx** işlemlerini Aspose.Cells kullanarak nasıl yapacağınızı öğrendiniz. Çözüm, Excel içinde görsel biçimlendirmeyi ve `ExportTableOptions` aracılığıyla veri dışa aktarımında yuvarlamayı bir arada gösterir.

Bundan sonra şunları yapabilirsiniz:

* Yaklaşımı tüm aralıklar veya tablolar için genişletin.  
* `StyleFlag` ile birden fazla stili (yazı tipleri, kenarlıklar) birleştirin.  
* Veri kaynakları üzerinde döngü kurarak aynı biçimlendirme mantığını uygulayan rapor otomasyonu oluşturun.  

Farklı format dizeleri, ondalık sayıları veya dışa aktarım seçenekleriyle deneyler yaparak kendi raporlama ihtiyaçlarınıza en uygun çözümü bulun. İyi kodlamalar!


## What Should You Learn Next?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve ilgili konuları derinlemesine ele alan içeriklerdir. Her biri, adım adım açıklamalar ve tam çalışan kod örnekleri sunar; böylece API özelliklerini daha iyi kavrayabilir ve projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Create Excel Workbook C# – Step‑by‑Step Guide with Conditional Formatting](/cells/english/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/)
- [Create Excel Workbook C# – Add Comment & Save as XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}