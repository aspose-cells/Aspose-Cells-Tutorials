---
category: general
date: 2026-06-08
description: Dodaj własne menu kontekstowe do GridJs i wyeksportuj siatkę do CSV z
  pobieraniem pliku CSV jako blob. Postępuj zgodnie z tym samouczkiem krok po kroku,
  aby uzyskać w pełni działający przykład.
draft: false
keywords:
- add custom context menu
- export grid to csv
- download csv file blob
- GridJs context menu
- Flask CSV export
language: pl
og_description: Dodaj własne menu kontekstowe do GridJs i wyeksportuj siatkę do CSV
  przy użyciu pobierania pliku CSV jako blob. Poznaj pełną implementację w mniej niż
  10 minut.
og_title: Dodaj własne menu kontekstowe do GridJs – kompletny przewodnik
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Add custom context menu to GridJs and export grid to CSV with a download
    CSV file blob. Follow this step‑by‑step tutorial for a fully working example.
  headline: Add Custom Context Menu to GridJs – Complete Guide
  type: TechArticle
tags:
- GridJs
- JavaScript
- Python
- Flask
title: Dodaj własne menu kontekstowe do GridJs – Kompletny przewodnik
url: /pl/python/formulas-and-functions/add-custom-context-menu-to-gridjs-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dodaj własne menu kontekstowe do GridJs – Kompletny przewodnik

Chcesz **dodać własne menu kontekstowe** do komponentu GridJs? W tym samouczku przeprowadzimy Cię krok po kroku przez ten proces i pokażemy, jak **wyeksportować siatkę do CSV** używając **blobu pliku CSV do pobrania**. Niezależnie od tego, czy tworzysz szybki panel administracyjny, czy rozbudowany pulpit raportowy, menu po kliknięciu prawym przyciskiem, które pozwala użytkownikom wyciągnąć dane jako CSV, może znacząco zwiększyć produktywność.

Omówimy wszystko, czego potrzebujesz: część Pythona z Flask, obsługę JavaScript, która tworzy Blob, oraz HTML/JS generowany przez GridJs. Po zakończeniu będziesz mieć samodzielny przykład, który możesz wkleić do dowolnego projektu.

---

## Czego będziesz potrzebować

- **Python 3.9+** i **Flask** zainstalowane (`pip install flask`).
- Wrapper **gridjs** w Pythonie (lub bezpośrednio biblioteka JavaScript) – w tym przewodniku zakładamy cienki wrapper Pythona odzwierciedlający API JavaScript.
- Podstawowa znajomość **async JavaScript** (`fetch`, `Promise`) – ale nie martw się, wyjaśnimy każdy wiersz.
- Edytor, który lubisz (VS Code, PyCharm, a nawet prosty edytor tekstu).

To wszystko. Nie potrzebujesz dodatkowych narzędzi front‑end, nie ma tańca z Node npm. Po prostu czysty Flask serwujący HTML generowany przez GridJs.

## Dodaj własne menu kontekstowe do GridJs

Pierwszą rzeczą, którą musisz zrobić, jest poinformowanie GridJs, że chcesz własne menu po kliknięciu prawym przyciskiem. Domyślnie GridJs dostarcza minimalny zestaw (kopiuj, wklej itp.), ale możesz go całkowicie zastąpić.

```python
# Step 1: Create a new workbook that will be displayed in the grid
workbook = Workbook()

# Step 2: Initialise the GridJs component with the workbook
grid_js = GridJs(workbook)

# Step 3: Define a custom context‑menu that includes an "Export CSV" command
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]
```

**Dlaczego to ważne:**  
Ustawienie `CustomContextMenu` zastępuje domyślną listę tą, którą podasz. Ciąg znaków `"Export CSV"` to tylko etykieta – prawdziwa praca odbywa się, gdy użytkownik kliknie ją, co podłączymy w następnym kroku.

> *Wskazówka:* Trzymaj listę krótką. Zagracone menu kontekstowe psuje cel szybkich akcji.

## Eksportuj siatkę do CSV przy użyciu pobrania Blob

Teraz, gdy pozycja menu istnieje, potrzebujemy obsługi JavaScript, która komunikuje się z serwerem, pobiera CSV, zamienia go w **Blob** i wymusza pobranie. To właśnie tutaj pojawia się fraza **download CSV file blob**.

```python
# Step 4: Attach a JavaScript handler that runs when "Export CSV" is chosen.
#         The handler sends an AJAX request to a server endpoint,
#         receives the CSV file as a Blob, and triggers a download.
grid_js.CustomContextMenuHandler = """
function(action, cell) {
    if (action === "Export CSV") {
        fetch('/export/csv?sheet=' + cell.sheetName)
            .then(r => r.blob())
            .then(b => {
                const url = URL.createObjectURL(b);
                const a = document.createElement('a');
                a.href = url;
                a.download = cell.sheetName + ".csv";
                a.click();
            });
    }
}
"""
```

