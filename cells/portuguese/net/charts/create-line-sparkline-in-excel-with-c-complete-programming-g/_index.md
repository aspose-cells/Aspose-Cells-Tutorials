---
category: general
date: 2026-06-30
description: Crie sparkline de linha no Excel com C# rapidamente. Aprenda como adicionar
  sparkline, criar uma pasta de trabalho Excel em C# e inserir sparkline em uma célula
  em poucos passos.
draft: false
keywords:
- create line sparkline
- how to add sparkline
- add line sparkline
- create excel workbook c#
- add sparkline to cell
language: pt
og_description: Criar sparkline de linha no Excel com C#. Este tutorial mostra como
  adicionar sparkline, criar uma pasta de trabalho do Excel em C# e incorporar a sparkline
  em uma célula.
og_title: Crie sparkline de linha no Excel com C# – Guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create line sparkline in Excel with C# quickly. Learn how to add sparkline,
    create Excel workbook C#, and add sparkline to cell in a few steps.
  headline: Create line sparkline in Excel with C# – Complete Programming Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Criar sparkline de linha no Excel com C# – Guia completo de programação
url: /pt/net/charts/create-line-sparkline-in-excel-with-c-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar sparkline de linha no Excel com C# – Guia de Programação Completo

Já se perguntou como **criar sparkline de linha** em um arquivo Excel usando C#? Você não é o único — os desenvolvedores perguntam constantemente: “como adiciono sparkline a um relatório sem abrir o Excel manualmente?” A boa notícia é que, com algumas linhas de código, você pode gerar uma elegante sparkline de linha diretamente na pasta de trabalho, sem necessidade de interface.

Neste tutorial, percorreremos tudo o que você precisa saber: desde os fundamentos de **create Excel workbook C#**, passando pela inserção de dados, até os passos exatos para **add line sparkline** e **add sparkline to cell**. Ao final, você terá um arquivo *.xlsx* pronto para uso que visualiza as tendências de vendas mensais de forma instantânea. Sem enrolação, apenas uma solução prática e executável.

---

## O que Você Vai Construir

- Uma nova pasta de trabalho Excel chamada *KPI_Sparklines.xlsx*  
- Uma planilha chamada **KPI** contendo números de vendas de exemplo  
- Uma **line sparkline** posicionada na célula **D2** que referencia o intervalo de dados **B2:B13**  
- Formatação básica (cor, espessura da linha) para destacar a sparkline  

Pré-requisitos? Apenas o .NET SDK (3.1+ ou .NET 6) e a biblioteca gratuita Aspose.Cells para .NET (disponível via NuGet). Se você nunca usou Aspose.Cells antes, pense nela como um poderoso motor Excel que pode ser chamado a partir do código — sem interop COM, sem necessidade de instalação do Excel.

