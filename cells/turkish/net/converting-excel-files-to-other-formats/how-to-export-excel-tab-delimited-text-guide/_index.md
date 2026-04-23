---
category: general
date: 2026-02-26
description: C# kullanarak Excel'i sekme‑ayraçlı bir txt dosyasına nasıl dışa aktarılır.
  Excel'i sekme olarak dışa aktarmayı, Excel'i txt'ye dönüştürmeyi ve Excel'i ayırıcıyla
  dışa aktarmayı üç kolay adımda öğrenin.
draft: false
keywords:
- how to export excel
- export excel as tab
- convert excel to txt
- export excel with delimiter
- export excel range
language: tr
og_description: C# kullanarak Excel'i sekme‑ayırmalı bir txt dosyasına nasıl dışa
  aktarılır. Bu öğreticide Excel'i sekme olarak dışa aktarma, Excel'i txt'ye dönüştürme
  ve Excel'i ayırıcıyla dışa aktarma gösterilmektedir.
og_title: Excel'i nasıl dışa aktarılır – Sekmeli Metin Kılavuzu
tags:
- csharp
- excel
- file-conversion
title: Excel'i nasıl dışa aktarılır – Sekme Ayrımlı Metin Kılavuzu
url: /tr/net/converting-excel-files-to-other-formats/how-to-export-excel-tab-delimited-text-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'i dışa aktarma – Tam C# Öğreticisi

Hiç **how to export excel** verilerini biçim kaybı olmadan düz‑metin dosyasına aktarmayı merak ettiniz mi? Belki bir veri‑hattı için hızlı bir TSV (tab‑separated values) ihtiyacınız var ya da yalnızca `.txt` okuyan eski bir sisteme veri gönderiyorsunuz. Her iki durumda da yalnız değilsiniz—geliştiriciler elektronik tablolardan veri çıkartırken sürekli bu duvara çarpıyor.

İyi haber? Sadece üç basit adımda **export excel as tab**‑delimited metin, **convert excel to txt** yapabilir ve daha sonra fikrinizi değiştirirseniz özel bir ayırıcı seçebilirsiniz. Aşağıda tamamen çalıştırılabilir bir C# örneği, her satırın neden önemli olduğu ve yaygın tuzaklardan kaçınmak için birkaç ipucu göreceksiniz.

> **Pro tip:** Bu yaklaşım popüler Aspose.Cells kütüphanesiyle çalışır, ancak kavramlar `ExportTable`‑style metodunu sunan herhangi bir .NET Excel API'sine de uygulanabilir.

## Gereksinimler

- **.NET 6+** (veya .NET Framework 4.6+). Kod, herhangi bir yeni çalışma zamanında derlenir.
- **Aspose.Cells for .NET** (ücretsiz deneme veya lisanslı). NuGet üzerinden kurun: `dotnet add package Aspose.Cells`.
- `input.xlsx` adlı bir giriş çalışma kitabı, kontrol ettiğiniz bir klasöre yerleştirilmiş.
- Biraz merak—Excel iç yapıları hakkında derin bilgi gerekmez.

Eğer bunlara sahipseniz, doğrudan çözüme geçelim.

## Adım 1 – Dışa Aktarmak İstediğiniz Çalışma Kitabını Yükleyin

