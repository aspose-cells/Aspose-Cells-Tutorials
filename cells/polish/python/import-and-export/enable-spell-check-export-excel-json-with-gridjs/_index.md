---
category: general
date: 2026-06-21
description: Włącz sprawdzanie pisowni podczas eksportowania JSON z Excela przy użyciu
  GridJs. Dowiedz się, jak konwertować pliki xlsx na JSON, konfigurować leniwe ładowanie
  i efektywnie wczytywać skoroszyt Excel.
draft: false
keywords:
- enable spell check
- export excel json
- convert xlsx to json
- configure lazy loading
- load excel workbook
language: pl
og_description: Włącz sprawdzanie pisowni podczas eksportowania JSON z Excela przy
  użyciu GridJs. Ten przewodnik pokazuje, jak przekonwertować plik xlsx na JSON, skonfigurować
  leniwe ładowanie i wczytać skoroszyt Excel.
og_title: Włącz sprawdzanie pisowni i eksportuj Excel JSON za pomocą GridJs
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Enable spell check while you export Excel JSON using GridJs. Learn
    to convert xlsx to JSON, configure lazy loading, and load Excel workbook efficiently.
  headline: Enable Spell Check & Export Excel JSON with GridJs
  type: TechArticle
tags:
- GridJs
- Excel
- JSON
- Python
title: Włącz sprawdzanie pisowni i eksportuj Excel JSON przy użyciu GridJs
url: /pl/python/import-and-export/enable-spell-check-export-excel-json-with-gridjs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Włącz sprawdzanie pisowni i eksportuj Excel JSON przy użyciu GridJs

Czy kiedykolwiek potrzebowałeś **włączyć sprawdzanie pisowni** w interfejsie arkusza kalkulacyjnego opartym na sieci i zastanawiałeś się, jak jednocześnie uzyskać dane w formacie JSON? Nie jesteś sam. Wielu programistów napotyka ten sam problem, gdy próbują **wyeksportować Excel JSON** z zeszytu, zachowując jednocześnie zaawansowane funkcje, takie jak weryfikacja formuł.

W tym samouczku przeprowadzimy Cię przez kompletny, działający przykład, który pokaże, jak **załadować skoroszyt Excel**, przekształcić go w ładunek JSON przy użyciu GridJs, **skonfigurować leniwe ładowanie** i oczywiście **włączyć sprawdzanie pisowni**. Po zakończeniu będziesz w stanie **konwertować xlsx na JSON** w zaledwie kilku linijkach — bez tajemnic, bez brakujących elementów.

> **Co wyniesiesz z tego**  
> * Skrypt w Pythonie, który odczytuje plik `.xlsx`, uruchamia obiekt serwera GridJs i zapisuje `grid_data.json`.  
> * Zrozumienie, dlaczego każda opcja ma znaczenie (sprawdzanie pisowni, sprawdzanie formuł, leniwe ładowanie).  
> * Wskazówki dotyczące skalowania rozwiązania do większych skoroszytów.

---

## Wymagania wstępne

Zanim zanurkujemy, upewnij się, że masz następujące elementy na swoim komputerze:

| Wymaganie | Dlaczego jest ważne |
|-------------|----------------|
| Python 3.9+ | Wymagany dla pakietu `cells` używanego poniżej. |
| `cells` library (`pip install cells`) | Udostępnia klasy `Workbook` i `GridJs`. |
| A sample Excel file (`sample.xlsx`) | To jest źródło, z którego **załadujemy skoroszyt Excel**. |
| Write permission to the output folder | Uprawnienia do zapisu w folderze wyjściowym. |

Jeśli któreś z tych wymagań jest Ci nieznane, zatrzymaj się i najpierw je zainstaluj — w przeciwnym razie skrypt zgłosi błąd importu.

---

## Krok 1: Załaduj skoroszyt Excel

Pierwszą rzeczą, którą robisz, gdy chcesz **konwertować xlsx na json**, jest otwarcie skoroszytu. Pomyśl o tym jak o odblokowaniu drzwi, zanim będziesz mógł udekorować pokój.

```python
import cells

# Replace YOUR_DIRECTORY with the actual path on your system
workbook_path = "YOUR_DIRECTORY/sample.xlsx"

# Load the workbook – this is the entry point for all further operations
workbook = cells.Workbook(workbook_path)
print(f"Workbook loaded: {workbook_path}")
```

> **Pro tip:** Jeśli Twój plik jest ogromny, rozważ użycie `cells.Workbook(..., read_only=True)`, aby zmniejszyć zużycie pamięci.

---

