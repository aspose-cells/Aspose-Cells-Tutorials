---
category: general
date: 2026-03-29
description: GridJs'te satır eklemeyi hızlı bir şekilde öğrenin. Bu kılavuz ayrıca
  satır eklemeyi ve toplu işlemle birden fazla satır eklemeyi de kapsar.
draft: false
keywords:
- how to insert rows
- how to add rows
- add multiple rows grid
- batch row insertion
- large grid performance
language: tr
og_description: GridJs'de satır eklemeyi hızlı bir şekilde öğrenin. Bu rehber, satır
  eklemeyi, birden fazla satır eklemeyi ve büyük toplu eklemeleri nasıl yöneteceğinizi
  gösterir.
og_title: GridJs'te Satır Ekleme – Çoklu Satırları Etkili Bir Şekilde Ekleyin
tags:
- GridJs
- C#
- data‑grid
title: GridJs'de Satır Ekleme – Çoklu Satırları Verimli Bir Şekilde Ekleyin
url: /tr/net/row-and-column-management/how-to-insert-rows-in-gridjs-add-multiple-rows-grid-efficien/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GridJs'de Satır Ekleme – Grid'de Çoklu Satırları Verimli Şekilde Ekleyin

Hiç **satır ekleme**'nin dev bir GridJs tablosunda UI'yı dondurmadan nasıl yapılacağını merak ettiniz mi? Belki **satır ekleme**'yi tek tek yapmaya çalışırken bir duvara çarptınız ve performans tamamen çöküyor. İyi haber şu ki GridJs, tek bir çağrıda **grid'de çoklu satır ekleme** yapmanızı sağlayan bir batch API sunuyor, böylece milyonlarca kayıtla çalışırken bile sistem hızlı kalıyor.

Bu öğreticide, `InsertRowsBatch` kullanarak **satır ekleme**'nin tam olarak nasıl yapılacağını gösteren eksiksiz, çalıştırılabilir bir örnek üzerinden adım adım ilerleyeceğiz. Batch işlemenin neden önemli olduğunu, sonucu nasıl doğrulayacağınızı ve hedeflediğiniz indeks çok büyük olduğunda nelere dikkat etmeniz gerektiğini göreceksiniz. Sonuna geldiğinizde, herhangi bir GridJs örneğine bin yeni kaydı güvenle ekleyebileceksiniz.

## Önkoşullar

- .NET 6.0 veya üzeri (kod, herhangi bir yeni SDK ile derlenebilir)
- `GridJs` NuGet paketine referans (veya özel bir derleme kullanıyorsanız DLL)
- Temel C# bilgisi – uzman olmanıza gerek yok, sadece sınıflar ve metodlarla rahat olmanız yeterli
- Seçtiğiniz bir IDE veya editör (Visual Studio, Rider, VS Code… hepsi çalışır)

> **Pro tip:** Gerçekten devasa grid'lerle (onlarca milyon satır) çalışmayı planlıyorsanız, UI render'ını hafif tutmak için `gridJs.EnableVirtualization = true;`'yi etkinleştirin.

## Adım 1: GridJs Örneğini Oluşturun ve Yapılandırın

İlk olarak: canlı bir `GridJs` nesnesine ihtiyacınız var. Bunu, satırları çizeceğiniz bir tuval gibi düşünün.

```csharp
using System;
using GridJsLibrary;   // Assume this is the namespace for GridJs

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Initialize the grid
            GridJs gridJs = new GridJs();

            // Optional: turn on virtualization for huge data sets
            gridJs.EnableVirtualization = true;

            // Populate the grid with some dummy data so we can see the effect
            SeedInitialData(gridJs);

            // Now we’re ready to insert rows in bulk
            InsertRowsInBatch(gridJs);
        }

        // Helper: add 2 000 000 rows so our batch lands at index 2 000 001
        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }
```

> **Neden bu adım önemli:** Grid'i başlatmak ve isteğe bağlı olarak veri eklemek, grid'in zaten büyük miktarda bilgi tuttuğu gerçek bir senaryoyu yansıtır. Daha sonra yapacağımız batch ekleme, sıfır‑tabanlı indeksi göz önünde bulundurmalıdır; bu yüzden tam ekleme noktasını göstermek için önceden veri dolduruyoruz.

## Adım 2: `InsertRowsBatch` Kullanarak **Grid'de Çoklu Satır Ekleyin**

Şimdi öğretinin çekirdeği – toplu olarak **satır ekleme** yapan çağrı. Metod imzası `InsertRowsBatch(int startIndex, int count)`. Örneğimizde, 2 000 000 indeksinden (2 000 001. satıra karşılık gelir) başlayarak on satır ekleyeceğiz.

```csharp
        // Step 2 – Insert a batch of rows
        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based, so this is row 2 000 001
            int rowsToAdd = 10;

            // The batch call creates placeholder rows; you can later populate them
            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Verify by reading back a few rows
            VerifyInsertion(grid, startIndex, rowsToAdd);
        }
```

