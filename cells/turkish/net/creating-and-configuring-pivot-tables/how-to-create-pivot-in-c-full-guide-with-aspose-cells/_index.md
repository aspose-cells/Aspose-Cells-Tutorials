---
category: general
date: 2026-03-27
description: Aspose.Cells kullanarak C#'de pivot tablo nasıl oluşturulur – tek bir
  öğreticide veri eklemeyi, yenilemeyi etkinleştirmeyi ve çalışma kitabını xlsx olarak
  kaydetmeyi öğrenin.
draft: false
keywords:
- how to create pivot
- save workbook as xlsx
- how to enable refresh
- how to add data
- generate excel file c#
language: tr
og_description: C# ile Aspose.Cells kullanarak pivot nasıl oluşturulur. Bu rehber,
  verileri nasıl ekleyeceğinizi, yenilemeyi nasıl etkinleştireceğinizi ve çalışma
  kitabını xlsx olarak nasıl kaydedeceğinizi gösterir.
og_title: C#'ta Pivot Nasıl Oluşturulur – Tam Aspose.Cells Eğitimi
tags:
- Aspose.Cells
- C#
- Excel automation
title: C#'ta Pivot Nasıl Oluşturulur – Aspose.Cells ile Tam Rehber
url: /tr/net/creating-and-configuring-pivot-tables/how-to-create-pivot-in-c-full-guide-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#’ta Pivot Nasıl Oluşturulur – Eksiksiz Aspose.Cells Öğreticisi

COM interop ile uğraşmadan **C#’ta pivot nasıl oluşturulur** diye hiç merak ettiniz mi? Tek başınıza değilsiniz. Birçok veri‑odaklı uygulamada ham satış rakamlarını düzenli bir özet haline getirmek için hızlı bir yola ihtiyaç duyarız ve Aspose.Cells bunu çocuk oyuncağı hâline getiriyor.  

Bu öğreticide her adımı adım adım inceleyeceğiz: verileri ekleme, pivot tabloyu oluşturma, otomatik yenilemeyi etkinleştirme ve sonunda **workbook’u xlsx olarak kaydetme** ki kullanıcılarınız dosyayı anında Excel’de açabilsin. Sonunda hazır bir `PivotRefresh.xlsx` dosyanız ve her satırın neden önemli olduğuna dair sağlam bir anlayışınız olacak.

## Önkoşullar

- .NET 6+ (veya .NET Framework 4.7.2 ve üzeri) – herhangi bir güncel runtime yeterlidir.  
- Aspose.Cells for .NET – NuGet üzerinden çekebilirsiniz (`Install-Package Aspose.Cells`).  
- C# sözdizimine temel bir aşinalık – derin Excel bilgisi gerekmez.

> **Pro ipucu:** Kurumsal bir makinede çalışıyorsanız, Aspose lisansının uygulanmış olduğundan emin olun; aksi takdirde oluşturulan dosyada filigran görürsünüz.

## Adım 1 – Yeni Bir Workbook’a Veri Nasıl Eklenir

Pivot var olabilmesi için bir kaynak tablo olması gerekir. Yeni bir workbook oluşturacağız, ilk çalışma sayfasına *SalesData* adını vereceğiz ve gerçek dünya satış verisini taklit eden birkaç satır ekleyeceğiz.

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and grab the default sheet
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        // 2️⃣ Write column headers
        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // 3️⃣ Insert a sample row – add more rows as your scenario demands
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);
```

**Neden önemli:**  
- `PutValue` kullanmak hücre tipini otomatik olarak ayarlar, böylece daha sonra string‑ve‑numeric uyumsuzluklarıyla uğraşmazsınız.  
- 1. satırda başlıkları tanımlamak, pivot motorunun alanları eşleştirirken referans alacağı bir şey sağlar.

## Adım 2 – Pivot Tablosunun Barınacağı Çalışma Sayfasını Oluşturun

Pivot tablosu kendi sayfasında bulunur, böylece kaynak veri temiz kalır ve rapor düzenli olur.

```csharp
        // 4️⃣ Add a dedicated sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");
```

> **Peki ya zaten bir sayfanız var ise?** Yeni bir sayfa eklemek yerine (`workbook.Worksheets["MySheet"]`) indeksle referans verin.

## Adım 3 – Kaynak Aralığı Tanımlama (Veri Ekle → Aralığı Tanımla)

Aspose.Cells bir `CellArea` ya da hem başlıkları hem de verileri kapsayan bir aralık dizesi ister. Burada maksimum 100 satır varsayıyoruz; ihtiyacınıza göre ayarlayın.

```csharp
        // 5️⃣ Build the source range (A1:D100 covers headers + up to 99 data rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");
```

**Köşe durum:** Veri kümeniz dinamikse, son kullanılan satırı `salesDataSheet.Cells.MaxDataRow` ile hesaplayıp aralığı buna göre oluşturabilirsiniz.

## Adım 4 – Pivot Nasıl Oluşturulur – Pivot Tablosunu Ekleme

Şimdi eğlenceli kısım: Aspose.Cells’e az önce tanımladığımız aralığa bağlı bir pivot oluşturmasını söylüyoruz.

```csharp
        // 6️⃣ Insert the pivot table at cell A3 of the pivot sheet
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];
```

Formül‑stili referansa (`=SalesData!A1:D100`) dikkat edin. Bu, Excel’de yazacağınız aynı sözdizimi, API’yı sezgisel kılıyor.

## Adım 5 – Satır, Sütun ve Veri Alanlarını Yapılandırma (Veri Ekle → Alanlar)

*Region*’u satırlara, *Product*’ı sütunlara ve hem *Units* hem de *Revenue*’yi toplamak (sum) için yerleştireceğiz.

```csharp
        // 7️⃣ Set up row, column, and data fields
        pivotTable.RowFields.Add(0); // 0 = first column => Region
        pivotTable.ColumnFields.Add(1); // 1 = second column => Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);
