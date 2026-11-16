---
category: general
date: 2026-11-16
description: Como copiar células entre pastas de trabalho do Excel em Java – carregar
  uma pasta de trabalho, copiar intervalo entre pastas de trabalho (incluindo uma
  tabela dinâmica) e salvar o arquivo da pasta de trabalho.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy cells
- copy range between workbooks
- copy pivot table workbook
- save workbook file
- load excel workbook java
language: pt
lastmod: 2026-11-16
og_description: Como copiar células entre pastas de trabalho do Excel em Java. Aprenda
  a carregar uma pasta de trabalho do Excel, copiar um intervalo (incluindo uma tabela
  dinâmica) entre pastas de trabalho e salvar o arquivo da pasta de trabalho.
og_image_alt: Screenshot of Java code copying a cell range from one Excel workbook
  to another
og_title: Como copiar células entre pastas de trabalho do Excel em Java – guia completo
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  headline: How to copy cells between Excel workbooks in Java
  type: TechArticle
- description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  name: How to copy cells between Excel workbooks in Java
  steps:
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Define the range that includes the pivot table
    text: '```java // Define the cell range that you want to copy. // Adjust "A1:G20"
      to match the area that contains your data/pivot table. Range srcRange = srcWs.getCells().createRange("A1:G20");
      ```'
  - name: Create the destination workbook
    text: '```java // Create a new, empty workbook that will receive the copied range.
      Workbook destWb = new Workbook(); // defaults to a single empty sheet Worksheet
      destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range to the destination workbook
    text: '```java // Copy the source range to cell A1 of the destination worksheet.
      destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1")); ```'
  - name: Save the destination workbook
    text: '```java // Save the new workbook to disk. destWb.save("YOUR_DIRECTORY/dest.xlsx");
      } } ```'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Workbook manipulation
title: Como copiar células entre pastas de trabalho do Excel em Java
url: /pt/java/workbook-operations/how-to-copy-cells-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como copiar células entre pastas de trabalho do Excel em Java

Se você precisar **copiar células** de uma pasta de trabalho do Excel para outra usando Java, este guia mostra uma maneira confiável de fazer isso. Você aprenderá como **load Excel workbook Java**, copiar um intervalo que pode conter uma tabela dinâmica e, finalmente, **save workbook file** com os dados copiados.

Este tutorial cobre:

* Carregar uma pasta de trabalho de origem e selecionar uma planilha.  
* Definir o intervalo exato que você deseja mover (incluindo uma tabela dinâmica).  
* Criar uma pasta de trabalho de destino e copiar o intervalo.  
* Salvar o arquivo de destino.  

O exemplo usa a biblioteca Aspose.Cells for Java, que trabalha com arquivos Excel sem exigir Microsoft Office. O código funciona em Java 8+ e em qualquer IDE moderna (IntelliJ IDEA, Eclipse, VS Code, etc.).

---

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

| Requisito | Motivo |
|-------------|--------|
| Java Development Kit (JDK) 8 ou mais recente | Necessário para compilar e executar o código. |
| Maven ou Gradle | Simplifica a adição da dependência Aspose.Cells. |
| Aspose.Cells for Java library (última versão) | Fornece as classes `Workbook`, `Worksheet` e `Range` usadas no exemplo. |
| Dois arquivos Excel (`source.xlsx` e uma pasta vazia para `dest.xlsx`) | O arquivo de origem deve conter os dados e, opcionalmente, uma tabela dinâmica que você deseja copiar. |

Adicione a dependência Aspose.Cells ao seu `pom.xml` (Maven) ou `build.gradle` (Gradle). Exemplo para Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

---

## Como copiar células com Aspose.Cells

Os passos a seguir orientam você por todo o processo. Cada passo inclui o código Java, uma explicação do **por quê** o passo é importante e uma dica para evitar armadilhas comuns.

### Etapa 1: Carregar a pasta de trabalho de origem

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source Excel file (replace with your actual path)
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Get the first worksheet (index 0)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**Por quê?**  
`Workbook` representa todo o arquivo Excel. Carregá‑lo dá acesso a todas as planilhas, células e objetos como tabelas dinâmicas. Usar a primeira planilha é comum, mas você pode selecionar qualquer planilha pelo nome (`srcWb.getWorksheets().get("Sheet2")`).

**Dica profissional:**  
Se o arquivo de origem for grande, considere carregá‑lo em modo *memory‑efficient*: `new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setMemorySetting(MemorySetting.MEMORY_PREFERENCE); }});`

### Etapa 2: Definir o intervalo que inclui a tabela dinâmica

```java
        // Define the cell range that you want to copy.
        // Adjust "A1:G20" to match the area that contains your data/pivot table.
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**Por quê?**  
Um objeto `Range` abstrai um bloco retangular de células. Ao especificar `"A1:G20"` você indica ao Aspose.Cells exatamente quais células—including any embedded pivot table—copiar. A biblioteca copia automaticamente os dados subjacentes, estilos e definições da tabela dinâmica.

**Caso especial:**  
Se a tabela dinâmica se estender além do intervalo definido, amplie o endereço (por exemplo, `"A1:Z100"`). Você também pode usar `srcWs.getCells().getMaxDataColumn()` e `getMaxDataRow()` para calcular a área usada dinamicamente.

