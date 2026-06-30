---
category: general
date: 2026-06-30
description: Crie formatação condicional em uma pasta de trabalho do Excel usando
  Aspose.Cells. Aprenda como definir o plano de fundo das células, classificar células
  e construir o arquivo programaticamente.
draft: false
keywords:
- create conditional formatting
- create excel workbook
- set cell background
- how to rank cells
- how to use aspose
language: pt
og_description: Crie formatação condicional em uma pasta de trabalho do Excel usando
  Aspose.Cells. Siga este tutorial completo para definir o plano de fundo das células,
  classificar células e automatizar o Excel.
og_title: Crie Formatação Condicional no Excel com Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create conditional formatting in an Excel workbook using Aspose.Cells.
    Learn how to set cell background, rank cells, and build the file programmatically.
  headline: Create Conditional Formatting in Excel with Aspose.Cells – Step‑by‑Step
    Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Criar Formatação Condicional no Excel com Aspose.Cells – Guia Passo a Passo
url: /pt/net/excel-conditional-formatting/create-conditional-formatting-in-excel-with-aspose-cells-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crie Formatação Condicional no Excel com Aspose.Cells – Guia Passo a Passo

Já se perguntou como **criar formatação condicional** em um arquivo Excel sem abrir a interface? Você não está sozinho. Muitos desenvolvedores precisam **criar excel workbook** dinamicamente, e fazê‑lo programaticamente economiza horas de trabalho manual. Neste tutorial vamos mostrar exatamente como **criar formatação condicional**, estilizar células e até classificar os valores mais altos — tudo com a poderosa biblioteca Aspose.Cells para .NET.

Vamos percorrer um exemplo do mundo real: gerar uma planilha de pontuação, destacar pontuações altas em verde‑claro e aplicar um fundo dourado aos 3 melhores desempenhos. Ao final, você saberá **como definir o fundo da célula**, **como classificar células** e **como usar Aspose** para automação avançada de Excel. Sem enrolação, apenas uma solução completa e executável que pode ser inserida em qualquer projeto C#.

## O que Você Vai Aprender

- Como **criar excel workbook** usando Aspose.Cells  
- Como preencher um intervalo com dados aleatórios (pontuações)  
- Como **definir o fundo da célula** com cores sólidas  
- Como aplicar uma regra baseada em fórmula para **classificar células** e destacar as três melhores  
- Como salvar o resultado como um arquivo .xlsx  

Pré‑requisitos: .NET 6+ (ou .NET Framework 4.6+), Visual Studio (ou qualquer IDE C#) e uma referência ao pacote NuGet Aspose.Cells. Se você nunca usou Aspose antes, não se preocupe — vamos cobrir **como usar Aspose** do zero.

---

![Exemplo de formatação condicional](https://example.com/images/create-conditional-formatting.png "Captura de tela mostrando formatação condicional no arquivo Excel gerado")

*Texto alternativo da imagem: exemplo de formatação condicional em uma planilha Excel gerada com Aspose.Cells.*

## Como Criar um Excel Workbook com Aspose.Cells

Primeiro de tudo: você precisa de um objeto workbook para trabalhar. Aspose.Cells faz isso em uma única linha.

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Instantiate a new workbook and give the first sheet a friendly name
    Workbook workbook = new Workbook();                 // creates an empty workbook
    Worksheet sheet = workbook.Worksheets[0];           // grab the default worksheet
    sheet.Name = "Scores";                              // rename it to something meaningful
```

Por que renomeamos a planilha? Um nome claro (como **Scores**) facilita a referência posterior, especialmente quando você compartilha o arquivo com usuários não técnicos.  

Agora que o workbook existe, vamos preencher a coluna A com pontuações aleatórias.

## Como Preencher Dados – Criando Pontuações Aleatórias

```csharp
    // Step 2: Populate A2:A21 with random values between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)               // 20 rows of data
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }
```

Uma observação rápida: `PutValue` detecta automaticamente o tipo de dado, então você não precisa converter para `int`. O laço começa em `i = 0` mas grava na linha `i + 1` porque as linhas do Excel são baseadas em 1, enquanto a coleção `Cells` é baseada em 0.

## Como Definir o Fundo da Célula para Pontuações Altas

Agora vamos **criar formatação condicional** que pinta qualquer pontuação ≥ 80 em um tom verde‑claro.

```csharp
    // Step 3: Define a conditional formatting range (A2:A21)
    int firstRow = 1, lastRow = 20;                     // zero‑based indices for rows 2‑21
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];

    // Add a rule: cell value >= 80 → light‑green background
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");

    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;
