---
category: general
date: 2026-02-15
description: C#'ta fontu kopyalama ve hücre stilini uygulama, basit bir örnekle. Hücre
  stilini nasıl alacağınızı ve hücre biçimlendirmesini kullanarak metin kutusu font
  boyutunu nasıl ayarlayacağınızı öğrenin.
draft: false
keywords:
- how to copy font
- apply cell style
- get cell style
- use cell formatting
- set textbox font size
language: tr
og_description: Bir çalışma sayfası hücresinden yazı tipini kopyalayıp hücre stilini
  bir Metin Kutusuna uygulama. Bu rehber, hücre stilini nasıl alacağınızı, hücre biçimlendirmesini
  nasıl kullanacağınızı ve metin kutusu yazı tipi boyutunu nasıl ayarlayacağınızı
  gösterir.
og_title: Excel hücresinden fontu nasıl kopyalarsınız – Tam C# öğreticisi
tags:
- C#
- EPPlus
- UI‑grid
- Excel‑interop
title: Excel hücresinden bir TextBox'a yazı tipini nasıl kopyalarsınız – Adım Adım
  Kılavuz
url: /tr/net/working-with-fonts-in-excel/how-to-copy-font-from-an-excel-cell-to-a-textbox-step-by-ste/
---

placeholders.

Let's craft translation.

Be careful with markdown formatting.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel hücresinden bir TextBox'a yazı tipini kopyalama – Tam C# Öğreticisi

Bir elektronik tablo hücresinden **yazı tipini** kopyalayıp bir UI metin kutusunun aynı şekilde görünmesini istediğiniz oldu mu? Tek başınıza değilsiniz. Birçok raporlama aracı ya da özel gösterge panellerinde Excel’den veri çekip görsel tutarlılığı—yazı tipi ailesi, boyutu ve rengi—korumaya çalışırsınız.  

İyi haber şu ki, sadece birkaç C# satırıyla **hücre stilini alabilir**, yazı tipi özelliklerini okuyabilir ve **hücre stilini** herhangi bir metin‑kutusu kontrolüne **uygulayabilirsiniz**. Bu öğreticide, **hücre biçimlendirmesini** nasıl kullanacağınızı ve hatta programatik olarak **textbox yazı tipi boyutunu** nasıl ayarlayacağınızı gösteren tam, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz.

---

## Öğrenecekleriniz

- Bir ızgara bileşeninden (`gridJs` örneğimizde) bir `TextBox` nesnesinin nasıl alınacağını
- Belirli bir Excel hücresinden (`B2`) yazı tipi ailesi, boyutu ve renginin nasıl okunacağını
- Bu yazı tipi özelliklerinin metin kutusuna nasıl kopyalanacağını, böylece UI elektronik tabloyu yansıtacak
- Yaygın tuzaklar (ör. renk dönüşümü) ve kodunuzun sağlam kalması için birkaç **pro ipucu**
- Konsol uygulaması ya da WinForms projesine doğrudan ekleyebileceğiniz hazır‑çalışır kod parçacığı

**Önkoşullar**  
Şunlara sahip olmalısınız:

1. .NET 6+ (veya .NET Framework 4.8) yüklü  
2. EPPlus NuGet paketi (Excel işleme için)  
3. `TextBoxes` sözlüğünü ortaya çıkaran bir ızgara kontrolü (örnek, kurgusal bir `gridJs` kullanıyor ancak fikir herhangi bir UI kütüphanesiyle çalışır)

Şimdi, işe koyulalım.

---

## Adım 1: Projeyi Oluşturun ve Çalışma Sayfasını Yükleyin

İlk olarak yeni bir konsol ya da WinForms projesi oluşturun ve EPPlus’u ekleyin:

```bash
dotnet add package EPPlus --version 6.*
```

Ardından, çalışma kitabını yükleyin ve stilini kopyalamak istediğiniz hücreyi alın.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System.Drawing;

// ...

// Load the Excel file (make sure the file exists at the given path)
var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
using var package = new ExcelPackage(fileInfo);
ExcelWorksheet ws = package.Workbook.Worksheets["Sheet1"]; // adjust sheet name if needed

// Retrieve the style of cell B2
ExcelStyle cellStyle = ws.Cells["B2"].Style;
```

**Neden önemli:** EPPlus, `Style` nesnesine doğrudan erişim sağlar; bu nesne `Font` alt‑nesnesini içerir. Buradan `Name`, `Size` ve `Color` değerlerini okuyabilirsiniz. Bu, **hücre stilini alma** işleminin çekirdeğidir.

---

## Adım 2: Hedef TextBox'ı Izgaradan Alın

UI ızgaranız (`gridJs`) metin kutularını sütun adıyla anahtarlandırılmış bir sözlükte tutuyorsa, istediğiniz kutuyu şu şekilde alabilirsiniz:

```csharp
// Fake grid class for illustration – replace with your actual grid component
var gridJs = new MyGrid(); // MyGrid is a placeholder for your UI control

