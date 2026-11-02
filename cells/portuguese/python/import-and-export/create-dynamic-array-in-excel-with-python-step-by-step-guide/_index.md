---
category: general
date: 2026-06-21
description: Crie uma matriz dinâmica usando Python e a função SEQUENCE no Excel.
  Aprenda a ler o resultado da fórmula, recalcular fórmulas do Excel e veja um exemplo
  da função SEQUENCE no Excel.
draft: false
keywords:
- create dynamic array
- sequence function excel
- read formula result
- recalculate excel formulas
- excel sequence example
language: pt
og_description: Crie uma matriz dinâmica no Excel usando Python. Este tutorial mostra
  como usar a função SEQUENCE, recalcular fórmulas do Excel e ler o resultado da fórmula.
og_title: Crie uma Matriz Dinâmica no Excel com Python – Guia Completo
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create dynamic array using Python and the SEQUENCE function in Excel.
    Learn to read formula result, recalculate Excel formulas, and see an Excel SEQUENCE
    example.
  headline: Create Dynamic Array in Excel with Python – Step‑by‑Step Guide
  type: TechArticle
tags:
- excel
- python
- xlwings
- dynamic arrays
title: Crie uma Matriz Dinâmica no Excel com Python – Guia Passo a Passo
url: /pt/python/import-and-export/create-dynamic-array-in-excel-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crie Array Dinâmico no Excel com Python – Guia Completo

Já se perguntou como **criar fórmulas de array dinâmico** no Excel sem sair do seu script Python? Você não está sozinho. Seja automatizando um relatório mensal ou construindo um motor de dados leve, poder inserir uma fórmula `SEQUENCE` em uma planilha, recalcular e trazer o intervalo de spill de volta para o Python é revolucionário.

Neste tutorial vamos percorrer um **exemplo real de sequência no Excel**, mostrar como **ler o resultado da fórmula** e explicar a melhor forma de **recalcular fórmulas do Excel** depois de injetar nova lógica. Ao final, você terá um script autocontido que pode copiar‑colar, executar e adaptar às suas necessidades.

## O que você vai aprender

- Como a função `SEQUENCE` funciona e por que ela é perfeita para gerar matrizes.
- A diferença entre o valor de uma célula regular e o endereço de um intervalo de spill.
- Usar `wb.calculate_formula()` (ou equivalente) para forçar o Excel a avaliar novas fórmulas.
- Extrair o endereço de um array dinâmico com `ANCHORARRAY`.
- Um exemplo completo em Python que pode ser inserido em qualquer projeto.

Nenhuma experiência prévia com o novo motor de arrays dinâmicos do Excel é necessária — apenas familiaridade básica com Python e uma biblioteca como **xlwings** que consiga se comunicar com o Excel.

---

## Como criar um Array Dinâmico com SEQUENCE no Excel usando Python

O primeiro passo é escrever uma fórmula **array dinâmico** diretamente em uma célula da planilha. No Excel moderno, a função `SEQUENCE` pode gerar uma matriz de números instantaneamente. Aqui está a sintaxe que usaremos:

```python
# Step 1: Write a dynamic array formula that generates a 3×2 matrix starting at 10 with step 5
ws.cells["A1"].formula = "=SEQUENCE(3,2,10,5)"   # Returns a 3×2 array
```

**Por que `SEQUENCE`?**  
Pense nela como o `range()` embutido do Excel para planilhas. Ela permite especificar linhas, colunas, um valor inicial e um incremento — tudo em uma única linha organizada. No nosso caso pedimos 3 linhas e 2 colunas, começando em 10 e avançando de 5 em 5, o que gera:

|   | A | B |
|---|---|---|
|1|10|15|
|2|20|25|
|3|30|35|

Como a fórmula está em `A1`, o Excel automaticamente “spilha” o resultado nas células vizinhas `A1:B3`. Esse spill é o que recuperaremos mais adiante.

---

## Usando a Função SEQUENCE no Excel – Um Exemplo Rápido de Sequência

Se você abrir o Excel manualmente e digitar `=SEQUENCE(3,2,10,5)` em uma célula, verá a mesma matriz aparecer instantaneamente. A função faz parte do motor de **array dinâmico** do Excel introduzido no Office 365, o que significa:

- Não há necessidade de Ctrl+Shift+Enter.
- O resultado pode expandir ou contrair automaticamente.
- Você pode referenciar todo o intervalo de spill com funções como `@` ou `#`.

Em Python, a única diferença é que atribuímos a fórmula como uma string à propriedade `.formula` da célula. A biblioteca cuida do resto.

---

## Recuperando o Endereço do Intervalo de Spill com ANCHORARRAY

Depois que o array dinâmico está no lugar, muitas vezes você precisa saber onde o Excel realmente colocou os valores. É aí que `ANCHORARRAY` brilha. Ela devolve o endereço da célula superior‑esquerda do intervalo de spill — exatamente o que precisamos ler de volta no nosso script.

```python
# Step 2: Retrieve the address of the spill range produced by the formula in A1
ws.cells["C1"].formula = "=ANCHORARRAY(A1)"      # Returns the address of the spill range
```

Colocar essa fórmula em `C1` nos dá uma string de texto como `"A1:B3"`. Observe que estamos **lendo o resultado da fórmula** como um valor simples, não como outra fórmula. Esse pequeno truque evita a necessidade de analisar a planilha manualmente.

---

## Recalculando Fórmulas do Excel e Lendo o Resultado

O Excel nem sempre recalcula instantaneamente quando uma nova fórmula é injetada a partir de um script externo. Para garantir que a pasta de trabalho reflita as alterações mais recentes, acionamos explicitamente uma passagem de cálculo.

