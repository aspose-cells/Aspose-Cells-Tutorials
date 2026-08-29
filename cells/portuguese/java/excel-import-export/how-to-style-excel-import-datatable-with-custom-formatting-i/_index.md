---
category: general
date: 2026-07-03
description: Como estilizar arquivos Excel usando Java. Aprenda a formatar a data
  de coluna no Excel, aplicar formato numérico no Excel, exportar DataTable para XLSX
  e importar DataTable para o Excel com Aspose Cells.
draft: false
keywords:
- how to style excel
- format column date excel
- apply number format excel
- export datatable to xlsx
- import datatable into excel
language: pt
og_description: Como estilizar arquivos Excel em Java. Este tutorial mostra como formatar
  a data da coluna no Excel, aplicar formato numérico no Excel, exportar DataTable
  para XLSX e importar DataTable para o Excel.
og_title: Como estilizar o Excel – Guia Java para formatação personalizada de colunas
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to style Excel files using Java. Learn to format column date Excel,
    apply number format Excel, export DataTable to XLSX and import DataTable into
    Excel with Aspose Cells.
  headline: How to Style Excel – Import DataTable with Custom Formatting in Java
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: Como estilizar o Excel – Importar DataTable com formatação personalizada em
  Java
url: /pt/java/excel-import-export/how-to-style-excel-import-datatable-with-custom-formatting-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Estilizar Excel – Importar DataTable com Formatação Personalizada em Java

Já se perguntou **como estilizar planilhas Excel** programaticamente sem abrir o arquivo manualmente? Você não está sozinho. Muitos desenvolvedores precisam gerar relatórios onde a primeira coluna está em negrito, a segunda exibe datas e o restante segue um layout limpo. Neste guia vamos percorrer um exemplo completo e executável que **importa um DataTable para o Excel**, aplica um cabeçalho em negrito, formata uma coluna de data e, finalmente, **exporta DataTable para XLSX**.  

Usaremos Aspose.Cells para Java, mas os conceitos se aplicam a qualquer biblioteca que permita trabalhar com estilos. Ao final, você terá um padrão reutilizável para **apply number format Excel** células, **format column date Excel**, e entregar uma planilha polida aos seus usuários.

## Pré‑requisitos

- Java 17 (ou qualquer JDK recente)  
- Aspose.Cells for Java 23.9 ou mais recente (a versão de avaliação gratuita funciona)  
- Uma estrutura semelhante a `DataTable` (o exemplo usa um mock simples)  
- Seu IDE favorito (IntelliJ IDEA, Eclipse, VS Code…)

Nenhum plugin Maven adicional é necessário; basta adicionar o JAR do Aspose.Cells ao seu classpath.

---

## Etapa 1: Obter o DataTable Fonte – Preparação do “Export DataTable to XLSX”

Antes de podermos **importar datatable into excel**, precisamos de um objeto `DataTable` que represente os dados que você deseja exportar. Em projetos reais você pode obtê‑los de um banco de dados, arquivo CSV ou uma API. Para este tutorial vamos simular uma tabela pequena:

```java
import java.util.*;
import com.aspose.cells.*;

public class DemoData {
    public static DataTable getDataTable() {
        // Create a simple table with three columns: ID, Date, Amount
        DataTable dt = new DataTable();
        dt.getColumns().add("ID", DataType.INTEGER);
        dt.getColumns().add("OrderDate", DataType.DATE_TIME);
        dt.getColumns().add("Total", DataType.DOUBLE);

        // Add a few rows
        dt.getRows().add(new Object[]{1, new Date(), 125.50});
        dt.getRows().add(new Object[]{2, new Date(System.currentTimeMillis() - 86400000L), 99.99});
        dt.getRows().add(new Object[]{3, new Date(System.currentTimeMillis() - 2*86400000L), 250.00});
        return dt;
    }
}
```

> **Por que isso importa:** Obter os dados corretos logo no início significa que o restante da lógica de estilo pode focar exclusivamente na apresentação, não na manipulação dos dados.

---

## Etapa 2: Criar um Array para Guardar as Definições de Estilo de Cada Coluna

Aspose.Cells permite que você passe um array **Style[]** ao importar um `DataTable`. Cada entrada corresponde a uma coluna e determina como essa coluna ficará após a importação. Vamos alocar o array com base no número de colunas:

```java
DataTable dataTable = DemoData.getDataTable();
Style[] columnStyles = new Style[dataTable.getColumns().size()];
```

> **Dica:** Se você tem muitas colunas, considere construir o array em um loop e reutilizar um único objeto `Style` onde a formatação seja idêntica. Isso reduz o consumo de memória.

---

## Etapa 3: Definir os Estilos – Cabeçalho em Negrito e Formatação de Data

Agora respondemos à clássica pergunta **format column date excel** e também demonstramos **apply number format excel** para outras colunas.

```java
// --- Style for the first column (header bold) ---
columnStyles[0] = new Style();
columnStyles[0].getFont().setBold(true);          // Makes header text bold

// --- Style for the second column (date formatting) ---
columnStyles[1] = new Style();
columnStyles[1].setNumber(StyleNumberFormat.DATE); // Uses the built‑in DATE format

// --- Optional: Style for the third column (currency) ---
columnStyles[2] = new Style();
columnStyles[2].setNumber(StyleNumberFormat.CURRENCY_USD);
```

