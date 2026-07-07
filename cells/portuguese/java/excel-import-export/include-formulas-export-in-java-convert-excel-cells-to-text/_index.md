---
category: general
date: 2026-07-03
description: Inclua a exportação de fórmulas em Java para converter células do Excel
  em texto usando Aspose.Cells. Aprenda como imprimir um intervalo do Excel e obter
  a string de valores das células de forma eficiente.
draft: false
keywords:
- include formulas export
- convert excel cells text
- print excel range
- export table options
- get cell values string
language: pt
og_description: Inclua exportação de fórmulas em Java para converter células do Excel
  em texto. Guia passo a passo mostrando como imprimir um intervalo do Excel e recuperar
  os valores das células como uma string.
og_title: Incluir Exportação de Fórmulas em Java – Converter Células do Excel em Texto
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  headline: Include Formulas Export in Java – Convert Excel Cells to Text
  type: TechArticle
- description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  name: Include Formulas Export in Java – Convert Excel Cells to Text
  steps:
  - name: Prerequisites
    text: '- Java 17 or newer (the code compiles with older versions but we’ll stick
      to the latest LTS). - Aspose.Cells for Java 23.10 (or any recent release)—you
      can grab it from Maven Central. - A sample `input.xlsx` placed in a folder you
      control (the path is hard‑coded in the example for clarity).'
  - name: Optional Tweaks
    text: '- `eto.setExportHiddenRows(true);` – include rows hidden in Excel. - `eto.setExportHiddenColumns(true);`
      – same for columns. - `eto.setExportAsHTML(true);` – get HTML instead of plain
      text.'
  - name: Expected Output (sample)
    text: '``` =SUM(A2:A3) 42 Hello =IF(B1>10,"Yes","No") =AVERAGE(C1:C3) =VLOOKUP(A1,Sheet2!A:B,2,FALSE)
      ```'
  - name: What if the range contains merged cells?
    text: Merged cells are treated as the value of the top‑left cell. The rest of
      the merged area will appear as empty strings. If you need the merged region’s
      address, query `Cell.getMergedRange()` before export.
  - name: Can I export a massive sheet (hundreds of thousands of rows)?
    text: Yes, but beware of memory consumption. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to let Aspose.Cells stream data to disk. Also, consider exporting in chunks
      (e.g., 10 000 rows at a time) to keep the string manageable.
  - name: How do I change the column delimiter?
    text: '`ExportTableOptions` exposes `setSeparator(char separator)`. For CSV‑style
      output, set it to `'',''`:'
  - name: Do formulas respect external references?
    text: If a formula points to another workbook, Aspose.Cells will keep the reference
      text (`='[Other.xlsx]Sheet1'!A1`). It won’t evaluate the external value unless
      you load that workbook as well.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Export
title: Incluir Exportação de Fórmulas em Java – Converter Células do Excel para Texto
url: /pt/java/excel-import-export/include-formulas-export-in-java-convert-excel-cells-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Incluir Exportação de Fórmulas em Java – Converter Células do Excel em Texto

Já precisou **incluir exportação de fórmulas** ao extrair dados de uma pasta de trabalho do Excel? Talvez você esteja construindo um serviço de relatórios que deve preservar as fórmulas originais enquanto ainda entrega um bloco de texto organizado. Nesse caso, você está no lugar certo. Este guia mostra como converter células do Excel em texto simples—*incluindo* quaisquer fórmulas incorporadas—usando Aspose.Cells for Java.

Também abordaremos como **imprimir intervalo do Excel**, ajustar **opções de exportação de tabela**, e finalmente **obter string de valores de célula** que você pode registrar, enviar via API ou armazenar em um banco de dados. Ao final, você terá um trecho totalmente executável e uma compreensão sólida do porquê de cada chamada.

## O que você levará consigo

- Um programa Java completo, pronto para copiar e colar, que lê um arquivo `.xlsx`, seleciona um intervalo e o exporta como uma string formatada.
- Compreensão da classe `ExportTableOptions` e por que alternar `setExportAsString` e `setIncludeFormula` é importante.
- Dicas para lidar com planilhas grandes, tratar diferentes tipos de dados e personalizar o formato de saída.
- Uma lista de verificação rápida para armadilhas comuns (por exemplo, células mescladas, linhas ocultas e formatos numéricos específicos de localidade).

### Pré-requisitos

- Java 17 ou superior (o código compila com versões mais antigas, mas usaremos a última LTS).
- Aspose.Cells for Java 23.10 (ou qualquer versão recente) — você pode obtê-lo no Maven Central.
- Um exemplo `input.xlsx` colocado em uma pasta que você controla (o caminho está codificado no exemplo para clareza).

Se você já tem isso, vamos mergulhar.

## Etapa 1: Configurar o Projeto e Adicionar Dependências

Primeiro, crie um projeto Maven (ou Gradle, se preferir). Adicione a dependência Aspose.Cells ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Dica profissional:** Se você estiver usando um proxy corporativo, certifique‑se de que o repositório esteja acessível; caso contrário, a compilação falhará com o erro “Could not resolve dependencies”.

Quando o Maven terminar de baixar, você estará pronto para escrever um pouco de Java.

## Etapa 2: Carregar a Pasta de Trabalho e Obter a Planilha Desejada

A primeira linha do exemplo de código mostra como abrir uma pasta de trabalho existente:

```java
// Step 1: Load the workbook
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Substitua `YOUR_DIRECTORY` pelo caminho absoluto ou relativo do seu arquivo. O construtor `Workbook` detecta automaticamente o formato do arquivo (XLS, XLSX, CSV, etc.), portanto você não precisa especificá‑lo.

