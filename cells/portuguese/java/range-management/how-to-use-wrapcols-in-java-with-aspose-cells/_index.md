---
category: general
date: 2026-11-22
description: Aprenda como usar wrapcols em Java para converter um intervalo em colunas
  usando Aspose.Cells. Este guia percorre a função wrap columns do Excel passo a passo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- convert range to columns
- wrap columns excel function
language: pt
lastmod: 2026-11-22
og_description: Como usar wrapcols em Java para converter um intervalo em colunas.
  Siga este tutorial para dominar a função wrap columns do Excel com Aspose.Cells.
og_image_alt: Screenshot showing how to use wrapcols formula in Excel
og_title: Como usar wrapcols em Java – guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to use wrapcols in Java to convert a range to columns using
    Aspose.Cells. This guide walks through the wrap columns excel function step by
    step.
  headline: How to use wrapcols in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to use wrapcols in Java to convert a range to columns using
    Aspose.Cells. This guide walks through the wrap columns excel function step by
    step.
  name: How to use wrapcols in Java with Aspose.Cells
  steps:
  - name: Load the workbook
    text: '```java import com.aspose.cells.*;'
  - name: Access the first worksheet
    text: '```java // Step 2: Access the first worksheet Worksheet worksheet = workbook.getWorksheets().get(0);
      ```'
  - name: Set the WRAPCOLS formula
    text: '```java // Step 3: Set the WRAPCOLS formula in cell A1 worksheet.getCells().get("A1").setFormula("=WRAPCOLS(A1:A10,
      3)"); ```'
  - name: Save the workbook
    text: '```java // Step 4: Save the workbook with the formula applied workbook.save("YOUR_DIRECTORY/output.xlsx");
      } } ```'
  - name: Expected output
    text: 'When you open `output.xlsx`, cells `A1:C4` (or however many rows are needed)
      will contain the original list from `A1:A10` spread across three columns. The
      layout looks like this:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel automation
title: Como usar wrapcols em Java com Aspose.Cells
url: /pt/java/range-management/how-to-use-wrapcols-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar wrapcols em Java com Aspose.Cells

Se você precisa **how to use wrapcols** para remodelar dados em uma pasta de trabalho do Excel, este tutorial mostra o processo completo. Você verá como a fórmula WRAPCOLS transforma um intervalo vertical em um conjunto de colunas, facilitando a apresentação de listas lado a lado.

O guia cobre tudo o que você precisa: carregar uma pasta de trabalho, aplicar a fórmula WRAPCOLS e salvar o resultado. Nenhuma referência externa é necessária, então você pode copiar o código e executá‑lo imediatamente. Ao longo do caminho também explicamos a *wrap columns excel function* e demonstramos como **convert range to columns** para cenários de relatório comuns.

## O que você precisará

- Java 17 ou superior  
- Aspose.Cells for Java (versão mais recente)  
- Uma IDE Java (IntelliJ IDEA, Eclipse ou VS Code)  
- Um arquivo Excel de entrada (`input.xlsx`) contendo dados na coluna A  

## Como usar wrapcols em Java com Aspose.Cells

Os quatro passos a seguir implementam o fluxo de trabalho **how to use wrapcols**. Cada passo inclui um trecho de código, uma explicação do porquê ele é importante e uma dica para evitar armadilhas comuns.

### Etapa 1: Carregar a pasta de trabalho

```java
import com.aspose.cells.*;

public class WrapColsExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load a workbook (or create a new one)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Por que este passo é importante*: `Workbook` é o ponto de entrada para todas as operações do Excel no Aspose.Cells. Carregar o arquivo lhe dá acesso às planilhas, células e fórmulas.  

**Dica profissional**: Use um caminho absoluto durante o desenvolvimento para evitar `FileNotFoundException`. Troque para um caminho relativo quando o projeto for empacotado.

### Etapa 2: Acessar a primeira planilha

```java
        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

A primeira planilha (`index 0`) normalmente contém os dados que você deseja transformar. Se seus dados estiverem em outra planilha, altere o índice ou use `get("SheetName")`.  

**Por que este passo é importante**: Trabalhar com a planilha correta garante que a fórmula WRAPCOLS faça referência ao intervalo desejado.

### Etapa 3: Definir a fórmula WRAPCOLS

```java
        // Step 3: Set the WRAPCOLS formula in cell A1
        worksheet.getCells().get("A1").setFormula("=WRAPCOLS(A1:A10, 3)");
```

`WRAPCOLS(range, columns)` é a **wrap columns excel function** que distribui os valores de `range` pelas colunas especificadas. Neste exemplo, pegamos os valores de `A1:A10` e os distribuímos em três colunas, começando em `A1`.  

**Por que este passo é importante**: A fórmula faz o trabalho pesado — não é necessário loop manual ou manipulação de arrays.  

**Dica para convert range to columns**: Ajuste o segundo argumento (`3`) para corresponder ao número de colunas que você precisa. Se o comprimento do intervalo não for múltiplo da contagem de colunas, a última coluna conterá os itens restantes.

### Etapa 4: Salvar a pasta de trabalho

```java
        // Step 4: Save the workbook with the formula applied
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Salvar grava a fórmula WRAPCOLS em `output.xlsx`. Quando você abrir o arquivo no Excel, a fórmula será avaliada e exibirá os dados distribuídos nas colunas.  

**Por que este passo é importante**: Persistir a pasta de trabalho permite que você verifique o resultado e compartilhe o arquivo com usuários que não utilizam Java.

