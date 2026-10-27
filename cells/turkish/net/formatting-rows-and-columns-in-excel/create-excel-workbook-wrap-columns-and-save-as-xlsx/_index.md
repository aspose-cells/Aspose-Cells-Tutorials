---
category: general
date: 2026-04-07
description: Excel çalışma kitabı oluşturun, Excel'de sütunları kaydırın, formülleri
  hesaplayın ve adım adım C# kodu ile çalışma kitabını XLSX olarak kaydedin.
draft: false
keywords:
- create excel workbook
- wrap columns in excel
- save workbook as xlsx
- how to calculate formulas
- how to save excel
language: tr
og_description: Excel çalışma kitabı oluşturun, Excel'de sütunları kaydırın, formülleri
  hesaplayın ve çalışma kitabını XLSX olarak kaydedin. Çalıştırılabilir kod ile tam
  süreci öğrenin.
og_title: Excel Çalışma Kitabı Oluştur – Tam C# Rehberi
tags:
- csharp
- aspnet
- excel
- automation
title: Excel Çalışma Kitabı Oluştur – Sütunları Kaydır ve XLSX Olarak Kaydet
url: /tr/net/formatting-rows-and-columns-in-excel/create-excel-workbook-wrap-columns-and-save-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel Çalışma Kitabı Oluştur – Sütunları Sar ve XLSX Olarak Kaydet

Programlı olarak **Excel çalışma kitabı oluşturma** ihtiyacı hiç duydunuz mu ve verilerin çok sütunlu bir düzen içinde güzelce sığdırılmasını merak ettiniz mi? Yalnız değilsiniz. Bu öğreticide, çalışma kitabını oluşturmayı, `WRAPCOLS` formülünü **Excel'de sütunları sarmak** için uygulamayı, motoru sonucu hesaplamaya zorlamayı ve sonunda **çalışma kitabını XLSX olarak kaydetmeyi** adım adım göstereceğiz, böylece herhangi bir tablo programında açabilirsiniz.

Ayrıca kaçınılmaz takip sorularını da yanıtlayacağız: *Formülleri anında nasıl hesaplarım?* *Sütun sayısını değiştirmem gerekirse ne olur?* ve *Dosyayı hızlıca kalıcı hale getirmenin bir yolu var mı?* Sonunda, tüm bunları yapan ve kendi projelerinize kopyalayabileceğiniz birkaç ekstra ipucu içeren, bağımsız, çalıştırmaya hazır bir C# kod parçacığına sahip olacaksınız.

## Önkoşullar

- .NET 6.0 veya daha yeni (kod .NET Framework 4.6+ üzerinde de çalışır)
- **Aspose.Cells** kütüphanesi (veya `WRAPCOLS` destekleyen herhangi bir Excel işleme paketi; örnek, basit bir `CalculateFormula` yöntemi sunduğu için Aspose.Cells kullanıyor)
- Biraz C# deneyimi – `Console.WriteLine` yazabiliyorsanız, hazırsınız

> **Pro ipucu:** Henüz Aspose.Cells için bir lisansınız yoksa, web sitelerinden ücretsiz deneme anahtarı talep edebilirsiniz; deneme, öğrenme amaçları için mükemmel çalışır.

## Adım 1: Excel Çalışma Kitabı Oluştur

İhtiyacınız olan ilk şey, Excel dosyasını bellekte temsil eden boş bir çalışma kitabı nesnesidir. Bu, **Excel çalışma kitabı oluşturma** işleminin temelidir.

```csharp
using Aspose.Cells;

// Step 1: Instantiate a new workbook
Workbook workbook = new Workbook();

// Grab the first worksheet – it’s already there by default
Worksheet worksheet = workbook.Worksheets[0];
```

*Neden önemli?* `Workbook` sınıfı, herhangi bir Excel işlemi için giriş noktasıdır. Onu önce oluşturarak, sonraki eylemlerin—örneğin sütunları sarmak—yan etki olmadan uygulanabileceği temiz bir tuval hazırlamış olursunuz.

## Adım 2: Örnek Veri Doldur (İsteğe Bağlı ama Faydalı)

Sütunları sarmadan önce, `A1:D10` aralığına küçük bir veri kümesi ekleyelim. Bu, yeniden şekillendirilmesi gereken ham bir tabloya sahip olduğunuz gerçek bir senaryoyu yansıtır.

```csharp
// Fill A1:D10 with sample numbers for demonstration
for (int row = 0; row < 10; row++)
{
    for (int col = 0; col < 4; col++)
    {
        worksheet.Cells[row, col].PutValue(row * 4 + col + 1);
    }
}
```

Eğer çalışma sayfasında zaten veri varsa bu bloğu atlayabilirsiniz; sarma mantığı mevcut herhangi bir aralıkta çalışır.

## Adım 3: Excel'de Sütunları Sar

Şimdi gösterinin yıldızı geliyor: `WRAPCOLS` işlevi. Bir kaynak aralığı ve sütun sayısını alır, ardından verileri yeni düzene yayar. Sonucun üç sütunu kaplaması için **A1** hücresine nasıl uygulanacağını aşağıda görebilirsiniz.

```csharp
// Apply WRAPCOLS to A1 – the result will spill into a 3‑column layout
worksheet.Cells["A1"].Formula = "=WRAPCOLS(A1:D10,3)";
```

**Arka planda ne oluyor?**  
`WRAPCOLS(A1:D10,3)` Excel'e `A1:D10` aralığındaki 40 hücreyi okumasını ve ardından satır satır üç sütuna yazmasını söyler, gerektiği kadar satırı otomatik olarak oluşturur. Bu, uzun bir listeyi daha kompakt, gazete tarzı bir görünüme dönüştürmek için mükemmeldir.

