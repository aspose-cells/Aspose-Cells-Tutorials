---
category: general
date: 2026-06-30
description: Ordene valores únicos no Excel usando Java. Aprenda como definir fórmulas,
  recalcular fórmulas e gerar lista única no Excel com Aspose.Cells.
draft: false
keywords:
- sort unique values excel
- how to set formula
- how to recalculate formulas
- generate unique list excel
- set array formula
language: pt
og_description: Ordene valores únicos no Excel com Java. Este guia mostra como definir
  fórmulas, recalcular fórmulas e gerar uma lista única no Excel em minutos.
og_title: Ordenar Valores Únicos no Excel – Tutorial Java para Fórmulas de Matriz
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  headline: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  type: TechArticle
- description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  name: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  steps:
  - name: How It Works
    text: '- `UNIQUE(B1:B10)` scans the range and returns a vertical array of distinct
      strings. - `SORT(...)` takes that array and orders it in ascending order. -
      Wrapping the whole thing in `=` and calling `setFormulaArray` tells Aspose.Cells
      to treat the result as a **spilled array**, just like Excel would.'
  - name: Empty Cells in the Source Range
    text: 'If `B1:B10` contains blanks, `UNIQUE` will treat them as a distinct entry.
      To ignore blanks, wrap the range with `FILTER`:'
  - name: Non‑Contiguous Data
    text: 'When your data lives in multiple columns, you can join them with `CHOOSE`
      or `TEXTJOIN` before applying `UNIQUE`. For example:'
  - name: ' ## What Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [How to Sort Excel Files by Cell Color Using Aspose.Cells Java&#58; A Comprehensive
      Guide](/cells/english/java/data-analysis/excel-file-sorting-aspose-cells-java/)
      - [Mastering Aspose.Cells Java&#58; How to Interrupt Formula Calculation in
      Excel Workbooks](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
      - [How to Create an Excel Data Validation List with Aspose.Cells for Java&#58;
      A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)

      {{< /blocks/products/pf/tutorial-page-section >}}'
    text: '{{< /blocks/products/pf/main-container >}} {{< /blocks/products/pf/main-wrap-class
      >}} {{< blocks/products/products-backtop-button >}}'
  type: HowTo
- questions:
  - answer: The `SORT` and `UNIQUE` functions are part of the Dynamic Array engine
      introduced in Excel 365. For legacy files you’d need to use classic array formulas
      like `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Aspose.Cells
      can still evaluate them, but the syntax is more verbose.
    question: Does this work with older Excel versions (pre‑Office 365)?
  - answer: Absolutely. Just change the address in `cells.get("A1")`. The spilled
      array will always start at the cell you specify and expand right‑and‑down as
      needed.
    question: Can I set the array formula on a range other than `A1`?
  - answer: 'Replace the static range with a dynamic one, e.g., `B:B` or a named range.
      The formula becomes `=SORT(UNIQUE(B:B))`. Be cautious with whole‑column references
      on very large sheets; they can impact performance. --- ## Conclusion We’ve just
      covered **how to set formula** in Java to **sort unique values'
    question: What if my source data is larger than `B1:B10`?
  type: FAQPage
tags:
- Excel automation
- Java
- Aspose.Cells
title: Ordenar Valores Únicos no Excel – Guia Completo de Java para Configurar Fórmulas
  de Matriz
url: /pt/java/formulas-functions/sort-unique-values-excel-complete-java-guide-to-set-array-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ordenar Valores Únicos no Excel – Guia Completo em Java para Definir Fórmulas de Matriz

Já se perguntou como **sort unique values Excel** sem arrastar fórmulas? Você não está sozinho. Em muitos cenários de relatórios, você precisa de uma lista limpa, ordenada alfabeticamente, de entradas distintas, e fazer isso manualmente é um incômodo.  

A boa notícia? Com algumas linhas de código Java você pode **set array formula** em uma planilha, então **recalculate formulas** para que o intervalo derramado se preencha automaticamente. Neste tutorial, percorreremos tudo — desde a criação de uma workbook até a geração de uma lista única no estilo Excel — para que você possa incorporar a solução diretamente em sua aplicação.

## O que este tutorial cobre

- Configurar um projeto Java com Aspose.Cells (a biblioteca que alimenta o trecho de código).  
- Usar as funções `SORT` e `UNIQUE` juntas para **generate unique list Excel** resultados.  
- Aplicar uma **array formula** a uma célula programaticamente.  
- Acionar uma passagem de cálculo para que a etapa **how to recalculate formulas** aconteça instantaneamente.  
- Verificar a saída e ajustar a solução para casos extremos, como células vazias ou intervalos não contíguos.

Ao final deste guia, você será capaz de inserir um método pronto‑para‑usar em qualquer serviço Java que precise exportar planilhas Excel limpas.

> **Dica profissional:** Se você já está usando Maven, adicionar Aspose.Cells como dependência evita que você precise lidar manualmente com arquivos JAR.

---

## Pré-requisitos

| Requisito | Por que é importante |
|-----------|----------------------|
| Java 8 ou superior | Aspose.Cells tem como alvo Java 8+. |
| Maven (ou Gradle) | Simplifica o gerenciamento de dependências. |
| Aspose.Cells for Java | Fornece as APIs `Workbook`, `Worksheet` e de fórmulas que usaremos. |
| Familiaridade básica com funções do Excel | Entender `SORT` e `UNIQUE` ajuda a adaptar o código. |

> *Se ainda não tem Aspose.Cells, adicione isso ao seu `pom.xml`*:

```xml
<!-- Aspose.Cells for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- latest as of June 2026 -->
</dependency>
```

---

## Etapa 1: Criar uma Nova Workbook (Como Definir Fórmula Começa Aqui)

Primeiro precisamos de uma workbook em branco. Pense nela como a tela vazia onde mais tarde **set array formula** na célula `A1`.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // The rest of the steps follow...
```

