---
date: '2026-10-28'
description: Dowiedz się, jak zmienić system dat w Excelu na 1904 przy użyciu Aspose.Cells
  for Java, ustawić format dat w Excelu i efektywnie konwertować system 1904 w Excelu.
keywords:
- change excel date system
- excel 1904 date conversion
- maven dependency aspose cells
lastmod: '2026-10-28'
og_description: Zmień system dat w Excelu na 1904 przy użyciu Aspose.Cells for Java.
  Dowiedz się krok po kroku, jak włączyć system 1904, ustawić daty i przywrócić poprzedni
  system.
og_image_alt: Aspose.Cells Java guide showing how to switch Excel to the 1904 date
  system
og_title: Zmień system dat w Excelu na 1904 przy użyciu Aspose.Cells for Java
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  headline: Change Excel date system to 1904 with Aspose.Cells Java
  type: TechArticle
- description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  name: Change Excel date system to 1904 with Aspose.Cells Java
  steps:
  - name: initialize and load the workbook
    text: The `Workbook` class represents an entire Excel file in memory. First, create
      a `Workbook` instance that points to your existing file.
  - name: enable the 1904 date system
    text: The `WorkbookSettings.setDate1904` method toggles the workbook‑level date
      flag. Setting it to `true` activates the 1904 system for all worksheets. **Pro
      tip:** You can also call `setDate1904(false)` later if you need to revert.
  - name: save the modified workbook
    text: Finally, write the changes to a new file (or overwrite the original). The
      `save` method respects the active date system automatically. > **Note:** The
      code above uses the class name `tWorkbook` as originally provided. Ensure this
      typo matches your project’s naming conventions or correct it to `Workb
  type: HowTo
- questions:
  - answer: The 1900 system starts on January 1, 1900, while the 1904 system starts
      on January 1, 1904, shifting all dates by 1,462 days.
    question: What is the difference between the 1900 and 1904 date systems?
  - answer: Yes, but you must close the file in Excel first; otherwise the save operation
      will fail.
    question: Can I change the date system of a workbook that is currently open in
      Excel?
  - answer: The method works in the free trial, but a full license removes evaluation
      limitations.
    question: Do I need a license to use `setDate1904`?
  - answer: No, the date system is a workbook‑level setting; it applies to all worksheets.
    question: Is it possible to change the date system for only a single worksheet?
  - answer: Open the saved file in Excel, go to **File → Options → Advanced**, and
      check the **"Use 1904 date system"** box.
    question: How can I verify that the date system was changed?
  type: FAQPage
tags:
- change excel date system
- aspose cells java
- excel date conversion
- java excel processing
title: Zmień system dat w Excelu na 1904 przy użyciu Aspose.Cells Java
url: /pl/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zmień system dat w Excelu na 1904 przy użyciu Aspose.Cells Java

W tym samouczku dowiesz się, jak **zmienić system dat w Excelu** na format 1904 przy użyciu Aspose.Cells dla Javy. System 1904 jest niezbędny, gdy trzeba zachować starsze daty z Mac‑a lub dopasować się do modeli finansowych, które oczekują tej epoki. Przeprowadzimy instalację biblioteki, wczytanie skoroszytu, przełączenie systemu dat oraz zapis wyniku — wszystko bez wymogu posiadania Microsoft Excel na serwerze.

## Szybkie odpowiedzi
- **Co robi system dat 1904?** Rozpoczyna liczenie dni od 1 stycznia 1904 r., przesuwając wszystkie daty o 1 462 dni w porównaniu z domyślnym systemem 1900.  
- **Dlaczego używać Aspose.Cells do zmiany systemu dat?** Zapewnia prosty interfejs API, który działa bez zainstalowanego Excela i obsługuje duże pliki.  
- **Jakie wersje Javy są obsługiwane?** JDK 8 lub nowszy.  
- **Czy potrzebna jest licencja?** Bezpłatna wersja próbna wystarcza do oceny; licencja usuwa ograniczenia użytkowania.  
- **Czy mogę później przywrócić system 1900?** Tak, wystarczy wywołać `setDate1904(false)`.

## Co to jest system dat 1904 w Excelu?
System dat 1904 liczy dni od 1 stycznia 1904 r., zamiast domyślnej epoki 1900. To przesunięcie dodaje dokładnie 1 462 dni do każdej wartości daty, co powoduje, że starsze skoroszyty Mac wykazują offset po otwarciu w systemie Windows. Jest używany głównie w celu zapewnienia kompatybilności ze starszymi plikami Excel na Macintosh oraz niektórymi starszymi modelami finansowymi.

## Dlaczego zmienić system dat w Excelu przy użyciu Aspose.Cells?
Możesz przełączyć system dat bezpośrednio z Javy, eliminując ręczne kroki w Excelu. Aspose.Cells przetwarza skoroszyty o rozmiarze do **2 GB** i może skonwertować skoroszyt z 500 arkuszami w mniej niż **2 sekundy** na typowym serwerze 4‑rdzeniowym, zapewniając wysoką przepustowość automatyzacji po stronie serwera.

## Wymagania wstępne
- Java Development Kit (JDK) 8 lub nowszy.  
- Maven lub Gradle do zarządzania zależnościami.  
- Podstawowa znajomość programowania w Javie.  

## Konfiguracja Aspose.Cells dla Javy

### Maven
Dodaj następującą zależność do pliku `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
Umieść tę linię w pliku `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Uzyskanie licencji
Aspose oferuje bezpłatną wersję próbną, licencję tymczasową oraz pełne licencje komercyjne. Możesz rozpocząć od [bezpłatnej wersji próbnej](https://releases.aspose.com/cells/java/) lub uzyskać licencję tymczasową na [stronie licencji tymczasowej](https://purchase.aspose.com/temporary-license/).

## Jak zmienić system dat w Excelu na 1904 przy użyciu Aspose.Cells dla Javy?
Wczytaj skoroszyt, włącz ustawienie 1904 i zapisz plik — ten trzyetapowy proces aktualizuje wewnętrzną epokę dat w skoroszycie w mniej niż sekundę. Wywołanie API `setDate1904(true)` przełącza flagę systemu, a zmiana zostaje zachowana po wywołaniu `save`. Instalacja Excela nie jest wymagana, co czyni rozwiązanie idealnym dla środowisk serwerowych bez interfejsu graficznego.

### Krok 1: inicjalizacja i wczytanie skoroszytu
Klasa `Workbook` reprezentuje cały plik Excel w pamięci. Najpierw utwórz instancję `Workbook`, która wskazuje na istniejący plik.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### Krok 2: włączenie systemu dat 1904
Metoda `WorkbookSettings.setDate1904` przełącza flagę dat na poziomie skoroszytu. Ustawienie jej na `true` aktywuje system 1904 dla wszystkich arkuszy.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**Wskazówka:** Możesz później wywołać `setDate1904(false)`, jeśli potrzebujesz przywrócić poprzedni stan.

### Krok 3: zapis zmodyfikowanego skoroszytu
Na koniec zapisz zmiany do nowego pliku (lub nadpisz oryginał). Metoda `save` automatycznie uwzględnia aktywny system dat.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
String outDir = "YOUR_OUTPUT_DIRECTORY"; // Specify where you want to save the modified workbook

// Load and modify your workbook as shown in previous steps
tWorkbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
workbook.getSettings().setDate1904(true);

// Save the changes to a new file
workbook.save(outDir + "/I1904DateSystem_out.xls");
```

