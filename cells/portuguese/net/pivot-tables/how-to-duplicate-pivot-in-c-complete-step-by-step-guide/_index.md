---
category: general
date: 2026-03-22
description: Aprenda como duplicar uma tabela dinâmica em C# usando Aspose.Cells.
  Este guia também mostra como copiar linhas e carregar uma pasta de trabalho Excel
  em C# para uma automação de Excel fluida ao copiar linhas.
draft: false
keywords:
- how to duplicate pivot
- how to copy rows
- load excel workbook c#
- excel automation copy rows
language: pt
og_description: Como duplicar uma tabela dinâmica em C#? Siga este tutorial conciso
  para carregar a planilha Excel em C#, copiar linhas e dominar a automação do Excel
  copiando linhas.
og_title: Como Duplicar Pivot em C# – Guia Completo
tags:
- C#
- Excel Automation
- Aspose.Cells
title: Como Duplicar Pivot em C# – Guia Completo Passo a Passo
url: /pt/net/pivot-tables/how-to-duplicate-pivot-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Duplicar Pivot em C# – Guia Completo Passo a Passo

Já se perguntou **como duplicar pivot** tabelas programaticamente sem arrastá‑las manualmente no Excel? Você não é o único. Em muitos pipelines de relatórios o mesmo layout de pivot é necessário em um novo conjunto de linhas, e fazer isso manualmente é uma perda de tempo.  

A boa notícia? Com algumas linhas de C# você pode carregar uma pasta de trabalho Excel, definir a área que contém o pivot e **como copiar linhas** para que o pivot apareça em um novo local — tudo em uma execução automatizada. Neste tutorial também abordaremos os fundamentos de **load excel workbook c#** e daremos uma base sólida para tarefas de **excel automation copy rows**.

> **O que você levará consigo**  
> • Um exemplo completo e executável que duplica uma tabela pivot.  
> • Uma explicação do porquê cada linha importa.  
> • Dicas para lidar com casos extremos como planilhas ocultas ou múltiplos pivots.

---

## Pré-requisitos

Before we dive in, make sure you have:

- **.NET 6.0** (ou qualquer versão recente do .NET) instalado.  
- **Aspose.Cells for .NET** – a biblioteca que usaremos para manipular arquivos Excel. Você pode obtê‑la via NuGet:  

```bash
dotnet add package Aspose.Cells
```  

- Uma pasta de trabalho fonte (`Source.xlsx`) que já contém uma tabela pivot no intervalo **A1:J20** (o intervalo que iremos duplicar).  
- Familiaridade básica com a sintaxe C# – nada sofisticado, apenas as declarações `using` habituais e o método `Main`.

Se algum desses itens lhe for desconhecido, faça uma pausa e instale o pacote; o restante do guia assume que a biblioteca está pronta para uso.

