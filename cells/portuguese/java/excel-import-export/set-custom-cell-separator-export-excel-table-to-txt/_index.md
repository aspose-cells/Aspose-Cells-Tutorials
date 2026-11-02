---
category: general
date: 2026-07-16
description: Defina separador de célula personalizado ao exportar a tabela do Excel
  para TXT usando Aspose.Cells. Aprenda como exportar fórmulas do Excel para texto
  e salvar a planilha como arquivo txt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom cell separator
- export excel table to txt
- export excel formulas to text
- save worksheet as txt file
- export excel data as plain text
language: pt
lastmod: 2026-07-16
og_description: Definir separador de célula personalizado no Aspose.Cells permite
  exportar a tabela do Excel para TXT com formatação exata. Exporte fórmulas do Excel
  para texto e salve a planilha como arquivo txt facilmente.
og_image_alt: Screenshot showing set custom cell separator option in Aspose.Cells
  export settings
og_title: Definir Separador de Célula Personalizado – Exportar Tabela do Excel para
  TXT
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Set custom cell separator when exporting Excel table to TXT using Aspose.Cells.
    Learn how to export Excel formulas to text and save worksheet as txt file.
  headline: Set Custom Cell Separator – Export Excel Table to TXT
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel Export
title: Definir separador de célula personalizado – Exportar tabela do Excel para TXT
url: /pt/java/excel-import-export/set-custom-cell-separator-export-excel-table-to-txt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definir Separador de Célula Personalizado – Exportar Tabela do Excel para TXT

Definir separador de célula personalizado é o ingrediente secreto que você precisa quando deseja um despejo de texto organizado a partir de uma planilha Excel. Já se perguntou como **export excel table to txt** sem acabar com uma bagunça de vírgulas e quebras de linha? Neste tutorial vamos percorrer todo o processo usando Aspose.Cells for Java, desde o carregamento de uma pasta de trabalho até **save worksheet as txt file** com um delimitador que você escolher.

## O que você aprenderá

- Como **set custom cell separator** para exportações de texto.
- Os passos exatos para **export excel formulas to text** para que os valores avaliados viajem com você.
- Formas de **export excel data as plain text** preservando o layout.
- Um exemplo de código completo, pronto‑para‑executar, que você pode copiar‑colar em seu projeto.

Ao final deste guia, você será capaz de pegar qualquer pasta de trabalho Excel, escolher um pipe (`|`), uma tabulação (`\t`) ou qualquer caractere que desejar, e gerar um arquivo de texto delimitado limpo que os sistemas downstream adoram.

### Pré-requisitos

- Java 8 ou superior instalado.
- Maven (ou qualquer ferramenta de build) para obter a biblioteca Aspose.Cells for Java.
- Uma pasta de trabalho de exemplo (`TableDemo.xlsx`) que contém uma tabela com fórmulas.

Se você tem isso, vamos mergulhar — sem enrolação, apenas passos práticos.

## Etapa 1: Adicionar Aspose.Cells ao seu Projeto

Antes de poder **set custom cell separator**, você precisa do JAR Aspose.Cells no classpath. A maneira mais fácil é via Maven:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

Se preferir Gradle, troque o XML pelo equivalente `implementation 'com.aspose:aspose-cells:24.10'`. Depois que a dependência for resolvida, você estará pronto para escrever código Java que interage com arquivos Excel.

## Etapa 2: Carregar a Pasta de Trabalho – Preparando para Exportar Tabela Excel para TXT

A primeira linha de código real é sempre a mesma: abrir a pasta de trabalho que contém a tabela que você deseja exportar.

