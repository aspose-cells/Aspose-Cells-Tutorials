---
category: general
date: 2026-03-30
description: Criar pasta de trabalho Excel em C# com formatação de moeda. Aprenda
  como importar um DataTable, adicionar formatação numérica no Excel e aplicar formatação
  de moeda em uma coluna em minutos.
draft: false
keywords:
- create excel workbook c#
- format cells currency
- import datatable to excel
- add number format excel
- apply currency format column
language: pt
og_description: Crie uma planilha Excel em C# e formate instantaneamente as células
  como moeda. Este tutorial passo a passo mostra como importar um DataTable para o
  Excel e adicionar formatação numérica a uma coluna.
og_title: Criar Pasta de Trabalho Excel C# – Guia de Formatação de Moeda
tags:
- Aspose.Cells
- C#
- Excel automation
title: Criar Pasta de Trabalho Excel C# – Aplicar Formato de Moeda e Importar DataTable
url: /pt/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Excel Workbook C# – Aplicar Formato de Moeda e Importar DataTable

Já precisou **create Excel workbook C#** que já pareça um relatório bem elaborado? Talvez você esteja extraindo números de vendas de um banco de dados e queira que a coluna de preço apareça em dólares sem ter que mexer manualmente no Excel. Soa familiar? Você não está sozinho—a maioria dos desenvolvedores encontra esse obstáculo ao automatizar exportações para Excel pela primeira vez.

Neste guia, percorreremos uma solução completa, pronta‑para‑executar, que **creates an Excel workbook C#**, importa um `DataTable` e **formats the Price column as currency**. Ao final, você terá um arquivo chamado `StyledTable.xlsx` que pode abrir e verá números formatados corretamente. Nenhum pós‑processamento adicional é necessário.

> **O que você aprenderá**
> - Como configurar Aspose.Cells em um projeto .NET  
> - Como **import datatable to excel** com um array de estilos  
> - Como **add number format excel** para uma coluna específica  
> - Dicas para lidar com mais colunas ou diferentes localidades  

> **Pré-requisitos**  
> - .NET 6+ (ou .NET Framework 4.6+) instalado  
> - Aspose.Cells for .NET NuGet package (`Install-Package Aspose.Cells`)  
> - Familiaridade básica com C# e DataTables  

---

## Etapa 1: Preparar o DataTable (import datatable to excel)

Primeiro, precisamos de alguns dados de exemplo. Em um aplicativo real, você provavelmente preencheria esta tabela a partir de uma consulta ao banco de dados, mas um exemplo codificado mantém as coisas simples.

```csharp
using System.Data;

// Create a DataTable with two columns: Product (string) and Price (double)
DataTable dataTable = new DataTable();
dataTable.Columns.Add("Product", typeof(string));
dataTable.Columns.Add("Price", typeof(double));

// Add a few rows – you can add as many as you like
dataTable.Rows.Add("Apple", 1.23);
dataTable.Rows.Add("Banana", 0.78);
dataTable.Rows.Add("Cherry", 2.50);
```

*Por que isso importa*: O `DataTable` é a ponte entre seus dados de negócios e o arquivo Excel. Aspose.Cells pode importá‑lo diretamente, preservando nomes de colunas e tipos de dados.

---

## Etapa 2: Criar uma Nova Pasta de Trabalho (create excel workbook c#)

Agora criamos o objeto real do arquivo Excel. Pense nele como a tela em branco que você vai pintar.

```csharp
using Aspose.Cells;

// Instantiate a fresh workbook – this is the core of create excel workbook c#
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0). You could also add more sheets later.
Worksheet worksheet = workbook.Worksheets[0];
```

> **Dica profissional:** Se precisar de várias planilhas, chame `workbook.Worksheets.Add()` e dê a cada uma um nome significativo.

---

## Etapa 3: Definir um Estilo de Moeda (format cells currency)

Aspose.Cells permite criar um objeto `Style` que descreve como as células devem aparecer. Para moeda, usamos o ID de formato numérico embutido 164 (`"$#,##0.00"`).

```csharp
// Create a new style object for the price column
Style priceStyle = workbook.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format "$#,##0.00"
```

*Por que não simplesmente definir a string de formato?* Usar o ID embutido garante compatibilidade entre versões do Excel e evita particularidades específicas de localidade.

---

## Etapa 4: Construir o Array de Estilos (apply currency format column)

Ao importar um `DataTable`, você pode passar um array de objetos `Style` — um por coluna. `null` significa “usar o estilo padrão”. Aqui aplicamos `priceStyle` apenas à segunda coluna.

```csharp
// Column 0 (Product) gets the default style, Column 1 (Price) gets the currency style
Style[] columnStyles = { null, priceStyle };
```

Se mais tarde você adicionar mais colunas, basta estender o array adequadamente. O comprimento de `columnStyles` deve corresponder ao número de colunas que você está importando, caso contrário o Aspose lançará uma exceção.

---

## Etapa 5: Importar o DataTable com Estilos (import datatable to excel)

Agora a mágica acontece — nosso `DataTable` chega à planilha, e a coluna de preço mostra instantaneamente como moeda.

