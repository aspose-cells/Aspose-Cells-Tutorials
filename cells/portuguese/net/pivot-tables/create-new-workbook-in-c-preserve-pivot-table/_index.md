---
category: general
date: 2026-02-15
description: Crie uma nova planilha em C# e copie uma tabela dinâmica sem perder sua
  definição. Aprenda como copiar linhas, preservar a tabela dinâmica e duplicar a
  tabela dinâmica facilmente.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- duplicate pivot table
language: pt
og_description: Criar nova pasta de trabalho em C# e copiar uma tabela dinâmica preservando
  sua definição. Guia passo a passo para desenvolvedores.
og_title: Criar Nova Pasta de Trabalho em C# – Preservar Tabela Dinâmica
tags:
- Aspose.Cells
- C#
- Excel automation
title: Criar nova pasta de trabalho em C# – Preservar tabela dinâmica
url: /pt/net/pivot-tables/create-new-workbook-in-c-preserve-pivot-table/
---

iar nova pasta de trabalho**.

Proceed.

Also "Aspose.Cells" keep.

"Pro tip" keep maybe translate "Dica profissional". Keep bold? It's a blockquote.

Image alt: "Create new workbook with copied pivot table" translate to "Criar nova pasta de trabalho com tabela dinâmica copiada". Title attribute also.

Step headings: "Step 1 – Create New Workbook and Load the Source File" translate.

Code block placeholders remain.

List items etc.

In tables, translate column headings and content.

Make sure to keep markdown formatting.

Now produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Nova Pasta de Trabalho em C# – Preservar Pivot Table

Já precisou **criar nova pasta de trabalho** em C# que contenha uma cópia exata de uma **pivot table** de outro arquivo? Você não está sozinho. Em muitos pipelines de relatórios a **pivot table** é o coração da análise, e perder sua definição ao mover os dados é um pesadelo.

A boa notícia? Com algumas linhas de código do Aspose.Cells você pode copiar linhas — incluindo a **pivot table** — para uma pasta de trabalho nova e manter tudo intacto. A seguir, você verá **como copiar linhas**, **preservar a pivot table** e até **duplicar a pivot table** entre arquivos sem quebrar fórmulas ou cache.

## O Que Este Tutorial Cobre

Neste guia vamos percorrer:

1. Carregar a pasta de trabalho fonte que já contém uma **pivot table**.  
2. **Criar nova pasta de trabalho** para o destino.  
3. Usar `CopyRows` para transferir o intervalo que contém a **pivot table**.  
4. Salvar o resultado garantindo que a **pivot table** continue funcional.  

Nenhuma documentação externa necessária — apenas o código, o porquê e algumas dicas práticas que você pode colar direto no seu projeto.

> **Dica profissional:** Aspose.Cells funciona com .NET Core, .NET Framework e até Xamarin, então o mesmo trecho roda onde você precisar.

---

![Criar nova pasta de trabalho com tabela dinâmica copiada](/images/create-new-workbook-pivot.png "criar nova pasta de trabalho com tabela dinâmica copiada")

## Etapa 1 – Criar Nova Pasta de Trabalho e Carregar o Arquivo Fonte

A primeira coisa que fazemos é **criar nova pasta de trabalho**. Uma mantém os dados originais, a outra receberá o intervalo copiado.

```csharp
using Aspose.Cells;

// Load the source workbook that already contains a pivot table
var sourceWorkbook = new Workbook(@"C:\Data\source.xlsx");

// Create an empty workbook that will become the destination
var destinationWorkbook = new Workbook();
```

*Por que isso importa:*  
`Workbook` é o ponto de entrada para qualquer manipulação de Excel no Aspose.Cells. Ao instanciar uma pasta de trabalho limpa garantimos um ponto de partida sem estilos ocultos ou planilhas indesejadas que possam interferir depois.

## Etapa 2 – Como Copiar Linhas Incluindo uma Pivot Table

Agora vem o cerne do problema: **como copiar linhas** que encapsulam a **pivot table** sem achatá‑la. O método `CopyRows` faz exatamente isso.

```csharp
// Copy the first 20 rows (adjust as needed) from the source to the destination
// Parameters: startRow, totalRows, targetCells, targetStartRow
sourceWorkbook.Worksheets[0].Cells.CopyRows(
    startRow: 0,
    totalRows: 20,
    targetCells: destinationWorkbook.Worksheets[0].Cells,
    targetStartRow: 0);
```

Alguns pontos a observar:

* `startRow` e `totalRows` definem o bloco que contém a **pivot table**.  
* O método copia **ambos** os dados brutos e o cache da **pivot**, de modo que a pasta de trabalho de destino saiba reconstruir a **pivot table** on‑the‑fly.  
* Se sua **pivot** começar mais abaixo na planilha, basta alterar os índices — não é necessário chamar outra API.

