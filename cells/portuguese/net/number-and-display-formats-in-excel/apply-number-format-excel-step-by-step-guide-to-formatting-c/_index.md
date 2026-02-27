---
category: general
date: 2026-02-26
description: Aplique formatação de número no Excel rapidamente e aprenda como formatar
  coluna como moeda, definir o formato numérico da coluna e definir a cor da fonte
  da coluna em apenas algumas linhas de C#.
draft: false
keywords:
- apply number format excel
- format column as currency
- set column number format
- format currency column
- set column font color
language: pt
og_description: aplique formatação de número no Excel em C# com passos fáceis. Aprenda
  a formatar a coluna como moeda, definir o formato numérico da coluna e definir a
  cor da fonte da coluna para planilhas profissionais.
og_title: Aplicar formatação de número no Excel – Guia completo de estilo de colunas
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: Aplicar formato de número no Excel – Guia passo a passo para formatar colunas
url: /pt/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# aplicar formatação numérica no Excel – Como estilizar colunas do Excel em C#

Já se perguntou como **aplicar formatação numérica no Excel** enquanto já está percorrendo um `DataTable`? Você não está sozinho. A maioria dos desenvolvedores encontra um obstáculo quando precisa de um cabeçalho com fonte azul *e* uma coluna formatada como moeda na mesma operação de importação. A boa notícia? Com algumas linhas de C# e os objetos de estilo corretos, você pode fazer isso sem pós‑processamento da planilha.

Neste tutorial vamos percorrer um exemplo completo e executável que mostra como **formatar coluna como moeda**, **definir formatação numérica da coluna** para qualquer outra coluna e até **definir cor da fonte da coluna** para cabeçalhos. Ao final, você terá um padrão reutilizável que pode ser inserido em qualquer projeto Aspose.Cells (ou similar).

## O que você aprenderá

- Como recuperar um `DataTable` e mapear cada coluna para um `Style` específico.  
- As etapas exatas para **aplicar formatação numérica no Excel** usando `Worksheet.Cells.ImportDataTable`.  
- Por que criar estilos antecipadamente é mais eficiente do que formatar células uma a uma.  
- Tratamento de casos limites quando a tabela de origem tem mais colunas do que você estilizou.  
- Um exemplo de código completo, pronto para copiar e colar, que você pode executar hoje.

> **Pré‑requisito:** Este guia assume que você tem o Aspose.Cells para .NET (ou qualquer biblioteca que exponha as APIs `Workbook`, `Worksheet`, `Style`) referenciada no seu projeto. Se estiver usando outra biblioteca, os conceitos são diretamente aplicáveis — basta substituir os nomes dos tipos.

---

## Etapa 1: Recuperar os dados de origem como um DataTable

Antes que qualquer estilo possa ser aplicado, você precisa dos dados brutos. Na maioria dos cenários reais, os dados vivem em um banco de dados, CSV ou API. Para fins de clareza, vamos simular um `DataTable` simples com duas colunas: *Product* (string) e *Price* (decimal).

```csharp
using System;
using System.Data;
using Aspose.Cells;
using System.Drawing;

public static DataTable GetData()
{
    var dt = new DataTable();
    dt.Columns.Add("Product", typeof(string));
    dt.Columns.Add("Price", typeof(decimal));

    dt.Rows.Add("Apple", 1.25m);
    dt.Rows.Add("Banana", 0.75m);
    dt.Rows.Add("Cherry", 2.10m);

    return dt;
}
```

> **Por que isso importa:** Carregar os dados em um `DataTable` fornece uma representação tabular em memória que `ImportDataTable` pode consumir diretamente, eliminando a necessidade de inserção manual célula a célula.

## Etapa 2: Criar um array de estilos – Um por coluna

A sobrecarga de `ImportDataTable` que usaremos aceita um array de objetos `Style`. Cada entrada corresponde a um índice de coluna. Se você deixar uma entrada como `null`, a coluna herdará o estilo padrão da pasta de trabalho.

```csharp
// Initialize the workbook (Aspose.Cells)
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Prepare the style array based on the number of columns
DataTable dataTable = GetData();
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

> **Dica profissional:** Declarar o array *depois* de ter o `DataTable` garante que o tamanho corresponda exatamente, evitando `IndexOutOfRangeException` mais tarde.

## Etapa 3: Definir a cor da fonte da coluna (azul) para a primeira coluna

Um pedido comum é destacar cabeçalhos ou colunas chave com uma cor de fonte distinta. Aqui deixamos o texto da primeira coluna em azul.

```csharp
// Style for the first column – blue font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = Color.Blue;
```

> **Por que usar um objeto de estilo?** Estilos são reutilizáveis e aplicados em lote, o que é muito mais rápido do que iterar sobre cada célula após a importação. A pasta de trabalho armazena em cache o estilo uma vez e o reutiliza para cada célula daquela coluna.

## Etapa 4: FormatAR a segunda coluna como moeda

Os formatos numéricos internos do Excel são identificados por um índice. `14` corresponde ao formato de moeda padrão (ex.: `$1,234.00`). Se precisar de um formato personalizado, pode atribuir uma string de formato em vez disso.

```csharp
// Style for the second column – built‑in currency format (ID 14)
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].Number = 14; // 14 = built‑in currency format
```

> **Caso limite:** Se sua pasta de trabalho usar um locale onde o símbolo da moeda não for `$`, o mesmo índice se adaptará automaticamente (ex.: `€` para locais alemães).

## Etapa 5: Importar o DataTable com os estilos definidos

Agora juntamos tudo. O método `ImportDataTable` colará os dados a partir da célula `A1` (linha 0, coluna 0) e aplicará os estilos que preparamos.

```csharp
// Import the DataTable into the worksheet, applying the column styles
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