```csharp
// Parameters:
//  - dataTable: source data
//  - true: include column headers
//  - startRow: 0 (top of sheet)
//  - startColumn: 0 (first column)
//  - columnStyles: style array defined above
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

*E se você tiver mais de duas colunas?* Basta expandir `columnStyles` para que cada coluna receba o estilo apropriado (ou `null` para o padrão). Esta é a maneira mais limpa de **add number format excel** seletivamente.

---

## Etapa 6: Salvar a Pasta de Trabalho (create excel workbook c#)

Finalmente, gravamos o arquivo no disco. Escolha qualquer pasta em que você tenha permissão de escrita.

```csharp
// Save the workbook as an XLSX file
workbook.Save("YOUR_DIRECTORY/StyledTable.xlsx");
```

Abra `StyledTable.xlsx` no Excel e você deverá ver:

| Product | Price |
|---------|-------|
| Apple   | $1.23 |
| Banana  | $0.78 |
| Cherry  | $2.50 |

A coluna **Price** já está formatada como moeda — nenhum passo extra necessário.

---

## Casos de Borda e Variações

### Mais Colunas, Formatos Diferentes

Se precisar **format cells currency** para várias colunas (por exemplo, Cost, Tax, Total), crie um `Style` separado para cada uma e preencha `columnStyles` adequadamente:

```csharp
Style costStyle = workbook.CreateStyle();
costStyle.Number = 164; // currency

Style taxStyle = workbook.CreateStyle();
taxStyle.Number = 164;

// Assuming columns: Product, Cost, Tax, Total
Style[] styles = { null, costStyle, taxStyle, priceStyle };
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, styles);
```

### Moeda Específica de Localidade

Para Euro ou Libra Esterlina, use IDs embutidos diferentes (por exemplo, 165 para `€#,##0.00`). Alternativamente, defina uma string de formato personalizada:

```csharp
priceStyle.Custom = "€#,##0.00";
```

### Conjuntos de Dados Grandes

Aspose.Cells pode lidar com milhões de linhas, mas o consumo de memória cresce com objetos de estilo. Reutilize uma única instância de `Style` para todas as colunas de moeda para manter a pegada baixa.

### Estilos Ausentes

Se `columnStyles` for mais curto que o número de colunas, o Aspose aplicará o estilo padrão às colunas restantes. Isso é útil quando você se importa apenas com algumas colunas.

---

## Exemplo Completo Funcional (Todas as Etapas Combinadas)

Abaixo está o programa completo que você pode copiar‑colar em um aplicativo console. Ele inclui todas as partes que discutimos, além de alguns comentários úteis.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Build sample DataTable (import datatable to excel)
        // -------------------------------------------------
        DataTable dataTable = new DataTable();
        dataTable.Columns.Add("Product", typeof(string));
        dataTable.Columns.Add("Price", typeof(double));
        dataTable.Rows.Add("Apple", 1.23);
        dataTable.Rows.Add("Banana", 0.78);
        dataTable.Rows.Add("Cherry", 2.50);
        // You can add as many rows as you like here.

        // -------------------------------------------------
        // Step 2: Create a new workbook (create excel workbook c#)
        // -------------------------------------------------
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // -------------------------------------------------
        // Step 3: Define a currency style (format cells currency)
        // -------------------------------------------------
        Style priceStyle = workbook.CreateStyle();
        priceStyle.Number = 164; // "$#,##0.00" – built‑in currency format

        // -------------------------------------------------
        // Step 4: Build the style array (apply currency format column)
        // -------------------------------------------------
        // First column gets default style (null), second column uses priceStyle.
        Style[] columnStyles = { null, priceStyle };

        // -------------------------------------------------
        // Step 5: Import the DataTable with the style array
        // -------------------------------------------------
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // -------------------------------------------------
        // Step 6: Save the workbook to disk
        // -------------------------------------------------
        string outputPath = @"YOUR_DIRECTORY\StyledTable.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Resultado esperado:** Ao abrir `StyledTable.xlsx` a coluna `Price` aparece com o símbolo de dólar e duas casas decimais, exatamente como a instrução `format cells currency` exigia.

---

## Perguntas Frequentes

**Q: Isso funciona com .NET Core?**  
A: Absolutamente. Aspose.Cells é compatível com .NET‑standard, então você pode direcionar .NET 5, .NET 6 ou versões posteriores sem alterações.

**Q: E se meu DataTable tem 10 colunas mas eu só quero formatar a coluna 5?**  
A: Crie um `Style[]` com comprimento 10, preencha as posições 0‑4 e 6‑9 com `null`, e coloque seu estilo personalizado no índice 4 (base zero). O Aspose respeitará cada entrada.

**Q: Posso ocultar a linha de cabeçalho?**  
A: Após a importação, defina `worksheet.Cells.Rows[0].Hidden = true;` ou simplesmente passe `false` para o parâmetro `includeColumnNames` em `ImportDataTable`.

---

## Conclusão

Acabamos de **create Excel workbook C#**, importar um `DataTable` e **apply a currency format column** usando Aspose.Cells. As etapas principais — preparar os dados, definir um estilo, construir um array de estilos, importar com `ImportDataTable` e salvar — cobrem o núcleo da maioria das tarefas de automação do Excel.

A partir daqui você pode explorar:

- **add number format excel** para datas ou percentuais  
- Exportar várias planilhas em um único arquivo  
- Usar **format cells currency** com símbolos específicos de localidade  
- Automatizar a criação de gráficos com base nos mesmos dados  

Experimente, e você rapidamente se tornará a pessoa de referência para relatórios Excel em sua equipe. Tem uma variação que gostaria de compartilhar? Deixe um comentário abaixo — feliz codificação!  

![create excel workbook c# screenshot](image.png "create excel workbook c#")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}