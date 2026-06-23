---
category: general
date: 2026-03-27
description: Como vincular dados em C# usando Aspose.Cells – aprenda a salvar a pasta
  de trabalho como XLSX, adicionar um gráfico e exportar o Excel com gráfico em minutos.
draft: false
keywords:
- how to bind data
- save workbook as xlsx
- create excel workbook c#
- how to add chart
- export excel with chart
language: pt
og_description: Como vincular dados em C# com Aspose.Cells. Este guia mostra como
  salvar a pasta de trabalho como XLSX, adicionar um gráfico e exportar o Excel com
  o gráfico.
og_title: Como Vincular Dados em C# – Criar Pasta de Trabalho do Excel
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Como Vincular Dados em C# – Criar Pasta de Trabalho do Excel
url: /pt/net/excel-data-import-export/how-to-bind-data-in-c-create-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Vincular Dados em C# – Criar Pasta de Trabalho Excel

Já se perguntou **como vincular dados** a um gráfico em C# sem perder a cabeça? Você não está sozinho. Muitos desenvolvedores esbarram em um obstáculo quando precisam gerar arquivos Excel programaticamente que realmente *pareçam* com os que criariam manualmente.  

Neste tutorial vamos percorrer um exemplo completo, pronto‑para‑executar, que cria uma pasta de trabalho Excel, preenche‑a com dados, vincula esses dados a um gráfico Waterfall e, por fim, salva o arquivo como `.xlsx`. Ao final, você saberá exatamente como **salvar pasta de trabalho como XLSX**, **como adicionar gráfico** a uma planilha e como **exportar Excel com gráfico** para relatórios posteriores.

> **Pré‑requisitos** – Você precisa do Aspose.Cells para .NET (a versão de avaliação funciona) e de um ambiente de desenvolvimento .NET como o Visual Studio 2022. Nenhum outro pacote NuGet é necessário.

---

## O Que Este Guia Cobre

- **Criar pasta de trabalho Excel C#** – configurar um novo `Workbook` e uma planilha.  
- **Como vincular dados** – mapear sua série numérica e rótulos de categoria para a fonte de dados do gráfico.  
- **Como adicionar gráfico** – inserir um gráfico Waterfall e configurar seu título.  
- **Salvar pasta de trabalho como XLSX** – persistir o arquivo em disco para que qualquer pessoa possa abri‑lo no Excel.  
- **Exportar Excel com gráfico** – o produto final é uma pasta de trabalho totalmente funcional que você pode compartilhar.

Se você está confortável com a sintaxe básica de C#, achará isso muito simples. Vamos começar.

---

## Etapa 1: Criar uma Pasta de Trabalho Excel em C#  

Primeiro de tudo – precisamos de um objeto workbook para trabalhar. Pense na classe `Workbook` como o caderno vazio que você preencherá depois com páginas (planilhas) e conteúdo.

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;

