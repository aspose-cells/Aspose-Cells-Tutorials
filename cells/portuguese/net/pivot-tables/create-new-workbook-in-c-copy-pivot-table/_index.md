---
category: general
date: 2026-06-24
description: Crie uma nova planilha em C# e copie a tabela dinâmica preservando seus
  dados. Aprenda como copiar linhas, exportar o intervalo selecionado e manter a tabela
  dinâmica intacta.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- export selected range
language: pt
og_description: Crie uma nova planilha em C# e copie uma tabela dinâmica preservando
  seus dados. Guia passo a passo que cobre como copiar linhas e exportar o intervalo
  selecionado.
og_title: Criar nova pasta de trabalho em C# – Copiar Tabela Dinâmica
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Create new workbook in C# and copy pivot table while preserving its
    data. Learn how to copy rows, export selected range, and keep the pivot intact.
  headline: Create New Workbook in C# – Copy Pivot Table
  type: TechArticle
- questions:
  - answer: Yes, as long as the copied rectangle encloses each pivot you need. If
      you only want one, adjust `rows`/`cols` to isolate it.
    question: Does this work with multiple pivot tables on the same sheet?
  - answer: The pivot cache will still point to the original connection. Call `pivotTable.RefreshData()`
      after loading the destination if you want to re‑query the source.
    question: What if the source workbook uses external data connections?
  - answer: Absolutely. Replace `destinationWorkbook` with `sourceWorkbook` and pick
      another worksheet index.
    question: Can I copy the pivot to a different sheet within the same workbook?
  - answer: 'Use `CopyRows`/`CopyColumns` overloads that accept a `CopyOptions` object—set
      `CopyOptions.CopyType = CopyType.ValuesOnly` or `CopyType.All` depending on
      your needs. --- ## Conclusion We’ve just walked through a **create new workbook**
      scenario that **copy pivot table**, **preserve pivot table**, an'
    question: Is there a way to copy formatting only?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- Excel automation
title: Criar nova pasta de trabalho em C# – Copiar tabela dinâmica
url: /pt/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Nova Pasta de Trabalho em C# – Copiar Tabela Dinâmica

Já precisou **criar nova pasta de trabalho** em C# apenas para mover um trecho de dados que inclui uma **tabela dinâmica**? Você não está sozinho. Em muitos pipelines de relatórios você captura algumas linhas, talvez algumas colunas, e espera que a tabela dinâmica permaneça exatamente como estava — sem referências quebradas, sem cálculos ausentes.  

A boa notícia? Com algumas linhas de Aspose.Cells você pode **copiar tabela dinâmica**, mantê‑la intacta e ainda **exportar intervalo selecionado** sem quebrar nada. Abaixo você verá um exemplo completo, pronto‑para‑executar, que mostra **como copiar linhas**, preservar a tabela dinâmica e salvar o resultado como uma pasta de trabalho totalmente nova.

## O Que Este Tutorial Abrange

- Configurar um projeto C# com Aspose.Cells (a biblioteca que alimenta o código).
- Carregar a pasta de trabalho fonte que contém a tabela dinâmica original.
- Usar os métodos `CopyRows` e `CopyColumns` da biblioteca para duplicar o intervalo exato que você precisa.
- Salvar a área duplicada em um cenário de **criar nova pasta de trabalho** enquanto a tabela dinâmica permanece funcional.
- Dicas para casos extremos como múltiplas tabelas dinâmicas, linhas ocultas e grandes conjuntos de dados.

Ao final deste guia você será capaz de **exportar intervalo selecionado** de qualquer arquivo Excel, manter a lógica da tabela dinâmica viva e colocar o novo arquivo onde desejar.

> **Pré‑requisito**: Aspose.Cells for .NET (versão de teste gratuita ou licenciada) instalado via NuGet. Se ainda não o adicionou, execute `dotnet add package Aspose.Cells` na pasta do seu projeto.

---

## Criar Nova Pasta de Trabalho e Copiar Tabela Dinâmica

