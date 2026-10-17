---
category: general
date: 2026-06-18
description: Tutorial Java para criar arquivo Excel mostrando como definir a cor de
  fundo das linhas, gerar Excel a partir de DataTable e salvar a planilha como XLSX
  com sombreamento alternado de linhas.
draft: false
keywords:
- create excel file java
- set row background color
- save workbook as xlsx
- alternating row shading excel
- generate excel from datatable
language: pt
og_description: Crie um arquivo Excel em Java passo a passo. Aprenda a definir a cor
  de fundo das linhas, aplicar sombreamento alternado nas linhas, gerar Excel a partir
  de DataTable e salvar a pasta de trabalho como XLSX.
og_title: Criar Arquivo Excel em Java – Guia Completo de Estilização e Exportação
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Create Excel file Java tutorial showing how to set row background color,
    generate Excel from DataTable, and save workbook as XLSX with alternating row
    shading.
  headline: Create Excel File Java – Full Guide with Row Styling and XLSX Export
  type: TechArticle
- description: Create Excel file Java tutorial showing how to set row background color,
    generate Excel from DataTable, and save workbook as XLSX with alternating row
    shading.
  name: Create Excel File Java – Full Guide with Row Styling and XLSX Export
  steps:
  - name: Exporting a Large DataTable
    text: 'When dealing with 100k+ rows, you may hit memory limits. Aspose.Cells supports
      **streaming** mode:'
  - name: Using Apache POI Instead of Aspose.Cells
    text: 'If licensing is a concern, you can replace the import logic with POI’s
      `CellStyle` objects. The concept stays the same: create two `CellStyle`s, loop
      over rows, and apply `setFillForegroundColor` with `IndexedColors`. The only
      downside is the code becomes a bit more verbose.'
  - name: Adding Conditional Formatting
    text: 'Suppose you want to highlight any score above 90 in green. Add this after
      the import:'
  type: HowTo
tags:
- java
- excel
- aspose-cells
- data-export
title: Criar Arquivo Excel em Java – Guia Completo com Estilização de Linhas e Exportação
  XLSX
url: /pt/java/excel-import-export/create-excel-file-java-full-guide-with-row-styling-and-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Arquivo Excel Java – Guia Completo com Estilização de Linhas e Exportação XLSX

Já se perguntou como **criar excel file java** que pareça polido logo de cara? Você não está sozinho — desenvolvedores frequentemente precisam de uma maneira rápida de transformar dados tabulares em uma planilha bem formatada sem abrir o Excel manualmente. Neste tutorial vamos percorrer uma solução completa: obter dados de um `DataTable`, aplicar **alternating row shading excel**, e finalmente **save workbook as xlsx**. Ao final, você terá um trecho reutilizável que pode ser inserido em qualquer projeto Java.

Cobriremos tudo o que você precisa: a biblioteca necessária (Aspose.Cells for Java), o código exato para definir **row background color**, como **generate excel from datatable**, e algumas dicas práticas para evitar armadilhas comuns. Sem enrolação, apenas um exemplo sólido, pronto‑para‑executar, que você pode adaptar hoje.

## Pré‑requisitos

Antes de mergulharmos, certifique‑se de que você tem:

- Java 17 ou superior (o código funciona com qualquer JDK recente)
- Maven ou Gradle para gerenciar dependências
- Noções básicas de coleções Java
- Acesso à biblioteca Aspose.Cells for Java (versão trial ou licenciada)

Se preferir uma alternativa open‑source, a lógica se traduz facilmente para Apache POI — basta trocar as chamadas de API. Por brevidade, ficaremos com Aspose.Cells porque seu método `importDataTable` torna o passo **generate excel from datatable** um comando de uma linha.

## Etapa 1: Configurar o Projeto e Adicionar Aspose.Cells

Adicione a dependência a seguir ao seu `pom.xml` (Maven) ou `build.gradle` (Gradle). Isso traz a biblioteca principal que nos permite manipular workbooks, estilos e cores.

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

```gradle
// Gradle
implementation 'com.aspose:aspose-cells:24.9'
```

Após atualizar seu projeto, você está pronto para escrever código Java no estilo **create excel file java**.

