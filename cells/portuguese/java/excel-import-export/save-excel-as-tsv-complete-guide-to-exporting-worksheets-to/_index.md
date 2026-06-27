---
category: general
date: 2026-06-27
description: Salve o Excel como TSV rapidamente usando Java. Aprenda como exportar
  a planilha para texto, exportar a planilha como texto simples e exportar a string
  de dados do Excel com Aspose.Cells.
draft: false
keywords:
- save excel as tsv
- export worksheet to text
- export sheet plain text
- export excel data string
language: pt
og_description: Salvar Excel como TSV usando Java. Este tutorial mostra como exportar
  a planilha para texto, exportar a planilha em texto simples e exportar a string
  de dados do Excel de forma eficiente.
og_title: Salvar Excel como TSV – Guia de Exportação Passo a Passo
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Save Excel as TSV quickly using Java. Learn how to export worksheet
    to text, export sheet plain text, and export Excel data string with Aspose.Cells.
  headline: Save Excel as TSV – Complete Guide to Exporting Worksheets to Text
  type: TechArticle
- description: Save Excel as TSV quickly using Java. Learn how to export worksheet
    to text, export sheet plain text, and export Excel data string with Aspose.Cells.
  name: Save Excel as TSV – Complete Guide to Exporting Worksheets to Text
  steps:
  - name: Pro tip
    text: If you’re dealing with password‑protected files, call `new Workbook("file.xlsx",
      new LoadOptions(LoadFormat.XLSX) {{ setPassword("yourPassword"); }})`.
  - name: 'Edge case: Custom delimiters'
    text: 'If your downstream system expects a pipe (`|`) instead of a tab, just change
      the delimiter:'
  - name: Pro tip
    text: 'After exporting, you can also capture the string directly:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel automation
title: Salvar Excel como TSV – Guia Completo para Exportar Planilhas para Texto
url: /pt/java/excel-import-export/save-excel-as-tsv-complete-guide-to-exporting-worksheets-to/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Salvar Excel como TSV – Guia Completo para Exportar Planilhas para Texto

Já precisou **salvar Excel como TSV** mas não sabia qual chamada de API usar? Você não está sozinho. Muitos desenvolvedores se deparam com dificuldades ao tentar transformar uma planilha em um arquivo delimitado por tabulação para processamento posterior. A boa notícia? Com algumas linhas de Java e Aspose.Cells você pode exportar uma planilha para texto, exportar planilha como texto simples e até exportar string de dados do Excel sem esforço.

Neste tutorial, percorreremos todo o fluxo de trabalho — desde o carregamento de uma pasta de trabalho até a configuração das opções de exportação e, finalmente, a gravação de um arquivo TSV no disco. Ao final, você será capaz de **salvar Excel como TSV** em qualquer projeto Java, seja manipulando uma única planilha ou processando dezenas de arquivos em lote.

## O Que Este Guia Cobre

* Carregar uma pasta de trabalho Excel do disco  
* Selecionar a planilha correta (ou iterar sobre várias)  
* Configurar `ExportTableOptions` para produzir saída em texto simples  
* Gravar os dados como um arquivo de valores separados por tabulação (TSV)  
* Dicas para lidar com grandes intervalos, diferentes delimitadores e caracteres Unicode  

Nenhuma ferramenta externa necessária — apenas Aspose.Cells para Java e um runtime Java 8+.

---

## Etapa 1: Configure Seu Projeto e Carregue a Pasta de Trabalho

Antes de mergulharmos no código, certifique-se de que você adicionou o JAR do Aspose.Cells ao classpath do seu projeto. Se estiver usando Maven, a dependência fica assim:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

Agora podemos carregar a pasta de trabalho:

```java
// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Quick sanity check – print the number of worksheets
System.out.println("Worksheets count: " + workbook.getWorksheets().getCount());
```

> **Por que isso importa:** Carregar o arquivo é o primeiro passo em qualquer fluxo de trabalho de **export Excel data string**. Se o arquivo não puder ser aberto, nada mais funcionará.

### Dica profissional
Se você estiver lidando com arquivos protegidos por senha, chame `new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setPassword("yourPassword"); }})`.

---

## Etapa 2: Escolha a Planilha Que Deseja Exportar

Você pode obter a primeira planilha, uma planilha por nome ou iterar sobre todas elas. Aqui está o caso mais simples — exportar a primeira planilha:

```java
// Step 2: Access the first worksheet (or any specific sheet)
Worksheet ws = workbook.getWorksheets().get(0);
System.out.println("Exporting sheet: " + ws.getName());
```

Se precisar **exportar worksheet to text** para cada planilha, envolva o código acima em um loop `for`:

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    // Export each sheet separately...
}
```

---

## Etapa 3: Crie e Configure as Opções de Exportação

O núcleo de **export sheet plain text** está em `ExportTableOptions`. Ao alternar algumas propriedades, transformamos o intervalo em uma string de texto simples com delimitador de tabulação:

```java
// Step 3: Create export options for the table
ExportTableOptions exportOptions = new ExportTableOptions();