```

A propriedade `ForegroundColor` controla a cor de preenchimento, enquanto `Pattern = BackgroundType.Solid` indica ao Excel que use um preenchimento sólido em vez de gradiente ou padrão. Este é o núcleo de **como definir o fundo da célula** com base em um limite numérico.

## Como Classificar Células e Destacar as Top‑3

Classificar é um pouco mais complexo porque precisamos de uma fórmula que avalie cada célula em relação a todo o intervalo. Aspose.Cells permite usar a mesma sintaxe de fórmula do Excel que você digitária na interface.

```csharp
    // Step 4: Add a formula‑based rule to color the top‑3 scores gold
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);

    // The formula uses the RANK function; note the absolute references ($) lock the range
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";

    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;
```

Por que `A2` na fórmula? Aspose avalia a fórmula relativa a cada célula no intervalo, então `A2` se desloca automaticamente para `A3`, `A4` etc., à medida que a regra é aplicada linha a linha. A função `RANK` devolve a posição de um valor dentro do intervalo especificado, e a parte `<=3` garante que apenas as três maiores pontuações recebam o preenchimento dourado.

## Como Salvar o Workbook

```csharp
    // Step 5: Persist the workbook to disk
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

Substitua `YOUR_DIRECTORY` por um caminho absoluto ou relativo onde sua aplicação tenha permissão de gravação. Após executar o método, abra o arquivo no Excel e você verá:

- Células verde‑claro para qualquer pontuação ≥ 80  
- Células douradas para as três maiores pontuações, independentemente de serem também ≥ 80  

Esse é o pipeline completo de **criar formatação condicional**.

---

## Exemplo Completo e Executável

Aqui está o método inteiro novamente, pronto para copiar e colar em um aplicativo console ou qualquer classe C#:

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Create a new workbook and name the first worksheet
    Workbook workbook = new Workbook();
    Worksheet sheet = workbook.Worksheets[0];
    sheet.Name = "Scores";

    // Step 2: Fill column A (A2:A21) with random scores between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }

    // Step 3: Highlight scores >= 80 with a light‑green background
    int firstRow = 1, lastRow = 20;
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");
    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;

    // Step 4: Color the top‑3 scores with a gold background using a formula rule
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";
    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;

    // Step 5: Save the workbook
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

### Resultado Esperado

Ao abrir `Scores_ConditionalFormatting.xlsx`:

- Células com valores **80** ou superiores brilham em verde‑claro.  
- Os três maiores números (mesmo que estejam abaixo de 80) aparecem com fundo **dourado**.  
- Todas as demais células mantêm o fundo branco padrão.

Essa pista visual informa instantaneamente a um gestor quem são os principais desempenhos, sem necessidade de ordenação manual.

---

## Perguntas Frequentes & Casos de Borda

**E se eu precisar de mais de três pontuações principais?**  
Basta mudar a parte `<=3` da fórmula para `<=5` (ou qualquer número que desejar). A regra se adaptará automaticamente.

**Posso aplicar múltiplos intervalos de formatação?**  
Com certeza. Chame `sheet.ConditionalFormattings.Add` novamente com um intervalo diferente e, em seguida, adicione condições ao novo objeto `ConditionalFormatting`.

**E quanto a versões mais antigas do Excel?**  
Aspose.Cells salva no formato moderno `.xlsx` por padrão, compatível com Excel 2007 e posteriores. Se precisar de `.xls`, passe `SaveFormat.Excel97To2003` ao método `Save`.

**Existe impacto de desempenho para planilhas grandes?**  
A formatação condicional é armazenada como metadados, portanto não afeta significativamente o tamanho do arquivo. Contudo, gerar centenas de milhares de linhas pode aumentar o uso de memória — considere processar em lotes.

---

## Próximos Passos

Agora que você dominou **como criar formatação condicional**, pode explorar:

- **Como criar gráficos Excel** programaticamente (outro recurso valioso do Aspose.Cells)  
- **Como definir o fundo da célula** com base em valores de texto (ex.: “Pass/Fail”)  
- **Como usar Aspose.Cells para validação de dados** e listas suspensas  

Cada um desses tópicos se baseia nos mesmos fundamentos que você acabou de aprender, então você se sentirá em casa.

---

## Conclusão

Acabamos de percorrer um exemplo completo, de ponta a ponta, de como **criar formatação condicional** em um workbook Excel usando Aspose.Cells. Desde a inicialização do workbook, preenchimento de dados, **definição do fundo da célula**, classificação dos melhores desempenhos, até a gravação final do arquivo, cada etapa foi abordada com foco em **como classificar células** e **como usar Aspose**.  

Teste o código, ajuste os limites e veja como você pode gerar relatórios refinados rapidamente para qualquer cenário de negócios. Tem alguma variação que gostaria de compartilhar? Deixe um comentário abaixo — feliz codificação!

## O Que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais, com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Automate Excel Conditional Formatting Using Aspose.Cells for Java&#58; A Complete Guide](/cells/english/java/formatting/automate-conditional-formatting-excel-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java&#58; A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Create an Excel Workbook using Aspose.Cells in Java&#58; A Step‑By‑Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}