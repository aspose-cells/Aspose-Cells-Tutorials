---
category: general
date: 2026-07-14
description: Copiar tabela dinâmica entre pastas de trabalho usando Java. Aprenda
  como copiar a tabela dinâmica, copiar intervalo do Excel e exportar a tabela dinâmica
  em minutos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- copy range between workbooks
- export pivot table
language: pt
lastmod: 2026-07-14
og_description: Copie tabela dinâmica em Java rapidamente. Este guia mostra como copiar
  a tabela dinâmica, copiar intervalo do Excel e exportar a tabela dinâmica com Aspose.Cells.
og_image_alt: Diagram illustrating copy pivot table process between two Excel workbooks
og_title: Copiar Tabela Dinâmica Entre Pastas de Trabalho – Tutorial de Automação
  Java
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Copy pivot table between workbooks using Java. Learn how to copy pivot,
    copy Excel range, and export pivot table in minutes.
  headline: Copy Pivot Table Between Workbooks – Step‑by‑Step Java Guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Copiar Tabela Dinâmica entre Pastas de Trabalho – Guia Java Passo a Passo
url: /pt/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copiar Tabela Dinâmica Entre Pastas de Trabalho – Tutorial Completo em Java

Já precisou **copiar uma tabela dinâmica** de uma pasta de trabalho para outra e se perguntou por que os truques habituais de copiar‑colar acabam quebrando o layout? Você não está sozinho. Em muitos pipelines de relatórios a tabela dinâmica vive em um arquivo mestre, mas processos subsequentes exigem uma cópia leve.  

Neste guia vamos percorrer uma maneira limpa e programática de duplicar uma tabela dinâmica — sem necessidade de ajustes manuais. Ao final você saberá **como copiar uma tabela dinâmica**, como **copiar intervalo do Excel** com segurança e até como **exportar tabela dinâmica** para um novo arquivo, tudo com Aspose.Cells para Java.

## O que você vai construir

- Carregar uma pasta de trabalho fonte que já contém uma tabela dinâmica.  
- Criar (ou abrir) uma pasta de trabalho de destino.  
- Definir o intervalo exato que contém a tabela dinâmica.  
- Copiar esse intervalo — incluindo a definição da tabela dinâmica — para a nova pasta de trabalho.  
- Salvar o resultado para que outros aplicativos possam abri‑lo sem perder nenhum cálculo.

Sem ferramentas externas, sem VBA, apenas código Java puro que você pode inserir em qualquer projeto Maven ou Gradle.

## Pré‑requisitos

- Java 17 ou superior (o código funciona em Java 8+, mas JDKs mais recentes oferecem melhor desempenho).  
- Aspose.Cells para Java 23.9 ou mais recente – adicione a dependência do Maven Central.  
- Dois arquivos Excel: `SourceWithPivot.xlsx` (contém a tabela dinâmica) e um placeholder vazio para a cópia.  

Se você é novo no Aspose.Cells, a biblioteca abstrai os detalhes de baixo nível do OOXML, permitindo que você trate planilhas como objetos Java normais.

## Etapa 1: Configurar seu projeto

Primeiro, adicione o artefato Aspose.Cells ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust if you use a different JDK -->
</dependency>
```

Ou, para Gradle:

```gradle
implementation 'com.aspose:aspose-cells:23.9:jdk17'
```

> **Dica de especialista:** Se você estiver usando uma IDE como IntelliJ, deixe‑a importar a biblioteca automaticamente; isso economiza muito digitação.

## Etapa 2: Carregar a pasta de trabalho fonte

Precisamos de uma instância `Workbook` que aponte para o arquivo que contém a tabela dinâmica. O construtor lê todo o arquivo para a memória, permitindo que você trabalhe offline.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {

        // Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

Por que carregá‑la primeiro? Porque o cache da tabela dinâmica, a lista de campos e o layout são armazenados dentro da planilha. Trazer a pasta de trabalho para a memória garante que copiemos a *definição* e não apenas os valores renderizados.

## Etapa 3: Criar ou abrir a pasta de trabalho de destino

Você tem duas opções: iniciar com uma pasta de trabalho totalmente nova ou abrir um modelo existente. Aqui criaremos uma em branco, que é o cenário mais comum quando se precisa de uma cópia limpa.

```java
        // Create an empty destination workbook (or open an existing one)
        Workbook destinationWorkbook = new Workbook(); // blank workbook with a default sheet
```

Se mais tarde decidir copiar para uma planilha específica, basta substituir `getWorksheets().get(0)` pelo índice ou nome apropriado.

## Etapa 4: Definir o intervalo exato que contém a tabela dinâmica

Uma tabela dinâmica normalmente ocupa um bloco retangular. A abordagem mais segura é especificar explicitamente as células superior‑esquerda e inferior‑direita. No nosso exemplo a tabela dinâmica vai de **A1** a **H30**.

```java
        // Define the range in the source sheet that includes the pivot table
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)                     // first worksheet
                                          .getCells()
                                          .createRange("A1:H30");
