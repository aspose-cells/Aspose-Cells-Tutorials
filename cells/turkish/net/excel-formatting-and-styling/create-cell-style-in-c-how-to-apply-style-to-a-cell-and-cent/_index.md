---
category: general
date: 2026-02-21
description: C#'ta hücre stilini hızlıca oluşturun. Bir hücreye stil uygulamayı, hücrede
  metni ortalamayı, hücre hizalamasını ayarlamayı ve hücre biçimlendirmesinde uzmanlaşmayı
  öğrenin.
draft: false
keywords:
- create cell style
- apply style to cell
- center text in cell
- set cell alignment
- how to center text
language: tr
og_description: C#'ta hücre stili oluşturun ve bir hücreye stil uygulamayı, hücrede
  metni ortalamayı ve hücre hizalamasını ayarlamayı net, adım adım bir kılavuzla öğrenin.
og_title: C#'ta hücre stili oluşturma – Bir hücreye stil uygulama ve metni ortalama
tags:
- C#
- Aspose.Cells
- Excel automation
title: C#'ta hücre stili oluşturma – Hücreye stil uygulama ve metni ortalama
url: /tr/net/excel-formatting-and-styling/create-cell-style-in-c-how-to-apply-style-to-a-cell-and-cent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta hücre stili oluşturma – Stilleri Uygulama ve Metni Ortalamaya Tam Kılavuz

Bir Excel çalışma sayfasında **create cell style** oluşturmanız gerektiğinde ama nereden başlayacağınızı bilemediğiniz oldu mu? Yalnız değilsiniz. Birçok otomasyon projesinde, **apply style to cell** nesnelerini uygulama yeteneği, sıradan bir elektronik tablo ile cilalı bir rapor arasındaki farktır.  

Bu öğreticide, bir hücre içinde **how to center text** gösteren tam, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz, hizalamayı ayarlayacağız ve ince bir kenarlık ekleyeceğiz—hepsi sadece birkaç C# satırıyla. Sonunda her bir parçanın neden önemli olduğunu ve kendi senaryolarınıza nasıl uyarlayacağınızı tam olarak öğreneceksiniz.

## Öğrenecekleriniz

- Aspose.Cells (veya benzeri bir kütüphane) kullanarak **create cell style** iş akışının net bir anlayışı.
- **apply style to cell** için bir konsol uygulamasına kopyalayıp‑yapıştırabileceğiniz tam kod.
- **center text in cell**, **set cell alignment** konularına dair içgörüler ve birleştirilmiş hücreler ya da özel sayı biçimleri gibi uç durumların nasıl ele alınacağı.
- Stili genişletmek için ipuçları—farklı yazı tipleri, arka plan renkleri veya koşullu biçimlendirme.

