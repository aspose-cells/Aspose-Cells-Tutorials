---
category: general
date: 2026-03-29
description: Aprenda a copiar intervalos, copiar tabelas dinâmicas, salvar a pasta
  de trabalho e carregá‑la em C#. Mova tabelas dinâmicas facilmente com código passo
  a passo.
draft: false
keywords:
- how to copy range
- copy pivot tables
- how to save workbook
- how to load workbook
- move pivot table
language: pt
og_description: Como copiar intervalos, copiar tabelas dinâmicas, como salvar a pasta
  de trabalho e como carregar a pasta de trabalho em C#. Mova tabelas dinâmicas sem
  esforço com código claro.
og_title: Como copiar intervalo com tabelas dinâmicas em C# – Guia Completo
tags:
- C#
- Aspose.Cells
- Excel automation
title: Como copiar intervalo com tabelas dinâmicas em C# – Guia completo
url: /pt/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como copiar intervalo com tabelas dinâmicas em C# – Guia Completo

Já se perguntou **como copiar intervalo** que contém uma tabela dinâmica sem quebrar o vínculo com seus dados de origem? Você não está sozinho. Em muitos projetos reais, encontrei esse mesmo obstáculo—arquivos Excel chegam com tabelas dinâmicas sofisticadas, e a necessidade é reposicioná‑las ou duplicar os dados em outro lugar.  

A boa notícia? A solução é bem simples assim que você souber **como carregar a pasta de trabalho**, fazer uma cópia e então **como salvar a pasta de trabalho** novamente. Neste tutorial percorreremos todo o processo, incluindo como **copiar tabelas dinâmicas**, e ainda uma dica rápida sobre **mover tabela dinâmica** caso precise dela em outro local na mesma planilha.

Ao final deste guia você terá um trecho de código C# totalmente funcional que:

1. Carrega um arquivo Excel existente.  
2. Copia um intervalo (incluindo a tabela dinâmica) para um novo local.  
3. Salva a pasta de trabalho modificada em um novo arquivo.

Sem scripts externos, sem manipulação manual—apenas código limpo e reutilizável.

---

## Pré-requisitos

- **.NET 6+** (qualquer versão recente funciona).  
- **Aspose.Cells for .NET** – a biblioteca que fornece `Workbook`, `WorksheetCopyOptions`, etc. Você pode instalá‑la via NuGet:

```bash
dotnet add package Aspose.Cells
```

- Uma pasta de trabalho de entrada (`input.xlsx`) que já contém uma tabela dinâmica no intervalo `A1:G20`.  
- Familiaridade básica com C# e Visual Studio (ou sua IDE favorita).

> **Dica profissional:** Se você estiver usando uma biblioteca Excel diferente (por exemplo, EPPlus), os conceitos são os mesmos—basta trocar as chamadas de API.

---

## Etapa 1 – Como carregar a pasta de trabalho (Configuração Primária)

Antes de podermos copiar qualquer coisa, precisamos trazer o arquivo Excel para a memória.

```csharp
using Aspose.Cells;

// Step 1: Load the source workbook
var sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// Grab the first worksheet – this is where our pivot lives
var sourceWorksheet = sourceWorkbook.Worksheets[0];
```

**Por que isso importa:**  
Carregar a pasta de trabalho fornece um modelo de objetos que você pode manipular. Sem `como carregar a pasta de trabalho` corretamente, qualquer operação de cópia subsequente lançaria uma exceção *FileNotFound* ou *InvalidOperation*.

> **Atenção:** Se o arquivo for grande, considere usar `LoadOptions` com `MemorySetting` para controlar o uso de memória.

---

## Etapa 2 – Como copiar intervalo (incluindo a tabela dinâmica)

Agora vem a estrela do espetáculo: copiar um intervalo que contém uma tabela dinâmica. O método `CopyRange`, combinado com `WorksheetCopyOptions`, faz o trabalho pesado.

```csharp
// Step 2: Copy a range that includes a pivot table to a new location
sourceWorksheet.CopyRange(
    "A1:G20",                                   // Source range
    new WorksheetCopyOptions { CopyPivotTables = true }, // Ensure pivot tables travel with the data
    sourceWorksheet,                           // Destination worksheet (same sheet in this case)
    "A25");                                     // Upper‑left corner of the destination
```

**Por que definimos `CopyPivotTables = true`:**  
Por padrão, copiar um intervalo move apenas as células brutas. O cache da tabela dinâmica permanece, e a tabela dinâmica copiada torna‑se uma tabela estática. Definir `CopyPivotTables` preserva a conexão ao vivo, de modo que a tabela dinâmica duplicada ainda seja atualizada quando seus dados de origem mudarem.

