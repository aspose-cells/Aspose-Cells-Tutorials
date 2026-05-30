---
category: general
date: 2026-05-30
description: C# kullanarak Excel’de metin kutusu yazı tipi boyutunu değiştirin. Excel
  metin kutusu yazı tipini adım adım kodla hızlı bir şekilde nasıl değiştireceğinizi
  öğrenin.
draft: false
keywords:
- change textbox font size
- modify excel textbox font
language: tr
og_description: C# kullanarak Excel'de metin kutusu yazı tipi boyutunu değiştirin.
  Bu kılavuz, Excel metin kutusu yazı tipini güvenli ve verimli bir şekilde nasıl
  değiştireceğinizi gösterir.
og_title: C# ile Excel'de Metin Kutusu Yazı Tipi Boyutunu Değiştir – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  headline: Change Textbox Font Size in Excel with C# – Complete Guide
  type: TechArticle
- description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  name: Change Textbox Font Size in Excel with C# – Complete Guide
  steps:
  - name: Why this matters
    text: Opening the workbook via COM gives us a live object model—meaning any change
      we make reflects instantly in the file. Setting `Visible = false` speeds things
      up and avoids popping windows during automation.
  - name: Why we use `TextFrame2`
    text: '`TextFrame2` is the newer object model introduced with Office 2007. It
      supports advanced typographic features and is generally more reliable than the
      older `TextFrame`. Using it ensures our **change textbox font size** operation
      works across modern Excel versions.'
  - name: 1. Change *all* textboxes on a sheet
    text: '```csharp foreach (Excel.Shape s in xlWorksheet.Shapes) { if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
      { var tr = s.TextFrame2.TextRange; tr.Font.Name = fontName; tr.Font.Size = newSize;
      } } ```'
  - name: 2. Identify a textbox by its **Name** instead of index
    text: 'If you gave your textbox a meaningful name (e.g., “TitleBox”), you can
      fetch it directly:'
  type: HowTo
tags:
- Excel Interop
- C#
- Office Automation
title: C# ile Excel’de Metin Kutusu Yazı Tipi Boyutunu Değiştirme – Tam Kılavuz
url: /tr/net/excel-shape-text-modifications/change-textbox-font-size-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile Excel'de Metin Kutusu Yazı Tipi Boyutunu Değiştirme – Tam Kılavuz

C# kullanarak bir Excel çalışma sayfasındaki **metin kutusu yazı tipi boyutunu** değiştirmek mi istiyorsunuz? Doğru yerdesiniz. Raporlar oluşturuyor, bir gösterge paneli inşa ediyor ya da sadece bir şablonu ayarlıyorsanız, bir metin kutusunun görünümünü düzenlemek elektronik tablonuzun çok daha profesyonel görünmesini sağlar.

Bu öğreticide ayrıca **excel metin kutusu yazı tipini** sadece boyutla sınırlı kalmayacak şekilde—yazı tipi ailesi, kalınlık ve birden fazla şekil yönetimi gibi—değiştireceğiz. Sonunda, çalışma kitabını açmaktan COM nesnelerini temizlemeye kadar sürecin her köşesine dokunan, hemen projenize ekleyebileceğiniz hazır bir kod parçacığına sahip olacaksınız. Gereksiz ayrıntı yok, sadece bugün projenize ekleyebileceğiniz pratik kod.

## Önkoşullar — İhtiyacınız Olanlar

İlerlemeye başlamadan önce makinenizde aşağıdakilerin olduğundan emin olun:

| Requirement | Why it matters |
|-------------|----------------|
| **.NET 6+** (or .NET Framework 4.7.2+) | C# derleyicisi ve çalışma zamanı sağlar. |
| **Microsoft.Office.Interop.Excel** NuGet paketi | Excel ile iletişim kurmak için gereken COM interop tiplerini verir. |
| **Excel yüklü** (any recent version) | Interop katmanı yalnızca Office uygulaması mevcutken çalışır. |
| **Temel C# bilgisi** | Kolayca takip edebileceksiniz, ancak her satırı açıklayacağız. |

Eğer bunlardan biri eksikse, şimdi durup kurun; rehberin geri kalanı bu bileşenlerin mevcut olduğunu varsayar.

## Adım 1: Projeyi Oluşturun ve Namespace'leri İçeri Aktarın

İlk iş olarak yeni bir console uygulaması oluşturun (veya mevcut birine entegre edin) ve interop namespace'ini ekleyin.

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll call the helper method that does the heavy lifting.
            ChangeTextboxFontSize(@"C:\Temp\Sample.xlsx", "Sheet1", 0, 14, "Calibri");
        }
    }
}
```

