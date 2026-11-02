---
category: general
date: 2026-09-21
description: C#'ta SmartMarkerOptions ArrayAsSingle'ı yapılandırarak JSON dizilerini
  bir Excel çalışma kitabında tek hücre değeri olarak dışa aktarın.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- configure smartmarkeroptions arrayassingle
- Aspose.Cells smart markers
- export JSON array
- C# DataTable
- Workbook ProcessSmartMarkers
language: tr
lastmod: 2026-09-21
og_description: C#'ta SmartMarkerOptions ArrayAsSingle seçeneğini yapılandırarak JSON
  dizilerini tek bir hücre değeri olarak dışa aktarın. Tam adım adım çözümü öğrenin.
og_image_alt: Screenshot of an Excel sheet showing a JSON array stored in a single
  cell after using SmartMarkerOptions
og_title: C#'ta SmartMarkerOptions ArrayAsSingle'ı yapılandırma – tam rehber
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Configure SmartMarkerOptions ArrayAsSingle in C# to export JSON arrays
    as a single cell value in an Excel workbook.
  headline: Configure SmartMarkerOptions ArrayAsSingle in C# for JSON arrays
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: C#'ta JSON dizileri için SmartMarkerOptions ArrayAsSingle'ı yapılandırın
url: /tr/net/smart-markers-dynamic-data/configure-smartmarkeroptions-arrayassingle-in-c-for-json-arr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#’ta SmartMarkerOptions ArrayAsSingle’ı JSON Dizileri İçin Yapılandırma

Aspose.Cells ile Excel dosyaları oluştururken **SmartMarkerOptions ArrayAsSingle** özelliğini yapılandırmanız gerekiyorsa, bu kılavuz tam olarak nasıl yapılacağını gösterir. JSON dizisini birden çok satıra yaymak yerine tek bir hücrede tutmayı öğreneceksiniz.

JSON verileriyle elektronik tablo çalışmak, çoğu zaman düzleştirilmiş bir görünüm ile kompakt bir temsil arasında seçim yapmayı gerektirir. Birçok raporlama senaryosunda—etiket listesi veya kimlik seti gibi—tüm JSON dizesinin tek bir hücrede kalmasını istersiniz. `SmartMarkerOptions` içindeki **ArrayAsSingle** bayrağı bu imkanı sağlar.

Bu öğreticide şunları yapacaksınız:

* JSON dizisini bir sütunda tutan bir `DataTable` oluşturma.
* Excel çalışma sayfasına Smart Marker’lar ekleme.
* **SmartMarkerOptions ArrayAsSingle**’ı yapılandırarak JSON dizisinin tek hücre değeri olarak işlenmesini sağlama.
* Marker’ları işleyip çalışma kitabını kaydetme.
* Çıktıyı doğrulama.

> **Önkoşullar** – Aspose.Cells for .NET kütüphanesinin (v23.12 veya daha yeni) ve bir .NET geliştirme ortamının (Visual Studio 2022 önerilir) kurulu olması gerekir. C# ve DataTable’lar hakkında temel bilgi varsayılmıştır.

---

## Adım 1: JSON Dizisi İçeren Veri Kaynağını Hazırlama

İlk olarak, bir hizmetten veya veritabanından alacağınız veriyi taklit eden bir `DataTable` oluşturun. **Names** sütunu, bir dizi ismi temsil eden JSON‑kodlu bir dize içerir.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable dataTable = new DataTable();
dataTable.Columns.Add("Id", typeof(int));
dataTable.Columns.Add("Names", typeof(string));

// Store the JSON array as a plain string
dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");
```

*Bu adım neden?*  
Smart Marker’lar .NET nesnelerinden doğrudan veri okur. JSON dizisini bir dize sütununda tutarak, daha sonra hücreye değişmeden yazılabilecek tam JSON sözdizimini korumuş olursunuz.

---

## Adım 2: Yeni Bir Çalışma Kitabına Smart Marker’lar Ekleyin

Yeni bir çalışma kitabı oluşturun, ilk çalışma sayfasını seçin ve tüm tabloyu ve özellikle **Names** sütununu referans alan Smart Marker’ları yazın.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Smart marker for the entire table (optional, shown for completeness)
worksheet.Cells["A1"].PutValue("&=dataTable");

// Smart marker that targets only the Names column
worksheet.Cells["A2"].PutValue("&=dataTable.Names");
```

`&=dataTable.Names` işareti, Aspose.Cells’e `dataTable` içindeki **Names** sütununun değerini her satır için hücreye yerleştirmesini söyler. Sadece bir satırımız olduğu için işaretçi bir kez işlenecektir.

---

## Adım 3: **SmartMarkerOptions ArrayAsSingle**’ı **Yapılandırma**

Varsayılan olarak, Aspose.Cells bir dizi‑gibi dizeyi ayrı satırlara genişletir. `ArrayAsSingle`’ı `true` olarak ayarlamak bu davranışı geçersiz kılar ve bütün JSON dizesinin tek bir hücrede kalmasını sağlar.

```csharp
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    // Export the JSON array as a single cell value
    ArrayAsSingle = true
};
```

*`ArrayAsSingle` neden etkinleştirilmeli?*  
`ArrayAsSingle` `false` olduğunda motor `["Alice","Bob"]` ifadesini iki ayrı değer olarak yorumlar ve yan yana satırlara yazar. `true` yapıldığında dize atomik bir değer olarak ele alınır; bu, Excel içinde JSON formatının korunması için kritiktir.

