---
category: general
date: 2026-06-21
description: Criar tutorial em Python para planilha Excel mostrando como usar a função
  MAP e lambda para converter Celsius em Fahrenheit rapidamente.
draft: false
keywords:
- create excel workbook python
- convert celsius to fahrenheit
- use map function
- how to use map
- how to use lambda
language: pt
og_description: Crie uma planilha Excel em Python e aprenda a usar a função MAP com
  lambda para converter Celsius em Fahrenheit em minutos.
og_title: Criar Pasta de Trabalho Excel em Python – Guia Passo a Passo
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create Excel workbook Python tutorial showing how to use MAP function
    and lambda to convert Celsius to Fahrenheit quickly.
  headline: Create Excel Workbook Python – Full Guide
  type: TechArticle
- description: Create Excel workbook Python tutorial showing how to use MAP function
    and lambda to convert Celsius to Fahrenheit quickly.
  name: Create Excel Workbook Python – Full Guide
  steps:
  - name: '**How to use map** for multi‑column transformations, e.g., converting temperatures
      and rounding in one go.'
    text: '**How to use map** for multi‑column transformations, e.g., converting temperatures
      and rounding in one go.'
  - name: '**How to use lambda** to embed conditional logic: `LAMBDA(c, IF(c<0, "below
      freezing", c*9/5+32))`.'
    text: '**How to use lambda** to embed conditional logic: `LAMBDA(c, IF(c<0, "below
      freezing", c*9/5+32))`.'
  - name: 'Saving the workbook to disk: `wb.save("temperatures.xlsx")`.'
    text: 'Saving the workbook to disk: `wb.save("temperatures.xlsx")`.'
  - name: Adding styling (fonts, borders) via Aspose’s rich formatting API.
    text: Adding styling (fonts, borders) via Aspose’s rich formatting API.
  - name: Initialize a workbook.
    text: Initialize a workbook.
  - name: Write raw data.
    text: Write raw data.
  - name: Apply a MAP‑based formula.
    text: Apply a MAP‑based formula.
  - name: Force calculation.
    text: Force calculation.
  - name: Pull the results back into Python.
    text: Pull the results back into Python.
  type: HowTo
- questions:
  - answer: Just extend the range in the `put_value` call and adjust the list comprehension
      range accordingly. The MAP formula will automatically expand if you reference
      a larger range.
    question: What if I have more than four rows?
  - answer: Absolutely. Replace the lambda body with any arithmetic you need, e.g.,
      `LAMBDA(c, c*2)` for a simple doubling operation.
    question: Can I use MAP with other conversions?
  - answer: The library offers a free evaluation mode, but for production use you’ll
      want a proper license to avoid watermarks.
    question: Do I need a license for Aspose.Cells?
  - answer: No, MAP is part of the dynamic array functions introduced in Excel 365.
      If you target legacy Excel, you’d fall back to traditional copy‑down formulas.
    question: Is the MAP function available in older Excel versions?
  type: FAQPage
tags:
- python
- excel
- aspose-cells
- data conversion
title: Criar Pasta de Trabalho Excel em Python – Guia Completo
url: /pt/python/import-and-export/create-excel-workbook-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Pasta de Trabalho Excel Python – Guia Completo

Já se perguntou como **criar pasta de trabalho excel python**‑style sem abrir o Excel manualmente? Talvez você precise transformar uma lista de temperaturas em Celsius para valores em Fahrenheit em tempo real, e prefira não copiar‑colar fórmulas manualmente. Neste tutorial vamos resolver exatamente isso: você verá como gerar um arquivo Excel, inserir uma coluna de dados em Celsius e então **converter celsius para fahrenheit** com uma única fórmula elegante que usa a **função MAP** e um **lambda**.

Por que isso importa? Automatizar planilhas economiza tempo, reduz erros humanos e torna trivial integrar o Excel em pipelines de dados maiores. Além disso, com Aspose.Cells para Python você obtém todas as funcionalidades do Excel sem a pesada interoperação COM. Pronto? Vamos mergulhar.

## O que você vai precisar

- Python 3.9+ (qualquer versão recente serve)
- Pacote `aspose-cells` instalado (`pip install aspose-cells`)
- Noções básicas de listas e funções em Python
- Nenhuma experiência prévia com Excel é necessária; nós cuidaremos da criação da pasta de trabalho para você

Se você já marcou esses itens, está tudo pronto. Caso contrário, faça uma pausa para instalar a biblioteca — confie em mim, vale a pena.

![create excel workbook python example](excel_workbook.png)

*Texto alternativo da imagem: exemplo de criar pasta de trabalho excel python mostrando uma planilha preenchida*

## Etapa 1: Criar Pasta de Trabalho Excel em Python

A primeira coisa que devemos fazer é **criar pasta de trabalho excel python** usando Aspose.Cells. Pense na pasta de trabalho como um caderno novo onde cada planilha é uma página que você pode escrever.

```python
import aspose.cells as cells

# Initialize a new workbook – this is our blank Excel file
wb = cells.Workbook()

# Grab the first worksheet (index 0) to start populating data
ws = wb.worksheets[0]
```

*Por que isso importa*: Instanciar `Workbook()` fornece uma representação em memória de um arquivo `.xlsx`. Ainda não há I/O de disco, o que mantém tudo rápido.

## Etapa 2: Preencher a Coluna A com Temperaturas em Celsius

