---
"date": "2025-04-08"
"description": "Excel çalışma kitaplarına metin kutuları eklemek ve satır aralığını ayarlamak için Java için Aspose.Cells'i nasıl kullanacağınızı öğrenin. Çalışma kitabı sunumlarınızı biçimlendirilmiş metin şekilleriyle geliştirin."
"title": "Aspose.Cells for Java Kullanarak Excel'de Metin Kutusu Ekleme ve Satır Aralığını Ayarlama"
"url": "/tr/java/images-shapes/aspose-cells-java-add-text-box-line-spacing/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# Aspose.Cells for Java Kullanarak Excel'de Metin Kutusu Ekleme ve Satır Aralığını Ayarlama

## giriiş

Dinamik Excel raporları oluşturmak genellikle özel metin biçimlendirmesi gerektirir, örneğin belirli satır aralığına sahip metin kutuları eklemek gibi. Java için Aspose.Cells ile bu basit ve etkili hale gelir. Bu eğitim, biçimlendirilmiş metin şekilleri eklemek için Java için Aspose.Cells kullanarak çalışma kitabı sunumlarınızı geliştirmenize rehberlik edecektir.

Bu kılavuzun sonunda şunları öğreneceksiniz:
- Yeni bir Excel çalışma kitabı oluşturun ve çalışma sayfalarına erişin
- Çalışma sayfasına bir metin kutusu şekli ekleyin
- Bir metin şeklinin içinde özel satır aralığını ayarlayın
- Biçimlendirilmiş çalışma kitabınızı XLSX biçiminde kaydedin

Öncelikle ortamınızı ayarlayarak başlayalım.

### Ön koşullar

Başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:
- Makinenize Java Geliştirme Kiti (JDK) yüklendi
- Java kodu yazmak için bir IDE veya düzenleyici
- Bağımlılıkları yönetmek üzere yapılandırılmış Maven veya Gradle derleme sistemi

Java programlamaya dair temel bir anlayışa ve Excel dosya yapılarına aşinalığa sahip olmak faydalı olacaktır.

## Java için Aspose.Cells Kurulumu

Maven veya Gradle kullanarak projenizin bağımlılık yönetimine Aspose.Cells'i dahil edin:

**Usta**

Aşağıdaki bağımlılık bloğunu ekleyin `pom.xml` dosya:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**

Bunu da ekleyin `build.gradle` dosya:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

Daha sonra, ücretsiz denemeyi seçerek, geçici lisans talebinde bulunarak veya tam lisans satın alarak Aspose.Cells için bir lisans edinin.

### Aspose.Cells başlatılıyor

