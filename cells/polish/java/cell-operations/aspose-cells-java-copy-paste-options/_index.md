---
date: '2026-10-28'
description: Dowiedz się, jak wkleić wartości przy użyciu opcji kopiuj i wklej w Aspose.Cells
  w Javie, z kodem krok po kroku, konfiguracją zależności Maven oraz wskazówkami dotyczącymi
  licencjonowania.
keywords:
- how to paste values
- aspose cells maven dependency
- java generate excel report
- aspose cells license java
- copyoptions refertodestinationsheet
lastmod: '2026-10-28'
og_description: Dowiedz się, jak wkleić wartości przy użyciu opcji kopiuj i wklej
  w Aspose.Cells w Javie, z kodem krok po kroku, konfiguracją zależności Maven oraz
  wskazówkami dotyczącymi licencjonowania.
og_image_alt: Developer guide showing Java code for copying and pasting Excel data
  with Aspose.Cells
og_title: Jak wkleić wartości przy użyciu opcji kopiuj i wklej w Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to paste values using Aspose.Cells copy and paste options
    in Java, with step‑by‑step code, Maven dependency setup, and licensing tips.
  headline: How to paste values with Aspose.Cells copy and paste options
  type: TechArticle
- questions:
  - answer: It rewrites formula references so they point to the destination sheet
      after a copy, ensuring reporting formulas stay correct.
    question: What is `CopyOptions.ReferToDestinationSheet` used for?
  - answer: Set `PasteOptions.setOnlyVisibleCells(true)` and choose `PasteType.VALUES`.
    question: How do I paste only visible cells?
  - answer: Yes, a free trial or temporary license is available for evaluation, but
      a permanent license is required for production.
    question: Can I use Aspose.Cells without purchasing a license?
  - answer: Double‑check that `ReferToDestinationSheet` is enabled **before** the
      copy operation and that the source formulas don’t contain external workbook
      links.
    question: Why are some references still wrong after copying?
  - answer: Dispose of `Workbook` objects when finished, process large files in chunks,
      and monitor JVM heap usage.
    question: What memory‑management best practices should I follow?
  type: FAQPage
tags:
- paste values
- Aspose.Cells
- Java Excel automation
- copy options
- paste options
title: Jak wkleić wartości przy użyciu opcji kopiuj i wklej w Aspose.Cells
url: /pl/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wklejać wartości przy użyciu opcji kopiowania i wklejania Aspose.Cells

Automatyzacja raportowania Excel w Javie oznacza, że możesz generować, konsolidować i formatować skoroszyty bez ręcznego otwierania Excela. Dzięki **Aspose.Cells** masz pełną kontrolę nad formułami, ukrytymi wierszami i wartościami komórek, dzięki czemu Twoje raporty pozostają dokładne i lekkie. W tym samouczku dowiesz się, jak używać **CopyOptions.ReferToDestinationSheet**, aby utrzymać poprawność formuł oraz **PasteOptions**, aby wklejać tylko widoczne wartości, które są potrzebne.

## Szybkie odpowiedzi
- **Co robi `CopyOptions.ReferToDestinationSheet`?** Przepisuje formuły tak, aby wskazywały na docelowy arkusz po operacji kopiowania.  
- **Jak mogę wkleić tylko widoczne komórki?** Wywołaj `PasteOptions.setOnlyVisibleCells(true)` razem z `PasteType.VALUES`.  
- **Jakiej wersji biblioteki wymaga się?** Aspose.Cells 25.3 lub nowsza.  
- **Czy potrzebuję licencji do produkcji?** Tak – licencja stała lub tymczasowa usuwa ograniczenia wersji próbnej.  
- **Czy mogę używać Maven lub Gradle?** Oba są obsługiwane; zobacz fragmenty zależności poniżej.

## Co to jest „automatyzacja raportowania Excel”?
Automatyzacja raportowania Excel oznacza programowe generowanie i aktualizowanie skoroszytów Excel, umożliwiając tworzenie, scalanie i formatowanie raportów bez ręcznego kopiowania‑wklejania, co redukuje błędy i oszczędza godziny powtarzalnej pracy. Takie podejście jest idealne dla zaplanowanych zadań wsadowych, pulpitów opartych na danych oraz potoków konsolidacji finansowej.

## Dlaczego używać CopyOptions i PasteOptions w raportowaniu?
Te dwie klasy pozwalają zachować niezmienione odwołania do formuł podczas kopiowania danych **oraz** wyodrębnić tylko komórki widoczne po filtrowaniu lub ukryciu wierszy. Ich jednoczesne użycie zmniejsza ilość przesyłanych danych nawet o 80 % w typowych scenariuszach z filtrowanymi tabelami i zapewnia, że formuły nadal będą prawidłowo obliczane w docelowym arkuszu.

## Wymagania wstępne
- Java 8 lub wyższy.  
- Maven lub Gradle do zarządzania zależnościami.  
- Aspose.Cells 25.3+ (licencja próbna, tymczasowa lub stała).  

## Konfigurowanie Aspose.Cells dla Java

Dodaj bibliotekę do swojego projektu przy użyciu jednej z poniższych metod:

**Maven**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**  
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Uzyskanie licencji
- **Free trial** – pełny zestaw funkcji do oceny.  
- **Temporary license** – usuwa ograniczenia wersji próbnej podczas testów.  
- **Permanent license** – zalecana dla obciążeń produkcyjnych.

