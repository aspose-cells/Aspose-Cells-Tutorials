---
category: general
date: 2026-10-07
description: Como dividir colunas usando Aspose.Cells para Java. Aprenda a dividir
  strings em colunas, automatizar fórmulas do Excel e escrever fórmulas em células
  em poucas linhas de código.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to split columns
- split string into columns
- automate excel formula
- write formula to cell
language: pt
lastmod: 2026-10-07
og_description: Como dividir colunas em Java com Aspose.Cells. Este tutorial mostra
  como dividir uma string em colunas, automatizar a avaliação de fórmulas do Excel
  e escrever uma fórmula em uma célula.
og_image_alt: Screenshot of Java code that splits columns in an Excel worksheet using
  Aspose.Cells
og_title: Como dividir colunas em Java com Aspose.Cells – tutorial rápido
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: How to split columns using Aspose.Cells for Java. Learn to split string
    into columns, automate Excel formula, and write formula to cell in a few lines
    of code.
  headline: How to split columns in Java with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Como dividir colunas em Java com Aspose.Cells – guia passo a passo
url: /pt/java/data-manipulation/how-to-split-columns-in-java-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como dividir colunas em Java com Aspose.Cells – guia passo a passo

Se você precisa **como dividir colunas** em uma planilha Excel programaticamente, este guia mostra o processo completo com Aspose.Cells para Java. Você também aprenderá como **dividir string em colunas**, **automatizar a avaliação de fórmulas do Excel** e **escrever fórmula em uma célula** usando código conciso e pronto para produção.

A divisão programática de colunas elimina cópias‑e‑colagens manuais, reduz erros e permite transformações de dados em grande escala. Ao final deste tutorial você poderá gerar, modificar e avaliar fórmulas em tempo real, tornando o Excel uma parte verdadeira do seu backend Java.

## Prerequisites

Antes de começar, certifique‑se de que você tem:

* Java 17 ou posterior instalado.
* Maven 3.8+ (ou Gradle) para gerenciamento de dependências.
* Uma licença do Aspose.Cells para Java (a versão de avaliação gratuita funciona para aprendizado).
* Familiaridade básica com a sintaxe Java e conceitos do Excel.

Se algum desses itens estiver faltando, instale‑os primeiro; os exemplos de código assumem um projeto Maven padrão.

## Step 1: Add Aspose.Cells to your project

Adicione a dependência a seguir ao seu `pom.xml`. Isso traz a biblioteca Aspose.Cells estável mais recente.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version available -->
</dependency>
```

**Why this step matters:** A biblioteca fornece as classes `Workbook`, `Worksheet` e `Cell` necessárias para manipular arquivos Excel sem o Microsoft Office. Sem a dependência o código não compilará.

## Step 2: Create a workbook and select the first worksheet

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize a new workbook and access the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
        Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
```

O objeto `Workbook` representa o arquivo Excel completo. Acessar a primeira planilha garante um ponto de partida previsível para a fórmula que iremos escrever.

## Step 3: Write the WRAPCOLS formula to a target cell

```java
        // Step 3: Identify the target cell (A1) where the formula will be placed
        Cell targetCell = worksheet.getCells().get("A1");

        // Step 3: Write the WRAPCOLS formula to split a long string into three columns
        // WRAPCOLS(string, columns) distributes the string across the specified number of columns.
        targetCell.setFormula("=WRAPCOLS(\"This is a very long string that needs to be split\",3)");
```

**Why we use `WRAPCOLS`:** A função interna do Excel `WRAPCOLS` divide automaticamente um único valor de texto em um número definido de colunas, tratando limites de palavras de forma inteligente. Esta é a maneira mais confiável de **dividir string em colunas** sem lógica de análise personalizada.

## Step 4: Force the workbook to evaluate the formula

```java
        // Step 4: Calculate all formulas in the workbook so the result becomes visible
        workbook.calculateFormula();
```

Chamar `calculateFormula()` **automatiza a avaliação de fórmulas do Excel** no lado do servidor. Sem essa chamada a célula ainda conterá o texto da fórmula, não os valores calculados.

## Step 5: Retrieve and display the wrapped result