## Krok 2: Utwórz obiekt serwera GridJs

Teraz, gdy skoroszyt znajduje się w pamięci, potrzebujemy obiektu **GridJs**, który przetłumaczy arkusze na JSON, który może być użyty przez interfejs klienta.

```python
# Create a GridJs instance linked to the workbook
grid = cells.GridJs(workbook)
print("GridJs server object created.")
```

Zmienna `grid` jest w zasadzie cienką warstwą otaczającą skoroszyt, która potrafi serializować komórki, formuły i nawet informacje o stylach.

---

## Krok 3: Włącz sprawdzanie pisowni (i sprawdzanie formuł)

Tutaj główne słowo kluczowe błyszczy. Przełączając flagę `enableSpellCheck`, dajesz użytkownikom końcowym zabezpieczenie przed literówkami — tak jak w wersji desktopowej Excela.

```python
# Turn on advanced validation features
grid.options["enableFormulaChecker"] = True   # optional but handy
grid.options["enableSpellCheck"] = True       # <-- enable spell check
print("Spell check and formula checker enabled.")
```

Dlaczego włączyć oba? Sprawdzanie pisowni łapie błędy tekstowe, podczas gdy sprawdzanie formuł chroni przed zepsutymi obliczeniami. Razem sprawiają, że interfejs webowy jest tak dopracowany, jak natywne doświadczenie Excela.

---

## Krok 4: Skonfiguruj leniwe ładowanie

Jeśli masz do czynienia z tysiącami wierszy, wysłanie całego zestawu danych w jednym ładunku obciąży przeglądarkę. **Skonfiguruj leniwe ładowanie**, aby przesyłać dane w małych porcjach (500 wierszy na żądanie w naszym przykładzie).

```python
# Lazy loading improves performance for large sheets
grid.options["lazyLoading"] = {"pageSize": 500}
print("Lazy loading configured: 500 rows per request.")
```

Możesz dostosować `pageSize` w zależności od warunków sieciowych. Mniejsze strony oznaczają więcej zapytań, ale płynniejszy interfejs; większe strony zmniejszają liczbę wywołań, ale mogą powodować opóźnienia.

---

## Krok 5: Eksportuj Excel JSON

Całe ciężkie przetwarzanie odbywa się teraz w tle. Ostatnim krokiem jest **eksportowanie excel json** do pliku, który może być żądany przez front‑end.

```python
# Destination for the generated JSON
output_path = "YOUR_DIRECTORY/grid_data.json"

# Persist the JSON representation
grid.save(output_path)
print(f"JSON exported to: {output_path}")
```

Gdy metoda `save` zakończy się, będziesz mieć schludny plik `grid_data.json` zawierający:

* Nazwy arkuszy i ich ID  
* Dane wierszy (wartości, formuły i formatowanie)  
* Metadane o włączonych funkcjach (sprawdzanie pisowni, leniwe ładowanie itp.)

Możesz zweryfikować wynik, otwierając plik w edytorze tekstu lub ładując go w konsoli przeglądarki:

```json
{
  "sheets": [
    {
      "name": "Sheet1",
      "rows": [
        {"c": [{"v": "Hello"}, {"v": 123}]},
        {"c": [{"v": "World"}, {"v": 456}]}
      ]
    }
  ],
  "options": {
    "enableSpellCheck": true,
    "enableFormulaChecker": true,
    "lazyLoading": {"pageSize": 500}
  }
}
```

To **kompletne, samodzielne rozwiązanie** do przekształcania pliku Excel w ładunek JSON przy jednoczesnym utrzymaniu sprawdzania pisowni.

---

## Pełny skrypt – połącz wszystko razem

Poniżej znajduje się cały program, który możesz skopiować‑wkleić, dostosować ścieżki i uruchomić. Bez ukrytych kroków, bez zewnętrznych skryptów — tylko jeden plik.

