---
category: general
date: 2026-03-30
description: C# ile para birimi biçimlendirmeli bir Excel çalışma kitabı oluşturun.
  Bir DataTable'ı nasıl içe aktaracağınızı, Excel'de sayı biçimi eklemeyi ve dakikalar
  içinde para birimi biçimlendirmeli bir sütun uygulamayı öğrenin.
draft: false
keywords:
- create excel workbook c#
- format cells currency
- import datatable to excel
- add number format excel
- apply currency format column
language: tr
og_description: C# ile Excel çalışma kitabı oluşturun ve hücreleri anında para birimi
  olarak biçimlendirin. Bu adım adım öğretici, bir DataTable'ı Excel'e nasıl içe aktaracağınızı
  ve bir sütun için sayı biçimini nasıl ekleyeceğinizi gösterir.
og_title: Excel Çalışma Kitabı Oluşturma C# – Para Birimi Biçimlendirme Rehberi
tags:
- Aspose.Cells
- C#
- Excel automation
title: Excel Çalışma Kitabı Oluştur C# – Para Birimi Formatı Uygula ve DataTable'ı
  İçe Aktar
url: /tr/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel Çalışma Kitabı Oluştur C# – Para Birimi Biçimi Uygula ve DataTable İçe Aktar

Hiç **create Excel workbook C#** gibi zaten cilalı bir rapor gibi görünen bir dosya oluşturmanız gerekti mi? Belki bir veritabanından satış rakamlarını çekiyorsunuz ve fiyat sütununu dolar olarak göstermek istiyorsunuz, Excel’i manuel olarak ayarlamadan. Tanıdık geliyor mu? Yalnız değilsiniz—çoğu geliştirici, Excel dışa aktarmalarını otomatikleştirirken bu sorunu ilk kez yaşar.

Bu rehberde, **Excel çalışma kitabı C#** oluşturan, bir `DataTable` içe aktaran ve **Fiyat sütununu para birimi olarak biçimlendiren** eksiksiz, çalıştırılabilir bir çözümü adım adım inceleyeceğiz. Sonunda `StyledTable.xlsx` adlı bir dosyanız olacak; bunu açtığınızda güzel biçimlendirilmiş sayılar göreceksiniz. Ek bir post‑işleme gerek yok.

> **Öğrenecekleriniz**
> - .NET projesinde Aspose.Cells nasıl kurulur  
> - **datatable to excel** nasıl içe aktarılır ve stil dizisiyle birlikte kullanılır  
> - Belirli bir sütun için **add number format excel** nasıl eklenir  
> - Daha fazla sütun veya farklı yerel ayarlar için ipuçları  

> **Önkoşullar**  
> - .NET 6+ (veya .NET Framework 4.6+) yüklü  
> - Aspose.Cells for .NET NuGet paketi (`Install-Package Aspose.Cells`)  
> - C# ve DataTable’lar hakkında temel bilgi  

---

## Adım 1: DataTable’ı Hazırlayın (import datatable to excel)

İlk olarak örnek veri oluşturalım. Gerçek bir uygulamada bu tabloyu bir DB sorgusundan doldurursunuz, ancak sabit kodlu bir örnek işleri basitleştirir.

```csharp
using System.Data;

// Create a DataTable with two columns: Product (string) and Price (double)
DataTable dataTable = new DataTable();
dataTable.Columns.Add("Product", typeof(string));
dataTable.Columns.Add("Price", typeof(double));

// Add a few rows – you can add as many as you like
dataTable.Rows.Add("Apple", 1.23);
dataTable.Rows.Add("Banana", 0.78);
dataTable.Rows.Add("Cherry", 2.50);
```

*Neden önemli*: `DataTable`, iş verileriniz ile Excel dosyası arasındaki köprüdür. Aspose.Cells, sütun adlarını ve veri tiplerini koruyarak doğrudan içe aktarabilir.

---

## Adım 2: Yeni Bir Workbook Oluşturun (create excel workbook c#)

Şimdi gerçek Excel dosyası nesnesini oluşturuyoruz. Bunu, üzerine çizeceğiniz boş bir kanvas olarak düşünün.

