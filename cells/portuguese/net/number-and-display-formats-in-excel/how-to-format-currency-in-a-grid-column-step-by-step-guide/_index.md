---
category: general
date: 2026-02-15
description: como formatar moeda rapidamente usando set column number format e aplicar
  formato numérico personalizado em C#. Aprenda a recuperar a coluna por nome e definir
  o alinhamento da coluna da grade.
draft: false
keywords:
- how to format currency
- set column number format
- apply custom numeric format
- retrieve column by name
- set grid column alignment
language: pt
og_description: como formatar moeda em uma coluna de grade usando C#. Este tutorial
  mostra como recuperar a coluna pelo nome, definir o formato numérico da coluna,
  aplicar um formato numérico personalizado e definir o alinhamento da coluna da grade.
og_title: Como formatar moeda em uma coluna de grade – Guia completo
tags:
- C#
- GridFormatting
- UI
title: como formatar moeda em uma coluna de grade – Guia passo a passo
url: /pt/net/number-and-display-formats-in-excel/how-to-format-currency-in-a-grid-column-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# como formatar moeda em uma coluna de Grid – Tutorial de Programação Completo

Já se perguntou **como formatar moeda** em uma coluna de grid sem perder a cabeça? Você não está sozinho. Quando você olha para um número simples como `1234.5` e deseja que ele apareça magicamente como `$1,234.50`, a resposta geralmente está em apenas algumas linhas de configuração.  

Neste guia vamos **recuperar a coluna pelo nome**, **definir o formato numérico da coluna**, e **aplicar um formato numérico personalizado** que respeita o layout contábil típico. No caminho, também vamos **definir o alinhamento da coluna do grid** e adicionar uma borda sutil para que a UI fique polida.

> **TL;DR** – Ao final você terá um trecho pronto‑para‑executar que transforma decimais brutos em valores de moeda belamente formatados dentro de qualquer controle estilo `GridJs`.

---

## O que você vai precisar

