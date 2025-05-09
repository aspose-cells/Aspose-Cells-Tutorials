---
"date": "2025-04-08"
"description": "Aspose.Cells for Java kullanarak Excel sayfalarını iç içe geçmiş verilerle verimli bir şekilde nasıl dolduracağınızı öğrenin. Bu kılavuz, çalışma kitaplarını ayarlamayı, akıllı işaretçileri uygulamayı ve karmaşık veri kümelerini işlemeyi kapsar."
"title": "Aspose.Cells for Java Kullanarak Excel'i İç İçe Verilerle Doldurun&#58; Kapsamlı Bir Kılavuz"
"url": "/tr/java/data-manipulation/populate-excel-nested-data-aspose-cells-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Aspose.Cells for Java Kullanarak Excel'i İç İçe Verilerle Doldurun

## giriiş

Excel'de iç içe geçmiş veri yapılarını etkin bir şekilde yönetmek zor olabilir. **Java için Aspose.Cells** Akıllı işaretçileri kullanarak Excel çalışma kitaplarını dinamik olarak doldurmak için güçlü bir çözüm sunar. Bu eğitim, bireyler ve aile üyeleri gibi karmaşık veri kümelerini kolaylıkla işleyebilmenizi sağlayarak sizi süreç boyunca yönlendirecektir.

Bu kılavuzu takip ederek şunları öğreneceksiniz:
- Yeni bir çalışma kitabı ve çalışma sayfası ayarlayın.
- Verimli veri doldurma için akıllı işaretleyicileri uygulayın.
- Kapsamlı veri kümeleri için Java'da iç içe geçmiş nesne yapıları oluşturun.
- Çalışma kitabını Aspose.Cells' WorkbookDesigner sınıfını kullanarak işleyin.

Uygulamaya geçmeden önce, ortamınızın tüm gerekli ön koşullara uygun şekilde kurulduğundan emin olalım.

## Ön koşullar

Devam etmeden önce şunlara sahip olduğunuzdan emin olun:
- **Java Geliştirme Kiti (JDK)**: Sisteminizde JDK 8 veya üzeri sürümün yüklü olduğundan emin olun.
- **Java için Aspose.Cells**: Aspose.Cells kütüphanesini aşağıda ayrıntılı olarak açıklandığı gibi Maven veya Gradle kullanarak projenize ekleyin.
- **Geliştirme Ortamı**: IntelliJ IDEA, Eclipse veya NetBeans gibi bir metin editörü veya IDE kullanın.

### Gerekli Kütüphaneler ve Bağımlılıklar

Projenize Aspose.Cells'i dahil etmek için:

**Usta:**
```xml
<dependency>
  <groupId>com.aspose</groupId>
  <artifactId>aspose-cells</artifactId>
  <version>25.3</version>
</dependency>
```

**Gradle:**
```gradle
implementation group: 'com.aspose', name: 'aspose-cells', version: '25.3'
```

### Lisans Edinimi

Aspose.Cells'i kullanmak için şunları yapabilirsiniz:
- **Ücretsiz Deneme**: Kütüphaneyi indirin ve geçici değerlendirme lisansıyla başlayın.
- **Satın almak**: Üretim amaçlı kullanım için tam lisans edinin.

