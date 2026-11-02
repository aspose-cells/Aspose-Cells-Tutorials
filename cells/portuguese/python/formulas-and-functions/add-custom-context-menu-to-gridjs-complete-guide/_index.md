---
category: general
date: 2026-06-08
description: Adicione um menu de contexto personalizado ao GridJs e exporte a grade
  para CSV com um blob de arquivo CSV para download. Siga este tutorial passo a passo
  para um exemplo totalmente funcional.
draft: false
keywords:
- add custom context menu
- export grid to csv
- download csv file blob
- GridJs context menu
- Flask CSV export
language: pt
og_description: Adicione menu de contexto personalizado ao GridJs e exporte a grade
  para CSV com um blob de arquivo CSV para download. Aprenda a implementação completa
  em menos de 10 minutos.
og_title: Adicionar Menu de Contexto Personalizado ao GridJs – Guia Completo
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
title: Adicionar Menu de Contexto Personalizado ao GridJs – Guia Completo
url: /pt/python/formulas-and-functions/add-custom-context-menu-to-gridjs-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar Menu de Contexto Personalizado ao GridJs – Guia Completo

Quer **adicionar um menu de contexto personalizado** a um componente GridJs? Neste tutorial vamos guiá‑lo passo a passo e mostrar como **exportar a grade para CSV** usando um **blob de arquivo CSV para download**. Seja construindo um painel administrativo rápido ou um painel de relatórios completo, um menu de clique‑direito que permite aos usuários extrair dados como CSV pode ser um grande aumento de produtividade.

Cobriremos tudo o que você precisa: o lado Python com Flask, o manipulador JavaScript que cria o Blob e o HTML/JS que o GridJs gera. Ao final, você terá um exemplo autocontido que pode ser inserido em qualquer projeto.

---

## O que você precisará

- **Python 3.9+** e **Flask** instalados (`pip install flask`).
- O **gridjs** wrapper para Python (ou a biblioteca JavaScript diretamente) – para este guia assumiremos um wrapper Python leve que espelha a API JavaScript.
- Um entendimento básico de **async JavaScript** (`fetch`, `Promise`) – mas não se preocupe, explicaremos cada linha.
- Um editor de sua preferência (VS Code, PyCharm ou até mesmo um editor de texto simples).

É isso. Sem ferramentas extras de build front‑end, sem dança do Node npm. Apenas Flask simples servindo o HTML que o GridJs gera.

---

## Adicionar Menu de Contexto Personalizado ao GridJs

A primeira coisa que você precisa fazer é informar ao GridJs que deseja um menu de clique‑direito personalizado. Por padrão, o GridJs vem com um conjunto mínimo (copiar, colar, etc.), mas você pode substituí‑lo completamente.

```python
# Step 1: Create a new workbook that will be displayed in the grid
workbook = Workbook()

# Step 2: Initialise the GridJs component with the workbook
grid_js = GridJs(workbook)

# Step 3: Define a custom context‑menu that includes an "Export CSV" command
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]
```

**Por que isso importa:**  
Definir `CustomContextMenu` substitui a lista padrão pela que você fornece. A string `"Export CSV"` é apenas um rótulo – o trabalho real acontece quando o usuário clica nela, o que conectaremos no próximo passo.

> *Dica:* Mantenha a lista curta. Um menu de contexto desordenado anula o propósito de ações rápidas.

---

## Exportar a Grade para CSV com Download de Blob

Agora que o item de menu existe, precisamos de um manipulador JavaScript que converse com o servidor, busque o CSV, o transforme em um **Blob** e force o download. É aqui que a expressão **download CSV file blob** aparece.

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

### Desmembrando o Manipulador

| Line | What It Does |
|------|--------------|
| `fetch('/export/csv?sheet=' + cell.sheetName)` | Chama uma rota Flask (`/export/csv`) passando o nome da planilha como string de consulta. |
| `.then(r => r.blob())` | Converte a resposta HTTP para um **Blob** – essencialmente um contêiner binário para os dados CSV. |
| `URL.createObjectURL(b)` | Gera uma URL temporária que o navegador pode tratar como um arquivo. |
| `a.download = cell.sheetName + ".csv"` | Define o nome do arquivo que o usuário verá na caixa de diálogo de download. |
| `a.click()` | Clica programaticamente no âncora oculto, provocando o download do Blob. |

> **Por que usar um Blob?**  
> Os navegadores não podem baixar diretamente texto bruto retornado por `fetch` sem transformá‑lo em algo semelhante a um arquivo. O truque da Blob‑URL é a forma mais confiável e compatível entre navegadores de disparar um **download CSV file blob** sem recarregar a página.

---

## Configurando o Backend Flask

O manipulador front‑end espera um endpoint em `/export/csv`. Aqui está uma visualização Flask mínima que recebe o nome da planilha, extrai os dados da pasta de trabalho e devolve um CSV em streaming.

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

### Pontos Principais

- **`io.StringIO`** nos permite construir o CSV na memória sem tocar no sistema de arquivos.
- **`Content‑Disposition`** informa ao navegador que o arquivo é um anexo e sugere um nome de arquivo. Embora o front‑end também defina `a.download`, tê‑lo no lado do servidor fornece uma alternativa para clientes sem JavaScript.
- A rota é deliberadamente simples; você pode adicionar autenticação, verificações de permissão ou streaming para conjuntos de dados enormes posteriormente.

---

## Renderizando a Grade no Cliente

Com o menu de contexto e o backend prontos, a peça final é renderizar o componente GridJs e enviar o HTML/JS ao navegador.

```python
# Step 5: Render the grid to obtain the full HTML/JS needed on the client side
html_output = grid_js.Render()
print(html_output)   # Sends the HTML/JS to the client (e.g., in a Flask view)
```

Em uma visualização Flask, você normalmente faria:

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

Quando a página carrega, o GridJs constrói a tabela, injeta o menu de contexto personalizado e o manipulador JavaScript que definimos anteriormente está pronto para ser acionado. Clique‑direito em qualquer célula, escolha **Export CSV** e veja o navegador baixar um arquivo nomeado com o nome da planilha.

---

## Exemplo Completo Funcional (Todos os Arquivos)

Abaixo está o código completo e executável que você pode copiar‑colar em uma nova pasta. Instale o Flask (`pip install flask`) e execute `python app.py`.

**`app.py`**



## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Carregar arquivos CSV com analisadores personalizados Aspose Cells Java](/cells/hindi/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)
- [Código de exportação CSV em Java](/cells/hindi/java/excel-import-export/csv-export-java-code/)
- [Exportar Excel CSV linhas em branco Aspose Cells .NET](/cells/hindi/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}