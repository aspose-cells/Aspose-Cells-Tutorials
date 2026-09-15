---
category: general
date: 2026-03-01
description: HTML ve diğer formatlarda yazı tiplerini nasıl gömeceğinizi öğrenin.
  HTML'de yazı tipi gömme, Excel'i HTML'ye dönüştürme, OLE'yi dışa aktarma ve Excel'i
  XPS'ye dönüştürme konularını kapsayan adım adım öğretici.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- convert excel to html
- how to export ole
- convert excel to xps
language: tr
og_description: HTML, XPS ve OLE dışa aktarımlarında yazı tiplerini nasıl gömülür.
  Tam iş akışını öğrenin, çalıştırılabilir Java kodunu görün ve Excel dönüşümleri
  için HTML'de yazı tiplerini gömme konusunda uzmanlaşın.
og_title: Yazı Tiplerini Gömme – Tam Java Öğreticisi
tags:
- Aspose.Cells
- Java
- Document Export
title: Yazı Tiplerini Gömme – HTML, XPS ve OLE Dışa Aktarım İçin Tam Kılavuz
url: /tr/java/ole-objects-embedded-content/how-to-embed-fonts-complete-guide-for-html-xps-and-ole-expor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Yazı Tiplerini Gömme – HTML, XPS ve OLE Dışa Aktarma İçin Tam Kılavuz

Hiç Excel çalışma kitabını bir web sayfasına ya da yazdırılabilir bir belgeye dönüştürürken **yazı tiplerini nasıl gömeceğinizi** merak ettiniz mi? Yalnız değilsiniz. Birçok geliştirici, çıktının kendi makinesinde güzel görünürken başka birinde eksik yazı tipleri nedeniyle bozulmasıyla karşılaşır.  

Bu öğreticide Aspose.Cells for Java kullanarak gerçek bir senaryoyu adım adım inceleyeceğiz: HTML'de yazı tiplerini gömecek, XPS'e dönüştürürken emoji varyasyon seçicilerini koruyacak ve PPTX'e dışa aktarırken bir OLE nesnesinin düzenlenebilirliğini bile tutacağız. Sonunda “yazı tiplerini nasıl gömeceğim” sorusuna yanıt veren, aynı zamanda **embed fonts in html**, **convert excel to html**, **how to export ole**, ve **convert excel to xps** konularına da değinen sağlam bir kopyala‑yapıştır çözümüne sahip olacaksınız.

## Ön Koşullar

- Java 17 (veya herhangi bir güncel JDK)  
- Aspose.Cells for Java 25.x veya üzeri  
- Bir geliştirme IDE'si (IntelliJ IDEA, Eclipse veya VS Code)  
- Excel veri yapılarıyla temel aşinalık  

Harici hizmetlere gerek yok—her şey yerel olarak çalışır.

## Çözümün Genel Görünümü

1. **Bir çalışma kitabı oluşturun** ve `WRAPCOLS` işlevini kullanarak dikey bir aralığı üç sütunlu bir düzene dönüştürün.  
2. **Çalışma kitabını XPS olarak kaydedin** ve yazı tipi varyasyon seçicilerini etkinleştirerek emoji'lerin bozulmadan kalmasını sağlayın.  
3. **HTML'ye dışa aktarın** gömülü yazı tipleriyle, sayfanın her yerde aynı görünmesini garantileyin.  
4. **OLE nesnesi içeren bir çalışma kitabını PPTX'e dışa aktarın**, düzenlenebilirliği koruyarak.  
5. **Smart Marker şablonu uygulayın**; bu, master‑detail veri bağlamasını gösterir.  

Her adım kendi H2 bölümünde izole edilmiştir, bu da kılavuzu hem arama motorları hem de AI asistanları için hızlıca göz atmayı kolaylaştırır.

![Yazı tiplerini gömme illüstrasyonu](image.png "yazı tiplerini gömme")

*Görsel alt metni: Excel'den HTML, XPS ve PPTX'e iş akışını gösteren yazı tiplerini gömme diyagramı.*

---

## Adım 1 – Bir Çalışma Kitabı Oluşturun ve WRAPCOLS Kullanarak (embed fonts in html için Bunun Önemi)

Yazı tiplerini gömmekten önce, içinde veri bulunan bir çalışma kitabına ihtiyacımız var. `WRAPCOLS` işlevi, tek bir sütunu birden fazla sütuna bölmenin pratik bir yoludur ve bu genellikle son HTML'nin daha okunabilir olmasını sağlar.