Ziyaret etmek [Aspose Satın Alma](https://purchase.aspose.com/buy) lisans edinme hakkında daha fazla bilgi edinmek için. Ücretsiz deneme için şuraya gidin: [Aspose Sürümleri](https://releases.aspose.com/cells/java/).

## Java için Aspose.Cells Kurulumu

Ön koşullar bölümünde açıklandığı gibi projenize Aspose.Cells bağımlılığını ekleyerek başlayın. Kütüphaneyi ekledikten sonra, onu Java uygulamanızda başlatın.

İşte temel bir kurulum:
```java
import com.aspose.cells.Workbook;

public class AsposeCellsSetup {
    public static void main(String[] args) {
        // Yeni bir Çalışma Kitabı nesnesi başlatın.
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java is set up and ready to use!");
    }
}
```

Bu kod parçası Aspose.Cells ile çalışmaya başlamanın ne kadar basit olduğunu göstermektedir. Herhangi bir kodu daha fazla çalıştırmadan önce ortamınızın kütüphaneyi tanıdığından emin olun.

## Uygulama Kılavuzu

Uygulamamızı, her biri Aspose.Cells for Java'nın belirli işlevlerine odaklanan yönetilebilir bölümlere ayıralım.

### Başlangıç Verileri ile Bir Çalışma Kitabı Oluşturma

#### Genel bakış

Bu bölüm yeni bir çalışma kitabının başlatılmasını ve akıllı işaretçiler kullanılarak ilk çalışma sayfasında başlangıç başlıklarının ayarlanmasını içerir.

**Uygulama Adımları:**
1. **Çalışma Kitabını ve Çalışma Sayfasını Başlat**:
   - Bir örnek oluşturun `Workbook`.
   - Çalışma kitabından ilk çalışma sayfasına erişin.
2. **Sütun Başlıklarını Ayarla**:
   - A, B, C ve D sütunları için başlıkları tanımlayın.
3. **Akıllı İşaretleyicileri Uygulayın**:
   - Veri yer tutucularını hazırlamak için akıllı işaretleyicileri kullanın.

**Kod Uygulaması:**
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

public class InitializeWorkbook {
    public static void main(String[] args) throws Exception {
        // Yeni bir çalışma kitabı başlatın ve ilk çalışma sayfasını alın.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // A, B, C ve D sütunları için başlıkları ayarlayın.
        worksheet.getCells().get("A1").putValue("Person Name");
        worksheet.getCells().get("B1").putValue("Person Age");
        worksheet.getCells().get("C1").putValue("Wife Name");
        worksheet.getCells().get("D1").putValue("Wife Age");

        // Veri doldurma için akıllı işaretçiler ayarlayın.
        worksheet.getCells().get("A2").putValue("&=Individual.Name");
        worksheet.getCells().get("B2").putValue("&=Individual.Age");
        worksheet.getCells().get("C2").putValue("&=Individual.Wife.Name");
        worksheet.getCells().get("D2").putValue("&=Individual.Wife.Age");

        // Çalışma kitabını kaydetmek için yer tutucu yol.
        String outDir = "YOUR_OUTPUT_DIRECTORY";
        workbook.save(outDir + "/UsingNestedObjects-out.xlsx");
    }
}
```

### Veri Kaynağı için İç İçe Nesnelerin Bir Listesini Oluşturma

#### Genel bakış

Bu adım, Excel çalışma kitabımızda veri kaynağı olarak kullanılacak iç içe geçmiş veri yapılarını temsil eden Java sınıfları oluşturmayı içerir.

**Uygulama Adımları:**
1. **Sınıf Yapısını Tanımla**:
   - Yaratmak `Individual` Ve `Person` sınıflar.
   - Gerekli alanları ve oluşturucuları ekleyin.
2. **Veri Listesi Oluştur**:
   - Nesneleri örneklendir `Individual`her biri iç içe geçmiş bir `Person`.

**Kod Uygulaması:**
```java
import java.util.ArrayList;

// Birey ve Kişi için sınıf yapılarını tanımlayın.
class Individual {
    String name;
    int age;
    Person wife;

    public Individual(String name, int age, Person wife) {
        this.name = name;
        this.age = age;
        this.wife = wife;
    }
}

class Person {
    String name;
    int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

// İç içe geçmiş Eş ayrıntılarıyla Bireysel nesnelerin bir listesini oluşturun.
public class CreateDataList {
    public static void main(String[] args) {
        ArrayList<Individual> individuals = new ArrayList<>();
        individuals.add(new Individual("John", 23, new Person("Jill", 20)));
        individuals.add(new Individual("Jack", 25, new Person("Hilly", 21)));
        individuals.add(new Individual("James", 26, new Person("Hally", 22)));
        individuals.add(new Individual("Baptist", 27, new Person("Newly", 23)));

        System.out.println("Data list created successfully!");
    }
}
```

### Çalışma Kitabını Akıllı İşaretleyiciler ve Veri Kaynağı ile İşleme

#### Genel bakış

Burada, kullanacaksınız `WorkbookDesigner` Akıllı işaretleyicileri ve veri kaynağını kullanarak çalışma kitabınızı işlemek için.

**Uygulama Adımları:**
1. **WorkbookDesigner'ı Başlat**:
   - Bir örnek oluşturun `WorkbookDesigner`.
2. **Veri Kaynağını Ata**:
   - Akıllı belirteçleri işlemek için bireylerin listesini veri kaynağı olarak ayarlayın.
3. **Çalışma Kitabını İşle**:
   - Kullanın `process` çalışma kitabını iç içe geçmiş verilerinizle doldurma yöntemi.

**Kod Uygulaması:**
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorkbookDesigner;

public class ProcessWorkbook {
    public static void main(String[] args) throws Exception {
        // Çalışma kitabını işlemek için bir WorkbookDesigner ayarlayın.
        Workbook workbook = new Workbook("YOUR_OUTPUT_DIRECTORY/UsingNestedObjects-out.xlsx");
        WorkbookDesigner designer = new WorkbookDesigner();
        designer.setWorkbook(workbook);

        // 'Bireylerin' önceki adımlardan zaten doldurulduğunu varsayarak
        ArrayList<Individual> individuals = new ArrayList<>();
        individuals.add(new Individual("John", 23, new Person("Jill", 20)));
        individuals.add(new Individual("Jack", 25, new Person("Hilly", 21)));
        individuals.add(new Individual("James", 26, new Person("Hally", 22)));
        individuals.add(new Individual("Baptist", 27, new Person("Newly", 23)));

        // Akıllı işaretçiler için veri kaynağı olarak bireylerin listesini atayın.
        designer.setDataSource("Individual", individuals);

        // Akıllı işaretçilerle ayarlanan veri kaynağını kullanarak çalışma kitabını işleyin.
        designer.process();

        // İşlenen çalışma kitabını bir dosyaya kaydedin.
        String outDir = "YOUR_OUTPUT_DIRECTORY";
        workbook.save(outDir + "/PopulatedUsingNestedObjects.xlsx");
    }
}
```

## Çözüm

Bu kılavuzu takip ederek, Aspose.Cells for Java kullanarak Excel çalışma kitaplarını iç içe geçmiş verilerle nasıl verimli bir şekilde yöneteceğinizi ve dolduracağınızı öğrendiniz. Bu yaklaşım yalnızca karmaşık veri kümelerinin işlenmesini basitleştirmekle kalmaz, aynı zamanda veri yönetimi süreçlerinizin esnekliğini de artırır.

Daha fazla keşif için Aspose.Cells'in daha gelişmiş özelliklerini incelemeyi veya farklı veri yapıları türlerini denemeyi düşünebilirsiniz.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}