> **Pro tip:** .NET 6+ hedefliyorsanız `Microsoft.Office.Interop.Excel` paketini `dotnet add package Microsoft.Office.Interop.Excel` komutuyla ekleyin. Bu, `Excel` takma adının doğru çözülmesini sağlar.

## Adım 2: Çalışma Kitabını Açın ve Hedef Çalışma Sayfasını Alın

Şimdi Excel'i başlatıp dosyayı açmalı ve metin kutusunun bulunduğu sayfayı işaret etmeliyiz. Bunu bir `try/finally` bloğuna sarmak, bir şeyler ters gittiğinde bile COM nesnelerinin serbest bırakılmasını garantiler.

```csharp
static void ChangeTextboxFontSize(string workbookPath,
                                  string sheetName,
                                  int textboxIndex,
                                  double newSize,
                                  string fontName)
{
    Excel.Application xlApp = null;
    Excel.Workbook xlWorkbook = null;
    Excel.Worksheet xlWorksheet = null;

    try
    {
        xlApp = new Excel.Application
        {
            // Keep Excel hidden; set to true if you want to watch the changes.
            Visible = false,
            DisplayAlerts = false
        };

        xlWorkbook = xlApp.Workbooks.Open(workbookPath);
        xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;
        if (xlWorksheet == null)
            throw new ArgumentException($"Worksheet '{sheetName}' not found.");
```

### Neden Önemli

COM üzerinden çalışma kitabını açmak, canlı bir nesne modeli elde etmemizi sağlar—yapılan her değişiklik dosyada anında yansır. `Visible = false` ayarı, otomasyon sırasında pencerelerin açılmasını önleyerek işlemi hızlandırır.

## Adım 3: Metin Kutusu Şeklini Alın

Excel, metin kutularını `Shapes` koleksiyonundaki `Shape` nesneleri olarak ele alır; ayrı bir `TextBox` koleksiyonu yoktur. Bu yüzden aşağıdaki kod, internette gördüğünüz örneklerden biraz farklı görünebilir.

```csharp
        // Excel stores all drawing objects (including textboxes) in the Shapes collection.
        Excel.Shapes shapes = xlWorksheet.Shapes;

        // Guard against an out‑of‑range index.
        if (textboxIndex < 0 || textboxIndex >= shapes.Count)
            throw new IndexOutOfRangeException("Textbox index is out of range.");

        // Grab the specific shape; we assume it’s a textbox.
        Excel.Shape textboxShape = shapes.Item(textboxIndex + 1); // COM collections are 1‑based.
        if (!textboxShape.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
            throw new InvalidOperationException("Selected shape is not a textbox.");
```

> **Dikkat:** `Shapes` koleksiyonu 1‑tabanlıdır, bu yüzden gönderdiğiniz sıfır‑tabanlı `textboxIndex` değerine `+1` ekleriz. Bunu unutmak, “index out of range” hatalarına yol açar ve hata ayıklamayı zorlaştırır.

## Adım 4: Metin Kutusu Yazı Tipi Boyutunu (ve Adını) Değiştirin

İşte **metin kutusu yazı tipi boyutunu** nihayet değiştirdiğimiz yer. `TextFrame2` özelliği, `Font.Name` ve `Font.Size` gibi zengin‑metin biçimlendirme seçeneklerine erişim sağlar.

```csharp
        // Access the text range inside the textbox.
        Excel.TextRange2 textRange = textboxShape.TextFrame2.TextRange;

        // Change the font name – this also “modifies excel textbox font”.
        textRange.Font.Name = fontName;

        // Change the font size – the core of our tutorial.
        textRange.Font.Size = newSize;

        // Optional: make the text bold for extra emphasis.
        // textRange.Font.Bold = Microsoft.Office.Core.MsoTriState.msoTrue;
```

### Neden `TextFrame2` Kullanıyoruz

`TextFrame2`, Office 2007 ile tanıtılan yeni nesne modelidir. Gelişmiş tipografik özellikleri destekler ve genellikle eski `TextFrame`'e göre daha güvenilirdir. `TextFrame2` kullanmak, **metin kutusu yazı tipi boyutunu** değiştirme işleminin modern Excel sürümlerinde sorunsuz çalışmasını sağlar.

## Adım 5: Kaydedin, Temizleyin ve Doğrulayın

Yazı tipini ayarladıktan sonra değişiklikleri kalıcı hâle getirmeli ve her COM referansını serbest bırakmalıyız. Temizleme adımını atlamak, arka planda terkedilmiş Excel süreçlerinin kalmasına neden olabilir.

