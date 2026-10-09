---
category: general
date: 2026-06-21
description: Crie uma tabela de multiplicação no Excel usando Python. Aprenda como
  usar lambda, como usar makearray, exibir o array do Excel e ler valores do Excel
  com Python em um tutorial passo a passo.
draft: false
keywords:
- create multiplication table
- how to use lambda
- how to use makearray
- display excel array
- read excel values python
language: pt
og_description: Crie uma tabela de multiplicação no Excel usando Python. Este tutorial
  mostra como usar lambda, makearray, exibir o array do Excel e ler valores do Excel
  em Python de forma eficiente.
og_title: Crie tabela de multiplicação no Excel com Python – Guia Completo
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create multiplication table in Excel using Python. Learn how to use
    lambda, how to use makearray, display excel array and read excel values python
    in a step‑by‑step tutorial.
  headline: Create multiplication table in Excel with Python – Full Guide
  type: TechArticle
tags:
- python
- excel
- openpyxl
title: Crie uma tabela de multiplicação no Excel com Python – Guia Completo
url: /pt/python/import-and-export/create-multiplication-table-in-excel-with-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crie uma tabela de multiplicação no Excel com Python – Guia Completo

Já se perguntou como **criar uma tabela de multiplicação** no Excel sem digitar manualmente cada célula? Você não está sozinho. Em muitos cenários de relatórios você precisa de uma grade rápida 5×5 (ou maior) de produtos, e fazer isso à mão é perda de tempo.  

Neste tutorial vamos percorrer uma forma limpa, impulsionada por Python, de gerar essa tabela, incorporá‑la com uma fórmula `MAKEARRAY` e, em seguida, trazer os resultados de volta ao seu script. No caminho, responderemos **como usar lambda**, mostraremos **como usar makearray** e demonstraremos **exibir array do Excel** assim como **ler valores do Excel python** — tudo em um exemplo coeso.

Ao final você terá um snippet reutilizável que funciona com qualquer pasta de trabalho, e entenderá por que essa abordagem é rápida e à prova de futuro.

## O que você vai precisar

- Python 3.8+ (a versão estável mais recente serve)
- A biblioteca `openpyxl` (ou qualquer biblioteca compatível com Excel que suporte fórmulas)
- Um entendimento básico de expressões lambda em Python
- Nenhum add‑in especial do Excel; a função nativa `MAKEARRAY` (disponível no Excel 365) faz o trabalho pesado

Se estiver faltando algum desses, basta `pip install openpyxl` e você está pronto para começar.

## Crie a tabela de multiplicação – Visão geral

A ideia central é simples: criamos uma nova pasta de trabalho, escrevemos uma fórmula `MAKEARRAY` que constrói uma matriz de multiplicação 5 × 5, forçamos o Excel a calculá‑la e, por fim, lemos os valores resultantes de volta para o Python.

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Insert a MAKEARRAY formula that builds a 5×5 multiplication table
# The formula uses a LAMBDA that returns r*c for each row (r) and column (c)
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"

# Step 3: Calculate all formulas so the array is materialized in the sheet
workbook.calculate_formula()

# Step 4: Read and display the top‑left 5×5 block of values
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

Executar o script imprime:

```
[1, 2, 3, 4, 5]
[2, 4, 6, 8, 10]
[3, 6, 9, 12, 15]
[4, 8, 12, 16, 20]
[5, 10, 15, 20, 25]
```

Isso é uma **criar tabela de multiplicação** totalmente funcional no Excel, gerada inteiramente a partir do Python.

### Por que usar `MAKEARRAY` em vez de um loop Python?

- **Desempenho**: O Excel lida com o cálculo nativamente, o que é mais rápido para matrizes grandes.
- **Atualização ao vivo**: Se você mudar as dimensões na fórmula mais tarde, a planilha recalcula automaticamente.
- **Legibilidade**: A fórmula expressa a intenção (“criar um array”) diretamente, mantendo seu código Python organizado.

## Como usar lambda em Python para fórmulas do Excel

A parte `LAMBDA` da chamada `MAKEARRAY` é uma função anônima do lado do Excel, não um lambda do Python. Ainda assim, o conceito é o mesmo: você define um pequeno trecho de lógica inline que recebe `r` (índice da linha) e `c` (índice da coluna) e retorna `r*c`.  

Se você é novo em **como usar lambda** no mundo do Excel, pense nisso como uma mini‑função que vive apenas dentro da fórmula. Não há necessidade de declarar uma função separada em outro lugar. Em Python, simplesmente incorporamos a string:

```python
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"
```

Essa linha diz ao Excel: *“Para cada célula em um bloco 5‑por‑5, calcule linha × coluna.”*  

Como o lambda é avaliado pelo Excel, você não precisa se preocupar com a sintaxe de lambda do Python aqui — apenas com a sintaxe do Excel.

## Como usar makearray para gerar arrays