## Adım 4: Formülleri Nasıl Hesaplarım

Bir formül ayarlamak sadece işin yarısıdır; Excel, bir hesaplama geçişi tetiklenene kadar sonucu hesaplamaz. Aspose.Cells'ta bunu `CalculateFormula()` ile yaparsınız.

```csharp
// Force the workbook to evaluate all pending formulas
workbook.CalculateFormula();
```

> **Neden buna ihtiyacınız var:** `CalculateFormula` çağrılmadan, dosyayı açtığınızda `A1` hücresi sadece formül metnini içerir ve sarılmış düzen, bir kullanıcı manuel olarak yeniden hesaplayana kadar görünmez.

## Adım 5: Çalışma Kitabını XLSX Olarak Kaydet

Son olarak, çalışma kitabını diske kalıcı hale getirin. `Save` yöntemi dosya uzantısından formatı otomatik olarak çıkarır, bu yüzden **.xlsx** kullanmak modern Open XML formatını almanızı sağlar.

```csharp
// Choose a folder you have write access to and save the file
string outputPath = @"C:\Temp\output.xlsx";
workbook.Save(outputPath);
```

`output.xlsx` dosyasını Excel'de açtığınızda, orijinal verilerin **A1** hücresinden başlayarak üç sütuna düzgün bir şekilde sarıldığını göreceksiniz. Sayfanın geri kalanı dokunulmaz kalır; bu, kaynak tabloyu referans olarak tutmanız gerektiğinde kullanışlıdır.

### Beklenen Sonuç Ekran Görüntüsü

<img src="images/wrapcols-result.png" alt="excel çalışma kitabı oluşturma örneği" />

Yukarıdaki görsel, son düzeni gösterir: `A1:D10` aralığındaki sayılar artık üç sütun boyunca gösteriliyor ve tüm değerleri sığdırmak için satırlar otomatik olarak oluşturuluyor.

## Yaygın Varyasyonlar ve Kenar Durumları

### Sütun Sayısını Değiştirme

Farklı bir sütun sayısına ihtiyacınız varsa, sadece `WRAPCOLS`'in ikinci argümanını ayarlayın:

```csharp
worksheet.Cells["A1"].Formula = "=WRAPCOLS(A1:D10,5)"; // five‑column layout
```

Her değişiklikten sonra `CalculateFormula()`'ı yeniden çalıştırmayı unutmayın.

### Ayrık Aralıkları Sarma

`WRAPCOLS` yalnızca bitişik aralıklarla çalışır. Kaynak veriniz birden fazla alana dağılmışsa, sarmadan önce önce birleştirin (ör. yardımcı bir sütunda `UNION` kullanarak).

### Büyük Veri Setleri

Çok büyük tablolar için hesaplama birkaç saniye sürebilir. Formülü ayarlamadan önce otomatik hesaplamayı devre dışı bırakarak ve ardından yeniden etkinleştirerek performansı artırabilirsiniz:

```csharp
workbook.Settings.CalcMode = CalcMode.Manual;
worksheet.Cells["A1"].Formula = "=WRAPCOLS(A1:D1000,4)";
workbook.CalculateFormula();
workbook.Settings.CalcMode = CalcMode.Automatic;
```

### Bir Akıma Kaydetme

Bir web API'si oluşturuyorsanız ve dosyayı doğrudan istemciye döndürmek istiyorsanız, fiziksel bir dosya yerine bir `MemoryStream`'e yazabilirsiniz:

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
ms.Position = 0; // reset for reading
// return ms as a FileResult in ASP.NET Core, for example
```

## Tam Çalışan Örnek

Her şeyi bir araya getirerek, işte tam, kopyala‑yapıştır‑hazır program:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Fill A1:D10 with sample data (optional)
        for (int row = 0; row < 10; row++)
        {
            for (int col = 0; col < 4; col++)
            {
                worksheet.Cells[row, col].PutValue(row * 4 + col + 1);
            }
        }

        // 3️⃣ Apply WRAPCOLS to produce a 3‑column layout
        worksheet.Cells["A1"].Formula = "=WRAPCOLS(A1:D10,3)";

        // 4️⃣ Force calculation so the formula result is materialized
        workbook.CalculateFormula();

        // 5️⃣ Save the workbook as XLSX
        string outputPath = @"C:\Temp\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Bu programı çalıştırın, oluşturulan `output.xlsx` dosyasını açın ve verilerin tam olarak tarif edildiği gibi sarıldığını göreceksiniz.

## Sonuç

Artık C#'ta **Excel çalışma kitabı oluşturma** nesnelerini nasıl oluşturacağınızı, güçlü `WRAPCOLS` işlevini **Excel'de sütunları sarmak** için nasıl uygulayacağınızı, isteğe bağlı **formülleri hesaplayacağınızı** ve **çalışma kitabını XLSX olarak kaydedeceğinizi** biliyorsunuz. Bu uçtan uca akış, basit demolarından üretim‑düzeyi otomasyona kadar en yaygın senaryoları kapsar.

### Sıradaki Adımlar?

- `FILTER`, `SORT` veya `UNIQUE` gibi diğer dinamik dizi işlevleriyle deney yapın.
- Belirli satırları vurgulamak için `WRAPCOLS`'i koşullu biçimlendirme ile birleştirin.
- Bu mantığı bir ASP.NET Core uç noktasına entegre edin, böylece kullanıcılar tek bir tıklamayla özelleştirilmiş raporu indirebilir.

Sütun sayısını, kaynak aralığını veya çıktı yolunu kendi proje ihtiyaçlarınıza göre değiştirmekten çekinmeyin. Herhangi bir sorunla karşılaşırsanız, aşağıya bir yorum bırakın—iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}