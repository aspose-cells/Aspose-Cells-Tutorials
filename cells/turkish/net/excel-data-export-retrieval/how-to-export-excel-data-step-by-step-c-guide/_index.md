---
category: general
date: 2026-03-29
description: C# kullanarak Excel tablolarını düz metne dışa aktarmayı, dizeyi dosyaya
  yazmayı ve Excel tablosunu CSV veya TXT'ye dönüştürmeyi öğrenin. Tam kod ve ipuçları
  içerir.
draft: false
keywords:
- how to export excel
- write string to file
- convert excel table
- export table as csv
- save txt file c#
language: tr
og_description: C#'ta Excel tablolarını metin dosyalarına nasıl dışa aktarılır? Excel
  tablolarını dönüştürme ve TXT dosyalarını kaydetme konusunda tam çözüm, kod ve en
  iyi uygulamaları edinin.
og_title: Excel Verilerini Nasıl Dışa Aktarılır – Tam C# Öğreticisi
tags:
- C#
- Excel
- File I/O
title: Excel Verilerini Nasıl Dışa Aktarırsınız – Adım Adım C# Rehberi
url: /tr/net/excel-data-export-retrieval/how-to-export-excel-data-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel Verilerini Dışa Aktarma – Tam C# Rehberi

Excel verilerini manuel olarak elektronik tabloyu açmadan dışa aktarmayı hiç merak ettiniz mi? Belki eski bir sistem için bir tabloyu basit bir metin dosyasına dökmeniz gerekiyor ya da veri analizi boru hatları için hızlı bir CSV dışa aktarımı istiyorsunuz. Bu öğreticide, **bir dizeyi dosyaya yazma** işlemini içeren pratik, uçtan uca bir çözümü adım adım gösterecek ve C# kullanarak **Excel tablosunu** sınırlı bir metin formatına nasıl dönüştüreceğinizi anlatacağız.

Çalışma kitabını yüklemekten, doğru tabloyu seçmeye, dışa aktarma seçeneklerini yapılandırmaya ve sonunda sonucu bir `.txt` dosyası olarak kaydetmeye kadar her şeyi ele alacağız. Sonunda **tabloyu CSV olarak dışa aktarabilir** (veya seçtiğiniz herhangi bir ayırıcıyı kullanabilirsiniz) ve **C# txt dosyası kaydetme** projeleri için birkaç kullanışlı ipucu da göreceksiniz. Harici araçlara gerek yok—sadece birkaç NuGet paketi ve bir miktar kod yeterli.

---

## What You’ll Need

- **.NET 6.0+** (veya klasik tercih ediyorsanız .NET Framework 4.7.2)
- **Syncfusion.XlsIO** NuGet paketi (`ExportTableOptions` sınıfı burada bulunur)
- Temel bir C# IDE'si (Visual Studio, VS Code, Rider—herhangi biri işe yarar)
- En az bir tablo içeren bir Excel çalışma kitabı (örnekte `ws.Tables[0]` kullanacağız)

> Pro ipucu: Syncfusion kütüphaneniz yoksa, komut satırından  
> `dotnet add package Syncfusion.XlsIO.Net.Core` komutunu çalıştırın.

---

## Step 1 – Open the Workbook and Grab the First Table  

İlk olarak Excel dosyasını yükleyip tabloyu içeren çalışma sayfasına bir referans almanız gerekir. Bu adım, **excel tablosunu dönüştürme** işleminin ham hücre aralıkları yerine bir `ITable` nesnesi üzerinde çalıştığı için kritiktir.

```csharp
using Syncfusion.XlsIO;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        // Load the workbook (replace with your actual file path)
        using (ExcelEngine excelEngine = new ExcelEngine())
        {
            IApplication application = excelEngine.Excel;
            application.DefaultVersion = ExcelVersion.Xlsx;

            // Open the file
            FileStream stream = new FileStream(@"C:\Data\Sample.xlsx", FileMode.Open, FileAccess.Read);
            IWorkbook workbook = application.Workbooks.Open(stream);
            IWorksheet ws = workbook.Worksheets[0];   // First worksheet
```