// Step 1: Retrieve the "Notes" text box from the grid
var notesTextBox = gridJs.TextBoxes["Notes"];
```

WinForms kullanıyorsanız, `notesTextBox` bir `TextBox` kontrolü olabilir; WPF’de bir `TextBox` öğesi, web‑tabanlı bir ızgarada ise bir JavaScript interop nesnesi olabilir. Önemli olan, manipüle edebileceğiniz bir referansa sahip olmanızdır.

---

## Adım 3: Yazı Tipi Ailesini Aktarın

Kaynak stil ve hedef kontrol elimizde olduğuna göre, yazı tipi ailesini kopyalayalım.

```csharp
// Apply the cell's font family to the text box
notesTextBox.FontFamily = cellStyle.Font.Name;
```

**Pro ipucu:** Tüm UI framework’leri düz bir string kabul eden bir `FontFamily` özelliği sunmaz. WinForms’ta `notesTextBox.Font = new Font(cellStyle.Font.Name, notesTextBox.Font.Size);` şeklinde ayarlarsınız. Kendi ortamınıza göre uyarlayın.

---

## Adım 4: Yazı Tipi Boyutunu Aktarın

Yazı tipi boyutu EPPlus’da bir `float` olarak saklanır. Doğrudan uygulayın:

```csharp
// Apply the cell's font size to the text box
notesTextBox.FontSize = cellStyle.Font.Size;
```

Kontrolünüz puan (point) biriminde çalışıyorsa (çoğu öyle), dönüşüm yapmadan değeri atayabilirsiniz. CSS‑tabanlı ızgaralarda `"pt"` eklemeniz gerekebilir.

---

## Adım 5: Yazı Tipi Rengini Aktarın

Renk dönüşümü en zor kısımdır; EPPlus renkleri ARGB tamsayıları olarak saklarken, birçok UI framework `System.Drawing.Color` ya da bir CSS hex dizesi bekler.

```csharp
// Apply the cell's font colour to the text box
// EPPlus stores colour as a System.Drawing.Color when using .Color property
var excelColor = cellStyle.Font.Color?.GetColor();

// Fallback to black if the cell has no explicit colour
var safeColor = excelColor ?? Color.Black;

// Convert to the format your UI expects (example for WinForms)
notesTextBox.FontColor = safeColor;
```

> **Neden işe yarıyor:** `GetColor()` tema‑tabanlı renkleri çözer ve somut bir `System.Drawing.Color` döndürür. Hücre varsayılan rengi (açıkça ayarlanmamış) kullanıyorsa, null referans hatalarını önlemek için varsayılan olarak siyah alırız.

---

## Tam Çalışan Örnek

Her şeyi bir araya getirdiğimizde, Excel dosyasını okuyan, **B2** hücresinin yazı tipini çıkaran ve bir taklit metin kutusuna uygulayan minimal bir konsol uygulaması aşağıdadır.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System;
using System.Collections.Generic;
using System.Drawing;

namespace FontCopyDemo
{
    // Mock grid control – replace with your real UI component
    public class MyGrid
    {
        public Dictionary<string, TextBoxMock> TextBoxes { get; } = new()
        {
            { "Notes", new TextBoxMock() }
        };
    }

    // Simple text box representation for demonstration
    public class TextBoxMock
    {
        public string FontFamily { get; set; }
        public float FontSize { get; set; }
        public Color FontColor { get; set; }

        public override string ToString()
        {
            return $"FontFamily: {FontFamily}, FontSize: {FontSize}, FontColor: {FontColor.Name}";
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Load Excel worksheet
            var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
            using var package = new ExcelPackage(fileInfo);
            var ws = package.Workbook.Worksheets["Sheet1"];
            var cellStyle = ws.Cells["B2"].Style;

            // 2️⃣ Grab the target TextBox from the grid
            var gridJs = new MyGrid();
            var notesTextBox = gridJs.TextBoxes["Notes"];

            // 3️⃣ Apply font family
            notesTextBox.FontFamily = cellStyle.Font.Name;

            // 4️⃣ Apply font size
            notesTextBox.FontSize = cellStyle.Font.Size;

            // 5️⃣ Apply font colour (with safety net)
            var excelColor = cellStyle.Font.Color?.GetColor();
            notesTextBox.FontColor = excelColor ?? Color.Black;

            // Output the result for verification
            Console.WriteLine("TextBox after copying font:");
            Console.WriteLine(notesTextBox);
        }
    }
}
```

