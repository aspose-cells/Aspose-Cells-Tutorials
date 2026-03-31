---
category: general
date: 2026-03-30
description: Como copiar planilha em C# usando Aspose.Cells – guia passo a passo cobrindo
  cópia de intervalo de células, cópia de colunas entre planilhas, cópia de tabela
  dinâmica da planilha e código para adicionar nova planilha.
draft: false
keywords:
- how to copy worksheet
- copy cell range
- copy columns between sheets
- copy worksheet pivot table
- add new worksheet code
language: pt
og_description: Aprenda como copiar planilha em C# com Aspose.Cells. Este guia mostra
  como copiar intervalo de células, preservar tabelas dinâmicas, copiar colunas entre
  planilhas e adicionar código para nova planilha.
og_title: Como Copiar Planilha no C# – Tutorial Completo do Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Como copiar planilha no C# com Aspose.Cells – Guia completo
url: /pt/net/excel-copy-worksheet/how-to-copy-worksheet-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Copiar Planilha em C# com Aspose.Cells – Guia Completo

Já se perguntou **como copiar worksheet** em C# sem perder nenhuma tabela dinâmica ou fórmula? Você não está sozinho — muitos desenvolvedores encontram dificuldades quando precisam duplicar uma planilha mantendo todos os recursos intactos. Neste tutorial, vamos percorrer uma solução prática, de ponta a ponta, que não só copia os dados, mas também preserva a **copy worksheet pivot table**, lida com **copy cell range**, e mostra o **add new worksheet code** que você precisará.

Cobriremos tudo, desde o carregamento da pasta de trabalho de origem até a gravação do arquivo de destino, para que você possa copy columns between sheets, preservar objetos e manter seu código limpo. Sem referências vagas, apenas um exemplo completo e executável que você pode inserir em seu projeto hoje.

## O que este tutorial cobre

- Carregar um arquivo Excel existente com Aspose.Cells  
- Usar **add new worksheet code** para criar uma planilha de destino  
- Definir um **copy cell range** que inclui uma tabela dinâmica  
- Configurar **CopyOptions** para manter gráficos, fórmulas e tabelas dinâmicas intactas  
- Executar **copy columns between sheets** com precisão linha a linha  
- Salvar o resultado e verificar se a planilha foi copiada corretamente  

Ao final deste guia, você será capaz de responder à pergunta “how to copy worksheet” com confiança, seja automatizando relatórios ou construindo uma interface baseada em planilhas.

## Como copiar worksheet – Visão geral

Antes de mergulharmos no código, vamos delinear o fluxo de alto nível. Pense nisso como uma receita:

1. **Load** a pasta de trabalho de origem (`Source.xlsx`).  
2. **Add** uma nova planilha para conter a cópia (`add new worksheet code`).  
3. **Define** a área que você deseja duplicar (`copy cell range`).  
4. **Configure** as opções de cópia para que a tabela dinâmica sobreviva (`copy worksheet pivot table`).  
5. **Copy** linhas e colunas (`copy columns between sheets`).  
6. **Save** a nova pasta de trabalho (`Destination.xlsx`).  

É isso — seis passos, sem mágica. Cada passo é explicado abaixo com trechos de código e o raciocínio por trás dele.

## Etapa 1 – Carregar a pasta de trabalho de origem

Primeiro de tudo: você precisa de uma instância `Workbook` apontando para o arquivo que deseja duplicar. Esta etapa é essencial porque o Aspose.Cells trabalha diretamente com o sistema de arquivos, não com a interface do Office.

```csharp
using Aspose.Cells;

// Path to the original file
string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";

// Load the workbook – this is the starting point for how to copy worksheet
Workbook workbook = new Workbook(sourcePath);
```

*Por que isso importa:* Carregar o arquivo cria uma representação em memória de cada planilha, célula e objeto. Sem isso, não há nada para copiar, e qualquer tentativa de `add new worksheet code` mais tarde falharia porque os dados de origem não estão presentes.

## Etapa 2 – Adicionar uma nova planilha (add new worksheet code)

Agora precisamos de um local para colar os dados copiados. É aqui que o **add new worksheet code** brilha. Você pode nomear a planilha como quiser; aqui a chamamos de `"Copy"`.

```csharp
// Grab the first worksheet (the one we want to copy)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a fresh worksheet to receive the copy
Worksheet copySheet = workbook.Worksheets.Add("Copy");
```

*Dica de especialista:* Se você planeja copiar várias planilhas, chame `Worksheets.Add` dentro de um loop e dê a cada planilha um nome exclusivo. Dessa forma, você evita colisões de nomes e mantém sua pasta de trabalho organizada.

## Etapa 3 – Definir o intervalo de células a copiar

Um **copy cell range** informa ao Aspose.Cells exatamente quais linhas e colunas duplicar. Em muitos cenários reais, o intervalo inclui uma tabela dinâmica, portanto devemos ser precisos.

```csharp
// Define the area that contains the pivot table (A1:G20)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 19,       // Row 20
    EndColumn = 6      // Column G
};

// Destination range – we start at the same top‑left corner
CellArea destinationRange = new CellArea
{
    StartRow = 0,
    StartColumn = 0,
    EndRow = 19,
    EndColumn = 6
};
```

*Por que precisamos disso:* Ao declarar explicitamente o intervalo, você evita copiar a planilha inteira (o que pode ser desperdiçador) e garante que a tabela dinâmica esteja dentro da área copiada. Este é o cerne de **how to copy worksheet** quando você precisa apenas de parte da planilha.

