---
category: general
date: 2026-11-22
description: Aprenda a servir Excel em um aplicativo web usando Flask. Este guia mostra
  como carregar uma planilha Excel e exibir o Excel na web com GridJs.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to serve excel
- load excel workbook
- display excel web
language: pt
lastmod: 2026-11-22
og_description: Como servir arquivos Excel usando Flask e GridJs. Siga este tutorial
  completo para carregar uma planilha Excel e exibi‑la na web.
og_image_alt: Screenshot of a Flask‑powered GridJs table showing Excel data
og_title: Como servir Excel com Flask – guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to serve Excel in a web app using Flask. This guide shows
    how to load Excel workbook and display Excel on the web with GridJs.
  headline: How to serve Excel files with Flask and GridJs
  type: TechArticle
- description: Learn how to serve Excel in a web app using Flask. This guide shows
    how to load Excel workbook and display Excel on the web with GridJs.
  name: How to serve Excel files with Flask and GridJs
  steps:
  - name: Load the Excel workbook
    text: '```python # Step 1: Load the workbook you want to expose via GridJs import
      cells'
  - name: Create a GridJs server‑side handler
    text: '```python # Step 2: Create a GridJs server‑side handler for the workbook
      grid_handler = cells.GridJsHandler(workbook) ```'
  - name: Enable optional features (lazy loading)
    text: '```python # Step 3: Enable optional features (e.g., lazy loading for large
      sheets) grid_handler.settings.lazy_load = True ```'
  - name: Set up a minimal Flask application
    text: '```python # Step 4: Set up a minimal Flask application to serve the GridJs
      UI from flask import Flask, request, jsonify'
  - name: Define the GridJs endpoint
    text: '```python # Step 5: Define an endpoint that returns the current view state
      # and applies any client‑side edits sent as JSON @app.route("/gridjs", methods=["GET",
      "POST"]) def gridjs(): if request.method == "POST": # Apply edits sent from
      the GridJs UI grid_handler.apply_changes(request.json) # Retur'
  - name: Run the Flask server
    text: '```python # Step 6: Run the Flask server (default port 5000) if __name__
      == "__main__": # Debug mode is off for production; enable it only during development.
      app.run(port=5000, debug=False) ```'
  type: HowTo
tags:
- Flask
- Python
- Excel
title: Como servir arquivos Excel com Flask e GridJs
url: /pt/python/integration-and-interoperability/how-to-serve-excel-files-with-flask-and-gridjs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como servir arquivos Excel com Flask e GridJs

Se você precisa **how to serve excel** em uma aplicação web Python, este tutorial mostra uma solução completa. Você aprenderá como **load excel workbook** com a biblioteca `cells`, expô-lo através de um endpoint Flask e permitir que os usuários **display excel web** usando GridJs.

Percorreremos cada linha de código, explicaremos por que cada parte importa e forneceremos um exemplo pronto‑para‑executar. Ao final do guia, você poderá incorporar qualquer arquivo `.xlsx` em uma grade responsiva do lado do cliente sem escrever analisadores de dados JavaScript personalizados.

## Pré-requisitos

- Python 3.9+ instalado  
- Pacotes `flask` e `cells` (`pip install flask cells`)  
- Um arquivo Excel de exemplo (por exemplo, `sample.xlsx`) em um diretório conhecido  

Nenhum framework front‑end adicional é necessário; o GridJs lida com a UI automaticamente.

## Visão geral da solução

A ideia central é simples:

1. **Load** o workbook Excel no servidor.  
2. **Create** um `GridJsHandler` que traduz os dados da planilha para o formato JSON que o GridJs espera.  
3. **Expose** uma rota Flask que retorna a visualização JSON e aceita edições do cliente.  
4. **Run** o servidor Flask para que o navegador possa buscar os dados e renderizar a grade.

Agora vamos implementar cada passo.

## Como servir Excel com Flask e GridJs

### Passo 1: Carregar o workbook Excel

```python
# Step 1: Load the workbook you want to expose via GridJs
import cells