> **Önkoşul:** Visual Studio 2022 (veya herhangi bir C# IDE) ve Aspose.Cells for .NET NuGet paketi. Başka bir bağımlılık gerekmez.

---

## Adım 1: Projenizi Kurun ve Ad Alanlarını İçe Aktarın

**create cell style** oluşturabilmemiz için, Excel kütüphanesine referans veren bir projeye ihtiyacımız var.

```csharp
// Program.cs – entry point
using System;
using Aspose.Cells;   // Make sure the Aspose.Cells NuGet package is installed

class Program
{
    static void Main()
    {
        // We'll fill in the rest of the steps here.
    }
}
```

*Neden önemli:* `Aspose.Cells`'i içe aktarmak, `Workbook`, `Worksheet`, `Style` ve `Border` sınıflarına erişim sağlar. Farklı bir kütüphane (ör. EPPlus) kullanıyorsanız, sınıf adları değişir ancak kavram aynı kalır.

---

## Adım 2: Bir Çalışma Kitabı Oluşturun ve İlk Hücreyi Alın

Şimdi **create cell style** yapmak için, biçimlendirmek istediğimiz hücreye bir referans alıyoruz.

```csharp
// Inside Main()
Workbook workbook = new Workbook();           // New, empty workbook
Worksheet ws = workbook.Worksheets[0];        // First worksheet (index 0)

// Step 1: Get a reference to the first cell (row 0, column 0) in the worksheet
Cell firstCell = ws.Cells[0, 0];               // A1 in Excel terms
firstCell.PutValue("Hello, styled world!");
```

`Cell` kullandığımızı, genel `var` yerine fark ettiniz—açık tip tanımlaması yeni başlayanlar için kodu daha anlaşılır kılar. `PutValue` çağrısı bir dize yazar, böylece stil etkisini daha sonra görebiliriz.

---

## Adım 3: Stili Tanımlayın – Metni Ortala, İnce Kenarlık Ekle

İşte **create cell style** işleminin kalbi. Yatay hizalamayı, ince bir kenarlığı ve birkaç isteğe bağlı inceliği ayarlayacağız.

```csharp
// Step 2: Define a style that centers the text and adds a thin border
Style cellStyle = workbook.CreateStyle();          // Create a fresh Style object
cellStyle.HorizontalAlignment = TextAlignmentType.Center; // Center text horizontally
cellStyle.VerticalAlignment = TextAlignmentType.Center;   // Center vertically – often forgotten
cellStyle.Borders[BorderType.TopBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.LeftBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.RightBorder].LineStyle = CellBorderType.Thin;

// Optional: set a light gray background to make the border pop
cellStyle.ForegroundColor = System.Drawing.Color.LightGray;
cellStyle.Pattern = BackgroundType.Solid;
```

*Bunu yapmamızın nedeni:*  
- **HorizontalAlignment** ve **VerticalAlignment** birlikte “**how to center text** in a cell?” sorusuna yanıt verir.  
- Dört kenarın da eklenmesi, hücrenin kutu şeklinde bir etiket gibi görünmesini sağlar; bu başlıklar için faydalıdır.  
- Arka plan rengi zorunlu değildir, ancak stilin daha sonra nasıl genişletilebileceğini gösterir.

---

## Adım 4: Tanımlanan Stili Seçilen Hücreye Uygulayın

Stil artık mevcut, bir tek metod çağrısıyla **apply style to cell** yapıyoruz.

```csharp
// Step 3: Apply the defined style to the selected cell
firstCell.SetStyle(cellStyle);
```

Hepsi bu—Aspose.Cells, stili hücrenin iç stil koleksiyonuna kopyalamayı halleder. Aynı biçimlendirmeyi bir aralıkta da ihtiyacınız varsa, `ws.Cells.CreateRange("A1:D1").ApplyStyle(cellStyle, new StyleFlag { All = true });` kullanabilirsiniz.

---

## Adım 5: Çalışma Kitabını Kaydedin ve Sonucu Doğrulayın

Hızlı bir kaydetme, dosyayı Excel'de açıp metnin gerçekten ortalandığını ve kenarlığın göründüğünü doğrulamanızı sağlar.

```csharp
// Save the workbook to disk
string outputPath = "StyledCell.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
```

*Beklenen çıktı:* **StyledCell.xlsx** dosyasını açtığınızda, **A1** hücresi “Hello, styled world!” metnini hem yatay hem de dikey olarak ortalanmış, ince gri bir kenarlıkla çevrelenmiş ve açık gri bir arka planla gösterir.

---

## Yaygın Varyasyonlar ve Uç Durumlar

### 1. Birleştirilmiş Bölge İçinde Metni Ortala

Eğer **A1:C1** hücrelerini birleştirir ve yine de metni ortalamak isterseniz, birleştirmeden **sonra** stilinizi sol‑üst hücreye uygulamalısınız:

```csharp
ws.Cells.Merge(0, 0, 1, 3); // Merge A1:C1
firstCell.SetStyle(cellStyle); // Style still works because it’s applied to the anchor cell
```

### 2. Sayısal Biçim Kullanma

Bazen **set cell alignment** *ve* sayıları belirli bir formatta göstermeniz gerekir:

```csharp
cellStyle.Custom = "#,##0.00"; // Two decimal places
firstCell.PutValue(12345.678);
firstCell.SetStyle(cellStyle);
```

Hizalama ortalanmış kalır ve sayı `12,345.68` şeklinde görünür.

### 3. Stilleri Verimli Bir Şekilde Yeniden Kullanma

Her hücre için yeni bir `Style` oluşturmak performansı düşürebilir. Bunun yerine, tek bir stil nesnesi oluşturup birçok hücre veya aralıkta yeniden kullanın. `StyleFlag` sınıfı, sadece ihtiyacınız olan bölümleri uygulamanıza izin vererek belleği tasarruf ettirir.

```csharp
StyleFlag flag = new StyleFlag { HorizontalAlignment = true, Borders = true };
ws.Cells.CreateRange("B2:B10").ApplyStyle(cellStyle, flag);
```

---

## Profesyonel İpuçları ve Dikkat Edilmesi Gereken Tuzaklar

- **Dikey hizalamayı unutmayın** – sadece yatay ortalama, özellikle daha yüksek satırlarda garip görünür.
- **Kenarlık tipleri**: `CellBorderType.Thin` çoğu rapor için uygundur, ancak görsel hiyerarşi için `Medium` veya `Dashed` tiplerine geçebilirsiniz.
- **Renk işleme**: .NET Core hedefliyorsanız, `System.Drawing.Common` paketinden `System.Drawing.Color` kullanın; aksi takdirde çalışma zamanı hatası alırsınız.
- **Kaydetme formatı**: Eski Excel sürümleriyle uyumluluk gerekiyorsa, `SaveFormat.Xlsx` yerine `SaveFormat.Xls` kullanın.

![ortalanmış metin ve ince kenarlık gösteren bir hücre örneği](https://example.com/images/create-cell-style.png "C#'ta hücre stili oluşturma")

*Alt metin: ortalanmış metin ve ince kenarlık gösteren bir hücrenin ekran görüntüsü, create cell style öğreticisi tarafından oluşturulmuştur.*

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```csharp
using System;
using Aspose.Cells;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Grab the first cell and put a sample value
        Cell firstCell = ws.Cells[0, 0];
        firstCell.PutValue("Hello, styled world!");

        // 3️⃣ Create the style: center text, thin border, light gray background
        Style cellStyle = workbook.CreateStyle();
        cellStyle.HorizontalAlignment = TextAlignmentType.Center;
        cellStyle.VerticalAlignment   = TextAlignmentType.Center;
        cellStyle.Borders[BorderType.TopBorder].LineStyle    = CellBorderType.Thin;
        cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
        cellStyle.Borders[BorderType.LeftBorder].LineStyle   = CellBorderType.Thin;
        cellStyle.Borders[BorderType.RightBorder].LineStyle  = CellBorderType.Thin;
        cellStyle.ForegroundColor = Color.LightGray;
        cellStyle.Pattern = BackgroundType.Solid;

        // 4️⃣ Apply the style to the cell
        firstCell.SetStyle(cellStyle);

        // 5️⃣ Save the result
        string outputPath = "StyledCell.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
    }
}
```

Bu programı çalıştırın, **StyledCell.xlsx** dosyasını açın ve daha önce açıklanan tam sonucu göreceksiniz. Metni, kenarlık stilini veya arka plan rengini markanıza uygun şekilde değiştirmekten çekinmeyin.

---

## Sonuç

Sıfırdan **created cell style** yaptık, **apply style to cell** uyguladık ve **how to center text**'i hem yatay hem de dikey olarak gösterdik. Bu yapı taşlarını ustalaştığınızda artık başlıkları biçimlendirebilir, toplamları vurgulayabilir veya C#'tan çıkmadan tam rapor şablonları oluşturabilirsiniz.  

Bir sonraki adımları merak ediyorsanız, şunları deneyin:

- **Aynı stili tüm bir satıra uygulama** (`ws.Cells.CreateRange("A2:E2").ApplyStyle(cellStyle, new StyleFlag { All = true });`).
- **Koşullu biçimlendirme ekleme** ile hücre değerlerine göre arka planı değiştirme.
- **Stili koruyarak PDF'ye dışa aktarma**.

Unutmayın, stil oluşturma okunabilirlik kadar estetikle de ilgilidir. Deneyin, yineleyin ve yakında elektronik tablolarınız kodunuz kadar profesyonel görünecek.

*Kodlamanın keyfini çıkarın!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}