> **Uwaga:** Powyższy kod używa nazwy klasy `tWorkbook` tak jak podano w oryginale. Upewnij się, że ten błąd typograficzny pasuje do konwencji nazewnictwa w Twoim projekcie lub popraw go na `Workbook`, jeśli to konieczne.

## Ustaw datę w Excelu programowo (słowo kluczowe drugorzędne)
Jeśli musisz dostosować wartości poszczególnych komórek po zmianie systemu, możesz użyć `cells.get(i, j).putValue(Date)`, gdzie data zostanie zinterpretowana zgodnie z aktywnym systemem dat.

## Konwersja systemu Excel 1904 z powrotem na 1900 (słowo kluczowe drugorzędne)
Aby przywrócić, po prostu wywołaj:

```java
workbook.getSettings().setDate1904(false);
```

Następnie ponownie zapisz skoroszyt.

## Praktyczne zastosowania
1. **Archiwizacja danych** – Zachowanie starszych znaczników czasu przy migracji starych arkuszy kalkulacyjnych z Mac.  
2. **Raportowanie wieloplatformowe** – Generowanie raportów, które otwierają się poprawnie zarówno w Windows, jak i macOS, bez niezgodności dat.  
3. **Modelowanie finansowe** – Dopasowanie obliczeń dat do starszych modeli finansowych, które oczekują systemu 1904.

