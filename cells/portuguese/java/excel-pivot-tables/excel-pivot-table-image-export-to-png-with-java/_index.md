---
category: general
date: 2026-07-03
description: Exporte uma imagem de tabela dinâmica do Excel usando Java. Aprenda como
  definir o formato de imagem PNG com Aspose.Cells passo a passo.
draft: false
keywords:
- excel pivot table image
- set image format png
- Aspose.Cells export
- Java Excel automation
- pivot table to image
language: pt
og_description: Exportação de imagem de tabela dinâmica do Excel em Java explicada.
  Siga este tutorial para definir o formato de imagem PNG de forma rápida e confiável.
og_title: imagem de tabela dinâmica do Excel – guia Java para exportação PNG
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Export an excel pivot table image using Java. Learn how to set image
    format png with Aspose.Cells step‑by‑step.
  headline: 'excel pivot table image: Export to PNG with Java'
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel
- ImageExport
title: 'imagem de tabela dinâmica do Excel: exportar para PNG com Java'
url: /pt/java/excel-pivot-tables/excel-pivot-table-image-export-to-png-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# imagem de tabela dinâmica do Excel – Exportar uma Tabela Dinâmica como PNG em Java

Já precisou transformar uma **excel pivot table image** em um PNG pronto para compartilhamento, mas não sabia por onde começar? Você não está sozinho. Em muitas pipelines de relatórios a tabela dinâmica é a estrela, mas o resto da equipe só quer uma imagem estática. A boa notícia? Com algumas linhas de Java e Aspose.Cells você pode **set image format png** e obter exatamente o que precisa.

Neste guia vamos percorrer todo o processo: carregar uma pasta de trabalho, obter a primeira tabela dinâmica, configurar as opções de exportação e, finalmente, gravar um arquivo PNG nítido no disco. Ao final você terá um trecho reutilizável que pode inserir em qualquer projeto Java.

## O que você aprenderá

- Como carregar uma pasta de trabalho Excel a partir do sistema de arquivos.
- Como localizar uma tabela dinâmica específica em uma planilha.
- Os passos exatos para **set image format png** da imagem exportada.
- Armadilhas comuns (múltiplas tabelas dinâmicas, grandes conjuntos de dados) e como evitá‑las.
- Uma classe Java pronta‑para‑executar que você pode copiar‑colar.

### Pré‑requisitos

- Java 8 ou superior instalado.
- Biblioteca Aspose.Cells for Java (a versão mais recente em 2026‑07‑03).
- Um arquivo Excel (`input.xlsx`) que contém ao menos uma tabela dinâmica.
- Familiaridade básica com Maven ou Gradle para gerenciamento de dependências.

---

## Etapa 1: Adicionar Aspose.Cells ao seu Projeto

Primeiro de tudo—certifique‑se de que o JAR do Aspose.Cells está no seu classpath. Se você estiver usando Maven, adicione isto ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- latest at time of writing -->
</dependency>
```

Para Gradle, é igualmente simples:

```gradle
implementation 'com.aspose:aspose-cells:24.10'
```

> **Dica profissional:** Aspose oferece uma chave de avaliação gratuita de 30 dias. Registre‑se no site deles, então adicione `License.setLicense("Aspose.Cells.lic");` no início do seu programa para desbloquear todos os recursos.

## Etapa 2: Carregar a Pasta de Trabalho e Acessar a Tabela Dinâmica

Agora vamos abrir o arquivo Excel e buscar a primeira tabela dinâmica. O código abaixo faz exatamente isso, e é deliberadamente defensivo—se a pasta de trabalho não tiver planilhas ou a planilha não contiver uma tabela dinâmica, lançaremos uma exceção clara.

```java
import com.aspose.cells.*;

import java.io.File;

public class PivotTableToPng {

