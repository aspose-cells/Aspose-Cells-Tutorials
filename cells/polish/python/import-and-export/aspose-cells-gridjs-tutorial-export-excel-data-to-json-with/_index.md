---
category: general
date: 2026-07-03
description: Samouczek Aspose Cells GridJs pokazujący, jak eksportować dane Excela
  do formatu JSON oraz eksportować arkusz do JSON efektywnie, wykorzystując leniwe
  ładowanie.
draft: false
keywords:
- aspose cells gridjs tutorial
- export excel data json
- export worksheet to json
language: pl
og_description: Samouczek Aspose Cells GridJs wyjaśnia, jak wyeksportować dane z Excela
  do formatu JSON oraz jak wyeksportować arkusz do JSON z leniwym ładowaniem dla dużych
  arkuszy kalkulacyjnych.
og_title: Samouczek Aspose Cells GridJs – Eksport danych Excel do JSON
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Aspose Cells GridJs tutorial showing how to export Excel data JSON
    and export worksheet to JSON efficiently using lazy loading.
  headline: Aspose Cells GridJs tutorial – Export Excel data to JSON with lazy loading
  type: TechArticle
- description: Aspose Cells GridJs tutorial showing how to export Excel data JSON
    and export worksheet to JSON efficiently using lazy loading.
  name: Aspose Cells GridJs tutorial – Export Excel data to JSON with lazy loading
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed locally. - `asposecells` package (you can `pip
      install aspose-cells`). - A sizeable Excel file (e.g., `large-data.xlsx`) placed
      in a known directory. - Basic familiarity with Python and web development concepts.'
  - name: Exporting a specific worksheet
    text: 'The example above always uses the first worksheet (`Worksheets[0]`). To
      export a different sheet, simply change the index or use the sheet name:'
  - name: Changing the chunk size for massive files
    text: For files with millions of rows, a chunk size of 500 may still be too small,
      causing many round‑trips. You can increase it to 2000 or more, but remember
      that larger chunks consume more bandwidth per request.
  - name: Exporting to a stream instead of a file
    text: 'If your API returns the JSON directly, you don’t need to write to disk:'
  - name: Handling formulas and formatting
    text: 'By default, `ExportGridJsJson` includes the calculated values of formulas.
      If you need raw formulas instead, set:'
  type: HowTo
tags:
- Aspose.Cells
- Python
- GridJs
- JSON export
title: Samouczek Aspose Cells GridJs – Eksport danych z Excela do JSON z leniwym ładowaniem
url: /pl/python/import-and-export/aspose-cells-gridjs-tutorial-export-excel-data-to-json-with/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Samouczek Aspose Cells GridJs – Eksport danych Excel do JSON z leniwym ładowaniem

Zastanawiałeś się kiedyś, jak **eksportować dane Excel do JSON** z ogromnego arkusza kalkulacyjnego bez obciążania przeglądarki? W tym samouczku Aspose Cells GridJs przeprowadzimy Cię przez kompletną, gotową do uruchomienia rozwiązanie, które umożliwia **eksport arkusza do JSON** przy użyciu leniwego ładowania, tak aby pobierane były tylko potrzebne wiersze na żądanie.

Jeśli walczysz z ogromnymi plikami `.xlsx`, a strona kliencka ciągle się zawiesza, nie jesteś sam. Dobra wiadomość? Podejście, które tutaj przedstawiamy, jest lekkie i skalowalne, a możesz je wstawić do dowolnego projektu w Pythonie, który już korzysta z biblioteki Aspose.Cells.

## Co obejmuje ten przewodnik

W ciągu kilku minut nauczysz się:

1. Załadować duży skoroszyt przy użyciu Aspose.Cells.  
2. Włączyć leniwe ładowanie w GridJs, aby serwer przesyłał wiersze w partiach.  
3. Wyeksportować konfigurację GridJs do pliku JSON, który może być użyty po stronie front‑endu.  
4. Dostosować rozmiar partii dla optymalnej wydajności.  
5. Zweryfikować wynik i zintegrować go z prostą stroną HTML.

Bez zewnętrznych usług, bez ukrytej magii — tylko czysty Python i API Aspose.Cells. Po zakończeniu będziesz mieć **kompletny pipeline eksportu arkusza do JSON**, który możesz dostosować do pulpitów, narzędzi raportowych lub dowolnego komponentu siatki danych.

### Wymagania wstępne

