---
category: general
date: 2026-03-18
description: Aprenda a aplicar cores alternadas nas linhas de uma planilha usando
  C#. Inclui definir a cor de fundo da linha, adicionar fundo amarelo claro e colorir
  as linhas alternadamente.
draft: false
keywords:
- apply alternating row colors
- set row background color
- add light yellow background
- set alternating row shading
- color rows alternately
language: pt
og_description: Aplique cores alternadas nas linhas em C# para melhorar a legibilidade.
  Este guia mostra como definir a cor de fundo da linha, adicionar um fundo amarelo
  claro e colorir as linhas alternadamente.
og_title: Aplicar cores alternadas nas linhas em C# – Tutorial completo
tags:
- C#
- DataTable
- Spreadsheet styling
- UI design
title: Aplicar cores alternadas nas linhas em C# – Guia passo a passo
url: /pt/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aplicar Cores Alternadas nas Linhas em C# – Tutorial Completo

Já precisou **aplicar cores alternadas nas linhas** a uma planilha orientada a dados, mas não sabia por onde começar? Você não é o único — a maioria dos desenvolvedores encontra esse obstáculo ao tentar deixar as tabelas um pouco mais amigáveis. A boa notícia? Em apenas algumas linhas de C# você pode **definir a cor de fundo da linha**, adicionar um **fundo amarelo claro**, e obter uma grade polida que melhora instantaneamente a legibilidade.

Neste tutorial vamos percorrer todo o processo, desde a obtenção de um `DataTable` na memória até a estilização de cada linha com uma faixa sutil amarelo‑branca. Ao final, você será capaz de **colorir linhas alternadamente** com confiança, e também verá algumas variações úteis para quando precisar de tons diferentes ou temáticas dinâmicas.

## O que você precisará

- Um projeto .NET direcionado ao .NET 6 ou posterior (o código também funciona no .NET Framework 4.7+).  
- Uma biblioteca de planilhas que suporte objetos de estilo – o exemplo usa uma API genérica `Workbook`/`Worksheet` que espelha bibliotecas como **Aspose.Cells**, **GemBox.Spreadsheet**, ou **ClosedXML**.  
- Uma fonte `DataTable` – pode ser de uma consulta ao banco de dados, importação CSV, ou qualquer coleção em memória.  

Nenhum pacote NuGet extra além da própria biblioteca de planilhas. Se você estiver usando Aspose.Cells, o namespace é `Aspose.Cells`; para ClosedXML é `ClosedXML.Excel`. Troque as chamadas `CreateStyle` e `ImportDataTable` conforme necessário.

## Etapa 1: Recuperar os Dados de Origem como um DataTable

Primeiro de tudo—obtenha os dados que deseja exibir. Em aplicativos reais isso geralmente significa acessar um banco de dados, mas para clareza vamos criar um método auxiliar chamado `GetData()` que retorna um `DataTable` preenchido.

```csharp
// Step 1: Retrieve the source data as a DataTable
DataTable dataTable = GetData();   // Replace with your actual data retrieval logic
```

> **Por que isso importa:** O `DataTable` define as linhas e colunas que mais tarde receberão o sombreamento alternado. Se a tabela estiver vazia, não há nada para estilizar, portanto sempre verifique se `Rows.Count` > 0 antes de prosseguir.

### Dica profissional
Se você estiver extraindo dados do Entity Framework, pode usar `DataTable.Load(reader)` após executar um `SqlCommand`. Isso mantém o código organizado e evita definições manuais de colunas.

## Etapa 2: Alocar um Array para Segurar um Estilo para Cada Linha

Em seguida, precisamos de um contêiner que corresponda ao número de linhas. A maioria das APIs de planilhas permite passar um array de estilos para o método de importação, então criaremos um `Style[]` dimensionado exatamente para a contagem de linhas.

```csharp
// Step 2: Allocate an array to hold a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];
```

> **Explicação:** Ao pré‑alocar o array, evitamos realocar um novo objeto de estilo a cada iteração, o que pode ser um ganho de desempenho ao lidar com milhares de linhas.

## Etapa 3: Aplicar Cores Alternadas nas Linhas (Amarelo Claro / Branco)

Agora vem o coração da questão: **aplicar cores alternadas nas linhas**. Vamos percorrer cada linha, criar uma nova instância de estilo a partir da workbook e definir seu fundo com base no índice da linha. Linhas pares recebem um preenchimento amarelo claro, linhas ímpares permanecem brancas.

```csharp
// Step 3: Create alternating background colors (light yellow / white) for the rows
for (int rowIndex = 0; rowIndex < dataTable.Rows.Count; rowIndex++)
{
    // Create a new style instance from the workbook
    rowStyles[rowIndex] = wb.CreateStyle();

    // Apply a light yellow background to even rows, white to odd rows
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow   // add light yellow background
        : Color.White;        // set row background color to white

    rowStyles[rowIndex].Pattern = BackgroundType.Solid; // set alternating row shading
}
```

### Por que isso funciona
- **`rowIndex % 2 == 0`** verifica se a linha é par.  
- **`Color.LightYellow`** fornece um tom suave e não intrusivo, perfeito para tabelas de dados.  
- **`BackgroundType.Solid`** garante que o preenchimento cubra toda a célula, alcançando o efeito de **definir cor de fundo da linha**.  

Você pode trocar `Color.LightYellow` por qualquer outro tom (por exemplo, `Color.LightCyan`) se preferir um visual diferente. A mesma lógica também permite **colorir linhas alternadamente** com base em outros critérios, como flags de status.

## Etapa 4: Importar o DataTable para a Planilha com os Estilos Preparados

