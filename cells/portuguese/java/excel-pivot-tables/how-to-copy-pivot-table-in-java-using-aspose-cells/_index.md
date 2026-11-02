---
category: general
date: 2026-07-06
description: Como copiar tabela dinâmica em Java com Aspose.Cells – guia passo a passo
  para duplicar tabelas dinâmicas do Excel programaticamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- duplicate excel pivot
language: pt
lastmod: 2026-07-06
og_description: Como copiar tabela dinâmica em Java usando Aspose.Cells permite duplicar
  tabelas dinâmicas do Excel de forma rápida e confiável.
og_image_alt: Screenshot of Java code copying an Excel pivot table with Aspose.Cells
og_title: Como copiar tabela dinâmica em Java – Guia completo do Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-07-06'
  description: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
    to duplicate Excel pivot tables programmatically.
  headline: How to copy pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
title: Como copiar tabela dinâmica em Java usando Aspose.Cells
url: /pt/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como copiar tabelas dinâmicas em Java usando Aspose.Cells

Já se perguntou **como copiar pivot** tables dentro de um arquivo Excel sem abrir a pasta de trabalho manualmente? Você não está sozinho. Em muitos pipelines de relatórios você precisa **duplicar Excel pivot** tables on the fly—talvez para criar um snapshot, mover para uma nova planilha ou gerar um template para usuários downstream.

Neste tutorial vamos percorrer um exemplo completo e executável que demonstra exatamente isso. Usando a biblioteca Aspose.Cells for Java vamos carregar uma workbook, localizar o intervalo pivot de origem, copiá‑lo para um novo local e salvar o resultado. Sem referências vagas, apenas uma solução concreta que você pode inserir no seu projeto hoje.

---

## Pré-requisitos

* **Java Development Kit (JDK) 8+** – o código compila com qualquer JDK recente.  
* **Aspose.Cells for Java** versão 25.11 ou mais nova – o método `Range.copy` que suporta tabelas dinâmicas foi introduzido nesta versão.  
* Um arquivo **input.xlsx** que já contém uma tabela dinâmica (você pode criar uma no Excel para teste).  
* Uma ferramenta de build de sua escolha (Maven, Gradle ou plain `javac`). Mostraremos a dependência Maven para início rápido.  

```xml
<!-- Add this to your pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.12</version> <!-- Use the latest stable -->
</dependency>
```

---

## Etapa 1: Carregar a pasta de trabalho de origem

A primeira coisa que fazemos é abrir o arquivo Excel que contém a tabela dinâmica original. Aspose.Cells trata a workbook como um objeto em memória, permitindo manipulá‑la sem iniciar o Excel.  

```java
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

> **Por que isso importa:** Carregar a workbook nos dá acesso às worksheets, cells e, crucialmente, ao pivot cache que sustenta a tabela dinâmica. Sem esta etapa a biblioteca não tem nada para copiar.

---

## Etapa 2: Obter a planilha que contém a pivot

Se sua workbook tem várias planilhas, você precisa apontar para a correta. Aqui simplesmente pegamos a primeira planilha, mas você também pode usar `get("SheetName")` para uma busca por nome.  

```java
// Obtain the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);
```

> **Dica de especialista:** Ao lidar com muitas planilhas, armazene o índice ou nome em um arquivo de configuração para evitar hard‑coding de números.

---

## Etapa 3: Definir o intervalo de origem que inclui a tabela dinâmica

A partir da versão 25.11 Aspose.Cells permite tratar uma tabela dinâmica como um intervalo de células regular. Especifique as células superior‑esquerda e inferior‑direita que envolvem toda a pivot.  

```java
// The range A1:D20 covers the whole pivot table in this example
Range sourceRange = worksheet.getCells().createRange("A1:D20");
```

> **Caso extremo:** Se sua pivot se expande dinamicamente (ex.: linhas são adicionadas depois), considere usar `worksheet.getPivotTables().get(0).getDataRange()` para obter o intervalo exato programaticamente.

---

## Etapa 4: Definir o intervalo de destino onde a pivot será copiada

Escolha qualquer célula vazia onde você deseja que a pivot duplicada apareça. Neste demo começamos em **F1**, deixando um espaço entre a original e a cópia.  

```java
// Destination starts at cell F1 – adjust as needed
Range destinationRange = worksheet.getCells().createRange("F1");
```

> **Por que não uma nova planilha?** Você também pode criar uma worksheet nova (`workbook.getWorksheets().add("Copy")`) e usar suas cells como destino. O mesmo método `copy` funciona entre planilhas.

---

## Etapa 5: Copiar a tabela dinâmica para o novo local

Agora a mágica acontece. O método `copy` clona a pivot, seu cache, formatação e até quaisquer slicers associados (a partir da versão mais recente).  

```java
// Perform the copy – the pivot is now duplicated at the destination
sourceRange.copy(destinationRange);
```

> **Importante:** A operação de cópia é *deep*; ela **não** cria uma referência de volta à pivot original. Você pode modificar a nova pivot independentemente sem afetar a fonte.

---

## Etapa 6: Salvar a workbook com a pivot duplicada

Por fim, escreva a workbook modificada de volta ao disco. Você pode sobrescrever o original ou criar um novo arquivo; aqui escolhemos o último para manter a fonte intacta.  

```java
// Save the workbook – the duplicated pivot lives in output.xlsx
workbook.save("YOUR_DIRECTORY/output.xlsx");
```

Ao abrir **output.xlsx** no Excel, você verá a pivot original nas colunas A‑D e uma cópia perfeita começando na coluna F. Ambas as pivots podem ser atualizadas separadamente.

---

## Exemplo Completo Funcional

Juntando tudo, aqui está a classe Java completa que você pode compilar e executar diretamente:  

```java
import com.aspose.cells.*;

