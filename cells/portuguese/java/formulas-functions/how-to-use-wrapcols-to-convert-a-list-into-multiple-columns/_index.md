---
category: general
date: 2026-10-16
description: como usar wrapcols em Java e converter rapidamente uma lista em colunas
  com uma fórmula – aprenda como definir a fórmula para um layout de múltiplas colunas
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- convert list to columns
- how to set formula
- create multi‑column layout
language: pt
lastmod: 2026-10-16
og_description: como usar wrapcols para converter uma lista em colunas no Java. siga
  este guia completo para definir a fórmula e criar um layout de múltiplas colunas
  no Excel.
og_image_alt: Screenshot of an Excel sheet showing a wrapped list in three columns
og_title: Como usar wrapcols – guia passo a passo para desenvolvedores Java
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: how to use wrapcols in Java and quickly convert list to columns with
    a formula – learn how to set formula for a multi‑column layout
  headline: How to use wrapcols to convert a list into multiple columns in Java
  type: TechArticle
- description: how to use wrapcols in Java and quickly convert list to columns with
    a formula – learn how to set formula for a multi‑column layout
  name: How to use wrapcols to convert a list into multiple columns in Java
  steps:
  - name: What happens behind the scenes
    text: 'When the workbook is saved, Aspose.Cells evaluates the formula and writes
      the expanded values to the file. If you open `WrapColsResult.xlsx` in Excel,
      you’ll see:'
  - name: Changing the number of columns
    text: If you need a different column count, modify the second argument of `WRAPCOLS`.
      For example, `=WRAPCOLS(A2:A100,5)` creates five columns. The function automatically
      adjusts the row count to accommodate the new layout.
  - name: Handling a non‑even list size
    text: When the source range length isn’t divisible by the column count, `WRAPCOLS`
      pads the final column with blanks. This behavior is useful for creating balanced
      tables without manual trimming.
  - name: Using a dynamic range
    text: You can replace `A2:A100` with a named range or a formula that calculates
      the last row, such as `A2:INDEX(A:A, COUNTA(A:A))`. This makes the solution
      robust when the list length changes.
  - name: Avoiding circular references
    text: Place the formula in a cell that isn’t part of the source range. If you
      accidentally set the formula inside `A2:A100`, Excel will report a circular
      reference error. Always write the formula to a separate cell (commonly `A1`).
  type: HowTo
tags:
- wrapcols
- Aspose.Cells
- Java
- Excel automation
title: Como usar wrapcols para converter uma lista em várias colunas em Java
url: /pt/java/formulas-functions/how-to-use-wrapcols-to-convert-a-list-into-multiple-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar wrapcols para converter uma lista em várias colunas em Java

Se você precisa **como usar wrapcols** em um projeto Java, este guia mostra os passos exatos. Você aprenderá como definir a fórmula, converter uma lista em colunas e criar um layout de múltiplas colunas sem copiar‑colar manualmente.

O tutorial cobre tudo, desde a configuração do projeto até o tratamento de casos extremos, para que você possa aplicar a solução a qualquer planilha que contenha uma lista de coluna única. Nenhuma ferramenta adicional é necessária além do Aspose.Cells for Java.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

* Java 17 ou superior instalado  
* Maven 3.8+ (ou Gradle) para gerenciamento de dependências  
* Uma licença para **Aspose.Cells for Java** – a avaliação gratuita funciona para testes  
* Familiaridade básica com fórmulas do Excel  

Esses itens garantem que o código seja compilado sem erros.

## Etapa 1: Adicionar Aspose.Cells ao seu projeto

Adicione a dependência Maven a seguir em `pom.xml`. Se você usar Gradle, as mesmas coordenadas se aplicam.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

A biblioteca fornece as classes `Cell` e `Worksheet` usadas mais adiante quando você **como definir fórmula** para um intervalo.

## Etapa 2: Criar uma pasta de trabalho e preencher a lista de origem

A primeira tarefa é gerar uma pasta de trabalho que contenha uma lista vertical (A2:A100). Essa lista representa os dados que você deseja **converter lista em colunas**.

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // Populate A2:A100 with sample data
        for (int i = 0; i < 99; i++) {
            cells.get("A" + (i + 2)).setValue("Item " + (i + 1));
        }

        // Apply WRAPCOLS formula (see next step)
        applyWrapCols(cells);

        // Save the result
        workbook.save("WrapColsResult.xlsx");
    }