```java
import com.aspose.cells.*;

public class ExportTableWithOptions {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/TableDemo.xlsx");
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Aqui pegamos a primeira planilha (`get(0)`). Se seus dados estiverem em outra planilha, basta mudar o índice ou usar `get("SheetName")`. Esta parte é essencial para **export excel table to txt** porque o exportador funciona ao nível da planilha.

## Etapa 3: Definir Separador de Célula Personalizado – O Núcleo da Exportação

Agora vem a estrela do show: configurar `ExportTableOptions`. Este objeto permite que você decida exatamente como cada célula aparecerá no arquivo de texto final.

```java
        // Define how the table should be exported
        ExportTableOptions exportTableOptions = new ExportTableOptions();

        // 1️⃣ Export cell contents as plain strings (no rich formatting)
        exportTableOptions.setExportAsString(true);

        // 2️⃣ Include the evaluated formula result, not the formula itself
        exportTableOptions.setFormulaValueInCell(true);

        // 3️⃣ Set the custom separator – this is where we set custom cell separator
        exportTableOptions.setCellValueSeparator("|"); // you can use any char you like
```

Por que **set custom cell separator**? Porque o separador padrão é uma tabulação, que pode conflitar com dados que já contêm tabs. Ao escolher um pipe (`|`) ou um ponto‑e‑vírgula, você garante que cada coluna permaneça distinta quando um analisador downstream ler o arquivo.

### Exportar Fórmulas Excel para Texto

A linha `setFormulaValueInCell(true)` indica ao Aspose.Cells para escrever o **export excel formulas to text** como o *resultado* da fórmula, não a própria string da fórmula. Se você omitir isso, uma célula contendo `=SUM(A1:A5)` aparecerá como `=SUM(A1:A5)` no TXT, o que raramente é o que você deseja.

## Etapa 4: Anexar Opções de Exportação às Opções de Salvamento TXT

Agora vinculamos essas opções de tabela à configuração geral de exportação TXT.

```java
        // Attach the table export options to TXT save options
        TxtSaveOptions txtSaveOptions = new TxtSaveOptions();
        txtSaveOptions.setExportTableOptions(exportTableOptions);
```

`TxtSaveOptions` é o objeto abrangente que controla como toda a planilha é gravada. Ao inserir `exportTableOptions` nele, você garante que cada tabela na planilha respeite a regra **set custom cell separator**.

## Etapa 5: Salvar a Planilha como Arquivo TXT – Finalizando a Exportação

Finalmente, gravamos o arquivo no disco.

```java
        // Save the worksheet as a TXT file using the configured options
        workbook.save("YOUR_DIRECTORY/TableExported.txt", txtSaveOptions);
    }
}
```

Executar este programa cria `TableExported.txt`. Cada linha da tabela Excel original aparecerá agora como uma linha de valores separados por pipe, como:

```
Name|Quantity|Price|Total
Apple|10|0.50|5.00
Banana|5|0.30|1.50
```

Observe como a fórmula na coluna **Total** foi avaliada antes de ser escrita — graças a `setFormulaValueInCell(true)`. Essa é a essência de **export excel data as plain text** enquanto preserva os resultados calculados.

## Etapa 6: Verificar a Saída – Está Correta?

Abra o `TableExported.txt` gerado em qualquer editor de texto. Você deve ver:

- Uma linha por linha do Excel.
- Colunas separadas pelo caractere pipe que você definiu com `setCellValueSeparator`.
- Nenhuma vírgula ou tabulação extra, a menos que façam parte dos valores originais das células.
- Resultados das fórmulas, não as próprias fórmulas.

Se você encontrar caracteres inesperados, verifique novamente o separador escolhido. Alguns caracteres (como o pipe) são seguros para a maioria dos analisadores estilo CSV, mas se seus dados já contêm pipes, considere um delimitador diferente como `~` ou uma tabulação (`\t`).

## Dicas, Casos Limítrofes e Melhores Práticas – Exportar Dados Excel como Texto Simples

| Situação | O que fazer |
|-----------|------------|
| **Os dados já contêm o separador escolhido** | Mude para um caractere menos comum (`^`, `~`, ou caracteres Unicode não imprimíveis). |
| **Você precisa de codificação UTF‑8** |  |

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Save Excel as Text File with Custom Separator using Aspose.Cells](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Save Excel Text Custom Separator Aspose Cells Net](/cells/german/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Save Excel Text Custom Separator Aspose Cells Net](/cells/french/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}