---
category: general
date: 2026-08-04
description: como usar wrapcols com um exemplo completo em Java, reformar array no
  Excel e salvar a pasta de trabalho em arquivo usando Aspose.Cells
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- save workbook to file
- reshape array in excel
- excel wrapcols example
- create excel workbook java
language: pt
lastmod: 2026-08-04
og_description: Como usar wrapcols para remodelar um array no Excel com Java. Aprenda
  um exemplo completo de wrapcols no Excel, crie uma planilha Excel em Java e salve
  a planilha em um arquivo.
og_image_alt: Screenshot showing how to use WRAPCOLS in Java to reshape an array in
  Excel
og_title: como usar wrapcols em Java – guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: how to use wrapcols with a complete Java example, reshape array in
    Excel and save workbook to file using Aspose.Cells
  headline: how to use wrapcols in Java – reshape array in Excel
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Como usar wrapcols em Java – remodelar array no Excel
url: /pt/java/advanced-features/how-to-use-wrapcols-in-java-reshape-array-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# como usar wrapcols em Java – remodelar array no Excel

Se você precisa **how to use wrapcols** para transformar uma lista plana de valores em um intervalo de várias linhas, este guia mostra as etapas exatas. Você verá um **excel wrapcols example** que remodela um array 1‑D em um bloco de 3 linhas × 2 colunas, e aprenderá como **save workbook to file** com Aspose.Cells.

Ao final deste tutorial você será capaz de criar código **create excel workbook java** que:

* Inicializa uma nova pasta de trabalho e seleciona a célula A1.  
* Aplica a função `WRAPCOLS` para remodelar os dados.  
* Força o cálculo da fórmula para que o resultado apareça instantaneamente.  
* Recupera um valor do array calculado.  
* Persiste a pasta de trabalho no disco.

O único pré-requisito é um ambiente de desenvolvimento Java (JDK 8 ou mais recente) e a biblioteca Aspose.Cells for Java.

---

## Pré-requisitos

* JDK 8 + (ou qualquer versão posterior).  
* Maven ou Gradle para gerenciar a dependência Aspose.Cells.  
* Familiaridade básica com a sintaxe Java e fórmulas do Excel.

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **Dica profissional:** Se você usar Gradle, substitua o trecho XML pela linha `implementation` correspondente.

---

## Etapa 1: Criar uma pasta de trabalho Excel em Java

A primeira operação é criar código **create excel workbook java** que abre uma nova pasta de trabalho e obtém a primeira planilha e a célula A1.

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Access cell A1 where the formula will be placed
        Cell targetCell = worksheet.getCells().get("A1");
```

Criar a pasta de trabalho desta forma fornece uma tela limpa, garantindo que o exemplo funcione em qualquer máquina sem um arquivo existente.

---

## Etapa 2: Aplicar a função WRAPCOLS – um exemplo de excel wrapcols

`WRAPCOLS` recebe um array unidimensional e uma contagem de colunas, então retorna um intervalo que preenche linhas primeiro. Este é o núcleo de **reshape array in excel**.

```java
        // Step 2: Set the WRAPCOLS formula
        // {1,2,3,4,5,6} is the source 1‑D array
        // 2 tells WRAPCOLS to create 2 columns per row
        targetCell.setFormula("=WRAPCOLS({1,2,3,4,5,6}, 2)");
```

Por que isso funciona:

* O array literal `{1,2,3,4,5,6}` fornece seis números.  
* `WRAPCOLS(..., 2)` indica ao Excel para envolver os valores em 2 colunas, gerando automaticamente linhas suficientes (neste caso 3) para acomodar todos os itens.  
* O intervalo resultante ocupa as células **A1:B3**:

| A | B |
|---|---|
| 1 | 2 |
| 3 | 4 |
| 5 | 6 |

---

## Etapa 3: Forçar o cálculo para que a pasta de trabalho reflita a fórmula

Aspose.Cells não avalia fórmulas automaticamente quando você as define. Você deve chamar `calculateFormula()` para materializar o resultado.

```java
        // Step 3: Recalculate all formulas in the workbook
        workbook.calculateFormula();
```

Chamar este método garante que o array produzido por `WRAPCOLS` seja escrito nas células, permitindo que você leia os valores imediatamente.

---

## Etapa 4: Recuperar um valor do array remodelado

Para provar que a fórmula funcionou, leia a representação em string da célula alvo. Como `WRAPCOLS` retorna um array, o Excel exibe o **primeiro elemento** (valor `1`) na célula onde a fórmula está.

```java
        // Step 4: Print the first element of the array (cell A1)
        System.out.println("First element: " + targetCell.getStringValue());