- O segundo parâmetro `true` indica ao Aspose.Cells que a primeira linha do `DataTable` deve ser tratada como cabeçalhos de coluna.  
- As coordenadas `0, 0` especificam o canto superior‑esquerdo onde a importação começa.  
- `columnStyles` mapeia cada coluna para seu respectivo estilo.

## Etapa 6: Salvar a pasta de trabalho (Opcional, mas útil para verificação)

Se quiser ver o resultado no Excel, basta salvar a pasta de trabalho no disco. Esta etapa não é necessária para a lógica de estilo, mas é útil para depuração.

```csharp
// Save the workbook to a file
workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved as StyledReport.xlsx");
```

### Saída esperada

| **Produto** (fonte azul) | **Preço** (moeda) |
|--------------------------|-------------------|
| Apple                    | $1.25             |
| Banana                   | $0.75             |
| Cherry                   | $2.10             |

- A coluna *Produto* aparece em azul, destacando‑se.  
- A coluna *Preço* exibe valores com o símbolo de moeda padrão e duas casas decimais.

---

## Perguntas Frequentes & Variações

### Como eu **defino formatação numérica da coluna** para mais de duas colunas?

Basta estender o array `columnStyles`. Por exemplo, para mostrar um percentual na terceira coluna:

```csharp
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Number = 10; // 10 = built‑in percentage format
```

### E se eu precisar de um formato de moeda *personalizado*, como “USD 1,234.00”?

Substitua a propriedade `Number` por uma string de formato:

```csharp
columnStyles[1].Custom = "\"USD\" #,##0.00";
```

### Posso aplicar um **definir cor da fonte da coluna** a uma coluna numérica sem afetar seu formato numérico?

Com certeza. Estilos são composíveis. Você pode definir tanto `Font.Color` quanto `Number` na mesma instância de `Style`:

```csharp
columnStyles[3] = workbook.CreateStyle();
columnStyles[3].Font.Color = Color.Green;
columnStyles[3].Number = 2; // 2 = built‑in date format (just an example)
```

### O que acontece se o `DataTable` tiver mais colunas do que estilos?

Qualquer coluna sem um estilo explícito (`null` entry) herdará o estilo padrão da pasta de trabalho. Para evitar `null`s acidentais, você pode inicializar todo o array com um estilo base primeiro:

```csharp
Style defaultStyle = workbook.CreateStyle();
defaultStyle.Font.Size = 11;
for (int i = 0; i < columnStyles.Length; i++)
    columnStyles[i] = defaultStyle;
```

Em seguida, sobrescreva apenas as colunas que lhe interessam.

### Essa abordagem funciona com grandes volumes de dados (10 mil+ linhas)?

Sim. Como o estilo é aplicado *uma vez por coluna* antes da importação, a operação permanece O(N) em relação ao número de linhas, e o uso de memória permanece baixo. Evite percorrer cada célula após a importação — é aí que o desempenho degrada.

---

## Exemplo completo (Pronto para copiar e colar)

```csharp
using System;
using System.Data;
using System.Drawing;
using Aspose.Cells;

class ExcelStyler
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 3️⃣ Prepare style array (one per column)
        Style[] columnStyles = new Style[dataTable.Columns.Count];

        // 4️⃣ Style first column – blue font
        columnStyles[0] = workbook.CreateStyle();
        columnStyles[0].Font.Color = Color.Blue;

        // 5️⃣ Style second column – built‑in currency format (ID 14)
        columnStyles[1] = workbook.CreateStyle();
        columnStyles[1].Number = 14;

        // 6️⃣ (Optional) Add more styles here – e.g., percentage, custom formats

        // 7️⃣ Import the DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // 8️⃣ Save to file for verification
        workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
        Console.WriteLine("Excel file created: StyledReport.xlsx");
    }

    // Helper method to mock data
    public static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Price", typeof(decimal));

        dt.Rows.Add("Apple", 1.25m);
        dt.Rows.Add("Banana", 0.75m);
        dt.Rows.Add("Cherry", 2.10m);
        return dt;
    }
}
```

Execute o programa, abra `StyledReport.xlsx` e você verá o resultado de **aplicar formatação numérica no Excel** instantaneamente.

---

## Conclusão

Acabamos de demonstrar uma maneira limpa e eficiente de **aplicar formatação numérica no Excel** a um `DataTable` importado. Ao preparar um array `Style[]` antecipadamente, você pode **formatar coluna como moeda**, **definir formatação numérica da coluna** e **definir cor da fonte da coluna** em uma única chamada — sem necessidade de pós‑processamento.

Sinta‑se à vontade para expandir o padrão: adicionar estilos condicionais, mesclar células para cabeçalhos ou até injetar fórmulas. Os mesmos princípios se aplicam, mantendo seu código organizado e suas planilhas com aparência profissional.

---

### Próximos passos

- Explore **formatação condicional** para destacar valores que excedam um limite.  
- Combine esta técnica com **geração de tabelas dinâmicas** para relatórios dinâmicos.  
- Experimente **definir formatação numérica da coluna** para datas, percentuais ou notação científica personalizada.

Tentou alguma variação? Compartilhe nos comentários — vamos manter o

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}