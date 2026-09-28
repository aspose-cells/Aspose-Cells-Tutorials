---
category: general
date: 2026-09-27
description: Utwórz zakres nazwany w Excelu przy użyciu Aspose.Cells, ustaw nazwę
  tabeli, dodaj zakres nazwany, utwórz tabelę w Excelu i wykryj błędy duplikatów nazw.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create named range
- set table name
- create excel table
- add named range
- detect duplicate name
language: pl
lastmod: 2026-09-27
og_description: Utwórz nazwany zakres w Excelu przy użyciu Aspose.Cells, następnie
  ustaw nazwę tabeli, dodaj nazwany zakres, utwórz tabelę w Excelu i wykryj błędy
  duplikatów nazw.
og_image_alt: Screenshot showing how to create a named range in Excel with Aspose.Cells
og_title: Utwórz nazwany zakres i wykryj duplikat nazwy w Excelu
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Create a named range in Excel using Aspose.Cells, set table name, add
    named range, create Excel table, and detect duplicate name errors.
  headline: Create a named range and detect duplicate name in Excel
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Utwórz nazwany zakres i wykryj duplikat nazwy w Excelu
url: /pl/java/range-management/create-a-named-range-and-detect-duplicate-name-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz zakres nazwany i wykryj duplikat nazwy w Excelu

Jeśli potrzebujesz **create a named range** w skoroszycie Excel i chcesz uniknąć kolizji nazw, ten przewodnik pokazuje dokładnie, jak to zrobić przy użyciu Aspose.Cells for Java. Nauczysz się **add named range**, **create Excel table**, **set table name** oraz **detect duplicate name** błędów w jednym, samodzielnym przykładzie.

Praca z zakresami nazwanymi jest powszechnym wymaganiem przy tworzeniu narzędzi raportowych, arkuszy walidacji danych lub dynamicznych pulpitów nawigacyjnych. Po zakończeniu tego samouczka będziesz mieć działający program, który bezpiecznie tworzy zakres nazwany, buduje tabelę i elegancko obsługuje wszelkie wyjątki konfliktu nazw.

## Wymagania wstępne

- Java 17 lub nowszy zainstalowany
- Maven lub Gradle do zarządzania zależnościami
- Aspose.Cells for Java (najnowsza wersja; współrzędna Maven `com.aspose:aspose-cells:23.9` w momencie pisania)
- Podstawowa znajomość koncepcji Excela, takich jak arkusze, zakresy i tabele

## Krok 1: Utwórz zakres nazwany w skoroszycie

Pierwszym krokiem jest utworzenie obiektu `Workbook` i dodanie zakresu nazwanego, który wskazuje na określony blok komórek.

```java
import com.aspose.cells.*;

public class NamedRangeDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the default first worksheet (named "Sheet1")
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Define a named range called "MyRange" that covers A1:C5
        // This demonstrates the "add named range" operation.
        workbook.getNames().add("MyRange", "'Sheet1'!$A$1:$C$5");
```

**Dlaczego to jest ważne:**  
Zakres nazwany działa jako wielokrotnego użytku odwołanie, do którego mogą odwoływać się formuły i tabele. Dodanie go na wczesnym etapie zapewnia, że kolejne kroki mogą ponownie używać tego samego identyfikatora bez twardego kodowania adresów komórek.

## Krok 2: Utwórz tabelę Excel, która używa zakresu nazwanego

Następnie tworzymy strukturalną tabelę (ListObject), która zajmuje ten sam obszar co zakres nazwany. To ilustruje koncepcję **create excel table**.

```java
        // Create an Excel table (ListObject) that spans the same area as the named range.
        // The parameters (0,0,4,2) represent the top‑left cell (A1) and bottom‑right cell (C5).
        ListObject table = sheet.getListObjects().add(0, 0, 4, 2, true);
```

**Dlaczego to jest ważne:**  
Tabele zapewniają wbudowane sortowanie, filtrowanie i stylizację. Dopasowując tabelę do zakresu nazwanego, utrzymujesz spójny model danych.

## Krok 3: Ustaw nazwę tabeli i obsłuż możliwy konflikt

Teraz próbujemy nadać tabeli nazwę, która pasuje do wcześniej utworzonego zakresu nazwanego. Ten krok demonstruje **set table name** i celowo wywołuje konflikt nazw.

```java
        try {
            // Attempt to set the table name to "MyRange".
            // Because a named range with the same identifier already exists,
            // Aspose.Cells will throw an exception.
            table.setName("MyRange"); // <-- conflict expected
        } catch (Exception e) {
            // Step 4: Detect duplicate name and respond appropriately
            System.out.println("Name conflict detected: " + e.getMessage());
        }
```

**Dlaczego to jest ważne:**  
Excel nie pozwala, aby tabela i zakres nazwany współdzieliły ten sam identyfikator. Wczesne wykrycie konfliktu zapobiega uszkodzeniu skoroszytów i ułatwia debugowanie.