    public static void main(String[] args) {
        // Adjust these paths to match your environment
        String inputPath = "YOUR_DIRECTORY/input.xlsx";
        String outputPath = "YOUR_DIRECTORY/pivot.png";

        try {
            // Load the workbook from disk
            Workbook wb = new Workbook(inputPath);

            // Ensure there is at least one worksheet
            if (wb.getWorksheets().getCount() == 0) {
                throw new IllegalStateException("The workbook contains no worksheets.");
            }

            // Grab the first worksheet (index 0)
            Worksheet ws = wb.getWorksheets().get(0);

            // Verify that the worksheet actually has a pivot table
            if (ws.getPivotTables().getCount() == 0) {
                throw new IllegalStateException("No pivot tables found on the first worksheet.");
            }

            // Retrieve the first pivot table
            PivotTable pt = ws.getPivotTables().get(0);

            // -------------------------------------------------
            // Step 3: Configure image export options (PNG)
            // -------------------------------------------------
            ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
            // This is where we **set image format png**
            imgOpt.setImageFormat(ImageFormat.PNG);
            // Optional: increase the DPI for sharper output (default is 96)
            imgOpt.setResolution(300);

            // -------------------------------------------------
            // Step 4: Export the pivot table as an image file
            // -------------------------------------------------
            pt.toImage(outputPath, imgOpt);

            System.out.println("Successfully exported the excel pivot table image to: " + outputPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### Por que essas etapas são importantes

- **Carregar a pasta de trabalho** nos dá acesso às estruturas de dados subjacentes; Aspose.Cells abstrai o parsing de OpenXML de baixo nível.
- **Acessar a planilha** é necessário porque as tabelas dinâmicas estão vinculadas a uma planilha específica. Se você tem várias planilhas, pode percorrer `wb.getWorksheets()` e escolher a que contém a tabela dinâmica desejada.
- **Recuperar a tabela dinâmica** é o coração da operação. `ws.getPivotTables().get(0)` obtém a primeira, mas você também pode buscar por nome com `ws.getPivotTables().get("MyPivot")`.
- **Setting image format png** (a palavra‑chave secundária) indica ao Aspose.Cells que renderize a saída como PNG sem perdas. Esse formato preserva linhas nítidas e texto, ideal para relatórios.
- **Exportar com `toImage`** grava o arquivo em uma única chamada, lidando com paginação e dimensionamento automaticamente.

## Etapa 3: Verificar a Saída

Depois de executar o programa, navegue até `YOUR_DIRECTORY` e você deverá ver `pivot.png`. Abra-o com qualquer visualizador de imagens—note as linhas de grade nítidas e o layout exato que você vê no Excel. Se a imagem parecer borrada, aumente o DPI em `imgOpt.setResolution()`; 300‑600 funciona bem para ativos de qualidade de impressão.

![imagem de tabela dinâmica do excel exportada como PNG](excel-pivot-table-image.png "imagem de tabela dinâmica do excel exportada como PNG")

*Texto alternativo da imagem:* **excel pivot table image exported as PNG**

## Manipulando Múltiplas Tabelas Dinâmicas

E se sua planilha contiver mais de uma tabela dinâmica? O trecho acima obtém a primeira, mas você pode iterar:

```java
for (int i = 0; i < ws.getPivotTables().getCount(); i++) {
    PivotTable pt = ws.getPivotTables().get(i);
    String outFile = "YOUR_DIRECTORY/pivot_" + i + ".png";
    pt.toImage(outFile, imgOpt);
}
```

Esse loop produzirá `pivot_0.png`, `pivot_1.png`, etc., cada um representando uma tabela dinâmica diferente. Lembre‑se de **set image format png** uma vez antes do loop; a mesma instância de `ImageOrPrintOptions` pode ser reutilizada.

## Casos de Borda & Dicas

| Situação | O que observar | Correção sugerida |
|-----------|-------------------|---------------|
| **Grande tabela dinâmica (muitas linhas/colunas)** | PNG pode ficar enorme, causando pressão de memória. | Use `imgOpt.setOnePagePerSheet(false)` para dividir em várias páginas, ou reduza o DPI. |
| **Linhas/colunas ocultas** | Aspose respeita a visibilidade; dados ocultos não aparecerão. | Desoculte programaticamente com `ws.showRows(start, count, true)`. |
| **Estilos personalizados (fontes, cores)** | Algumas fontes corporativas podem não ser renderizadas se não estiverem instaladas no servidor. | Incorpore a fonte na JVM ou recorra a fontes do sistema via `imgOpt.setFontEmbeddingMode(FontEmbeddingMode.EMBED_ALL)`. |
| **Formato de saída diferente necessário mais tarde** | Você pode querer JPEG ou BMP. | Altere `imgOpt.setImageFormat(ImageFormat.JPEG)`—o mesmo código funciona, apenas um valor de enum diferente. |

## Exemplo Completo Funcionando (Copiar‑Colar)

Abaixo está a classe inteira, pronta para compilar. Cole-a em `PivotTableToPng.java`, ajuste os caminhos e execute `javac PivotTableToPng.java && java PivotTableToPng`.

```java
import com.aspose.cells.*;

public class PivotTableToPng {

    public static void main(String[] args) {
        // ----- Configuration -----
        String inputPath = "YOUR_DIRECTORY/input.xlsx";
        String outputPath = "YOUR_DIRECTORY/pivot.png";

        try {
            // Load workbook
            Workbook wb = new Workbook(inputPath);

            // Guard clauses
            if (wb.getWorksheets().getCount() == 0) {
                throw new IllegalStateException("Workbook has no worksheets.");
            }

            Worksheet ws = wb.getWorksheets().get(0);
            if (ws.getPivotTables().getCount() == 0) {
                throw new IllegalStateException("No pivot tables on the first worksheet.");
            }

            // Retrieve the first pivot table
            PivotTable pt = ws.getPivotTables().get(0);

            // ----- Set image format png -----
            ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
            imgOpt.setImageFormat(ImageFormat.PNG);   // <-- key line
            imgOpt.setResolution(300);                // optional, for sharper output

            // Export to PNG
            pt.toImage(outputPath, imgOpt);

            System.out.println("excel pivot table image exported successfully: " + outputPath);
        } catch (Exception ex) {
            System.err.println("Error during export:");
            ex.printStackTrace();
        }
    }
}
```

Execute-o, e você terá uma **excel pivot table image** salva como um arquivo PNG—exatamente o que o tutorial prometeu.

---

## Conclusão

Acabamos de cobrir tudo o que você precisa para **exportar uma excel pivot table image** usando Java, e mostramos exatamente como **set image format png** com Aspose.Cells. Desde o carregamento da pasta de trabalho até o tratamento de casos de borda, a solução é compacta, confiável e pronta para produção.

Qual o próximo passo? Tente exportar múltiplas tabelas dinâmicas em lote, experimente diferentes configurações de DPI para ativos prontos para impressão, ou altere o formato para JPEG para imagens otimizadas para web. Você também pode explorar a incorporação do PNG em um relatório PDF—Aspose.PDF torna isso simples.

Tem alguma variação no seu fluxo de trabalho ou um obstáculo? Deixe um comentário, e vamos solucionar juntos. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Exportar Pasta de Trabalho Excel como Imagem Usando Aspose.Cells para Java: Um Guia Passo a Passo](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Como Atualizar a Fonte da Tabela Dinâmica do Excel com Aspose.Cells para Java: Um Guia Abrangente](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Como Criar Gráfico Excel com Linha de Tendência e Exportar para Imagem usando Aspose.Cells para Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}