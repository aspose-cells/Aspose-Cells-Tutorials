---
category: general
date: 2026-07-14
description: Crie código Python que gera uma planilha Excel, define a cor de fundo
  das células, destaca células com base em intervalo de datas e salva a planilha como
  XLSX em minutos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- save workbook as xlsx
- highlight cells based on date range
- conditional formatting based on date
language: pt
lastmod: 2026-07-14
og_description: Crie uma pasta de trabalho Excel com Python instantaneamente. Aprenda
  a definir a cor de fundo das células, destacar células com base em intervalo de
  datas e salvar a pasta de trabalho como XLSX com Aspose.Cells.
og_image_alt: Screenshot showing an Excel sheet created with Python highlighting yesterday's
  dates
og_title: Criar Pasta de Trabalho do Excel em Python – Formatação Condicional Passo
  a Passo
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Create Excel workbook Python code that sets cell background color,
    highlights cells based on date range, and saves workbook as XLSX in minutes.
  headline: Create Excel Workbook Python – Full Guide with Conditional Formatting
  type: TechArticle
tags:
- Python
- Aspose.Cells
- Excel Automation
- Conditional Formatting
title: Criar Pasta de Trabalho Excel em Python – Guia Completo com Formatação Condicional
url: /pt/python/formatting/create-excel-workbook-python-full-guide-with-conditional-for/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel Workbook Python – Guia Completo com Formatação Condicional

Já se perguntou como criar scripts **create excel workbook python** que pareçam polidos sem abrir o Excel manualmente? Você não está sozinho. Em muitos projetos orientados a dados, precisamos gerar planilhas, colorir células e até marcar datas que caem dentro de um intervalo específico — tudo a partir de código Python puro.

Neste tutorial, percorreremos um exemplo completo e pronto‑para‑executar que **creates an Excel workbook python** usando a biblioteca Aspose.Cells, **sets cell background color**, aplica **conditional formatting based on date** e, finalmente, **saves workbook as xlsx**. Ao final, você terá um trecho reutilizável que pode inserir em qualquer pipeline de automação.

## O que você aprenderá

- Como inicializar um workbook e obter a primeira worksheet.  
- Uma função auxiliar que adiciona uma coleção de formatação condicional para qualquer intervalo de células.  
- Usando **conditional formatting based on date** para destacar as entradas de ontem.  
- Ajustando a largura das colunas para um layout organizado.  
- Persistindo o resultado com **save workbook as xlsx**.  

Nenhuma instalação externa do Excel é necessária — Aspose.Cells lida com tudo na memória.

## Pré-requisitos

- Python 3.8+ instalado.  
- `aspose-cells` package (`pip install aspose-cells`).  
- Familiaridade básica com funções Python e objetos datetime.  

Se você nunca usou o Aspose.Cells antes, pense nele como uma poderosa API pure‑Python que imita o modelo de objetos do Excel. É perfeito para geração no lado do servidor onde a suíte Office não está disponível.

## Etapa 1: Inicializar a Workbook (Create Excel Workbook Python)

Primeiro de tudo: precisamos **create excel workbook python** no estilo. Esta etapa cria um objeto workbook vazio e nos aponta para a worksheet padrão.

```python
# Step 1 – create a fresh workbook and get the first sheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, Color, SaveFormat
from datetime import datetime

workbook = Workbook()                     # <-- creates a new Excel file in memory
worksheet = workbook.worksheets[0]        # the default (first) sheet
```

> **Por que isso importa:** A classe `Workbook` é o ponto de entrada para toda operação do Excel. Ao criá‑la programaticamente evitamos qualquer manipulação manual de arquivos.

## Etapa 2: Auxiliar para Adicionar uma Coleção de Formatação Condicional (Set Cell Background Color)

A formatação condicional reside dentro de uma *coleção* anexada a um intervalo. Vamos envolver esse código repetitivo em um pequeno auxiliar que também nos permite **set cell background color** para todo o intervalo.

```python
def add_time_period_condition(cell_range: str, highlight_color: Color):
    """
    Adds a conditional‑formatting collection to `cell_range` and
    applies `highlight_color` as the base fill.
    """
    worksheet.conditional_formattings.add(cell_range)   # attach to the range
    cf = worksheet.conditional_formattings[-1]           # grab the newly added collection
    cf.style.background_color = highlight_color
    cf.style.pattern = BackgroundType.SOLID
    return cf
```

> **Dica profissional:** Usar um auxiliar mantém seu fluxo principal limpo e facilita reutilizar a mesma lógica para múltiplos intervalos.

## Etapa 3: Aplicar Formatação Condicional Baseada em Data (Highlight Cells Based on Date Range)

Agora vamos realmente **highlight cells based by date range**. O exemplo foca em “yesterday”, mas você pode trocar `TimePeriodType.YESTERDAY` por `TODAY`, `LAST_WEEK`, etc.