```

> **Por que não usar `copyRows`?**  
> `copyRows` copia apenas os valores brutos das células, descartando o cache subjacente da tabela dinâmica. Ao copiar todo o intervalo, o Aspose.Cells preserva os metadados da tabela dinâmica, permitindo que o destino mantenha a interatividade completa.

## Etapa 5: Copiar o intervalo (incluindo a tabela dinâmica) para o destino

Agora a mágica acontece. O método `copy` clona tudo — valores, fórmulas, formatos e o próprio objeto da tabela dinâmica — para o local de destino.

```java
        // Copy the defined range (with the pivot table) to the destination sheet
        sourceRange.copy(destinationWorkbook.getWorksheets()
                                            .get(0)               // destination sheet
                                            .getCells()
                                            .createRange("A1"));
```

Se precisar colar em uma célula diferente, basta mudar `"A1"` para `"C5"` ou qualquer endereço que desejar. O método ajusta automaticamente as referências internas para que a tabela dinâmica continue funcionando.

## Etapa 6: Salvar a pasta de trabalho de destino

Por fim, grave a nova pasta de trabalho no disco. O arquivo resultante pode ser aberto no Excel, LibreOffice ou qualquer outro visualizador de planilhas, e a tabela dinâmica se comportará exatamente como na origem.

```java
        // Save the destination workbook with the copied pivot table
        destinationWorkbook.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

### Resultado esperado

- `CopyPivotResult.xlsx` abre com uma tabela dinâmica totalmente funcional, idêntica à original.  
- Todos os slicers, filtros e campos calculados permanecem intactos.  
- Nenhuma perda de dados — os valores são calculados sob demanda ao atualizar a tabela dinâmica.

## Variações comuns e casos de borda

| Situação | O que ajustar |
|-----------|----------------|
| **Copiar para uma pasta de trabalho existente** | Carregue a pasta de trabalho de destino em vez de criar uma nova: `new Workbook("ExistingFile.xlsx")`. |
| **A tabela dinâmica tem tamanho desconhecido** | Use `Worksheet.getPivotTables().get(0).getPivotTableRange()` para obter o endereço exato programaticamente. |
| **Preservar conexões de dados** | Após copiar, chame `destinationWorkbook.getWorksheets().get(0).getPivotTables().get(0).setRefreshOnLoad(true);` para manter os links externos ativos. |
| **Exportar tabela dinâmica como CSV** | Depois de copiar, você pode chamar `destinationWorkbook.save("PivotExport.csv", SaveFormat.CSV);` – isso achata apenas os valores da tabela dinâmica. |

> **Atenção:** Quando as pastas de trabalho fonte e destino usam configurações de localidade diferentes, os formatos numéricos podem mudar. Defina explicitamente o `setLocale` da pasta de trabalho se precisar de consistência.

## Exemplo completo em funcionamento (todos os imports incluídos)

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load source workbook containing the pivot
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

        // 2️⃣ Create (or open) destination workbook
        Workbook destinationWorkbook = new Workbook(); // blank workbook

        // 3️⃣ Identify the range that encloses the pivot table
        //    If you don't know the range, you can retrieve it via:
        //    PivotTable pt = sourceWorkbook.getWorksheets().get(0).getPivotTables().get(0);
        //    String address = pt.getPivotTableRange().getRefersTo();
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)
                                          .getCells()
                                          .createRange("A1:H30");

        // 4️⃣ Copy the range (pivot included) to the destination sheet
        sourceRange.copy(destinationWorkbook.getWorksheets()
                                            .get(0)
                                            .getCells()
                                            .createRange("A1"));

        // 5️⃣ Persist the result
        destinationWorkbook.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");

        System.out.println("Pivot table copied successfully!");
    }
}
```

Execute o programa, abra `CopyPivotResult.xlsx` e você verá a mesma tabela dinâmica com a qual começou — pronta para análises adicionais ou distribuição.

## Recapitulação

Acabamos de demonstrar **como copiar uma tabela dinâmica** de uma pasta de trabalho para outra usando Aspose.Cells para Java. As etapas cobriram o carregamento da fonte, a definição do **intervalo de cópia do Excel**, a execução da cópia e, finalmente, a **exportação da tabela dinâmica** para um novo arquivo. Ao manipular o intervalo em vez de células individuais, garantimos que o cache interno da tabela dinâmica viaje junto, mantendo o relatório dinâmico.

## O que explorar a seguir

- **Automatizar atualização**: Agende a operação de cópia com um job Quartz para que seus arquivos downstream permaneçam atualizados.  
- **Copiar múltiplas tabelas dinâmicas**: Percorra `sourceWorkbook.getWorksheets().get(0).getPivotTables()` e copie cada uma para planilhas separadas.  
- **Aplicar estilos**: Use objetos `Style` para harmonizar fontes e cores na pasta de trabalho de destino.  

Se você tem dúvidas sobre como lidar com pastas de trabalho grandes ou preservar fontes de dados externas, deixe um comentário abaixo. Boa codificação e aproveite a liberdade da automação programática do Excel!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Manipulação de Tabela Dinâmica do Excel com Aspose.Cells Java&#58; Um Guia Abrangente](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [Como Atualizar a Fonte da Tabela Dinâmica do Excel com Aspose.Cells para Java&#58; Um Guia Abrangente](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Automatizar Estilização e Salvamento de Tabela Dinâmica do Excel com Aspose.Cells para Java&#58; Um Guia Abrangente](/cells/english/java/data-analysis/excel-pivot-table-styling-saving-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}