```python
# Step 3: Recalculate all formulas in the workbook and read the result
wb.calculate_formula()               # Forces Excel to evaluate pending formulas
print(ws.cells["C1"].value)          # → "A1:B3"
```

**Por que chamar `calculate_formula()`?**  
Se você pular esta etapa, `ws.cells["C1"].value` pode ainda retornar `None` ou um endereço antigo porque o Excel ainda está atualizando sua árvore de dependências. Forçando um recálculo, garantimos que o **resultado da fórmula lida** esteja atualizado.

---

## Script Completo – Do Início ao Fim

Abaixo está um exemplo completo, pronto‑para‑executar, que une tudo. Ele assume que você tem **xlwings** instalado (`pip install xlwings`) e que o Excel está disponível na sua máquina.

```python
import xlwings as xw

def create_dynamic_array_example():
    # Open a new workbook (or attach to an existing one)
    wb = xw.Book()               # Creates a fresh Excel workbook
    ws = wb.sheets[0]            # Grab the first worksheet

    # 1️⃣ Write the SEQUENCE formula – this creates a 3×2 matrix starting at 10, step 5
    ws.cells["A1"].formula = "=SEQUENCE(3,2,10,5)"

    # 2️⃣ Use ANCHORARRAY to capture the spill range address in C1
    ws.cells["C1"].formula = "=ANCHORARRAY(A1)"

    # 3️⃣ Force Excel to recalculate so that the ANCHORARRAY result is current
    wb.calculate_formula()

    # 4️⃣ Read back the address – this is our **read formula result** step
    spill_address = ws.cells["C1"].value
    print(f"The dynamic array spills into: {spill_address}")

    # 5️⃣ Optionally, fetch the actual values from the spill range
    # xlwings can read a range by address, so we demonstrate that too
    data = ws.range(spill_address).value
    print("Matrix values:")
    for row in data:
        print(row)

    # Clean up – close without saving to keep the demo tidy
    wb.close(save=False)

if __name__ == "__main__":
    create_dynamic_array_example()
```

### Saída Esperada

```
The dynamic array spills into: A1:B3
Matrix values:
[10, 15]
[20, 25]
[30, 35]
```

Executar o script abrirá o Excel, injetará a fórmula `SEQUENCE`, recalculará e então imprimirá tanto o endereço do spill quanto a própria matriz. Nenhum clique manual necessário.

---

## Armadilhas Comuns e Dicas Profissionais

- **Armadilha:** Esquecer de chamar `wb.calculate_formula()`.  
  *Resultado:* `C1` fica em branco ou mostra um endereço desatualizado.  
  *Correção:* Sempre acione um cálculo após escrever novas fórmulas.

- **Armadilha:** Usar uma versão mais antiga do Excel que não possui a função `SEQUENCE`.  
  *Resultado:* erro `#NAME?`.  
  *Correção:* Certifique‑se de que você tem Office 365 ou Excel 2021+.

- **Dica profissional:** Se precisar do intervalo de spill para processamento adicional (ex.: criação de gráficos), pode passar o endereço diretamente para `ws.range(spill_address)` como mostrado acima.

- **Dica profissional:** `ANCHORARRAY` funciona com qualquer array dinâmico, não apenas com `SEQUENCE`. Substitua por `=SORT(A2:A10)` ou `=FILTER(...)` e você ainda obterá o endereço correto do spill.

- **Caso extremo:** Quando a área de destino já está ocupada, o Excel retornará o erro `#SPILL!`. Nesse caso, limpe o intervalo de destino primeiro ou mova a fórmula para outra célula.

---

## Expandindo o Exemplo – O que vem a seguir?

Agora que você sabe como **criar fórmulas de array dinâmico**, **ler o resultado da fórmula** e **recalcular fórmulas do Excel**, pode explorar cenários mais avançados:

- **Dados dinâmicos para gráficos** – alimente um intervalo de spill como fonte de um gráfico e deixe o gráfico crescer automaticamente.
- **Formatação condicional** – aplique regras ao intervalo de spill usando seu endereço.
- **Referências entre pastas de trabalho** – escreva um array dinâmico em uma pasta e puxe os dados para outra via links do `xlwings`.

Cada um desses itens se baseia nos conceitos centrais abordados aqui, então sinta‑se à vontade para experimentar. O único limite é sua imaginação (e talvez o número máximo de linhas/colunas do Excel).

---

## Conclusão

Acabamos de percorrer um fluxo de trabalho completo para **criar fórmulas de array dinâmico** no Excel a partir do Python, usar a **função SEQUENCE**, recuperar o intervalo de spill com **ANCHORARRAY**, **recalcular fórmulas do Excel** e, finalmente, **ler o resultado da fórmula** de volta ao seu script. O exemplo curto demonstra o quão poderosa pode ser a nova engine de arrays dinâmicos do Excel quando combinada com ferramentas de automação como **xlwings**.

Experimente em seus próprios projetos, ajuste as dimensões da matriz ou substitua `SEQUENCE` por qualquer outra função dinâmica. Conforme você se familiariza, descobrirá que automatizar o Excel se torna não apenas possível, mas agradavelmente simples.

Tem perguntas ou quer compartilhar como estendeu esse padrão? Deixe um comentário abaixo e feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Processing Data Using Array Function in Excel](/cells/english/net/excel-formulas-and-calculation-options/processing-data-using-array-function/)
- [Create Dynamic Line Charts in Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/charts-graphs/create-line-charts-excel-aspose-cells-dotnet/)
- [Create Dynamic Excel Charts with Aspose.Cells Java&#58; A Comprehensive Guide for Developers](/cells/english/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}