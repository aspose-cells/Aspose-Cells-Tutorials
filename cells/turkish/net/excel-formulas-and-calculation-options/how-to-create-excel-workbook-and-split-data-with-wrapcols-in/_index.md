---
category: general
date: 2026-10-10
description: C#'ta Excel çalışma kitabı oluşturun ve dizi verilerini sütunlara bölmek
  için WRAPCOLS işlevini kullanın. Çalıştırılabilir kod içeren eksiksiz bir adım‑adım
  kılavuzu izleyin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- excel formula split data
- use wrapcols function
- how to use wrapcols
- split array columns
language: tr
lastmod: 2026-10-10
og_description: C# ile Excel çalışma kitabı oluşturun ve dizi verilerini sütunlara
  bölmek için WRAPCOLS işlevini uygulayın. Bu rehber tam kodu gösterir ve her adımı
  açıklar.
og_image_alt: Screenshot of an Excel sheet showing three columns filled by the WRAPCOLS
  formula
og_title: C#'ta Excel çalışma kitabı oluşturun ve WRAPCOLS ile verileri bölün
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  headline: How to create Excel workbook and split data with WRAPCOLS in C#
  type: TechArticle
- description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  name: How to create Excel workbook and split data with WRAPCOLS in C#
  steps:
  - name: Using the function with different data types
    text: 'The `WRAPCOLS` function is not limited to numbers. You can split text values,
      dates, or mixed types:'
  - name: Variable column count at runtime
    text: 'Often the number of columns you need depends on user input. You can build
      the formula string dynamically:'
  - name: Large arrays and performance
    text: '`WRAPCOLS` can handle thousands of elements, but evaluating extremely large
      arrays in a single cell may increase calculation time. If you notice slowdown:'
  - name: Handling empty cells
    text: If the source array contains empty strings (`""`) or `NULL` values, `WRAPCOLS`
      inserts blank cells, preserving the column layout. This behavior is useful when
      you need placeholder columns for later data entry.
  - name: Using named ranges instead of literals
    text: 'For maintainability, define a named range that holds the source data, then
      reference it:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: C#'ta Excel çalışma kitabı oluşturma ve WRAPCOLS ile verileri bölme
url: /tr/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-and-split-data-with-wrapcols-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel çalışma kitabı oluşturma ve WRAPCOLS ile veriyi bölme C#'ta

Programmatically **Excel çalışma kitabı oluşturmanız** gerekiyorsa, bu kılavuz tam olarak nasıl yapacağınızı ve `WRAPCOLS` işlevini kullanarak **dizi verisini** sütunlar arasında nasıl **bölümlendireceğinizi** gösterir. Üç sütuna dağıtılmış verilerle bir `.xlsx` dosyası üreten tam, çalıştırılabilir bir örnek elde edeceksiniz.

Bu öğretici ihtiyacınız olan her şeyi kapsar: gerekli NuGet paketleri, kodun her satırı, `WRAPCOLS` formülünün neden çalıştığı ve çözümü farklı dizi boyutları veya sütun sayıları için nasıl uyarlayacağınız. Sonunda, Excel dosyaları üreten herhangi bir C# projesine **use wrapcols function** tekniğini gömebileceksiniz.

## Önkoşullar

* .NET 6.0 SDK veya daha yeni bir sürüm yüklü  
* Bir C# IDE'si (Visual Studio, VS Code, Rider, vb.)  
* **Aspose.Cells for .NET** NuGet paketi – örneklerde kullanılan `Workbook` sınıfını sağlayan kütüphane  

Office kurulumu gerekmiyor; Aspose.Cells `.xlsx` dosyasını doğrudan yazar.

## 1. Adım – Excel çalışma kitabı oluşturma

İlk görev, yeni bir workbook nesnesi oluşturmak ve ilk worksheet'e bir referans almaktır. Bu adım, sonraki tüm manipülasyonların temelini oluşturur.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();                // creates an empty Excel file in memory
        Worksheet ws = wb.Worksheets[0];             // the default worksheet is at index 0
