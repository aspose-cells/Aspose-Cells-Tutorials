---
category: general
date: 2026-09-11
description: Crie uma nova planilha e copie um intervalo do Excel usando Aspose.Cells.
  Aprenda como copiar intervalos entre planilhas preservando as tabelas dinâmicas.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new worksheet
- copy excel range
- copy range between sheets
- copy range aspose.cells
language: pt
lastmod: 2026-09-11
og_description: Crie uma nova planilha e copie um intervalo do Excel com Aspose.Cells.
  Este tutorial mostra as etapas exatas para copiar o intervalo entre planilhas e
  manter as tabelas dinâmicas intactas.
og_image_alt: Screenshot of a Java IDE showing code that creates a new worksheet and
  copies an Excel range
og_title: Criar nova planilha e copiar intervalo do Excel – Guia Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Create new worksheet and copy Excel range using Aspose.Cells. Learn
    how to copy range between sheets while preserving pivot tables.
  headline: Create new worksheet and copy Excel range with Aspose.Cells
  type: TechArticle
- questions:
  - answer: The `copy` method also copies merge information, so merged cells appear
      unchanged on the destination sheet.
    question: What if the source range contains merged cells?
  - answer: Yes. Load a second `Workbook` instance, create a destination range in
      that workbook, and call `sourceRange.copy(destinationRange)`. The method handles
      cross‑workbook copying automatically.
    question: Can I copy to a different workbook?
  - answer: The copy operation overwrites any existing cells that intersect the destination
      range. To avoid data loss, ensure the destination area is empty or use a different
      start cell (e.g., `"B2"`).
    question: What if the destination sheet already has data?
  - answer: Aspose.Cells reuses the original pivot cache, which means the new pivot
      table remains linked to the same source data. If you need an independent cache,
      you must recreate the pivot table after copying.
    question: Is the pivot cache duplicated?
  type: FAQPage
tags:
- Aspose.Cells
- Excel automation
- Java
title: Criar nova planilha e copiar intervalo do Excel com Aspose.Cells
url: /pt/java/range-management/create-new-worksheet-and-copy-excel-range-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar nova planilha e copiar intervalo do Excel com Aspose.Cells

Se você precisa **criar nova planilha** e mover dados dentro de um arquivo Excel, o Aspose.Cells torna isso simples. Este guia mostra exatamente como copiar um intervalo do Excel de uma planilha para outra, preservando quaisquer tabelas dinâmicas dentro do intervalo.

Você aprenderá como **copiar intervalo do Excel**, como **copiar intervalo entre planilhas**, e por que o método `copy` do Aspose.Cells mantém as definições da tabela dinâmica intactas. Nenhuma ferramenta externa é necessária — apenas um projeto Java com a biblioteca Aspose.Cells.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

- Java 17 ou superior instalado
- Aspose.Cells for Java (versão 23.12 ou mais recente) adicionada ao classpath do seu projeto
- Uma pasta de trabalho de origem (`input.xlsx`) que contenha uma tabela dinâmica no intervalo que você deseja copiar
- Familiaridade básica com a sintaxe Java e gerenciamento de dependências Maven/Gradle

## Etapa 1: Configurar o projeto e importar Aspose.Cells

Crie um projeto Maven simples (ou Gradle, se preferir) e adicione a dependência Aspose.Cells:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

Em seguida, importe as classes necessárias no seu arquivo fonte Java:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

*Por que esta etapa importa*: Importar as classes corretas dá acesso a `Workbook`, `Worksheet`, `Range` e ao método `copy` que realizará a transferência do intervalo.

## Etapa 2: Carregar a pasta de trabalho de origem

Abra a pasta de trabalho que contém os dados que você deseja copiar. O código a seguir carrega `input.xlsx` a partir de um diretório que você especificar:

```java
public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Explicação*: `Workbook` representa o arquivo Excel completo. Carregá‑lo uma única vez fornece acesso de leitura/escrita a todas as planilhas e coleções de células.

## Etapa 3: Identificar o intervalo de origem que inclui a tabela dinâmica

Selecione a planilha que contém a tabela dinâmica e defina o bloco exato de células que você deseja copiar. Neste exemplo copiamos as células de A1 a D20:

```java
        // Get the first worksheet (index 0) that contains the pivot table
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the source range – this range includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");
```

*Por que isso importa*: Ao criar um objeto `Range`, você informa ao Aspose.Cells exatamente quais células (incluindo quaisquer objetos incorporados, como tabelas dinâmicas) devem ser duplicadas.

## Etapa 4: **Criar nova planilha** que receberá os dados copiados

Agora adicionamos uma planilha nova ao mesmo workbook. Este é o ponto onde a palavra‑chave principal aparece:

```java
        // Create a new worksheet named "Copy"
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // Define the top‑left cell of the destination range
        Range destinationRange = destinationSheet.getCells().createRange("A1");