workbook_path = "YOUR_DIRECTORY/sample.xlsx"
workbook = cells.Workbook(workbook_path)
```

**Por que isso importa:**  
`cells.Workbook` analisa o arquivo `.xlsx` em uma representação em memória. Carregar o workbook uma vez na inicialização mantém o servidor rápido, pois solicitações subsequentes reutilizam o mesmo objeto em vez de acessar o sistema de arquivos repetidamente.

### Passo 2: Criar um manipulador server‑side do GridJs

```python
# Step 2: Create a GridJs server‑side handler for the workbook
grid_handler = cells.GridJsHandler(workbook)
```

**Por que isso importa:**  
`GridJsHandler` abstrai a conversão de linhas/colunas do Excel para o esquema JSON que o GridJs consome. Também rastreia edições do lado do cliente, permitindo que você persista alterações de volta ao workbook posteriormente, se necessário.

### Passo 3: Habilitar recursos opcionais (lazy loading)

```python
# Step 3: Enable optional features (e.g., lazy loading for large sheets)
grid_handler.settings.lazy_load = True
```

**Por que isso importa:**  
Quando uma planilha contém milhares de linhas, enviar todo o conjunto de dados de uma vez pode sobrecarregar o navegador. O lazy loading transmite os dados página por página, melhorando o desempenho para o cenário **display excel web**.

### Passo 4: Configurar uma aplicação Flask mínima

```python
# Step 4: Set up a minimal Flask application to serve the GridJs UI
from flask import Flask, request, jsonify

app = Flask(__name__)
```

**Por que isso importa:**  
Flask fornece um servidor HTTP leve que pode servir endpoints JSON e arquivos estáticos. Manter a aplicação Flask mínima reduz a superfície de ataque e torna o exemplo fácil de adaptar.

### Passo 5: Definir o endpoint GridJs

```python
# Step 5: Define an endpoint that returns the current view state
#         and applies any client‑side edits sent as JSON
@app.route("/gridjs", methods=["GET", "POST"])
def gridjs():
    if request.method == "POST":
        # Apply edits sent from the GridJs UI
        grid_handler.apply_changes(request.json)
    # Return the JSON view expected by GridJs
    return jsonify(grid_handler.get_view())
```

**Por que isso importa:**  

- **GET** – O navegador obtém a visualização inicial da planilha.  
- **POST** – Quando um usuário edita uma célula, o GridJs envia um payload JSON; `apply_changes` mescla essas edições de volta ao estado interno do manipulador.  

Retornar `grid_handler.get_view()` garante que o cliente sempre receba os dados mais recentes, o que é essencial para uma experiência fluida de **display excel web**.

### Passo 6: Executar o servidor Flask

```python
# Step 6: Run the Flask server (default port 5000)
if __name__ == "__main__":
    # Debug mode is off for production; enable it only during development.
    app.run(port=5000, debug=False)
```

**Por que isso importa:**  
Executar na porta 5000 é o padrão do Flask, facilitando testes locais (`http://localhost:5000/gridjs`). Em produção, você colocaria o Flask atrás de um servidor WSGI (por exemplo, Gunicorn) e possivelmente habilitaria HTTPS.

## Saída JSON esperada

Ao navegar para `http://localhost:5000/gridjs` com uma requisição GET, a resposta se parece com:

```json
{
  "columns": ["A", "B", "C"],
  "data": [
    ["Header1", "Header2", "Header3"],
    ["Row1Col1", "Row1Col2", "Row1Col3"],
    ["Row2Col1", "Row2Col2", "Row2Col3"]
  ],
  "settings": {
    "lazy_load": true
  }
}
```

GridJs consome esse payload automaticamente, renderizando uma tabela pesquisável e ordenável no navegador.

## Exemplo completo executável