public class ExportPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Define the source range that includes the pivot table (supported from version 25.11)
        // Adjust the range to match your actual pivot dimensions
        Range sourceRange = worksheet.getCells().createRange("A1:D20");

        // Step 4: Define the destination range where the pivot table will be copied
        // Change "F1" to any starting cell you prefer
        Range destinationRange = worksheet.getCells().createRange("F1");

        // Step 5: Copy the pivot table to the new location
        sourceRange.copy(destinationRange);

        // Step 6: Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Resultado esperado:** Abrir `output.xlsx` mostra a pivot original (A1:D20) e uma pivot idêntica começando em F1. Ambas as tabelas mantêm seus filtros, estilos e campos calculados.

---

## Lidando com Variações Comuns

| Situação | O que ajustar |
|-----------|----------------|
| **Multiple pivots** on the same sheet | Percorra `worksheet.getPivotTables()` e copie cada uma com seu próprio intervalo de destino. |
| **Dynamic data range** | Use `worksheet.getPivotTables().get(0).getDataRange()` para detectar automaticamente a área de origem. |
| **Copy to another workbook** | Carregue uma segunda instância `Workbook`, crie uma worksheet de destino e então chame `sourceRange.copy(destWorksheet.getCells().createRange("A1"))`. |
| **Preserve slicers** | A partir da 25.12, slicers são copiados automaticamente quando o intervalo os inclui. Verifique no Excel após salvar. |

---

## Dicas Profissionais & Armadilhas

* **Verificação de versão:** O método `copy` que suporta pivots foi adicionado no **Aspose.Cells 25.11**. Se você estiver em uma versão mais antiga receberá uma exceção. Sempre verifique a versão `aspose-cells` no seu `pom.xml`.  
* **Desempenho:** Copiar pivots grandes pode consumir muita memória. Se você precisar apenas dos dados, considere exportar a pivot para uma tabela plana ao invés de clonar o objeto inteiro.  
* **Comportamento de atualização:** A pivot duplicada mantém seu próprio cache. Se você modificar os dados subjacentes, chame `pivotTable.refresh()` na nova pivot para recalcular.  
* **Quirks de formatação:** Alguns formatos numéricos personalizados podem não sobreviver à cópia em versões muito antigas do Excel (<2007). Teste com a versão de Excel do seu público‑alvo.  

---

## Conclusão

Agora você tem uma resposta completa, de ponta a ponta, para **como copiar pivot** tables usando Aspose.Cells for Java, e viu como **duplicar Excel pivot** tables em poucas linhas de código. A abordagem funciona para pivots únicas ou múltiplas, entre worksheets e até entre workbooks.

Próximos passos podem incluir:

* Automatizar a cópia para cada pivot em um job em lote.  
* Adicionar código para renomear a pivot duplicada (ex.: `pivotTable.setName("Copy_of_Sales")`).  
* Integrar a rotina em um serviço de relatórios maior que gera PDFs ou exportações CSV.  

Experimente, ajuste os intervalos para combinar com seus dados reais e deixe a biblioteca fazer o trabalho pesado. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Como criar tabelas dinâmicas no Excel usando Aspose.Cells for Java: Um Guia Abrangente](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Manipulação de Tabelas Dinâmicas no Excel com Aspose.Cells Java: Um Guia Abrangente](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [Como atualizar a fonte da tabela dinâmica do Excel com Aspose.Cells for Java: Um Guia Abrangente](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}