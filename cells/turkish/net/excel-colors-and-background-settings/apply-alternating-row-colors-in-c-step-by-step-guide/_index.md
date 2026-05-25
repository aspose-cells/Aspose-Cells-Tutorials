---
category: general
date: 2026-03-18
description: C# kullanarak bir çalışma sayfasında alternatif satır renkleri uygulamayı
  öğrenin. Satır arka plan rengini ayarlama, açık sarı arka plan ekleme ve satırları
  sırayla renklendirme içerir.
draft: false
keywords:
- apply alternating row colors
- set row background color
- add light yellow background
- set alternating row shading
- color rows alternately
language: tr
og_description: C#'de okunabilirliği artırmak için satır renklerini değiştirerek uygulayın.
  Bu kılavuz, satır arka plan rengini nasıl ayarlayacağınızı, açık sarı arka plan
  eklemeyi ve satırları dönüşümlü olarak renklendirmeyi gösterir.
og_title: C#'de Alternatif Satır Renkleri Uygulama – Tam Kılavuz
tags:
- C#
- DataTable
- Spreadsheet styling
- UI design
title: C#'de Alternatif Satır Renkleri Uygulama – Adım Adım Rehber
url: /tr/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Alternatif Satır Renkleri Uygulama – Tam Kılavuz

Veri‑odaklı bir çalışma sayfasına **alternatif satır renkleri uygulamayı** hiç ihtiyaç duydunuz mu ama nereden başlayacağınızı bilemediniz mi? Tek başınıza değilsiniz — çoğu geliştirici, tabloları biraz daha dostane göstermek istediklerinde bu soruna takılır. İyi haber? Sadece birkaç C# satırıyla **satır arka plan rengini ayarlayabilir**, **hafif sarı bir arka plan ekleyebilir** ve anında okunabilirliği artıran şık bir ızgara elde edebilirsiniz.

Bu öğreticide, bir `DataTable`'ı belleğe çekmekten her satırı hafif sarı‑beyaz bir şerit ile biçimlendirmeye kadar tüm süreci adım adım inceleyeceğiz. Sonunda **satırları alternatif olarak renklendirebilecek** ve farklı tonlar ya da dinamik temalar gerektiğinde kullanabileceğiniz birkaç pratik varyasyonu göreceksiniz.

## Gereksinimler

- .NET 6 veya daha yeni bir sürümü hedefleyen bir .NET projesi (kod .NET Framework 4.7+ üzerinde de çalışır).  
- Stil nesnelerini destekleyen bir elektronik tablo kütüphanesi – örnek, **Aspose.Cells**, **GemBox.Spreadsheet** veya **ClosedXML** gibi kütüphanelere benzer bir genel `Workbook`/`Worksheet` API'si kullanıyor.  
- Bir `DataTable` kaynağı – veritabanı sorgusu, CSV içe aktarma veya herhangi bir bellek içi koleksiyon olabilir.  

Ekstra bir NuGet paketi gerekmez; sadece elektronik tablo kütüphaneniz yeterli. Aspose.Cells kullanıyorsanız, ad alanı `Aspose.Cells`; ClosedXML için `ClosedXML.Excel` olur. `CreateStyle` ve `ImportDataTable` çağrılarını buna göre değiştirin.

## Adım 1: Kaynak Veriyi DataTable Olarak Alın

İlk iş, göstermek istediğiniz veriyi yakalamaktır. Gerçek dünyada bu genellikle bir veritabanına bağlanmak anlamına gelir, ancak açıklık sağlamak için `GetData()` adlı bir yardımcı yöntemi taklit edeceğiz; bu yöntem doldurulmuş bir `DataTable` döndürür.

```csharp
// Step 1: Retrieve the source data as a DataTable
DataTable dataTable = GetData();   // Replace with your actual data retrieval logic
```

> **Why this matters:** `DataTable`, daha sonra alternatif gölgelendirme uygulanacak satır ve sütunları tanımlar. Tablo boşsa stil uygulanacak bir şey yoktur, bu yüzden ilerlemeden önce her zaman `Rows.Count` > 0 olduğundan emin olun.

### Pro ipucu
Entity Framework'ten veri çekiyorsanız, bir `SqlCommand` çalıştırdıktan sonra `DataTable.Load(reader)` kullanabilirsiniz. Bu, kodu düzenli tutar ve manuel sütun tanımlamalarını önler.

## Adım 2: Her Satır İçin Bir Stil Tutacak Dizi Oluşturun