> **Pergunta comum:** *A **pivot** copiada perderá a referência aos dados de origem?*  
> Não. Aspose.Cells incorpora o cache diretamente na planilha, então a **pivot** torna‑se autônoma no novo arquivo.

## Etapa 3 – Preservar a Pivot Table ao Salvar o Destino

Depois que as linhas são copiadas, a **pivot table** vive na pasta de trabalho de destino exatamente como estava na fonte. Salvar o arquivo é simples.

```csharp
// Save the destination workbook; the pivot table remains functional
destinationWorkbook.Save(@"C:\Data\destination.xlsx");
```

Ao abrir `destination.xlsx` no Excel, você verá a **pivot table** pronta para atualizar. O comportamento de **preservar a pivot table** é automático porque o cache viajou junto com as linhas.

### Verificando o Resultado

Abra o arquivo e:

1. Clique na **pivot table**.  
2. Observe que a lista de campos aparece — isso indica que o cache está intacto.  
3. Tente atualizar; os dados são recarregados sem erros.

Se encontrar um erro *#REF!*, verifique se o intervalo copiado inclui as linhas de cache ocultas (geralmente logo após os dados visíveis).

## Etapa 4 – Duplicar a Pivot Table em Múltiplas Pastas de Trabalho (Opcional)

Às vezes você precisa da mesma **pivot** em vários relatórios. O padrão que acabamos de usar escala bem — basta repetir a cópia para cada nova pasta de trabalho.

```csharp
string[] targets = {
    @"C:\Reports\Q1.xlsx",
    @"C:\Reports\Q2.xlsx",
    @"C:\Reports\Q3.xlsx"
};

foreach (var path in targets)
{
    var wb = new Workbook(); // fresh workbook each loop
    sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 20, wb.Worksheets[0].Cells, 0);
    wb.Save(path);
}
```

Este trecho **duplica a pivot table** três vezes com um único loop. Ajuste o array `targets` para combinar com seu cronograma de relatórios.

### Casos Limite a Considerar

| Situação | O Que Observar | Solução |
|-----------|-------------------|-----|
| Pivot usa fonte de dados externa | O cache pode referenciar uma conexão que não existe na nova máquina | Incorpore a fonte de dados ou recrie a conexão na pasta de trabalho de destino |
| Pivot muito grande ( > 100 k linhas ) | `CopyRows` pode consumir muita memória | Use `CopyRows` em blocos ou considere `Copy` com `PasteOptions` para limitar o uso de memória |
| Planilha tem linhas/colunas ocultas | Linhas de cache ocultas podem ser puladas se você copiar apenas linhas visíveis | Sempre copie o intervalo exato de linhas que contém o cache, não apenas a área visível |

## Exemplo Completo

Juntando tudo, aqui está um programa autocontido que você pode colocar em um aplicativo console.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook (contains the original pivot)
            var sourcePath = @"C:\Data\source.xlsx";
            var sourceWorkbook = new Workbook(sourcePath);

            // 2️⃣ Prepare destination workbook
            var destinationWorkbook = new Workbook();

            // 3️⃣ Copy rows that include the pivot (adjust range as needed)
            sourceWorkbook.Worksheets[0].Cells.CopyRows(
                startRow: 0,
                totalRows: 20,
                targetCells: destinationWorkbook.Worksheets[0].Cells,
                targetStartRow: 0);

            // 4️⃣ Save – the pivot table is preserved
            var destPath = @"C:\Data\destination.xlsx";
            destinationWorkbook.Save(destPath);

            Console.WriteLine("Pivot table successfully copied!");
        }
    }
}
```

Execute o programa, abra `destination.xlsx` e você verá a mesma **pivot table** pronta para segmentar seus dados. Nenhuma recriação manual necessária.

---

## Conclusão

Acabamos de mostrar como **criar nova pasta de trabalho** em C# e **copiar a pivot table** mantendo todas as configurações vivas. Usando `CopyRows` você obtém uma forma confiável de **preservar a pivot table**, responde à antiga pergunta “**como copiar linhas**” e ainda **duplica a pivot table** em múltiplos relatórios com código mínimo.

Próximos passos? Experimente mudar o intervalo copiado para incluir gráficos que referenciam a mesma **pivot**, ou teste `PasteOptions` para manter a formatação exatamente. O mesmo padrão funciona para outros objetos do Aspose.Cells, como tabelas e intervalos nomeados, então sinta‑se à vontade para expandir.

Tem um caso especial — talvez uma **pivot** que puxa de um banco de dados externo, ou uma pasta de trabalho que vive na nuvem? Deixe um comentário abaixo, e vamos resolver juntos. Feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}