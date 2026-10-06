---
category: general
date: 2026-06-08
description: Como usar reduce no Excel com Java usando Aspose.Cells. Aprenda fórmula
  lambda no Excel, arrays dinâmicos em Java, como escrever lambda e somar com reduce
  em um tutorial claro passo a passo.
draft: false
keywords:
- how to use reduce
- lambda formula excel
- dynamic arrays java
- how to write lambda
- sum with reduce
language: pt
og_description: Como usar reduce no Excel com Java. Domine a fórmula lambda no Excel,
  arrays dinâmicos em Java e soma com reduce usando um exemplo completo e executável.
og_title: Como usar Reduce no Excel com Java – Guia de Fórmula Lambda
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to use reduce in Excel with Java using Aspose.Cells. Learn lambda
    formula Excel, dynamic arrays java, how to write lambda, and sum with reduce in
    a clear step‑by‑step tutorial.
  headline: How to Use Reduce in Excel with Java – Lambda Formula Guide
  type: TechArticle
- description: How to use reduce in Excel with Java using Aspose.Cells. Learn lambda
    formula Excel, dynamic arrays java, how to write lambda, and sum with reduce in
    a clear step‑by‑step tutorial.
  name: How to Use Reduce in Excel with Java – Lambda Formula Guide
  steps:
  - name: What if I need a horizontal array instead of vertical?
    text: 'Swap the column/row arguments in `EXPAND`. For a horizontal spill across
      B1:F1:'
  - name: Can I use REDUCE to multiply instead of sum?
    text: 'Absolutely. Just change the lambda body:'
  - name: Does Aspose.Cells support custom LAMBDA functions?
    text: Yes, you can define named LAMBDA functions via the workbook’s `Names` collection,
      then call them like any built‑in formula. That’s a deeper dive for a later tutorial
      on **how to write lambda** functions that live beyond a single cell.
  - name: What about older Excel versions that don’t recognize REDUCE?
    text: If you target Excel 2019 or earlier, the engine will return `#NAME?`. In
      such cases
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
title: Como usar Reduce no Excel com Java – Guia de Fórmula Lambda
url: /pt/java/formulas-functions/how-to-use-reduce-in-excel-with-java-lambda-formula-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Usar Reduce no Excel com Java – Guia de Fórmula Lambda

Já se perguntou **como usar reduce** no Excel ao escrever código Java? Você não está sozinho. Muitos desenvolvedores se deparam com dificuldades ao tentar combinar as novas funções de array dinâmico do Excel com automação baseada em Java, e a resposta não é tão enigmática quanto parece à primeira vista.

Neste tutorial, vamos percorrer um exemplo concreto que mostra **como usar reduce** junto com uma expressão **lambda formula Excel**, tudo impulsionado pela biblioteca Aspose.Cells for Java. Ao final, você será capaz de gerar arrays dinâmicos em Java, escrever funções lambda e calcular uma **soma com reduce** — sem precisar mexer manualmente nas planilhas.

---

## O Que Você Vai Construir

- Uma nova pasta de trabalho criada inteiramente a partir de Java.  
- Um array dinâmico **EXPAND** que preenche as células A1:A5 com os números 1‑5.  
- Uma fórmula **REDUCE** que soma esses números usando uma **lambda formula Excel**.  
- Um arquivo `.xlsx` salvo que você pode abrir em qualquer programa de planilha para verificar o resultado.

Sem macros externas, sem VBA — apenas código Java puro e as funções modernas do Excel.

---

## Pré‑requisitos

- Java 17 (ou qualquer JDK recente) – versões mais antigas funcionam, mas você perderá o açúcar sintático do `var`.  
- Aspose.Cells for Java (a versão de avaliação gratuita funciona bem para esta demonstração).  
- Familiaridade básica com a sintaxe Java e fórmulas do Excel.  

Se você é novo em **dynamic arrays java**, não se preocupe — este guia explica cada parte.

---

## Etapa 1: Configurar Seu Projeto e Importar Aspose.Cells