> *Por que criar uma nova workbook?*  
> Ela garante um ambiente limpo, evitando fórmulas ocultas que poderiam interferir nos nossos dados de teste.

---

## Etapa 2: Preencher Dados de Exemplo (Opcional, mas Útil)

Para ver o resultado claramente, vamos preencher a coluna **B** com algumas entradas duplicadas.

```java
        // Step 2: Get the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Sample data in B1:B10
        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }
```

> *Por que usar a coluna B?*  
> A fórmula que escreveremos referencia `B1:B10`, então manter os dados lá espelha o exemplo clássico do Excel.

---

## Etapa 3: Definir uma Fórmula de Matriz que **Sort Unique Values Excel**

Agora a mágica acontece. Combinamos `UNIQUE` (para remover duplicatas) com `SORT` (para ordená‑las alfabeticamente). A expressão resultante é uma **array formula**, o que significa que ela será derramada nas células adjacentes automaticamente.

```java
        // Step 3: Set an array formula that sorts the unique values from B1:B10
        // This is the core of “how to set formula” for our scenario.
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");
```

### Como funciona

- `UNIQUE(B1:B10)` varre o intervalo e retorna uma matriz vertical de strings distintas.  
- `SORT(...)` pega essa matriz e a ordena em ordem crescente.  
- Envolver tudo em `=` e chamar `setFormulaArray` indica ao Aspose.Cells que o resultado deve ser tratado como uma **spilled array**, assim como o Excel faria.

> **Nota:** Se você estiver usando uma versão mais antiga do Excel que não possui `SORT` ou `UNIQUE`, pode recorrer a `SORT(UNIQUE(...))` com a função **LET** ou usar fórmulas de matriz legadas (`=INDEX(...)`). O tutorial foca na abordagem moderna de matriz dinâmica porque é a maneira mais limpa de **generate unique list Excel** hoje.

---

## Etapa 4: Recalcular Fórmulas para que o Intervalo Derramado Seja Preenchido

Depois que a fórmula está no lugar, a workbook não a avalia automaticamente. É aqui que a etapa **how to recalculate formulas** entra.

```java
        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();
```

Chamar `calculateFormula()` força o Aspose.Cells a executar o motor do Excel, preenchendo as células `A1`, `A2`, … com os valores únicos ordenados.

> *Por que não confiar na avaliação preguiçosa?*  
> Em um contexto de servidor, você frequentemente precisa dos dados prontos para exportação (CSV, PDF, etc.) logo após o cálculo, então uma chamada explícita garante consistência.

