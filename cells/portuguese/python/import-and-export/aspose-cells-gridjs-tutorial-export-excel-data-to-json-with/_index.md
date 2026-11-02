---
category: general
date: 2026-07-03
description: Tutorial do Aspose Cells GridJs mostrando como exportar dados do Excel
  para JSON e exportar a planilha para JSON de forma eficiente usando carregamento
  preguiçoso.
draft: false
keywords:
- aspose cells gridjs tutorial
- export excel data json
- export worksheet to json
language: pt
og_description: O tutorial Aspose Cells GridJs explica como exportar dados do Excel
  para JSON e exportar a planilha para JSON com carregamento preguiçoso para planilhas
  grandes.
og_title: Tutorial Aspose Cells GridJs – Exportar dados do Excel para JSON
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
title: Tutorial Aspose Cells GridJs – Exportar dados do Excel para JSON com carregamento
  preguiçoso
url: /pt/python/import-and-export/aspose-cells-gridjs-tutorial-export-excel-data-to-json-with/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tutorial Aspose Cells GridJs – Exportar dados do Excel em JSON com carregamento preguiçoso

Já se perguntou como **exportar dados do Excel em JSON** de uma planilha enorme sem travar o navegador? Neste tutorial Aspose Cells GridJs vamos percorrer uma solução completa, pronta‑para‑executar que permite **exportar a planilha para JSON** usando carregamento preguiçoso, de modo que apenas as linhas necessárias sejam buscadas sob demanda.

Se você tem lutado com arquivos `.xlsx` gigantes e o lado do cliente continua travando, não está sozinho. A boa notícia? A abordagem que apresentamos aqui é leve e escalável, e você pode inseri‑la em qualquer projeto Python que já use a biblioteca Aspose.Cells.

## O que este guia cobre

1. Carregar uma grande pasta de trabalho com Aspose.Cells.
2. Ativar o carregamento preguiçoso do GridJs para que o servidor transmita linhas em blocos.
3. Exportar a configuração do GridJs para um arquivo JSON que o front‑end possa consumir.
4. Ajustar o tamanho do bloco para desempenho ideal.
5. Verificar a saída e integrá‑la com uma página HTML simples.

Sem serviços externos, sem mágica oculta — apenas Python puro e a API Aspose.Cells. Ao final, você terá um pipeline **completo de exportação de planilha para JSON** que pode adaptar a dashboards, ferramentas de relatório ou qualquer componente de grade de dados.

### Pré‑requisitos

- Python 3.8+ instalado localmente.
- `asposecells` package (você pode `pip install aspose-cells`).
- Um arquivo Excel de tamanho considerável (por exemplo, `large-data.xlsx`) colocado em um diretório conhecido.
- Familiaridade básica com Python e conceitos de desenvolvimento web.

Se algum desses itens lhe for desconhecido, não entre em pânico — cada passo inclui uma breve explicação “por quê”, para que você entenda o raciocínio por trás do código.

---

## Etapa 1: Instalar e importar Aspose.Cells

Primeiro de tudo, precisamos da biblioteca Aspose.Cells. É um produto comercial, mas uma avaliação gratuita funciona para desenvolvimento.

```bash
pip install aspose-cells
```

Agora importe as classes necessárias no seu script.

```python
# Step 1: Import the Aspose.Cells workbook class
import asposecells
from asposecells import Workbook
```

> **Por que isso importa:** Importar `Workbook` dá acesso ao motor de alto desempenho que lê arquivos Excel diretamente na memória, contornando a abordagem mais lenta do `openpyxl`.

## Etapa 2: Carregar a pasta de trabalho que contém o grande conjunto de dados

Com a biblioteca pronta, aponte-a para o seu arquivo Excel. O caminho pode ser absoluto ou relativo; apenas certifique‑se de que o arquivo exista.

```python
# Step 2: Load the workbook that contains a large data set
workbook = Workbook("YOUR_DIRECTORY/large-data.xlsx")
```

> **Dica profissional:** Se sua pasta de trabalho for maior que algumas centenas de megabytes, considere aumentar o limite de memória do processo Python ou usar um interpretador 64‑bits para evitar `MemoryError`.

## Etapa 3: Habilitar o carregamento preguiçoso do GridJs

GridJs é o componente de grade JavaScript da Aspose. O carregamento preguiçoso instrui o servidor a enviar apenas um subconjunto de linhas — perfeito para planilhas enormes.

```python
# Step 3: Enable lazy loading so the client fetches rows on demand
grid_options = workbook.Worksheets[0].Cells.GridJsOptions
grid_options.LazyLoading = True                 # fetch rows/columns only when needed
grid_options.LazyLoadingChunkSize = 500         # rows per server request
```

> **Por que carregamento preguiçoso?** Sem ele, toda a planilha seria serializada em JSON de uma só vez, o que pode facilmente exceder os limites de memória do navegador. Definindo `LazyLoadingChunkSize` para 500, cada requisição transporta uma carga útil manejável.

## Etapa 4: Exportar a configuração do GridJs para JSON

Agora pedimos à Aspose que produza o JSON que o componente GridJs do front‑end espera. Este é o núcleo da operação de **exportar dados do Excel em JSON**.

