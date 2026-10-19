---
category: general
date: 2026-06-17
description: Defina o formato de data no Excel usando C# e também defina o fundo da
  célula, aplique a cor do primeiro plano e colore a coluna do Excel durante a importação.
  Aprenda passo a passo.
draft: false
keywords:
- set date format
- set cell background
- apply foreground color
- color excel column
- excel import formatting
language: pt
og_description: Defina o formato de data no Excel com C# enquanto define o fundo da
  célula, aplica a cor do texto e colore a coluna do Excel durante a importação. Tutorial
  completo.
og_title: Defina o formato de data no Excel com C# – Guia Completo
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  headline: Set date format in Excel with C# – Full Import Formatting Guide
  type: TechArticle
- description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  name: Set date format in Excel with C# – Full Import Formatting Guide
  steps:
  - name: 2.1 Set Date Format for the First Column
    text: The first column (`OrderDate`) should display as “MM/dd/yyyy”. Aspose uses
      the built‑in number format index 14 for the short date, but you can also supply
      a custom format string if you prefer.
  - name: 2.2 Set Cell Background for the Second Column
    text: Let’s give the `CustomerName` column a light blue background. This is where
      **set cell background** comes into play.
  - name: 2.3 Apply Foreground (Text) Color – Optional Extra
    text: 'If you also want the text itself to be a contrasting color, you can tweak
      the same style:'
  - name: 3.1 Save the Workbook
    text: '```csharp // Save to a file – change path as needed wb.Save("FormattedReport.xlsx",
      SaveFormat.Xlsx); Console.WriteLine("Excel file created with date format and
      colors."); ```'
  - name: What if I have more than two columns?
    text: Just expand the `columnStyles` array and assign a `Style` to each index
      you care about. Unassigned indexes will fall back to the default style, which
      is perfectly fine.
  - name: How do I format a column as currency?
    text: '```csharp columnStyles[3] = wb.CreateStyle(); columnStyles[3].Number =
      164; // Built‑in currency format (e.g., $#,##0.00) ```'
  - name: Can I change the header row style separately?
    text: 'Yes. After the import, you can grab the first row and apply a distinct
      style:'
  - name: What if the DataTable contains null dates?
    text: 'Aspose will leave those cells blank. If you prefer a placeholder like “N/A”,
      you can preprocess the table:'
  type: HowTo
tags:
- excel
- csharp
- aspnet
- data-import
title: Defina o formato de data no Excel com C# – Guia completo de formatação de importação
url: /pt/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definir formato de data no Excel com C# – Guia Completo de Formatação de Importação

Já precisou **definir o formato de data** em uma planilha Excel gerada a partir de código C#, mas também queria que a coluna tivesse um fundo ou cor de texto personalizados? Você não está sozinho. Em muitos cenários de relatórios você obtém um `DataTable` de um banco de dados, o coloca em uma planilha e então corre para fazer as datas aparecerem corretamente e as colunas se destacarem com as cores certas.

Neste tutorial vamos percorrer uma solução limpa, de ponta a ponta, que **define o formato de data**, **define o fundo da célula**, **aplica a cor do primeiro plano**, e até **colore uma coluna do Excel** ao importar dados. Ao final, você terá um padrão reutilizável que lida com **formatação de importação de Excel** sem o habitual tentativa‑e‑erro.

> **O que você precisará**  
> * .NET 6+ (ou .NET Framework 4.7+)  
> * Aspose.Cells for .NET (versão de avaliação gratuita funciona para testes)  
> * Uma fonte `DataTable` – qualquer consulta ADO.NET serve  
> * Visual Studio ou sua IDE favorita  

Vamos começar.

---

## Visão geral da solução

Dividiremos o problema em três partes lógicas:

1. **Recuperar os dados de origem** – um `DataTable` com as linhas que você deseja exportar.  
2. **Criar estilos específicos por coluna** – um estilo para a coluna de data, outro para uma coluna de texto, além de quaisquer estilos adicionais que você desejar.  
3. **Importar a tabela com estilos** – use `Worksheet.Cells.ImportDataTable` para que cada coluna herde o estilo que você preparou.

Por que essa abordagem? Porque o Aspose.Cells permite anexar um array `Style` diretamente à chamada `ImportDataTable`, o que significa que você não precisa de uma segunda passagem para reaplicar a formatação. É mais rápido, menos propenso a erros e mantém seu código organizado.

## Etapa 1: Recuperar os Dados para Exportar

Primeiro de tudo – você precisa de um `DataTable`. Em um projeto real você provavelmente chamaria uma procedure armazenada ou usaria o Entity Framework para preenchê-lo, mas para fins de ilustração vamos simular uma tabela simples com uma coluna de data e uma coluna de texto.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("OrderDate", typeof(DateTime));
    table.Columns.Add("CustomerName", typeof(string));

    // Sample rows – replace with your DB call
    table.Rows.Add(DateTime.Today.AddDays(-2), "Acme Corp");
    table.Rows.Add(DateTime.Today.AddDays(-1), "Globex Inc");
    table.Rows.Add(DateTime.Today, "Soylent Co");

    return table;
}
```

> **Dica profissional:** Se sua fonte usa datas anuláveis, certifique‑se de que o tipo da coluna seja `typeof(DateTime?)` – o Aspose ainda respeitará o formato que você atribuir posteriormente.

---

## Etapa 2: Preparar um Array de Estilos – Um por Coluna

Agora criamos um `Style[]` cujo comprimento corresponde ao número de colunas no `DataTable`. Cada entrada conterá a formatação para sua respectiva coluna.

```csharp
// Create a new workbook and get the first worksheet
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Pull the data
DataTable dataTable = GetData();

// Allocate the style array
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