Em seguida, buscamos a primeira planilha:

```java
// Step 2: Get the first worksheet
Worksheet ws = wb.getWorksheets().get(0);
```

Por que a primeira planilha? Em muitos modelos os dados ficam na primeira aba, mas você pode passar qualquer índice ou até usar `get("SheetName")` se preferir uma abordagem por nome.

## Etapa 3: Definir o Intervalo que Você Deseja Exportar

Agora vem o coração da operação de **converter células do Excel em texto**. Você indica ao Aspose.Cells quais células extrair criando um objeto `Range`:

```java
// Step 3: Create a range covering cells A1 to C3
Range rng = ws.getCells().createRange("A1:C3");
```

A string `"A1:C3"` é um endereço clássico no estilo A1. Ela também pode ser construída programaticamente:

```java
int firstRow = 0, firstCol = 0, totalRows = 3, totalCols = 3;
Range rng = ws.getCells().createRange(firstRow, firstCol, totalRows, totalCols);
```

Essa flexibilidade ajuda quando o tamanho do intervalo é dinâmico — por exemplo, você lê a última linha usada com `ws.getCells().getMaxDataRow()`.

## Etapa 4: Configurar ExportTableOptions para Incluir Fórmulas

Aqui está onde a mágica de **incluir exportação de fórmulas** acontece. Por padrão, Aspose.Cells retorna os valores *exibidos*. Se uma célula contém `=SUM(A1:A3)`, você obterá o número calculado, não o texto da fórmula. Para mudar isso, configure `ExportTableOptions`:

```java
// Step 4: Set up export options to return the range as a string and include formulas
ExportTableOptions eto = new ExportTableOptions();
eto.setExportAsString(true);      // Forces the result to be a single string
eto.setIncludeFormula(true);      // Includes the underlying formula instead of the evaluated value
```

Por que ambas as flags? `setExportAsString(true)` indica à API concatenar as células usando o delimitador padrão (tabulação para colunas, nova linha para linhas). `setIncludeFormula(true)` altera a fonte do valor de “valor exibido” para “fórmula bruta”. Se você quiser apenas valores, deixe `false`.

### Ajustes Opcionais

