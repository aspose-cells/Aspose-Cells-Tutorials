---
category: general
date: 2026-03-18
description: Copiar tabela dinâmica em C# com Aspose.Cells. Aprenda como copiar intervalo
  do Excel, duplicar tabela dinâmica do Excel, copiar intervalo para uma nova planilha
  e copiar a tabela dinâmica para a planilha em minutos.
draft: false
keywords:
- copy pivot table
- copy excel range
- duplicate excel pivot
- copy range to new
- copy pivot to sheet
language: pt
og_description: Copiar tabela dinâmica em C# usando Aspose.Cells. Aprenda a duplicar
  a tabela dinâmica do Excel, copiar um intervalo do Excel para um novo local e copiar
  a tabela dinâmica para outra planilha, com exemplos completos de código.
og_title: Copiar tabela dinâmica em C# – Guia completo de programação
tags:
- Aspose.Cells
- C#
- Excel automation
title: Copiar tabela dinâmica em C# – Guia passo a passo
url: /pt/net/pivot-tables/copy-pivot-table-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copiar tabela dinâmica em C# – Guia de Programação Completo

Já precisou **copiar tabela dinâmica** de uma parte de uma pasta de trabalho para outra, mas não tinha certeza de como fazer isso sem perder as conexões de dados subjacentes? Você não está sozinho. Muitos desenvolvedores encontram esse obstáculo ao automatizar relatórios do Excel, especialmente quando a tabela dinâmica está dentro de um bloco de dados maior. A boa notícia? Com Aspose.Cells você pode copiar a tabela dinâmica **exatamente como ela aparece**, e também aprenderá como **copy excel range**, **duplicate excel pivot**, e até **copy pivot to sheet** com apenas algumas linhas de C#.

Neste tutorial, percorreremos um cenário do mundo real: mover uma tabela dinâmica que ocupa *A1:J20* para uma nova área *M1:V20* na mesma planilha. Ao final, você terá um programa executável, entenderá por que cada passo é importante e saberá como adaptar o código para outras áreas ou até mesmo planilhas separadas. Nenhuma documentação externa necessária—tudo está aqui.

---

## Pré-requisitos

Before we dive in, make sure you have:

- **Aspose.Cells for .NET** (versão 23.9 ou posterior). Você pode obtê-lo via NuGet: `Install-Package Aspose.Cells`.
- Um ambiente básico de desenvolvimento C# (Visual Studio 2022, Rider ou VS Code com a extensão C#).
- Um arquivo Excel (`source.xlsx`) que contém uma tabela dinâmica dentro da área *A1:J20*.

Isso é tudo. Se você está confortável criando um aplicativo de console, está pronto para começar.

---

## Como copiar tabela dinâmica no Aspose.Cells

O núcleo da solução é uma única chamada a `Worksheet.Cells.CopyRange`. Este método não apenas copia valores brutos das células, mas também preserva tabelas dinâmicas, gráficos e outros objetos ricos automaticamente. Vamos analisar passo a passo.

### Etapa 1: Carregar a pasta de trabalho de origem

First we need to bring the workbook into memory.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source workbook from disk
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Por que isso importa:** Carregar a pasta de trabalho cria uma representação em memória que o Aspose.Cells pode manipular sem iniciar o Excel. É rápido, thread‑safe e funciona em servidores.

### Etapa 2: Obter a primeira planilha

Most examples use the first sheet, but you can target any index or name.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = sourceWorkbook.Worksheets[0];
```

> **Dica:** Se você precisar **copy pivot to sheet** em vez da mesma planilha, basta mudar a referência `worksheet` para outro objeto `Worksheet`.

### Etapa 3: Definir as áreas de origem e destino

We’ll use `CellArea` structs to describe the blocks we’re moving.

```csharp
        // Define the source range (A1:J20) that contains the pivot table
        CellArea sourceRange = new CellArea(0, 0, 19, 9);   // rows 0‑19, columns 0‑9

        // Define the target range (M1:V20) where the data will be copied
        CellArea targetRange = new CellArea(0, 12, 19, 21); // rows 0‑19, columns 12‑21
```

> **Explicação:** Os índices de linhas e colunas são baseados em zero. Coluna 0 = **A**, coluna 12 = **M**, e assim por diante. Ajuste esses números se sua tabela dinâmica estiver em outro local.

### Etapa 4: Executar a operação de cópia

Now the magic happens. Setting the last boolean parameter to `true` tells Aspose.Cells to copy all objects—including the pivot.

```csharp
        // Copy the source range to the target range; pivot tables are copied automatically
        worksheet.Cells.CopyRange(
            sourceRange.StartRow, sourceRange.StartColumn,
            sourceRange.EndRow, sourceRange.EndColumn,
            targetRange.StartRow, targetRange.StartColumn,
            true);