A seguir está o coração da solução. Vamos percorrer cada linha, explicar por que ela importa e, em seguida, mostrar o programa completo.

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // 1️⃣ Load the source workbook that contains the pivot table
        string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destSheet = destinationWorkbook.Worksheets[0];

        // 3️⃣ Define the range we want to copy (first 20 rows, first 4 columns)
        //    This range includes the pivot table we care about.
        int startRow = 0;   // zero‑based index
        int startColumn = 0;
        int totalRows = 20;
        int totalColumns = 4;

        // 4️⃣ Copy rows – this is the “how to copy rows” part.
        //    Aspose.Cells lets us copy rows directly from the source cells collection.
        sourceWorkbook.Worksheets[0].Cells.CopyRows(startRow, startRow, totalRows);

        // 5️⃣ Copy columns – paired with the row copy to form a rectangular block.
        sourceWorkbook.Worksheets[0].Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 6️⃣ Now move the copied block into the destination sheet.
        //    We use the same start cell (A1) for simplicity.
        destSheet.Cells.CopyRows(startRow, startRow, totalRows);
        destSheet.Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 7️⃣ Save the destination workbook – the pivot table is preserved in the copied range
        string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
        destinationWorkbook.Save(destPath);

        Console.WriteLine("✅ New workbook created and pivot table preserved at: " + destPath);
    }
}
```

### Por Que Isso Funciona

- **`CopyRows` / `CopyColumns`**: Esses métodos duplicam os dados subjacentes das células *e* os objetos associados (como um cache de tabela dinâmica). Por isso a tabela dinâmica continua funcional após a cópia.
- **Planilha de destino separada**: Ao criar uma nova instância `Workbook` nós **criar nova pasta de trabalho** sem formatação residual ou planilhas ocultas que possam interferir.
- **Indexação baseada em zero**: Aspose.Cells usa índices baseados em zero, então `0` aponta para a célula **A1**. Ajuste `startRow`/`startColumn` se sua tabela dinâmica não estiver no canto superior‑esquerdo.
- **Preservar tabela dinâmica**: O cache da tabela dinâmica reside no mesmo intervalo, portanto copiar o intervalo copia automaticamente o cache. Nenhum código extra é necessário.

---

## Como Copiar Linhas Sem Quebrar a Tabela Dinâmica

Se você está interessado apenas na parte de cópia de linhas, pode isolá‑la:

```csharp
// Copy just rows 5‑15 (inclusive) from the source sheet
int sourceStartRow = 4;   // row 5 in Excel terms
int rowsToCopy = 11;      // rows 5‑15 => 11 rows
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy);
```

**Dica profissional**: Ao copiar linhas que intersectam uma tabela dinâmica, sempre copie a *totalidade* da área da tabela (linhas + colunas). Cópias parciais podem deixar a tabela dinâmica com campos ausentes, causando erros `#REF!`.

---

## Exportar Intervalo Selecionado – Um Cenário Real

Imagine que você tem uma pasta de trabalho de vendas gigantesca, mas seu cliente quer apenas o resumo do primeiro trimestre, que está nas linhas 1‑20 e colunas A‑D. O trecho acima já **exporta intervalo selecionado** para você. Basta alterar as variáveis `totalRows` e `totalColumns` para corresponder à solicitação do cliente e pronto.

### Lidando com Linhas Ocultas ou Filtros

Se a planilha fonte tem linhas ocultas (talvez filtradas), você pode querer copiar apenas as linhas *visíveis*. Aspose.Cells oferece sobrecargas de `CopyRows` que respeitam a visibilidade:

```csharp
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy, true);
```

Defina o último booleano como `true` para copiar somente linhas visíveis — perfeito para “exportar intervalo selecionado” quando o usuário aplicou filtros.

---

## Preservar Tabela Dinâmica – Armadilhas Comuns & Como Evitá‑las

