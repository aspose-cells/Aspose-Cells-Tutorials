---
category: general
date: 2026-08-14
description: Incorpore fontes em SVG ao exportar Excel para SVG usando Aspose.Cells.
  Aprenda como definir a área de impressão, definir opções de impressão e usar a função
  WRAPCOLS.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in svg
- export excel to svg
- set print area
- set print options
- use wrapcols function
language: pt
lastmod: 2026-08-14
og_description: Incorpore fontes em SVG ao exportar Excel para SVG com Aspose.Cells.
  Este guia mostra como definir a área de impressão, configurar as opções de impressão
  e aplicar a função WRAPCOLS.
og_image_alt: Screenshot of Java code exporting an Excel sheet to SVG with embedded
  fonts
og_title: Incorporar fontes em SVG ao exportar Excel para SVG – passo a passo
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  headline: Embed fonts in SVG while exporting Excel to SVG
  type: TechArticle
- description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  name: Embed fonts in SVG while exporting Excel to SVG
  steps:
  - name: Run the program.
    text: Run the program.
  - name: Open `output.svg` in a web browser.
    text: Open `output.svg` in a web browser.
  - name: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
    text: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
  - name: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
    text: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
title: Incorporar fontes em SVG ao exportar Excel para SVG
url: /pt/java/excel-import-export/embed-fonts-in-svg-while-exporting-excel-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Incorporar fontes em SVG ao exportar Excel para SVG

Se você precisa **incorporar fontes em SVG ao exportar Excel para SVG**, este tutorial mostra exatamente como fazer isso com Aspose.Cells for Java. Também abordaremos como **definir área de impressão**, **definir opções de impressão** e **usar a função WRAPCOLS** para formatar dados sem perder o layout.

Você seguirá um exemplo completo e executável que carrega uma pasta de trabalho existente, aplica a fórmula `WRAPCOLS`, configura opções de imagem específicas para SVG, define a região de impressão e, finalmente, salva o arquivo como SVG com fontes incorporadas. Nenhuma documentação externa é necessária — basta copiar o código, executá‑lo e inspecionar o SVG resultante.

## Incorporar fontes em SVG – configurando ImageOrPrintOptions

Incorporar fontes garante que o SVG seja renderizado exatamente como aparece no Excel, mesmo em máquinas que não têm as tipografias originais instaladas.

```java
// Create ImageOrPrintOptions for SVG output
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);          // Target format
imgOptions.setEmbedFonts(true);                     // <-- embed fonts in SVG
imgOptions.setFontVariationSelectors(true);        // Preserve variation selectors
```

*Por que isso importa*: Quando `setEmbedFonts(true)` está habilitado, o Aspose.Cells grava os dados da fonte diretamente na seção `<defs>` do SVG. O resultado é um arquivo autônomo que parece idêntico em diferentes navegadores e plataformas.

## Exportar Excel para SVG – fluxo completo

Os passos a seguir ilustram o processo de ponta a ponta, desde o carregamento da pasta de trabalho até a gravação do arquivo SVG.

```java
// Step 1: Load a workbook and access the first worksheet
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = workbook.getWorksheets().get(0);

// Step 2: Apply the WRAPCOLS formula to cell A1
Cell cell = ws.getCells().get("A1");
cell.setFormula("=WRAPCOLS(A2:A10,3)");

// Step 3: Configure image options (see previous section)
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);
imgOptions.setEmbedFonts(true);
imgOptions.setFontVariationSelectors(true);

// Step 4: Define the print area and assign the image options
ws.getPageSetup().setPrintArea("A1:H30");           // <-- set print area
ws.getPageSetup().setPrintOptions(imgOptions);     // <-- set print options

// Step 5: Save the worksheet as an SVG file
ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);
```

**Saída esperada**: `output.svg` aparece em `YOUR_DIRECTORY`. Ao abri‑lo em um navegador, a planilha é exibida com todas as fontes incorporadas, os dados distribuídos em três colunas (graças ao `WRAPCOLS`) e apenas as células dentro de `A1:H30` são renderizadas.

## Definir área de impressão para a planilha

Definir uma área de impressão limita o SVG exportado a um intervalo específico, o que reduz o tamanho do arquivo e concentra o visualizador nos dados relevantes.

```java
// Define a rectangular region that will be exported
ws.getPageSetup().setPrintArea("A1:H30");   // you can change the range as needed
```

*Dica*: O intervalo segue a notação A1 do Excel. Se precisar de um intervalo dinâmico, você pode calculá‑lo programaticamente com `ws.getCells().getMaxDisplayRange()`.

## Definir opções de impressão para a saída SVG

As opções de impressão controlam como o Aspose.Cells traduz a planilha em uma imagem. Além de incorporar fontes, você pode ajustar resolução, escala e layout da página.

