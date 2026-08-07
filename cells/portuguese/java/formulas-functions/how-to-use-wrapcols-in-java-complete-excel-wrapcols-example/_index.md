---
category: general
date: 2026-06-21
description: Como usar WRAPCOLS com Aspose.Cells Java para converter array em linhas,
  escrever fórmula em célula e preencher células com fórmula – guia passo a passo.
draft: false
keywords:
- how to use wrapcols
- convert array to rows
- write formula to cell
- excel wrapcols example
- populate cells with formula
language: pt
og_description: Como usar WRAPCOLS em Java com Aspose.Cells para converter um array
  em linhas, escrever uma fórmula em uma célula e preencher células com fórmula —
  tudo em um único guia.
og_title: Como usar WRAPCOLS em Java – Exemplo completo de WRAPCOLS no Excel
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: How to use WRAPCOLS with Aspose.Cells Java to convert array to rows,
    write formula to cell, and populate cells with formula – step‑by‑step guide.
  headline: How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example
  type: TechArticle
- description: How to use WRAPCOLS with Aspose.Cells Java to convert array to rows,
    write formula to cell, and populate cells with formula – step‑by‑step guide.
  name: How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example
  steps:
  - name: What the Formula Does
    text: '- `{1,2,3}` – a literal array containing three numbers. - `2` – the number
      of columns per row. - Result: - **A1** = 1, **B1** = 2 - **A2** = 3, **B2**
      = (blank)'
  - name: 1. Empty Arrays
    text: 'If the array literal is empty (`{}`), `WRAPCOLS` returns a `#VALUE!` error.
      To avoid breaking your sheet, guard the formula generation:'
  - name: 2. Non‑Numeric Data
    text: '`WRAPCOLS` works with text as well. For example, `WRAPCOLS({"A","B","C","D"},2)`
      produces a two‑column layout of strings. Just remember to quote strings inside
      the array literal.'
  - name: 3. Compatibility
    text: The `WRAPCOLS` function is available in Excel 365 and Excel 2019+ (Office
      2019, Excel for the web). If you need to support older versions, you’ll have
      to fall back to manual looping or use a different spill‑compatible function.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel formulas
- WRAPCOLS
title: Como usar WRAPCOLS em Java – Exemplo completo de WRAPCOLS no Excel
url: /pt/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar WRAPCOLS em Java – Exemplo completo de Excel WRAPCOLS

Já se perguntou **como usar WRAPCOLS** quando precisa transformar um array simples em uma tabela organizada no Excel? Você não está sozinho. Muitos desenvolvedores ficam presos ao verem a função `WRAPCOLS` pela primeira vez e pensam: “Como eu realmente escrevo essa fórmula em uma célula a partir do Java?” A boa notícia? É bastante simples depois que você conhece os passos corretos.

Neste tutorial vamos percorrer um exemplo totalmente executável de Aspose.Cells para Java que **converte um array em linhas**, grava a fórmula diretamente em uma célula e mostra como **preencher células com fórmula** em cenários reais. Ao final, você terá uma visão clara do **exemplo de excel wrapcols** e estará pronto para adaptá‑lo aos seus próprios projetos.

## Pré‑requisitos

Antes de mergulharmos, certifique‑se de que você tem:

- Java 17 ou superior (o código funciona com qualquer JDK recente).
- Biblioteca Aspose.Cells for Java (você pode obter o JAR mais recente no Maven Central).
- Noções básicas de sintaxe Java e fórmulas do Excel.
- Uma IDE ou editor de texto simples — nenhuma ferramenta especial é necessária.

Tudo pronto? Ótimo, vamos começar.

## Etapa 1: Configurar o projeto e carregar uma pasta de trabalho

Primeiro de tudo — crie um novo projeto Maven (ou Gradle) e adicione a dependência Aspose.Cells:

```xml
<!-- pom.xml snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

Agora podemos carregar uma pasta de trabalho existente (ou criar uma nova) e obter a primeira planilha:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook (or create a new one)
        Workbook wb = new Workbook();               // creates a blank workbook
        // Alternatively, load an existing file:
        // Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Access the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);
```

> **Por que carregamos uma pasta de trabalho** – Aspose.Cells trabalha com uma representação em memória de um arquivo Excel. Ao carregar (ou criar) uma pasta de trabalho, ganhamos acesso a células, linhas e fórmulas, o que é essencial para qualquer operação de **escrever fórmula em célula**.

## Etapa 2: Inserir a fórmula WRAPCOLS em uma célula

O coração do tutorial está na função `WRAPCOLS`. Ela recebe um array unidimensional e “envolve”‑o em um número especificado de colunas, espalhando automaticamente o restante em novas linhas. Aqui está a sintaxe que usaremos:

```java
// Step 3: Set a formula that wraps a collection into rows of 2 columns
// The formula WRAPCOLS({1,2,3},2) will produce:
//   Row 1: 1, 2
//   Row 2: 3
ws.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3},2)");
```

Observe como a fórmula é uma string simples passada para `setFormula`. Aspose.Cells faz o trabalho pesado — analisa a fórmula, avalia‑a e espalha os resultados na planilha. Esta é a maneira mais direta de **preencher células com fórmula** sem iterar manualmente sobre linhas e colunas.

### O que a fórmula faz

- `{1,2,3}` – um array literal contendo três números.
- `2` – o número de colunas por linha.
- Resultado:
  - **A1** = 1, **B1** = 2
  - **A2** = 3, **B2** = (vazio)

Se você quiser três colunas em vez disso, basta mudar o segundo argumento para `3`, e o array preencherá uma única linha.

## Etapa 3: Salvar a pasta de trabalho e verificar o resultado

