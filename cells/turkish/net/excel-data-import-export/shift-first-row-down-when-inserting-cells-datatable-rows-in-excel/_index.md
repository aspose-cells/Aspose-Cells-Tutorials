---
title: Excel'de DataTable Satırları Eklendiğinde İlk Satırı Aşağı Kaydır
linktitle: Excel'de DataTable Satırları Eklendiğinde İlk Satırı Aşağı Kaydır
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Aspose.Cells for .NET kullanarak ilk satırı aşağı kaydırmadan Excel'de DataTable satırları eklemeyi öğrenin. Zahmetsiz otomasyon için adım adım kılavuz.
weight: 11
url: /tr/net/excel-data-import-export/shift-first-row-down-when-inserting-cells-datatable-rows-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de DataTable Satırları Eklendiğinde İlk Satırı Aşağı Kaydır

## giriiş

Excel elektronik tablolarınıza yeni veriler eklerken satırları manuel olarak kaydırmaktan yoruldunuz mu? Şanslısınız! Bu makalede, .NET için Aspose.Cells kullanarak bu işlemi nasıl otomatikleştireceğinizi inceleyeceğiz. Bu eğitimin sonunda, yalnızca Excel'de veri tablolarıyla nasıl çalışacağınızı değil, aynı zamanda içe aktarma seçeneklerini ihtiyaçlarınıza daha iyi uyacak şekilde nasıl özelleştireceğinizi de öğreneceksiniz. İnanın bana; bu size çok zaman ve zahmet kazandırabilir! O halde bir fincan kahve alın ve başlayalım!

## Ön koşullar

Kodlamaya başlamadan önce her şeyin ayarlandığından emin olalım:

1. Visual Studio: Visual Studio'nun yüklü olduğundan emin olun (2017 veya üzeri sorunsuz çalışmalıdır).
2.  .NET için Aspose.Cells: Aspose.Cells kütüphanesine sahip olmanız gerekir. Bunu henüz yapmadıysanız, indirebilirsiniz[Burada](https://releases.aspose.com/cells/net/).
3. C# ve Excel'in Temel Anlayışı: C# programlamanın ve Excel'in nasıl çalıştığına dair temel bir anlayışa sahip olmak, kesinlikle daha etkili bir şekilde takip etmenize yardımcı olacaktır.

 Ayrıca elinizin altında bir örnek Excel dosyası bulundurmak isteyeceksiniz. Bu kılavuzda, şu şekilde adlandırılan bir örnek kullanacağız:`sampleImportTableOptionsShiftFirstRowDown.xlsx`Bu dosyayı kendiniz oluşturabilir veya ihtiyaçlarınıza uygun bir şablon bulabilirsiniz.

## Paketleri İçe Aktar

Kodlamaya dalmadan önce, gerekli paketleri içe aktardığımızdan emin olmamız gerekir. C# projenize aşağıdaki ad alanlarını ekleyin:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Bu paketler çalışma kitabı, çalışma sayfası ve tablolarla çalışmak için gereklidir.

## Adım 1: Projenizi Kurun

### Yeni Bir C# Projesi Oluşturun

Visual Studio'da yeni bir C# Konsol Uygulaması oluşturarak başlayın. Projenize "ExcelDataImport" gibi uygun bir isim verin.

### Aspose.Cells NuGet Paketini Ekle

Aspose.Cells paketini eklemek için Çözüm Gezgini'nde projenize sağ tıklayın, NuGet Paketlerini Yönet'i seçin ve “Aspose.Cells”i arayın. İhtiyacımız olan tüm işlevlere erişebildiğinizden emin olmak için paketi yükleyin.

## Adım 2: Veri Tablosunu Tanımlayın

 Daha sonra, şunu uygulayacağız:`ICellsDataTable` İçeri aktarılacak verileri sağlayan bir sınıf oluşturmak için arayüz. İşte nasıl yapılandırabileceğiniz`CellsDataTable` sınıf:

```csharp
class CellsDataTable : ICellsDataTable
{
    int m_index = -1;
    static String[] colsNames = new String[] { "Pet", "Fruit", "Country", "Color" };
    static String[] col0data = new String[] { "Dog", "Cat", "Duck" };
    static String[] col1data = new String[] { "Apple", "Pear", "Banana" };
    static String[] col2data = new String[] { "UK", "USA", "China" };
    static String[] col3data = new String[] { "Red", "Green", "Blue" };
    static String[][] colsData = new String[][] { col0data, col1data, col2data, col3data };
    
    // ... Diğer üyeleri uygula ...
}
```

Burada, içe aktardığımız tablonun yapısını kolaylaştıracak olan sütun adlarını ve her sütuna ait verileri tanımlıyoruz.

## Adım 3: ICellsDataTable Arayüz Üyelerini Uygulayın

 İçinde`CellsDataTable` sınıfın üyelerini uygulamanız gerekir`ICellsDataTable` arayüz. Gerekli uygulama şu şekildedir:

```csharp
public object this[string columnName]
{
    get
    {
        throw new NotImplementedException();
    }
}

object ICellsDataTable.this[int columnIndex]
{
    get
    {
        return colsData[columnIndex][m_index];
    }
}

string[] ICellsDataTable.Columns
{
    get { return colsNames; }
}

int ICellsDataTable.Count
{
    get { return col0data.Length; }
}

void ICellsDataTable.BeforeFirst()
{
    m_index = -1;
}

bool ICellsDataTable.Next()
{
    m_index++;
    return (m_index < Count);
}
```

Sınıfın bu kısmı veri alma, kaç satır ve sütun olduğunu tanımlama ve geçerli dizin durumunu yönetme işlemlerini gerçekleştirir.

## Adım 4: Ana Fonksiyonu Yazın

 Şimdi, şunu yaratalım:`Run`tüm tablo içe aktarma sürecini düzenleme yöntemi:

```csharp
public static void Run()
{
    string sourceDir = "Your Document Directory\\";
    string outputDir = "Your Document Directory\\";
    
    CellsDataTable cellsDataTable = new CellsDataTable();
    Workbook wb = new Workbook(sourceDir + "sampleImportTableOptionsShiftFirstRowDown.xlsx");
    Worksheet ws = wb.Worksheets[0];
```

## Adım 5: İçe Aktarma Seçeneklerini Ayarlayın

 İçe aktarma davranışını kontrol etmek için bir örnek oluşturmalısınız`ImportTableOptions` ve özellikleri buna göre ayarlayın. Özellikle, ayarlamak istiyoruz`ShiftFirstRowDown` ile`false`.

```csharp
    ImportTableOptions opts = new ImportTableOptions();
    opts.ShiftFirstRowDown = false; // İlk satırı aşağı kaydırmak istemiyoruz
```

## Adım 6: DataTable'ı içe aktarın

 Artık verileri kendi sistemimizden içe aktarabiliriz.`CellsDataTable` çalışma kağıdına.

```csharp
    ws.Cells.ImportData(cellsDataTable, 2, 2, opts);
}
```

Bu komut, belirtilen satır ve sütundan başlayarak veri tablonuzu doğrudan ekleyecektir.

## Adım 7: Çalışma Kitabını Kaydedin

Son olarak, değiştirilen çalışma kitabını bir dosyaya geri kaydedeceğiz:

```csharp
    wb.Save(outputDir + "outputImportTableOptionsShiftFirstRowDown-False.xlsx");
}
```

## Çözüm

İşte karşınızda! Aspose.Cells for .NET kullanarak ilk satırı taşımadan bir Excel sayfasına DataTable satırlarını nasıl ekleyeceğinizi öğrendiniz. Bu işlem yalnızca Excel içindeki veri manipülasyonunu kolaylaştırmakla kalmaz, aynı zamanda tipik olarak zahmetli bir görevi otomatikleştirerek uygulamanızın performansını da artırır. Araç setinizde bu bilgiyle Excel otomasyon görevlerini daha iyi idare edebilir, zamandan ve emekten tasarruf edebilirsiniz.

## SSS

### Aspose.Cells for .NET nedir?
Aspose.Cells for .NET, geliştiricilerin .NET uygulamalarında Excel dosyaları oluşturmasına, düzenlemesine ve dönüştürmesine olanak tanıyan bir programlama kütüphanesidir.

### Aspose.Cells'i kullanmak için lisansa ihtiyacım var mı?
Evet, tüm özellikler için geçerli bir lisansa ihtiyacınız olacak. Ancak, ilk test için ücretsiz bir deneme mevcuttur.

### Aspose.Cells'i web uygulamalarında kullanabilir miyim?
Kesinlikle! Aspose.Cells, .NET'te geliştirilen masaüstü, web ve bulut tabanlı uygulamalar için mükemmeldir.

### Aspose.Cells ile hangi tür Excel dosyaları oluşturabilirim?
XLSX, XLS, CSV ve daha fazlası dahil olmak üzere çeşitli Excel dosya biçimleri oluşturabilirsiniz.

### Aspose.Cells için desteği nereden alabilirim?
 Sorularınızı sorabilir veya yardım alabilirsiniz.[Aspose forumları](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