**Beklenen çıktı (B2 Arial, 12 pt, mavi kullanıyorsa):**

```
TextBox after copying font:
FontFamily: Arial, FontSize: 12, FontColor: Blue
```

Programı çalıştırın, UI’nizi açın ve “Notes” metin kutusunun artık **B2** hücresinin tam yazı tipi stilini yansıttığını göreceksiniz. Elle ayarlama yapmanıza gerek kalmadı.

---

## Sık Sorulan Sorular & Kenar Durumları

### Hücre bir tema rengi kullanıyorsa ne olur?

EPPlus’un `GetColor()` tema renklerini otomatik olarak somut bir `System.Drawing.Color` değerine dönüştürür. Ancak, yalnızca tema indeksini döndüren eski bir kütüphane kullanıyorsanız, bu indeksi bir renk paletine kendiniz eşlemeniz gerekir.

### Başka stil özelliklerini (ör. kalın, italik) kopyalayabilir miyim?

Kesinlikle. `ExcelStyle.Font` nesnesi ayrıca `Bold`, `Italic`, `Underline` ve `Strike` özelliklerini sunar. UI kontrolünüzde karşılık gelen özellikleri şu şekilde ayarlayabilirsiniz:

```csharp
notesTextBox.FontBold = cellStyle.Font.Bold;
notesTextBox.FontItalic = cellStyle.Font.Italic;
```

### Izgara kontrolü bir `FontColor` özelliği sunmuyorsa?

Çoğu modern UI framework’ü bunu sağlar, ama sadece bir CSS dizesi kabul ediyorsa, `Color` nesnesini hex’e çevirin:

```csharp
string hex = $"#{notesTextBox.FontColor.R:X2}{notesTextBox.FontColor.G:X2}{notesTextBox.FontColor.B:X2}";
notesTextBox.Style["color"] = hex; // for web‑based grids
```

### Birden fazla hücreyi aynı anda nasıl işlerim?

İstenen aralık üzerinde döngü kurun, her hücrenin stilini alın ve ilgili metin kutusuna uygulayın. Çok sayıda satır işliyorsanız, stil nesnelerini önbelleğe alarak performans kayıplarını önleyin.

---

## Pro İpuçları & Yaygın Tuzaklar

- **ExcelPackage’ı önbellekle** – her hücre için dosyayı açıp kapatmak maliyetlidir. Çalışma kitabını bir kez yükleyin, ardından aynı `ExcelWorksheet` nesnesini yeniden kullanın.  
- **Null renklerine dikkat** – varsayılan rengi miras alan bir hücre `null` döndürür. Her zaman bir yedek (siyah ya da kontrolün varsayılanı) sağlayın.  
- **DPI ölçeklemesini unutma** – yüksek‑DPI monitörlerde yazı tipleri biraz daha büyük görünebilir. Gerekirse `Graphics.DpiX` ile ayarlama yapın.  
- **İş parçacığı güvenliği** – EPPlus iş parçacığı‑güvenli değildir. Birden çok sayfayı paralel işliyorsanız, her iş parçacığı için ayrı bir `ExcelPackage` oluşturun.

---

## Sonuç

Artık **Excel hücresinden yazı tipini kopyalama** ve **hücre stilini** herhangi bir metin‑kutusu kontrolüne C# ile **uygulama** konusunda bilgi sahibisiniz. Hücrenin `Style` nesnesini alıp, `Font` özelliklerini çıkarıp UI öğesine atayarak, manuel kopyalamaya gerek kalmadan görsel tutarlılığı koruyabilirsiniz.  

Tam çözüm—çalışma kitabını yükleme, hücre stilini alma ve metin kutusunun yazı tipi ailesi, boyutu ve rengini ayarlama—**hücre biçimlendirmesini kullanma** ve **textbox yazı tipi boyutunu ayarlama** konularının özünü kapsar.  

Şimdi örneği genişleterek arka plan renklerini, kenarlıkları ya da hatta tüm hücre içeriklerini kopyalamayı deneyin. Zengin hücre renderlamasını destekleyen bir veri‑ızgara kütüphaneniz varsa, Excel’den çektiğiniz aynı stil bilgilerini ona besleyebilir, UI ve raporlarınızı mükemmel bir senkron içinde tutabilirsiniz.

Daha fazla sorunuz mu var? Yorum bırakın ya da “dinamik Excel‑to‑UI bağlama” ve “tema‑duyarlı renk dönüşümü” gibi ilgili konuları keşfedin. Kodlamanın tadını çıkarın!

---

![yazı tipini kopyalama örneği](placeholder-image.jpg "Excel hücresinden TextBox'a yazı tipini kopyalama")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}