---
category: general
date: 2026-01-14
description: Como incorporar fontes em HTML e forçar o cálculo de fórmulas ao converter
  Excel para HTML. Aprenda a definir a área de impressão e exportar gráficos.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- force formula calculation
- convert excel to html
- how to set print area
language: pt
og_description: Como incorporar fontes em HTML, forçar o cálculo de fórmulas e converter
  Excel para HTML com configurações de área de impressão — tudo em C#.
og_title: Como incorporar fontes em HTML – Guia completo de C#
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Como Incorporar Fontes em HTML – Guia Completo de C#
url: /pt/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Incorporar Fontes em HTML – Guia Completo em C#

Já se perguntou **como incorporar fontes em HTML** ao exportar uma pasta de trabalho do Excel? Você não está sozinho. Muitos desenvolvedores esbarram quando o HTML gerado parece perfeito na máquina deles, mas perde a tipografia em outro dispositivo. A boa notícia? Com Aspose.Cells para .NET você pode incorporar os arquivos de fonte diretamente na saída HTML — nada de glifos ausentes.

Neste tutorial vamos percorrer um exemplo completo que não só mostra **como incorporar fontes em HTML**, mas também demonstra **forçar o cálculo de fórmulas**, **converter Excel para HTML**, e ainda **como definir a área de impressão** antes de exportar um gráfico para um PPTX editável. Ao final, você terá um único programa C# executável que pode ser inserido em qualquer projeto .NET.

---

## O que Você Vai Construir

- Criar uma pasta de trabalho nova, escrever algumas fórmulas de matriz e **forçar o cálculo de fórmulas** para que os resultados fiquem gravados no arquivo.
- Salvar a pasta de trabalho como HTML enquanto **incorpora fontes** e seus seletores de variação.
- Carregar uma segunda pasta de trabalho que contém um gráfico, definir uma **área de impressão**, e exportar essa planilha para uma apresentação PowerPoint editável.
- Tudo isso usando apenas algumas linhas de código C# limpo e bem comentado.

Sem ferramentas externas, sem copiar‑colar manual de arquivos de fonte — o Aspose.Cells faz o trabalho pesado para você.

---

## Pré‑requisitos

| Requisito | Motivo |
|-----------|--------|
| .NET 6.0 ou superior | Recursos modernos da linguagem e melhor desempenho |
| Aspose.Cells para .NET (pacote NuGet `Aspose.Cells`) | Fornece `Workbook`, `HtmlSaveOptions`, `ImageOrPrintOptions`, etc. |
| Alguns arquivos de fonte TrueType/OpenType (ex.: `Arial.ttf`) colocados na pasta do projeto | Necessários para incorporação; o Aspose os buscará automaticamente se estiverem instalados no SO host |
| Conhecimento básico de C# | Para seguir o código e adaptá‑lo aos seus próprios cenários |

---

## Etapa 1 – Criar uma Pasta de Trabalho e Escrever Fórmulas de Matriz  

Primeiro criamos uma nova instância de `Workbook` e inserimos duas fórmulas de matriz nas células **A1** e **A3**. Essas fórmulas (`WRAPCOLS` e `WRAPROWS`) produzem uma pequena matriz 2‑colunas/2‑linhas que veremos renderizada na saída HTML.

```csharp
using Aspose.Cells;

namespace FontEmbeddingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Write WRAPCOLS formula – returns a 2‑column array
            worksheet.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4},2)";

            // Write WRAPROWS formula – returns a 2‑row array
            worksheet.Cells[2, 0].Formula = "=WRAPROWS({1;2;3;4},2)";
```

> **Por que isso importa:** Ao inserir fórmulas você obtém conteúdo dinâmico que será avaliado quando forçarmos o cálculo mais tarde. Também demonstra que a exportação para HTML pode lidar corretamente com resultados de matriz.

---

## Etapa 2 – Forçar o Cálculo de Fórmulas  

O Aspose.Cells avalia fórmulas de forma preguiçosa. Para garantir que nosso HTML contenha os valores calculados (em vez das fórmulas brutas), chamamos `CalculateFormula()`.