İlk olarak kaynak dosyaya işaret eden bir `Workbook` nesnesi oluştururuz. Bu nesne, tüm çalışma sayfaları, adlandırılmış aralıklar ve biçimlendirme dahil olmak üzere tüm Excel dosyasını temsil eder.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook that contains the data to export
Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
```

*Neden Önemli:*  
Çalışma kitabını yüklemek, çalışma sayfası koleksiyonuna (`workbook.Worksheets`) erişim sağlar. Bu nesne olmadan hücrelere, aralıklara veya dışa aktarma ayarlarına ulaşamazsınız.  

> **Not:** Dosyanız bir ağ paylaşımında bulunuyorsa, başına `\\` ekleyin veya bir UNC yolu kullanın—Aspose.Cells bunu sorunsuz yönetir.

## Adım 2 – Dışa Aktarma Seçeneklerini Yapılandırın (String Değerleri ve Tab Ayırıcı)

Şimdi kütüphaneye verilerin nasıl yazılacağını söylüyoruz. `ExportAsString = true` ayarlayarak her hücreyi düz bir string olarak ele alıyoruz; bu, Excel'in bölgeye özgü sayı biçimlerini ortadan kaldırır. `Delimiter = "\t"` kısmı **export excel as tab** ifadesinin kalbidir.

```csharp
// Step 2: Configure the export options – export values as strings and use a tab delimiter
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,   // ensures numbers become plain text, not scientific notation
    Delimiter = "\t"         // tab character – perfect for TSV files
};
```

*Neden Önemli:*  
`ExportAsString`'i atlamanız durumunda, `12345` içeren bir hücre bazı bölgelerde `12,345` haline gelebilir ve sonraki ayrıştırıcıları bozabilir. Ayırıcı, daha sonra **export excel with delimiter** bir sekme dışındaki bir karakterle (virgül, boru `|` vb.) değiştirilebilir.

## Adım 3 – Belirli Bir Aralığı Metin Dosyasına Dışa Aktarın

Son olarak, ilgilendiğimiz aralığı (`A1:D10` bu örnekte) seçip `out.txt` dosyasına yazıyoruz. `ExportTable` metodu tüm işi yapar: hücreleri okur, seçenekleri uygular ve sonucu diske akıtır.

```csharp
// Step 3: Export the range A1:D10 from the first worksheet to a text file
Worksheet sheet = workbook.Worksheets[0]; // first worksheet (index 0)
sheet.Cells.ExportTable("A1", "D10", @"C:\Data\out.txt", exportOptions);
```

Bu çalıştıktan sonra, `out.txt` içinde şu şekilde bir içerik bulacaksınız:

```
Name    Age    City    Score
Alice   30     NY      85
Bob     25     LA      90
...
```

Her sütun bir **tab** ile ayrılmıştır, bu da `awk`, `PowerShell` veya sekmeleri tanıyan herhangi bir CSV‑uyumlu araç için hazırdır.

### Hızlı Doğrulama

Oluşturulan dosyayı bir düz metin düzenleyicide (Notepad, VS Code) açın ve doğrulayın:

1. “Show whitespace” (Boşlukları göster) seçeneğini etkinleştirdiğinizde sütunlar hizalanır.
2. Fazladan tırnak işareti veya virgül bulunmaz.
3. Tüm sayısal hücreler, Excel'de olduğu gibi tam olarak görünür (`ExportAsString` sayesinde).

Bir şey yanlış görünüyorsa, kaynak çalışma kitabının satır/sütunları gizlemediğini iki kez kontrol edin ve doğru çalışma sayfası indeksine başvurduğunuzdan emin olun.

## Yaygın Varyasyonlar ve Kenar Durumları

### Tüm Çalışma Sayfasını Dışa Aktarma

Eğer tüm sayfayı kapsayan bir **export excel range** yapmak istiyorsanız, `sheet.Cells.MaxDisplayRange` kullanabilirsiniz:

```csharp
var maxRange = sheet.Cells.MaxDisplayRange;
sheet.Cells.ExportTable(maxRange.FirstRow, maxRange.FirstColumn,
                       maxRange.RowCount, maxRange.ColumnCount,
                       @"C:\Data\fullSheet.txt", exportOptions);