> **Nasıl çalışır:** `InsertRowsBatch`, istenen sayıda satırı dahili olarak ayırır ve mevcut satırları aşağı kaydırır. İşlem tek bir işlemde gerçekleştiği için UI yalnızca bir kez yenilenir; bu yüzden bu metod, **satır ekleme**'yi verimli bir şekilde yapmanın önerilen yoludur.

## Adım 3: Ekleme İşlemini Doğrulayın – Satırlar Beklenen Yerde mi?

Batch işlemi sonrasında satırların düşündüğünüz yerde olduğundan emin olmak isteyeceksiniz. Aşağıdaki yardımcı, yeni eklenen bloğun ilk ve son satırlarını okur ve konsola yazdırır.

```csharp
        // Step 3 – Simple verification
        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

**Beklenen çıktı**

```
Initial seed completed – 2 000 000 rows present.
Inserted 10 rows starting at index 2000001.
Verifying inserted rows:
Row 2000001: , 
Row 2000002: , 
...
Row 2000010: , 
```

Boş hücreler, satırların veri bekleyen yer tutucular olduğunu gösterir. Şimdi bunları tek tek doldurabilir veya başka bir batch güncellemesi çalıştırabilirsiniz.

> **Köşe durum notu:** `startIndex` mevcut satır sayısını aşarsa, GridJs yeni satırları otomatik olarak sonuna ekler. Öte yandan, negatif bir indeks `ArgumentOutOfRangeException` hatası fırlatır; bu yüzden kullanıcı tarafından sağlanan indeksleri her zaman doğrulayın.

## Adım 4: Yeni Satırları Doldurun (Opsiyonel ama Yaygın)

Genellikle sadece boş satırlar istemezsiniz; bunları anlamlı değerlerle doldurmanız gerekir. Yeni oluşturulan aralık üzerinde döngü yaparak `SetCell` ya da benzeri bir API'yi çağırabilirsiniz.

```csharp
        // Optional: fill the newly added rows with sample data
        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }
```

Satırları hemen görüntülenebilir hâle getirmek istiyorsanız, batch eklemeden hemen sonra `PopulateNewRows(gridJs, startIndex, rowsToAdd);` çağrısını yapabilirsiniz.

## Adım 5: Çok Büyük Grid'ler İçin Performans İpuçları

Milyonlarca **grid'de çoklu satır ekleme** ile uğraşırken, şu ipuçlarını aklınızda bulundurun:

1. **Batch boyutu önemlidir** – 10 000 satırı bir kerede eklemek, her biri 1 000 satır olan on ayrı batch'ten daha hızlı olabilir çünkü her batch tek bir UI yenilemesi oluşturur.
2. **UI güncellemelerini kapatın** – Bazı GridJs sürümleri `grid.SuspendLayout()` / `grid.ResumeLayout()` sağlar. Gecikme fark ederseniz batch'inizi bu çağrıların içine alın.
3. **Sanalizasyonu kullanın** – Daha önce gösterildiği gibi, `EnableVirtualization` bellek tüketimini ve render süresini büyük ölçüde azaltır.
4. **Derin kopyalardan kaçının** – Grid'e basit değer tipleri veya hafif nesneler gönderin; ağır nesneler grid'in veriyi kopyalamasına neden olur ve performansı düşürür.

## Tam Çalışan Örnek

Her şeyi bir araya getirerek, yeni bir konsol projesine kopyalayıp yapıştırabileceğiniz tam program aşağıdadır:

```csharp
using System;
using GridJsLibrary;   // Replace with the actual namespace of your GridJs library

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            GridJs gridJs = new GridJs
            {
                EnableVirtualization = true
            };

            SeedInitialData(gridJs);
            InsertRowsInBatch(gridJs);
        }

        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }

        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based index for row 2 000 001
            int rowsToAdd = 10;

            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Optional: fill them with data
            PopulateNewRows(grid, startIndex, rowsToAdd);

            VerifyInsertion(grid, startIndex, rowsToAdd);
        }

        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }

        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

Programı çalıştırın; konsol çıktısının on satırın doğru konuma eklendiğini ve ardından doldurulduğunu onayladığını göreceksiniz.

## Sonuç

Batch API kullanarak GridJs'de **satır ekleme**'yi ele aldık, **satır ekleme**'yi verimli bir şekilde gösterdik ve UI'yı yavaşlatmadan **grid'de çoklu satır ekleme** yollarını inceledik. Temel çıkarımlar şunlardır:

- `InsertRowsBatch(startIndex, count)`'i herhangi bir toplu işlem için kullanın.
- İndeksleri doğrulayın ve büyük veri setleri için sanalizasyonu düşünün.
- Acil içerik gerekiyorsa batch'ten sonra satırları doldurun.

Sonra, **satır silme**'yi keşfetmek, batch düzenlemeler için **geri al/yeniden yap** işlevini uygulamak veya GridJs'i talep üzerine veri akışı sağlayan bir back‑end servisiyle entegre etmek isteyebilirsiniz. Bu konular, az önce öğrendiğiniz kavramların üzerine doğrudan inşa edilir.

Deney yapmaktan çekinmeyin—batch boyutunu değiştirin, grid'in en başına eklemeyi deneyin veya tek bir işlemde birden fazla batch'i birleştirin. Ne kadar çok oynarsanız, büyük 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}