**Caso limite:** Se o intervalo de destino se sobrepõe ao de origem, o Aspose.Cells lançará um `ArgumentException`. Sempre escolha um alvo que não se sobreponha, ou crie uma nova planilha primeiro.

---

## Etapa 3 – Como salvar a pasta de trabalho (Persistir as alterações)

Após a cópia, você desejará gravar as alterações de volta ao disco. É aqui que **como salvar a pasta de trabalho** entra em ação.

```csharp
// Step 3: Save the modified workbook to a new file
sourceWorkbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

**O que acontece nos bastidores:**  
`Save` serializa a pasta de trabalho em memória, incluindo a tabela dinâmica recém‑copiada, em um pacote padrão `.xlsx`. Se precisar de um formato diferente (CSV, PDF, etc.), basta mudar a extensão do arquivo ou usar a sobrecarga que aceita `SaveFormat`.

> **Dica:** Use `Workbook.Save(string, SaveOptions)` se precisar proteger o arquivo com uma senha ou definir outras opções de exportação.

---

## Exemplo Completo Funcional

Juntando tudo, aqui está o programa completo, pronto‑para‑executar:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ How to load workbook
        var sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
        var sourceWorksheet = sourceWorkbook.Worksheets[0];

        // 2️⃣ How to copy range (including pivot tables)
        sourceWorksheet.CopyRange(
            "A1:G20",
            new WorksheetCopyOptions { CopyPivotTables = true },
            sourceWorksheet,
            "A25");

        // 3️⃣ How to save workbook
        sourceWorkbook.Save(@"YOUR_DIRECTORY\output.xlsx");

        Console.WriteLine("✅ Range copied and workbook saved successfully!");
    }
}
```

**Resultado esperado:**  
Abra `output.xlsx`. Você verá a tabela dinâmica original ainda em `A1:G20`, e uma cópia idêntica, totalmente funcional, começando em `A25`. Ambas as tabelas apontam para os mesmos dados de origem, então atualizar uma atualiza a outra.

---

## Perguntas Frequentes & Variações

### Posso **mover tabela dinâmica** em vez de copiá‑la?

Com certeza. Após copiar, basta limpar o intervalo original (ou usar `sourceWorksheet.Cells.ClearRange(0, 0, 19, 6)`) e então renomear o intervalo de destino, se necessário. Isso efetivamente “move” a tabela dinâmica.

### E se a tabela dinâmica usar uma fonte de dados externa?

`CopyPivotTables = true` copia apenas a definição da tabela dinâmica, não a conexão externa em si. Garanta que a pasta de trabalho de destino tenha acesso à mesma fonte de dados, ou recrie a conexão após a cópia.

### Como copio para uma **planilha diferente**?

Just pass the destination worksheet object instead of `sourceWorksheet`:

```csharp
var destWorksheet = sourceWorkbook.Worksheets.Add("CopiedPivot");
sourceWorksheet.CopyRange("A1:G20", new WorksheetCopyOptions { CopyPivotTables = true }, destWorksheet, "A1");
```

### Existe uma maneira de copiar **múltiplos intervalos** de uma vez?

Você pode chamar `CopyRange` repetidamente ou usar `CopyRows`/`CopyColumns` para blocos maiores. Iterar sobre uma lista de strings de endereço é uma abordagem limpa.

---

## Armadilhas Comuns & Dicas Profissionais

- **Tamanho do cache da tabela dinâmica:** Caches grandes podem inflar o tamanho da pasta de trabalho. Se você precisar apenas dos dados exibidos, considere `CopyPivotTables = false` e então use `PivotTable.RefreshData()` no destino.  
- **Caminhos de arquivos:** Use `Path.Combine` para evitar separadores codificados, especialmente em .NET multiplataforma.  
- **Desempenho:** Para pastas de trabalho massivas, envolva a cópia em um `using (var stream = new MemoryStream())` e salve primeiro no stream, depois escreva no disco. Isso reduz a sobrecarga de I/O.

---

## Conclusão

Agora você sabe **como copiar intervalo** que contém uma tabela dinâmica, como **copiar tabelas dinâmicas**, e os passos exatos para **como carregar a pasta de trabalho** e **como salvar a pasta de trabalho** após a operação. Seja para **mover tabela dinâmica** dentro da mesma planilha ou para outra planilha, o padrão permanece o mesmo—carregar, copiar com as opções corretas e salvar.

Experimente com seus próprios arquivos, ajuste o endereço de destino e experimente diferentes configurações de tabelas dinâmicas. Quanto mais você brincar, mais confiante ficará ao automatizar tarefas do Excel em C#.

---

![Diagrama mostrando o intervalo de origem A1:G20 sendo copiado para A25 na mesma planilha – como copiar intervalo com tabelas dinâmicas](/images/how-to-copy-range-diagram.png "como copiar intervalo com tabelas dinâmicas")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}