```

### Farklı Bir Ayırıcı Kullanma

Sekmeden boruya (`|`) geçmek, sadece bir satırı değiştirmek kadar kolaydır:

```csharp
exportOptions.Delimiter = "|"; // now we have a pipe‑delimited file
```

Bu, başka bir kodu yeniden yazmadan **export excel with delimiter** senaryosunu karşılar.

### Büyük Dosyaları İşleme (> 100 MB)

Büyük çalışma kitapları için, her şeyi belleğe yüklemekten kaçınmak amacıyla dışa aktarmayı akış olarak yapın:

```csharp
using (FileStream fs = new FileStream(@"C:\Data\largeOut.txt", FileMode.Create, FileAccess.Write))
{
    sheet.Cells.ExportTable("A1", "Z5000", fs, exportOptions);
}
```

### Tek Seferde Birden Çok Sayfayı Dönüştürme

Birden çok sayfa için **convert excel to txt** yapmanız gerekiyorsa, bunlar üzerinde döngü oluşturun:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string outPath = $@"C:\Data\Sheet{i + 1}.txt";
    workbook.Worksheets[i].Cells.ExportTable("A1", "D10", outPath, exportOptions);
}
```

Her sayfa kendi TSV dosyasını alır—toplu işler için kullanışlıdır.

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda, derlemeye hazır tam program yer alıyor. Dosya yollarını kendi yollarınızla değiştirmeniz yeterli.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook
            string inputPath = @"C:\Data\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // 2️⃣ Set export options – strings + tab delimiter
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                Delimiter = "\t"
            };

            // 3️⃣ Export range A1:D10 from the first worksheet
            Worksheet sheet = workbook.Worksheets[0];
            string outputPath = @"C:\Data\out.txt";
            sheet.Cells.ExportTable("A1", "D10", outputPath, exportOptions);

            Console.WriteLine($"Export complete! Check {outputPath}");
        }
    }
}
```

**Beklenen çıktı:** Her sütunun bir sekme karakteriyle ayrıldığı ve her hücre değerinin Excel'de olduğu gibi tam olarak göründüğü `out.txt` adlı dosya.

## Sık Sorulan Sorular

- **Bu .xls dosyalarıyla çalışır mı?**  
  Evet. Aspose.Cells formatı otomatik algılar, böylece `Workbook`'ı eski bir `.xls` dosyasına yönlendirebilir ve aynı kod geçerli olur.

- **Verilerimde sekmeler varsa ne olur?**  
  Hücre içindeki sekmeler korunur, bu da TSV ayrıştırıcılarını bozabilir. Bu durumda, `exportOptions.Delimiter`'ı güncelleyerek boru (`|`) ayırıcıya geçmeyi düşünün.

- **Değerler yerine formülleri dışa aktarabilir miyim?**  
  `exportOptions.ExportAsString = false` olarak ayarlayın ve `ExportFormula = true` içeren `ExportTableOptions` aşırı yüklemesini kullanın. Çıktı ham formül metnini içerecektir.

- **Gizli satırları atlamanın bir yolu var mı?**  
  Evet. `exportOptions.ExportHiddenRows = false` olarak ayarlayın (varsayılan `true`). Gizli satırlar son metin dosyasından çıkarılacaktır.

## Sonuç

Artık **how to export excel** verilerini sekme‑ayırmalı bir metin dosyası olarak dışa aktarmak, **export excel as tab** yapmak ve **convert excel to txt** için ayırıcılar ve aralık seçimi üzerinde tam kontrol sağlayan sağlam, üretim‑hazır bir tarifiniz var. Aspose.Cells’ `ExportTable` metodunu kullanarak manuel CSV oluşturmayı önler, veri bütünlüğünü korur ve kod tabanınızı temiz tutarsınız.

Bir sonraki zorluk için hazır mısınız? Şunları deneyin:

- Web API'leri için doğrudan bir `MemoryStream`'e dışa aktarma.  
- İlk satırın içeriğine göre dinamik bir başlık satırı ekleme.  
- Bu rutini, yeni Excel yüklemelerini izleyen bir depolama kovasını (storage bucket) izleyen bir Azure Function'a entegre etme.

Deneyin, ayırıcıyı ayarlayın ve verinin ihtiyacınız olan yere akmasını sağlayın. Kodlamanın tadını çıkarın!  

<img src="export-excel.png" alt="how to export excel example" style="max-width:100%; height:auto;" />

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}