```csharp
using Aspose.Cells;

// Instantiate a fresh workbook – this is the core of create excel workbook c#
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0). You could also add more sheets later.
Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro ipucu:** Birden fazla sayfa (sheet) eklemeniz gerekiyorsa `workbook.Worksheets.Add()` çağırın ve her birine anlamlı bir ad verin.

---

## Adım 3: Para Birimi Stili Tanımlayın (format cells currency)

Aspose.Cells, hücrelerin nasıl görüneceğini tanımlayan bir `Style` nesnesi oluşturmanıza izin verir. Para birimi için yerleşik sayı biçimi kimliği 164 (`"$#,##0.00"`) kullanılır.

```csharp
// Create a new style object for the price column
Style priceStyle = workbook.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format "$#,##0.00"
```

*Niçin sadece biçim dizesi ayarlamıyoruz?* Yerleşik kimliği kullanmak, Excel sürümleri arasında uyumluluğu garantiler ve yerel ayar kaynaklı tuhaflıkları önler.

---

## Adım 4: Stil Dizisini Oluşturun (apply currency format column)

Bir `DataTable` içe aktarırken, sütun başına bir `Style` nesnesi içeren bir dizi geçebilirsiniz—her sütun için bir tane. `null` değeri “varsayılan stili kullan” anlamına gelir. Burada sadece ikinci sütuna `priceStyle` uyguluyoruz.

```csharp
// Column 0 (Product) gets the default style, Column 1 (Price) gets the currency style
Style[] columnStyles = { null, priceStyle };
```

Daha sonra daha fazla sütun eklerseniz, diziyi buna göre genişletmeniz yeterli. `columnStyles` uzunluğu, içe aktaracağınız sütun sayısıyla aynı olmalıdır; aksi takdirde Aspose bir istisna fırlatır.

---

## Adım 5: DataTable’ı Stillerle İçe Aktarın (import datatable to excel)

Şimdi sihir gerçekleşiyor—`DataTable` çalışma sayfasına yerleşiyor ve fiyat sütunu anında para birimi olarak gösteriliyor.

```csharp
// Parameters:
//  - dataTable: source data
//  - true: include column headers
//  - startRow: 0 (top of sheet)
//  - startColumn: 0 (first column)
//  - columnStyles: style array defined above
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

*Daha iki sütundan fazla varsa ne olur?* `columnStyles` dizisini genişletin; her sütun için uygun stili (veya varsayılan için `null`) atayın. Bu, **add number format excel** işlemini seçici olarak yapmanın en temiz yoludur.

---

## Adım 6: Workbook’u Kaydedin (create excel workbook c#)

Son olarak dosyayı diske yazıyoruz. Yazma izniniz olan herhangi bir klasörü seçin.

```csharp
// Save the workbook as an XLSX file
workbook.Save("YOUR_DIRECTORY/StyledTable.xlsx");
```

`StyledTable.xlsx` dosyasını Excel’de açtığınızda şu tabloyu görmelisiniz:

| Product | Price |
|---------|-------|
| Apple   | $1.23 |
| Banana  | $0.78 |
| Cherry  | $2.50 |

**Price** sütunu zaten para birimi olarak biçimlendirilmiş—ek bir adım gerekmez.

---

## Kenar Durumları ve Varyasyonlar

### Daha Fazla Sütun, Farklı Biçimler

Birden fazla sütun için **format cells currency** uygulamanız gerekiyorsa (ör. Cost, Tax, Total), her biri için ayrı bir `Style` oluşturun ve `columnStyles` dizisini ona göre doldurun:

```csharp
Style costStyle = workbook.CreateStyle();
costStyle.Number = 164; // currency

Style taxStyle = workbook.CreateStyle();
taxStyle.Number = 164;

// Assuming columns: Product, Cost, Tax, Total
Style[] styles = { null, costStyle, taxStyle, priceStyle };
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, styles);
```

### Yerel Para Birimi

Euro veya İngiliz Sterlini için farklı yerleşik kimlikler kullanın (ör. `€#,##0.00` için 165). Alternatif olarak özel bir biçim dizesi ayarlayabilirsiniz:

```csharp
priceStyle.Custom = "€#,##0.00";
```

### Büyük Veri Setleri

Aspose.Cells milyonlarca satırı işleyebilir, ancak stil nesneleri bellek tüketimini artırır. Tüm para birimi sütunları için tek bir `Style` örneği yeniden kullanarak ayak izini düşük tutun.