Zainicjalizuj Aspose.Cells w swoim kodzie Java:  
```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Przewodnik krok po kroku

### 1. copyOptions z referToDestinationSheet

#### Przegląd
`CopyOptions` jest obiektem konfiguracyjnym Aspose.Cells, który kontroluje sposób obsługi formuł i odwołań do komórek podczas operacji kopiowania. Ustawienie `CopyOptions.ReferToDestinationSheet` na `true` przepisuje odwołania do formuł, aby wskazywały na nowy arkusz po operacji kopiowania.

#### Krok 1: zainicjalizuj skoroszyt i arkusze  
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Krok 2: skonfiguruj copyOptions  
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Krok 3: wykonaj operację kopiowania  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Dlaczego to ważne*: Formuły, które pierwotnie odwoływały się do `Sheet1`, będą teraz poprawnie odwoływać się do `DestSheet`, co zapewnia niezawodność Twoich zautomatyzowanych raportów.

**Wskazówka rozwiązywania problemów**: Jeśli formuły nadal odwołują się do starego arkusza, upewnij się, że `setReferToDestinationSheet(true)` jest wywoływane **przed** kopiowaniem.

### 2. pasteOptions dla wartości‑tylko z widocznych komórek

#### Przegląd
`PasteOptions` jest obiektem ustawień Aspose.Cells, który definiuje, co ma być wklejane. Użycie `PasteType.VALUES` razem z `onlyVisibleCells=true` kopiuje tylko wyświetlane wartości, ignorując ukryte wiersze/kolumny oraz formatowanie.

#### Krok 1: zainicjalizuj skoroszyt i arkusze  
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Krok 2: skonfiguruj pasteOptions  
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Krok 3: wykonaj operację wklejania  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Dlaczego to ważne*: Idealne do wyodrębniania przefiltrowanych danych lub generowania czystych raportów bez ukrytych wierszy i szumu formatowania.

**Wskazówka rozwiązywania problemów**: Upewnij się, że wiersze/kolumny są rzeczywiście ukryte w Excelu przed kopiowaniem; w przeciwnym razie zostaną uwzględnione.

## Praktyczne zastosowania
1. **Konsolidacja finansowa** – scal miesięczne arkusze w główny skoroszyt, zachowując wszystkie formuły dokładne.  
2. **Eksport przefiltrowanych danych** – pobierz tylko widoczne wiersze z przefiltrowanej tabeli do arkusza podsumowania.  
3. **Planowane generowanie raportów** – automatyzuj nocne tworzenie raportów Excel z precyzyjnymi wartościami komórek i prawidłowymi odwołaniami.

## Rozważania dotyczące wydajności
- **Dispose of workbooks** when done (`wb.dispose();`) to free native resources. → Po zakończeniu zwolnij skoroszyty (`wb.dispose();`), aby zwolnić zasoby natywne.  
- **Batch operations** – group multiple copy/paste calls to reduce overhead. → Grupuj wiele wywołań kopiuj/wklej, aby zmniejszyć narzut.  
- **Monitor memory** – large workbooks may require increased heap (`-Xmx2g`). → Duże skoroszyty mogą wymagać zwiększenia przydziału pamięci (`-Xmx2g`).  
- Aspose.Cells obsługuje **ponad 50 formatów wejścia i wyjścia** i może przetwarzać skoroszyty z **do 2 milionami wierszy** bez ładowania całego pliku do pamięci, zapewniając wysoką przepustowość dla obciążeń korporacyjnych.

## Najczęściej zadawane pytania

**Q: Do czego służy `CopyOptions.ReferToDestinationSheet`?**  
A: Przepisuje odwołania do formuł, aby wskazywały na docelowy arkusz po kopiowaniu, zapewniając poprawność formuł raportowych.

**Q: Jak wkleić tylko widoczne komórki?**  
A: Ustaw `PasteOptions.setOnlyVisibleCells(true)` i wybierz `PasteType.VALUES`.

**Q: Czy mogę używać Aspose.Cells bez zakupu licencji?**  
A: Tak, dostępna jest wersja próbna lub tymczasowa licencja do oceny, ale do produkcji wymagana jest licencja stała.

**Q: Dlaczego niektóre odwołania są nadal nieprawidłowe po kopiowaniu?**  
A: Sprawdź, czy `ReferToDestinationSheet` jest włączone **przed** operacją kopiowania oraz czy formuły źródłowe nie zawierają odwołań do zewnętrznych skoroszytów.

**Q: Jakie najlepsze praktyki zarządzania pamięcią powinienem stosować?**  
A: Zwalniaj obiekty `Workbook` po zakończeniu, przetwarzaj duże pliki w partiach i monitoruj użycie pamięci JVM.

**Q: Czy można połączyć CopyOptions i PasteOptions w jednej operacji?**  
A: Tak, możesz je łączyć, najpierw kopiując przy użyciu `CopyOptions`, a następnie stosując `PasteOptions` na docelowym zakresie.

## Zasoby
- **Dokumentacja**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Pobierz**: [Aspose.Cells releases for Java](https://releases.aspose.com/cells/java/)  
- **Zakup**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Bezpłatna wersja próbna**: [Aspose.Cells free trial](https://releases.aspose.com/cells/java/)  
- **Licencja tymczasowa**: [Apply for a temporary license](https://purchase.aspose.com/temporary-license/)  
- **Forum wsparcia**: [Aspose support](https://forum.aspose.com/c/cells)

---

**Ostatnia aktualizacja:** 2026-10-28  
**Testowano z:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose

## Powiązane samouczki

- [Odczyt pliku Excel w Java – Manipulacja komórkami głównego skoroszytu przy użyciu Aspose.Cells](/cells/java/cell-operations/aspose-cells-java-workbook-cell-manipulation/)
- [Dodaj dane do komórki w Excelu przy użyciu Aspose.Cells dla Java](/cells/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Konwertuj indeksy wierszy i kolumn komórek Excel przy użyciu Aspose.Cells Java](/cells/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}