class WaterfallDemo
{
    static void Main()
    {
        // Initialize a new workbook – this is your blank Excel file.
        Workbook workbook = new Workbook();

        // Grab the first worksheet (index 0). It’s already created for us.
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Dica:** Se precisar de várias planilhas, basta chamar `workbook.Worksheets.Add()` e manter uma referência a cada nova `Worksheet`.

---

## Etapa 2: Preencher a Planilha com Categorias e Valores  

Agora vamos **criar dados no estilo excel workbook c#**. O exemplo usa um cenário clássico de Waterfall: início, receita, custo, lucro e fim.  

```csharp
        // Add header labels.
        worksheet.Cells["A1"].PutValue("Category");
        worksheet.Cells["B1"].PutValue("Amount");

        // Sample data – you can replace these with your own source (database, API, etc.).
        string[] categoryLabels = { "Start", "Revenue", "Cost", "Profit", "End" };
        double[] values = { 0, 150, -70, 0, 80 };

        // Fill rows 2‑6 with the data.
        for (int i = 0; i < categoryLabels.Length; i++)
        {
            worksheet.Cells[i + 1, 0].PutValue(categoryLabels[i]); // Column A
            worksheet.Cells[i + 1, 1].PutValue(values[i]);       // Column B
        }
```

Por que colocamos `0` para “Start” e “Profit”? Em um gráfico Waterfall esses zeros funcionam como *conectores* que fazem o fluxo visual ficar correto. Se você os omitir, o gráfico ficará quebrado.

---

## Etapa 3: Como Adicionar Gráfico – Inserir um Gráfico Waterfall  

Com os dados no lugar, é hora de **como adicionar gráfico**. Aspose.Cells torna isso tão fácil quanto chamar `Charts.Add`.

```csharp
        // Insert a Waterfall chart starting at row 7, column 0 and spanning to row 25, column 10.
        int chartIndex = worksheet.Charts.Add(ChartType.Waterfall, 7, 0, 25, 10);
        Chart waterfallChart = worksheet.Charts[chartIndex];

        // Give the chart a meaningful title.
        waterfallChart.Title.Text = "Quarterly Waterfall";
```

As coordenadas `(7,0,25,10)` definem a célula superior‑esquerda e a célula inferior‑direita da caixa delimitadora do gráfico. Ajuste‑as conforme o layout desejado.

---

## Etapa 4: Como Vincular Dados – Conectar Séries e Categorias  

Aqui está o coração do tutorial: **como vincular dados** ao gráfico. O método `NSeries.Add` recebe o intervalo de valores Y, enquanto `CategoryData` aponta para os rótulos do eixo X.

```csharp
        // Bind the numeric series (values) – the second parameter “true” tells Aspose to treat it as a series.
        waterfallChart.NSeries.Add("B2:B6", true);

        // Bind the category (X‑axis) labels.
        waterfallChart.NSeries.CategoryData = "A2:A6";
```

Observe que referenciamos as mesmas células que preenchemos antes (`A2:A6` para categorias, `B2:B6` para valores). Se mudar a disposição dos dados, basta atualizar esses intervalos.

---

## Etapa 5: Salvar Pasta de Trabalho como XLSX – Persistir o Arquivo  

Por fim, **salvar pasta de trabalho como XLSX**. O método `Save` escolhe automaticamente o formato correto com base na extensão do arquivo.

```csharp
        // Save the workbook to disk. Replace YOUR_DIRECTORY with an actual path.
        workbook.Save("YOUR_DIRECTORY/WaterfallChart.xlsx");
    }
}
```

Ao abrir `WaterfallChart.xlsx` no Excel, você verá um gráfico Waterfall bem renderizado que reflete os dados inseridos. Essa é a parte de **exportar excel com gráfico** concluída.

---

## Resultado Esperado  

- **Arquivo Excel:** `WaterfallChart.xlsx` localizado na pasta que você especificou.  
- **Layout da planilha:** A coluna A contém as categorias, a coluna B contém os valores, e o gráfico fica abaixo da tabela.  
- **Aparência do gráfico:** Um gráfico Waterfall intitulado “Quarterly Waterfall” com cinco colunas representando Start, Revenue, Cost, Profit e End.  

![exemplo de gráfico waterfall vinculando dados](waterfall_chart.png "Gráfico Waterfall gerado pelo Aspose.Cells")

*O texto alternativo da imagem inclui a palavra‑chave principal, ajudando tanto no SEO quanto na citação por IA.*

---

## Perguntas Frequentes & Casos de Borda  

### E se minha fonte de dados for dinâmica?  
Substitua os arrays estáticos por um loop que leia de um banco de dados ou de uma API. Enquanto você escrever os valores no mesmo intervalo de células, o código de vinculação permanece inalterado.

### Posso mudar o tipo de gráfico?  
Claro. Troque `ChartType.Waterfall` por `ChartType.Column`, `ChartType.Line`, etc. Apenas lembre‑se de ajustar os dados da série se o novo gráfico exigir uma disposição diferente.

### Como definir as cores do gráfico?  
Use `waterfallChart.NSeries[0].Format.Fill.ForeColor = Color.Yellow;` (ou qualquer `System.Drawing.Color`). Isso é útil quando você quer que a coluna “Profit” se destaque.

### E se eu precisar exportar para PDF em vez de XLSX?  
Chame `workbook.Save("Report.pdf", SaveFormat.Pdf);`. O gráfico será renderizado no PDF automaticamente.

---

## Dicas para Código Pronto para Produção  

- **Liberar objetos** – Envolva `Workbook` em um bloco `using` se estiver usando .NET Core para liberar recursos rapidamente.  
- **Manipulação de caminhos** – Use `Path.Combine(Environment.CurrentDirectory, "WaterfallChart.xlsx")` para evitar codificar separadores manualmente.  
- **Tratamento de erros** – Capture `Exception` ao redor de `Save` para detectar problemas de permissão ou espaço em disco logo no início.  
- **Verificação de versão** – Aspose.Cells 23.10+ introduziu suporte aprimorado a Waterfall; certifique‑se de estar em uma versão recente para obter os melhores resultados.

---

## Conclusão  

Agora você tem um exemplo completo, de ponta a ponta, que demonstra **como vincular dados** em C#, **criar pasta de trabalho excel c#**, **como adicionar gráfico**, **salvar pasta de trabalho como xlsx** e **exportar excel com gráfico**. O código está pronto para ser inserido em qualquer projeto .NET, e os conceitos escalam para conjuntos de dados maiores e diferentes tipos de gráficos.

Pronto para o próximo passo? Experimente adicionar múltiplas séries, teste gráficos empilhados ou automatize a geração de relatórios mensais que são enviados por e‑mail aos interessados. O céu é o limite depois que você domina o básico da automação Excel com Aspose.Cells.

Bom código, e que suas planilhas sempre sejam renderizadas perfeitamente!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}