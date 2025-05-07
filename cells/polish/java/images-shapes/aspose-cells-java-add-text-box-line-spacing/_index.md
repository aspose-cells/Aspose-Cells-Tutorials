---
"date": "2025-04-08"
"description": "Dowiedz się, jak używać Aspose.Cells for Java do dodawania pól tekstowych i ustawiania odstępów między wierszami w skoroszytach programu Excel. Ulepsz swoje prezentacje skoroszytów za pomocą stylizowanych kształtów tekstowych."
"title": "Dodaj pole tekstowe i ustaw odstępy między wierszami w programie Excel za pomocą Aspose.Cells dla języka Java"
"url": "/pl/java/images-shapes/aspose-cells-java-add-text-box-line-spacing/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# Dodaj pole tekstowe i ustaw odstępy między wierszami w programie Excel za pomocą Aspose.Cells dla języka Java

## Wstęp

Tworzenie dynamicznych raportów Excela często wymaga niestandardowego formatowania tekstu, takiego jak dodawanie pól tekstowych z określonym odstępem między wierszami. Dzięki Aspose.Cells for Java staje się to proste i wydajne. Ten samouczek przeprowadzi Cię przez proces ulepszania prezentacji skoroszytu za pomocą Aspose.Cells for Java w celu dodawania stylizowanych kształtów tekstu.

Do końca tego przewodnika nauczysz się, jak:
- Utwórz nowy skoroszyt programu Excel i uzyskaj dostęp do jego arkuszy
- Dodaj kształt pola tekstowego do arkusza kalkulacyjnego
- Ustaw niestandardowy odstęp między wierszami wewnątrz kształtu tekstu
- Zapisz sformatowany skoroszyt w formacie XLSX

Zacznijmy od skonfigurowania środowiska.

### Wymagania wstępne

Zanim zaczniesz, upewnij się, że masz następujące rzeczy:
- Java Development Kit (JDK) zainstalowany na Twoim komputerze
- IDE lub edytor do pisania kodu Java
- System kompilacji Maven lub Gradle skonfigurowany do zarządzania zależnościami

Przydatna będzie podstawowa znajomość programowania w Javie i struktur plików programu Excel.

## Konfigurowanie Aspose.Cells dla Java

Dodaj Aspose.Cells do zarządzania zależnościami swojego projektu za pomocą Maven lub Gradle:

**Maven**

Dodaj następujący blok zależności do swojego `pom.xml` plik:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**

Uwzględnij to w swoim `build.gradle` plik:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

Następnie możesz nabyć licencję na Aspose.Cells, wybierając bezpłatny okres próbny, prosząc o licencję tymczasową lub kupując pełną licencję.

### Inicjalizacja Aspose.Cells