![Ilustração de como duplicar pivot em C# usando Aspose.Cells](https://example.com/duplicate-pivot.png "ilustração de como duplicar pivot em C#")

*Texto alternativo da imagem: "exemplo de como duplicar pivot em C# mostrando linhas de origem e linhas de pivot duplicadas".*

## Etapa 1: Carregar Pasta de Trabalho Excel C# – Abrindo o Arquivo

A primeira coisa que você precisa fazer quando deseja **load excel workbook c#** é criar uma instância `Workbook` apontando para o seu arquivo. Esse objeto dá acesso a todas as planilhas, células e pivots dentro do arquivo.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 1: Load the source workbook
        string sourcePath = @"C:\Data\Source.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // From here on we can work with worksheets, ranges, and pivots.
```

**Por que isso importa:**  
`Workbook` abstrai todo o arquivo Excel em um modelo em memória. Sem carregá‑lo primeiro, você não pode inspecionar a localização do pivot ou copiar linhas. Além disso, o construtor detecta automaticamente o formato do arquivo (XLS, XLSX, CSV, etc.), portanto não é necessário código extra para detecção de formato.

## Etapa 2: Como Copiar Linhas – Definindo a Área do Pivot

Agora que a pasta de trabalho está em memória, precisamos dizer ao Aspose.Cells quais linhas contêm o pivot. No nosso exemplo o pivot está em **A1:J20**, que corresponde às linhas **0‑19** (indexação baseada em zero). Envolvemos isso em uma estrutura `CellArea`.

```csharp
        // Step 2: Define the cell area that contains the pivot table (A1:J20)
        // Row indices are zero‑based, column indices are also zero‑based.
        CellArea copyRange = new CellArea(startRow: 0, startColumn: 0, endRow: 19, endColumn: 9);
```

**Por que usamos `CellArea`:**  
É uma forma leve de descrever um bloco retangular. Quando você chamar `CopyRows` mais tarde, o método lê esse objeto para saber exatamente quais linhas duplicar. Se precisar ajustar o intervalo (por exemplo, o pivot crescer para a coluna K), basta mudar o valor `endColumn`.

## Etapa 3: Acessar a Planilha de Destino

A maioria das pastas de trabalho tem uma única planilha, mas a API funciona da mesma forma para múltiplas planilhas. Pegue a primeira planilha (índice 0) – é onde o pivot original está.

```csharp
        // Step 3: Get the first worksheet from the workbook
        Worksheet worksheet = workbook.Worksheets[0];
```

**Dica profissional:**  
Se você tem planilhas nomeadas, também pode recuperá‑las pelo nome: `workbook.Worksheets["Sheet1"]`. Isso ajuda a evitar codificação fixa de índices quando a estrutura da pasta de trabalho mudar.

## Etapa 4: Como Copiar Linhas – Duplicando a Tabela Pivot

Eis o coração de **how to duplicate pivot**: copiamos as linhas que contêm o pivot para um novo local. No nosso caso começamos na linha 31 (índice baseado em zero 30). O método `CopyRows` copia *ambos* os dados e o cache subjacente do pivot, de modo que as novas linhas se comportam exatamente como as originais.

```csharp
        // Step 4: Copy the rows of the defined range to a new location (starting at row 31)
        // The third argument is the destination start row (zero‑based).
        worksheet.Cells.CopyRows(copyRange.StartRow, copyRange.EndRow, destinationRow: 30);
```

**O que está acontecendo nos bastidores?**  
`CopyRows` clona cada linha, preservando fórmulas, estilos e definições do pivot. Como o cache do pivot reside ao nível da pasta de trabalho, o pivot duplicado referencia automaticamente a mesma fonte de dados – sem necessidade de configuração extra.

**Caso extremo – linhas ocultas:**  
Se alguma das linhas no intervalo de origem estiver oculta, ela permanecerá oculta após a cópia. Se quiser revelá‑las, chame `worksheet.Rows[destRow].IsHidden = false` após a cópia.

## Etapa 5: Salvar a Pasta de Trabalho – Verificando a Duplicata

Por fim, grave as alterações de volta ao disco. Você pode sobrescrever o arquivo original ou, de forma mais segura, salvar com um novo nome para poder comparar antes/depois.

```csharp
        // Step 5: Save the workbook – the pivot table is now duplicated in the new rows
        string outputPath = @"C:\Data\CopyWithPivot.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine("Pivot duplicated successfully! Check " + outputPath);
    }
}
```

**Resultado esperado:**  
Abra `CopyWithPivot.xlsx`. Você encontrará o pivot original em **A1:J20** e uma cópia idêntica começando em **A31:J50**. Ambos os pivots podem ser atualizados independentemente, e quaisquer segmentações (slicers) vinculadas ao original ainda funcionarão na cópia porque compartilham o mesmo cache.

## Perguntas Frequentes & Variações

### Posso duplicar múltiplos pivots de uma vez?

Com certeza. Percorra todas as tabelas pivot (`worksheet.PivotTables`) e copie o intervalo de cada uma para um destino diferente. Apenas certifique‑se de que os intervalos de destino não se sobreponham.

### E se a pasta de trabalho fonte estiver protegida por senha?

O Aspose.Cells permite abrir um arquivo protegido passando a senha ao construtor `Workbook`:

```csharp
Workbook workbook = new Workbook(sourcePath, new LoadOptions { Password = "mySecret" });
```

### Como copiar linhas sem afetar fórmulas?

Se você precisar apenas dos *valores* (sem fórmulas), use `CopyRows` com a flag `CopyOptions`:

```csharp
worksheet.Cells.CopyRows(sourceStart, sourceEnd, destStart, new CopyOptions { CopyValues = true });
```

### Existe uma forma de copiar linhas para uma *outra* pasta de trabalho?

Sim. Depois de copiar as linhas na planilha de origem, você pode clonar a planilha em outra instância `Workbook` usando `targetWorkbook.Worksheets.AddCopy(worksheet)`.

## Dicas Profissionais para Copiar Linhas com Automação Excel Confiável

- **Valide o intervalo** antes de copiar. Um rápido `if (copyRange.EndRow >= worksheet.Cells.MaxDataRow)` impede erros de fora do intervalo.  
- **Desative o cálculo** enquanto copia grandes intervalos: `workbook.Settings.CalcMode = CalcMode.Manual;` – isso acelera a operação drasticamente.  
- **Dispose objetos** (`workbook.Dispose()`) se estiver processando muitos arquivos em um loop para liberar recursos nativos.  
- **Registre a operação** – especialmente em pipelines de produção – para que você possa rastrear quais arquivos foram processados e detectar falhas cedo.

## Conclusão

Agora você sabe **how to duplicate pivot** tabelas em C# usando Aspose.Cells, e viu o fluxo completo desde **load excel workbook c#** até **excel automation copy rows** e, finalmente, salvar o resultado. O exemplo é autônomo, funciona imediatamente e pode ser estendido para lidar com múltiplos pivots, arquivos protegidos ou cópia entre pastas de trabalho.

Próximos passos? Experimente adaptar o script para:

- Atualizar o pivot duplicado programaticamente (`pivotTable.RefreshData();`).  
- Exportar a área duplicada para um CSV para processamento posterior.  
- Integrar o código em uma API ASP.NET Core para que usuários possam enviar um arquivo e receber instantaneamente a versão com pivot duplicado.

Feliz codificação, e que sua automação Excel seja sempre fluida!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}