```csharp
        // Save the workbook – you can also use SaveAs to create a copy.
        xlWorkbook.Save();

        Console.WriteLine($"Successfully changed textbox font size to {newSize} pt and font to '{fontName}'.");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Error: {ex.Message}");
    }
    finally
    {
        // Release COM objects in reverse order of creation.
        if (xlWorksheet != null) System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorksheet);
        if (xlWorkbook != null)
        {
            xlWorkbook.Close(false);
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorkbook);
        }
        if (xlApp != null)
        {
            xlApp.Quit();
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlApp);
        }

        // Force garbage collection to clean up any remaining RCWs.
        GC.Collect();
        GC.WaitForPendingFinalizers();
    }
}
```

> **Pro tip:** Birçok çalışma sayfasında **excel metin kutusu yazı tipini** değiştirmek istiyorsanız, iç mantığı `Workbook.Worksheets` üzerinde dönen bir döngüye alın. Her sayfa için `textboxIndex` değerini sıfırlamayı unutmayın.

## Kenar Durumlarını Ele Alma — Birden Fazla Metin Kutusu ve Eksik Şekiller

Gerçek dünyadaki elektronik tablolar nadiren tek bir metin kutusu içerir. Aşağıda, yöntemi tamamen yeniden yazmadan uygulayabileceğiniz iki hızlı strateji bulabilirsiniz.

### 1. Sayfadaki *tüm* metin kutularını değiştir

```csharp
foreach (Excel.Shape s in xlWorksheet.Shapes)
{
    if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
    {
        var tr = s.TextFrame2.TextRange;
        tr.Font.Name = fontName;
        tr.Font.Size = newSize;
    }
}
```

### 2. Metin kutusunu **İsim** ile, indeks yerine tanımla

Eğer metin kutunuza anlamlı bir isim (ör. “TitleBox”) verdiyseniz, doğrudan bu ismi kullanarak alabilirsiniz:

```csharp
Excel.Shape namedBox = xlWorksheet.Shapes.Item("TitleBox");
namedBox.TextFrame2.TextRange.Font.Size = newSize;
```

Her iki yaklaşım da, çalışma kitabının nasıl yapılandırılmış olursa olsun, **excel metin kutusu yazı tipini** hassas bir şekilde değiştirmenizi sağlar.

## Görsel Genel Bakış (İsteğe Bağlı)

Hızlı bir görsel ipucu isterseniz, aşağıdaki diyagramı hayal edin:

![Screenshot showing Excel worksheet with a highlighted textbox – demonstrates how to change textbox font size](change-textbox-font-size.png)

*Alt metin:* *Excel'de metin kutusu yazı tipi boyutunu değiştirme – vurgulanmış metin kutusu, yazı tipi değişikliği için hazır.*

## Tam Çalışan Örnek

Her şeyi bir araya getirdiğimizde, tek bir dosyaya kopyalayıp bir console projesine yapıştırarak hemen çalıştırabileceğiniz (dosya yolu ve sayfa adını güncellemeniz yeterli) bir örnek:

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Ortamınıza göre bu parametreleri ayarlayın.
            string workbookPath = @"C:\Temp\Sample.xlsx";
            string sheetName = "Sheet1";
            int textboxIndex = 0;          // Sayfadaki ilk metin kutusu.
            double newFontSize = 14;       // İstenen yazı tipi boyutu.
            string newFontName = "Calibri";

            ChangeTextboxFontSize(workbookPath, sheetName, textboxIndex, newFontSize, newFontName);
        }

        static void ChangeTextboxFontSize(string workbookPath,
                                          string sheetName,
                                          int textboxIndex,
                                          double newSize,
                                          string fontName)
        {
            Excel.Application xlApp = null;
            Excel.Workbook xlWorkbook = null;
            Excel.Worksheet xlWorksheet = null;

            try
            {
                xlApp = new Excel.Application { Visible = false, DisplayAlerts = false };
                xlWorkbook = xlApp.Workbooks.Open(workbookPath);
                xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;

                if (xlWorksheet == null)


## Sonra Ne Öğrenmelisiniz?

- [Changing Font Size in Excel](/cells/english/net/working-with-fonts-in-excel/changing-font-size/)
- [How to Customize Font Size in Excel Cells Using Aspose.Cells .NET | Complete Guide](/cells/english/net/formatting/customize-font-size-excel-aspose-cells-dotnet/)
- [How to Set Font Styles in Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}