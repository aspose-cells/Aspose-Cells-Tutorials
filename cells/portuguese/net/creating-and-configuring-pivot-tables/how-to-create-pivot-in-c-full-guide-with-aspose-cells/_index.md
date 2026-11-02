---
category: general
date: 2026-03-27
description: Como criar uma tabela dinâmica em C# usando Aspose.Cells – aprenda a
  adicionar dados, habilitar a atualização e salvar a planilha como xlsx em um único
  tutorial.
draft: false
keywords:
- how to create pivot
- save workbook as xlsx
- how to enable refresh
- how to add data
- generate excel file c#
language: pt
og_description: Como criar uma tabela dinâmica em C# com Aspose.Cells. Este guia mostra
  como adicionar dados, habilitar a atualização e salvar a pasta de trabalho como
  xlsx.
og_title: Como criar Tabela Dinâmica em C# – Tutorial completo do Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel automation
title: Como criar Tabela Dinâmica em C# – Guia completo com Aspose.Cells
url: /pt/net/creating-and-configuring-pivot-tables/how-to-create-pivot-in-c-full-guide-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Criar Tabelas Dinâmicas em C# – Tutorial Completo do Aspose.Cells

Já se perguntou **como criar tabelas dinâmicas** em C# sem lidar com COM interop? Você não está sozinho. Em muitas aplicações orientadas a dados precisamos de uma maneira rápida de transformar números de vendas brutos em um resumo organizado, e o Aspose.Cells torna isso muito simples.  

Neste tutorial vamos percorrer cada passo: adicionar dados, construir a tabela dinâmica, habilitar a atualização automática e, finalmente, **salvar a pasta de trabalho como xlsx** para que seus usuários a abram no Excel instantaneamente. Ao final, você terá um arquivo pronto‑para‑uso `PivotRefresh.xlsx` e uma compreensão sólida do porquê de cada linha.

## Pré‑requisitos

- .NET 6+ (ou .NET Framework 4.7.2 ou superior) – qualquer runtime recente funciona.
- Aspose.Cells for .NET – você pode obtê‑lo via NuGet (`Install-Package Aspose.Cells`).
- Familiaridade básica com a sintaxe C# – não é necessário conhecimento profundo de Excel.

> **Dica profissional:** Se você estiver em uma máquina corporativa, certifique‑se de que a licença Aspose está aplicada; caso contrário, um marca‑d’água aparecerá no arquivo gerado.

## Etapa 1 – Como Adicionar Dados a uma Nova Pasta de Trabalho

Antes que uma tabela dinâmica exista, deve haver uma tabela de origem. Criaremos uma pasta de trabalho nova, nomearemos a primeira planilha *SalesData* e inseriremos algumas linhas que simulam um dump de vendas real.

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and grab the default sheet
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        // 2️⃣ Write column headers
        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // 3️⃣ Insert a sample row – add more rows as your scenario demands
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);
```

**Por que isso importa:**  
- Usar `PutValue` define automaticamente o tipo da célula, evitando problemas de incompatibilidade entre string e número mais tarde.  
- Definir cabeçalhos na linha 1 fornece ao mecanismo da tabela dinâmica algo para referenciar ao mapear os campos.

## Etapa 2 – Criar uma Planilha que Hospedará a Tabela Dinâmica

Uma tabela dinâmica vive em sua própria planilha, mantendo os dados de origem limpos e o relatório organizado.

```csharp
        // 4️⃣ Add a dedicated sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");
```

> **E se você já tem uma planilha?** Basta referenciá‑la pelo índice (`workbook.Worksheets["MySheet"]`) em vez de adicionar uma nova.

## Etapa 3 – Definir o Intervalo de Origem (Como Adicionar Dados → Definir Intervalo)

O Aspose.Cells precisa de um `CellArea` ou de uma string de intervalo que englobe cabeçalhos e dados. Aqui assumimos no máximo 100 linhas; ajuste conforme necessário.

```csharp
        // 5️⃣ Build the source range (A1:D100 covers headers + up to 99 data rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");
```

**Caso extremo:** Se seu conjunto de dados for dinâmico, você pode calcular a última linha usada com `salesDataSheet.Cells.MaxDataRow` e montar o intervalo de acordo.

## Etapa 4 – Como Criar a Tabela Dinâmica – Inserir a Tabela Dinâmica

Agora vem a parte divertida: instruímos o Aspose.Cells a criar uma tabela dinâmica vinculada ao intervalo que acabamos de definir.

```csharp
        // 6️⃣ Insert the pivot table at cell A3 of the pivot sheet
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];
```

Observe a referência no estilo de fórmula (`=SalesData!A1:D100`). Essa é a mesma sintaxe que você digitária no Excel, o que torna a API intuitiva.

## Etapa 5 – Configurar Campos de Linha, Coluna e Dados (Como Adicionar Dados → Campos)

Colocaremos *Region* nas linhas, *Product* nas colunas e somaremos tanto *Units* quanto *Revenue*.

```csharp
        // 7️⃣ Set up row, column, and data fields
        pivotTable.RowFields.Add(0); // 0 = first column => Region
        pivotTable.ColumnFields.Add(1); // 1 = second column => Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);