```python
# Step 4: Export the GridJs configuration to a JSON file for the client side
grid_json = workbook.Worksheets[0].Cells.ExportGridJsJson()
```

O método `ExportGridJsJson` retorna um objeto `bytes` contendo a representação JSON da planilha, pronto para ser salvo ou transmitido.

## Etapa 5: Gravar o JSON em um arquivo (ou transmiti‑lo)

Para um teste rápido, grave o JSON no disco. Em uma API de produção, você o retornaria diretamente de um endpoint Flask/Django.

```python
# Step 5: Persist the JSON to a file
output_path = "YOUR_DIRECTORY/lazygrid.json"
with open(output_path, "wb") as f:
    f.write(grid_json)

print(f"✅ GridJs JSON exported successfully to {output_path}")
```

> **O que você verá:** Abrir `lazygrid.json` revela uma estrutura com `columns`, `rows` e metadados de paginação. O array `rows` estará inicialmente vazio; o GridJs solicitará o primeiro bloco quando a página for carregada.

## Etapa 6: Conectar o JSON a uma página HTML simples (opcional)

Se quiser ver a grade em ação, crie um pequeno arquivo HTML que carregue o GridJs de um CDN e aponte‑o para o JSON gerado.

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

> **Por que incluir isso?** Demonstra o ciclo completo: Python cria o JSON, o navegador o obtém, e o GridJs renderiza os dados bloco a bloco. Agora você pode experimentar diferentes valores de `LazyLoadingChunkSize` para encontrar o ponto ideal para sua rede.

## Etapa 7: Verificar e solucionar problemas

Execute o script Python:

```bash
python export_lazy_grid.py
```

Você deve ver a mensagem de sucesso e um arquivo `lazygrid.json`. Abra o arquivo HTML em um navegador; a grade deve exibir as primeiras 500 linhas instantaneamente, com controles de paginação para carregar mais.

Se a grade aparecer vazia:

- **Verifique o tamanho do arquivo JSON** – um arquivo de zero bytes geralmente indica que o caminho da pasta de trabalho está errado.
- **Confirme que o carregamento preguiçoso está habilitado** – a flag `LazyLoading` deve ser `True`.
- **Inspecione o console do navegador** – quaisquer erros CORS ou 404 indicam que o JSON não está sendo servido corretamente.

---

## Variações comuns e casos de borda

### Exportando uma planilha específica

O exemplo acima sempre usa a primeira planilha (`Worksheets[0]`). Para exportar outra planilha, basta mudar o índice ou usar o nome da planilha:

```python
sheet = workbook.Worksheets["DataSheet"]   # by name
grid_options = sheet.Cells.GridJsOptions
grid_json = sheet.Cells.ExportGridJsJson()
```

### Alterando o tamanho do bloco para arquivos massivos

Para arquivos com milhões de linhas, um tamanho de bloco de 500 ainda pode ser pequeno, causando muitas idas‑e‑voltas. Você pode aumentá‑lo para 2000 ou mais, mas lembre‑se de que blocos maiores consomem mais largura de banda por requisição.

```python
grid_options.LazyLoadingChunkSize = 2000
```

### Exportando para um stream em vez de um arquivo

Se sua API retorna o JSON diretamente, você não precisa gravá‑lo no disco:

```python
from flask import Flask, Response
app = Flask(__name__)

@app.route("/api/gridjson")
def gridjson():
    json_bytes = workbook.Worksheets[0].Cells.ExportGridJsJson()
    return Response(json_bytes, mimetype="application/json")
```

### Lidando com fórmulas e formatação

Por padrão, `ExportGridJsJson` inclui os valores calculados das fórmulas. Se precisar das fórmulas brutas, defina:

```python
grid_options.ExportFormulas = True
```

## Conclusão

Neste **tutorial Aspose Cells GridJs** cobrimos tudo o que você precisa para **exportar dados do Excel em JSON** e **exportar planilha para JSON** com carregamento preguiçoso. Desde a instalação do Aspose.Cells, habilitação do carregamento preguiçoso, geração do JSON, até a integração com uma página HTML simples, agora você tem um padrão full‑stack que escala elegantemente com planilhas massivas.

Experimente — ajuste o tamanho do bloco, aponte para diferentes planilhas ou integre o endpoint em um app Flask ou Django. As possibilidades são infinitas, e os ganhos de desempenho são imediatos.

Pronto para o próximo passo? Tente adicionar ordenação de colunas, renderizadores de célula personalizados ou até filtragem no lado do servidor para tornar sua grade GridJs realmente interativa. Se encontrar algum problema, deixe um comentário abaixo; feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Importar Dados JSON para Excel Usando Aspose.Cells Java: Um Guia Abrangente](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Carregar CSV e Exportar para JSON Usando Aspose.Cells para .NET: Um Guia Abrangente](/cells/english/net/import-export/load-csv-export-json-aspose-cells-dotnet/)
- [Exportar Dados do Excel Usando Aspose.Cells .NET: Um Guia Completo para Exportação de Dados Sem Falhas](/cells/english/net/import-export/export-excel-data-aspose-cells-net-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}