### 2.1 Definir o Formato de Data para a Primeira Coluna

A primeira coluna (`OrderDate`) deve ser exibida como “MM/dd/yyyy”. O Aspose usa o índice de formato numérico interno 14 para a data curta, mas você também pode fornecer uma string de formato personalizada, se preferir.

```csharp
// Style for the date column (index 0)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Built‑in short date format
// Or a custom pattern:
// columnStyles[0].Custom = "mm/dd/yyyy";
```

**Por que isso importa:** O Excel armazena datas como números seriais. Ao atribuir um formato numérico, você indica ao Excel que renderize esses seriais como datas legíveis por humanos em vez de números brutos.

### 2.2 Definir o Fundo da Célula para a Segunda Coluna

Vamos dar à coluna `CustomerName` um fundo azul claro. É aqui que **definir o fundo da célula** entra em ação.

```csharp
// Style for the text column (index 1)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightBlue;
columnStyles[1].Pattern = BackgroundType.Solid; // Needed to show the color
```

> **Nota:** Sem definir `Pattern` como `Solid`, a cor do primeiro plano não aparecerá porque o padrão padrão é “None”.

### 2.3 Aplicar Cor do Primeiro Plano (Texto) – Extra Opcional

Se você também quiser que o próprio texto tenha uma cor contrastante, pode ajustar o mesmo estilo:

```csharp
columnStyles[1].Font.Color = System.Drawing.Color.DarkBlue; // apply foreground color
```

Isso satisfaz o requisito de **aplicar cor do primeiro plano** enquanto mantém o fundo da coluna intacto.

---

## Etapa 3: Importar o DataTable com os Estilos Definidos

Com os estilos prontos, o passo final é uma única linha que importa os dados e aplica os estilos coluna por coluna.

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// includeColumnNames = true to add a header row
ws.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**Como funciona:** O Aspose lê o array `columnStyles` e mapeia cada `Style` para o índice de coluna correspondente. A linha de cabeçalho herda o estilo padrão, a menos que você forneça um estilo separado para a linha 0.

### 3.1 Salvar a Pasta de Trabalho

```csharp
// Save to a file – change path as needed
wb.Save("FormattedReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Excel file created with date format and colors.");
```

Execute o programa, abra *FormattedReport.xlsx*, e você deverá ver:

- **OrderDate** coluna exibida como datas (ex., `06/15/2026`).  
- **CustomerName** coluna com preenchimento azul‑claro e texto azul‑escuro.  

Esse é todo o fluxo de **formatação de importação de Excel** em menos de 30 linhas de C#.

---

## Recapitulação Passo a Passo (com Por quê)

| Etapa | O que você faz | Por que isso importa |
|------|----------------|----------------------|
| **Retrieve data** | Chame `GetData()` para preencher um `DataTable`. | Fornece uma fonte estruturada que o Aspose pode ingerir diretamente. |
| **Create style array** | Aloca `Style[]` correspondendo ao número de colunas. | Permite estilização por coluna em uma única chamada de importação. |
| **Set date format** | `columnStyles[0].Number = 14;` | Garante que as datas sejam renderizadas corretamente no Excel. |
| **Set background color** | `ForegroundColor = LightBlue; Pattern = Solid;` | Destaca a coluna, atendendo ao requisito de **definir o fundo da célula**. |
| **Apply foreground color** | `Font.Color = DarkBlue;` | Melhora a legibilidade e atende ao requisito de **aplicar cor do primeiro plano**. |
| **Import with styles** | `ImportDataTable(..., columnStyles);` | Importação em uma única passagem que respeita toda a formatação. |
| **Save workbook** | `wb.Save(...);` | Persiste o resultado para usuários subsequentes. |

---

## Lidando com Casos de Borda & Perguntas Frequentes

### E se eu tiver mais de duas colunas?

Basta expandir o array `columnStyles` e atribuir um `Style` a cada índice que você desejar. Índices não atribuídos voltarão ao estilo padrão, o que é perfeitamente aceitável.

```csharp
columnStyles[2] = wb.CreateStyle();
columnStyles[2].Number = 0; // General format for numeric columns
```

### Como formatar uma coluna como moeda?

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 164; // Built‑in currency format (e.g., $#,##0.00)
```

### Posso alterar o estilo da linha de cabeçalho separadamente?

Sim. Após a importação, você pode obter a primeira linha e aplicar um estilo distinto:

```csharp
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = System.Drawing.Color.Gold;
headerStyle.Pattern = BackgroundType.Solid;

ws.Cells.Rows[0].ApplyStyle(headerStyle, new StyleFlag { All = true });
```

### E se o DataTable contiver datas nulas?

O Aspose deixará essas células vazias. Se você preferir um placeholder como “N/A”, pode pré-processar a tabela:

```csharp
foreach (DataRow row in dataTable.Rows)
{
    if (row.IsNull("OrderDate"))
        row["OrderDate"] = DateTime.MinValue; // or any sentinel
}
```

Em seguida, ajuste o estilo para exibir um formato personalizado que mostre “N/A” para o valor sentinela.

---

## Exemplo Completo em Funcionamento

Abaixo está o programa completo, pronto para copiar e colar. Execute‑o como um aplicativo de console e você obterá um arquivo Excel bem formatado.



## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Definir Cor da Fonte em Células do Excel usando Aspose.Cells para .NET](/cells/english/net/formatting/setting-font-color/)
- [Definir Cor da Fonte no Excel .NET com Aspose.Cells](/cells/english/net/formatting/set-font-color-net-excel-aspose-cells/)
- [Definir Larguras de Colunas do Excel em Pixels Usando Aspose.Cells para .NET | Guia Passo a Passo](/cells/english/net/formatting/set-excel-column-width-pixels-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}