**O que está acontecendo aqui?**  
- `StyleNumberFormat.DATE` indica ao Excel que o valor da célula deve ser tratado como data curta (ex.: *31/01/2024*).  
- `StyleNumberFormat.CURRENCY_USD` adiciona automaticamente o símbolo `$` e duas casas decimais.  
- Definir a fonte em negrito na primeira coluna faz o cabeçalho se destacar, o que é um requisito frequente quando você **how to style excel** planilhas para melhorar a legibilidade.

> **Caso extremo:** Se seus dados de origem já contêm strings formatadas, pode ser necessário convertê‑las para objetos `java.util.Date` antes da importação; caso contrário, o Excel as tratará como texto simples.

---

## Etapa 4: Criar uma Nova Pasta de Trabalho e Acessar sua Primeira Planilha

Uma pasta de trabalho nova nos fornece uma tela limpa. Vamos obter a primeira planilha, que é onde a importação será feita.

```java
Workbook workbook = new Workbook();               // New empty workbook
Worksheet worksheet = workbook.getWorksheets().get(0); // First sheet (index 0)
```

> **Por que uma nova pasta de trabalho?** Começar do zero garante que nenhum estilo residual ou linhas ocultas interfiram no resultado final—essencial quando você **how to style excel** arquivos de forma consistente em várias execuções.

---

## Etapa 5: Importar o DataTable com os Estilos das Colunas

Aqui está o núcleo da operação: alimentar o `DataTable` na planilha enquanto aplicamos o array de estilos que criamos.

```java
// The third argument (true) tells Aspose.Cells to include column headers.
worksheet.getCells().importDataTable(dataTable, true, columnStyles);
```

**Explicação:**  
- `importDataTable` copia tanto a linha de cabeçalho quanto as linhas de dados.  
- O array `columnStyles` alinha‑se com cada coluna, de modo que o cabeçalho da primeira coluna fique em negrito, a segunda coluna mostre datas e a terceira coluna apareça como moeda.  
- Essa única linha substitui dezenas de passos manuais de formatação célula a célula, ilustrando uma maneira limpa de **apply number format excel** programaticamente.

---

## Etapa 6: Salvar a Pasta de Trabalho Estilizada – Concluindo o “Export DataTable to XLSX”

Por fim, persistimos a pasta de trabalho no disco. Ajuste o caminho para uma pasta gravável na sua máquina.

```java
String outputPath = "C:/temp/styledImport.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Abra o arquivo no Excel e você deverá ver:

- Cabeçalho da coluna **ID** em negrito.  
- Coluna **OrderDate** formatada como datas (ex.: *27/04/2024*).  
- Coluna **Total** exibida com o símbolo de dólar e duas casas decimais.

> **Dica de especialista:** Se precisar dar suporte a versões mais antigas do Excel, chame `workbook.save(outputPath, SaveFormat.XLS)` em vez do padrão XLSX.

---

## Etapa 7: Verificar o Resultado & Ajustes Opcionais

É uma boa prática conferir o arquivo gerado, especialmente ao automatizar relatórios para partes interessadas.

```java
// Quick verification: read the first cell's style
Cell firstHeader = worksheet.getCells().get(0, 0);
boolean isBold = firstHeader.getStyle().getFont().isBold();
System.out.println("Header bold? " + isBold);
```

Se `isBold` imprimir `true`, sua rotina **how to style excel** funcionou como esperado. A partir daqui você pode:

- Adicionar formatação condicional (ex.: destacar totais > $200).  
- Congelar a primeira linha para facilitar a rolagem.  
- Inserir um gráfico que faça referência aos dados importados.

Todas essas extensões seguem o mesmo padrão: definir um `Style`, aplicá‑lo e salvar.

---

## Perguntas Frequentes & Casos de Borda

| Pergunta | Resposta |
|----------|----------|
| **Posso estilizar mais de uma coluna da mesma forma?** | Sim—reutilize uma única instância de `Style` para todas as colunas que compartilham a mesma formatação. |
| **E se meu DataTable tiver mais colunas que estilos?** | Qualquer coluna sem uma entrada correspondente em `columnStyles` usará o estilo padrão. |
| **Como mudar o formato de data para “dd‑MMM‑yyyy”?** | Use `columnStyles[1].setCustom("#dd-MMM-yyyy#");` em vez do `DATE` embutido. |
| **Existe uma forma de auto‑ajustar colunas após a importação?** | Chame `worksheet.autoFitColumns();` após `importDataTable`. |
| **Isso funciona em Linux/macOS?** | Absolutamente—Aspose.Cells é independente de plataforma, contanto que você tenha um JDK compatível. |

---

## Conclusão

Agora você tem um exemplo sólido, de ponta a ponta, de **how to style Excel** ao **importar datatable into excel**, **format column date excel**, e **apply number format excel** usando Java. O código mostra todo o fluxo desde **export datatable to xlsx** até abrir o arquivo no Excel, cobrindo tanto o *quê* quanto o *porquê* de cada passo.  

Experimente: ajuste o array de estilos, adicione mais colunas ou conecte a uma consulta real ao banco de dados. O mesmo padrão permitirá gerar relatórios com aparência profissional ao clique de um botão, sem necessidade de formatação manual.

---

![Styled Excel worksheet generated by the tutorial code](https://example.com/images/styled-worksheet.png "Captura de tela da planilha Excel estilizada criada com Java e Aspose.Cells")

*Texto alternativo da imagem: “Planilha Excel estilizada criada com Java e Aspose.Cells, mostrando cabeçalho em negrito e coluna de data formatada.”*


## O Que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [How to Style Excel Cells and Add Hyperlinks Using Aspose.Cells for Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)
- [Aspose.Cells for Java: How to Create and Format Excel Workbooks Efficiently](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}