- `eto.setExportHiddenRows(true);` – inclui linhas ocultas no Excel.  
- `eto.setExportHiddenColumns(true);` – mesmo para colunas.  
- `eto.setExportAsHTML(true);` – obtém HTML em vez de texto simples.

Sinta‑se à vontade para experimentar; a classe de opções é um playground de **export table options**.

## Etapa 5: Recuperar o Intervalo como uma String Formatada

Agora extraímos os dados:

```java
// Step 5: Retrieve the range values as a formatted string using the options
String txt = rng.getValueAsString(eto);
```

A string `txt` retornada se parece com isto (supondo que A1:C3 contenha uma mistura de valores e fórmulas):

```
=SUM(A2:A3)	42	"Hello"
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Observe a tabulação (`\t`) separando colunas e a nova linha (`\n`) separando linhas. Você pode dividir a string depois se precisar de um array 2‑D:

```java
String[] rows = txt.split("\n");
for (String row : rows) {
    String[] cells = row.split("\t");
    // Process each cell...
}
```

## Etapa 6: Imprimir o Resultado – “Imprimir Intervalo do Excel” Simplificado

Finalmente, despejamos a string no console:

```java
// Step 6: Print the resulting string
System.out.println(txt);
```

Executar o programa imprime exatamente a saída mostrada acima. A partir daqui você pode gravar a string em um arquivo de log, enviá‑la via HTTP ou armazená‑la em um documento NoSQL.

## Exemplo Completo, Pronto‑para‑Executar

Juntando tudo, aqui está o programa completo. Copie, cole e pressione **Run** — sem importações ausentes.

```java
import com.aspose.cells.*;

public class ExportFormulaRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook
        Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // Define the range A1:C3 (adjust as needed)
        Range rng = ws.getCells().createRange("A1:C3");

        // Configure export options: string output + include formulas
        ExportTableOptions eto = new ExportTableOptions();
        eto.setExportAsString(true);
        eto.setIncludeFormula(true);

        // Get the string representation of the range
        String txt = rng.getValueAsString(eto);

        // Print the resulting text
        System.out.println(txt);
    }
}
```

### Expected Output (sample)

```
=SUM(A2:A3)	42	Hello
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Se sua pasta de trabalho contém números formatados como datas, eles aparecerão no formato específico da localidade (por exemplo, `2026‑07‑03`). Para forçar datas ISO, você pode ajustar o `ExportTableOptions` com um `NumberFormat` personalizado.

## Lidando com Casos de Borda e Perguntas Frequentes

### E se o intervalo contiver células mescladas?

Células mescladas são tratadas como o valor da célula superior‑esquerda. O restante da área mesclada aparecerá como strings vazias. Se você precisar do endereço da região mesclada, consulte `Cell.getMergedRange()` antes da exportação.

### Posso exportar uma planilha massiva (centenas de milhares de linhas)?

Sim, mas tome cuidado com o consumo de memória. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` para permitir que Aspose.Cells transmita os dados para o disco. Também, considere exportar em blocos (por exemplo, 10 000 linhas por vez) para manter a string manejável.

### Como mudar o delimitador de coluna?

`ExportTableOptions` expõe `setSeparator(char separator)`. Para saída no estilo CSV, defina como `','`:

```java
eto.setSeparator(',');
```

### As fórmulas respeitam referências externas?

Se uma fórmula aponta para outra pasta de trabalho, Aspose.Cells manterá o texto da referência (`='[Other.xlsx]Sheet1'!A1`). Ele não avaliará o valor externo a menos que você carregue também essa pasta de trabalho.

## Dicas Profissionais para Código Pronto para Produção

- **Cache a pasta de trabalho** se você estiver lendo o

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como Criar e Exportar Excel para HTML Usando Aspose.Cells Java \| Guia de Operações de Pasta de Trabalho](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Como Converter Excel para PDF em Java Usando Aspose.Cells: Um Guia Passo a Passo](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Exportar Pasta de Trabalho Excel como Imagem Usando Aspose.Cells for Java: Um Guia Passo a Passo](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}