## Krok 4: Wykryj duplikat nazwy i rozwiąż go

Gdy wyjątek zostanie przechwycony, możesz albo zmienić nazwę tabeli, albo usunąć kolidujący zakres nazwany. Poniżej znajduje się prosta strategia rozwiązania, która zmienia nazwę tabeli, dodając przyrostek.

```java
            // Resolve the conflict by appending a numeric suffix
            String baseName = "MyRange";
            int suffix = 1;
            String newName;
            do {
                newName = baseName + "_" + suffix;
                suffix++;
            } while (workbook.getNames().get(newName) != null);

            table.setName(newName);
            System.out.println("Table renamed to: " + newName);
        }

        // Save the workbook to verify the result
        workbook.save("NamedRangeDemo.xlsx");
    }
}
```

**Kluczowe punkty rozwiązania:**

- **detect duplicate name** – blok `catch` potwierdza konflikt.
- Pętla sprawdza kolekcję nazw skoroszytu, aby zapewnić, że nowy identyfikator jest unikalny.
- Na koniec skoroszyt jest zapisywany, abyś mógł otworzyć go w Excelu i zweryfikować, że tabela ma odrębną nazwę, podczas gdy oryginalny zakres nazwany pozostaje nienaruszony.

## Pełny, działający przykład

Łącząc wszystkie elementy razem, pełny program wygląda następująco:

```java
import com.aspose.cells.*;

public class NamedRangeDemo {
    public static void main(String[] args) throws Exception {
        // Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Add a named range called "MyRange" covering A1:C5
        workbook.getNames().add("MyRange", "'Sheet1'!$A$1:$C$5");

        // Create an Excel table that occupies the same cells
        ListObject table = sheet.getListObjects().add(0, 0, 4, 2, true);

        try {
            // Try to set the table name to the same identifier
            table.setName("MyRange");
        } catch (Exception e) {
            // Detect duplicate name and resolve it
            System.out.println("Name conflict detected: " + e.getMessage());

            String baseName = "MyRange";
            int suffix = 1;
            String newName;
            do {
                newName = baseName + "_" + suffix;
                suffix++;
            } while (workbook.getNames().get(newName) != null);

            table.setName(newName);
            System.out.println("Table renamed to: " + newName);
        }

        // Save the file for inspection
        workbook.save("NamedRangeDemo.xlsx");
    }
}
```

**Oczekiwany wynik po uruchomieniu programu:** 

```
Name conflict detected: A name with the specified identifier already exists.
Table renamed to: MyRange_1
```

Otwierając `NamedRangeDemo.xlsx` w Excelu zobaczysz:

- Zakres nazwany **MyRange**, który odwołuje się do komórek A1:C5.
- Tabela o nazwie **MyRange_1**, obejmująca te same komórki.
- Brak błędu nazewnictwa przy próbie dodania formuł odwołujących się do `MyRange`.

## Częste pułapki i najlepsze praktyki

- **Do not reuse identifiers**: Zawsze sprawdzaj, czy nazwa nie istnieje już przed przypisaniem jej do tabeli.  
- **Prefer explicit checks**: `workbook.getNames().get("Name")` zwraca `null`, jeśli nazwa jest wolna, co jest bezpieczniejsze niż przechwytywanie ogólnego wyjątku.  
- **Keep naming conventions consistent**: Używanie prefiksu takiego jak `tbl_` dla tabel i `rng_` dla zakresów zmniejsza ryzyko kolizji.  
- **Version compatibility**: Kod działa z Aspose.Cells 23.9 i nowszymi; wcześniejsze wersje mogą mieć inne komunikaty wyjątków.

## Zakończenie

Teraz wiesz, jak **create a named range**, **add named range**, **create Excel table**, **set table name** oraz **detect duplicate name** konflikty przy użyciu Aspose.Cells for Java. Dzięki proaktywnemu radzeniu sobie z kolizjami nazw, utrzymujesz swoje skoroszyty w czystości, a skrypty automatyzacji są solidne.

**Kolejne kroki**

- Zbadaj dalej API **set table name**, aby zastosować opcje stylizacji.  
- Użyj wzorca **detect duplicate name** przy programowym generowaniu wielu tabel.  
- Połącz zakresy nazwane z formułami lub walidacją danych dla dynamicznego raportowania.

Miłego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i zbadać alternatywne podejścia implementacyjne w własnych projektach.

- [Utwórz stylowany zakres nazwany Excel Aspose Cells Java](/cells/hindi/java/tables-structured-references/create-style-named-range-excel-aspose-cells-java/)
- [Utwórz stylowany zakres nazwany Excel Aspose Cells Java](/cells/german/java/tables-structured-references/create-style-named-range-excel-aspose-cells-java/)
- [Utwórz stylowany zakres nazwany Excel Aspose Cells Java](/cells/french/java/tables-structured-references/create-style-named-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}