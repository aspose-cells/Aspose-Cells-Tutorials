---
category: general
date: 2026-08-20
description: Aprenda como exportar gráfico para docx e converter pasta de trabalho
  do Excel para docx com Aspose.Cells em Java. Guia passo a passo com código completo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export chart to docx
- convert excel workbook to docx
- Aspose.Cells Java
- editable chart DOCX
- Excel to Word conversion
language: pt
lastmod: 2026-08-20
og_description: Exporte o gráfico para docx e converta a planilha do Excel para docx
  usando Aspose.Cells para Java. Siga este tutorial completo e executável.
og_image_alt: Screenshot showing a Java code editor exporting an Excel chart to a
  DOCX file
og_title: Exportar gráfico para docx com Aspose.Cells – Guia Java
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn how to export chart to docx and convert Excel workbook to docx
    with Aspose.Cells in Java. Step‑by‑step guide with complete code.
  headline: How to export chart to docx from Excel using Aspose.Cells for Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- DOCX
- Excel
title: Como exportar gráfico para docx a partir do Excel usando Aspose.Cells para
  Java
url: /pt/java/integration-interoperability/how-to-export-chart-to-docx-from-excel-using-aspose-cells-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportar gráfico para docx a partir de uma pasta de trabalho Excel usando Java

Se você precisa **exportar gráfico para docx** diretamente de um arquivo Excel, este tutorial mostra uma solução pronta‑para‑executar. Ao final do guia você também saberá como **converter pasta de trabalho Excel para docx** preservando um gráfico editável, de modo que o documento Word resultante possa ser modificado sem perder fidelidade.

Exportar gráficos é comum ao gerar relatórios que combinam cálculos de planilhas com layouts ricos do Word. Aspose.Cells for Java torna a conversão simples, e a API permite manter o gráfico editável—nenhuma imagem estática necessária.

## O que este tutorial cobre

* Carregar uma pasta de trabalho existente que contém um gráfico.  
* Configurar `ImageOrPrintOptions` para o formato DOCX.  
* Habilitar a flag `ExportEditableCharts` (disponível a partir da versão 25.10).  
* Salvar a pasta de trabalho como um arquivo DOCX que mantém um gráfico editável.  

Nenhuma ferramenta externa é necessária além do JAR do Aspose.Cells. O código funciona com Java 8+ e qualquer versão recente do Aspose.Cells.

## Pré-requisitos

| Requisito | Por que é importante |
|-------------|----------------|
| **Aspose.Cells for Java** (v25.10 ou posterior) | O recurso `setExportEditableCharts` foi introduzido nesta versão. |
| **Java Development Kit (JDK) 8 ou mais recente** | Fornece o runtime para compilar e executar o exemplo. |
| **Uma pasta de trabalho Excel (`.xlsx`) que contém ao menos um gráfico** | O gráfico é o objeto que será exportado para DOCX. |
| **Um IDE Java ou ferramenta de build (por exemplo, Maven, Gradle)** | Simplifica o gerenciamento de dependências e a execução. |