![Criar sparkline de linha no Excel usando C#](https://example.com/images/create-line-sparkline.png "Criar sparkline de linha no Excel com C#")

*Texto alternativo da imagem: exemplo de código para criar sparkline de linha no Excel usando C#*

## Etapa 1: **Create Excel workbook C#** – Configurar o arquivo e a planilha

Primeiro de tudo. Precisamos de um objeto workbook e de uma planilha onde os dados ficarão. Esta é a base para qualquer automação Excel, seja para **add line sparkline** ou escrever fórmulas.

```csharp
using Aspose.Cells;
using System.Drawing;

// Initialize a new workbook
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0) and give it a meaningful name
Worksheet worksheet = workbook.Worksheets[0];
worksheet.Name = "KPI";   // “KPI” will hold our key performance indicators
```

> **Por que isso importa:** A classe `Workbook` representa o arquivo inteiro, enquanto `Worksheet` é a tela para linhas, colunas e, eventualmente, nossa sparkline. Nomear a planilha cedo mantém o arquivo organizado e auto‑documentado.

---

## Etapa 2: Preencher dados – O intervalo de origem para a sparkline

Uma sparkline precisa de dados para ser plotada. Vamos simular 12 meses de números de vendas. Você poderia obter esses dados de um banco de dados, mas para clareza os geraremos dinamicamente.

```csharp
// Fill column B (index 1) with monthly sales numbers
for (int month = 0; month < 12; month++)
{
    // Example pattern: start at 5,000 and increase by 750 each month
    worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
}
```

> **Dica:** `PutValue` detecta automaticamente o tipo de dado, então você não precisa converter para `double` ou `int`. Se precisar formatar as células (moeda, separador de milhar), pode aplicar um objeto `Style` posteriormente.

---

## Etapa 3: **Create line sparkline** – Adicionar a sparkline a uma célula específica

Agora vem a estrela do show: a **line sparkline**. O Aspose.Cells agrupa sparklines, então primeiro criamos um `SparklineGroup` do tipo `Line`, e então indicamos onde colocar a visualização.

```csharp
// Add a new SparklineGroup of type Line
int groupIndex = worksheet.SparklineGroups.Add(SparklineType.Line);
SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIndex];

// Add a sparkline that lives in D2 (row 1, column 3) and reads data from B2:B13
// Parameters: firstRow, firstColumn, lastRow, lastColumn, firstDataRow, lastDataRow
sparklineGroup.Add(1, 3, 1, 3, 1, 12);   // D2 ↔ B2:B13
```

> **Como funciona:**  
> - `firstRow/firstColumn` e `lastRow/lastColumn` definem a *célula alvo* (onde a sparkline aparece).  
> - `firstDataRow/lastDataRow` apontam para o intervalo de origem.  
> Como estamos usando uma **line sparkline**, a visualização será uma linha fina simples que segue a tendência dos números.

### Opcional: **How to add sparkline** com estilo personalizado

Se você quiser que a sparkline se destaque, ajuste algumas propriedades:

```csharp
sparklineGroup.LineWeight = 1.0;               // Thickness of the line
sparklineGroup.SeriesColor = Color.DarkBlue;  // Color of the sparkline line
sparklineGroup.ShowMarkers = true;             // Show data markers (optional)
sparklineGroup.MarkerColor = Color.OrangeRed;  // Marker color
```

> **Por que estilizar?** Uma linha azul escura sobre fundo branco é agradável aos olhos, enquanto marcadores fornecem uma indicação rápida dos pontos de dados individuais — útil para apresentações.

---

## Etapa 4: Salvar a pasta de trabalho – Verificar o resultado

Com a sparkline no lugar, só precisamos gravar o arquivo no disco. Escolha uma pasta onde você tenha permissão de escrita; o exemplo usa um caminho placeholder que você deve substituir.

```csharp
// Save the workbook as an .xlsx file
string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
workbook.Save(outputPath);
```

> **Verificação:** Abra o arquivo gerado no Excel (ou em qualquer visualizador que suporte .xlsx). Você deverá ver uma **line sparkline** na célula **D2** que reflete o aumento dos números de vendas na coluna **B**. Passar o mouse sobre a sparkline exibirá uma tooltip com os valores subjacentes.

---

## Etapa 5: Armadilhas comuns ao **add sparkline to cell**

Mesmo um exemplo simples pode confundir iniciantes. Aqui estão algumas coisas a observar:

| Problema | Por que acontece | Correção |
|----------|------------------|----------|
| Coordenadas de célula incorretas | O alvo da sparkline usa índice de coluna baseado em zero, mas índice de linha baseado em um. | Lembre‑se de que `Cells[row, column]` onde `row` é baseado em zero, e `column` também é baseado em zero. Em `SparklineGroup.Add`, linhas e colunas são **baseadas em 1**. |
| Nenhum dado exibido | O intervalo de origem está vazio ou contém valores não numéricos. | Garanta que o intervalo (por exemplo, `B2:B13`) contenha números. Use `PutValue` com tipos numéricos. |
| Sparkline desaparece após salvar | Incompatibilidade de versão da biblioteca ou licença ausente. | Use a versão mais recente do pacote Aspose.Cells e forneça uma licença válida se estiver além dos limites de avaliação. |
| Formatação não aplicada | Alterações de estilo feitas antes de adicionar a sparkline. | Defina o estilo **depois** de criar o grupo, como mostrado acima. |

---

## Código Fonte Completo – Copiar‑e‑colar em um único passo

Abaixo está o programa completo, pronto para execução. Cole‑o em um novo projeto de console, adicione o pacote NuGet Aspose.Cells e pressione **F5**.

```csharp
using Aspose.Cells;
using System.Drawing;

namespace SparklineDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create Excel workbook C#
            // -------------------------------------------------
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "KPI";

            // -------------------------------------------------
            // Step 2: Populate monthly sales data (B2:B13)
            // -------------------------------------------------
            for (int month = 0; month < 12; month++)
            {
                worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
            }

            // -------------------------------------------------
            // Step 3: Create line sparkline and add it to D2
            // -------------------------------------------------
            int groupIdx = worksheet.SparklineGroups.Add(SparklineType.Line);
            SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIdx];
            sparklineGroup.Add(1, 3, 1, 3, 1, 12); // D2 ↔ B2:B13

            // -------------------------------------------------
            // Step 4: Optional formatting (how to add sparkline with style)
            // -------------------------------------------------
            sparklineGroup.LineWeight = 1.0;
            sparklineGroup.SeriesColor = Color.DarkBlue;
            sparklineGroup.ShowMarkers = true;
            sparklineGroup.MarkerColor = Color.OrangeRed;

            // -------------------------------------------------
            // Step 5: Save the workbook
            // -------------------------------------------------
            string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
            workbook.Save(outputPath);

            System.Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Saída esperada:** Ao abrir *KPI_Sparklines.xlsx*, a coluna **B** lista doze números (5.000 → 13.250) e a célula **D2** contém uma suave sparkline de linha azul‑escura que sobe de forma constante. Os marcadores aparecem como pequenos pontos laranja‑vermelhos se você habilitou `ShowMarkers`.

---

## O que vem a seguir? Expandindo suas habilidades com Sparkline

Agora que você dominou **create line sparkline** com Aspose.Cells, considere explorar estes tópicos relacionados:

- **Add column sparkline** – perfeito para mostrar dados empilhados.  
- **Create multi‑sparkline groups** na mesma planilha para comparação lado a lado.  
- **Export to PDF** mantendo as sparklines (Aspose.Cells suporta conversão para PDF).  
- **Dynamic data sources** – obter números reais de vendas de um banco de dados SQL em vez de valores codificados.  

Cada um desses se baseia nos mesmos conceitos centrais: **create Excel workbook C#**, preencher dados e **add sparkline to cell** no estilo desejado.

---

### TL;DR

Mostramos como **create line sparkline** em uma pasta de trabalho Excel usando C#. Os passos — *create workbook, fill data, add sparkline, style it, and save* — estão todos encapsulados em um único programa autônomo. Sinta‑se à vontade para ajustar as cores, espessura da linha ou intervalo de origem para atender às suas necessidades de relatório.

Tem alguma variação que gostaria de compartilhar? Deixe um comentário abaixo, e feliz codificação!

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Automação Excel: Criar uma Pasta de Trabalho e Adicionar um ListBox Usando Aspose.Cells para .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Automação Excel Criar Pasta de Trabalho Adicionar ListBox Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Automação Excel Criar Pasta de Trabalho Adicionar ListBox Aspose Cells](/cells/french/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}