```

> **Por que `true`?** O sinalizador indica “copiar todos os objetos”. Se você defini-lo como `false`, apenas os valores simples das células seriam movidos, e a tabela dinâmica seria perdida.

### Etapa 5: Salvar a pasta de trabalho

Finally, write the modified workbook back to disk.

```csharp
        // Save the workbook with the copied range
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copy-pivot.xlsx");
    }
}
```

> **Resultado:** `copy-pivot.xlsx` agora contém a tabela dinâmica original em *A1:J20* **e** uma cópia idêntica em *M1:V20*. Abra o arquivo no Excel para verificar que ambas as tabelas dinâmicas estão funcionais e mantêm suas conexões de dados.

---

## Copiar intervalo Excel para um novo local – uma variação rápida

Sometimes you only need to **copy excel range** without worrying about pivots. The same `CopyRange` method does the trick; just set the last argument to `false`.

```csharp
worksheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    false); // plain values only
```

> **Quando usar:** Se você está movendo dados brutos para uma planilha de cálculo temporária, desabilitar a cópia de objetos economiza memória e acelera a operação.

---

## Duplicar tabela dinâmica Excel em várias planilhas

What if you want to **duplicate excel pivot** on a different worksheet? The pattern stays the same; you just reference another `Worksheet` for the destination.

```csharp
// Assume we have a second sheet already created
Worksheet destSheet = sourceWorkbook.Worksheets.Add("PivotCopy");

// Copy the pivot (and its data source) to the new sheet starting at A1
destSheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    0, 0, // destination at A1
    true);
```

> **Caso extremo:** Se a tabela dinâmica de origem usa uma tabela que está na planilha original, o Aspose.Cells também copiará a definição da tabela subjacente, garantindo que a nova tabela dinâmica funcione imediatamente.

---

## Armadilhas comuns e como evitá‑las

| Pitfall | Why it happens | Fix |
|---------|----------------|-----|
| **Pivot loses its cache** | Usando `CopyRange` com `false` ou uma rotina de cópia personalizada que ignora objetos. | Sempre passe `true` quando precisar da própria tabela dinâmica. |
| **Target cells already contain data** | Sobrescreve silenciosamente, potencialmente corrompendo fórmulas existentes. | Limpe a área de destino primeiro: `worksheet.Cells.ClearRange(targetRange.StartRow, targetRange.StartColumn, targetRange.EndRow, targetRange.EndColumn, true);` |
| **Source range doesn’t include the whole pivot** | Tabelas dinâmicas abrangem mais linhas/colunas do que você espera (por exemplo, linhas ocultas). | Use `worksheet.PivotTables[0].DataRange` para obter programaticamente os limites exatos. |
| **Copying between workbooks** | `CopyRange` funciona apenas dentro da mesma pasta de trabalho. | Use `sourceWorksheet.Cells.CopyRange` para um intervalo temporário, então `destWorkbook.Worksheets.AddCopy(sourceWorksheet);` |

---

## Saída esperada & verificação

After running the program:

1. Abra `copy-pivot.xlsx`.
2. Você verá duas tabelas dinâmicas idênticas—uma em **A1:J20**, outra em **M1:V20**.
3. Atualize qualquer tabela dinâmica; ambas devem refletir os mesmos dados subjacentes.
4. Se você duplicou para outra planilha, a nova planilha conterá também uma cópia funcional.

A quick way to verify via code:

```csharp
int pivotCount = worksheet.PivotTables.Count; // should be 2 after copy
Console.WriteLine($"Pivot tables on the sheet: {pivotCount}");
```

---

## Dica profissional: Automatizar detecção de intervalo

Hard‑coding `CellArea` works for static reports, but production code often needs to locate the pivot dynamically.

```csharp
// Find the first pivot table on the sheet
PivotTable pt = worksheet.PivotTables[0];
CellArea ptRange = pt.DataRange;

// Use the detected range for copying
worksheet.Cells.CopyRange(
    ptRange.StartRow, ptRange.StartColumn,
    ptRange.EndRow, ptRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    true);
```

> **Por que se preocupar?** Isso torna sua solução resiliente a alterações de layout—chega de erros “Ops, a tabela dinâmica mudou para B2”.

![copy pivot table example](copy-pivot.png){alt="exemplo de cópia de tabela dinâmica"}

*The screenshot (placeholder) shows the original pivot on the left and the duplicated one on the right.*

---

## Recapitulação

Acabamos de cobrir como **copy pivot table** em C# usando Aspose.Cells, exploramos maneiras de **copy excel range**, **duplicate excel pivot**, e até **copy pivot to sheet** entre planilhas. Os principais pontos são:

- Use `Worksheet.Cells.CopyRange` com o sinalizador `true` para preservar objetos ricos.
- Defina objetos `CellArea` de origem e destino com índices baseados em zero.
- Ajuste a planilha de destino se precisar **copy pivot to sheet**.
- Fique atento a casos extremos como dados existentes, linhas ocultas e cenários entre pastas de trabalho.

---

## O que vem a seguir?

- **Dynamic pivot discovery**: Construa um helper que escaneia uma pasta de trabalho em busca de todas as tabelas dinâmicas e as replica automaticamente.
- **Export to PDF/HTML**: Após copiar, você pode querer renderizar a planilha para um formato de relatório—Aspose.Cells também lida com isso.
- **Performance tuning**: Para pastas de trabalho massivas, considere desativar o cálculo antes de copiar e reativá‑lo depois.

Sinta‑se à vontade para experimentar: altere as coordenadas de destino, copie para uma nova pasta de trabalho, ou até mesmo faça loop sobre várias planilhas para criar um relatório consolidado. As possibilidades são infinitas, e com a base que você tem agora, será capaz de adaptar o código para praticamente qualquer tarefa de automação do Excel.

Feliz codificação, e que suas tabelas dinâmicas estejam sempre perfeitamente sincronizadas!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}