### Etapa 3: Criar a pasta de trabalho de destino

```java
        // Create a new, empty workbook that will receive the copied range.
        Workbook destWb = new Workbook();               // defaults to a single empty sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**Por quê?**  
Uma nova pasta de trabalho garante que nenhuma formatação indesejada ou planilhas ocultas interfiram no conteúdo copiado. A pasta de trabalho padrão já contém uma planilha, que usaremos como destino.

### Etapa 4: Copiar o intervalo para a pasta de trabalho de destino

```java
        // Copy the source range to cell A1 of the destination worksheet.
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));
```

**Por quê?**  
`copyRange` lida com todos os atributos das células: valores, fórmulas, formatação e até caches de tabelas dinâmicas. Ao copiar para `"A1"` você posiciona o intervalo no canto superior‑esquerdo da planilha de destino, preservando o layout original.

**Pergunta comum:** *A tabela dinâmica continuará funcional?*  
Sim. Aspose.Cells copia a definição da tabela dinâmica e seu cache, de modo que a tabela funciona exatamente como na pasta de trabalho de origem.

### Etapa 5: Salvar a pasta de trabalho de destino

```java
        // Save the new workbook to disk.
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Por quê?**  
Chamar `save` grava a pasta de trabalho em memória em um arquivo físico `.xlsx`. Você também pode salvar em outros formatos (`.xls`, `.csv`, `.pdf`) alterando a extensão do arquivo ou usando `SaveOptions`.

**Dica:**  
Se precisar transmitir o arquivo como resposta web, use `destWb.save(OutputStream, SaveFormat.XLSX);` em vez de um caminho de arquivo.

---

## Copiar intervalo entre pastas de trabalho – código‑fonte completo

Abaixo está a classe Java completa, pronta para execução. Substitua `YOUR_DIRECTORY` pelo caminho real na sua máquina.

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Define the range that includes the data and pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Create a new destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Copy the defined range to the destination workbook
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Resultado esperado:**  
`dest.xlsx` contém uma réplica exata do intervalo `A1:G20` de `source.xlsx`. Se o intervalo de origem continha uma tabela dinâmica, o arquivo de destino mostra a mesma tabela dinâmica com sua fonte de dados corretamente vinculada às células copiadas.

Você pode abrir `dest.xlsx` no Excel, LibreOffice ou qualquer visualizador que suporte `.xlsx` para verificar que os valores, formatações e funcionalidades da tabela dinâmica foram preservados.

---

## Copiar pasta de trabalho de tabela dinâmica – o que você deve saber

* **O cache da tabela dinâmica é copiado automaticamente.** A biblioteca transfere o cache subjacente, de modo que a tabela não precisa ser atualizada manualmente.
* **Fontes de dados externas não são transferidas.** Se a tabela dinâmica obtém dados de um banco externo, você deve garantir que a pasta de trabalho de destino possa acessar a mesma fonte ou recriar o cache localmente.
* **Tabelas dinâmicas grandes podem aumentar o uso de memória.** Para pastas de trabalho muito grandes, considere aumentar o heap da JVM (`-Xmx2g`) para evitar `OutOfMemoryError`.

---

## Salvar arquivo de pasta de trabalho em diferentes formatos

Aspose.Cells permite salvar o resultado em muitos formatos sem alterações de código:

```java
// Save as XLS (Excel 97-2003)
destWb.save("dest.xls");

// Save as CSV (first worksheet only)
destWb.save("dest.csv");

// Save as PDF (visual representation)
destWb.save("dest.pdf");
```

Escolha o formato que corresponde ao seu processo downstream. A mesma lógica `copyRange` funciona independentemente do formato final.

---

## Carregar Excel workbook Java – dicas adicionais

* **Carregando arquivos criptografados:** Use `LoadOptions` com uma senha:  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setPassword("myPassword");
  Workbook wb = new Workbook("encrypted.xlsx", opt);
  ```
* **Lendo apenas planilhas específicas:**  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setLoadDataOnly(true); // faster if you only need values
  Workbook wb = new Workbook("file.xlsx", opt);
  ```

Essas opções podem acelerar a etapa **load excel workbook java**, especialmente para arquivos grandes.

---

## Conclusão

Agora você sabe **como copiar células** entre pastas de trabalho do Excel em Java, como **copiar intervalo entre pastas de trabalho** que contém uma **tabela dinâmica**, e como **save workbook file** no formato que precisar. Seguindo os passos acima, você pode integrar a manipulação de dados Excel em qualquer aplicação Java—seja construindo um motor de relatórios, um pipeline ETL ou um utilitário simples de conversão de arquivos.

**Próximas etapas** que você pode explorar:

* Use **copy range between workbooks** para mesclar múltiplos relatórios em

## O que você deve aprender a seguir?


Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Salvar Nova Pasta de Trabalho em Java – Tutorial de Copiar Intervalo Entre Pastas de Trabalho](/cells/english/java/workbook-operations/save-new-workbook-in-java-copy-range-between-workbooks-tutor/)
- [Como copiar tabelas dinâmicas entre pastas de trabalho do Excel em Java](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/)
- [Como copiar intervalo em Java – Copiar Tabela Dinâmica com Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}