![Fórmula Wrapcols aplicada no Excel](wrapcols-example.png){: .align-center alt="Captura de tela de como usar wrapcols no Excel"}

### Saída esperada

Ao abrir `output.xlsx`, as células `A1:C4` (ou quantas linhas forem necessárias) conterão a lista original de `A1:A10` distribuída em três colunas. O layout fica assim:

| A | B | C |
|---|---|---|
| Item 1 | Item 4 | Item 7 |
| Item 2 | Item 5 | Item 8 |
| Item 3 | Item 6 | Item 9 |
| Item 10 |   |   |

A **wrap columns excel function** preenche automaticamente as células vazias com espaços em branco, portanto você não precisa de código adicional de limpeza.

## Entendendo a wrap columns excel function

A fórmula WRAPCOLS faz parte das funções de matriz dinâmica do Excel introduzidas no Excel 365. Ela funciona de forma semelhante ao `TEXTSPLIT`, mas foca na distribuição por colunas.  

- **Sintaxe**: `=WRAPCOLS(source_range, columns)`  
- **Parâmetros**:  
  - `source_range` – o intervalo vertical que você deseja remodelar.  
  - `columns` – o número de colunas nas quais os dados serão distribuídos.  

Ao chamar `=WRAPCOLS(A1:A10, 3)`, o Excel trata a origem como um array unidimensional e preenche a primeira coluna, depois a segunda e assim por diante, até que todos os valores sejam posicionados. Isso torna **how to use wrapcols** uma ferramenta perfeita para converter uma lista de uma única coluna em um relatório de múltiplas colunas sem VBA.

## Converter intervalo em colunas sem fórmulas (opcional)

Se você preferir executar a operação **convert range to columns** totalmente em Java — sem depender do motor de cálculo do Excel —, pode ler os valores de origem, montar um array bidimensional e gravá‑los de volta manualmente:

```java
        // Optional: programmatic conversion without WRAPCOLS
        Cells cells = worksheet.getCells();
        int rows = 10; // A1:A10
        int cols = 3;
        String[][] matrix = new String[rows][cols];

        // Fill matrix column‑wise
        for (int i = 0; i < rows; i++) {
            String value = cells.get(i, 0).getStringValue(); // column A
            int colIdx = i % cols;
            int rowIdx = i / cols;
            matrix[rowIdx][colIdx] = value;
        }

        // Write matrix back starting at A1
        for (int r = 0; r < rows / cols + 1; r++) {
            for (int c = 0; c < cols; c++) {
                if (matrix[r][c] != null) {
                    cells.get(r, c).putValue(matrix[r][c]);
                }
            }
        }
```

Este trecho mostra uma maneira alternativa de **convert range to columns** quando você precisa de controle total sobre a saída (por exemplo, aplicando formatação personalizada por coluna). No entanto, usar a **wrap columns excel function** via WRAPCOLS costuma ser mais conciso e permite que o Excel trate a recalculação automaticamente.

## Casos de borda e boas práticas

- **Células vazias**: WRAPCOLS trata células vazias como espaços em branco. Se o seu intervalo de origem contiver lacunas, a saída preservará esses espaços.  
- **Intervalos dinâmicos**: Use um intervalo nomeado ou uma referência de tabela (`Table1[Column]`) para que a fórmula se ajuste quando linhas forem adicionadas.  
- **Desempenho**: Aplicar a fórmula é O(1) porque o Excel a avalia de forma preguiçosa. A conversão programática mostrada acima é O(n) e pode ser mais lenta para intervalos muito grandes.  
- **Compatibilidade de versão**: A função WRAPCOLS requer Excel 365 ou posterior. Se precisar dar suporte a versões mais antigas, use o método de conversão do lado Java.  

## Como usar wrapcols em outros cenários

- **Painéis de relatório**: Transforme uma lista vertical de nomes de KPI em uma tabela compacta com três colunas por linha.  
- **Formulários de entrada de dados**: Converta uma coluna de entradas de usuário em um layout lado a lado para facilitar a comparação visual.  
- **Exportação para CSV**: Após aplicar WRAPCOLS, salve a pasta de trabalho como CSV para obter uma visualização delimitada que corresponda ao layout de colunas.  

Cada um desses casos segue o mesmo padrão **how to use wrapcols**: carregar, referenciar, definir a fórmula, salvar.

## Conclusão

Agora você sabe **how to use wrapcols** em Java com Aspose.Cells para **convert range to columns** de forma eficiente. Ao aplicar a fórmula `WRAPCOLS` você aproveita a *wrap columns excel function* nativa, mantendo seu código conciso enquanto permite que o Excel tenha controle total sobre o cálculo e a exibição.  

Experimente diferentes contagens de colunas, intervalos dinâmicos ou a conversão opcional apenas em Java para atender às necessidades do seu projeto. Quando você dominar essa técnica, remodelar dados no Excel se torna uma operação de uma linha ao invés de uma tarefa manual.

---


## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como usar wrapcols para converter uma lista em múltiplas colunas em Java](/cells/english/java/formulas-functions/how-to-use-wrapcols-to-convert-a-list-into-multiple-columns/)
- [Como usar WRAPCOLS em Java – Guia completo de fórmulas de matriz do Excel](/cells/english/java/integration-interoperability/how-to-use-wrapcols-in-java-complete-guide-to-excel-array-fo/)
- [Como usar WRAPCOLS em Java – Exemplo completo de WRAPCOLS no Excel](/cells/english/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}