Sonra, satır sayısıyla eşleşen bir kapsayıcıya ihtiyacımız var. Çoğu elektronik tablo API'si, içe aktarma metoduna bir stil dizisi geçmenize izin verir; bu yüzden satır sayısına tam olarak uyan bir `Style[]` oluşturacağız.

```csharp
// Step 2: Allocate an array to hold a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];
```

> **Explanation:** Diziyi önceden ayırarak, her yinelemede yeni bir stil nesnesi yeniden tahsis edilmesinden kaçınırız; bu, binlerce satırla çalışırken performans kazancı sağlayabilir.

## Adım 3: Alternatif Satır Renklerini Uygulayın (Açık Sarı / Beyaz)

Şimdi işin özü: **alternatif satır renkleri uygulama**. Her satırı döngüyle gezip, çalışma kitabından yeni bir stil örneği oluşturacağız ve arka planını satır indeksine göre ayarlayacağız. Çift satırlar açık sarı, tek satırlar beyaz kalacak.

```csharp
// Step 3: Create alternating background colors (light yellow / white) for the rows
for (int rowIndex = 0; rowIndex < dataTable.Rows.Count; rowIndex++)
{
    // Create a new style instance from the workbook
    rowStyles[rowIndex] = wb.CreateStyle();

    // Apply a light yellow background to even rows, white to odd rows
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow   // add light yellow background
        : Color.White;        // set row background color to white

    rowStyles[rowIndex].Pattern = BackgroundType.Solid; // set alternating row shading
}
```

### Neden Bu Çalışıyor
- **`rowIndex % 2 == 0`** satırın çift olup olmadığını kontrol eder.  
- **`Color.LightYellow`** veri tabloları için mükemmel, hafif ve göz yormayan bir ton sağlar.  
- **`BackgroundType.Solid`** doldurmanın tüm hücreyi kaplamasını sağlar ve **set row background color** etkisini verir.  

`Color.LightYellow` yerine başka bir ton (ör. `Color.LightCyan`) kullanarak farklı bir görünüm elde edebilirsiniz. Aynı mantık, durum bayrakları gibi başka kriterlere göre **satırları alternatif olarak renklendirme** imkanı da sunar.

## Adım 4: Hazırlanan Stillerle DataTable'ı Worksheet'e İçe Aktarın

Son olarak, her şeyi çalışma sayfasına gönderiyoruz. Çoğu kütüphane, stil dizisini kabul eden bir `ImportDataTable` aşırı yüklemesi sunar. `true` bayrağı API'ye sütun başlıklarını yazmasını söyler, `0, 0` koordinatları ise sol‑üst hücreden başlamasını sağlar.

```csharp
// Step 4: Import the DataTable into the worksheet, applying the prepared row styles
ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

> **Result:** Worksheet artık temiz bir **alternatif satır gölgelendirme** deseniyle verinizi gösteriyor—çift satırlarda açık sarı, tek satırlarda beyaz. Kullanıcılar ızgarayı gözlerini geri‑geri hareket ettirmeden tarayabilir.

### Beklenen Çıktı
Eğer oluşturulan elektronik tabloyu açarsanız, aşağıdaki gibi bir görünüm görürsünüz:

| ID | Name      | Quantity |
|----|-----------|----------|
| **1** | Apple      | 50       |
| **2** | Banana     | 30       |
| **3** | Cherry     | 20       |
| **4** | Date       | 15       |

Satır 1, 3, 5… **açık sarı arka plan** alırken, satır 2, 4, 6… **beyaz** kalır. Başlık satırı (satır 0) ayrı bir şekilde özelleştirilmediği sürece varsayılan stili devralır.

## İsteğe Bağlı Varyasyonlar & Kenar Durumları

### 1. Farklı Bir Renk Paleti Kullanma
Açık sarı, markanızla çelişiyorsa, sadece `Color.LightYellow` yerine başka bir `System.Drawing.Color` ile değiştirin. Mavi‑gri bir tema için şu şekilde kullanabilirsiniz:

```csharp
rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
    ? Color.FromArgb(220, 235, 247) // soft blue
    : Color.White;
