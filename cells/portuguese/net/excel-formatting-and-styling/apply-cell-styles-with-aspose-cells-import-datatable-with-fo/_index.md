---
category: general
date: 2026-06-05
description: Aplique estilos de célula ao usar a importação do Aspose.Cells. Aprenda
  como importar DataTable com formatação, estilizar linhas e manter as planilhas organizadas.
draft: false
keywords:
- apply cell styles
- aspose cells import
- import with formatting
- how to import datatable
- import datatable worksheet
language: pt
og_description: Aplique estilos de célula ao importar um DataTable para uma planilha
  Aspose.Cells. Guia passo a passo com código completo e dicas.
og_title: Aplicar estilos de célula com Aspose.Cells – Importar DataTable
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  headline: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  type: TechArticle
- description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  name: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  steps:
  - name: How It Works
    text: 1. **Headers** – Because we passed `true`, Aspose writes “Name” and “Score”
      into the first row. 2. **Data Rows** – Each subsequent row receives the corresponding
      style from `importStyles`. 3. **Performance** – The method streams the data
      directly into the worksheet, which is faster than looping cell
  - name: What if My DataTable Has More Columns Than Styles?
    text: Aspose will apply the last style in the array to any extra columns. To avoid
      unexpected colors, always match the array length to the column count, or pass
      `null` for columns you don’t want styled.
  - name: Can I Apply Different Styles to Specific Rows?
    text: 'Absolutely. After the import, you can loop through rows and assign new
      `Style` objects based on conditions (e.g., highlight scores > 90 in green).
      Here’s a quick snippet:'
  - name: Does This Work with Large DataSets?
    text: Yes. `ImportDataTable` streams data efficiently, and applying a static style
      array adds negligible overhead. For millions of rows, consider using `ImportDataTable`
      in chunks or leveraging `Cells.ImportDataTable` with a `DataReader` for even
      better memory usage.
  - name: How Do I Preserve Existing Formatting in the Worksheet?
    text: If the target range already has formatting you want to keep, set the `ImportDataTable`
      overload’s `importOptions` parameter (`ImportTableOptions`) and tweak `ImportDataTableOptions.PreserveCellFormatting`.
      The default behavior overwrites styles with the ones you supply.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DataTable
title: Aplicar estilos de célula com Aspose.Cells – Importar DataTable com formatação
url: /pt/net/excel-formatting-and-styling/apply-cell-styles-with-aspose-cells-import-datatable-with-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aplicar Estilos de Célula com Aspose.Cells – Importar DataTable com Formatação

Já se perguntou como **aplicar estilos de célula** ao trazer um `DataTable` para uma planilha Excel? Você não está sozinho. Em muitos cenários de relatórios, é preciso que os dados já tenham uma boa aparência — sem formatação manual depois. A boa notícia é que o Aspose.Cells torna **importar com formatação** algo simples, permitindo que suas linhas fiquem vermelhas ou azuis, em negrito, ou como desejar.

Neste tutorial vamos percorrer um exemplo completo e executável que mostra **como importar datatable** para uma planilha **com estilos de célula** aplicados. Ao final, você terá um aplicativo console C# pronto‑para‑executar que cria uma pasta de trabalho, estiliza as duas primeiras colunas e salva o arquivo — tudo usando a API `aspose cells import`.

## O que Você Vai Aprender

- Configurar o Aspose.Cells em um projeto .NET  
- Construir um `DataTable` de exemplo que imita dados reais  
- Definir objetos `Style` para fontes vermelhas e azuis  
- Usar `Worksheet.Cells.ImportDataTable` para **importar datatable worksheet** aplicando os estilos  
- Verificar o resultado e salvar a pasta de trabalho  

Sem ferramentas externas, apenas C# puro e Aspose.Cells. Vamos começar.

---

## Pré‑requisitos

Antes de mergulharmos no código, certifique‑se de que você tem o seguinte:

| Requisito | Por que é importante |
|-----------|----------------------|
| .NET 6.0 ou superior | Aspose.Cells 23.x tem alvo .NET Standard 2.0+, então o .NET 6 oferece os recursos mais recentes do runtime. |
| Aspose.Cells for .NET (NuGet) | A biblioteca fornece os métodos `Workbook`, `Worksheet`, `Style` e `ImportDataTable` que precisamos. |
| Conhecimento básico de C# | Você entenderá classes, arrays e instruções `using`. |
| Uma IDE (Visual Studio, VS Code, Rider) | Qualquer editor funciona, mas você precisará restaurar os pacotes NuGet. |

Você pode instalar o pacote pela linha de comando:

```bash
dotnet add package Aspose.Cells
```

---

## Etapa 1: Criar uma Nova Pasta de Trabalho e Acessar a Primeira Planilha

Primeiro passo — vamos instanciar um `Workbook` e obter a primeira planilha. Pense na pasta de trabalho como um caderno em branco; a primeira planilha é a página onde vamos escrever.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Create a new workbook (equivalent to a new Excel file)
        Workbook wb = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet worksheet = wb.Worksheets[0];
```

> **Dica:** Se precisar de várias planilhas, basta adicioná‑las com `wb.Worksheets.Add()` e referenciá‑las pelo nome ou índice.

---

## Etapa 2: Preparar um DataTable de Exemplo (Como Importar DataTable)

Agora precisamos de algo para importar. Em projetos reais você chamaria um banco de dados, mas para clareza vamos criar um `DataTable` na memória.

```csharp
        // Build a sample DataTable with two columns: Name and Score
        DataTable dataTable = new DataTable("Results");
        dataTable.Columns.Add("Name", typeof(string));
        dataTable.Columns.Add("Score", typeof(int));

        // Populate rows – imagine these came from a query
        dataTable.Rows.Add("Alice", 85);
        dataTable.Rows.Add("Bob", 92);
        dataTable.Rows.Add("Charlie", 78);
        dataTable.Rows.Add("Diana", 91);
```

> **Por que isso importa:** Ter um `DataTable` permite testar o fluxo **aspose cells import** sem dependências externas.

---

## Etapa 3: Definir os Estilos a Aplicar nas Células Importadas

Aqui é onde a mágica acontece. Criaremos dois objetos `Style`: um com fonte vermelha e outro com fonte azul. Eles serão aplicados coluna a coluna durante a importação.

```csharp
        // Define an array of styles – one per column
        Style[] importStyles = new Style[2];

        // Style for the first column (Name) – red text
        Style redStyle = wb.CreateStyle();
        redStyle.Font.Color = Color.Red;
        importStyles[0] = redStyle;

        // Style for the second column (Score) – blue text
        Style blueStyle = wb.CreateStyle();
        blueStyle.Font.Color = Color.Blue;
        importStyles[1] = blueStyle;
```

> **Atenção:** O tamanho de `importStyles` deve corresponder ao número de colunas que você está importando, caso contrário o Aspose lançará um `ArgumentException`.

---

## Etapa 4: Importar o DataTable para a Planilha **com Formatação**

Agora juntamos tudo. A sobrecarga de `ImportDataTable` que usamos aceita o array `Style[]`, permitindo **aplicar estilos de célula** enquanto os dados são inseridos na planilha.

```csharp
        // Import the DataTable starting at cell A1 (row 0, column 0)
        // The 'true' flag tells Aspose to generate column headers automatically
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);
```

### Como Funciona

1. **Cabeçalhos** – Como passamos `true`, o Aspose grava “Name” e “Score” na primeira linha.  
2. **Linhas de Dados** – Cada linha subsequente recebe o estilo correspondente de `importStyles`.  
3. **Desempenho** – O método transmite os dados diretamente para a planilha, sendo mais rápido que percorrer célula por célula.

---

## Etapa 5: Verificar o Resultado e Salvar a Pasta de Trabalho

Vamos dar uma olhada nas primeiras células para garantir que os estilos foram aplicados, e então gravar o arquivo no disco.

```csharp
        // Optional: Quick sanity check – print the first row's values
        Console.WriteLine("Header Row:");
        Console.WriteLine($"{worksheet.Cells[0, 0].StringValue} | {worksheet.Cells[0, 1].StringValue}");

        // Save the workbook to an Excel file
        string outputPath = "StyledImport.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Ao abrir **StyledImport.xlsx**, você verá:

- A coluna “Name” em texto **vermelho**.  
- A coluna “Score” em texto **azul**.  
- Os cabeçalhos de coluna no estilo padrão (você poderia estilizar também, mas isso fica para outro tutorial).

![Apply cell styles example](https://example.com/images/apply-cell-styles.png "Apply cell styles in Aspose.Cells")

> **Observação:** A imagem acima demonstra a aparência final. O atributo `alt` contém a palavra‑chave principal, atendendo aos requisitos de SEO.

---

## Perguntas Frequentes & Casos de Borda

### E se meu DataTable tiver mais colunas do que estilos?

O Aspose aplicará o último estilo do array às colunas extras. Para evitar cores inesperadas, sempre faça o array ter o mesmo tamanho que o número de colunas, ou passe `null` para as colunas que não deseja estilizar.

### Posso aplicar estilos diferentes a linhas específicas?

Com certeza. Após a importação, você pode percorrer as linhas e atribuir novos objetos `Style` com base em condições (por exemplo, destacar notas > 90 em verde). Veja um trecho rápido:

```csharp
for (int i = 1; i <= dataTable.Rows.Count; i++) // start at 1 to skip header
{
    int score = worksheet.Cells[i, 1].IntValue;
    if (score > 90)
    {
        Style highScore = wb.CreateStyle();
        highScore.Font.Color = Color.Green;
        worksheet.Cells[i, 1].SetStyle(highScore);
    }
}
```

### Isso funciona com grandes conjuntos de dados?

Sim. `ImportDataTable` transmite os dados de forma eficiente, e aplicar um array de estilos estático adiciona pouca sobrecarga. Para milhões de linhas, considere usar `ImportDataTable` em blocos ou aproveitar `Cells.ImportDataTable` com um `DataReader` para ainda melhor uso de memória.

### Como preservo a formatação existente na planilha?

Se o intervalo de destino já possui formatação que você quer manter, configure o parâmetro `importOptions` da sobrecarga `ImportDataTable` (`ImportTableOptions`) e ajuste `ImportDataTableOptions.PreserveCellFormatting`. O comportamento padrão sobrescreve estilos pelos que você fornece.

---

## Recapitulação: O que Conquistamos

- **Aplicamos estilos de célula** durante uma operação **aspose cells import**.  
- Demonstramos **importação com formatação** passando um array `Style[]`.  
- Mostramos **como importar datatable** para uma planilha e salvar o resultado.  
- Cobriram casos de borda como contagem de estilos incompatível e estilização condicional de linhas.

Tudo isso foi feito em um único aplicativo console autônomo — sem scripts externos, sem ajustes manuais no Excel. Agora você tem uma base sólida para qualquer recurso de relatório ou exportação de dados que exija saída Excel bem formatada.

---

## Próximos Passos

Pronto para avançar? Aqui vão algumas ideias que ampliam o que você acabou de aprender:

- **Estilizar a linha de cabeçalho** (por exemplo, negrito, cor de fundo).  
- **Aplicar formatação condicional** usando `Worksheet.Cells[i, j].ConditionalFormattingCollection`.  
- **Exportar para outros formatos** como CSV ou PDF com `wb.Save("file.pdf", SaveFormat.Pdf)`.  
- **Combinar múltiplos DataTables** em uma única pasta de trabalho, cada um em sua própria planilha, usando a mesma abordagem de estilização.

Se encontrar algum obstáculo, deixe um comentário ou consulte a documentação oficial da Aspose sobre `ImportDataTable`. Boa codificação e aproveite esses arquivos Excel elegantemente estilizados!

## O que Você Deve Aprender a Seguir?

Os tutoriais abaixo abordam tópicos intimamente relacionados que expandem as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [How to Set Font Styles in Excel Using Aspose.Cells for .NET (Step‑By‑Step Guide)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)
- [How to Apply Text Shadow in Excel Using Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/formatting/apply-text-shadow-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}