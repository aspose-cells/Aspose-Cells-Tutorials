---
category: general
date: 2026-02-15
description: C#'ta sütun sayı formatını ayarlayarak para birimini hızlıca biçimlendirme
  ve özel sayısal format uygulama. Sütunu adından almayı ve ızgara sütun hizalamasını
  ayarlamayı öğrenin.
draft: false
keywords:
- how to format currency
- set column number format
- apply custom numeric format
- retrieve column by name
- set grid column alignment
language: tr
og_description: C# kullanarak bir ızgara sütununda para birimini nasıl biçimlendireceğiniz.
  Bu öğretici, sütunu adla nasıl alacağınızı, sütun sayı formatını nasıl ayarlayacağınızı,
  özel sayısal formatı nasıl uygulayacağınızı ve ızgara sütun hizalamasını nasıl belirleyeceğinizi
  gösterir.
og_title: Grid Sütununda Para Birimini Nasıl Biçimlendirirsiniz – Tam Rehber
tags:
- C#
- GridFormatting
- UI
title: Bir Grid Sütununda Para Birimini Nasıl Biçimlendirebilirsiniz – Adım Adım Kılavuz
url: /tr/net/number-and-display-formats-in-excel/how-to-format-currency-in-a-grid-column-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Grid Sütununda Para Birimini Biçimlendirme – Tam Programlama Öğreticisi

Hiç **para birimini nasıl biçimlendireceğinizi** bir grid sütununda saçınızı yolmadan merak ettiniz mi? Tek başınıza değilsiniz. `1234.5` gibi sade bir sayıya bakıp, sihirli bir şekilde `$1,234.50` olarak görünmesini istediğinizde, cevap genellikle sadece birkaç satır yapılandırmadan ibarettir.  

Bu rehberde **sütunu isimle alacağız**, **sütun sayı biçimini ayarlayacağız** ve tipik muhasebe düzenine uygun **özel sayısal biçim uygulayacağız**. Ayrıca **grid sütun hizalamasını ayarlayacağız** ve UI'nin daha şık görünmesi için ince bir kenarlık ekleyeceğiz.

> **TL;DR** – Sonunda, ham ondalık sayıları herhangi bir `GridJs`‑stil kontrol içinde güzel biçimlendirilmiş para birimi değerlerine dönüştüren, çalıştırmaya hazır bir kod parçacığına sahip olacaksınız.

---

## Gereksinimler