```

*Explicação*: Adicionar uma nova planilha isola os dados copiados, facilitando a verificação de que a operação **copy excel range** foi bem‑sucedida sem afetar a planilha original.

## Etapa 5: Copiar o intervalo – a tabela dinâmica é preservada automaticamente

Use o método `copy` para mover o intervalo da planilha de origem para a planilha de destino. O Aspose.Cells copia fórmulas, formatação e definições de tabelas dinâmicas:

```java
        // Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);
```

*Por que isso funciona*: O método `copy` realiza uma cópia profunda das células de origem. Ele não copia apenas valores; replica toda a estrutura da célula, que inclui o cache da tabela dinâmica. É por isso que você pode **copy range aspose.cells** e ainda ver uma tabela dinâmica funcional na nova planilha.

## Etapa 6: Salvar a pasta de trabalho com a nova planilha

Por fim, grave o workbook modificado no disco:

```java
        // Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

*Resultado*: `output.xlsx` agora contém a planilha original mais uma nova planilha chamada **Copy** que possui exatamente o mesmo intervalo, incluindo a tabela dinâmica.

## Exemplo completo em funcionamento

Juntando todas as peças, aqui está o programa completo e executável:

```java
import com.aspose.cells.*;
import java.io.IOException;

public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table and define the source range
        Worksheet sourceSheet = workbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");

        // Step 3: Create a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
        Range destinationRange = destinationSheet.getCells().createRange("A1");

        // Step 4: Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);

        // Step 5: Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Saída esperada**: Abra `output.xlsx` no Excel. Você verá uma planilha chamada **Copy** cujas células A1:D20 contêm os mesmos dados, formatação e uma tabela dinâmica ativa idêntica à original.

## Perguntas comuns e casos de borda

- **E se o intervalo de origem contiver células mescladas?**  
  O método `copy` também copia as informações de mesclagem, de modo que as células mescladas permanecem inalteradas na planilha de destino.

- **Posso copiar para um workbook diferente?**  
  Sim. Carregue uma segunda instância de `Workbook`, crie um intervalo de destino nesse workbook e chame `sourceRange.copy(destinationRange)`. O método lida com a cópia entre workbooks automaticamente.

- **E se a planilha de destino já contiver dados?**  
  A operação de cópia sobrescreve quaisquer células existentes que intersectem o intervalo de destino. Para evitar perda de dados, garanta que a área de destino esteja vazia ou use uma célula inicial diferente (por exemplo, `"B2"`).

- **O cache da tabela dinâmica é duplicado?**  
  O Aspose.Cells reutiliza o cache original, o que significa que a nova tabela dinâmica permanece vinculada aos mesmos dados de origem. Se precisar de um cache independente, será necessário recriar a tabela dinâmica após a cópia.

## Dicas e boas práticas

- **Dica profissional**: Use `Workbook.setForceFormulaRecalculation(true)` antes de salvar se seu intervalo contiver fórmulas que dependam de dados fora do bloco copiado.
- **Cuidado com** intervalos grandes: copiar planilhas massivas pode consumir muita memória. Considere copiar em blocos menores se encontrar `OutOfMemoryError`.
- **Dica de desempenho**: Desative a atualização de tela (`workbook.getSettings().setCalculateFormulaOnOpen(false)`) ao trabalhar com arquivos muito grandes para acelerar o processo de cópia.

## Conclusão

Agora você sabe como **criar nova planilha** e **copiar intervalo do Excel** entre planilhas usando Aspose.Cells, preservando tabelas dinâmicas e todos os atributos das células. Essa técnica permite duplicar blocos de dados programaticamente, criar modelos de relatórios ou reestruturar workbooks sem copiar‑colar manualmente.

Em seguida, explore tópicos relacionados como **copy range aspose.cells** para operações entre workbooks, automação de atualização de tabelas dinâmicas ou exportação da planilha copiada para PDF. Experimente diferentes intervalos de origem e nomes de planilhas para adequar à sua situação de automação específica. Boa codificação!


## O que você deve aprender a seguir?


Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Copy Shapes Between Excel Sheets Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/images-shapes/copy-shapes-between-sheets-aspose-cells-dotnet/)
- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}