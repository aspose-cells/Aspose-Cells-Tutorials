---
category: general
date: 2026-03-01
description: Criar uma nova pasta de trabalho e copiar a planilha para a pasta de
  trabalho com uma tabela dinâmica. Aprenda como exportar a tabela dinâmica, copiar
  a planilha e copiar a tabela dinâmica em C#.
draft: false
keywords:
- create new workbook
- copy worksheet to workbook
- export pivot table
- how to copy sheet
- how to copy pivot
language: pt
og_description: Crie uma nova pasta de trabalho em C# e copie a planilha para a pasta
  de trabalho preservando a tabela dinâmica. Guia passo a passo com código completo.
og_title: Criar Nova Pasta de Trabalho – Copiar Planilha e Tabela Dinâmica em C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Criar Nova Pasta de Trabalho – Como Copiar uma Planilha com uma Tabela Dinâmica
url: /pt/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Nova Pasta de Trabalho – Copiar Planilha & Tabela Dinâmica em C#

Já precisou **create new workbook** que contenha uma tabela dinâmica pronta sem reconstruí‑la do zero? Você não está sozinho. Em muitos cenários de relatórios você tem um arquivo mestre (`src.xlsx`) com uma tabela dinâmica complexa, e deseja enviar uma cópia limpa (`dest.xlsx`) para um cliente ou outro sistema. A boa notícia? Você pode fazer isso em apenas duas linhas de C# — e este guia mostrará exatamente como.

Vamos percorrer todo o processo: carregar a pasta de trabalho de origem, copiar a primeira planilha (que contém a tabela dinâmica) e salvá‑la como uma nova pasta de trabalho. Ao final você saberá **how to copy sheet** que contém uma tabela dinâmica, como **export pivot table** dados se precisar, e ainda alguns truques para casos especiais, como copiar para um arquivo existente.

## Pré-requisitos

- .NET 6.0 ou posterior (qualquer versão recente funciona)
- Aspose.Cells for .NET (versão de avaliação gratuita ou licenciada) – esta biblioteca fornece a classe `Workbook` usada abaixo.
- Um arquivo Excel de origem (`src.xlsx`) que já contém uma tabela dinâmica na sua primeira planilha.

Se você ainda não tem o Aspose.Cells, adicione-o via NuGet:

```bash
dotnet add package Aspose.Cells
```

É isso—sem COM interop extra, sem Excel instalado no servidor.

## O Que Este Tutorial Aborda

- **Create new workbook** de uma planilha existente que contém uma tabela dinâmica.
- **Copy worksheet to workbook** preservando todas as definições da tabela dinâmica.
- **Export pivot table** dados para um DataTable (opcional).
- Armadilhas comuns ao usar **how to copy pivot** em diferentes ambientes.
- Um exemplo completo e executável que você pode inserir em um aplicativo console.

---

## Etapa 1: Carregar a Pasta de Trabalho de Origem (How to Copy Sheet)

A primeira coisa que você faz é abrir a pasta de trabalho que contém a tabela dinâmica. Usar Aspose.Cells torna isso simples porque lê o arquivo na memória sem iniciar o Excel.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // Path to the source workbook that holds the pivot
        string srcPath = @"YOUR_DIRECTORY\src.xlsx";

        // Load the workbook – this is where we **create new workbook** later
        Workbook sourceWorkbook = new Workbook(srcPath);
```

> **Por que isso importa:** Carregar o arquivo valida que a tabela dinâmica existe e lhe dá acesso à coleção de planilhas. Se o arquivo estiver corrompido, `Workbook` lança uma exceção clara, poupando‑o de resultados misteriosos mais tarde.

## Etapa 2: Copiar a Planilha para uma Nova Pasta de Trabalho (Copy Worksheet to Workbook)

Agora realmente **copy worksheet to workbook**. O método `CopyTo` do Aspose.Cells clona a planilha inteira — incluindo fórmulas, formatação e cache da tabela dinâmica — em um novo arquivo.

```csharp
        // Destination path for the new workbook
        string destPath = @"YOUR_DIRECTORY\dest.xlsx";

        // Copy the first worksheet (index 0) which contains the pivot
        sourceWorkbook.Worksheets[0].CopyTo(destPath);
```

> **Dica profissional:** `CopyTo` cria uma nova pasta de trabalho nos bastidores, portanto você não precisa instanciar outro objeto `Workbook`. Isso mantém o uso de memória baixo e garante que a definição da tabela dinâmica permaneça intacta.

## Etapa 3: Verificar a Tabela Dinâmica Copiada (How to Copy Pivot)

Depois que a cópia termina, é uma boa ideia abrir o novo arquivo e confirmar que a tabela dinâmica ainda funciona. Você pode fazer isso programaticamente ou simplesmente abri‑lo no Excel.

```csharp
        // Optional: Load the destination workbook to verify
        Workbook destWorkbook = new Workbook(destPath);
        Worksheet copiedSheet = destWorkbook.Worksheets[0];

        // Find the first pivot table on the copied sheet
        PivotTable pivot = copiedSheet.PivotTables[0];

        Console.WriteLine($"Pivot name: {pivot.Name}");
        Console.WriteLine($"Data source range: {pivot.DataSource}");
        Console.WriteLine($"Number of rows in pivot cache: {pivot.CacheDefinition.RecordCount}");
    }
}
```

Executar o programa imprime algo como:

```
Pivot name: PivotTable1
Data source range: A1:D100
Number of rows in pivot cache: 100
```

Se você vir esses valores, a etapa **how to copy pivot** foi bem‑sucedida.

## Etapa 4: (Opcional) Exportar Dados da Tabela Dinâmica para um DataTable

Às vezes você precisa dos números brutos da tabela dinâmica sem abrir o Excel. Aspose.Cells permite extrair os dados da tabela dinâmica para um `DataTable` — perfeito para processamento adicional ou respostas de API.

```csharp
        // Export pivot data to a DataTable
        DataTable pivotData = pivot.ExportDataTable(pivot.RowFields[0].Name, 
                                                   pivot.ColumnFields[0].Name,
                                                   true);

        // Display a few rows in the console
        foreach (DataRow row in pivotData.Rows)
        {
            Console.WriteLine(string.Join("\t", row.ItemArray));
        }