Agora que a fórmula está em **A1**, vamos persistir a pasta de trabalho no disco para que você possa abri‑la no Excel e ver o spill:

```java
        // (Optional) Save the workbook to see the result
        wb.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Abra `output.xlsx` e você verá exatamente o que o comentário descreveu — duas colunas na primeira linha e o valor restante na segunda linha. Essa é a essência do **exemplo de excel wrapcols**.

## Etapa 4: Expandindo o exemplo – Convertendo arrays maiores

Projetos reais raramente trabalham com apenas três números. Suponha que você tenha uma coleção maior, por exemplo `{10,20,30,40,50,60,70}` e queira três colunas por linha. Veja como ajustar o código:

```java
String largeArray = "{10,20,30,40,50,60,70}";
int columnsPerRow = 3;
String formula = String.format("=WRAPCOLS(%s,%d)", largeArray, columnsPerRow);
ws.getCells().get("C5").setFormula(formula);
```

Agora o spill começa em **C5**, produzindo:

| C5 | D5 | E5 |
|----|----|----|
|10  |20  |30  |
|40  |50  |60  |
|70  |    |    |

Isso demonstra como você pode **converter array em linhas** dinamicamente, simplesmente ajustando a string da fórmula. Sem loops, sem atribuições manuais de células — Aspose.Cells cuida do resto.

## Etapa 5: Tratando casos de borda e armadilhas comuns

### 1. Arrays vazios

Se o literal do array estiver vazio (`{}`), `WRAPCOLS` retorna um erro `#VALUE!`. Para evitar quebrar sua planilha, proteja a geração da fórmula:

```java
if (arrayContent.isEmpty()) {
    ws.getCells().get("F1").setValue("No data");
} else {
    ws.getCells().get("F1").setFormula(formula);
}
```

### 2. Dados não numéricos

`WRAPCOLS` funciona também com texto. Por exemplo, `WRAPCOLS({"A","B","C","D"},2)` produz um layout de duas colunas com strings. Apenas lembre‑se de colocar aspas nas strings dentro do literal do array.

### 3. Compatibilidade

A função `WRAPCOLS` está disponível no Excel 365 e no Excel 2019+ (Office 2019, Excel para a web). Se precisar dar suporte a versões mais antigas, será necessário recorrer a loops manuais ou usar outra função compatível com spill.

## Etapa 6: Dicas práticas e truques avançados

- **Dica de especialista:** Use `Cell.setFormulaLocal` se precisar de um separador específico de localidade (vírgula vs ponto‑e‑vírgula) dependendo das configurações regionais do usuário.
- **Cuidado com:** Sobrescrever dados existentes. A área de spill substituirá qualquer conteúdo que já exista no intervalo de destino.
- **Nota de desempenho:** Definir uma fórmula é barato; o trabalho pesado ocorre ao **salvar** ou **recalcular** a pasta de trabalho. Se você estiver gerando milhares de fórmulas, considere desativar o cálculo automático (`wb.calculateFormula()` posteriormente) para acelerar o processamento.

## Exemplo completo em funcionamento

Abaixo está a classe Java completa, pronta para ser executada, que incorpora tudo o que discutimos:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook
        Workbook wb = new Workbook();

        // 2️⃣ Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // 3️⃣ Simple WRAPCOLS formula – basic excel wrapcols example
        ws.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3},2)");

        // 4️⃣ Larger array with three columns per row
        String largeArray = "{10,20,30,40,50,60,70}";
        int cols = 3;
        String largeFormula = String.format("=WRAPCOLS(%s,%d)", largeArray, cols);
        ws.getCells().get("C5").setFormula(largeFormula);

        // 5️⃣ Text array demonstration
        ws.getCells().get("G1").setFormula("=WRAPCOLS({\"Apple\",\"Banana\",\"Cherry\",\"Date\"},2)");

        // 6️⃣ Save the result
        wb.save("output.xlsx");
    }
}
```

**Saída esperada:** Abra `output.xlsx` e você verá três regiões de spill distintas:

- **A1:B2** – números 1‑3 envolvidos em duas colunas.
- **C5:E7** – números 10‑70 envolvidos em três colunas.
- **G1:H2** – nomes de frutas envolvidos em duas colunas.

## Conclusão

Acabamos de cobrir **como usar WRAPCOLS** com Aspose.Cells para Java, mostrando como **converter array em linhas**, **escrever fórmula em célula** e **preencher células com fórmula** de forma limpa e reutilizável. A abordagem elimina loops tediosos, aproveita o comportamento nativo de spill do Excel e mantém seu código conciso.

Pronto para o próximo desafio? Experimente combinar `WRAPCOLS` com fontes de dados dinâmicas — talvez extraindo valores de um banco de dados, construindo a string do array em tempo real e deixando o Excel fazer o layout. Você também pode experimentar outras funções de spill como `SEQUENCE` ou `FILTER` para criar relatórios ainda mais ricos.

Se encontrar algum problema, deixe um comentário abaixo ou explore a documentação extensa da Aspose. Boa codificação e aproveite o poder das fórmulas modernas do Excel direto do Java!

![how to use wrapcols example](/images/wrapcols-demo.png "how to use wrapcols in Java – screenshot of spilled data")


## O que você deve aprender a seguir?


Os tutoriais a seguir abordam tópicos estreitamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [How to Select Cell Ranges in Excel Using Aspose.Cells for Java (2023 Guide)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)
- [How to Set an Active Cell in Excel Using Aspose.Cells for Java: A Complete Guide](/cells/english/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [How to Insert Rows into Excel Workbooks Using Aspose.Cells for Java](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}