## Etapa 2: Criar o Workbook e Carregar Seus Dados

Primeiro instanciamos um novo `Workbook`. Em seguida, obtemos um `DataTable` — isso pode ser o resultado de uma consulta JDBC, de um parser CSV ou de qualquer tabela em memória que você já possua.

```java
import com.aspose.cells.*;

public class ExcelExporter {

    // Simulated method that returns a DataTable with dummy data
    private static DataTable getData() {
        DataTable dt = new DataTable();
        dt.getColumns().add("ID", DataType.INTEGER);
        dt.getColumns().add("Name", DataType.STRING);
        dt.getColumns().add("Score", DataType.DOUBLE);

        // Add some rows
        dt.getRows().add(new Object[]{1, "Alice", 92.5});
        dt.getRows().add(new Object[]{2, "Bob", 85.0});
        dt.getRows().add(new Object[]{3, "Charlie", 78.3});
        dt.getRows().add(new Object[]{4, "Diana", 88.9});
        return dt;
    }

    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook (or load an existing one)
        Workbook workbook = new Workbook();

        // Step 2: Obtain the data to be written as a DataTable
        DataTable dataTable = getData(); // assume this returns the source data
```

Neste ponto temos um workbook limpo e um `DataTable` preenchido. O próximo passo é onde a mágica visual acontece.

## Etapa 3: Definir Estilos de Linha – Definindo a Cor de Fundo da Linha

Queremos que cada linha tenha um fundo distinto, alternando entre azul claro e cinza claro. Isso melhora a legibilidade, especialmente em relatórios extensos. O código abaixo cria um array `Style` — uma entrada por linha de dados — e atribui um **set row background color** com base no índice da linha.

```java
        // Step 3: Prepare an array of row styles – one style per data row
        Style[] rowStyles = new Style[dataTable.getRows().size()];
        for (int i = 0; i < rowStyles.length; i++) {
            rowStyles[i] = workbook.createStyle();

            // Step 4: Alternate background colors for better readability
            if (i % 2 == 0) {
                // Even rows – light blue
                rowStyles[i].setForegroundColor(Color.getLightBlue());
            } else {
                // Odd rows – light gray
                rowStyles[i].setForegroundColor(Color.getLightGray());
            }
            // Apply solid fill pattern
            rowStyles[i].setPattern(BackgroundType.SOLID);
        }
```

Observe como usamos `Color.getLightBlue()` e `Color.getLightGray()`. Aspose.Cells oferece uma paleta rica, mas você pode substituir essas chamadas por qualquer `Color` que desejar — talvez as cores da sua marca corporativa.

## Etapa 4: Importar o DataTable com Estilização

Agora juntamos os dados e o array de estilos. O método `importDataTable` cuida de copiar as linhas, aplicar o estilo correspondente e ainda adiciona cabeçalhos de coluna se você passar `true` para o parâmetro `importColumnNames`.

```java
        // Step 5: Import the DataTable into the first worksheet using the styles
        Worksheet sheet = workbook.getWorksheets().get(0);
        sheet.getCells().importDataTable(dataTable, true, "A1", rowStyles);
```

A âncora `"A1"` indica ao Aspose onde começar a escrever — canto superior esquerdo da planilha. Como fornecemos o array `rowStyles`, cada linha herda a cor de fundo que definimos anteriormente, alcançando **alternating row shading excel** sem precisar de um loop após a importação.

## Etapa 5: Salvar o Workbook Estilizado como XLSX

Por fim, persistimos o workbook no disco. O método `save` determina automaticamente o formato a partir da extensão do arquivo, então usar `.xlsx` nos dá um workbook Office Open XML moderno que pode ser aberto no Excel, Google Sheets ou LibreOffice.

```java
        // Step 6: Save the styled workbook to a file
        workbook.save("styledTable.xlsx"); // save workbook as xlsx
        System.out.println("Excel file created successfully!");
    }
}
```

Executar o método `main` produz um arquivo chamado `styledTable.xlsx` no diretório raiz do seu projeto. Abra‑lo e você verá uma tabela bem formatada com cores de linha alternadas — exatamente o que um stakeholder de negócios espera de um relatório.

