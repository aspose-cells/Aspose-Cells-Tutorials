---
date: '2026-03-15'
description: Dowiedz się, jak podzielić nazwy na osobne kolumny i zapisać skoroszyt
  xlsx przy użyciu Aspose Cells Java w samouczku krok po kroku.
keywords:
- Aspose.Cells Java
- split names columns
- Excel manipulation
- text to columns Java
- Java Excel processing
title: aspose cells java – Rozdziel nazwy na kolumny
url: /pl/java/cell-operations/aspose-cells-java-split-names-columns/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Opanowanie **aspose cells java**: Rozdzielanie nazw na kolumny

Witamy w naszym kompleksowym **aspose cells java** tutorialu. W tym przewodniku nauczysz się **jak rozdzielić nazwiska**, które są przechowywane w jednej kolumnie Excela, na dwie oddzielne kolumny — imię i nazwisko — przy użyciu potężnej funkcji tekst‑do‑kolumn. Niezależnie od tego, czy porządkujesz listę kontaktów, przygotowujesz dane do importu do CRM, czy po prostu potrzebujesz szybkiego sposobu na przekształcenie arkuszy, ten tutorial pokaże Ci dokładnie, jak **zapisz skoroszyt xlsx** po transformacji.

## Quick Answers
- **What does this tutorial cover?** Rozdzielanie pełnych nazwisk na kolumny imienia i nazwiska przy użyciu Aspose.Cells dla Javy.  
- **Which library version is used?** Najnowsze stabilne wydanie (stan na 2026).  
- **Do I need a license?** Darmowa wersja próbna wystarczy do rozwoju; licencja komercyjna jest wymagana w środowisku produkcyjnym.  
- **Can I split on other delimiters?** Tak — wystarczy zmienić separator w `TxtLoadOptions`.  
- **Is the output an .xlsx file?** Oczywiście, skoroszyt jest zapisywany w formacie XLSX.

## What is **aspose cells java**?
**Aspose.Cells java** to wysokowydajny interfejs API w języku Java, który umożliwia programistom tworzenie, modyfikowanie, konwertowanie i renderowanie plików Excel bez potrzeby posiadania Microsoft Office. Obsługuje wszystkie główne formaty Excel oraz oferuje zaawansowane funkcje, takie jak formuły, wykresy i manipulacja danymi.

## Why use **aspose cells java** for splitting names?
- **Zero‑install**: Działa w dowolnym środowisku serwerowym Java.  
- **Speed**: Przetwarza duże arkusze szybciej niż natywne interfejsy Excel.  
- **Precision**: Pełna kontrola nad separatorami, zakresami kolumn i formatami wyjściowymi.  
- **Reliability**: Brak zależności od COM czy Office, co czyni go idealnym do wdrożeń w chmurze lub kontenerach.

## Prerequisites
- Java Development Kit (JDK) 8 lub nowszy.  
- IDE, takie jak IntelliJ IDEA lub Eclipse (opcjonalnie, ale zalecane).  
- Maven lub Gradle do zarządzania zależnościami.  

### Maven Setup
Dodaj zależność Aspose.Cells do swojego `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle Setup
Dodaj bibliotekę do swojego `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

> **Pro tip:** Użyj tymczasowej licencji z portalu Aspose, aby odblokować pełną funkcjonalność podczas rozwoju.

## Step‑by‑Step Implementation

### Step 1: Create a Workbook and Access the First Worksheet
Najpierw zaimportuj klasy podstawowe i utwórz nowy skoroszyt. Dzięki temu otrzymasz czysty plik Excel gotowy do wstawiania danych.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
```

```java
String dataDir = "YOUR_DATA_DIRECTORY"; // Define your directory path here

Workbook wb = new Workbook();
Worksheet ws = wb.getWorksheets().get(0);
```

### Step 2: Populate the Worksheet with Sample Names
Następnie dodaj kilka pełnych nazwisk do kolumny **A**. W rzeczywistym projekcie odczytywałbyś je z bazy danych lub pliku CSV.

```java
import com.aspose.cells.Cell;

String outDir = "YOUR_OUTPUT_DIRECTORY"; // Define your output directory path here

ws.getCells().get("A1").putValue("John Teal");
ws.getCells().get("A2").putValue("Peter Graham");
ws.getCells().get("A3").putValue("Brady Cortez");
ws.getCells().get("A4").putValue("Mack Nick");
ws.getCells().get("A5").putValue("Hsu Lee");
```

### Step 3: Configure Text Load Options for Column Splitting
Klasa `TxtLoadOptions` informuje Aspose.Cells, jak interpretować tekst. Tutaj używamy spacji (`' '`) jako separatora.

```java
import com.aspose.cells.TxtLoadOptions;