### Analiza obsługi

| Linia | Co robi |
|------|--------------|
| `fetch('/export/csv?sheet=' + cell.sheetName)` | Wywołuje trasę Flask (`/export/csv`), przekazując nazwę arkusza jako parametr zapytania. |
| `.then(r => r.blob())` | Konwertuje odpowiedź HTTP na **Blob** – w zasadzie binarny kontener danych CSV. |
| `URL.createObjectURL(b)` | Generuje tymczasowy URL, który przeglądarka może traktować jak plik. |
| `a.download = cell.sheetName + ".csv"` | Ustawia nazwę pliku, którą użytkownik zobaczy w oknie pobierania. |
| `a.click()` | Programowo klika ukryty element anchor, wywołując pobranie Blobu. |

> **Dlaczego używać Blob?**  
> Przeglądarki nie mogą bezpośrednio pobrać surowego tekstu zwróconego przez `fetch` bez przekształcenia go w coś podobnego do pliku. Sztuczka z Blob‑URL jest najpewniejszym, działającym we wszystkich przeglądarkach sposobem na wywołanie **download CSV file blob** bez odświeżania strony.

## Konfiguracja backendu Flask

Obsługa front‑endu oczekuje punktu końcowego pod `/export/csv`. Oto minimalny widok Flask, który przyjmuje nazwę arkusza, pobiera dane z skoroszytu i zwraca CSV.

```python
from flask import Flask, request, Response
import csv
import io

app = Flask(__name__)

# Assume `workbook` is a global object we created earlier
# (in a real app you’d probably fetch it from a database or session)
@app.route('/export/csv')
def export_csv():
    sheet_name = request.args.get('sheet', 'default')
    # Retrieve the sheet data – this is pseudo‑code; replace with your actual API
    sheet = workbook.get_sheet(sheet_name)

    # Convert rows to CSV in memory
    output = io.StringIO()
    writer = csv.writer(output)
    writer.writerow(sheet.headers)          # Header row
    writer.writerows(sheet.rows)            # Data rows

    # Create a Flask response with the correct MIME type
    csv_bytes = output.getvalue().encode('utf-8')
    return Response(
        csv_bytes,
        mimetype='text/csv',
        headers={'Content-Disposition': f'attachment;filename={sheet_name}.csv'}
    )
```

### Kluczowe punkty

- **`io.StringIO`** pozwala nam budować CSV w pamięci, nie dotykając systemu plików.
- **`Content‑Disposition`** informuje przeglądarkę, że plik jest załącznikiem i sugeruje nazwę pliku. Mimo że front‑end również ustawia `a.download`, posiadanie tego po stronie serwera zapewnia awaryjny sposób dla klientów nie‑JS.
- Trasa jest celowo prosta; później możesz dodać uwierzytelnianie, sprawdzanie uprawnień lub strumieniowanie dla bardzo dużych zestawów danych.

## Renderowanie siatki po stronie klienta

Po przygotowaniu menu kontekstowego i backendu, ostatnim elementem jest wyrenderowanie komponentu GridJs i dostarczenie HTML/JS do przeglądarki.

```python
# Step 5: Render the grid to obtain the full HTML/JS needed on the client side
html_output = grid_js.Render()
print(html_output)   # Sends the HTML/JS to the client (e.g., in a Flask view)
```

W widoku Flask zazwyczaj robisz:

```python
@app.route('/')
def index():
    html_output = grid_js.Render()
    return f"""
    <!doctype html>
    <html>
    <head>
        <title>Grid with Custom Context Menu</title>
        <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
        <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
    </head>
    <body>
        {html_output}
    </body>
    </html>
    """
```

Gdy strona się załaduje, GridJs buduje tabelę, wstrzykuje własne menu kontekstowe, a wcześniej zdefiniowana obsługa JavaScript jest gotowa do uruchomienia. Kliknij prawym przyciskiem dowolną komórkę, wybierz **Export CSV** i obserwuj, jak przeglądarka pobiera plik nazwany po nazwie arkusza.

## Pełny działający przykład (wszystkie pliki)

Poniżej znajduje się kompletny, gotowy do uruchomienia kod, który możesz skopiować‑wkleić do nowego folderu. Zainstaluj Flask (`pip install flask`) i uruchom `python app.py`.

**`app.py`**



## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Ładowanie plików CSV z własnymi parserami Aspose Cells Java](/cells/hindi/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)
- [Eksport CSV w Javie – kod](/cells/hindi/java/excel-import-export/csv-export-java-code/)
- [Eksport Excel CSV z pustymi wierszami – Aspose Cells .NET](/cells/hindi/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}