```

**Bu indeksler neden?**  
Aspose.Cells sütunları 0’dan başlatır, bu yüzden `0` *Region*’a işaret eder. `DataFields.Add` metodu alanı yeniden adlandırmanıza (ör. “Sum of Units”) ve bir toplama türü seçmenize izin verir – sayısal veriler için `Sum` en yaygın olanıdır.

## Adım 6 – Yenilemeyi Etkinleştirme – Pivot’u Açıldığında Otomatik Güncelle

Kaynak veri daha sonra değişirse, pivotun bu değişiklikleri otomatik olarak yansıtmasını isteyebilirsiniz. İşte `RefreshDataOnOpen` burada devreye girer.

```csharp
        // 8️⃣ Turn on automatic refresh when the file is opened
        pivotTable.RefreshDataOnOpen = true;
```

> **Not:** Bu bayrak yalnızca workbook Excel’de açıldığında çalışır; Aspose.Cells içinde otomatik yeniden hesaplama yapmaz, `pivotTable.RefreshData()` metodunu manuel olarak çağırmanız gerekir.

## Adım 7 – Workbook’u XLSX Olarak Kaydetme (Workbook’u XLSX Olarak Kaydet)

Son olarak dosyayı diske kalıcı olarak yazdırıyoruz. `.xlsx` formatı, her yerde çalışan modern, zip‑tabanlı Excel dosya tipidir.

```csharp
        // 9️⃣ Save the workbook – this also satisfies the “save workbook as xlsx” requirement
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

Programı çalıştırdığınızda **PivotRefresh.xlsx** adlı bir dosya yürütme klasöründe oluşur. Excel’de açtığınızda *Region* satırları, *Product* sütunları ve toplanmış *Units* ve *Revenue* değerleriyle düzenli bir pivot göreceksiniz. Yenilemeyi etkinleştirdiğimiz için *SalesData* sayfasında yaptığınız herhangi bir düzenleme, workbook’u bir sonraki açışınızda pivotta otomatik olarak güncellenecektir.

### Beklenen Çıktı

| Region | Widget | Gadget | … |
|--------|--------|--------|---|
| East   | 120    | 0      |   |
| West   | 0      | 85     |   |
| **Grand Total** | **120** | **85** |   |

*(Satırlarınıza eklediğiniz verilere göre sayılar değişecektir.)*

---

## Sık Sorulan Sorular & Varyasyonlar

### Birden fazla pivot tabloya ihtiyacım olursa ne yapmalıyım?

**Adım 4**’ü farklı bir ad ve konumla tekrarlayabilirsiniz. `PivotTables.Add` her seferinde yeni bir indeks döndürür; bu indeksi tablo nesnesini almak için kullanabilirsiniz.

### Toplam yerine *Ortalama* (Average) kullanmak istiyorum, nasıl değiştiririm?

`DataFields.Add` çağrılarındaki `PivotTableDataAggregationType.Sum` ifadesini `PivotTableDataAggregationType.Average` ile değiştirin.

### Pivotun stilini (yazı tipleri, renkler) ayarlayabilir miyim?

Evet. Pivotu oluşturduktan sonra `Style` özelliğine erişebilir ya da pivotun bulunduğu aralığa hücre biçimlendirmesi uygulayabilirsiniz. Örneğin:

```csharp
pivotTable.Style = workbook.Styles[workbook.Styles.Add()];
pivotTable.Style.Font.Color = System.Drawing.Color.DarkBlue;
```

### Workbook kaydedildikten sonra daha fazla satır eklemek mümkün mü?

Kesinlikle. Dosyayı `new Workbook("PivotRefresh.xlsx")` ile yükleyin, *SalesData* sayfasına satır ekleyin ve tekrar kaydetmeden önce `pivotTable.RefreshData()` metodunu çağırın.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // Step 1: Create workbook & add sample data
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // Sample rows – extend as needed
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);

        salesDataSheet.Cells["A3"].PutValue("West");
        salesDataSheet.Cells["B3"].PutValue("Gadget");
        salesDataSheet.Cells["C3"].PutValue(85);
        salesDataSheet.Cells["D3"].PutValue(4250);

        // Step 2: Add sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");

        // Step 3: Define source range (covers up to 100 rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");

        // Step 4: Insert pivot table
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];

        // Step 5: Configure fields
        pivotTable.RowFields.Add(0); // Region
        pivotTable.ColumnFields.Add(1); // Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);

        // Step 6: Enable automatic refresh
        pivotTable.RefreshDataOnOpen = true;

        // Step 7: Save as .xlsx
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

Dosyayı kaydedin, çalıştırın ve oluşturulan **PivotRefresh.xlsx** dosyasını açın – **C#’ta pivot nasıl oluşturulur** konusunda uzmanlaştınız.

---

## Sonuç

**Pivot tablolarını programatik olarak nasıl oluşturulur**, **veri nasıl eklenir**, **yenileme nasıl etkinleştirilir** ve sonunda **workbook nasıl xlsx olarak kaydedilir** konularını Aspose.Cells kullanarak ele aldık. Kod

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}