```java
        // Step 5: Retrieve the computed value from the target cell
        String result = targetCell.getStringValue(); // returns the first column of the split result
        System.out.println("First column output: " + result);

        // Optionally, read the other columns created by WRAPCOLS
        String second = worksheet.getCells().get("B1").getStringValue();
        String third  = worksheet.getCells().get("C1").getStringValue();

        System.out.println("Second column output: " + second);
        System.out.println("Third column output: " + third);

        // Save the workbook to verify the split visually (optional)
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

Ao executar o programa, o console exibe:

```
First column output: This is a very long
Second column output: string that needs
Third column output: to be split
```

O arquivo gerado `SplitColumnsResult.xlsx` mostra as três colunas preenchidas com o texto dividido.

## Understanding the WRAPCOLS function

* **Syntax:** `WRAPCOLS(text, columns, [delimiter])`
* **Parameters:**
  * `text` – a string que você deseja dividir.
  * `columns` – o número de colunas nas quais distribuir o texto.
  * `delimiter` (optional) – caractere usado para separar a string; o padrão é um espaço.
* **Return value:** Um array que se espalha para células adjacentes, cada elemento contendo uma parte do texto original.

Como a função se espalha horizontalmente, você só precisa escrever a fórmula na célula mais à esquerda (A1 no exemplo). O Excel preenche automaticamente B1, C1, … conforme necessário.

## Common variations and edge cases

| Situation | Recommended adjustment |
|-----------|------------------------|
| **Variable column count** | Replace the hard‑coded `3` with a variable: `targetCell.setFormula(String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount));` |
| **Custom delimiter** | Use the third argument, e.g., `=WRAPCOLS(A2,4,",")` to split on commas. |
| **Empty source string** | The function returns empty cells; guard against `null` or empty strings before setting the formula. |
| **Large datasets** | Apply the formula in a loop for each row, then call `calculateFormula()` once after the loop to improve performance. |
| **Non‑ASCII characters** | WRAPCOLS works with Unicode; ensure your Java source file is saved as UTF‑8. |

**Pro tip:** When processing many rows, store the formula in a string variable and reuse it to avoid repeated string concatenation overhead.

## Full, runnable example

Abaixo está o programa completo pronto para copiar‑colar. Ele inclui declarações de importação, tratamento de exceções e uma operação opcional de salvamento.

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Define the long string and desired column count
        String longString = "This is a very long string that needs to be split";
        int columnCount = 3;

        // Write the WRAPCOLS formula to cell A1
        Cell targetCell = worksheet.getCells().get("A1");
        String formula = String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount);
        targetCell.setFormula(formula);

        // Evaluate all formulas in the workbook
        workbook.calculateFormula();

        // Read and display each column's result
        System.out.println("First column output: " + worksheet.getCells().get("A1").getStringValue());
        System.out.println("Second column output: " + worksheet.getCells().get("B1").getStringValue());
        System.out.println("Third column output: " + worksheet.getCells().get("C1").getStringValue());

        // Save the workbook for visual verification
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

Executar este programa produz a mesma saída de console mostrada anteriormente e grava um arquivo Excel que demonstra claramente **como dividir colunas**.

## Troubleshooting checklist

* **Formula not evaluating** – Ensure `workbook.calculateFormula()` is called after setting the formula.
* **Empty cells after split** – Verify that the source string is not `null` or empty, and that the column count is greater than zero.
* **License exception** – Provide a valid Aspose.Cells license file (`License license = new License(); license.setLicense("Aspose.Total.lic");`) before creating the workbook to remove evaluation watermarks.
* **Performance lag on large sheets** – Call `calculateFormula()` once after all formulas are written, not after each individual cell.

## Conclusion

Agora você sabe **como dividir colunas** em Java usando Aspose.Cells, como **dividir string em colunas** com a função `WRAPCOLS`, como **automatizar a avaliação de fórmulas do Excel** e como **escrever fórmula em uma célula** programaticamente. Essa técnica elimina etapas manuais de preparação de dados e integra as poderosas capacidades de manipulação de texto do Excel diretamente em suas aplicações Java.

### Next steps

* Explore outras funções de texto como `TEXTSPLIT` e `FILTERXML` para cenários de análise mais complexos.
* Combine `WRAPCOLS` com `IFERROR` para lidar com entradas inesperadas de forma elegante.
* Integre a solução em um serviço Spring Boot que recebe dados CSV via REST e devolve um arquivo Excel preenchido.

Ao dominar esses padrões, você pode criar fluxos de trabalho Excel robustos e automatizados que escalam com as necessidades do seu negócio. Feliz codificação!

## What Should You Learn Next?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [aspose cells java – Dividir Nomes em Colunas](/cells/english/java/cell-operations/aspose-cells-java-split-names-columns/)
- [Ajustar Automaticamente Colunas do Excel em Java Usando Aspose.Cells](/cells/english/java/formatting/aspose-cells-java-auto-fit-excel-columns-guide/)
- [Como Excluir Colunas em Branco no Excel Usando Aspose.Cells Java&#58; Um Guia Abrangente](/cells/english/java/worksheet-management/delete-blank-columns-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}