```python
# Step 3 – create a TIME_PERIOD rule for I19:K20 (yesterday)
cf = add_time_period_condition("I19:K20", Color.medium_sea_green)

condition_index = cf.add_condition(FormatConditionType.TIME_PERIOD)
condition = cf[condition_index]

# Define the visual style for the matching cells
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# The actual rule: any cell whose date is yesterday gets the pink fill
condition.time_period = TimePeriodType.YESTERDAY
```

> **O que está acontecendo?**  
> 1. Primeiro damos ao intervalo inteiro um fundo verde neutro.  
> 2. Em seguida, adicionamos uma condição `TIME_PERIOD` que sobrescreve o preenchimento com rosa **apenas** quando a data da célula for igual a ontem.  
> 3. O enum `TimePeriodType` abstrai o cálculo da data, então você não precisa escrever lógica personalizada.

## Etapa 4: Preencher Datas de Exemplo (Para que a Regra Seja Avaliada)

Para ver a regra em ação, inseriremos algumas datas na planilha. Uma cai dentro da janela de “yesterday”, a outra não.

```python
# Populate I19 with a date that is yesterday (relative to the hard‑coded date)
date_cell = worksheet.cells.get("I19")
date_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008
date_style = date_cell.get_style()
date_style.number = 30                     # Excel’s built‑in date format
date_cell.set_style(date_style)

# Populate K20 with a date that is NOT yesterday
date_cell = worksheet.cells.get("K20")
date_cell.put_value(datetime(2008, 8, 3))    # 03‑Aug‑2008
date_style = date_cell.get_style()
date_style.number = 30
date_cell.set_style(date_style)

# Add a label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

> **Nota de caso extremo:** Se sua workbook for aberta em diferentes localidades, considere usar `date_style.custom = "dd‑mm‑yyyy"` para impor uma exibição consistente.

## Etapa 5: Organizar o Layout (Auto‑Fit Columns)

Uma planilha apertada parece pouco profissional. Vamos **adjust column width for a tidy output**.

```python
# Auto‑fit column L (index 12) to show the full content without truncation
worksheet.auto_fit_column(12)
```

> **Por que auto‑fit?** Garante que quaisquer rótulos ou datas longas sejam totalmente visíveis, o que é especialmente importante ao compartilhar o arquivo com partes interessadas não técnicas.

## Etapa 6: Salvar a Workbook (Save Workbook As XLSX)

Finalmente, nós **save workbook as xlsx** para um local de sua escolha. A constante `SaveFormat.XLSX` indica ao Aspose.Cells que escreva no formato OpenXML moderno.

```python
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Resultado que você deve ver:**  
> - As células I19 e K20 contêm datas.  
> - I19 (yesterday) está destacada em rosa, enquanto K20 permanece verde.  
> - A coluna L expande automaticamente para caber o rótulo “Yesterday”.  

Se você abrir `TimePeriodDemo.xlsx` no Excel, a formatação condicional já estará aplicada — sem etapas extras necessárias.

![Planilha Excel mostrando data de ontem destacada](https://example.com/images/excel-demo.png "Captura de tela do arquivo Excel gerado com células destacadas")

*A imagem acima ilustra a workbook final; observe o destaque rosa na célula que contém a data de ontem.*

## Recapitulação: O que Conquistamos

- **Created an Excel workbook python** do zero usando Aspose.Cells.  
- **Set cell background color** para todo o intervalo para dar à planilha um indicativo visual.  
- Aplicou **conditional formatting based on date** para marcar automaticamente as entradas de ontem.  
- **Saved workbook as xlsx**, pronto para distribuição ou processamento adicional.  

Tudo isso foi feito em menos de 60 linhas de Python, e o código funciona em qualquer plataforma que suporte o runtime do Aspose.Cells.

## Próximos Passos e Tópicos Relacionados

Se você achou isso útil, talvez queira explorar também:

- **set cell background color** para linhas inteiras com base em valores de status (ex.: “Completed”, “Pending”).  
- Usando **highlight cells based on date range** para criar janelas móveis (últimos 7 dias, mês corrente).  
- Exportando para outros formatos como **CSV** ou **PDF** com `SaveFormat.CSV` ou `SaveFormat.PDF`.  
- Adicionando **charts** programaticamente para visualizar os dados que você acabou de formatar.  

Sinta-se à vontade para ajustar a lógica de datas, trocar a paleta de cores ou expandir o intervalo para cobrir colunas inteiras. O padrão permanece o mesmo: criar uma workbook, anexar uma coleção de formatação condicional, definir a regra e salvar.

Tem perguntas sobre um caso de uso específico? Deixe um comentário abaixo, e feliz codificação!

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Automação Excel com Aspose.Cells .NET: Criar Workbook & Definir Links Externos](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Criar e Salvar Workbook Excel Aspose Cells Java](/cells/hongkong/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Criar e Salvar Workbook Excel Aspose Cells Dotnet](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}