*Neden önemli:* Çalışma kitabını `using` ile açmak, tüm yönetilmeyen kaynakların serbest bırakılmasını sağlar ve daha sonra **dizeyi dosyaya yazma** girişiminde dosya kilidi sorunlarını önler.

## Step 2 – Configure Export Options (Plain Text, No Headers, Semicolon Delimiter)  

Şimdi Syncfusion'a tablonun nasıl serileştirileceğini söylüyoruz. `ExportTableOptions` başlık eklemeyi açıp kapatmanıza, bir ayırıcı seçmenize ve bir dize mi yoksa bayt dizisi mi alacağınıza karar vermenizi sağlar.

```csharp
            // Step 2: Configure export options – plain text, omit headers, ';' delimiter
            var exportOptions = new ExportTableOptions
            {
                ExportAsString = true,      // Returns a string we can write directly
                IncludeHeaders = false,     // Skip column headers if you don’t need them
                Delimiter = ";"             // Change to ',' for classic CSV
            };
```

*Neden önemli:* `IncludeHeaders = false` ayarı, genellikle sütun sırasını zaten bilen alttaki sistemlerin beklentileriyle eşleşir. Ayırıcıyı değiştirmek, **tabloyu CSV olarak dışa aktarma** işlemini özel bir ayırıcıyla yapmanın yoludur.

## Step 3 – Export the Table to a String  

Seçenekler hazır olduğunda `ExportToString` metodunu çağırıyoruz. Bu yöntem tüm tabloyu (tüm satırları dahil) alır ve dosya çıktısı için hazır tek bir dize döndürür.

```csharp
            // Step 3: Export the first table to a string using the configured options
            ITable firstTable = ws.Tables[0];               // Access the first table
            string tableText = firstTable.ExportToString(exportOptions);
```

*Neden önemli:* `ExportToString` çağrısı, Excel ızgarasını sınırlı bir formata dönüştürmenin zor işini yapar. Ayarladığınız `Delimiter` değerine saygı gösterir, böylece ekstra işleme gerek kalmadan temiz bir **tabloyu csv olarak dışa aktar** sonucu elde edersiniz.

## Step 4 – Write the Exported Text to a File  

Son olarak, dizeyi diske kaydediyoruz. `File.WriteAllText`, **C# txt dosyası kaydetme** için en basit yoldur; dosya yoksa otomatik olarak oluşturur, varsa üzerine yazar.

```csharp
            // Step 4: Write the exported text to a file
            string outputPath = @"C:\Data\ExportedTable.txt";
            File.WriteAllText(outputPath, tableText);
            System.Console.WriteLine($"Table exported successfully to {outputPath}");
        }
    }
}
```

*Neden önemli:* Dizeyi doğrudan yazarak ekstra bir dönüşüm adımından kaçınırsınız. Dosya artık `Value1;Value2;Value3` gibi satırlar içerir ve herhangi bir alttaki ayrıştırıcı için hazırdır.

## Full Working Example (All Steps in One Place)  

Aşağıda, tartıştığımız her şeyi birleştiren, kopyala‑yapıştır hazır tam program bulunmaktadır. Hata yönetimi ve açıklayıcı yorumlar içerir.

```csharp
using Syncfusion.XlsIO;
using System;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load workbook and get first worksheet
            using (ExcelEngine excelEngine = new ExcelEngine())
            {
                IApplication app = excelEngine.Excel;
                app.DefaultVersion = ExcelVersion.Xlsx;

                string sourcePath = @"C:\Data\Sample.xlsx";
                using (FileStream fs = new FileStream(sourcePath, FileMode.Open, FileAccess.Read))
                {
                    IWorkbook wb = app.Workbooks.Open(fs);
                    IWorksheet ws = wb.Worksheets[0]; // first sheet

                    // 2️⃣ Set export options (plain text, no headers, ';' delimiter)
                    var opts = new ExportTableOptions
                    {
                        ExportAsString = true,
                        IncludeHeaders = false,
                        Delimiter = ";"
                    };

                    // 3️⃣ Export the first table to a string
                    ITable table = ws.Tables[0];
                    string csvText = table.ExportToString(opts);

                    // 4️⃣ Save the string to a .txt file
                    string destPath = @"C:\Data\ExportedTable.txt";
                    File.WriteAllText(destPath, csvText);

                    Console.WriteLine($"✅ Export complete! File saved at: {destPath}");
                }
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }
}
```

