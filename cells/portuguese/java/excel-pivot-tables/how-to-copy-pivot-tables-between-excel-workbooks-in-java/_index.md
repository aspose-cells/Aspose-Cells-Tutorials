---
category: general
date: 2026-10-01
description: Aprenda a copiar tabelas dinâmicas entre pastas de trabalho do Excel
  usando Java. Este guia passo a passo também mostra como copiar intervalos entre
  pastas de trabalho e duplicar intervalos do Excel com segurança.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range between workbooks
- how to copy excel
- duplicate excel range
- copy range to workbook
language: pt
lastmod: 2026-10-01
og_description: Como copiar tabelas dinâmicas entre pastas de trabalho do Excel usando
  Java. Siga este guia para copiar intervalos para a pasta de trabalho, duplicar intervalos
  do Excel e preservar os dados da tabela dinâmica.
og_image_alt: Screenshot of Java code that copies a pivot table from one Excel workbook
  to another
og_title: Como copiar tabelas dinâmicas entre pastas de trabalho do Excel em Java
  – guia completo
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to copy pivot tables between Excel workbooks using Java.
    This step‑by‑step guide also shows how to copy range between workbooks and duplicate
    Excel ranges safely.
  headline: How to copy pivot tables between Excel workbooks in Java
  type: TechArticle
- description: Learn how to copy pivot tables between Excel workbooks using Java.
    This step‑by‑step guide also shows how to copy range between workbooks and duplicate
    Excel ranges safely.
  name: How to copy pivot tables between Excel workbooks in Java
  steps:
  - name: Expected output
    text: '* Console: `Pivot table copied successfully.` * `destination.xlsx` opens
      in Excel with a pivot table identical to the one in `source.xlsx`. Refreshing
      the pivot shows the same data source, proving that **how to copy pivot** works
      as intended.'
  - name: Copying multiple worksheets
    text: If your project requires copying several sheets, loop through the workbook’s
      worksheets and repeat steps 2‑4 for each sheet. The pivot in each sheet will
      be preserved independently.
  - name: Preserving external data connections
    text: Pivot tables that rely on external data sources keep the connection string
      after copying. However, the destination file must have access to the same data
      source. Verify the connection by opening the pivot and checking the **Data**
      tab.
  - name: Dealing with merged cells
    text: If the source range contains merged cells, Aspose.Cells copies the merge
      layout automatically. Still, validate the result if the destination workbook
      uses a different default column width.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- Pivot table
- Data manipulation
title: Como copiar tabelas dinâmicas entre pastas de trabalho do Excel em Java
url: /pt/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como copiar tabelas dinâmicas entre pastas de trabalho do Excel em Java

Se você precisa **how to copy pivot** tabelas de um arquivo Excel para outro, este guia oferece uma solução pronta‑para‑executar. Ao final das duas primeiras frases, você saberá exatamente quais chamadas de API preservam a definição da tabela dinâmica ao copiar o intervalo de dados.

Você também aprenderá como **copy range between workbooks**, **duplicate Excel range** objetos, e como copiar com segurança **copy range to workbook** sem perder fórmulas ou formatação. Nenhum script externo é necessário—apenas um único projeto Java que usa Aspose.Cells for Java.

## Pré-requisitos

* Java Development Kit 17 ou posterior.
* Maven ou Gradle para gerenciar dependências.
* Uma licença válida do Aspose.Cells for Java (a avaliação gratuita funciona para testes).
* Dois arquivos Excel: `source.xlsx` (contém a tabela dinâmica) e um `destination.xlsx` vazio (ou deixe o código criá‑lo).

## Etapa 1: Configurar o projeto Maven

Crie um `pom.xml` que inclua o Aspose.Cells. Essa dependência fornece as classes `Workbook`, `Worksheet` e `Range` usadas no exemplo.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>excel-pivot-copy</artifactId>
    <version>1.0.0</version>
    <properties>
        <java.version>17</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>24.10</version> <!-- latest at time of writing -->
        </dependency>
    </dependencies>
</project>
```

> **Pro tip:** Mantenha a versão do Aspose.Cells atualizada; lançamentos mais recentes adicionam melhor suporte para estruturas complexas de cache de tabelas dinâmicas.

## Etapa 2: Carregar a pasta de trabalho fonte que contém a tabela dinâmica

O primeiro bloco de código demonstra **how to copy excel** dados ao carregar o arquivo fonte. O construtor `Workbook` lê todo o arquivo na memória, preservando todos os objetos da planilha, incluindo tabelas dinâmicas.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook containing the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Access the first worksheet (index 0) where the pivot resides
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

*Por que isso importa:* Aspose.Cells armazena tabelas dinâmicas como parte do modelo interno da planilha. Carregar a pasta de trabalho garante que o cache da tabela dinâmica esteja disponível para cópia posterior.

## Etapa 3: Definir o intervalo que inclui a tabela dinâmica

Uma tabela dinâmica pode abranger várias linhas e colunas. Na maioria dos casos, você pode copiar todo o intervalo usado da planilha. O método `createRange` cria um objeto `Range` que a operação de cópia manipulará.

```java
        // Define the range to copy – includes the pivot table and its source data
        // Adjust the address if your pivot occupies a different block
        Range srcRange = srcWs.getCells().createRange("A1:H20");