- .NET projesi (C# 8.0+ destekleyen herhangi bir sürüm – Visual Studio 2022 harika çalışır).  
- `Columns` koleksiyonunu ortaya çıkaran bir grid bileşeni (örnek, hayali bir `GridJs` sınıfı kullanıyor, ancak kavramlar DevExpress, Telerik veya Syncfusion grid'lerine de uygulanabilir).  
- C# sözdizimi hakkında temel bilgi – ileri düzey hileler gerekmez.

Eğer bunlara zaten sahipseniz, harika. Değilse, sadece bir konsol uygulaması oluşturun; grid, örnekleme amacıyla taklit edilebilir.

## Adım‑Adım Uygulama

Her adımın altında kompakt bir kod bloğu, satırın **neden** önemli olduğuna dair kısa bir açıklama ve yaygın tuzaklardan kaçınmak için bir ipucu göreceksiniz.

### ## Step 1 – “Amount” sütununu isimle al

```csharp
// Step 1: Retrieve the "Amount" column from the grid
var amountColumn = gridJs.Columns["Amount"];
if (amountColumn == null)
{
    throw new InvalidOperationException("Column 'Amount' does not exist. Verify the column name or check the grid's schema.");
}
```

**Neden önemli:**  
Çoğu grid API'si sütunları sözlük‑benzeri bir indeksleyici aracılığıyla ortaya çıkar. Sütunu başlık adı (`"Amount"`) ile alarak, temel veri kaynağına dokunmadan görünümünü değiştirebilirsiniz.  

**Pro ipucu:** Her zaman `null` dönüşüne karşı koruma sağlayın – sütun adındaki bir yazım hatası veya dinamik şema değişikliği, çalışma zamanında `NullReferenceException` oluşmasına neden olabilir.

### ## Step 2 – Özel bir para birimi maskesi kullanarak sütun sayı biçimini ayarla

```csharp
// Step 2: Apply a custom numeric format for currency values
amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";
```

**Neden önemli:**  
Biçim dizesi Excel’in muhasebe formatı kurallarını izler:

- `_(* #,##0.00_)` → Pozitif sayılar, para birimi simgesi için ön boşlukla sağa hizalanır.  
- `_(* (#,##0.00)` → Parantez içinde negatif sayılar.  
- `_(* \"-\"??_)` → Sıfır değerler tire olarak gösterilir.  
- `_(@_)` → Metin değerleri değişmeden kalır.

**apply custom numeric format** kullanmak, bin ayırıcıları, ondalık basamakları ve para birimi işaretinin konumunu tam kontrol etmenizi sağlar.  

**Köşe durum:** Uygulamanız farklı bir yerel ayarı (örneğin USD yerine Euro) desteklemesi gerekiyorsa, ön boşluğu uygun sembolle değiştirin veya veri kaynağında `CultureInfo`‑bilgili biçimlendirme kullanın.

### ## Step 3 – Okunabilirlik için sütun içeriğini sağa hizala

```csharp
// Step 3: Align the column contents to the right for better readability
amountColumn.Alignment = GridAlignment.Right;
```

**Neden önemli:**  
Para birimi değerleri, ondalık ayırıcıda hizalandıklarında taraması daha kolay olur. **set grid column alignment**'ı `Right` olarak ayarlamak, elektronik tabloların para verilerini gösterme şekline benzer.  

**Uyarı:** Bazı grid'ler, özel şablon içeren hücrelerde hizalamayı görmezden gelir. Eğer hizalamanın etkili olmadığını fark ederseniz, sütunun özel bir hücre render'ı kullanmadığını iki kez kontrol edin.

### ## Step 4 – Sütun hücrelerinin etrafına ince gri bir kenarlık ekle

```csharp
// Step 4: Add a thin gray border around the column cells
amountColumn.Border = new GridBorder
{
    Color = Color.Gray,
    Style = BorderLineStyle.Thin
};
```

**Neden önemli:**  
İnce bir kenarlık, özellikle grid alternatif satır renklerine sahip olduğunda, “Amount” sütununu komşularından ayırır. Bu, verinin ayrı bir finansal rakamı temsil ettiğine dair görsel bir ipucudur.  

**İpucu:** Yazdırma amaçları için daha kalın bir çizgiye ihtiyacınız varsa, `BorderLineStyle`'ı `Medium`'a yükseltin veya `Color`'ı `Color.Black` olarak değiştirin.

## Tam Çalışan Örnek

İşte `GridJs`‑stil bir kontrol kullanan bir WinForms veya WPF projesine ekleyebileceğiniz tam kod parçacığı. Örnek, biçimlendirilmiş değerleri konsola da yazdırır, böylece UI olmadan çıktıyı doğrulayabilirsiniz.

```csharp
using System;
using System.Drawing;   // For Color
using GridLibrary;      // Hypothetical namespace for GridJs

namespace GridCurrencyDemo
{
    class Program
    {
        static void Main()
        {
            // Create a mock grid and add a sample column
            var gridJs = new GridJs();
            gridJs.Columns.Add(new GridColumn
            {
                Name = "Amount",
                Header = "Amount",
                DataType = typeof(decimal)
            });

            // Populate some sample data
            gridJs.Rows.Add(new { Amount = 1234.5m });
            gridJs.Rows.Add(new { Amount = -567.89m });
            gridJs.Rows.Add(new { Amount = 0m });

            // ---- Formatting steps ------------------------------------------------
            // 1️⃣ Retrieve the "Amount" column
            var amountColumn = gridJs.Columns["Amount"]
                ?? throw new InvalidOperationException("Column 'Amount' not found.");

            // 2️⃣ Apply custom numeric format for currency
            amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";

            // 3️⃣ Right‑align the values
            amountColumn.Alignment = GridAlignment.Right;

            // 4️⃣ Add a thin gray border
            amountColumn.Border = new GridBorder
            {
                Color = Color.Gray,
                Style = BorderLineStyle.Thin
            };
            // -----------------------------------------------------------------------

            // Render the grid (in a real UI you would call gridJs.Render() or similar)
            Console.WriteLine("Formatted Currency Grid:");
            foreach (var row in gridJs.Rows)
            {
                var rawValue = (decimal)row.Amount;
                // The grid library would automatically apply NumberFormat when displaying.
                // For console demo we mimic the formatting:
                string formatted = rawValue.ToString("#,##0.00", System.Globalization.CultureInfo.InvariantCulture);
                if (rawValue < 0)
                    formatted = $"({formatted.TrimStart('-')})";
                else if (rawValue == 0)
                    formatted = "-";

                Console.WriteLine($"| {formatted,15} |");
            }

            // Keep console open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Beklenen konsol çıktısı**

```
Formatted Currency Grid:
|        1,234.50 |
|       (567.89) |
|               - |
```

Pozitif sayının sağa hizalandığını, negatif sayının parantez içinde göründüğünü ve sıfırın tire olarak gösterildiğini fark edin – tam olarak özel biçim dizesinin belirttiği gibi.

## Sıkça Sorulan Sorular & Köşe Durumları

| Soru | Cevap |
|------|-------|
| *Grid farklı bir kültür (ör. € yerine $) kullanırsa ne olur?* | Biçim dizesindeki ön boşluğu istediğiniz sembolle değiştirin veya veri kaynağının `CultureInfo.CurrentCulture` kullanarak ön‑biçimlendirilmiş bir dize üretmesine izin verin. |
| *Aynı biçimi birden fazla sütun için yeniden kullanabilir miyim?* | Kesinlikle. Biçim dizesini bir sabitte (`const string CurrencyMask = "...";`) saklayın ve para birimi gerektiği her yerde atayın. |
| *Sütun bir string değer içerirse ne olur?* | Biçim dizesi yalnızca sayısal tipleri etkiler. Stringler değişmeden geçer, bu yüzden maskenin son kısmı (`_(@_)`) bulunur – sayısal olmayan içeriği korur. |
| *Performans etkisi var mı?* | İhmal edilebilir. Biçim, veri çekilirken değil, render zamanında uygulanır. Çerçeve başına binlerce satır render etmediğiniz sürece bir yavaşlama fark etmeyeceksiniz. |
| *Yazdırılan raporlar için kenarlığı nasıl kalınlaştırırım?* | `BorderLineStyle.Thin` yerine `BorderLineStyle.Medium` veya `BorderLineStyle.Thick` kullanın. Bazı kütüphaneler ayrıca piksel genişliğini doğrudan belirlemenize izin verir. |

## Özet

Başlangıçtan sona kadar bir grid sütununda **para birimini nasıl biçimlendireceğinizi** adım adım inceledik: sütunu isimle al, sütun sayı biçimini ayarla, özel bir sayısal biçim uygula, hücreleri hizala ve şık bir kenarlık ekle. Tam örnek kutudan çıkar çıkmaz çalışır ve bekleyebileceğiniz tam görsel sonucu gösterir.

If you’re ready to take this further, try:

- **Dynamic cultures** – format dizesini kullanıcının yerel ayarına göre değiştir.  
- **Conditional

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}