Finalmente, enviamos tudo para a planilha. A maioria das bibliotecas expõe uma sobrecarga `ImportDataTable` que aceita um array de estilos. O parâmetro `true` indica à API que escreva os cabeçalhos das colunas, e as coordenadas `0, 0` iniciam na célula superior‑esquerda.

```csharp
// Step 4: Import the DataTable into the worksheet, applying the prepared row styles
ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

> **Resultado:** A planilha agora exibe seus dados com um padrão limpo de **sombreamento alternado de linhas**—amarelo claro nas linhas pares, branco nas linhas ímpares. Os usuários podem percorrer a grade sem que os olhos pulem de um lado para o outro.

### Saída Esperada
Se você abrir a planilha resultante, verá algo como isto:

| ID | Name      | Quantity |
|----|-----------|----------|
| **1** | Apple      | 50       |
| **2** | Banana     | 30       |
| **3** | Cherry     | 20       |
| **4** | Date       | 15       |

Linhas 1, 3, 5… têm um **fundo amarelo claro**, enquanto linhas 2, 4, 6… permanecem **brancas**. A linha de cabeçalho (linha 0) herda o estilo padrão, a menos que você a personalize separadamente.

## Variações Opcionais e Casos de Borda

### 1. Usando uma Paleta de Cores Diferente
Se o amarelo claro conflitar com a identidade visual da sua marca, basta substituir `Color.LightYellow` por outro `System.Drawing.Color`. Para um tema azul‑cinza, você poderia usar:

```csharp
rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
    ? Color.FromArgb(220, 235, 247) // soft blue
    : Color.White;
```

### 2. Sombreamento Dinâmico com Base nos Dados
Às vezes você quer destacar linhas que atendam a uma condição (por exemplo, estoque baixo). Combine a verificação de módulo com um teste personalizado:

```csharp
int quantity = Convert.ToInt32(dataTable.Rows[rowIndex]["Quantity"]);
if (quantity < 20)
{
    rowStyles[rowIndex].ForegroundColor = Color.Salmon; // urgent low‑stock color
}
else
{
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow
        : Color.White;
}
```

### 3. Aplicando Estilos Apenas a Colunas Específicas
Se você precisar apenas do **definir cor de fundo da linha** em colunas específicas, crie um estilo separado para cada coluna e atribua‑o após a importação usando a API de intervalo de células da planilha.

```csharp
// Example for column B only
var colBStyle = wb.CreateStyle();
colBStyle.ForegroundColor = Color.LightYellow;
colBStyle.Pattern = BackgroundType.Solid;

// Apply after import
ws.Cells[$"B2:B{dataTable.Rows.Count + 1}"].SetStyle(colBStyle);
```

### 4. Dica de Performance para Tabelas Grandes
Ao lidar com > 10.000 linhas, considere reutilizar um único objeto de estilo para cada cor em vez de criar um novo por linha. O array então contém referências aos dois estilos compartilhados, reduzindo drasticamente o uso de memória.

```csharp
Style yellowStyle = wb.CreateStyle();
yellowStyle.ForegroundColor = Color.LightYellow;
yellowStyle.Pattern = BackgroundType.Solid;

Style whiteStyle = wb.CreateStyle();
whiteStyle.ForegroundColor = Color.White;
whiteStyle.Pattern = BackgroundType.Solid;

for (int i = 0; i < dataTable.Rows.Count; i++)
    rowStyles[i] = (i % 2 == 0) ? yellowStyle : whiteStyle;
```

## Exemplo Completo em Funcionamento

Abaixo está um programa autocontido que você pode colar em um aplicativo de console. Ele usa uma API fictícia `Workbook`/`Worksheet`; substitua os tipos pelos da biblioteca que você escolheu.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using YourSpreadsheetLib;     // Replace with actual namespace

class Program
{
    static void Main()
    {
        // Initialize workbook & worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Step 1: Retrieve data
        DataTable dataTable = GetData();

        // Step 2: Allocate style array
        Style[] rowStyles = new Style[dataTable.Rows.Count];

        // Step 3: Apply alternating row colors
        for (int i = 0; i < dataTable.Rows.Count; i++)
        {
            rowStyles[i] = wb.CreateStyle();
            rowStyles[i].ForegroundColor = (i % 2 == 0)
                ? Color.LightYellow   // add light yellow background
                : Color.White;        // set row background color
            rowStyles[i].Pattern = BackgroundType.Solid; // set alternating row shading
        }

        // Step 4: Import with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // Save to file
        wb.Save("AlternatingRows.xlsx");
        Console.WriteLine("Workbook saved with alternating row colors.");
    }

    // Sample data generator
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Quantity", typeof(int));

        dt.Rows.Add(1, "Apple", 50);
        dt.Rows.Add(2, "Banana", 30);
        dt.Rows.Add(3, "Cherry", 20);
        dt.Rows.Add(4, "Date", 15);
        dt.Rows.Add(5, "Elderberry", 5);
        return dt;
    }
}
```

**Saída:** Um arquivo chamado `AlternatingRows.xlsx` onde cada linha alterna entre um preenchimento amarelo claro e branco, facilitando a visualização da tabela.

## Perguntas Frequentes

**Q: Esse método funciona com formatação condicional ao estilo do Excel?**  
A: Sim. Se sua biblioteca suportar regras condicionais, você pode traduzir a mesma lógica para uma regra que verifica `MOD(ROW(),2)=0`. O método baseado em código mostrado aqui é mais portátil entre bibliotecas que não possuem formatação condicional integrada.

**Q: E se eu precisar **colorir linhas alternadamente** em uma tabela PDF em vez de uma planilha Excel?**  
A: A maioria dos geradores de tabelas PDF (por exemplo, iTextSharp, PdfSharp) permite definir um `BackgroundColor` por linha. O mesmo cálculo de módulo se aplica—

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}