// Step 4: Configure the options – export as plain text and use a tab delimiter
exportOptions.setExportAsString(true);   // Returns a string instead of binary Excel format
exportOptions.setDelimiter('\t');        // Tab character makes it TSV
```

> **Por que usar `setExportAsString(true)`?**  
> Ele indica ao Aspose.Cells que trate a saída como texto bruto, que é exatamente o que você precisa quando deseja **salvar Excel como TSV**. A alternativa seria uma exportação CSV ou HTML, nenhuma das quais fornece separação por tabulação limpa.

### Caso de borda: Delimitadores personalizados
Se o seu sistema downstream espera um pipe (`|`) em vez de uma tabulação, basta mudar o delimitador:

```java
exportOptions.setDelimiter('|');
```

---

## Etapa 4: Exporte o Intervalo Desejado para um Arquivo de Texto

Agora realmente gravamos o arquivo TSV. O método `exportTable` recebe três argumentos: o intervalo de células, o caminho de saída e o `ExportTableOptions` que acabamos de configurar.

```java
// Step 5: Export the range A1:D20 to a text file using the configured options
ws.getCells().exportTable("A1:D20", "YOUR_DIRECTORY/out.tsv", exportOptions);
System.out.println("TSV file created successfully!");
```

Se quiser exportar o intervalo *inteiro* usado, substitua `"A1:D20"` por `ws.getCells().getMaxDisplayRange()`:

```java
String fullRange = ws.getCells().getMaxDisplayRange();
ws.getCells().exportTable(fullRange, "out.tsv", exportOptions);
```

### Dica profissional
Após a exportação, você também pode capturar a string diretamente:

```java
String tsvContent = ws.getCells().exportTable("A1:D20", exportOptions);
System.out.println(tsvContent); // Handy for debugging or sending over a network
```

Isso fornece a **export Excel data string** bruta sem tocar no sistema de arquivos.

---

## Etapa 5: Lidando com Arquivos Grandes e Dicas de Performance

Ao lidar com planilhas massivas (centenas de milhares de linhas), considere estas otimizações:

| Problema | Solução |
|----------|----------|
| Pressão de memória | Use `WorkbookFactory.create(InputStream)` para transmitir o arquivo ao invés de carregá-lo completamente. |
| I/O lento | Escreva em um `BufferedWriter` ou use NIO `Files.newBufferedWriter`. |
| Caracteres Unicode | Garanta que o arquivo de saída seja escrito com UTF‑8: `exportTable(..., "out.tsv", exportOptions, Encoding.getUTF8())`. |

Abaixo está um trecho que combina streaming e codificação UTF‑8:

```java
try (InputStream is = Files.newInputStream(Paths.get("input.xlsx"));
     BufferedWriter writer = Files.newBufferedWriter(Paths.get("out.tsv"), StandardCharsets.UTF_8)) {

    Workbook wb = new Workbook(is);
    Worksheet sheet = wb.getWorksheets().get(0);
    ExportTableOptions opts = new ExportTableOptions();
    opts.setExportAsString(true);
    opts.setDelimiter('\t');

    String tsv = sheet.getCells().exportTable("A1:D20", opts);
    writer.write(tsv);
}
```

---

## Armadilhas Comuns e Como Evitá‑las

1. **Esqueceu de definir `setExportAsString(true)`.**  
   Sem essa flag, o Aspose gerará um arquivo Excel binário, comprometendo seu objetivo de **export worksheet to text**.

2. **Usando o delimitador errado.**  
   Uma vírgula em vez de uma tabulação resultará em CSV, não TSV. Verifique `setDelimiter('\t')`.

3. **Sintaxe de intervalo incorreta.**  
   `"A1:D20"` está correta, mas `"A1:D20:"` (dois pontos extras) lançará um `IllegalArgumentException`.

4. **Permissões de arquivo.**  
   Certifique‑se de que o diretório de destino seja gravável. No Linux, `chmod 755` costuma resolver o problema.

---

## Concluindo – Exemplo Completo Funcional

Aqui está o programa completo, pronto‑para‑executar, que demonstra **salvar Excel como TSV** do início ao fim:

```java
import com.aspose.cells.*;

import java.io.*;
import java.nio.charset.StandardCharsets;
import java.nio.file.*;

public class ExcelToTsv {
    public static void main(String[] args) throws Exception {
        // Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Choose worksheet (first sheet in this case)
        Worksheet ws = workbook.getWorksheets().get(0);

        // Set up export options for plain‑text TSV output
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);   // Export as string
        exportOptions.setDelimiter('\t');        // Tab delimiter for TSV

        // Define the range you want to export
        String range = "A1:D20"; // Change as needed or use ws.getCells().getMaxDisplayRange()

        // Export to a file
        ws.getCells().exportTable(range, "YOUR_DIRECTORY/out.tsv", exportOptions);
        System.out.println("Successfully saved Excel as TSV at YOUR_DIRECTORY/out.tsv");
    }
}
```

Executar este programa gera um arquivo separado por tabulação (`out.tsv`) que qualquer sistema downstream — seja um carregador de banco de dados, um script Unix `awk` ou um visualizador simples de planilhas — pode consumir.

---

## Conclusão

Cobrimos tudo o que você precisa para **salvar Excel como TSV** usando Java e Aspose.Cells. Desde o carregamento da pasta de trabalho, seleção da planilha correta, configuração de `ExportTableOptions` e, finalmente, gravação do arquivo, você agora possui um padrão sólido e pronto para produção para os cenários **export worksheet to text**, **export sheet plain text** e **export Excel data string**.

O que vem a seguir? Experimente exportar múltiplos intervalos, trocar delimitadores dinamicamente ou transmitir a saída diretamente para uma resposta HTTP para downloads baseados na web. Os mesmos princípios se aplicam, e você descobrirá que manipular dados do Excel em texto simples é muito fácil quando os fundamentos estão estabelecidos.

Tem perguntas ou encontrou um caso de borda estranho? Deixe um comentário abaixo, e feliz codificação!

## O Que Você Deve Aprender a Seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como Exportar Dados do Excel para HTML5 Usando Aspose.Cells Java](/cells/english/java/import-export/aspose-cells-java-export-excel-html5/)
- [Exportação de Dados do Excel sem Esforço usando Aspose.Cells para Java](/cells/english/java/import-export/aspose-cells-java-excel-data-export/)
- [Como Exportar uma Planilha Excel para PNG Usando Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}