```csharp
            // Step 2: Force calculation so the formulas are evaluated
            worksheet.CalculateFormula();
```

> **Dica profissional:** Se você pular esta etapa, o HTML exibirá o texto da fórmula (`=WRAPCOLS...`) em vez dos números, o que anula o objetivo de uma exportação polida.

---

## Etapa 3 – Configurar Opções de Salvamento HTML para Incorporar Fontes  

Agora vem a estrela do show: incorporação de fontes. Definir `EmbedFonts` como `true` instrui o Aspose a incluir os dados da fonte como fluxos codificados em Base64 dentro do arquivo HTML gerado. Habilitar `EmbedFontVariationSelectors` garante que quaisquer seletores de variação OpenType (usados para tipografia avançada) também sejam preservados.

```csharp
            // Step 3: Prepare HTML save options that embed fonts and their variation selectors
            HtmlSaveOptions htmlSaveOptions = new HtmlSaveOptions
            {
                EmbedFonts = true,
                EmbedFontVariationSelectors = true
            };
```

> **Como funciona:** Quando o HTML é escrito, o Aspose injeta um bloco `<style>` com regras `@font-face` que referenciam os URIs de dados incorporados. Os navegadores renderizarão a mesma fonte independentemente das fontes instaladas no cliente.

---

## Etapa 4 – Salvar a Pasta de Trabalho como HTML  

Primeiro persistimos a pasta de trabalho em um arquivo `.xlsx` (caso você precise da fonte) e então a exportamos para HTML usando as opções que acabamos de definir.

```csharp
            // Step 4: Save the workbook as HTML using the configured options
            string outputDir = @"C:\Demo\Output\"; // adjust to your environment
            workbook.Save(Path.Combine(outputDir, "fontDemo.xlsx"));
            workbook.Save(Path.Combine(outputDir, "fontDemo.html"), htmlSaveOptions);
```

> **Resultado:** Abra `fontDemo.html` em qualquer navegador moderno e você verá os valores da matriz renderizados com a fonte incorporada, mesmo que a fonte não esteja instalada na sua máquina.

---

## Etapa 5 – Carregar uma Pasta de Trabalho com um Gráfico e Definir a Área de Impressão  

Em seguida demonstramos **como definir a área de impressão** antes de exportar uma planilha que contém um gráfico. A área de impressão limita o que será renderizado, o que é útil quando você deseja apenas um intervalo específico no PPTX final.

```csharp
            // Step 5: Load a workbook that contains a chart and configure PPTX export options
            Workbook chartWorkbook = new Workbook(Path.Combine(outputDir, "chartEditable.xlsx"));

            // Define the print area (e.g., A1:G20) – this is the SECONDARY keyword in action
            chartWorkbook.Worksheets[0].PageSetup.PrintArea = "A1:G20";
```

> **Por que definir uma área de impressão?** Sem ela, o Aspose exportaria a planilha inteira, potencialmente incluindo linhas/colunas vazias e aumentando o tamanho do arquivo PPTX.

---

## Etapa 6 – Exportar a Planilha para um PPTX Editável  

Por fim exportamos a planilha para um arquivo PowerPoint editável. Definindo `ExportChartAsEditable = true`, o gráfico é salvo como formas nativas do PowerPoint, permitindo que os usuários finais o modifiquem diretamente no PowerPoint.

```csharp
            // Step 6: Configure PPTX export options
            ImageOrPrintOptions pptSaveOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportChartAsEditable = true
            };

            // Step 7: Save as editable PPTX
            chartWorkbook.Save(Path.Combine(outputDir, "editableChart.pptx"), pptSaveOptions);
        }
    }
}
```

> **O que você obtém:** `editableChart.pptx` contém o gráfico de `chartEditable.xlsx` como objetos editáveis do PowerPoint, limitados ao intervalo `A1:G20`.

---

## Visão Geral da Saída Esperada  