```

`Workbook` tüm dosyayı temsil eder, `Worksheet` ise tek bir sayfayı temsil eder. Workbook'u bellek içinde oluşturduğunuzda, açıkça kaydedene kadar disk I/O'dan kaçınırsınız.

## 2. Adım – WRAPCOLS'u uygulayarak dizi sütunlarını bölme

Şimdi **A1** hücresine `WRAPCOLS` kullanan bir formül yerleştireceksiniz. Fonksiyon iki argüman alır: kaynak dizi ve dizinin sarmalanmasını istediğiniz sütun sayısı.

```csharp
        // Step 2: Apply the WRAPCOLS formula to split the array into 3 columns
        // The array {1,2,3,4,5,6} will be distributed as:
        // 1 2 3
        // 4 5 6
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

**Neden çalışır:** `WRAPCOLS`, düz dizi `{1,2,3,4,5,6}`'yı alır ve worksheet'i satır satır doldurarak her satırda üç sütun oluşturur. İlk argüman herhangi bir Excel dizi literalı, adlandırılmış bir aralık veya dinamik dizi formülü olabilir. İkinci argüman (`3`) Excel'e bir sonraki satıra geçmeden önce kaç sütun oluşturacağını söyler.

### Farklı veri tipleriyle fonksiyonu kullanma

`WRAPCOLS` fonksiyonu sadece sayılarla sınırlı değildir. Metin değerlerini, tarihleri veya karışık tipleri bölüştürebilirsiniz:

```csharp
        // Example with mixed data: strings and numbers
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";
```

Kaynak dizi stringler içerdiğinde, Excel sonucu otomatik olarak metin hücreleri olarak işler. Bu esneklik, **excel formula split data**'yi raporlama, gösterge panoları veya veri‑göçü görevleri için kullanmanıza olanak tanır.

## 3. Adım – Formülleri hesaplayarak worksheet'in doldurulması

Formüller, workbook'tan değerlendirilmesi istenene kadar string olarak saklanır. `CalculateFormula` çağrısı değerlendirmeyi zorlar ve sonuçları hücrelere yazar.

```csharp
        // Step 3: Calculate formulas so the worksheet is populated
        wb.CalculateFormula();   // evaluates all formulas in the workbook
```

Bu çağrı olmadan kaydedilen dosya sadece formül metnini içerir, hesaplanmış değerleri değil. Metot tüm workbook'ta çalışır, böylece başka yerlere ek formüller koyabilir ve hepsi tek bir çağrıyla çözülür.

## 4. Adım – Sonucu görmek için workbook'u kaydetme

Son olarak, workbook'u diske yazın. Yazma izniniz olan bir klasör seçin ve dosyaya açık bir isim verin.

```csharp
        // Step 4: Save the workbook to see the result
        string outputPath = @"output.xlsx";
        wb.Save(outputPath);      // creates output.xlsx in the application directory
    }
}
```

`output.xlsx` dosyasını Excel'de (veya uyumlu bir görüntüleyicide) açtığınızda şunları göreceksiniz:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

Karışık‑tip örneğini kullandıysanız, 3‑4. satırlar ilgili metin ve sayıları içerecektir.

## Gelişmiş varyasyonlar ve kenar‑durum yönetimi

### Çalışma zamanında değişken sütun sayısı

Sıklıkla ihtiyaç duyduğunuz sütun sayısı kullanıcı girdisine bağlıdır. Formül dizesini dinamik olarak oluşturabilirsiniz:

```csharp
int columns = 4; // could come from UI, config, etc.
string arrayLiteral = "{10,20,30,40,50,60,70,80}";
ws.Cells[5, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
```

### Büyük diziler ve performans

`WRAPCOLS` binlerce öğeyi işleyebilir, ancak tek bir hücrede çok büyük dizileri değerlendirmek hesaplama süresini artırabilir. Yavaşlama fark ederseniz:

* Kaynak diziyi daha küçük parçalara bölün ve her parçayı ayrı bir başlangıç hücresine yazın.  
* `WorkbookSettings` kullanarak çok‑iş parçacıklı hesaplamayı etkinleştirin:

```csharp
wb.Settings.CalcMode = CalculationModeType.Automatic;
wb.Settings.EnableMultiThreadedCalc = true;
```

### Boş hücreleri işleme