```

**Por que esses índices?**  
O Aspose.Cells indexa colunas a partir de 0, então `0` aponta para *Region*. O método `DataFields.Add` permite renomear o campo (ex.: “Sum of Units”) e escolher um tipo de agregação – `Sum` é o mais comum para dados numéricos.

## Etapa 6 – Como Habilitar Atualização – Tornar a Tabela Dinâmica Auto‑Atualizável ao Abrir

Se os dados de origem mudarem depois, você provavelmente quer que a tabela dinâmica reflita essas alterações automaticamente. É aqui que `RefreshDataOnOpen` brilha.

```csharp
        // 8️⃣ Turn on automatic refresh when the file is opened
        pivotTable.RefreshDataOnOpen = true;
```

> **Observação:** Essa flag funciona apenas quando a pasta de trabalho é aberta no Excel; ela não recalcula dentro do Aspose.Cells a menos que você chame `pivotTable.RefreshData()` manualmente.

## Etapa 7 – Salvar a Pasta de Trabalho como XLSX (Como Salvar Pasta de Trabalho como XLSX)

Por fim, persistimos o arquivo no disco. O formato `.xlsx` é o tipo de arquivo Excel moderno, baseado em zip, que funciona em qualquer lugar.

```csharp
        // 9️⃣ Save the workbook – this also satisfies the “save workbook as xlsx” requirement
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

Executar o programa gera um arquivo chamado **PivotRefresh.xlsx** na pasta de execução. Abra‑o no Excel e você verá uma tabela dinâmica bem organizada com linhas *Region*, colunas *Product* e valores somados de *Units* e *Revenue*. Como habilitamos a atualização automática, quaisquer edições que você fizer na planilha *SalesData* atualizarão a tabela dinâmica na próxima vez que abrir a pasta de trabalho.

### Saída Esperada

| Region | Widget | Gadget | … |
|--------|--------|--------|---|
| East   | 120    | 0      |   |
| West   | 0      | 85     |   |
| **Grand Total** | **120** | **85** |   |

*(Os números variarão de acordo com as linhas que você adicionar.)*

---

## Perguntas Frequentes & Variações

### E se eu precisar de múltiplas tabelas dinâmicas?

Você pode repetir a **Etapa 4** com um nome e localização diferentes. Cada chamada a `PivotTables.Add` retorna um novo índice que pode ser usado para recuperar o objeto da tabela.

### Como mudar a agregação para *Average* em vez de *Sum*?

Substitua `PivotTableDataAggregationType.Sum` por `PivotTableDataAggregationType.Average` nas chamadas `DataFields.Add`.

### Posso estilizar a tabela dinâmica (fontes, cores)?

Sim. Após criar a tabela, você pode acessar a propriedade `Style` ou aplicar formatação de célula ao intervalo que contém a tabela dinâmica. Por exemplo:

```csharp
pivotTable.Style = workbook.Styles[workbook.Styles.Add()];
pivotTable.Style.Font.Color = System.Drawing.Color.DarkBlue;
```

### É possível adicionar mais linhas depois que a pasta de trabalho foi salva?

Absolutamente. Carregue o arquivo com `new Workbook("PivotRefresh.xlsx")`, anexe linhas à planilha *SalesData* e chame `pivotTable.RefreshData()` antes de salvar novamente.

---

## Exemplo Completo (Pronto para Copiar‑Colar)

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // Step 1: Create workbook & add sample data
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // Sample rows – extend as needed
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);

        salesDataSheet.Cells["A3"].PutValue("West");
        salesDataSheet.Cells["B3"].PutValue("Gadget");
        salesDataSheet.Cells["C3"].PutValue(85);
        salesDataSheet.Cells["D3"].PutValue(4250);

        // Step 2: Add sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");

        // Step 3: Define source range (covers up to 100 rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");

        // Step 4: Insert pivot table
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];

        // Step 5: Configure fields
        pivotTable.RowFields.Add(0); // Region
        pivotTable.ColumnFields.Add(1); // Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);

        // Step 6: Enable automatic refresh
        pivotTable.RefreshDataOnOpen = true;

        // Step 7: Save as .xlsx
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

Salve o arquivo, execute-o e abra o **PivotRefresh.xlsx** gerado – você acabou de dominar **como criar tabelas dinâmicas** em C#.

---

## Conclusão

Cobremos **como criar tabelas dinâmicas** programaticamente, como **adicionar dados**, como **habilitar atualização automática** e, por fim, como **salvar a pasta de trabalho como xlsx** usando Aspose.Cells. O código

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}