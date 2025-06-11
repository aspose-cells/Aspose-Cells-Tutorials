---
"description": "Aspose.Cells for Java kullanarak Excel'de pivot tabloların nasıl oluşturulacağını öğrenin. Kaynak kod örnekleriyle veri gruplandırma ve analizini otomatikleştirin."
"linktitle": "Pivot Tablolarda Verileri Gruplandırma"
"second_title": "Aspose.Cells Java Excel İşleme API'si"
"title": "Pivot Tablolarda Verileri Gruplandırma"
"url": "/tr/java/excel-pivot-tables/grouping-data-in-pivot-tables/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Pivot Tablolarda Verileri Gruplandırma


Pivot tablolar, elektronik tablolardaki verileri analiz etmek ve özetlemek için güçlü bir araçtır. Değerli içgörüler elde etmek için verileri gruplandırmanıza ve kategorilere ayırmanıza olanak tanır. Bu makalede, Java için Aspose.Cells'i kullanarak pivot tablolardaki verileri etkili bir şekilde nasıl gruplandıracağınızı ve kaynak kod örneklerini inceleyeceğiz.

## giriiş

Pivot tablolar, büyük veri kümelerinden gelen verileri düzenlemek ve özetlemek için esnek bir yol sunar. Verilerinizi kategorilere veya hiyerarşilere gruplayarak özel görünümler oluşturmanıza olanak tanır. Bu, verilerinizdeki eğilimleri, kalıpları ve aykırı değerleri daha kolay belirlemenize yardımcı olabilir.

## Adım 1: Pivot Tablo Oluşturun

Java için Aspose.Cells kullanarak bir pivot tablo oluşturarak başlayalım. Aşağıda örnek bir Excel dosyasından bir pivot tablonun nasıl oluşturulacağına dair bir örnek verilmiştir.

```java
// Excel dosyasını yükleyin
Workbook workbook = new Workbook("sample.xlsx");

// Verileri içeren çalışma sayfasına erişin
Worksheet worksheet = workbook.getWorksheets().get(0);

// Veri aralığını belirtin
CellArea sourceData = new CellArea();
sourceData.startRow = 0;
sourceData.endRow = 19; // 20 satır veri varsayıldığında
sourceData.startColumn = 0;
sourceData.endColumn = 3; // 4 sütun veri varsayıldığında

// Veri aralığına göre bir pivot tablo oluşturun
int index = worksheet.getPivotTables().add(sourceData, "A1", "PivotTable1");

// Pivot tabloyu dizine göre al
PivotTable pivotTable = worksheet.getPivotTables().get(index);

// Satırlara ve sütunlara alanlar ekleyin
pivotTable.addFieldToArea("Product", PivotFieldType.ROW);
pivotTable.addFieldToArea("Region", PivotFieldType.COLUMN);

// Değerleri ekleyin ve toplamayı uygulayın
pivotTable.addFieldToArea("Sales", PivotFieldType.DATA);
pivotTable.getDataFields().get(0).setFunction(PivotFieldFunction.SUM);

// Değiştirilen Excel dosyasını kaydedin
workbook.save("output.xlsx");
```

## Adım 2: Verileri Gruplandır

Java için Aspose.Cells'de, pivot tablo içindeki verileri şu şekilde gruplayabilirsiniz: `PivotField` sınıf. Pivot tabloda bir alanın nasıl gruplandırılacağına dair bir örnek:

```java
// Pivot tabloda "Ürün" alanına erişin
PivotField productField = pivotTable.getPivotFields().get("Product");

// "Ürün" alanını belirli bir ölçüte göre gruplandırın, örneğin başlangıç harfine göre
productField.setIsAutoSubtotals(false);
productField.setBaseField("Product");
productField.setAutoSort(true);
productField.setAutoShow(true);

// Değiştirilen Excel dosyasını gruplanmış verilerle kaydedin
workbook.save("output_grouped.xlsx");
```

## Adım 3: Gruplamayı Özelleştirin

Tarih tabanlı gruplama aralıkları veya özel gruplama kuralları gibi gruplama ayarlarını daha da özelleştirebilirsiniz. İşte tarih tabanlı gruplamayı özelleştirmenin bir örneği:

```java
// Pivot tabloda "Tarih" alanına erişin (bir tarih alanı olduğunu varsayarak)
PivotField dateField = pivotTable.getPivotFields().get("Date");

// Aylara göre grup tarihleri
dateField.setIsAutoSubtotals(false);
dateField.setIsDateGroup(true);
dateField.setDateGroupingType(PivotFieldDateGroupingType.MONTHS);

// Değiştirilen Excel dosyasını özel tarih gruplandırmasıyla kaydedin
workbook.save("output_custom_grouping.xlsx");
```

## Çözüm

Pivot tablolarda veri gruplandırma, Excel'de veri analiz etmek ve özetlemek için değerli bir tekniktir ve Java için Aspose.Cells bu süreci otomatikleştirmeyi kolaylaştırır. Sağlanan kaynak kodu örnekleriyle, pivot tablolar oluşturabilir, gruplandırmayı özelleştirebilir ve verilerinizden verimli bir şekilde içgörüler elde edebilirsiniz.

## SSS

### 1. Excel'deki pivot tabloların amacı nedir?

Excel'deki pivot tablolar büyük veri kümelerini özetlemek ve analiz etmek için kullanılır. Verilerinizin özel görünümlerini oluşturmanıza olanak tanır ve bu da kalıpları ve eğilimleri belirlemeyi kolaylaştırır.

### 2. Pivot tablodaki verilerin gruplandırılmasını nasıl özelleştirebilirim?

Pivot tablodaki verilerin gruplandırılmasını, şunu kullanarak özelleştirebilirsiniz: `PivotField` Java için Aspose.Cells'deki sınıf. Bu, tarih tabanlı aralıklar veya özel kurallar gibi gruplama ölçütlerini belirtmenize olanak tanır.

### 3. Java için Aspose.Cells'i kullanarak pivot tabloların oluşturulmasını otomatikleştirebilir miyim?

Evet, sağlanan kaynak kod örneklerinde gösterildiği gibi, Java için Aspose.Cells'i kullanarak Excel'de pivot tabloların oluşturulmasını otomatikleştirebilirsiniz.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}