- Python 3.8+ zainstalowany lokalnie.  
- Pakiet `asposecells` (możesz go zainstalować poleceniem `pip install aspose-cells`).  
- Znaczny plik Excel (np. `large-data.xlsx`) umieszczony w znanym katalogu.  
- Podstawowa znajomość Pythona i koncepcji tworzenia aplikacji webowych.

Jeśli którykolwiek z tych punktów jest Ci nieznany, nie panikuj — każdy krok zawiera krótkie wyjaśnienie „dlaczego”, abyś zrozumiał uzasadnienie kodu.

---

## Krok 1: Zainstaluj i zaimportuj Aspose.Cells

Najpierw potrzebujemy biblioteki Aspose.Cells. To produkt komercyjny, ale darmowa wersja próbna wystarczy do rozwoju.

```bash
pip install aspose-cells
```

Teraz zaimportuj niezbędne klasy w swoim skrypcie.

```python
# Step 1: Import the Aspose.Cells workbook class
import asposecells
from asposecells import Workbook
```

> **Dlaczego to ważne:** Importowanie `Workbook` daje dostęp do wysokowydajnego silnika, który odczytuje pliki Excel bezpośrednio do pamięci, omijając wolniejsze podejście oparte na `openpyxl`.

## Krok 2: Załaduj skoroszyt zawierający duży zestaw danych

Po przygotowaniu biblioteki wskaż na swój plik Excel. Ścieżka może być bezwzględna lub względna; po prostu upewnij się, że plik istnieje.

```python
# Step 2: Load the workbook that contains a large data set
workbook = Workbook("YOUR_DIRECTORY/large-data.xlsx")
```

> **Wskazówka:** Jeśli Twój skoroszyt ma rozmiar większy niż kilka set megabajtów, rozważ zwiększenie limitu pamięci procesu Pythona lub użycie interpretera 64‑bitowego, aby uniknąć `MemoryError`.

## Krok 3: Włącz leniwe ładowanie w GridJs

GridJs to komponent siatki JavaScript od Aspose. Leniwe ładowanie mówi serwerowi, aby wysyłał tylko podzbiór wierszy — idealne dla ogromnych arkuszy.

```python
# Step 3: Enable lazy loading so the client fetches rows on demand
grid_options = workbook.Worksheets[0].Cells.GridJsOptions
grid_options.LazyLoading = True                 # fetch rows/columns only when needed
grid_options.LazyLoadingChunkSize = 500         # rows per server request
```

> **Dlaczego leniwe ładowanie?** Bez tego cały arkusz byłby serializowany do JSON jednorazowo, co łatwo może przekroczyć limity pamięci przeglądarki. Ustawiając `LazyLoadingChunkSize` na 500, każde żądanie niesie ze sobą poręczną porcję danych.

## Krok 4: Wyeksportuj konfigurację GridJs do JSON

Teraz prosimy Aspose o wygenerowanie JSON, którego oczekuje komponent front‑endowy GridJs. To serce operacji **eksportu danych Excel do JSON**.

```python
# Step 4: Export the GridJs configuration to a JSON file for the client side
grid_json = workbook.Worksheets[0].Cells.ExportGridJsJson()
```

Metoda `ExportGridJsJson` zwraca obiekt `bytes` zawierający reprezentację JSON arkusza, gotową do zapisania lub strumieniowania.

## Krok 5: Zapisz JSON do pliku (lub strumieniuj go)

Na szybki test zapisz JSON na dysku. W produkcyjnym API zwrócisz go bezpośrednio z endpointu Flask/Django.

```python
# Step 5: Persist the JSON to a file
output_path = "YOUR_DIRECTORY/lazygrid.json"
with open(output_path, "wb") as f:
    f.write(grid_json)

print(f"✅ GridJs JSON exported successfully to {output_path}")
```

> **Co zobaczysz:** Otwierając `lazygrid.json` zobaczysz strukturę z `columns`, `rows` i metadanymi paginacji. Tablica `rows` będzie początkowo pusta; GridJs poprosi o pierwszą partię po załadowaniu strony.

## Krok 6: Podłącz JSON do prostej strony HTML (opcjonalnie)

Jeśli chcesz zobaczyć siatkę w akcji, utwórz mały plik HTML, który załaduje GridJs z CDN i wskaże na wygenerowany JSON.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Lazy‑Loaded GridJs Demo</title>
    <link href="https://unpkg.com/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
    <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
</head>
<body>
    <div id="wrapper"></div>
    <script>
        // Fetch the lazy‑loaded JSON and initialize GridJs
        fetch('lazygrid.json')
            .then(r => r.json())
            .then(config => {
                new gridjs.Grid({
                    ...config,
                    server: {
                        url: 'lazygrid.json',
                        then: data => data
                    }
                }).render(document.getElementById('wrapper'));
            });
    </script>