```java
import com.aspose.cells.*;

public class EmbedFontsDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Populate A2:A10 with sample data
        for (int i = 2; i <= 10; i++) {
            sheet.getCells().get("A" + i).putValue("Item " + (i - 1));
        }

        // Use WRAPCOLS to create a 3‑column block starting at A1
        Cell resultCell = sheet.getCells().get("A1");
        resultCell.setFormula("=WRAPCOLS(A2:A10,3)");
        workbook.calculateFormula();

        System.out.println("WRAPCOLS result: " + resultCell.getStringValue());
        // -----------------------------------------------------------------
        // The rest of the steps are demonstrated after this point.
        // -----------------------------------------------------------------
```

**Neden bu adım?**  
`WRAPCOLS` çağrısı, daha sonra HTML'de bir tablo olarak görülen çok sütunlu bir aralık oluşturur. Daha sonra **embed fonts in html** yaptığımızda, tablonun stilini gömdüğümüz yazı tipleri belirler ve tarayıcılar arasında tutarlı bir render sağlanır.

---

## Adım 2 – Çalışma Kitabını Emoji'leri Koruyarak XPS Olarak Kaydedin (convert excel to xps)

Baskıya hazır bir format gerekiyorsa, XPS sağlam bir tercihtir. Ancak, modern belgeler genellikle varyasyon seçicileri kullanan emoji veya semboller içerir. `EnableFontVariationSelectors` özelliğini açmak, bu karakterlerin dönüşüm sırasında korunmasını sağlar.

```java
        // --------------------------------------------------------------
        // Step 2: Save as XPS with font variation selectors enabled
        // --------------------------------------------------------------
        WorkbookSettings settings = workbook.getSettings();
        settings.setEnableFontVariationSelectors(true); // crucial for emoji

        String xpsPath = "output/withVariations.xps";
        workbook.save(xpsPath, SaveFormat.XPS);
        System.out.println("Workbook saved as XPS at: " + xpsPath);
```

**Ne elde edersiniz:**  
Kaynak çalışma kitabındaki gömülü emoji'leri tam olarak aynı şekilde gösteren bir XPS dosyası. Bu, **convert excel to xps** gereksinimini karşılar ve yazı tipi işlemenin yalnızca HTML ile sınırlı olmadığını gösterir.

---

## Adım 3 – Gömülü Yazı Tipleriyle HTML'ye Dışa Aktarın (how to embed fonts & embed fonts in html)

Şimdi öğreticinin özüne ulaşıyoruz: Excel'i HTML'ye dönüştürürken **how to embed fonts**. Aspose.Cells, oluşturulan HTML dosyasına doğrudan yazı tiplerini gömmemizi sağlar ve harici font dosyalarına ihtiyaç kalmaz.

```java
        // --------------------------------------------------------------
        // Step 3: Export to HTML with embedded fonts
        // --------------------------------------------------------------
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
        htmlOptions.setEmbedFonts(true); // this is the key line for embed fonts in html
        htmlOptions.setExportImagesAsBase64(true); // optional, keeps all assets in one file

        String htmlPath = "output/embeddedFonts.html";
        workbook.save(htmlPath, htmlOptions);
        System.out.println("HTML with embedded fonts saved at: " + htmlPath);
```

**Nasıl çalışır:**  
`setEmbedFonts(true)` renderlayıcıya, çalışma kitabında kullanılan font dosyalarını okuyup bunları `<style>` etiketi içinde Base64‑kodlu `@font-face` kuralları olarak gömmesini söyler. Ortaya çıkan HTML bağımsızdır, bu yüzden herhangi bir sunucuya koyduğunuzda fontlar doğru şekilde render edilir—tam da geliştiricilerin **how to embed fonts** aradığında istedikleri şey.

**Beklenen çıktı snippet'i (`embeddedFonts.html` içinde):**

```html
<style>
@font-face{font-family:"Arial";src:url(data:font/ttf;base64,AAEAAA... ) format('truetype');}
</style>
<table>
  <tr><td>Item 1</td><td>Item 4</td><td>Item 7</td></tr>
  <tr><td>Item 2</td><td>Item 5</td><td>Item 8</td></tr>
  <tr><td>Item 3</td><td>Item 6</td><td>Item 9</td></tr>
</table>
```

`@font-face` kuralına dikkat edin—bu, **embed fonts in html** sorusunun somut yanıtıdır.

---

## Adım 4 – OLE Nesnesi İçeren Bir Çalışma Kitabını PPTX'e Dışa Aktarın (how to export ole)

Birçok iş raporu, Word belgelerini, PDF'leri veya diğer Excel sayfalarını OLE nesneleri olarak gömer. Böyle bir çalışma kitabını PowerPoint'e dışa aktardığınızda, genellikle nesneyi düzenleme yeteneğini kaybedersiniz. Aspose.Cells, düzenlenebilirliği kutudan çıkar çıkmaz korur.