Você pode baixar o JAR mais recente do Aspose.Cells no [site da Aspose](https://products.aspose.com/cells/java/).

## Etapa 1: Configurar o projeto e adicionar a dependência Aspose.Cells

Se você usa Maven, adicione a seguinte dependência ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version> <!-- use the latest version -->
</dependency>
```

Para Gradle, adicione:

```gradle
implementation 'com.aspose:aspose-cells:25.10'
```

> **Dica profissional:** Use a versão exata que introduziu `ExportEditableCharts` (25.10) ou qualquer versão mais recente. Versões antigas ignorarão a flag e produzirão uma imagem estática.

## Etapa 2: Carregar a pasta de trabalho que contém o gráfico

A classe `Workbook` representa o arquivo Excel completo. Carregá‑lo é uma operação de uma linha:

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Load the workbook with the chart you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");
```

> **Por que isso importa:** A pasta de trabalho deve estar totalmente carregada antes de aplicar quaisquer opções de exportação. Se o caminho do arquivo estiver incorreto, o Aspose.Cells lança uma `FileNotFoundException`.

## Etapa 3: Configurar opções de imagem/impressão para saída DOCX

`ImageOrPrintOptions` controla como a pasta de trabalho é renderizada. Definir o formato de salvamento como `DOCX` indica ao Aspose.Cells que deve gerar um documento Word em vez de uma imagem.

```java
        // Create options and specify DOCX as the target format
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);
```

Você também pode ajustar o tamanho da página, DPI ou qualidade da imagem aqui, mas são opcionais para a exportação de gráficos.

## Etapa 4: Habilitar a exportação de gráficos editáveis

A partir da versão 25.10, o Aspose.Cells pode incorporar gráficos como objetos nativos de gráfico do Word. Isso os torna totalmente editáveis no Microsoft Word.

```java
        // Turn on the editable chart export flag
        options.setExportEditableCharts(true);
```

> **Caso extremo:** Se você definir essa flag como `false` (ou omití‑la), o gráfico será renderizado como uma imagem estática. Use `true` somente quando o público‑alvo precisar editar o gráfico após a conversão.

## Etapa 5: Salvar a pasta de trabalho como um arquivo DOCX

Finalmente, invoque `Workbook.save` com as opções configuradas:

```java
        // Save the workbook as a DOCX document that contains an editable chart
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

Quando o programa terminar, abra `ChartEditable.docx` no Microsoft Word. Você deverá ver o gráfico original e, se clicar com o botão direito nele, a opção **Edit Data** estará disponível—confirmando que o gráfico está realmente editável.

## Exemplo completo e executável

Abaixo está o arquivo fonte completo. Copie‑o para o seu IDE, substitua `YOUR_DIRECTORY` por um caminho absoluto ou relativo e execute.

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains the chart
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");

        // Step 2: Create image/print options and set the target format to DOCX
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);

        // Step 3: Enable exporting of editable charts (available from version 25.10)
        options.setExportEditableCharts(true);

        // Step 4: Save the workbook as a DOCX document with the configured options
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

**Saída esperada**

* Um arquivo chamado `ChartEditable.docx` no diretório especificado.  
* Abrir o arquivo no Word mostra o gráfico exatamente como apareceu no Excel, e você pode clicar duas vezes no gráfico para editar sua série de dados.

## Armadilhas comuns e como evitá‑las

| Sintoma | Causa | Correção |
|---------|-------|----------|
| Word mostra uma **imagem estática** em vez de um gráfico editável | `setExportEditableCharts` não chamado ou usando uma versão < 25.10 | Certifique‑se de que a flag está definida como `true` e que você está usando Aspose.Cells 25.10 ou mais recente. |
| O DOCX gerado está **em branco** | Caminho de arquivo incorreto para a pasta de trabalho fonte ou permissões insuficientes | Verifique o caminho da pasta de trabalho e se a aplicação tem acesso de leitura/escrita. |
| Layout do gráfico parece **distorto** | Configuração de página no Excel (por exemplo, linhas/colunas ocultas) difere dos padrões do Word | Ajuste `ImageOrPrintOptions` (por exemplo, `setOnePagePerSheet(true)`) para controlar a escala. |
| **Desempenho** degrada em pastas de trabalho grandes | Exportação de muitos gráficos ou conjuntos de dados grandes | Exporte apenas as planilhas necessárias ou use `setSheetIndex` para limitar o processamento. |

## Expandindo a solução

* **Múltiplos gráficos:** Itere sobre todas as planilhas e chame `worksheet.getCharts()` para exportar cada gráfico individualmente.  
* **Estilização personalizada de DOCX:** Após salvar, use Aspose.Words para aplicar cabeçalhos, rodapés ou estilos ao documento gerado.  
* **Conversão em lote:** Envolva o código em um loop que processa um diretório de arquivos `.xlsx`, produzindo um DOCX para cada um.

## Conclusão

Agora você tem um método confiável para **exportar gráfico para docx** e **converter pasta de trabalho Excel para docx** preservando a total editabilidade do gráfico. As etapas principais são carregar a pasta de trabalho, configurar `ImageOrPrintOptions` para DOCX, habilitar `ExportEditableCharts` e salvar o resultado.

Experimente opções adicionais—como definir margens de página ou incorporar as fórmulas da pasta de trabalho—para adaptar a saída ao seu fluxo de trabalho de relatórios. Quando precisar gerar relatórios Word a partir de dados Excel programaticamente, esta abordagem oferece uma solução limpa e sustentável.

--- 

*Pronto para experimentar? Clone o exemplo, atualize os caminhos dos arquivos e execute o programa. Se encontrar algum problema, consulte a documentação do Aspose.Cells for Java ou explore os tópicos relacionados abaixo.*  

### Tópicos relacionados que você pode explorar a seguir

* **convert excel workbook to pdf** – gerar relatórios PDF a partir da mesma pasta de trabalho.  
* **Aspose.Cells chart formatting** – personalizar cores, marcadores e eixos antes da exportação.  
* **Embedding images in DOCX with Aspose.Words** – combinar gráficos com outros conteúdos do Word.  

Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como criar gráfico Excel com linha de tendência e exportar para imagem usando Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Automatizar acesso a gráficos Excel usando Aspose.Cells Java: um guia passo a passo](/cells/english/java/charts-graphs/excel-charts-access-aspose-cells-java/)
- [Personalizar rótulos de dados de gráficos Excel usando Aspose.Cells for Java: um guia passo a passo](/cells/english/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}