![Screenshot of styled Excel file created with Java](images/styled_excel_java.png "exemplo de create excel file java")

*Texto alternativo da imagem:* **create excel file java** captura de tela mostrando sombreamento alternado de linhas

## Por Que Essa Abordagem Funciona Melhor Que a Estilização Manual Célula‑a‑Célula

Você pode se perguntar por que usamos um array de estilos em vez de percorrer cada linha após a importação. A resposta tem duas partes:

1. **Performance** – Aplicar um estilo durante a importação evita uma passagem extra sobre a planilha, o que pode ser custoso para milhares de linhas.
2. **Manutenibilidade** – A lógica de estilo fica em um único lugar (`rowStyles`), facilitando a troca de cores, adição de bordas ou mudança de padrão sem tocar no código de importação.

Se mais tarde precisar adicionar indicadores visuais (por exemplo, destacar linhas com pontuação abaixo de um limite), basta estender o bloco `if` dentro do loop — nenhuma outra alteração será necessária.

## Variações Comuns e Casos de Borda

### Exportando um DataTable Grande

Ao lidar com mais de 100 mil linhas, você pode atingir limites de memória. Aspose.Cells suporta modo **streaming**:

```java
Workbook wb = new Workbook(FileFormatType.XLSX);
wb.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
```

Defina a preferência de memória antes de criar os estilos, e a biblioteca escreverá os dados em arquivos temporários ao invés de mantê‑los todos na RAM.

### Usando Apache POI em Vez de Aspose.Cells

Se a licença for um problema, você pode substituir a lógica de importação pelos objetos `CellStyle` do POI. O conceito permanece o mesmo: criar dois `CellStyle`s, percorrer as linhas e aplicar `setFillForegroundColor` com `IndexedColors`. A única desvantagem é que o código fica um pouco mais verboso.

### Adicionando Formatação Condicional

Suponha que você queira destacar qualquer pontuação acima de 90 em verde. Adicione isso após a importação:

```java
FormatConditionCollection fcc = sheet.getConditionalFormattings().add();
FormatCondition fc = fcc.addCondition(FormatConditionType.CELL_VALUE, OperatorType.GREATER_THAN, "90");
Style conditionStyle = workbook.createStyle();
conditionStyle.setForegroundColor(Color.getLightGreen());
conditionStyle.setPattern(BackgroundType.SOLID);
fc.setStyle(conditionStyle);
```

Agora a planilha não só tem sombreamento alternado, mas também realces dinâmicos.

## Recapitulação: O Que Conquistamos

- **Create excel file java** a partir de um `DataTable` usando Aspose.Cells.
- **Set row background color** programaticamente, alcançando **alternating row shading excel**.
- **Save workbook as xlsx**, garantindo compatibilidade com ferramentas de planilha modernas.
- Demonstrado como **generate excel from datatable** de forma eficiente e extensível.

Tudo isso cabe em uma classe Java compacta e fácil de ler, que você pode copiar‑colar para sua própria base de código.

## Próximos Passos e Tópicos Relacionados

Se você gostou deste walkthrough, também pode explorar:

- **Exportando gráficos** de Java para Excel (API de gráficos do Aspose.Cells).
- **Protegendo com senha** o workbook gerado (`workbook.protect(...)`).
- **Escrevendo grandes conjuntos de dados** com streaming para manter baixo o uso de memória.
- **Integrando com Spring Boot** para servir o arquivo gerado como resposta para download.

Cada um desses tópicos se baseia na mesma fundação que apresentamos aqui — então sinta‑se à vontade para experimentar e expandir.

---

*Feliz codificação! Se encontrar algum obstáculo ou tiver ideias para melhorias adicionais, deixe um comentário abaixo. Vamos manter a conversa em andamento.*

## O Que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Create an Excel Workbook using Aspose.Cells in Java: A Step‑By‑Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [How to Set Excel Row Heights Using Aspose.Cells for Java - A Complete Guide](/cells/english/java/formatting/mastering-excel-row-heights-aspose-cells-java/)
- [How to Create Excel File Java and Style It with Aspose.Cells](/cells/english/java/advanced-features/excel-master-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}