### Stil Eksikliği

`columnStyles` sütun sayısından kısa ise, Aspose kalan sütunlara varsayılan stili uygular. Bu, sadece birkaç sütunla ilgilendiğinizde kullanışlıdır.

---

## Tam Çalışan Örnek (Tüm Adımlar Birleştirildi)

Aşağıda, bir konsol uygulamasına kopyalayıp yapıştırabileceğiniz eksiksiz program yer alıyor. Tartıştığımız tüm parçalar ve birkaç yardımcı yorum içeriyor.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Build sample DataTable (import datatable to excel)
        // -------------------------------------------------
        DataTable dataTable = new DataTable();
        dataTable.Columns.Add("Product", typeof(string));
        dataTable.Columns.Add("Price", typeof(double));
        dataTable.Rows.Add("Apple", 1.23);
        dataTable.Rows.Add("Banana", 0.78);
        dataTable.Rows.Add("Cherry", 2.50);
        // You can add as many rows as you like here.

        // -------------------------------------------------
        // Step 2: Create a new workbook (create excel workbook c#)
        // -------------------------------------------------
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // -------------------------------------------------
        // Step 3: Define a currency style (format cells currency)
        // -------------------------------------------------
        Style priceStyle = workbook.CreateStyle();
        priceStyle.Number = 164; // "$#,##0.00" – built‑in currency format

        // -------------------------------------------------
        // Step 4: Build the style array (apply currency format column)
        // -------------------------------------------------
        // First column gets default style (null), second column uses priceStyle.
        Style[] columnStyles = { null, priceStyle };

        // -------------------------------------------------
        // Step 5: Import the DataTable with the style array
        // -------------------------------------------------
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // -------------------------------------------------
        // Step 6: Save the workbook to disk
        // -------------------------------------------------
        string outputPath = @"YOUR_DIRECTORY\StyledTable.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Beklenen sonuç:** `StyledTable.xlsx` dosyasını açtığınızda `Price` sütunu dolar işareti ve iki ondalık basamakla gösterilir; tam da **format cells currency** talimatının istediği gibi.

---

## Sık Sorulan Sorular

**S: Bu .NET Core ile çalışır mı?**  
C: Kesinlikle. Aspose.Cells .NET‑standard uyumlu olduğu için .NET 5, .NET 6 veya daha yeni sürümlerle değişiklik yapmadan kullanılabilir.

**S: DataTable’ım 10 sütun içeriyor ama sadece 5. sütunu biçimlendirmek istiyorum, ne yapmalıyım?**  
C: Uzunluğu 10 olan bir `Style[]` oluşturun, 0‑4 ve 6‑9 indekslerini `null` ile doldurun, özel stilinizi 4. indekse (sıfır‑tabanlı) yerleştirin. Aspose her girişi dikkate alacaktır.

**S: Başlık satırını gizleyebilir miyim?**  
C: İçe aktarma sonrası `worksheet.Cells.Rows[0].Hidden = true;` satırını ekleyin veya `ImportDataTable` metodunda `includeColumnNames` parametresini `false` olarak geçin.

---

## Sonuç

Biz **Excel workbook C#** oluşturduk, bir `DataTable` içe aktardık ve Aspose.Cells kullanarak **para birimi formatlı bir sütun** ekledik. Veriyi hazırlama, stil tanımlama, stil dizisi oluşturma, `ImportDataTable` ile içe aktarma ve kaydetme adımları, çoğu Excel otomasyon görevinin temelini oluşturur.

Buradan ilerleyerek şunları keşfedebilirsiniz:

- **add number format excel** ile tarih veya yüzde biçimleri  
- Tek bir dosyada birden fazla çalışma sayfası dışa aktarma  
- **format cells currency** ile yerel para birimi sembolleri kullanma  
- Aynı veri üzerinden grafik otomasyonu  

Deneyin, ekibinizde Excel raporlamasının vazgeçilmez kişi haline gelin. Paylaşmak istediğiniz bir örnek var mı? Aşağıya yorum bırakın—mutlu kodlamalar!  

![excel çalışma kitabı oluştur c# ekran görüntüsü](image.png "excel çalışma kitabı oluştur c#")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}