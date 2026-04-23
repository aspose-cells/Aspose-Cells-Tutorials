---
category: general
date: 2026-02-26
description: Excel'de sayı biçimini hızlıca uygulayın ve sadece birkaç C# satırıyla
  bir sütunu para birimi olarak biçimlendirmeyi, sütun sayı biçimini ayarlamayı ve
  sütun yazı tipi rengini değiştirmeyi öğrenin.
draft: false
keywords:
- apply number format excel
- format column as currency
- set column number format
- format currency column
- set column font color
language: tr
og_description: Kolay adımlarla C#'ta Excel sayı formatı uygulayın. Sütunu para birimi
  olarak biçimlendirmeyi, sütun sayı formatını ayarlamayı ve profesyonel elektronik
  tablolar için sütun yazı tipi rengini ayarlamayı öğrenin.
og_title: Excel'de sayı biçimi uygulama – Sütun Stilinin Tam Rehberi
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: Excel'de Sayı Formatı Uygulama – Sütunları Biçimlendirme İçin Adım Adım Rehber
url: /tr/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# apply number format excel – C#'ta Excel Sütunlarını Nasıl Stilize Edersiniz

Hiç **apply number format excel**'i `DataTable` içinde dönerken nasıl yapacağınızı merak ettiniz mi? Tek başınıza değilsiniz. Çoğu geliştirici, aynı içe aktarma işleminde mavi‑yazı başlık *ve* para birimi‑stilinde bir sütun gerektiğinde bir engelle karşılaşır. İyi haber? Birkaç C# satırı ve doğru stil nesneleriyle, sayfayı sonradan işleme almadan bunu yapabilirsiniz.

Bu öğreticide, **format column as currency**, **set column number format** ve hatta başlıklar için **set column font color** nasıl yapılır gösteren eksiksiz, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz. Sonunda, herhangi bir Aspose.Cells (veya benzeri) projesine ekleyebileceğiniz yeniden kullanılabilir bir desen elde edeceksiniz.

## Öğrenecekleriniz

- `DataTable`'ı nasıl alacağınızı ve her sütunu belirli bir `Style` ile nasıl eşleyeceğinizi.
- `Worksheet.Cells.ImportDataTable` kullanarak **apply number format excel**'i nasıl yapacağınızı gösteren tam adımlar.
- Stilleri önceden oluşturmanın, hücreleri tek tek biçimlendirmeye göre neden daha verimli olduğunu.
- Kaynak tablonun stil verilen sütunlardan daha fazla sütunu olduğunda kenar‑durum yönetimi.
- Bugün çalıştırabileceğiniz tam, kopyala‑yapıştır‑hazır kod örneği.