**Beklenen çıktı** (`ExportedTable.txt` dosyasının içeriği):

```
John;Doe;35
Jane;Smith;28
Bob;Brown;42
```

Her satır, orijinal Excel tablosundan bir satıra karşılık gelir ve değerler noktalı virgül ile ayrılır. `Delimiter = ","` değiştirirseniz klasik bir CSV dosyası elde edersiniz.

## Common Questions & Edge Cases  

### What if My Workbook Has Multiple Tables?  
`ws.Tables[0]` ifadesini uygun indekse değiştirerek ya da `ws.Tables` üzerinde döngü kurarak birden fazla tabloyla çalışabilirsiniz:

```csharp
foreach (var tbl in ws.Tables)
{
    string txt = tbl.ExportToString(opts);
    // Save each table to a separate file or concatenate as needed
}
```

### How Do I Include Column Headers?  
`ExportTableOptions` içinde `IncludeHeaders = true` olarak ayarlayın. Bu, alttaki sistem bir başlık satırı beklediğinde faydalıdır.

### Can I Export to a Different Folder Dynamically?  
Kesinlikle. Çözümü daha esnek hale getirmek için `Path.Combine` ile `Environment.GetFolderPath(Environment.SpecialFolder.Desktop)` ya da kullanıcı tarafından sağlanan herhangi bir yolu kullanabilirsiniz.

### What About Large Files?  
Büyük tablolar için, tüm dizeyi belleğe yüklemek yerine çıktıyı akış olarak göndermeyi düşünün:

```csharp
using (StreamWriter writer = new StreamWriter(outputPath))
{
    writer.Write(table.ExportToString(opts));
}
```

### Does This Work on .NET Core?  
Evet—Syncfusion.XlsIO .NET 5/6/7'yi destekler. Uygun NuGet paketini referans gösterin, yeter.

## Pro Tips for Reliable Exports  

- **Dosya yolunu** yazmadan önce doğrulayın. Eksik bir dizin `DirectoryNotFoundException` hatası verir.  
- Tablo bellekte rahatça sığdığında **`ExportAsString`** kontrol edin; aksi takdirde büyük veri setleri için `ExportToStream` kullanın.  
- **Kültüre dikkat edin**: Veriniz ondalık ayırıcı olarak virgül içeriyorsa, CSV ayrıştırma hatalarını önlemek için noktalı virgül (`;`) ya da sekme (`\t`) ayırıcı seçin.  
- **Sürüm kilidi**: Syncfusion zaman zaman API imzalarını değiştirir. Derlemenizin tekrarlanabilir olmasını sağlamak için NuGet sürümünü sabitleyin (`<PackageReference Include="Syncfusion.XlsIO.Net.Core" Version="21.2.0.44" />`).

## Conclusion  

Bu rehberde, C# kullanarak **Excel** tablolarını düz metin dosyalarına nasıl dışa aktaracağınızı gösterdik. Çalışma kitabını yükleyip, `ExportTableOptions` yapılandırarak, tabloyu bir dizeye dışa aktararak ve sonunda **dizeyi dosyaya yazarak**, artık **excel tablosunu dönüştürme**, **tabloyu csv olarak dışa aktarma** ve **C# txt dosyası kaydetme** görevleri için sağlam bir deseniniz var.

Denemekten çekinmeyin—ayırıcıyı değiştirin, başlıkları ekleyin ya da birden fazla tablo üzerinde döngü kurun. Aynı yaklaşım CSV raporları oluşturmak, veriyi eski ayrıştırıcılara beslemek veya sadece elektronik tablo içeriklerini hafif metin dosyaları olarak arşivlemek için de işe yarar.

Ele almak istediğiniz başka senaryolar var mı? Belki **dizeyi dosyaya asenkron olarak yazma** ihtiyacınız var ya da çıktıyı anında sıkıştırmak istiyorsunuz. *C#'ta asenkron dosya I/O* ve *.NET ile dosya sıkıştırma* konulu sonraki öğreticilerimize göz atın ve ilerlemeyi sürdürün.

Kodlamanın tadını çıkarın! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}