```java
        // --------------------------------------------------------------
        // Step 4: Export a workbook with an OLE object to PPTX
        // --------------------------------------------------------------
        // Load a workbook that already contains an OLE object.
        Workbook oleWorkbook = new Workbook("input/oleObject.xlsx");

        String pptxPath = "output/oleEditable.pptx";
        oleWorkbook.save(pptxPath, SaveFormat.PPTX);
        System.out.println("PPTX with editable OLE object saved at: " + pptxPath);
```

**Neden önemli:**  
**how to export ole** arıyorsanız, bu snippet tam API çağrısını gösterir. Ortaya çıkan PowerPoint slaytı, OLE nesnesini çift tıklayarak düzenlenebilen canlı bir bileşen olarak içerir—ekstra bir işlem gerektirmez.

---

## Adım 5 – Smart Marker Şablonu Uygulayın (master‑detail) ve Demo'yu Tamamlayın

Smart Marker'lar, bir veri kaynağını (Map, JSON, DataTable) doğrudan bir Excel şablonuna bağlamanızı sağlar. İşte master‑detail satırlarını yazdıran minimal bir örnek.

```java
        // --------------------------------------------------------------
        // Step 5: Apply Smart Marker template (master‑detail)
        // --------------------------------------------------------------
        String smartMarkerTemplate = "${Orders.Master:OrderID,Customer}\n${Orders.Detail:Product,Qty,Price}";
        // Simulated data source
        java.util.Map<String, Object> dataSource = new java.util.HashMap<>();
        java.util.List<java.util.Map<String, Object>> master = new java.util.ArrayList<>();
        java.util.Map<String, Object> masterRow = new java.util.HashMap<>();
        masterRow.put("OrderID", 1001);
        masterRow.put("Customer", "Acme Corp");
        master.add(masterRow);
        dataSource.put("Orders.Master", master);

        java.util.List<java.util.Map<String, Object>> detail = new java.util.ArrayList<>();
        java.util.Map<String, Object> detailRow = new java.util.HashMap<>();
        detailRow.put("Product", "Widget");
        detailRow.put("Qty", 5);
        detailRow.put("Price", 9.99);
        detail.add(detailRow);
        dataSource.put("Orders.Detail", detail);

        SmartMarkerProcessor processor = new SmartMarkerProcessor(new Workbook());
        processor.apply(smartMarkerTemplate, dataSource);
        processor.getWorkbook().save("output/smartMarkerResult.xlsx");
        System.out.println("Smart Marker workbook saved.");
    }
}
```

**Ne görüyorsunuz:**  
Şablon yer tutucularının veriyle değiştirildiği yeni bir çalışma kitabı (`smartMarkerResult.xlsx`). Bu adım doğrudan fontlarla ilgili değil, ancak genellikle **embed fonts in html** dışa aktarımından önce gelen tipik bir raporlama iş akışını göstererek öğreticiyi tamamlar.

---

## Yaygın Tuzaklar ve Uzman İpuçları (Başarılı Yazı Tipi Gömmeyi Sağlamak)

| Sorun | Neden Oluşur | Çözüm |
|-------|----------------|-----|
| HTML dosyasında fontlar eksik | Çalışma kitabı, sunucuda yüklü olmayan bir sistem fontu kullanıyor. | Veri yüklemeden önce `Workbook.getSettings().setDefaultFont("Arial")` kullanın veya gerekli font dosyalarını manuel olarak gömün. |
| Çıktı HTML'si çok büyük | Birçok büyük fontun gömülmesi dosya boyutunu şişirir. | Sadece gerçekten kullandığınız fontları gömmekle sınırlayın: `htmlOptions.setFontEmbeddingMode(HtmlFontEmbeddingMode.EmbedSubset)`. |
| Emoji, XPS dönüşümünden sonra kaybolur | Varyasyon seçicileri varsayılan olarak kaldırılır. | Adım 2'de gösterildiği gibi `settings.setEnableFontVariationSelectors(true)` etkinleştirin. |
| OLE nesnesi PPTX'te statik bir görüntü olur | Kaynak çalışma kitabı `setSuppressOLEObjects(true)` ile kaydedildi. | PPTX kaydederken OLE nesnelerini **bastırmadığınızdan** emin olun. |

## Sonuçları Doğrulama

1. `embeddedFonts.html` dosyasını Chrome/Firefox'ta açın. Tablo, o font makinede yüklü olmasa bile gömülü font (ör. Arial) kullanılarak görüntülenmelidir.  
2. `withVariations.xps` dosyasını Windows XPS Viewer'da açın. 👍 gibi emoji'ler doğru şekilde render edilmelidir.  
3. `oleEditable.pptx` dosyasını PowerPoint'te açın. OLE şekline çift tıklayın;

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}