```

### 2. Veriye Dayalı Dinamik Gölgelendirme
Bazen bir koşulu karşılayan satırları vurgulamak istersiniz (ör. düşük stok). Modulo kontrolünü özel bir testle birleştirin:

```csharp
int quantity = Convert.ToInt32(dataTable.Rows[rowIndex]["Quantity"]);
if (quantity < 20)
{
    rowStyles[rowIndex].ForegroundColor = Color.Salmon; // urgent low‑stock color
}
else
{
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow
        : Color.White;
}
```

### 3. Yalnızca Belirli Sütunlara Stil Uygulama
Sadece belirli sütunlarda **set row background color** ihtiyacınız varsa, her sütun için ayrı bir stil oluşturun ve içe aktarmadan sonra worksheet'in hücre aralığı API'siyle atayın.

```csharp
// Example for column B only
var colBStyle = wb.CreateStyle();
colBStyle.ForegroundColor = Color.LightYellow;
colBStyle.Pattern = BackgroundType.Solid;

// Apply after import
ws.Cells[$"B2:B{dataTable.Rows.Count + 1}"].SetStyle(colBStyle);
```

### 4. Büyük Tablolar İçin Performans İpucu
> 10.000 satırdan fazla ile çalışırken, her satır için yeni bir stil nesnesi oluşturmak yerine her renk için tek bir stil nesnesi yeniden kullanın. Dizi, iki ortak stilin referanslarını tutar ve bellek kullanımını büyük ölçüde azaltır.

```csharp
Style yellowStyle = wb.CreateStyle();
yellowStyle.ForegroundColor = Color.LightYellow;
yellowStyle.Pattern = BackgroundType.Solid;

Style whiteStyle = wb.CreateStyle();
whiteStyle.ForegroundColor = Color.White;
whiteStyle.Pattern = BackgroundType.Solid;

for (int i = 0; i < dataTable.Rows.Count; i++)
    rowStyles[i] = (i % 2 == 0) ? yellowStyle : whiteStyle;
```

## Tam Çalışan Örnek

Aşağıda, bir console uygulamasına yapıştırabileceğiniz bağımsız bir program yer alıyor. Kurgusal bir `Workbook`/`Worksheet` API'si kullanıyor; türleri seçtiğiniz kütüphanenin karşılıklarıyla değiştirin.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using YourSpreadsheetLib;     // Replace with actual namespace

class Program
{
    static void Main()
    {
        // Initialize workbook & worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Step 1: Retrieve data
        DataTable dataTable = GetData();

        // Step 2: Allocate style array
        Style[] rowStyles = new Style[dataTable.Rows.Count];

        // Step 3: Apply alternating row colors
        for (int i = 0; i < dataTable.Rows.Count; i++)
        {
            rowStyles[i] = wb.CreateStyle();
            rowStyles[i].ForegroundColor = (i % 2 == 0)
                ? Color.LightYellow   // add light yellow background
                : Color.White;        // set row background color
            rowStyles[i].Pattern = BackgroundType.Solid; // set alternating row shading
        }

        // Step 4: Import with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // Save to file
        wb.Save("AlternatingRows.xlsx");
        Console.WriteLine("Workbook saved with alternating row colors.");
    }

    // Sample data generator
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Quantity", typeof(int));

        dt.Rows.Add(1, "Apple", 50);
        dt.Rows.Add(2, "Banana", 30);
        dt.Rows.Add(3, "Cherry", 20);
        dt.Rows.Add(4, "Date", 15);
        dt.Rows.Add(5, "Elderberry", 5);
        return dt;
    }
}
```

**Output:** `AlternatingRows.xlsx` adlı bir dosya oluşturur; her satır açık sarı dolgu ile beyaz arasında geçiş yapar ve tabloyu göz yorgunluğunu azaltacak şekilde daha okunabilir hâle getirir.

## Sıkça Sorulan Sorular

**S: Bu yaklaşım Excel‑stili koşullu biçimlendirme ile çalışır mı?**  
C: Evet. Kütüphaneniz koşullu kuralları destekliyorsa, aynı mantığı `MOD(ROW(),2)=0` kontrol eden bir kural haline getirebilirsiniz. Burada gösterilen kod‑tabanlı yöntem, yerleşik koşullu biçimlendirme bulunmayan kütüphanelerde daha taşınabilir bir çözümdür.

**S: Excel yerine bir PDF tablosunda **satırları alternatif olarak renklendirmem** gerekirse ne yapmalıyım?**  
C: Çoğu PDF tablo oluşturucu (ör. iTextSharp, PdfSharp) satır başına bir `BackgroundColor` ayarlamanıza izin verir. Aynı modulo hesabı burada da geçerlidir—

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}