> **Prerequisite:** Bu kılavuz, projenizde Aspose.Cells for .NET (veya `Workbook`, `Worksheet`, `Style` API'lerini sunan herhangi bir kütüphane) referansının olduğunu varsayar. Farklı bir kütüphane kullanıyorsanız, kavramlar doğrudan uygulanabilir—sadece tip adlarını değiştirin.

---

## Adım 1: Kaynak Veriyi DataTable Olarak Alın

Herhangi bir stil uygulanmadan önce ham veriye ihtiyacınız var. Çoğu gerçek dünyada senaryoda veri bir veritabanı, CSV veya bir API'de bulunur. Açıklık olması için iki sütunlu basit bir `DataTable` taklit edeceğiz: *Product* (string) ve *Price* (decimal).

```csharp
using System;
using System.Data;
using Aspose.Cells;
using System.Drawing;

public static DataTable GetData()
{
    var dt = new DataTable();
    dt.Columns.Add("Product", typeof(string));
    dt.Columns.Add("Price", typeof(decimal));

    dt.Rows.Add("Apple", 1.25m);
    dt.Rows.Add("Banana", 0.75m);
    dt.Rows.Add("Cherry", 2.10m);

    return dt;
}
```

> **Why this matters:** Veriyi bir `DataTable`'a çekmek, `ImportDataTable`'ın doğrudan tüketebileceği tablo‑şeklinde, bellek‑içi bir temsil sağlar ve manuel hücre‑hücre ekleme ihtiyacını ortadan kaldırır.

## Adım 2: Stil Dizisi Oluşturun – Her Sütun İçin Bir Tanesi

`ImportDataTable` aşırı yüklemesi, bir `Style` nesnesi dizisi alır. Her giriş bir sütun indeksine karşılık gelir. Bir girişi `null` bırakırsanız, sütun varsayılan çalışma kitabı stilini devralır.

```csharp
// Initialize the workbook (Aspose.Cells)
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Prepare the style array based on the number of columns
DataTable dataTable = GetData();
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

> **Pro tip:** Diziyi `DataTable`'ı aldıktan *sonra* bildirmeniz, boyutun tam olarak eşleşmesini sağlar ve daha sonra `IndexOutOfRangeException` oluşmasını önler.

## Adım 3: İlk Sütun İçin Sütun Yazı Rengini (Mavi) Ayarlayın

Yaygın bir istek, başlık veya ana sütunları belirgin bir yazı rengiyle vurgulamaktır. Burada ilk sütunun metnini mavi yapıyoruz.

```csharp
// Style for the first column – blue font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = Color.Blue;
```

> **Why use a style object?** Stiller yeniden kullanılabilir ve toplu olarak uygulanır, bu da içe aktarmadan sonra her hücreyi döndürmekten çok daha hızlıdır. Çalışma kitabı stili bir kez önbelleğe alır, ardından o sütundaki her hücre için tekrar kullanır.

## Adım 4: İkinci Sütunu Para Birimi Olarak Biçimlendirin

Excel'in yerleşik sayı formatları bir indeks ile tanımlanır. `14` varsayılan para birimi formatına (ör. `$1,234.00`) karşılık gelir. Özel bir format gerekiyorsa, bunun yerine bir format dizesi atayabilirsiniz.

```csharp
// Style for the second column – built‑in currency format (ID 14)
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].Number = 14; // 14 = built‑in currency format
```

> **Edge case:** Çalışma kitabınızın para birimi simgesi `$` olmayan bir yerel ayarı varsa, aynı indeks otomatik olarak uyum sağlar (ör. Almanya yerel ayarı için `€`).

## Adım 5: Tanımlı Stillerle DataTable'ı İçe Aktarın

Şimdi her şeyi bir araya getiriyoruz. `ImportDataTable` yöntemi, veriyi `A1` hücresinden (satır 0, sütun 0) başlayarak yapıştıracak ve hazırladığımız stilleri uygulayacaktır.

```csharp
// Import the DataTable into the worksheet, applying the column styles
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

- İkinci parametre `true`, Aspose.Cells'e `DataTable`'ın ilk satırını sütun başlıkları olarak ele almasını söyler.
- `0, 0` koordinatları, içe aktarmanın başladığı sol‑üst köşeyi belirtir.
- `columnStyles`, her sütunu ilgili stiline eşler.

## Adım 6: Çalışma Kitabını Kaydedin (İsteğe Bağlı, Ancak Doğrulama İçin Kullanışlı)

Sonucu Excel'de görmek istiyorsanız, çalışma kitabını diske kaydedin. Bu adım stil mantığı için gerekli değildir, ancak hata ayıklama için faydalıdır.

```csharp
// Save the workbook to a file
workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved as StyledReport.xlsx");
```

### Beklenen Çıktı

| **Product** (mavi yazı) | **Price** (para birimi) |
|--------------------------|--------------------------|
| Apple                    | $1.25                    |
| Banana                   | $0.75                    |
| Cherry                   | $2.10                    |

- *Product* sütunu mavi görünür, böylece öne çıkar.
- *Price* sütunu varsayılan para birimi simgesi ve iki ondalık basamakla değerleri gösterir.

---

## Sık Sorulan Sorular & Varyasyonlar

### Birden fazla iki sütun için **set column number format** nasıl yapılır?

`columnStyles` dizisini genişletmeniz yeterlidir. Örneğin, üçüncü sütunda yüzde göstermek için:

```csharp
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Number = 10; // 10 = built‑in percentage format
```