</body>
</html>
```

> **Dlaczego to uwzględnić?** Pokazuje pełny cykl: Python tworzy JSON, przeglądarka go pobiera, a GridJs renderuje dane partiami. Teraz możesz eksperymentować z różnymi wartościami `LazyLoadingChunkSize`, aby znaleźć optymalny punkt dla Twojej sieci.

## Krok 7: Zweryfikuj i rozwiąż problemy

Uruchom skrypt Pythona:

```bash
python export_lazy_grid.py
```

Powinieneś zobaczyć komunikat o sukcesie oraz plik `lazygrid.json`. Otwórz plik HTML w przeglądarce; siatka powinna natychmiast wyświetlić pierwsze 500 wierszy, a kontrolki paginacji umożliwią ładowanie kolejnych.

Jeśli siatka jest pusta:

- **Sprawdź rozmiar pliku JSON** — plik o zerowej wielkości zazwyczaj oznacza błędną ścieżkę do skoroszytu.  
- **Potwierdź, że leniwe ładowanie jest włączone** — flaga `LazyLoading` musi mieć wartość `True`.  
- **Przejrzyj konsolę przeglądarki** — błędy CORS lub 404 wskazują, że JSON nie jest prawidłowo serwowany.

---

## Typowe wariacje i przypadki brzegowe

### Eksport konkretnego arkusza

Powyższy przykład zawsze używa pierwszego arkusza (`Worksheets[0]`). Aby wyeksportować inny arkusz, po prostu zmień indeks lub użyj nazwy arkusza:

```python
sheet = workbook.Worksheets["DataSheet"]   # by name
grid_options = sheet.Cells.GridJsOptions
grid_json = sheet.Cells.ExportGridJsJson()
```

### Zmiana rozmiaru partii dla ogromnych plików

Dla plików z milionami wierszy rozmiar partii 500 może być nadal za mały, powodując wiele dodatkowych żądań. Możesz zwiększyć go do 2000 lub więcej, ale pamiętaj, że większe partie zużywają więcej pasma przy każdym żądaniu.

```python
grid_options.LazyLoadingChunkSize = 2000
```

### Eksport do strumienia zamiast do pliku

Jeśli Twój API zwraca JSON bezpośrednio, nie musisz zapisywać go na dysku:

```python
from flask import Flask, Response
app = Flask(__name__)

@app.route("/api/gridjson")
def gridjson():
    json_bytes = workbook.Worksheets[0].Cells.ExportGridJsJson()
    return Response(json_bytes, mimetype="application/json")
```

### Obsługa formuł i formatowania

Domyślnie `ExportGridJsJson` zawiera wyliczone wartości formuł. Jeśli potrzebujesz surowych formuł, ustaw:

```python
grid_options.ExportFormulas = True
```

---

## Zakończenie

W tym **samouczku Aspose Cells GridJs** omówiliśmy wszystko, co potrzebne do **eksportu danych Excel do JSON** oraz **eksportu arkusza do JSON** z leniwym ładowaniem. Od instalacji Aspose.Cells, przez włączenie leniwego ładowania, generowanie JSON, po podłączenie go do prostej strony HTML — masz teraz pełny wzorzec full‑stack, który skalowalnie radzi sobie z masywnymi arkuszami.

Wypróbuj go — dostosuj rozmiar partii, wskaż różne arkusze lub zintegruj endpoint z aplikacją Flask lub Django. Możliwości są nieograniczone, a zyski wydajnościowe natychmiastowe.

Gotowy na kolejny krok? Spróbuj dodać sortowanie kolumn, własne renderery komórek lub nawet filtrowanie po stronie serwera, aby Twoja siatka GridJs stała się naprawdę interaktywna. Jeśli napotkasz problem, zostaw komentarz poniżej; powodzenia w kodowaniu!

## Co warto nauczyć się dalej?

Poniższe samouczki dotyczą ściśle powiązanych tematów, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz wyjaśnienia krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Importowanie danych JSON do Excela przy użyciu Aspose.Cells Java: Kompletny przewodnik](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Ładowanie CSV i eksport do JSON przy użyciu Aspose.Cells dla .NET: Kompletny przewodnik](/cells/english/net/import-export/load-csv-export-json-aspose-cells-dotnet/)
- [Eksport danych Excel przy użyciu Aspose.Cells .NET: Pełny przewodnik dla bezproblemowego eksportu danych](/cells/english/net/import-export/export-excel-data-aspose-cells-net-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}