TxtLoadOptions opts = new TxtLoadOptions();
opts.setSeparator(' ');
```

### Step 4: Split the Text into Two Columns
Teraz wywołaj `textToColumns()` na obszarze komórek zawierającym nazwiska. Parametry `(0, 0, 5, opts)` oznaczają *rozpocznij od wiersza 0, kolumny 0, przetwórz 5 wierszy, używając właśnie zdefiniowanych opcji*.

```java
ws.getCells().textToColumns(0, 0, 5, opts);
```

Po tym wywołaniu kolumna A zawiera imiona, a kolumna B nazwiska.

### Step 5: Save the Workbook as an XLSX File
Na koniec zapisz zmodyfikowany skoroszyt na dysku. Enum `SaveFormat` zapewnia, że plik zostanie zapisany w nowoczesnym formacie XLSX.

```java
import com.aspose.cells.SaveFormat;

wb.save(outDir + "outputTextToColumns.xlsx");
```

> **Why this matters:** Korzystając z **save workbook xlsx**, zapewniasz kompatybilność z najnowszymi wersjami Excel, Google Sheets i innymi narzędziami arkuszy kalkulacyjnych.

## Practical Applications
- **Data Cleaning:** Szybko oddziel pola połączone w jedną całość przed załadowaniem ich do potoków analitycznych.  
- **CRM Integration:** Przekształć płaską listę kontaktów w ustrukturyzowaną tabelę do importu.  
- **HR Systems:** Rozdziel pełne nazwiska pracowników dla potrzeb płac lub przetwarzania świadczeń.

## Performance Considerations
Podczas pracy z tysiącami wierszy:

1. **Batch Updates:** Używaj `ws.getCells().setRowHeight()` lub podobnych metod wsadowych, aby zmniejszyć narzut.  
2. **Memory Management:** Wywołuj `wb.calculateFormula()` tylko w razie potrzeby i niezwłocznie zwalniaj duże obiekty.  
3. **Garbage Collection:** Uruchom JVM z odpowiednimi ustawieniami pamięci (`-Xmx2g` dla dużych plików), aby uniknąć błędów OutOfMemory.

## Common Issues and Solutions
| Issue | Solution |
|-------|----------|
| **Names contain middle initials** (e.g., “John A. Doe”) | Dostosuj separator lub po‑przetwórz drugą kolumnę, aby wyodrębnić nazwisko. |
| **Unexpected empty cells** | Sprawdź, czy zakres źródłowy (`textToColumns` parameters) odpowiada rzeczywistym wierszom danych. |
| **License not found** | Umieść tymczasowy plik licencji (`Aspose.Cells.lic`) w katalogu głównym projektu lub ustaw licencję programowo. |

## Frequently Asked Questions

**Q: What is Aspose.Cells Java?**  
A: Potężna biblioteka umożliwiająca programistyczne tworzenie, modyfikowanie i konwertowanie plików Excel przy użyciu Javy.

**Q: Can I split columns based on delimiters other than spaces?**  
A: Tak, dostosuj separator w `TxtLoadOptions` zgodnie z potrzebami danych.

**Q: How do I handle large datasets with Aspose.Cells?**  
A: Optymalizuj wydajność, zarządzając pamięcią i minimalizując operacje na skoroszycie, jak opisano powyżej.

**Q: Is there support available if I encounter issues?**  
A: Odwiedź [Aspose Forum](https://forum.aspose.com/c/cells/9) po pomoc społeczności lub skontaktuj się bezpośrednio z zespołem wsparcia Aspose.

**Q: What formats can Aspose.Cells save workbooks in?**  
A: Obsługuje szeroką gamę formatów plików Excel, w tym XLSX, XLS, CSV i wiele innych.

## Resources

- **Documentation**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **Download**: [Aspose.Cells Java Releases](https://releases.aspose.com/cells/java/)
- **Purchase**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **Free Trial**: [Try Aspose.Cells for Free](https://releases.aspose.com/cells/java/)
- **Temporary License**: [Request a Temporary License](https://purchase.aspose.com/temporary-license/)

Miłego kodowania i czerpania pełnej mocy **aspose cells java** w swoich projektach!

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Last Updated:** 2026-03-15  
**Tested With:** Aspose.Cells 25.3 for Java  
**Author:** Aspose