```

> **Por que você pode querer isso:** Exportar permite que você **export pivot table** o conteúdo para um banco de dados, payload JSON ou qualquer outro formato sem copiar‑colar manual.

## Etapa 5: Casos de Borda & Armadilhas Comuns

### Copiando para uma Pasta de Trabalho Existente

Se você precisar **copy worksheet to workbook** que já contém outras planilhas, use a sobrecarga que recebe uma instância `Workbook` de destino:

```csharp
        Workbook targetWorkbook = new Workbook(); // empty workbook
        sourceWorkbook.Worksheets[0].CopyTo(targetWorkbook);
        targetWorkbook.Save(@"YOUR_DIRECTORY\combined.xlsx");
```

### Preservando Fontes de Dados Externas

Tabelas dinâmicas que puxam de conexões externas (por exemplo, Power Query) podem perder o vínculo após a cópia. Nesses casos, defina `pivot.RefreshDataOnOpen = true` antes de salvar:

```csharp
        pivot.RefreshDataOnOpen = true;
```

### Arquivos Grandes & Desempenho

Para arquivos maiores que 50 MB, considere habilitar `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;` para reduzir a pressão de memória.

---

![criar nova pasta de trabalho – copiando uma planilha com uma tabela dinâmica](https://example.com/images/create-new-workbook.png "Criar nova pasta de trabalho")

*Texto alternativo da imagem: criar nova pasta de trabalho – copiando uma planilha com uma tabela dinâmica*

---

## Exemplo Completo em Funcionamento (Todas as Etapas Combinadas)

Abaixo está o aplicativo console completo, pronto‑para‑executar. Copie‑e‑cole em um novo `.csproj` e pressione **F5**.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace CopyPivotDemo
{
    class Program
    {
        static void Main()
        {
            // ==============================
            // 1️⃣ Load the source workbook
            // ==============================
            string srcPath = @"YOUR_DIRECTORY\src.xlsx";
            Workbook sourceWorkbook = new Workbook(srcPath);

            // ==============================
            // 2️⃣ Copy the first worksheet (pivot) to a new workbook
            // ==============================
            string destPath = @"YOUR_DIRECTORY\dest.xlsx";
            sourceWorkbook.Worksheets[0].CopyTo(destPath);

            // ==============================
            // 3️⃣ Verify the copied pivot (how to copy pivot)
            // ==============================
            Workbook destWorkbook = new Workbook(destPath);
            Worksheet copiedSheet = destWorkbook.Worksheets[0];
            PivotTable pivot = copiedSheet.PivotTables[0];

            Console.WriteLine($"Pivot name: {pivot.Name}");
            Console.WriteLine($"Data source range: {pivot.DataSource}");
            Console.WriteLine($"Cache rows: {pivot.CacheDefinition.RecordCount}");

            // ==============================
            // 4️⃣ (Optional) Export pivot data
            // ==============================
            if (pivot.RowFields.Count > 0 && pivot.ColumnFields.Count > 0)
            {
                DataTable dt = pivot.ExportDataTable(
                    pivot.RowFields[0].Name,
                    pivot.ColumnFields[0].Name,
                    true);

                Console.WriteLine("\n--- Pivot Data Preview ---");
                foreach (DataRow row in dt.Rows)
                {
                    Console.WriteLine(string.Join("\t", row.ItemArray));
                }
            }

            Console.WriteLine("\nDone! New workbook created at: " + destPath);
        }
    }
}
```

### Resultado Esperado

- `dest.xlsx` aparece em `YOUR_DIRECTORY`.
- A primeira planilha parece exatamente com a original, completa com a tabela dinâmica.
- Executar o console imprime metadados da tabela dinâmica e uma pequena pré‑visualização dos dados, confirmando que a cópia foi bem‑sucedida.

---

## Conclusão

Agora você sabe como **create new workbook** copiando uma planilha que contém uma tabela dinâmica, como **copy worksheet to workbook**, e até como **export pivot table** dados para processamento posterior. Seja construindo um serviço de relatórios, automatizando a distribuição de Excel, ou apenas precisando de uma maneira rápida de duplicar uma tabela dinâmica, as etapas acima fornecem uma solução confiável e pronta para produção.

**Próximos passos** que você pode explorar:

- Combine várias planilhas (use `CopyTo` repetidamente) – perfeito para empacotar um relatório completo.
- Ajuste as configurações de atualização do cache da tabela dinâmica quando os dados de origem mudarem.
- Use técnicas de **how to copy sheet** para duplicar gráficos, imagens ou módulos VBA.
- Aprofunde‑se no `WorkbookDesigner` do Aspose.Cells para geração de relatórios baseada em modelos.

Experimente, ajuste os caminhos e veja como é fácil distribuir pastas de trabalho limpas e prontas para tabelas dinâmicas. Tem perguntas sobre casos de borda ou licenciamento? Deixe um comentário abaixo, e feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}