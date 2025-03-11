---
title: XLS ve XLSX Biçimleri Tarafından Desteklenen Maksimum Satır ve Sütunları Bul
linktitle: XLS ve XLSX Biçimleri Tarafından Desteklenen Maksimum Satır ve Sütunları Bul
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Aspose.Cells for .NET kullanarak XLS ve XLSX formatlarının desteklediği maksimum satır ve sütunları keşfedin. Bu kapsamlı eğitimle Excel veri yönetiminizi en üst düzeye çıkarın.
weight: 11
url: /tr/net/workbook-settings/find-maximum-supported-rows-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# XLS ve XLSX Biçimleri Tarafından Desteklenen Maksimum Satır ve Sütunları Bul

## giriiş
Excel dünyasında, büyük veri kümelerini yönetmek, özellikle farklı dosya biçimleri tarafından desteklenen maksimum satır ve sütun sayısını işlemek söz konusu olduğunda, zorlu bir görev olabilir. Bu eğitim, Aspose.Cells for .NET kitaplığını kullanarak XLS ve XLSX biçimleri tarafından desteklenen maksimum satır ve sütun sayısını bulma sürecinde size rehberlik edecektir. Bu makalenin sonunda, Excel ile ilgili görevlerinizi verimli bir şekilde yönetmek için bu güçlü aracı nasıl kullanacağınıza dair kapsamlı bir anlayışa sahip olacaksınız.
## Ön koşullar
Eğitime başlamadan önce aşağıdaki ön koşulların mevcut olduğundan emin olun:
1. [.NET Çerçevesi](https://dotnet.microsoft.com/en-us/download) veya[.NET Çekirdeği](https://dotnet.microsoft.com/en-us/download) sisteminize yüklenmiştir.
2. [.NET için Aspose.Cells](https://releases.aspose.com/cells/net/) Projenizde indirilen ve referans alınan kütüphane.
 Henüz yapmadıysanız, Aspose.Cells for .NET kitaplığını şu adresten indirebilirsiniz:[web sitesi](https://releases.aspose.com/cells/net/) veya şunu kullanarak yükleyin:[NuGet](https://www.nuget.org/packages/Aspose.Cells/).
## Paketleri İçe Aktar
Başlamak için, Aspose.Cells for .NET kütüphanesinden gerekli paketleri içe aktarmanız gerekir. Aşağıdaki using ifadelerini C# dosyanızın en üstüne ekleyin:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## Adım 1: XLS Formatının Desteklediği Maksimum Satır ve Sütun Sayısını Bulun
XLS (Excel 97-2003) formatının desteklediği maksimum satır ve sütun sayısını inceleyerek başlayalım.
```csharp
// XLS formatı hakkında mesaj yazdır.
Console.WriteLine("Maximum Rows and Columns supported by XLS format.");
// XLS formatında çalışma kitabı oluşturun.
Workbook wb = new Workbook(FileFormatType.Excel97To2003);
// XLS formatının desteklediği maksimum satır ve sütun sayısını yazdır.
int maxRows = wb.Settings.MaxRow + 1;
int maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
Console.WriteLine();
```
Bu adımda:
1. XLS formatıyla çalıştığımızı belirtmek için bir mesaj yazdırın.
2.  Yeni bir tane oluştur`Workbook` örneğini kullanarak`FileFormatType.Excel97To2003` XLS formatını temsil eden enum.
3.  XLS biçimi tarafından desteklenen maksimum satır ve sütun sayısını alın`Workbook.Settings.MaxRow` Ve`Workbook.Settings.MaxColumn`sırasıyla özellikler. Gerçek maksimum satır ve sütun numaralarını elde etmek için bu değerlere 1 ekliyoruz (sıfır tabanlı oldukları için).
4. Konsola maksimum satır ve sütun sayısını yazdır.
## Adım 2: XLSX Biçimi Tarafından Desteklenen Maksimum Satır ve Sütun Sayısını Bulun
Şimdi XLSX (Excel 2007 ve sonrası) biçiminin desteklediği maksimum satır ve sütun sayısını inceleyelim.
```csharp
// XLSX formatı hakkında mesaj yazdır.
Console.WriteLine("Maximum Rows and Columns supported by XLSX format.");
// XLSX formatında çalışma kitabı oluşturun.
wb = new Workbook(FileFormatType.Xlsx);
// XLSX formatının desteklediği maksimum satır ve sütun sayısını yazdır.
maxRows = wb.Settings.MaxRow + 1;
maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
```
Bu adımda:
1. XLSX formatıyla çalıştığımızı belirtmek için bir mesaj yazdırın.
2.  Yeni bir tane oluştur`Workbook` örneğini kullanarak`FileFormatType.Xlsx` XLSX formatını temsil eden enum.
3.  XLSX biçimi tarafından desteklenen maksimum satır ve sütun sayısını alın`Workbook.Settings.MaxRow` Ve`Workbook.Settings.MaxColumn`sırasıyla özellikler. Gerçek maksimum satır ve sütun numaralarını elde etmek için bu değerlere 1 ekliyoruz (sıfır tabanlı oldukları için).
4. Konsola maksimum satır ve sütun sayısını yazdır.
## Adım 3: Başarılı Mesajını Göster
Son olarak, "FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats" örneğinin başarıyla yürütüldüğünü belirtmek için bir başarı mesajı görüntüleyelim.
```csharp
Console.WriteLine("FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats executed successfully.");
```
Bu adım konsola bir başarı mesajı yazdırır.
## Çözüm
Bu eğitimde, XLS ve XLSX dosya biçimleri tarafından desteklenen maksimum satır ve sütunları bulmak için Aspose.Cells for .NET kitaplığını nasıl kullanacağınızı öğrendiniz. Bu biçimlerin sınırlamalarını anlayarak, verilerinizin desteklenen aralıklara uymasını sağlayarak Excel tabanlı projelerinizi daha iyi planlayabilir ve yönetebilirsiniz.
## SSS
### XLS formatı tarafından desteklenen maksimum satır sayısı nedir?
XLS (Excel 97-2003) formatının desteklediği maksimum satır sayısı 65.536'dır.
### XLS formatı tarafından desteklenen maksimum sütun sayısı nedir?
XLS (Excel 97-2003) biçiminin desteklediği maksimum sütun sayısı 256'dır.
### XLSX formatı tarafından desteklenen maksimum satır sayısı nedir?
XLSX (Excel 2007 ve sonrası) biçimi tarafından desteklenen maksimum satır sayısı 1.048.576'dır.
### XLSX formatı tarafından desteklenen maksimum sütun sayısı nedir?
XLSX (Excel 2007 ve sonrası) biçimi tarafından desteklenen maksimum sütun sayısı 16.384'tür.
### Aspose.Cells for .NET kitaplığını diğer Excel dosya formatlarıyla çalışmak için kullanabilir miyim?
 Evet, Aspose.Cells for .NET kitaplığı XLS, XLSX, ODS ve daha fazlası dahil olmak üzere çok çeşitli Excel dosya biçimlerini destekler.[belgeleme](https://reference.aspose.com/cells/net/) Mevcut özellikler ve işlevler hakkında bilgi edinmek için.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
