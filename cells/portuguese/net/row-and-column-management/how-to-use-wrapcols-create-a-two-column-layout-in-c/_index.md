---
category: general
date: 2026-02-15
description: Como usar WRAPCOLS para criar um layout de duas colunas, adicionar uma
  fórmula e gerar um array de sequência em planilhas C# – guia passo a passo.
draft: false
keywords:
- how to use wrapcols
- create two column layout
- how to add formula
- how to create columns
- generate sequence array
language: pt
og_description: Como usar WRAPCOLS para criar um layout de duas colunas, adicionar
  fórmulas e gerar um array de sequência em uma planilha C# – guia completo.
og_title: 'Como usar WRAPCOLS: Layout de duas colunas em C#'
tags:
- CSharp
- ExcelAutomation
- WorksheetFormula
title: 'Como usar WRAPCOLS: Crie um layout de duas colunas em C#'
url: /pt/net/row-and-column-management/how-to-use-wrapcols-create-a-two-column-layout-in-c/
---

them as is.

Check for any URLs: none.

Check for any markdown links: none.

All good.

Now produce final answer with only translated content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Usar WRAPCOLS: Criar um Layout de Duas Colunas em C#

Já se perguntou **como usar WRAPCOLS** quando precisa de uma visualização rápida de duas colunas dentro de uma planilha estilo Excel? Você não está sozinho. Muitos desenvolvedores se deparam com dificuldades ao tentar dividir uma lista gerada em colunas organizadas sem escrever um loop para cada célula. A boa notícia? Com a função `WRAPCOLS` você pode inserir uma única fórmula em `A1` e deixar o Excel (ou um mecanismo compatível) fazer o trabalho pesado.

Neste tutorial, vamos percorrer **como adicionar fórmula** que cria um **layout de duas colunas**, mostrar **como criar colunas** dinamicamente e até **gerar array de sequência** de valores em tempo real. Ao final, você terá um trecho de código C# totalmente executável que pode colar em seu projeto, executar e ver um bloco de duas colunas organizado aparecer instantaneamente.

## O que Você Vai Aprender

- O propósito do `WRAPCOLS` e por que ele é uma alternativa melhor ao loop manual.  
- Como **adicionar uma fórmula** a uma célula da planilha usando C#.  
- Como gerar um array de sequência com `SEQUENCE` e alimentá‑lo ao `WRAPCOLS`.  
- Dicas para recalcular a planilha de modo que a fórmula seja resolvida imediatamente.  
- Tratamento de casos extremos (ex.: planilhas vazias, contagens de colunas personalizadas).

Nenhuma biblioteca externa além de um pacote padrão de processamento de Excel é necessária – usaremos **ClosedXML** por sua API simples, mas os conceitos se aplicam ao EPPlus, SpreadsheetGear ou até ao Google Sheets via sua API.

## Pré‑requisitos

- .NET 6.0 ou superior (o código compila no .NET Core e no .NET Framework).  
- Uma referência ao **ClosedXML** (`dotnet add package ClosedXML`).  
- Conhecimento básico de C# – você deve estar confortável com declarações `using` e inicialização de objetos.  

Se você já tem uma pasta de trabalho aberta, pode pular a parte de criação de arquivo e ir direto para a seção de fórmula.

## Etapa 1: Configurar a Planilha (Como Criar Colunas)

Primeiro precisamos de um objeto `Worksheet` para trabalhar. No ClosedXML você o obtém a partir de um `XLWorkbook`. O trecho abaixo cria uma nova pasta de trabalho, adiciona uma planilha chamada *Demo* e obtém uma referência chamada `worksheet` para clareza.

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // Create a fresh workbook and add a worksheet named "Demo"
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");

            // Rename for clarity – this is the worksheet we’ll manipulate
            var worksheet = ws;   // <-- same object, just a clearer name

            // --------------------------------------------------------------
            // Next step: write the WRAPCOLS formula
            // --------------------------------------------------------------
```

> **Por que renomear?**  
> Manter o nome da variável curto (`worksheet`) facilita a leitura do código posterior, especialmente quando você encadeia várias operações. Também reflete o estilo de nomenclatura que você verá na maioria da documentação, reduzindo a carga cognitiva.

## Etapa 2: Escrever a Fórmula (Como Adicionar Fórmula + Gerar Array de Sequência)

Agora vem a linha mágica. Vamos colocar uma fórmula na célula **A1** que faz duas coisas:

1. **Gerar um array de sequência** de seis números (`SEQUENCE(6)` → 1,2,3,4,5,6).  
2. **Envolver esses números em duas colunas** (`WRAPCOLS(..., 2)`).

```csharp
            // Write the WRAPCOLS formula into A1
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // --------------------------------------------------------------
            // Finally, force the engine to evaluate the formula
            // --------------------------------------------------------------