---

## Adım 4: Yapılandırılmış Seçeneklerle Smart Marker’ları İşleyin

Şimdi, az önce yapılandırdığınız seçenek nesnesini geçirerek Smart Marker motorunu çalıştırın.

```csharp
// Process smart markers using the custom options
workbook.ProcessSmartMarkers(smartMarkerOptions);
```

İşleme sırasında Aspose.Cells `dataTable`’ı okur, marker’ları uygular ve `ArrayAsSingle` bayrağına saygı göstererek JSON dizisini dokunulmaz bırakır.

---

## Adım 5: Çalışma Kitabını Kaydedin ve Sonucu Doğrulayın

Son olarak, çalışma kitabını diske yazın. Oluşturulan dosyayı Excel ya da herhangi bir elektronik tablo görüntüleyicide açarak **A2** hücresinin tam JSON dizesini içerdiğini doğrulayın.

```csharp
// Save the resulting workbook
string outputPath = @"C:\Temp\SmartMarkerJson.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### Beklenen çıktı

| A   |
|-----|
| **["Alice","Bob"]** |

**A2** hücresi, `DataTable`’da depolandığı gibi JSON dizisini tek bir metin değeri olarak gösterir. Ek satır oluşturulmaz.

---

## Yaygın varyasyonlar ve kenar‑durumları

| Durum | Nasıl uyarlamalı |
|-----------|--------------|
| **JSON dizileri içeren birden fazla satır** | Aynı `ArrayAsSingle` ayarı geçerlidir; her satırın JSON dizisi kendi hücresinde kalır. |
| **Farklı JSON yapıları (nesneler, iç içe diziler)** | JSON bir dize olduğu sürece `ArrayAsSingle` bütünlüğünü korur. Karmaşık nesneler için tırnakları kaçırmanız gerekebilir. |
| **Farklı bir veri kaynağı kullanmak (ör. List\<T\>)** | `DataTable` yerine herhangi bir enumerable koleksiyonla değiştirin; işaretçi sözdizimi (`&=myList.Property`) aynı kalır. |
| **XLSX yerine CSV’ye dışa aktarma** | `ArrayAsSingle` hâlâ geçerlidir, ancak CSV hücre biçimlendirmesini korumaz; JSON’u tırnak içinde sarmanız gerekebilir. |

**İpucu:** `ProcessSmartMarkers` çağrısından **önce** `ArrayAsSingle`’ı ayarlamayı unutmayın. Bayrağı işlemden sonra değiştirmek, zaten oluşturulmuş hücreleri etkilemez.

---

## Tam, çalıştırılabilir örnek

Aşağıda, bir konsol uygulamasına kopyalayıp yapıştırabileceğiniz tam program yer alıyor. Tüm `using` yönergeleri ve açıklayıcı yorumlar dahildir.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the data source with a JSON array
            DataTable dataTable = new DataTable();
            dataTable.Columns.Add("Id", typeof(int));
            dataTable.Columns.Add("Names", typeof(string));
            dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");

            // 2️⃣ Build a workbook and place smart markers
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Cells["A1"].PutValue("&=dataTable");          // whole table (optional)
            worksheet.Cells["A2"].PutValue("&=dataTable.Names");   // Names column

            // 3️⃣ Configure SmartMarkerOptions to treat arrays as single values
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 4️⃣ Process the markers with the custom options
            workbook.ProcessSmartMarkers(options);

            // 5️⃣ Save the file
            string path = @"C:\Temp\SmartMarkerJson.xlsx";
            workbook.Save(path);
            Console.WriteLine($"Workbook saved to {path}");
        }
    }
}
```

Programı çalıştırın, `SmartMarkerJson.xlsx` dosyasını açın; JSON dizisinin **A2** hücresinde korunduğunu göreceksiniz.

---

## Sonuç

C#’ta Aspose.Cells akıllı marker’ları kullanırken JSON dizisini tek bir hücre değeri olarak tutmak için **SmartMarkerOptions ArrayAsSingle**’ı nasıl yapılandıracağınızı öğrendiniz. `DataTable` hazırlama, marker ekleme, `ArrayAsSingle` bayrağını ayarlama, işleme ve kaydetme adımları, Excel içinde kompakt JSON temsili gerektiren her senaryoya uygulanabilecek tekrar edilebilir bir desen oluşturur.

Sonraki adımlarda şunları keşfedebilirsiniz:

* **Aspose.Cells smart markers** ile koleksiyonlar üzerinde döngü oluşturma.
* Hücre biçimlendirmesini özelleştirerek **iç içe JSON nesneleri** dışa aktarma.
* Daha zengin raporlar için **koşullu biçimlendirme** ile smart marker’ları birleştirme.

Farklı veri yapılarıyla denemeler yapın ve bulgularınızı paylaşın. Kodlamanın tadını çıkarın!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve ilgili konuları ayrıntılı olarak ele alan tam çalışan kod örnekleri içerir.

- [Create Excel Workbook from JSON – Complete Aspose.Cells Guide](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Create Configure Excel Workbook Aspose Cells Net](/cells/hindi/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Create Configure Excel Workbook Aspose Cells Net](/cells/german/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}