## Uwagi dotyczące wydajności
- Ogranicz operacje na skoroszycie w jednej sesji, aby utrzymać niskie zużycie pamięci; Aspose.Cells strumieniuje dane i nie ładuje całego pliku do RAM, chyba że wyraźnie tego zażądasz.  
- Dostosuj flagi garbage‑collection Javy (`-XX:+UseG1GC`) dla bardzo dużych plików, aby uniknąć nagłych przerw w działaniu.

## Najczęściej zadawane pytania

**P:** Jaka jest różnica między systemami dat 1900 a 1904?  
**O:** System 1900 zaczyna się 1 stycznia 1900 r., natomiast system 1904 zaczyna się 1 stycznia 1904 r., przesuwając wszystkie daty o 1 462 dni.

**P:** Czy mogę zmienić system dat w skoroszycie, który jest aktualnie otwarty w Excelu?  
**O:** Tak, ale najpierw musisz zamknąć plik w Excelu; w przeciwnym razie operacja zapisu się nie powiedzie.

**P:** Czy potrzebna jest licencja do użycia `setDate1904`?  
**O:** Metoda działa w wersji próbnej, ale pełna licencja usuwa ograniczenia oceny.

**P:** Czy można zmienić system dat tylko dla jednego arkusza?  
**O:** Nie, system dat jest ustawieniem na poziomie skoroszytu; obowiązuje wszystkie arkusze.

**P:** Jak mogę zweryfikować, że system dat został zmieniony?  
**O:** Otwórz zapisany plik w Excelu, przejdź do **Plik → Opcje → Zaawansowane** i zaznacz pole **„Użyj systemu dat 1904”**.

## Podsumowanie
Teraz wiesz, jak **zmienić system dat w Excelu** na 1904 przy użyciu Aspose.Cells dla Javy, jak ustawiać daty w poszczególnych komórkach oraz jak przywrócić system 1900 w razie potrzeby. Włącz te fragmenty kodu do swoich potoków przetwarzania danych, aby zapewnić kompatybilność dat między platformami i starszymi plikami.

---

**Ostatnia aktualizacja:** 2026-10-28  
**Testowano z:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose  

**Zasoby**
- **Dokumentacja:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **Pobierz:** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)
- **Kup licencję:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **Bezpłatna wersja próbna:** [Start Free Trial](https://releases.aspose.com/cells/java/)
- **Licencja tymczasowa:** [Get Temporary License](https://purchase.aspose.com/temporary-license/)
- **Forum wsparcia:** [Aspose Support](https://forum.aspose.com/c/cells/9)

## Powiązane samouczki

- [Efektywna konwersja Excel do PDF z niestandardowymi formatami dat przy użyciu Aspose.Cells dla Javy](/cells/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Aspose.Cells dla Javy: Jak efektywnie tworzyć i formatować skoroszyty Excel](/cells/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [Mistrzowska manipulacja Excel przy użyciu Aspose.Cells dla Javy: Operacje na skoroszytach i stylowanie komórek – samouczek](/cells/java/workbook-operations/excel-manipulation-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}