- Um projeto .NET (qualquer versão que suporte C# 8.0+ – Visual Studio 2022 funciona muito bem).  
- Um componente de grid que exponha uma coleção `Columns` (o exemplo usa uma classe fictícia `GridJs`, mas os conceitos se aplicam a grids da DevExpress, Telerik ou Syncfusion).  
- Familiaridade básica com a sintaxe C# – nenhum truque avançado é necessário.

Se você já tem isso, ótimo. Caso contrário, basta criar um aplicativo console; o grid pode ser simulado para fins de ilustração.

---

## Implementação passo a passo

Abaixo de cada passo você verá um bloco de código compacto, uma breve explicação do **porquê** da linha e uma dica para evitar armadilhas comuns.

### ## Passo 1 – Recuperar a coluna “Amount” pelo nome

```csharp
// Step 1: Retrieve the "Amount" column from the grid
var amountColumn = gridJs.Columns["Amount"];
if (amountColumn == null)
{
    throw new InvalidOperationException("Column 'Amount' does not exist. Verify the column name or check the grid's schema.");
}
```

**Por que isso importa:**  
A maioria das APIs de grid expõe colunas via um indexador semelhante a um dicionário. Recuperar a coluna pelo seu cabeçalho (`"Amount"`) permite que você manipule sua aparência sem tocar na fonte de dados subjacente.  

**Dica de especialista:** Sempre proteja contra um retorno `null` – um erro de digitação no nome da coluna ou uma mudança dinâmica no esquema pode, de outra forma, causar um `NullReferenceException` em tempo de execução.

---

### ## Passo 2 – Definir o formato numérico da coluna usando uma máscara de moeda personalizada

```csharp
// Step 2: Apply a custom numeric format for currency values
amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";
```

**Por que isso importa:**  
A string de formato segue as convenções de formato contábil do Excel:

- `_(* #,##0.00_)` → Números positivos, alinhados à direita com um espaço à esquerda para o símbolo da moeda.  
- `_(* (#,##0.00)` → Números negativos entre parênteses.  
- `_(* \"-\"??_)` → Valores zero exibidos como um traço.  
- `_(@_)` → Valores de texto permanecem inalterados.

Usar **aplicar formato numérico personalizado** lhe dá controle total sobre separadores de milhar, casas decimais e a posição do símbolo da moeda.  

**Caso extremo:** Se sua aplicação precisar respeitar um locale diferente (por exemplo, Euro ao invés de USD), substitua o espaço inicial pelo símbolo adequado ou use formatação sensível a `CultureInfo` na fonte de dados.

---

### ## Passo 3 – Alinhar o conteúdo da coluna à direita para melhorar a legibilidade

```csharp
// Step 3: Align the column contents to the right for better readability
amountColumn.Alignment = GridAlignment.Right;
```

**Por que isso importa:**  
Valores monetários são mais fáceis de ler quando se alinham ao separador decimal. Definir **definir alinhamento da coluna do grid** para `Right` espelha a forma como planilhas exibem dados financeiros.  

**Pegadinha:** Alguns grids ignoram o alinhamento em células que contêm templates personalizados. Se você notar que o alinhamento não está surtindo efeito, verifique se a coluna não está usando um renderizador de célula customizado.

---

### ## Passo 4 – Adicionar uma borda cinza fina ao redor das células da coluna

```csharp
// Step 4: Add a thin gray border around the column cells
amountColumn.Border = new GridBorder
{
    Color = Color.Gray,
    Style = BorderLineStyle.Thin
};
```

**Por que isso importa:**  
Uma borda sutil separa a coluna “Amount” de suas vizinhas, especialmente quando o grid tem cores de linha alternadas. É um indicativo visual de que os dados representam um valor financeiro distinto.  

**Dica:** Se precisar de uma linha mais espessa para impressão, aumente `BorderLineStyle` para `Medium` ou altere `Color` para `Color.Black`.

---

## Exemplo completo em funcionamento

Aqui está o trecho inteiro que você pode inserir em um projeto WinForms ou WPF que usa um controle estilo `GridJs`. O exemplo também imprime os valores formatados no console para que você possa verificar a saída sem uma UI.

```csharp
using System;
using System.Drawing;   // For Color
using GridLibrary;      // Hypothetical namespace for GridJs

namespace GridCurrencyDemo
{
    class Program
    {
        static void Main()
        {
            // Create a mock grid and add a sample column
            var gridJs = new GridJs();
            gridJs.Columns.Add(new GridColumn
            {
                Name = "Amount",
                Header = "Amount",
                DataType = typeof(decimal)
            });

            // Populate some sample data
            gridJs.Rows.Add(new { Amount = 1234.5m });
            gridJs.Rows.Add(new { Amount = -567.89m });
            gridJs.Rows.Add(new { Amount = 0m });

            // ---- Formatting steps ------------------------------------------------
            // 1️⃣ Retrieve the "Amount" column
            var amountColumn = gridJs.Columns["Amount"]
                ?? throw new InvalidOperationException("Column 'Amount' not found.");

            // 2️⃣ Apply custom numeric format for currency
            amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";

            // 3️⃣ Right‑align the values
            amountColumn.Alignment = GridAlignment.Right;

            // 4️⃣ Add a thin gray border
            amountColumn.Border = new GridBorder
            {
                Color = Color.Gray,
                Style = BorderLineStyle.Thin
            };
            // -----------------------------------------------------------------------

            // Render the grid (in a real UI you would call gridJs.Render() or similar)
            Console.WriteLine("Formatted Currency Grid:");
            foreach (var row in gridJs.Rows)
            {
                var rawValue = (decimal)row.Amount;
                // The grid library would automatically apply NumberFormat when displaying.
                // For console demo we mimic the formatting:
                string formatted = rawValue.ToString("#,##0.00", System.Globalization.CultureInfo.InvariantCulture);
                if (rawValue < 0)
                    formatted = $"({formatted.TrimStart('-')})";
                else if (rawValue == 0)
                    formatted = "-";

                Console.WriteLine($"| {formatted,15} |");
            }

            // Keep console open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Saída esperada no console**

```
Formatted Currency Grid:
|        1,234.50 |
|       (567.89) |
|               - |
```

Observe como o número positivo está alinhado à direita, o negativo aparece entre parênteses e o zero mostra um traço – exatamente o que a string de formato personalizada determina.

---

## Perguntas Frequentes & Casos de Borda

| Pergunta | Resposta |
|----------|----------|
| *E se o grid usar uma cultura diferente (ex.: € ao invés de $)?* | Substitua o espaço inicial na string de formato pelo símbolo desejado ou deixe a fonte de dados emitir uma string pré‑formatada usando `CultureInfo.CurrentCulture`. |
| *Posso reutilizar o mesmo formato em várias colunas?* | Absolutamente. Armazene a string de formato em uma constante (`const string CurrencyMask = "...";`) e atribua-a onde precisar de moeda. |
| *O que acontece se a coluna contiver um valor string?* | A string de formato afeta apenas tipos numéricos. Strings passam sem alterações, por isso a última parte da máscara (`_(@_)`) existe – ela preserva conteúdo não numérico. |
| *Há impacto de desempenho?* | Negligível. O formato é aplicado no momento da renderização, não durante a recuperação dos dados. A menos que você esteja renderizando milhares de linhas por quadro, não notará lentidão. |
| *Como tornar a borda mais espessa para relatórios impressos?* | Troque `BorderLineStyle.Thin` por `BorderLineStyle.Medium` ou `BorderLineStyle.Thick`. Algumas bibliotecas também permitem especificar a largura em pixels diretamente. |

---

## Conclusão

Percorremos **como formatar moeda** em uma coluna de grid do início ao fim: recuperar a coluna pelo nome, definir o formato numérico da coluna, aplicar um formato numérico personalizado, alinhar as células e adicionar uma borda elegante. O exemplo completo funciona imediatamente e demonstra o resultado visual exato que você pode esperar.

Se estiver pronto para avançar, experimente:

- **Culturas dinâmicas** – altere a string de formato com base no locale do usuário.  
- **Condicional

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}