Agora que temos uma planilha, vamos colocar alguns valores em Celsius na coluna **A**. Usaremos o método `put_value`, que aceita uma lista Python e grava diretamente no intervalo de células.

```python
# Write a list of Celsius temperatures into cells A1:A4
ws.cells["A1:A4"].put_value([0, 20, 100, -10])
```

*Dica de especialista*: A string de intervalo `"A1:A4"` é flexível — se você expandir a lista depois, basta ajustar o intervalo ou usar um endereço dinâmico.

## Etapa 3: Aplicar MAP com um LAMBDA para Converter Cada Valor Celsius em Fahrenheit

É aqui que a mágica acontece. A **função MAP** (nova no Excel 365) permite aplicar um **lambda** a cada elemento de um array. No nosso caso, o array é `A1:A4`, e o lambda executa a clássica conversão `c * 9/5 + 32`.

```python
# Set the formula in B1 that maps each Celsius value to Fahrenheit
ws.cells["B1"].formula = "=MAP(A1:A4, LAMBDA(c, c*9/5 + 32))"
```

*Como funciona*:  
- `MAP(array, LAMBDA(parâmetro, expressão))` itera sobre `array`.  
- `c` é o placeholder para cada valor em Celsius.  
- A expressão `c*9/5 + 32` devolve o equivalente em Fahrenheit.

Se você é novo em **como usar map** no Excel, pense nisso como o `map()` embutido do Python, mas expresso como uma fórmula de planilha. Ele elimina a necessidade de arrastar fórmulas manualmente.

## Etapa 4: Calcular a Fórmula para que os Resultados Se Materializem

Aspose.Cells não avalia fórmulas automaticamente a menos que você o solicite. Chamar `calculate_formula()` força o motor a computar o resultado do MAP e armazenar os valores na coluna **B**.

```python
# Force calculation – this writes the computed Fahrenheit values into the cells
wb.calculate_formula()
```

*Caso extremo*: Se você modificar a coluna de Celsius depois, precisará executar `calculate_formula()` novamente, ou definir `calc_mode` da pasta de trabalho como automático.

## Etapa 5: Recuperar e Exibir os Valores em Fahrenheit da Coluna B

Por fim, vamos trazer os números calculados de volta ao Python e imprimi‑los. Isso demonstra **como usar lambda** programaticamente.

```python
# Extract the Fahrenheit values from B1:B4 into a Python list
fahrenheit = [ws.cells[f"B{i}"].value for i in range(1, 5)]
print(fahrenheit)
```

**Saída esperada**

```
[32.0, 68.0, 212.0, 14.0]
```

Se você vir esses números, parabéns — você criou **pasta de trabalho excel python**‑style, preencheu‑a e utilizou a **função map** junto com um **lambda** para **converter celsius para fahrenheit**.

## Perguntas Frequentes e Armadilhas

- **E se eu tiver mais de quatro linhas?**  
  Basta ampliar o intervalo na chamada `put_value` e ajustar o intervalo da list comprehension conforme necessário. A fórmula MAP será expandida automaticamente se você referenciar um intervalo maior.

- **Posso usar MAP com outras conversões?**  
  Absolutamente. Substitua o corpo do lambda por qualquer operação aritmética que precisar, por exemplo, `LAMBDA(c, c*2)` para dobrar o valor.

- **Preciso de licença para Aspose.Cells?**  
  A biblioteca oferece um modo de avaliação gratuito, mas para uso em produção você precisará de uma licença adequada para evitar marcas d’água.

- **A função MAP está disponível em versões antigas do Excel?**  
  Não, MAP faz parte das funções de array dinâmico introduzidas no Excel 365. Se você precisar suportar versões legadas, terá que recorrer a fórmulas tradicionais de cópia‑para‑baixo.

## Estendendo o Exemplo – Próximos Passos

Agora que o fluxo principal está claro, você pode experimentar:

1. **Como usar map** para transformações de múltiplas colunas, por exemplo, converter temperaturas e arredondar em um único passo.  
2. **Como usar lambda** para incorporar lógica condicional: `LAMBDA(c, IF(c<0, "below freezing", c*9/5+32))`.  
3. Salvar a pasta de trabalho no disco: `wb.save("temperatures.xlsx")`.  
4. Adicionar estilos (fontes, bordas) via API de formatação avançada da Aspose.  

Cada um desses itens se baseia na mesma fundação que acabamos de montar, mantendo o código conciso enquanto desbloqueia poderosas automações de planilhas.

## Conclusão

Percorremos todo o processo de **criar pasta de trabalho excel python** do zero, preenchendo‑a com dados em Celsius e então **convertendo celsius para fahrenheit** usando a **função MAP** e uma expressão **lambda**. Os passos foram:

1. Inicializar uma pasta de trabalho.  
2. Gravar os dados brutos.  
3. Aplicar uma fórmula baseada em MAP.  
4. Forçar o cálculo.  
5. Recuperar os resultados de volta ao Python.

Com essa receita no seu arsenal, automatizar pipelines de dados centrados no Excel torna‑se muito simples. Sinta‑se à vontade para ajustar o lambda, encadear múltiplas chamadas MAP ou até mesmo incorporar a pasta de trabalho em um serviço web. O céu é o limite.

Tem outra conversão em mente? Deixe um comentário e vamos explorar juntos. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}