Primeiro de tudo, adicione a dependência Maven do Aspose.Cells ao seu `pom.xml` (ou obtenha o JAR manualmente).

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- latest as of June 2026 -->
</dependency>
```

> **Dica profissional:** Mantenha suas dependências atualizadas; versões mais recentes melhoram a velocidade de avaliação de fórmulas, o que importa quando você está **como usar reduce** em planilhas grandes.

---

## Etapa 2: Criar uma Pasta de Trabalho e Acessar a Primeira Planilha

Agora vamos criar uma pasta de trabalho novinha em folha. Esta é a base para aprender **como usar reduce**, pois o objeto workbook nos fornece um sandbox para inserir fórmulas.

```java
// Step 2: Initialize a new workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet by default
```

*Por que isso importa:* A classe `Workbook` abstrai todo o arquivo Excel, enquanto `Worksheet` representa uma única aba. Mais adiante, você verá como **dynamic arrays java** podem preencher muitas células a partir de uma única fórmula colocada em A1.

---

## Etapa 3: Gerar um Array Vertical com EXPAND

A função `EXPAND` do Excel pode derramar valores em um intervalo. Usaremos ela para criar os números 1 até 5 na coluna A.

```java
// Step 3: Write an EXPAND formula to produce 1‑5 vertically
Cell expandCell = worksheet.getCells().get("A1");
expandCell.setFormula("=EXPAND({1},5,1)"); // {1} is the seed, 5 rows, 1 column
expandCell.calculate(); // forces the engine to evaluate the formula now
```

Se você abrir a pasta de trabalho resultante, as células A1:A5 exibirão 1, 2, 3, 4, 5. Esta é a parte de **dynamic arrays java** — uma fórmula popula todo um intervalo.

---

## Etapa 4: Escrever uma Lambda REDUCE para Somar o Array

Aqui é onde respondemos à pergunta central: **como usar reduce** no Excel a partir de Java. A função `REDUCE` itera sobre um array, aplicando uma lambda que você fornece. No nosso caso, vamos somar os números.

```java
// Step 4: Use REDUCE with a LAMBDA to compute the sum of A1:A5
Cell reduceCell = worksheet.getCells().get("B1");
reduceCell.setFormula(
    "=REDUCE(0, A1:A5, LAMBDA(acc, x, acc + x))"
);
reduceCell.calculate(); // forces evaluation immediately
```

Vamos detalhar:

- `0` – o valor inicial do acumulador (`acc`).  
- `A1:A5` – o array que geramos com **EXPAND**.  
- `LAMBDA(acc, x, acc + x)` – a **lambda formula Excel** que adiciona cada elemento (`x`) ao acumulador (`acc`).  

Quando a fórmula é executada, `B1` passa a conter **15**, a **soma com reduce** dos números 1‑5.

> **Como escrever lambda** no Excel? Pense nisso como uma função anônima onde os primeiros argumentos são os parâmetros, e a expressão final é o valor de retorno. Em Java, apenas incorporamos o texto; o motor do Excel faz o trabalho pesado.

---

## Etapa 5: Salvar a Pasta de Trabalho

Por fim, persistimos a pasta de trabalho no disco para que você possa abri‑la no Excel, Google Sheets ou qualquer visualizador que suporte `.xlsx`.

```java
// Step 5: Persist the workbook
String outputPath = "YOUR_DIRECTORY/new-functions.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Abra o arquivo e você verá:

| A | B |
|---|---|
| 1 | 15 |
| 2 |   |
| 3 |   |
| 4 |   |
| 5 |   |

A **soma com reduce** aparece em B1, confirmando que demonstramos com sucesso **como usar reduce** junto com uma **lambda formula Excel** a partir de Java.

---

## Exemplo Completo Funcionando

Abaixo está o programa Java completo, pronto para ser executado. Copie‑e cole no seu IDE, ajuste o diretório de saída e pressione **Run**.

```java
import com.aspose.cells.*;

public class ReduceLambdaDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create workbook & get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 2️⃣ EXPAND – generate vertical array 1‑5 in A1:A5
        Cell expandCell = worksheet.getCells().get("A1");
        expandCell.setFormula("=EXPAND({1},5,1)");
        expandCell.calculate(); // evaluate now

        // 3️⃣ REDUCE – sum the values using a lambda
        Cell reduceCell = worksheet.getCells().get("B1");
        reduceCell.setFormula("=REDUCE(0, A1:A5, LAMBDA(acc, x, acc + x))");
        reduceCell.calculate(); // evaluate now

        // 4️⃣ Save the workbook
        String outPath = "new-functions.xlsx";
        workbook.save(outPath);
        System.out.println("Workbook created at: " + outPath);
    }
}
```

**Saída esperada** ao abrir `new-functions.xlsx`:

- As células **A1:A5** contêm `1, 2, 3, 4, 5`.  
- A célula **B1** exibe `15`, confirmando a **soma com reduce**.

---

## Perguntas Frequentes & Casos de Borda

### E se eu precisar de um array horizontal em vez de vertical?

Troque os argumentos de coluna/linha em `EXPAND`. Para um derramamento horizontal de B1:F1:

```java
expandCell.setFormula("=EXPAND({1},1,5)");
```

### Posso usar REDUCE para multiplicar em vez de somar?

Com certeza. Basta mudar o corpo da lambda:

```java
reduceCell.setFormula("=REDUCE(1, A1:A5, LAMBDA(acc, x, acc * x))");
```

Agora B1 mostrará `120` (5 ! = 120).

### O Aspose.Cells suporta funções LAMBDA personalizadas?

Sim, você pode definir funções LAMBDA nomeadas via a coleção `Names` da pasta de trabalho, e então chamá‑las como qualquer fórmula incorporada. Isso é um mergulho mais profundo para um tutorial futuro sobre **como escrever lambda** que vivem além de uma única célula.

### E quanto às versões mais antigas do Excel que não reconhecem REDUCE?

Se você direcionar o Excel 2019 ou anterior, o motor retornará `#NAME?`. Nesses casos


## O Que Você Deve Aprender a Seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Mastering Aspose.Cells Java: How to Interrupt Formula Calculation in Excel Workbooks](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
- [How to Convert Excel Cell Names to Indices Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}