```java
// Assign the previously configured ImageOrPrintOptions
ws.getPageSetup().setPrintOptions(imgOptions);
```

*Por que você deve definir opções de impressão*: Sem opções explícitas, o Aspose.Cells usa padrões que podem omitir a incorporação de fontes ou aplicar um fator de escala indesejado, resultando em SVGs borrados ou com estilo incorreto.

## Usar a função WRAPCOLS para envolver dados de coluna

`WRAPCOLS` é uma fórmula do Excel que distribui um intervalo vertical em um número especificado de colunas. É útil quando você deseja exibir uma lista longa em uma grade compacta.

```java
// Insert the WRAPCOLS formula into cell A1
cell.setFormula("=WRAPCOLS(A2:A10,3)");
```

Ao salvar a pasta de trabalho, o Aspose.Cells avalia a fórmula, produzindo um layout de três colunas dentro da área de impressão definida. Essa técnica funciona para qualquer intervalo de tamanho — basta ajustar o segundo argumento para a contagem de colunas desejada.

## Exemplo completo executável

Abaixo está o programa Java completo que você pode colar em qualquer IDE. Certifique‑se de que a biblioteca Aspose.Cells for Java esteja no seu classpath.

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.getWorksheets().get(0);

        // Apply WRAPCOLS to reorganize data
        Cell wrapCell = ws.getCells().get("A1");
        wrapCell.setFormula("=WRAPCOLS(A2:A10,3)");

        // Configure SVG options with embedded fonts
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.SVG);
        imgOptions.setEmbedFonts(true);
        imgOptions.setFontVariationSelectors(true);

        // Set the region that will appear in the SVG
        ws.getPageSetup().setPrintArea("A1:H30");

        // Attach the image options to the worksheet
        ws.getPageSetup().setPrintOptions(imgOptions);

        // Export the worksheet as an SVG file
        ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);

        System.out.println("SVG exported successfully with embedded fonts.");
    }
}
```

**Etapas de verificação**

1. Execute o programa.  
2. Abra `output.svg` em um navegador web.  
3. Confirme que o texto usa a mesma tipografia do arquivo Excel original (as fontes estão incorporadas).  
4. Verifique que apenas as células dentro de `A1:H30` aparecem e que os dados de `A2:A10` são exibidos em três colunas.

## Armadilhas comuns e como evitá‑las

| Problema | Por que acontece | Correção |
|----------|------------------|----------|
| Fontes ausentes no SVG | `setEmbedFonts(false)` ou o arquivo de fonte não está acessível | Garanta `setEmbedFonts(true)` e que a fonte esteja instalada na máquina que executa o código |
| WRAPCOLS não avalia | Motor de cálculo desativado | Chame `workbook.calculateFormula()` antes de exportar, ou deixe o Aspose.Cells avaliar durante a gravação |
| SVG exportado está em branco | A área de impressão não inclui nenhum dado | Verifique novamente o intervalo passado para `setPrintArea` |
| Arquivo SVG é enorme | Nenhuma escala aplicada, alta resolução da imagem | Ajuste `imgOptions.setResolution(96)` ou similar para controlar DPI |

## Dica profissional: reutilizar ImageOrPrintOptions para várias planilhas

Se sua pasta de trabalho contém várias planilhas que precisam das mesmas configurações de SVG, crie uma única instância de `ImageOrPrintOptions` e atribua‑a ao `PageSetup` de cada planilha. Isso reduz o consumo de memória e garante a incorporação consistente de fontes em todos os arquivos exportados.

```java
ImageOrPrintOptions sharedOptions = new ImageOrPrintOptions();
sharedOptions.setImageFormat(ImageFormat.SVG);
sharedOptions.setEmbedFonts(true);
sharedOptions.setFontVariationSelectors(true);

for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    sheet.getPageSetup().setPrintOptions(sharedOptions);
    sheet.getPageSetup().setPrintArea("A1:H30");
    sheet.getPageSetup().save("YOUR_DIRECTORY/sheet" + i + ".svg", SaveFormat.SVG);
}
```

## Próximos passos

* **Exportar para outros formatos vetoriais** – Altere `ImageFormat.SVG` para `ImageFormat.PDF` para PDFs de alta qualidade.  
* **Processamento em lote** – Percorra uma pasta de arquivos `.xlsx` e gere SVGs automaticamente.  
* **Manipulação de fontes personalizadas** – Use `FontSettings` para carregar fontes de um diretório específico quando as fontes do sistema forem insuficientes.  

Ao dominar **embed fonts in SVG**, **export excel to svg**, **set print area**, **set print options** e **use WRAPCOLS function**, você pode automatizar a geração de SVGs de alta fidelidade para relatórios, painéis e visualizações web diretamente a partir dos dados do Excel. Feliz codificação!

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}