### *custom* bir para birimi formatına ihtiyacım olsaydı, örneğin “USD 1,234.00”?

`Number` özelliğini bir format dizesiyle değiştirin:

```csharp
columnStyles[1].Custom = "\"USD\" #,##0.00";
```

### Sayısal bir sütuna **set column font color** uygulayıp sayı formatını etkilemeden yapabilir miyim?

Kesinlikle. Stiller birleştirilebilir. Aynı `Style` örneğinde hem `Font.Color` hem de `Number` ayarlayabilirsiniz:

```csharp
columnStyles[3] = workbook.CreateStyle();
columnStyles[3].Font.Color = Color.Green;
columnStyles[3].Number = 2; // 2 = built‑in date format (just an example)
```

### `DataTable`'ın stil sayısından daha fazla sütunu olursa ne olur?

Açık bir stili (`null` giriş) olmayan herhangi bir sütun, çalışma kitabının varsayılan stilini devralır. Kazara `null` oluşmasını önlemek için, tüm diziyi önce bir temel stil ile başlatabilirsiniz:

```csharp
Style defaultStyle = workbook.CreateStyle();
defaultStyle.Font.Size = 11;
for (int i = 0; i < columnStyles.Length; i++)
    columnStyles[i] = defaultStyle;
```

Ardından sadece ilgilendiğiniz sütunları geçersiz kılın.

### Bu yaklaşım büyük veri setleri (10k+ satır) ile çalışır mı?

Evet. Stil, içe aktarmadan önce *her sütun için bir kez* uygulanabildiğinden, işlem satır sayısına göre O(N) kalır ve bellek kullanımı düşük olur. İçe aktarmadan sonra her hücreyi döngüye sokmaktan kaçının—performansın düşmeye başladığı yerdir.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```csharp
using System;
using System.Data;
using System.Drawing;
using Aspose.Cells;

class ExcelStyler
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 3️⃣ Prepare style array (one per column)
        Style[] columnStyles = new Style[dataTable.Columns.Count];

        // 4️⃣ Style first column – blue font
        columnStyles[0] = workbook.CreateStyle();
        columnStyles[0].Font.Color = Color.Blue;

        // 5️⃣ Style second column – built‑in currency format (ID 14)
        columnStyles[1] = workbook.CreateStyle();
        columnStyles[1].Number = 14;

        // 6️⃣ (Optional) Add more styles here – e.g., percentage, custom formats

        // 7️⃣ Import the DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // 8️⃣ Save to file for verification
        workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
        Console.WriteLine("Excel file created: StyledReport.xlsx");
    }

    // Helper method to mock data
    public static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Price", typeof(decimal));

        dt.Rows.Add("Apple", 1.25m);
        dt.Rows.Add("Banana", 0.75m);
        dt.Rows.Add("Cherry", 2.10m);
        return dt;
    }
}
```

Programı çalıştırın, `StyledReport.xlsx` dosyasını açın ve **apply number format excel** sonucunu anında göreceksiniz.

## Sonuç

İçe aktarılan bir `DataTable`'a **apply number format excel** uygulamanın temiz ve verimli bir yolunu gösterdik. Önceden bir `Style[]` dizisi hazırlayarak, tek bir çağrıda **format column as currency**, **set column number format** ve **set column font color** yapabilirsiniz—sonradan işleme gerek yok.

Deseni genişletmekten çekinmeyin: koşullu stil ekleyin, başlıklar için hücreleri birleştirin veya formüller ekleyin. Aynı prensipler geçerlidir, kodunuzu düzenli tutar ve elektronik tablolarınızın profesyonel görünmesini sağlar.

### Sıradaki Adımlar?

- **conditional formatting**'i keşfedin ve eşik değeri aşan değerleri vurgulayın.
- Bu tekniği **pivot table generation** ile birleştirerek dinamik raporlama yapın.
- Tarih, yüzde veya özel bilimsel gösterim için **setting column number format**'ı deneyin.

Denediğiniz bir değişiklik mi var? Yorumlarda paylaşın—devam edelim.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}