Kütüphane projenize dahil edildikten sonra onu Java uygulamanız içerisinde başlatın:

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) {
        // Çalışma Kitabı örneğini başlat (bir Excel dosyasını temsil eder)
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## Uygulama Kılavuzu

### Bir Çalışma Kitabı Oluşturun ve Çalışma Sayfasına Erişin

Yeni bir Excel çalışma kitabı oluşturarak ve ilk çalışma sayfasına erişerek başlayın. Metin kutunuzu buraya ekleyeceksiniz.

#### Genel bakış

Yeni bir çalışma kitabı oluşturmak, ihtiyaç duyulduğunda veri, şekil ve biçimlendirme eklemek için boş bir sayfa sağlar.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

public class ExcelDemo {
    public static void main(String[] args) {
        // Yeni bir Çalışma Kitabı (Excel dosyası) oluşturun
        Workbook workbook = new Workbook();
        
        // İlk çalışma sayfasına erişin
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        System.out.println("Workbook and first worksheet accessed.");
    }
}
```

### Çalışma Sayfasına Metin Kutusu Ekle

Sonra, seçili çalışma sayfanıza bir metin kutusu şekli ekleyin. Bu şekil, ihtiyacınız olan herhangi bir metinsel içeriği içerebilir.

#### Genel bakış

Metin kutuları, notlar veya talimatlar gibi özel metinleri doğrudan bir Excel sayfasına eklemek için çok yönlü araçlardır.

```java
import com.aspose.cells.Shape;
import com.aspose.cells.MsoDrawingType;

public class ExcelDemo {
    public static void main(String[] args) {
        // Yeni bir Çalışma Kitabı (Excel dosyası) oluşturun
        Workbook workbook = new Workbook();
        
        // İlk çalışma sayfasına erişin
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Çalışma sayfasına bir metin kutusu şekli ekleyin
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        System.out.println("Text box added.");
    }
}
```

### Metni Şekilde Ayarla

Metin kutunuz hazır olduğunda içeriğini ayarlayın ve içindeki metni biçimlendirin.

```java
import com.aspose.cells.Shape;

public class ExcelDemo {
    public static void main(String[] args) {
        // Yeni bir Çalışma Kitabı (Excel dosyası) oluşturun
        Workbook workbook = new Workbook();
        
        // İlk çalışma sayfasına erişin
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Çalışma sayfasına bir metin kutusu şekli ekleyin
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Şeklin içine metin içeriği koy
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        System.out.println("Text set in shape.");
    }
}
```

### Şekildeki Metin Paragraflarına Erişim

Belirli biçimlendirmeleri uygulamak için metin kutusu içindeki ayrı paragraflara erişebilirsiniz.

```java
import com.aspose.cells.TextParagraph;

public class ExcelDemo {
    public static void main(String[] args) {
        // Yeni bir Çalışma Kitabı (Excel dosyası) oluşturun
        Workbook workbook = new Workbook();
        
        // İlk çalışma sayfasına erişin
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Çalışma sayfasına bir metin kutusu şekli ekleyin
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Şeklin içine metin içeriği koy
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Şekildeki ikinci paragrafa erişin
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);
        
        System.out.println("Accessed second paragraph in text box.");
    }
}
```

### Paragrafın Satır Aralığını Ayarla

Satır aralığını özelleştirmek okunabilirliği artırabilir. İşte nasıl ayarlayacağınız:

```java
import com.aspose.cells.LineSpaceSizeType;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Yeni bir Çalışma Kitabı (Excel dosyası) oluşturun
        Workbook workbook = new Workbook();
        
        // İlk çalışma sayfasına erişin
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Çalışma sayfasına bir metin kutusu şekli ekleyin
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Şeklin içine metin içeriği koy
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Şekildeki ikinci paragrafa erişin
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Satır aralığını 20 puntoya ayarlayın
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // Paragraftan önce ve sonra boşluk yapılandırın
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        System.out.println("Line spacing set.");
    }
}
```

### Çalışma Kitabını Kaydet

Son olarak çalışma kitabınızı yeni eklediğiniz ve biçimlendirdiğiniz metin kutusuyla kaydedin.

```java
import com.aspose.cells.SaveFormat;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Yeni bir Çalışma Kitabı (Excel dosyası) oluşturun
        Workbook workbook = new Workbook();
        
        // İlk çalışma sayfasına erişin
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Çalışma sayfasına bir metin kutusu şekli ekleyin
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Şeklin içine metin içeriği koy
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Şekildeki ikinci paragrafa erişin
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Satır aralığını 20 puntoya ayarlayın
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // Paragraftan önce ve sonra boşluk yapılandırın
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        // Çalışma kitabını kaydet
        workbook.save("StyledTextShape.xlsx", SaveFormat.XLSX);
    }
}
```

## Çözüm

Aspose.Cells for Java kullanarak bir Excel çalışma kitabına metin kutusu eklemeyi ve satır aralığını ayarlamayı başarıyla öğrendiniz. Bu, dinamik, görsel olarak çekici raporlar oluşturma yeteneğinizi geliştirir.

## Anahtar Kelime Önerileri
- "Java için Aspose.Cells"
- "Excel'e Metin Kutusu Ekle"
- "Excel'de Satır Aralığını Ayarla"
- "Stillendirilmiş Metinli Excel Çalışma Kitabı"
- "Java ve Aspose.Cells"


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}