## Etapa 4 – Definir opções de cópia (preservar copy worksheet pivot table)

O Aspose.Cells oferece um objeto `CopyOptions` que controla o que é colado. Para manter a tabela dinâmica, gráficos e fórmulas, definimos `PasteType.All` e habilitamos `PasteSpecial`.

```csharp
CopyOptions copyOptions = new CopyOptions
{
    PasteType = PasteType.All,   // Copy everything: values, formats, objects
    PasteSpecial = true          // Enable special paste to retain pivot tables
};
```

*Explicação:* `PasteType.All` é a opção mais inclusiva, enquanto `PasteSpecial` indica ao motor que trate objetos complexos — como tabelas dinâmicas — adequadamente. Pular esta etapa é uma armadilha comum; a planilha copiada perderia seus recursos interativos.

## Etapa 5 – Copiar linhas e colunas (copy columns between sheets)

Agora vem a parte pesada: mover realmente os dados. Usaremos `CopyRows` e `CopyColumns` para lidar com **copy columns between sheets**. Fazer ambos garante que células mescladas e larguras de coluna sejam preservadas.

```csharp
// Copy rows from the source to the destination sheet
sourceSheet.Cells.CopyRows(
    sourceRange.StartRow,
    sourceRange.EndRow,
    copySheet.Cells,
    destinationRange.StartRow,
    copyOptions);

// Copy columns from the source to the destination sheet
sourceSheet.Cells.CopyColumns(
    sourceRange.StartColumn,
    sourceRange.EndColumn,
    copySheet.Cells,
    destinationRange.StartColumn,
    copyOptions);
```

*O que está acontecendo:* `CopyRows` move os dados linha a linha, enquanto `CopyColumns` faz o mesmo coluna a coluna. Executar ambos garante que todo o bloco retangular seja duplicado, o que é essencial quando você precisa **copy columns between sheets** que têm larguras de coluna diferentes ou colunas ocultas.

## Etapa 6 – Salvar a pasta de trabalho

Finalmente, escreva as alterações de volta ao disco. Esta etapa completa o processo de **how to copy worksheet**.

```csharp
// Save the workbook with the newly copied sheet
workbook.Save(destinationPath);
```

*Dica de verificação:* Abra `Destination.xlsx` e verifique se a planilha `"Copy"` está idêntica à original, as tabelas dinâmicas funcionam e as larguras das colunas correspondem. Se algo parecer errado, revise as configurações de `CopyOptions`.

## Casos de borda e variações comuns

### Copiando várias planilhas

Se você precisar duplicar várias planilhas, envolva a lógica acima em um loop `foreach`:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    Worksheet newWs = workbook.Worksheets.Add(ws.Name + "_Copy");
    // Re‑use sourceRange/destinationRange or calculate per sheet
    // Then call CopyRows/CopyColumns as shown earlier
}
```

### Preservando fórmulas entre diferentes pastas de trabalho

Quando as pastas de trabalho de origem e destino têm intervalos nomeados diferentes, defina `copyOptions` para `PasteType.Formulas` além de `All`:

```csharp
copyOptions.PasteType = PasteType.All | PasteType.Formulas;
```

### Grandes intervalos e desempenho

Para conjuntos de dados massivos (centenas de milhares de linhas), considere usar apenas `CopyRows` e pular `CopyColumns` se as larguras de coluna não forem críticas. Isso pode economizar alguns segundos.

## Exemplo completo em funcionamento

Abaixo está o programa completo, pronto‑para‑executar, que incorpora tudo o que discutimos. Cole-o em um aplicativo de console, ajuste os caminhos dos arquivos e pressione **F5**.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // ---------- Step 1: Load the source workbook ----------
        string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
        string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // ---------- Step 2: Add a new worksheet (add new worksheet code) ----------
        Worksheet sourceSheet = workbook.Worksheets[0];
        Worksheet copySheet = workbook.Worksheets.Add("Copy");

        // ---------- Step 3: Define the copy cell range ----------
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };
        CellArea destinationRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };

        // ---------- Step 4: Set copy options (preserve copy worksheet pivot table) ----------
        CopyOptions copyOptions = new CopyOptions
        {
            PasteType = PasteType.All,
            PasteSpecial = true
        };

        // ---------- Step 5: Copy rows and columns (copy columns between sheets) ----------
        sourceSheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            copySheet.Cells,
            destinationRange.StartRow,
            copyOptions);

        sourceSheet.Cells.CopyColumns(
            sourceRange.StartColumn,
            sourceRange.EndColumn,
            copySheet.Cells,
            destinationRange.StartColumn,
            copyOptions);

        // ---------- Step 6: Save the workbook ----------
        workbook.Save(destinationPath);
    }
}
```

**Resultado esperado:** Ao abrir `Destination.xlsx` aparece uma planilha chamada **Copy** que espelha a primeira planilha de `Source.xlsx` — incluindo quaisquer tabelas dinâmicas, formatação e larguras de coluna. O arquivo original permanece intacto.

## Perguntas Frequentes

**Q: Isso funciona com arquivos .xlsx criados pelo Excel 2019?**  
A: Absolutamente. O Aspose.Cells suporta todos os formatos modernos do Excel, portanto o mesmo código funciona para arquivos `.xlsx`, `.xlsm` e até mesmo os mais antigos `.xls`.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}