```python
import cells

# ----------------------------------------------------------------------
# Configuration – adjust these variables to match your environment
# ----------------------------------------------------------------------
WORKBOOK_PATH = "YOUR_DIRECTORY/sample.xlsx"
OUTPUT_JSON = "YOUR_DIRECTORY/grid_data.json"
PAGE_SIZE = 500   # rows per lazy‑load request

# ----------------------------------------------------------------------
# 1️⃣ Load the Excel workbook
# ----------------------------------------------------------------------
workbook = cells.Workbook(WORKBOOK_PATH)
print(f"[✓] Loaded workbook from {WORKBOOK_PATH}")

# ----------------------------------------------------------------------
# 2️⃣ Create GridJs server object
# ----------------------------------------------------------------------
grid = cells.GridJs(workbook)
print("[✓] GridJs instance ready")

# ----------------------------------------------------------------------
# 3️⃣ Enable spell check + formula checking
# ----------------------------------------------------------------------
grid.options["enableFormulaChecker"] = True
grid.options["enableSpellCheck"] = True
print("[✓] Spell check and formula checker enabled")

# ----------------------------------------------------------------------
# 4️⃣ Configure lazy loading for performance
# ----------------------------------------------------------------------
grid.options["lazyLoading"] = {"pageSize": PAGE_SIZE}
print(f"[✓] Lazy loading set to {PAGE_SIZE} rows per request")

# ----------------------------------------------------------------------
# 5️⃣ Export the workbook as JSON
# ----------------------------------------------------------------------
grid.save(OUTPUT_JSON)
print(f"[✓] Exported JSON to {OUTPUT_JSON}")
```

Zapisz to jako `export_gridjs.py` i uruchom:

```bash
python export_gridjs.py
```

Powinieneś zobaczyć serię komunikatów `[✓]` potwierdzających pomyślne wykonanie każdego kroku.

---

## Częste pytania i przypadki brzegowe

**Co jeśli mój skoroszyt zawiera wiele arkuszy?**  
GridJs automatycznie iteruje po każdym arkuszu, więc wynikowy JSON będzie miał tablicę `sheets`. Możesz filtrować po stronie klienta, jeśli potrzebujesz tylko podzbioru.

**Czy mogę wyłączyć sprawdzanie pisowni dla konkretnego arkusza?**  
Słownik `options` działa globalnie. Aby przełączać per‑arkusz, musiałbyś stworzyć osobne obiekty `GridJs` lub przetworzyć JSON po wygenerowaniu.

**Mój plik jest większy niż 10 MB — czy leniwe ładowanie nadal pomoże?**  
Zdecydowanie tak. Leniwe ładowanie działa na poziomie API; serwer strumieniuje tylko żądaną stronę. Rozważ jednak zwiększenie `pageSize` do 1000, jeśli opóźnienie sieci jest niskie.

**Czy muszę się martwić o znaki Unicode?**  
`cells` obsługuje UTF‑8 od razu, więc znaki takie jak emoji czy skrypty niełacińskie przetrwają konwersję.

---

## Wskazówki profesjonalne dla produkcji

* **Cache the JSON** – Jeśli skoroszyt rzadko się zmienia, buforuj `grid_data.json` w CDN dla błyskawicznego ładowania.  
* **Security** – Nigdy nie udostępniaj surowego pliku Excel; serwuj tylko wygenerowany JSON.  
* **Versioning** – Dołącz numer wersji do nazwy pliku JSON (np. `grid_data_v2.json`), aby uniknąć przestarzałych danych po aktualizacjach.  
* **Testing** – Napisz mały test jednostkowy, który ładuje JSON i sprawdza, czy `enableSpellCheck` jest `true`. Dzięki temu wczesnie wykryjesz regresje.

---

## Podsumowanie

Masz teraz solidny, kompleksowy przepis na **włączenie sprawdzania pisowni** podczas **eksportowania Excel JSON** przy użyciu GridJs. Od **ładowania skoroszytu Excel** po **konfigurację leniwego ładowania**, a w końcu **konwersję xlsx na json**, proces jest prosty i gotowy do produkcji.  

Kolejne kroki? Spróbuj podłączyć wygenerowany `grid_data.json` do prostej strony HTML używającej biblioteki klienckiej GridJs, eksperymentuj z własnymi renderownikami komórek lub dodaj uwierzytelnianie wokół endpointu JSON. Nie ma granic, gdy połączysz sprawdzanie pisowni, leniwe ładowanie i płynną konwersję Excel‑to‑JSON.

Masz więcej pytań lub trudny skoroszyt, z którym się mierzysz? zostaw komentarz poniżej i szczęśliwego kodowania!  

---

![Włącz sprawdzanie pisowni w GridJs](/images/enable-spell-check-gridjs.png "Zrzut ekranu pokazujący włączone sprawdzanie pisowni w interfejsie GridJs")

## Co warto nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Eksportuj Excel do JSON](/cells/english/java/excel-import-export/export-excel-to-json/)
- [Importuj dane JSON do Excela przy użyciu Aspose.Cells Java: Kompletny przewodnik](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Jak efektywnie filtrować dane podczas ładowania skoroszytów Excel przy użyciu Aspose.Cells w Javie](/cells/english/java/data-analysis/filter-data-excel-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}