```

**Saída esperada no console**

```
First element: 1
```

Se você inspecionar a planilha no Excel, verá o bloco completo de 3 × 2 preenchido conforme descrito anteriormente.

---

## Etapa 5: Salvar a pasta de trabalho em um arquivo – como salvar workbook to file

Persistir a pasta de trabalho permite que você a abra mais tarde no Excel ou a compartilhe com colegas. Use o método `save` com um caminho completo.

```java
        // Step 5: Save the workbook to disk
        String outputPath = "WrapFunctions.xlsx"; // adjust directory as needed
        workbook.save(outputPath);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

Executar o programa gera `WrapFunctions.xlsx` no diretório de trabalho. Abrir o arquivo revela o array remodelado nas células A1:B3, confirmando que **save workbook to file** foi bem-sucedido.

---

## Exemplo completo e executável

Juntando todas as peças, aqui está o programa completo que você pode copiar‑colar em uma IDE e executar:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cell targetCell = worksheet.getCells().get("A1");

        // Apply WRAPCOLS to reshape a 1‑D array into a 3‑row × 2‑col range
        targetCell.setFormula("=WRAPCOLS({1,2,3,4,5,6}, 2)");

        // Force formula evaluation
        workbook.calculateFormula();

        // Output the first element of the resulting array
        System.out.println("First element: " + targetCell.getStringValue());

        // Save the workbook to a file
        String outputPath = "WrapFunctions.xlsx";
        workbook.save(outputPath);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

**Verificação do resultado**

1. O console imprime `First element: 1`.  
2. O `WrapFunctions.xlsx` gerado contém:

| A | B |
|---|---|
| 1 | 2 |
| 3 | 4 |
| 5 | 6 |

Se precisar referenciar o array em outro lugar, você pode ler qualquer uma das células preenchidas usando `worksheet.getCells().get("B2").getIntValue()`, por exemplo.

---

## Perguntas comuns e casos de borda

| Question | Answer |
|----------|--------|
| *O WRAPCOLS pode lidar com arrays não numéricos?* | Sim. Você pode passar strings, datas ou valores lógicos dentro das chaves, e o Excel os envolverá adequadamente. |
| *E se eu precisar de mais linhas do que o Excel pode exibir?* | WRAPCOLS continuará espalhando em linhas adicionais até que o array de origem seja esgotado. Certifique-se de que a planilha tenha linhas suficientes (limite padrão é 1.048.576). |
| *Como mudar o número de colunas?* | Modifique o segundo argumento de `WRAPCOLS`. Para três colunas, use `=WRAPCOLS({1,2,3,4,5,6}, 3)`, que produz um bloco de 2 × 3. |
| *É possível escrever o resultado em uma célula inicial diferente?* | Sim. Defina a fórmula em qualquer célula (por exemplo, `C5`) e o intervalo envolvido se expandirá em relação a essa célula. |
| *Preciso chamar `calculateFormula` toda vez que mudar a fórmula?* | Sempre que você modificar uma fórmula programaticamente, invoque `calculateFormula` ou `calculateFormula(true)` para atualizar as células dependentes. |

---

## Conclusão

Este tutorial demonstrou **how to use wrapcols** em Java para **reshape array in excel**, forneceu um **excel wrapcols example** claro e mostrou a forma correta de **save workbook to file**. Agora você tem uma base sólida para projetos **create excel workbook java** que precisam de transformações dinâmicas de arrays.

Em seguida, explore tópicos relacionados como **using other array functions** (`TRANSPOSE`, `SEQUENCE`) ou **writing large data sets** com a API de streaming do Aspose.Cells. Experimente diferentes arrays de origem, contagens de colunas e posições iniciais para adaptar o padrão aos seus próprios fluxos de trabalho de relatórios ou processamento de dados. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [How to Open an Excel File Using Aspose.Cells for Java: A Complete Guide](/cells/english/java/getting-started/open-excel-aspose-cells-java-guide/)
- [How to Create and Merge Excel Workbooks Using Aspose.Cells for Java | Complete Guide](/cells/english/java/workbook-operations/create-merge-excel-workbooks-aspose-cells-java/)
- [How to Render Excel Sheets as Images Using Aspose.Cells for Java (Workbook Operations)](/cells/english/java/workbook-operations/render-excel-sheets-images-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}