```

> **O que está acontecendo?**  
> `SEQUENCE(6)` cria um array vertical `{1;2;3;4;5;6}`. `WRAPCOLS` então pega esse array e o “envolve” no número especificado de colunas — neste caso **2**. O resultado é um bloco de 3 linhas × 2 colunas que se parece com:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

Se você mudar o segundo argumento para **3**, obterá um layout de três colunas. Esse é o núcleo de **como criar colunas** dinamicamente sem loops manuais.

## Etapa 3: Recalcular a Planilha (Garantindo que a Fórmula Seja Avaliada)

O ClosedXML não avalia automaticamente as fórmulas quando você as escreve. É necessário chamar `Calculate()` na pasta de trabalho (ou na planilha específica) para forçar a avaliação.

```csharp
            // Recalculate so the formula is evaluated immediately
            worksheet.Calculate();

            // Optional: save the workbook to inspect the result
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

> **Dica profissional:** Se você estiver trabalhando com pastas de trabalho grandes, chame `Calculate()` apenas nas planilhas que realmente foram alteradas. Isso economiza memória e acelera o processamento.

Ao abrir `WrapColsDemo.xlsx` você verá o layout de duas colunas preenchido ordenadamente em **A1:B3**. Nenhum código adicional foi necessário para percorrer linhas ou colunas – `WRAPCOLS` cuidou de tudo.

## Etapa 4: Verificar a Saída (O que Esperar)

Depois de executar o programa, abra o arquivo gerado. Você deverá ver:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

Se os números aparecerem verticalmente (ou seja, todos na coluna A), verifique se você chamou `worksheet.Calculate()` **depois** de definir a fórmula. Alguns mecanismos também precisam de `workbook.Calculate()`; o trecho acima funciona com o avaliador interno do ClosedXML.

## Variações Comuns & Casos de Borda

### Alterando o Número de Colunas

Para **criar um layout de duas colunas** com uma contagem de linhas diferente, basta ajustar o tamanho do `SEQUENCE` ou o segundo argumento do `WRAPCOLS`:

```csharp
worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(12), 3)";
```

Isso produz um bloco de 4 linhas × 3 colunas (12 números divididos em três colunas).

### Usando uma Contagem de Colunas Dinâmica

Se a contagem de colunas vem de uma variável, incorpore-a com interpolação de strings:

```csharp
int colCount = 4;
worksheet.Cell("A1").FormulaA1 = $"=WRAPCOLS(SEQUENCE(8), {colCount})";
```

Agora você tem **como adicionar fórmula** que se adapta em tempo de execução.

### Planilhas Vazias

Se a planilha estiver vazia, `Calculate()` ainda funciona – a fórmula preencherá as células a partir de A1. Contudo, se você posteriormente excluir linhas/colunas que intersectam a faixa de saída, pode ver erros `#REF!`. Para evitar isso, limpe a faixa de destino primeiro:

```csharp
worksheet.Range("A1:Z100").Clear(); // wipes any leftovers
```

### Compatibilidade

`WRAPCOLS` e `SEQUENCE` fazem parte das funções **Array Dinâmico** do Excel, introduzidas no Office 365. Se você direcionar versões mais antigas do Excel, as funções não existirão, e será necessário um loop manual. O avaliador do ClosedXML espelha o comportamento mais recente do Excel, portanto é seguro para ambientes modernos.

## Exemplo Completo (Pronto para Copiar‑Colar)

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook & worksheet
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");
            var worksheet = ws;   // clearer name

            // 2️⃣ Write WRAPCOLS formula that generates a sequence array
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // 3️⃣ Force calculation so the formula resolves immediately
            worksheet.Calculate();

            // 4️⃣ Save the file (optional, but handy for verification)
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

**Resultado esperado:** Ao abrir *WrapColsDemo.xlsx* será exibido um layout de duas colunas organizado com os números de 1 a 6 dispostos como descrito anteriormente.

## Conclusão

Cobrimos **como usar WRAPCOLS** para **criar um layout de duas colunas**, demonstramos **como adicionar fórmula** programaticamente e vimos como `SEQUENCE` permite **gerar array de sequência** de valores sem um loop. Ao aproveitar as funções de array dinâmico do Excel a partir do C#, você pode manter seu código conciso, legível e fácil de manter.

Em seguida, você pode explorar:

- **Criar contagens de linhas dinâmicas** com `ROWS` ou `COUNTA`.  
- **Estilizar a saída** (bordas, formatos numéricos) usando a API de estilos do ClosedXML.  
- **Exportar para CSV** após o layout ser construído, para processamento posterior.

Experimente, ajuste a contagem de colunas e veja quão rápido você pode prototipar planilhas complexas. Feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}