```

O loop preenche a primeira coluna com 99 itens, fornecendo uma lista realista para trabalhar. Você pode substituir os valores gerados por dados lidos de um banco de dados ou outra fonte.

## Etapa 3: Como usar wrapcols para definir a fórmula

Agora você verá o núcleo do tutorial: usar a função `WRAPCOLS` para **criar layout de múltiplas colunas**. A função recebe dois argumentos – o intervalo de origem e o número de colunas desejado.

```java
    private static void applyWrapCols(Cells cells) {
        // Step 1: Get the cell where the formula will be placed (A1)
        Cell target = cells.get("A1");

        // Step 2: Apply the WRAPCOLS function to wrap A2:A100 into 3 columns
        target.setFormula("=WRAPCOLS(A2:A100,3)");
    }
}
```

*Por que isso funciona* – `WRAPCOLS` lê o intervalo vertical `A2:A100` e distribui os valores linha a linha em três colunas (B, C e D). O resultado aparece a partir da célula que contém a fórmula (`A1`). Como a fórmula retorna um array, o Aspose.Cells expande automaticamente o resultado nas células necessárias.

### O que acontece nos bastidores

Quando a pasta de trabalho é salva, o Aspose.Cells avalia a fórmula e grava os valores expandidos no arquivo. Se você abrir `WrapColsResult.xlsx` no Excel, verá:

| A1 | B1 | C1 | D1 |
|----|----|----|----|
| Item 1 | Item 34 | Item 67 |
| Item 2 | Item 35 | Item 68 |
| … | … | … |

O layout demonstra um padrão de **criar layout de múltiplas colunas** útil para relatórios, dashboards ou formulários imprimíveis.

## Etapa 4: Verificar a saída programaticamente (opcional)

Se quiser confirmar que a fórmula produziu a matriz esperada sem abrir o Excel, você pode ler os valores após o cálculo.

```java
        // Force calculation to ensure the array result is materialized
        workbook.calculateFormula();

        // Print the first three rows of the wrapped layout
        for (int row = 0; row < 3; row++) {
            StringBuilder line = new StringBuilder();
            for (int col = 0; col < 4; col++) { // A‑D columns
                line.append(cells.get(row, col).getStringValue()).append("\t");
            }
            System.out.println(line.toString().trim());
        }
```

Executar o programa imprime algo como:

```
Item 1    Item 34    Item 67    Item 100
Item 2    Item 35    Item 68    Item 101
Item 3    Item 36    Item 69    Item 102
```

Isso confirma que **como usar wrapcols** funciona como esperado e que a operação **converter lista em colunas** foi bem‑sucedida.

## Etapa 5: Variações comuns e casos de borda

### Alterando o número de colunas

Se precisar de uma contagem de colunas diferente, modifique o segundo argumento de `WRAPCOLS`. Por exemplo, `=WRAPCOLS(A2:A100,5)` cria cinco colunas. A função ajusta automaticamente a contagem de linhas para acomodar o novo layout.

### Lidando com um tamanho de lista não uniforme

Quando o comprimento do intervalo de origem não é divisível pelo número de colunas, `WRAPCOLS` preenche a coluna final com células vazias. Esse comportamento é útil para criar tabelas balanceadas sem cortes manuais.

### Usando um intervalo dinâmico

Você pode substituir `A2:A100` por um intervalo nomeado ou uma fórmula que calcule a última linha, como `A2:INDEX(A:A, COUNTA(A:A))`. Isso torna a solução robusta quando o tamanho da lista varia.

### Evitando referências circulares

Coloque a fórmula em uma célula que não faça parte do intervalo de origem. Se você definir a fórmula acidentalmente dentro de `A2:A100`, o Excel exibirá um erro de referência circular. Sempre escreva a fórmula em uma célula separada (geralmente `A1`).

## Etapa 6: Dicas para uso em produção

* **Cache da pasta de trabalho** – Se você gerar muitos relatórios em um loop, reutilize uma única instância de `Workbook` e limpe os dados anteriores para reduzir o consumo de memória.  
* **Definir modo de cálculo** – Use `workbook.getSettings().setCalculateFormulaOnOpen(false)` quando precisar apenas da fórmula bruta sem avaliação imediata.  
* **Internacionalização** – O nome da função `WRAPCOLS` é independente de localidade, mas os separadores decimais em outras fórmulas podem variar. Mantenha as fórmulas em inglês para evitar incompatibilidades.  
* **Desempenho** – Para listas com mais de 10 000 linhas, avalie a fórmula uma única vez e depois leia os valores do array diretamente, evitando cálculos repetidos.

## Conclusão

Agora você sabe **como usar wrapcols** em Java para **converter lista em colunas** e **criar layout de múltiplas colunas** com uma única fórmula. O exemplo completo e executável demonstra todo o fluxo de trabalho: adicionar a biblioteca, preencher os dados, aplicar a fórmula e verificar o resultado.  

A partir daqui você pode:

* Ajustar a contagem de colunas para se adequar ao seu estilo de relatório  
* Combinar `WRAPCOLS` com outras funções como `SORT` ou `FILTER` para modelagem avançada de dados  
* Exportar a pasta de trabalho para PDF, CSV ou HTML usando os conversores integrados do Aspose.Cells  

Experimente essas variações para otimizar suas tarefas de automação do Excel. Se encontrar algum problema, revise a seção de tratamento de casos de borda acima ou consulte a documentação do Aspose.Cells para suporte adicional a fórmulas. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [How to Use WRAPCOLS in Java – Complete Guide to Excel Array Formulas](/cells/english/java/integration-interoperability/how-to-use-wrapcols-in-java-complete-guide-to-excel-array-fo/)
- [How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example](/cells/english/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/)
- [How to Use Reduce in Excel with Java – Lambda Formula Guide](/cells/english/java/formulas-functions/how-to-use-reduce-in-excel-with-java-lambda-formula-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}