Abaixo está o script completo que você pode copiar para `app.py` e executar:

```python
import cells
from flask import Flask, request, jsonify

# -------------------------------------------------
# 1. Load the Excel workbook
# -------------------------------------------------
workbook_path = "YOUR_DIRECTORY/sample.xlsx"
workbook = cells.Workbook(workbook_path)

# -------------------------------------------------
# 2. Create the GridJs handler
# -------------------------------------------------
grid_handler = cells.GridJsHandler(workbook)

# -------------------------------------------------
# 3. Enable lazy loading (optional but recommended)
# -------------------------------------------------
grid_handler.settings.lazy_load = True

# -------------------------------------------------
# 4. Initialize Flask
# -------------------------------------------------
app = Flask(__name__)

# -------------------------------------------------
# 5. Define the GridJs endpoint
# -------------------------------------------------
@app.route("/gridjs", methods=["GET", "POST"])
def gridjs():
    if request.method == "POST":
        # Apply client‑side edits
        grid_handler.apply_changes(request.json)
    # Return current view as JSON
    return jsonify(grid_handler.get_view())

# -------------------------------------------------
# 6. Run the server
# -------------------------------------------------
if __name__ == "__main__":
    app.run(port=5000, debug=False)
```

Execute o script com:

```bash
python app.py
```

Abra um navegador e aponte para uma página HTML simples que carrega o GridJs (veja a documentação do GridJs para a tag `<script>`). A grade exibirá o conteúdo do Excel instantaneamente.

## Variações comuns e casos de borda

| Situation | How to adapt |
|-----------|--------------|
| **Multiple worksheets** | Crie um `GridJsHandler` separado para cada planilha e exponha endpoints distintos (`/gridjs/sheet1`, `/gridjs/sheet2`). |
| **Large files (>10 MB)** | Aumente o limite de tamanho de requisição do Flask (`app.config['MAX_CONTENT_LENGTH']`) e mantenha `lazy_load` habilitado. |
| **Persisting edits back to the file** | Após `apply_changes`, chame `workbook.save("output.xlsx")` para gravar as alterações no disco. |
| **Authentication** | Envolva o endpoint com Flask‑Login ou uma verificação de token de API antes de retornar os dados. |
| **CORS for external front‑ends** | Adicione `from flask_cors import CORS; CORS(app)` para permitir requisições cross‑origin. |

Essas ajustes permitem escalar o processo **load excel workbook** para cargas de trabalho de produção.

## Dicas profissionais

- **Cache the JSON view** se o workbook raramente mudar; use `functools.lru_cache` em torno de `grid_handler.get_view()` para reduzir a sobrecarga de serialização.  
- **Validate incoming edits** (`request.json`) para impedir que dados malformados corrompam o workbook.  
- Ao servir via HTTPS, configure `app.run(ssl_context=('cert.pem', 'key.pem'))` para criptografar o tráfego.

## Conclusão

Agora você sabe **how to serve excel** arquivos usando Flask e GridJs, desde o carregamento do workbook até a devolução de uma visualização JSON que o navegador pode renderizar. O exemplo cobre todo o ciclo de vida: **load excel workbook**, habilitar lazy loading, expor um endpoint REST e executar um servidor pronto para produção.

Em seguida, explore tópicos relacionados como **display excel web** em um front‑end React, ou estenda o manipulador para **load excel workbook** a partir de armazenamento em nuvem (por exemplo, AWS S3). Experimente estilizar colunas do GridJs, adicionar paginação ou persistir edições de usuários de volta à planilha original.

Feliz codificação, e aproveite transformar arquivos Excel estáticos em tabelas web interativas!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como carregar e modificar arquivos Excel usando Aspose.Cells para .NET: Um guia abrangente](/cells/english/net/workbook-operations/load-modify-excel-aspose-cells-net/)
- [Como criar e exportar Excel para HTML usando Aspose.Cells Java | Guia de Operações de Workbook](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}