---

## Etapa 5: Verificar o Resultado (Depuração Opcional)

É sempre uma boa ideia imprimir os valores derramados no console — especialmente quando você está aprendendo uma nova API.

```java
        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break; // stop at first empty cell
            System.out.println("- " + value);
            row++;
        }

        // Optionally, save the workbook to inspect in Excel
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

Executar o programa imprime:

```
Sorted unique list:
- Apple
- Banana
- Cherry
- Date
- Elderberry
- Fig
- Grape
```

Abra `SortedUniqueValues.xlsx` e você verá os mesmos dados derramando de `A1` para baixo.

---

## Lidando com Casos de Borda

### Células Vazias no Intervalo de Origem

Se `B1:B10` contiver vazios, `UNIQUE` os tratará como uma entrada distinta. Para ignorar vazios, envolva o intervalo com `FILTER`:

```java
cells.get("A1").setFormulaArray("=SORT(UNIQUE(FILTER(B1:B10, B1:B10<>\"\")))");
```

### Dados Não Contíguos

Quando seus dados estão em várias colunas, você pode juntá‑los com `CHOOSE` ou `TEXTJOIN` antes de aplicar `UNIQUE`. Por exemplo:

```java
cells.get("A1").setFormulaArray(
    "=SORT(UNIQUE(CHOOSE({1,2}, B1:B10, C1:C10)))"
);
```

Essas adaptações demonstram a flexibilidade de **how to set formula** para cenários mais complexos.

---

## Exemplo Completo em Funcionamento (Todas as Etapas Combinadas)

Abaixo está o programa Java completo e executável. Copie‑e‑cole no seu IDE, adicione a dependência Aspose.Cells e pressione *Run*.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // Step 2: Get the first worksheet and fill sample data
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }

        // Step 3: Set an array formula that sorts the unique values from B1:B10
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");

        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();

        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break;
            System.out.println("- " + value);
            row++;
        }

        // Save the workbook for visual verification
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

**Saída esperada** (mostrada no console) corresponde à lista ordenada e deduplicada que discutimos anteriormente. Abrir o arquivo Excel gerado revela os mesmos valores derramando de `A1` para baixo.

---

## Perguntas Frequentes

**Q: Isso funciona com versões mais antigas do Excel (pré‑Office 365)?**  
A: As funções `SORT` e `UNIQUE` fazem parte do mecanismo de Matriz Dinâmica introduzido no Excel 365. Para arquivos legados, você precisaria usar fórmulas de matriz clássicas como `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. O Aspose.Cells ainda pode avaliá‑las, mas a sintaxe é mais verbosa.

**Q: Posso definir a fórmula de matriz em um intervalo diferente de `A1`?**  
A: Absolutamente. Basta mudar o endereço em `cells.get("A1")`. A matriz derramada sempre começará na célula que você especificar e se expandirá para a direita e para baixo conforme necessário.

**Q: E se meus dados de origem forem maiores que `B1:B10`?**  
A: Substitua o intervalo estático por um dinâmico, por exemplo, `B:B` ou um intervalo nomeado. A fórmula torna‑se `=SORT(UNIQUE(B:B))`. Tenha cuidado com referências de coluna inteira em planilhas muito grandes; elas podem afetar o desempenho.

---

## Conclusão

Acabamos de cobrir **how to set formula** em Java para **sort unique values Excel**, como **recalculate formulas**, e como **generate unique list Excel** usando a poderosa API do Aspose.Cells. As etapas são simples: criar uma workbook, preencher dados, aplicar uma fórmula de matriz, acionar o cálculo e verificar o resultado.  

A partir daqui você pode expandir — adicionar formatação condicional, exportar para PDF, ou integrar o método em um serviço web que entrega relatórios prontos. A ideia central permanece a mesma: deixar as próprias funções do Excel fazerem o trabalho pesado e deixar o Java orquestrar o processo.

Pronto para elevar sua automação do Excel? Experimente substituir `SORT` por `SORTBY` para ordenar por uma coluna secundária, ou experimente `FILTER` para excluir linhas que não atendam às regras de negócio. As possibilidades são praticamente infinitas.

###

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}