Po uwzględnieniu biblioteki w projekcie zainicjuj ją w aplikacji Java:

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) {
        // Zainicjuj wystąpienie skoroszytu (reprezentuje plik Excela)
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## Przewodnik wdrażania

### Utwórz skoroszyt i uzyskaj dostęp do arkusza kalkulacyjnego

Zacznij od utworzenia nowego skoroszytu programu Excel i uzyskania dostępu do jego pierwszego arkusza. Tutaj dodasz pole tekstowe.

#### Przegląd

Utworzenie nowego skoroszytu powoduje utworzenie pustej powierzchni, na której można dodawać dane, kształty i formatowanie według potrzeb.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

public class ExcelDemo {
    public static void main(String[] args) {
        // Utwórz nowy skoroszyt (plik Excel)
        Workbook workbook = new Workbook();
        
        // Uzyskaj dostęp do pierwszego arkusza kalkulacyjnego
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        System.out.println("Workbook and first worksheet accessed.");
    }
}
```

### Dodaj pole tekstowe do arkusza kalkulacyjnego

Następnie dodaj kształt pola tekstowego do wybranego arkusza kalkulacyjnego. Ten kształt może zawierać dowolną potrzebną treść tekstową.

#### Przegląd

Pola tekstowe to wszechstronne narzędzia umożliwiające dodawanie niestandardowych tekstów, takich jak notatki lub instrukcje, bezpośrednio w arkuszu Excela.

```java
import com.aspose.cells.Shape;
import com.aspose.cells.MsoDrawingType;

public class ExcelDemo {
    public static void main(String[] args) {
        // Utwórz nowy skoroszyt (plik Excel)
        Workbook workbook = new Workbook();
        
        // Uzyskaj dostęp do pierwszego arkusza kalkulacyjnego
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Dodaj kształt pola tekstowego do arkusza kalkulacyjnego
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        System.out.println("Text box added.");
    }
}
```

### Ustaw tekst w kształcie

Gdy pole tekstowe będzie gotowe, ustaw jego zawartość i sformatuj tekst w nim zawarty.

```java
import com.aspose.cells.Shape;

public class ExcelDemo {
    public static void main(String[] args) {
        // Utwórz nowy skoroszyt (plik Excel)
        Workbook workbook = new Workbook();
        
        // Uzyskaj dostęp do pierwszego arkusza kalkulacyjnego
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Dodaj kształt pola tekstowego do arkusza kalkulacyjnego
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Ustaw zawartość tekstową wewnątrz kształtu
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        System.out.println("Text set in shape.");
    }
}
```

### Dostęp do akapitów tekstowych w Shape

Można uzyskać dostęp do pojedynczych akapitów w polu tekstowym, aby zastosować określone formatowanie.

```java
import com.aspose.cells.TextParagraph;

public class ExcelDemo {
    public static void main(String[] args) {
        // Utwórz nowy skoroszyt (plik Excel)
        Workbook workbook = new Workbook();
        
        // Uzyskaj dostęp do pierwszego arkusza kalkulacyjnego
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Dodaj kształt pola tekstowego do arkusza kalkulacyjnego
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Ustaw zawartość tekstową wewnątrz kształtu
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Uzyskaj dostęp do drugiego akapitu w kształcie
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);
        
        System.out.println("Accessed second paragraph in text box.");
    }
}
```

### Ustaw odstęp między wierszami akapitu

Dostosowanie odstępu między wierszami może poprawić czytelność. Oto jak to ustawić:

```java
import com.aspose.cells.LineSpaceSizeType;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Utwórz nowy skoroszyt (plik Excel)
        Workbook workbook = new Workbook();
        
        // Uzyskaj dostęp do pierwszego arkusza kalkulacyjnego
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Dodaj kształt pola tekstowego do arkusza kalkulacyjnego
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Ustaw zawartość tekstową wewnątrz kształtu
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Uzyskaj dostęp do drugiego akapitu w kształcie
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Ustaw odstęp między wierszami na 20 punktów
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // Skonfiguruj odstęp przed i po akapicie
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        System.out.println("Line spacing set.");
    }
}
```

### Zapisz skoroszyt

Na koniec zapisz skoroszyt z nowo dodanym i sformatowanym polem tekstowym.

```java
import com.aspose.cells.SaveFormat;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Utwórz nowy skoroszyt (plik Excel)
        Workbook workbook = new Workbook();
        
        // Uzyskaj dostęp do pierwszego arkusza kalkulacyjnego
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Dodaj kształt pola tekstowego do arkusza kalkulacyjnego
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Ustaw zawartość tekstową wewnątrz kształtu
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Uzyskaj dostęp do drugiego akapitu w kształcie
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Ustaw odstęp między wierszami na 20 punktów
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // Skonfiguruj odstęp przed i po akapicie
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        // Zapisz skoroszyt
        workbook.save("StyledTextShape.xlsx", SaveFormat.XLSX);
    }
}
```

## Wniosek

Udało Ci się nauczyć, jak dodać pole tekstowe i ustawić odstępy między wierszami w skoroszycie programu Excel przy użyciu Aspose.Cells for Java. Dzięki temu możesz tworzyć dynamiczne, atrakcyjne wizualnie raporty.

## Rekomendacje słów kluczowych
- „Aspose.Cells dla Javy”
- „Dodaj pole tekstowe w programie Excel”
- „Ustaw odstępy między wierszami w programie Excel”
- „Skoroszyt programu Excel ze stylizowanym tekstem”
- „Java i Aspose.Cells”


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}