| Arquivo | Descrição |
|---------|-----------|
| `fontDemo.xlsx` | Pasta de trabalho original com fórmulas de matriz calculadas. |
| `fontDemo.html` | Arquivo HTML que **incorpora fontes**, mostra os resultados da matriz e funciona offline. |
| `editableChart.pptx` | Apresentação PowerPoint com um gráfico editável, respeitando a **área de impressão** que você definiu. |

Abra `fontDemo.html` no Chrome ou Edge; você notará que o texto usa exatamente a fonte que foi incorporada (ex.: Arial) mesmo que seu sistema não a possua. O gráfico em `editableChart.pptx` pode ser clicado duas vezes e editado como qualquer gráfico nativo do PowerPoint.

---

## Perguntas Frequentes e Casos Limítrofes  

### E se a minha fonte não estiver instalada no servidor?  
O Aspose.Cells só incorporará as fontes que estiverem *disponíveis* em tempo de execução. Se um arquivo de fonte específico estiver ausente, o HTML recairá para a fonte padrão do navegador. Para garantir a incorporação, copie os arquivos `.ttf`/`.otf` necessários para a pasta da aplicação e faça referência a eles via `FontInfo` (cenário avançado).

### Posso incorporar apenas um subconjunto de caracteres para reduzir o tamanho do arquivo?  
Sim. Use `HtmlSaveOptions.FontEmbeddingMode = FontEmbeddingMode.Subset`. Isso indica ao Aspose que inclua somente os glifos realmente usados na pasta de trabalho, reduzindo drasticamente o peso do HTML.

### O **forçar o cálculo de fórmulas** também funciona para funções voláteis como `NOW()`?  
Absolutamente. `CalculateFormula()` avalia todas as fórmulas, incluindo as voláteis, no momento em que você o chama. Se precisar que o cálculo reflita uma data/hora específica, ajuste as `CalculationOptions` da pasta de trabalho antes.

### E quanto a pastas de trabalho grandes – a incorporação de fontes vai inflar o HTML?  
Incorporar fontes adiciona aproximadamente 100‑200 KB por fonte (dependendo do tamanho). Para relatórios massivos, considere vincular a fontes hospedadas na web em vez de incorporá‑las, ou use o modo de subconjunto mencionado anteriormente.

---

## Dicas Profissionais e Melhores Práticas  

- **Salvamentos em lote:** Se você gerar dezenas de arquivos HTML, reutilize a mesma instância de `HtmlSaveOptions` para evitar alocações desnecessárias.  
- **Cache de áreas de impressão:** Ao exportar muitas planilhas, armazene a área de impressão desejada em um arquivo de configuração para manter seu código DRY.  
- **Validar a saída:** Após salvar o HTML, execute uma verificação rápida em um navegador sem interface (ex.: Puppeteer) para garantir que as fontes estejam sendo renderizadas corretamente antes de entregar aos usuários.  
- **Bloqueio de versão:** O código acima tem como alvo o Aspose.Cells 23.12+. Versões mais recentes podem introduzir opções adicionais como `FontEmbeddingMode`. Sempre consulte as notas de versão.

---

## Conclusão  

Cobremos **como incorporar fontes em HTML** usando Aspose.Cells, demonstramos a importância de **forçar o cálculo de fórmulas**, apresentamos um fluxo limpo de **conversão de Excel para HTML**, e explicamos **como definir a área de impressão** antes de exportar um gráfico para um PPTX editável. O exemplo completo e executável está em um único arquivo `Program.cs`, para que você possa copiar, ajustar os caminhos e rodar hoje mesmo.

Pronto para o próximo passo? Experimente trocar a fonte incorporada por uma tipografia personalizada da sua marca, ou teste o modo de incorporação **Subset** para manter seu HTML leve. O mesmo padrão funciona para PDFs, imagens e até exportações CSV — basta mudar a classe `SaveOptions`.

Tem mais dúvidas sobre incorporação de fontes, manipulação de fórmulas ou truques de área de impressão? Deixe um comentário abaixo ou me procure nos fóruns da comunidade Aspose. Boa codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}