```

Se a tabela dinâmica se estender além de `H20`, basta alterar a string de endereço. Esta etapa é o núcleo do tratamento de **duplicate excel range**; o objeto range conhece fórmulas, estilos e linhas ocultas.

## Etapa 4: Criar uma nova pasta de trabalho que receberá o intervalo copiado

Você pode começar com uma pasta de trabalho em branco ou carregar um arquivo de destino existente. Aqui criamos uma nova pasta de trabalho, que é a maneira mais limpa de **copy range to workbook**.

```java
        // Create a new workbook for the destination
        Workbook destWb = new Workbook(); // starts with one default sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

> **Note:** Se precisar copiar a tabela dinâmica para um nome de planilha específico, renomeie `destWs` com `destWs.setName("Report")` antes de colar.

## Etapa 5: Copiar o intervalo – Aspose.Cells preserva automaticamente a tabela dinâmica

O método `copy` transfere tudo dentro do intervalo fonte, incluindo a definição da tabela dinâmica, o cache e a formatação. Nenhum código extra é necessário para manter a tabela dinâmica funcional.

```java
        // Copy the range to the destination worksheet; pivot tables are preserved automatically
        srcRange.copy(destWs.getCells().createRange("A1"));
```

*Por que funciona:* Aspose.Cells trata a tabela dinâmica como uma coleção de células ocultas e metadados anexados ao intervalo. Quando você chama `copy`, a biblioteca replica esses metadados na pasta de trabalho de destino.

## Etapa 6: Salvar a pasta de trabalho de destino

Finalmente, grave o resultado no disco. O arquivo salvo contém uma tabela dinâmica idêntica que você pode atualizar ou modificar como a original.

```java
        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");

        System.out.println("Pivot table copied successfully.");
    }
}
```

Executar o programa exibe uma confirmação e produz `destination.xlsx` com uma tabela dinâmica totalmente funcional.

## Exemplo completo e executável

Juntando todas as etapas, a classe Java completa fica assim:

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load source workbook with pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // 2️⃣ Define the range that contains the pivot and its source data
        Range srcRange = srcWs.getCells().createRange("A1:H20");

        // 3️⃣ Prepare destination workbook (blank by default)
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // 4️⃣ Copy range – pivot table is kept intact
        srcRange.copy(destWs.getCells().createRange("A1"));

        // 5️⃣ Save the new file
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

### Saída esperada

* Console: `Pivot table copied successfully.`
* `destination.xlsx` abre no Excel com uma tabela dinâmica idêntica à de `source.xlsx`. Atualizar a tabela dinâmica mostra a mesma fonte de dados, provando que **how to copy pivot** funciona como esperado.

## Lidando com variações comuns

### Copiando várias planilhas

Se seu projeto requer copiar várias planilhas, faça um loop pelas planilhas da pasta de trabalho e repita as etapas 2‑4 para cada planilha. A tabela dinâmica em cada planilha será preservada independentemente.

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet src = srcWb.getWorksheets().get(i);
    Worksheet dest = destWb.getWorksheets().add();
    src.getCells().copy(dest.getCells());
}
```

### Preservando conexões de dados externas

Tabelas dinâmicas que dependem de fontes de dados externas mantêm a string de conexão após a cópia. Contudo, o arquivo de destino deve ter acesso à mesma fonte de dados. Verifique a conexão abrindo a tabela dinâmica e conferindo a aba **Data**.

### Lidando com células mescladas

Se o intervalo fonte contém células mescladas, Aspose.Cells copia o layout de mesclagem automaticamente. Ainda assim, valide o resultado se a pasta de trabalho de destino usar uma largura de coluna padrão diferente.

## Melhores práticas para cópia confiável

| Prática | Motivo |
|----------|--------|
| Use o intervalo usado exato (`srcWs.getCells().getMaxDisplayRange()`) em vez de um endereço codificado | Garante que toda a tabela dinâmica e seus dados de origem sejam incluídos. |
| Aplique uma licença antes de operações pesadas | Prevém a marca d'água de avaliação e melhora o desempenho. |
| Atualize a tabela dinâmica após copiar (`pivotTable.refresh()`) se os dados de origem foram alterados | Garante que o destino reflita os valores mais recentes. |
| Escreva testes unitários que abram a pasta de trabalho de destino e verifiquem que `pivotTable.getPivotFields().size()` corresponde ao da origem | Detecta perda acidental de campos durante futuras alterações de código. |

## Conclusão

Agora você sabe **how to copy pivot** tabelas entre pastas de trabalho do Excel em Java, bem como como **copy range between workbooks**, **duplicate excel range** e **copy range to workbook** preservando toda a formatação e fórmulas. O exemplo usa Aspose.Cells, que abstrai o manuseio XML de baixo nível exigido pelo OpenXML SDK.

Em seguida, explore tópicos relacionados como **updating pivot cache programmatically**, **exporting pivot data to CSV**, ou **creating pivot tables from scratch**. Cada um desses se baseia nos mesmos conceitos demonstrados aqui.

Feliz codificação, e sinta-se à vontade para experimentar intervalos maiores, múltiplas tabelas dinâmicas ou estilos personalizados – o mesmo padrão se aplica a todos os cenários.

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Copy Multiple Columns in Excel Using Aspose.Cells Java: A Complete Guide](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}