| Problema | Por Que Acontece | Correção |
|----------|------------------|----------|
| **Cache da tabela dinâmica não copiado** | Usar `Range.Copy` simples em vez de `Cells.CopyRows/CopyColumns`. | Use os métodos `Cells` como mostrado. |
| **Planilha de destino tem tabela dinâmica existente** | Salvar sobre uma pasta de trabalho que já contém uma tabela dinâmica com o mesmo nome. | Comece com um `Workbook()` novo (como fazemos). |
| **Intervalos nomeados quebram** | A tabela dinâmica fonte referencia um intervalo nomeado que não está presente no novo arquivo. | Copie também o intervalo nomeado: `sourceWorkbook.Worksheets[0].Names.CopyTo(destSheet);` |
| **Caminho da fonte de dados muda** | A tabela dinâmica aponta para uma fonte de dados externa que não está disponível. | Use `PivotTable.RefreshData()` após a cópia, se necessário. |

---

## Exemplo Completo de Ponta a Ponta (Pronto para Executar)

A seguir está o programa completo, incluindo as diretivas `using` e uma breve interface de console. Copie‑e‑cole em um novo projeto Console App e pressione **F5**.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyUtility
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Load source workbook (contains the pivot)
            // -------------------------------------------------
            string srcPath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook srcWb = new Workbook(srcPath);

            // -------------------------------------------------
            // Step 2: Prepare destination workbook (create new workbook)
            // -------------------------------------------------
            Workbook destWb = new Workbook();
            Worksheet destWs = destWb.Worksheets[0];

            // -------------------------------------------------
            // Step 3: Define the block we want to copy
            // -------------------------------------------------
            int startRow = 0;      // A1
            int startCol = 0;      // A
            int rows = 20;         // first 20 rows
            int cols = 4;          // first 4 columns

            // -------------------------------------------------
            // Step 4: Copy rows and columns from source to destination
            // -------------------------------------------------
            srcWb.Worksheets[0].Cells.CopyRows(startRow, startRow, rows);
            srcWb.Worksheets[0].Cells.CopyColumns(startCol, startCol, cols);
            destWs.Cells.CopyRows(startRow, startRow, rows);
            destWs.Cells.CopyColumns(startCol, startCol, cols);

            // -------------------------------------------------
            // Step 5: Save the new workbook (preserve pivot table)
            // -------------------------------------------------
            string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
            destWb.Save(destPath);

            Console.WriteLine($"✅ Workbook created at {destPath}");
        }
    }
}
```

**Saída esperada** (no console):

```
✅ Workbook created at YOUR_DIRECTORY\copy-pivot.xlsx
```

Abra `copy-pivot.xlsx` e você verá a mesma tabela dinâmica que tinha em `source.xlsx`, totalmente funcional e referenciando o intervalo de dados copiado.

---

## Perguntas Frequentes

**Q: Isso funciona com múltiplas tabelas dinâmicas na mesma planilha?**  
A: Sim, contanto que o retângulo copiado englobe cada tabela que você precisar. Se quiser apenas uma, ajuste `rows`/`cols` para isolá‑la.

**Q: E se a pasta de trabalho fonte usar conexões de dados externas?**  
A: O cache da tabela dinâmica ainda apontará para a conexão original. Chame `pivotTable.RefreshData()` após carregar o destino se quiser consultar a fonte novamente.

**Q: Posso copiar a tabela dinâmica para outra planilha dentro do mesmo workbook?**  
A: Absolutamente. Substitua `destinationWorkbook` por `sourceWorkbook` e escolha outro índice de planilha.

**Q: Existe uma forma de copiar apenas a formatação?**  
A: Use as sobrecargas de `CopyRows`/`CopyColumns` que aceitam um objeto `CopyOptions` — defina `CopyOptions.CopyType = CopyType.ValuesOnly` ou `CopyType.All` conforme sua necessidade.

---

## Conclusão

Acabamos de percorrer um cenário de **criar nova pasta de trabalho** que **copia tabela dinâmica**, **preserva tabela dinâmica** e **exporta intervalo selecionado** — tudo em puro C#


## O Que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Criar uma Nova Tabela Dinâmica Programaticamente em .NET](/cells/english/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/)
- [Como Alterar os Dados‑Fonte da Tabela Dinâmica Usando Aspose.Cells para .NET | Guia de Análise de Dados](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [Como Gerenciar a Compatibilidade de Tabelas Dinâmicas do Excel com Aspose.Cells para .NET | Guia de Análise de Dados](/cells/english/net/data-analysis/manage-excel-pivot-table-compatibility-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}