Kaynak dizi boş stringler (`""`) veya `NULL` değerler içeriyorsa, `WRAPCOLS` boş hücreler ekler ve sütun düzenini korur. Bu davranış, daha sonraki veri girişi için yer tutucu sütunlara ihtiyaç duyduğunuzda faydalıdır.

### Literallar yerine adlandırılmış aralıklar kullanma

Bakım kolaylığı için, kaynak veriyi tutan bir adlandırılmış aralık tanımlayın ve ardından ona referans verin:

```csharp
ws.Cells["D1:D6"].PutValue(new object[] { 11, 12, 13, 14, 15, 16 });
ws.Cells["E1"].Formula = "=WRAPCOLS(D1:D6,3)";
```

Artık formül, verileri doğrudan worksheet'ten okur ve dinamik raporlama senaryolarında **how to use wrapcols**'ı etkinleştirir.

## Yaygın tuzaklar ve profesyonel ipuçları

* **İkinci argümanı atlamayın.** Sütun sayısı olmadan `WRAPCOLS(array)` tek bir sütun döndürür, bu da veriyi bölme amacını boşa çıkarır.  
* **Dizi boyutlarını karıştırmayın.** Kaynak dizi tek‑boyutlu olmalıdır; iki‑boyutlu bir dizi (ör. `{ {1,2},{3,4} }`) sağlamak `#VALUE!` hatasına yol açar.  
* **Hesaplamadan sonra kaydedin.** `CalculateFormula`'dan önce `wb.Save` çağırırsanız dosya sadece formül metnini içerir.  
* **Dosya izinlerini kontrol edin.** Kısıtlı ortamlarda (ör. ASP.NET) çalışırken, işlem kimliğinin hedef klasöre yazma izni olduğundan emin olun.

## Tam çalışan örnek

Aşağıda kopyalayıp yapıştırıp çalıştırabileceğiniz tam program yer alıyor. Tüm importları, hata yönetimini ve yorumları içerir.

```csharp
using System;
using Aspose.Cells;

class ExcelWrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Split a numeric array into 3 columns
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";

        // Split a mixed array (text + numbers) into 3 columns, starting at row 3
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";

        // Dynamically build a formula with a variable column count
        int columnCount = 4;
        string sourceArray = "{10,20,30,40,50,60,70,80}";
        ws.Cells[5, 0].Formula = $"=WRAPCOLS({sourceArray},{columnCount})";

        // Evaluate all formulas
        wb.CalculateFormula();

        // Save the workbook
        string outputPath = "output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Programı çalıştırdığınızda `output.xlsx` dosyası, `WRAPCOLS` işlevi kullanılarak **excel formula split data**'yi gösteren üç ayrı bölge üretir.

## Sonuç

Artık C#'ta **Excel çalışma kitabı** dosyaları oluşturmayı ve **use wrapcols function**'ı kullanarak **dizi sütunlarını** verimli bir şekilde **bölmeyi** biliyorsunuz. Temel adımlar—`Workbook`'u örneklemek, `WRAPCOLS` formülünü eklemek, hesaplamak ve kaydetmek—sütunlar arasında veri dağıtımı gerektiren her otomasyon görevi için yeniden kullanılabilir bir desen oluşturur.

Buradan itibaren şunları yapabilirsiniz:

* `WRAPCOLS`'u `FILTER` veya `SORT` gibi diğer dinamik‑dizi işlevleriyle birleştirin.  
* Veritabanlarından büyük veri setlerini dışa aktarın ve Excel'in düzeni otomatik olarak yönetmesine izin verin.  
* Sütun sayısının bir UI kontrolü aracılığıyla seçildiği kullanıcı‑odaklı raporlar oluşturun.

Farklı dizi kaynakları, sütun sayıları ve ek formüllerle deney yaparak bu temeli genişletin. Kodlamanın tadını çıkarın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [C#'ta WRAPCOLS Kullanımı – Wrap Fonksiyonlarıyla Excel Çalışma Kitabı Oluşturma](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Excel Çalışma Kitabı Oluştur – WRAPCOLS ile Diziyi Matrise Dönüştür](/cells/english/net/calculation-engine/create-excel-workbook-convert-array-to-matrix-with-wrapcols/)
- [Excel Çalışma Kitabı C# – Adım Adım Kılavuz](/cells/english/net/excel-workbook/create-excel-workbook-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}