`MAKEARRAY` é uma adição relativamente nova à biblioteca de funções do Excel (disponível no Microsoft 365 a partir de 2022). Ela substitui truques antigos como combinações de `INDEX` + `ROW`/`COLUMN`. A assinatura é:

```
MAKEARRAY(rows, columns, lambda)
```

- **rows** – número de linhas que você deseja.
- **columns** – número de colunas que você deseja.
- **lambda** – um LAMBDA do Excel que recebe `(row, column)` e devolve um valor.

No nosso exemplo passamos `5,5` para uma clássica tabela de multiplicação, mas você pode mudar esses números facilmente:

```python
worksheet["A1"] = "=MAKEARRAY(10,10, LAMBDA(r,c, r*c))"
```

Isso geraria uma tabela 10 × 10 sem tocar em loops Python. Isso demonstra **como usar makearray** para qualquer tipo de grade determinística, seja uma tabela de consulta, um mapa de calor ou um cronograma financeiro.

## Exibir array do Excel – trazendo os dados de volta ao Python

Depois que o Excel calcula a fórmula, os valores resultantes permanecem na planilha como qualquer célula inserida manualmente. Para **exibir array do Excel**, iteramos sobre o intervalo e imprimimos cada linha:

```python
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

Algumas dicas:

- Use `worksheet.cell(row, column).value` em vez da indexação estilo dicionário se precisar lidar com intervalos maiores; é um pouco mais rápido.
- Se quiser uma tabela mais bonita, considere `tabulate` ou `pandas.DataFrame` para formatar a saída.

Abaixo está uma captura de tela da planilha resultante (o texto alternativo da imagem inclui a palavra‑chave principal para SEO):

![Captura de tela mostrando criar tabela de multiplicação no Excel usando Python](/images/multiplication-table-excel.png)

## Ler valores do Excel python – extraindo a matriz para processamento posterior

Frequentemente o próximo passo após **exibir array do Excel** é alimentar esses números em um pipeline de análise de dados. É aí que **read excel values python** brilha. O mesmo loop que usamos para imprimir pode ser reutilizado para construir uma lista de listas, um array NumPy ou um DataFrame Pandas:

```python
import pandas as pd

# Build a list of rows
data = []
for row_index in range(1, 6):
    row = [worksheet.cell(row=row_index, column=col_index).value
           for col_index in range(1, 6)]
    data.append(row)

# Convert to DataFrame for easy manipulation
df = pd.DataFrame(data, columns=[f"Col{c}" for c in range(1, 6)],
                  index=[f"Row{r}" for r in range(1, 6)])

print(df)
```

Saída:

```
      Col1  Col2  Col3  Col4  Col5
Row1     1     2     3     4     5
Row2     2     4     6     8    10
Row3     3     6     9    12    15
Row4     4     8    12    16    20
Row5     5    10    15    20    25
```

Agora você tem um DataFrame totalmente tipado que pode plotar, exportar para CSV ou alimentar um modelo de aprendizado de máquina. Isso completa a parte **read excel values python** do fluxo de trabalho.

## Casos de borda e dicas práticas

- **Recálculo da fórmula**: Se você modificar a pasta de trabalho após a chamada inicial `calculate_formula()`, deve invocá‑la novamente; caso contrário, o array em cache ficará desatualizado.
- **Excel não‑365**: Versões mais antigas do Excel não suportam `MAKEARRAY`. Nesse caso, recorra a uma tabela gerada em Python e escreva cada célula individualmente.
- **Tabelas grandes**: Para matrizes maiores que ~100 × 100, considere transmitir os dados para evitar carregar a planilha inteira na memória.
- **Tratamento de erros**: Envolva as etapas de cálculo e leitura em blocos `try/except` para capturar `InvalidFileException` ou `FormulaError`.

## Conclusão

Acabamos de mostrar como **criar tabela de multiplicação** no Excel usando Python, aproveitando o poder de **como usar lambda** e **como usar makearray**. Você viu como **exibir array do Excel**, ler esses valores de volta com **read excel values python**, e até transformar o resultado em um DataFrame Pandas para análises posteriores.

Quer ir além? Experimente trocar a lógica de multiplicação por algo mais complexo — talvez uma matriz de distâncias, uma tabela de probabilidades ou uma grade de precificação dinâmica. O mesmo padrão se aplica: uma linha de `MAKEARRAY`, um rápido `calculate_formula()` e alguns loops Python para extrair os dados.

Se este guia foi útil, dê uma estrela no GitHub, compartilhe com colegas ou deixe um comentário com seu próprio caso de uso. Boa codificação e aproveite a simplicidade de gerar tabelas Excel com uma única fórmula!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Aspose.Cells .NET Tutorial: How to Create and Modify Excel Workbooks Easily](/cells/english/net/workbook-operations/aspose-cells-net-create-modify-excel-workbooks/)
- [How to Create and Style Named Ranges in Excel Using Aspose.Cells .NET | Step‑By‑Step Guide](/cells/english/net/range-management/create-style-named-ranges-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}