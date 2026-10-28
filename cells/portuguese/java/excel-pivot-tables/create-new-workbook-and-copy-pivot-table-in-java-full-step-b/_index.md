---
category: general
date: 2026-07-16
description: Crie uma nova pasta de trabalho e copie a tabela dinâmica usando Aspose.Cells
  para Java. Aprenda como duplicar a tabela dinâmica e copiar o intervalo do Excel
  em minutos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook
- copy pivot table
- duplicate pivot table
- how to copy pivot
- copy excel range
language: pt
lastmod: 2026-07-16
og_description: Crie uma nova pasta de trabalho e copie a tabela dinâmica com Aspose.Cells
  para Java. Este guia mostra como duplicar a tabela dinâmica e copiar o intervalo
  do Excel de forma eficiente.
og_image_alt: Screenshot of Java code that creates a new workbook and copies a pivot
  table using Aspose.Cells
og_title: Criar Nova Pasta de Trabalho e Copiar Tabela Dinâmica em Java – Tutorial
  Completo
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Create new workbook and copy pivot table using Aspose.Cells for Java.
    Learn how to duplicate pivot table and copy Excel range in minutes.
  headline: Create New Workbook and Copy Pivot Table in Java – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create new workbook and copy pivot table using Aspose.Cells for Java.
    Learn how to duplicate pivot table and copy Excel range in minutes.
  name: Create New Workbook and Copy Pivot Table in Java – Full Step‑by‑Step Guide
  steps:
  - name: What if the source pivot spans more than one sheet?
    text: Aspose.Cells can only copy ranges within a single worksheet at a time. If
      your pivot stretches across sheets, you’ll need to copy each relevant range
      separately and then re‑link them manually.
  - name: Does this method preserve custom number formats?
    text: Yes. The `copy` method copies cell styles, including number formats, fonts,
      and colors. However, if you have conditional formatting that references external
      ranges, double‑check those references after the copy.
  - name: How to copy a pivot that uses an external data source?
    text: When the pivot pulls data from an external connection (e.g., a SQL query),
      the connection information is **not** transferred by `copy`. You’ll need to
      recreate the data source in the destination workbook or embed the source data
      beforehand.
  - name: Can I copy only the pivot layout without the underlying data?
    text: You can achieve that by first clearing the data cells in the source range,
      then copying only the pivot’s layout. This is a more advanced scenario and usually
      not required for a simple **duplicate pivot table** task.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Criar Nova Pasta de Trabalho e Copiar Tabela Dinâmica em Java – Guia Completo
  Passo a Passo
url: /pt/java/excel-pivot-tables/create-new-workbook-and-copy-pivot-table-in-java-full-step-b/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Nova Pasta de Trabalho e Copiar Tabela Dinâmica em Java – Guia Completo Passo a Passo

Já se perguntou como **create new workbook** preservando uma tabela dinâmica complexa de um arquivo existente? Se você já ficou encarando uma planilha do Excel, pensando “Preciso dessa tabela dinâmica em outra pasta de trabalho”, e coçou a cabeça, não está sozinho. A boa notícia é que com Aspose.Cells for Java você pode duplicar uma tabela dinâmica em apenas algumas linhas.

Neste tutorial vamos percorrer os passos exatos para **copy pivot table** data, **duplicate pivot table** structures, e **copy Excel range** contents — tudo enquanto criamos uma nova pasta de trabalho do zero. Ao final, você terá um programa Java pronto‑para‑executar que faz exatamente o que você pediu.

## O que Você Vai Aprender

- Como **create new workbook** programaticamente com Aspose.Cells.
- A forma precisa de definir o intervalo que contém uma tabela dinâmica.
- Técnicas para **copy pivot table** e **duplicate pivot table** sem perder formatação ou conexões de dados.
- Como **copy Excel range** de forma eficiente e salvar o resultado.
- Armadilhas comuns e dicas para lidar com tabelas dinâmicas maiores.

Nenhuma referência externa necessária — tudo está autocontido, executável e explicado.

---

## Pré‑requisitos

Antes de mergulharmos, certifique‑se de que você tem:

1. **Java Development Kit (JDK) 11+** – qualquer versão recente funciona.
2. Biblioteca **Aspose.Cells for Java** (a versão mais recente em 2026‑07‑16). Você pode obtê‑la no Maven Central:

   ```xml
   <dependency>
       <groupId>com.aspose</groupId>
       <artifactId>aspose-cells</artifactId>
       <version>23.12</version>
   </dependency>
   ```

3. Um arquivo Excel fonte (`SourceWithPivot.xlsx`) que já contém a tabela dinâmica que você deseja copiar.
4. Uma IDE ou editor de texto simples — IntelliJ IDEA, Eclipse ou VS Code servem.

Tem tudo isso? Ótimo — vamos lá.

---

## Passo 1: **Create New Workbook** e Carregar o Arquivo Fonte

A primeira coisa que precisamos é um objeto workbook novo que eventualmente conterá a tabela dinâmica duplicada. Ao mesmo tempo, devemos carregar o workbook original para que possamos referenciar o intervalo da sua tabela dinâmica.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that already contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        // Grab the first worksheet where the pivot lives
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

> **Por que isso importa:**  
> Carregar o workbook fonte nos dá acesso ao objeto `Range` subjacente que encapsula a tabela dinâmica. Se você pular esta etapa, não terá nada para copiar, e a operação de **duplicate pivot table** falhará silenciosamente.

---

## Passo 2: Definir o **Copy Excel Range** Que Contém a Tabela Dinâmica

Uma tabela dinâmica não é uma única célula — ela ocupa um bloco retangular. Precisamos dizer ao Aspose.Cells exatamente quais células copiar.

```java
        // Define the cell range that includes the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

> **Dica:**  
> Se você não tem certeza do intervalo exato, abra o workbook fonte no Excel, selecione a tabela dinâmica e olhe a caixa de nome. Ela mostrará algo como `A1:G20`. Usar o intervalo exato garante que todas as configurações de campos, filtros e cálculos sejam mantidos quando nós **copy pivot table** mais tarde.

---

## Passo 3: **Create New Workbook** Que Receberá a Tabela Dinâmica Copiada

Agora criamos um workbook totalmente novo — é aqui que nossa **duplicate pivot table** viverá.

```java
        // Create a completely empty workbook for the destination
        Workbook dstWb = new Workbook(); // this automatically creates one empty worksheet
        Worksheet dstWs = dstWb.getWorksheets().get(0);
```

> **O que está acontecendo nos bastidores?**  
> O construtor padrão cria um workbook com uma única planilha vazia. Esta é a tela limpa que precisamos **para um create new workbook**. Nenhum estilo residual ou planilhas ocultas para se preocupar.

---

## Passo 4: **Copy Pivot Table** – Na Verdade Copiar o Intervalo do Excel Definido

Com a fonte e o destino prontos, executamos a operação de cópia. Esta etapa resolve a parte **how to copy pivot** do quebra‑cabeça.

```java
        // Copy the defined range (which includes the pivot) to the destination worksheet
        srcRange.copy(dstWs.getCells().createRange("A1"));
```

> **Por que `copy` funciona para tabelas dinâmicas:**  
> Aspose.Cells trata a tabela dinâmica como parte da coleção de células. Quando você copia o intervalo, ele traz o cache da tabela dinâmica, a lista de campos e o layout. O resultado é uma **duplicate pivot table** totalmente funcional no novo workbook.

---

## Passo 5: Salvar o Resultado e Verificar a Operação de **Copy Pivot Table**

Finalmente, persista o workbook de destino no disco. Abra o arquivo no Excel para confirmar que a tabela dinâmica aparece exatamente como no fonte.

```java
        // Save the destination workbook with the duplicated pivot table
        dstWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

**Resultado esperado:**  
- `CopyPivotResult.xlsx` abre com uma planilha contendo a mesma tabela dinâmica que você viu em `SourceWithPivot.xlsx`.  
- Todos os rótulos de linha/coluna, filtros e campos calculados permanecem intactos.  
- Você pode agora editar os dados fonte independentemente, e o novo workbook manterá seu próprio cache de tabela dinâmica.

---

## Casos de Borda & Perguntas Frequentes

### E se a tabela dinâmica fonte abranger mais de uma planilha?
Aspose.Cells só pode copiar intervalos dentro de uma única planilha por vez. Se sua tabela dinâmica se estender por várias planilhas, será necessário copiar cada intervalo relevante separadamente e então reconectar manualmente.

### Este método preserva formatos numéricos personalizados?
Sim. O método `copy` copia estilos de célula, incluindo formatos numéricos, fontes e cores. Contudo, se você tem formatação condicional que referencia intervalos externos, verifique essas referências após a cópia.

### Como copiar uma tabela dinâmica que usa uma fonte de dados externa?
Quando a tabela dinâmica obtém dados de uma conexão externa (por exemplo, uma consulta SQL), as informações da conexão **não** são transferidas pelo `copy`. Você precisará recriar a fonte de dados no workbook de destino ou incorporar os dados fonte previamente.

### Posso copiar apenas o layout da tabela dinâmica sem os dados subjacentes?
Você pode conseguir isso primeiro limpando as células de dados no intervalo fonte, e então copiando apenas o layout da tabela dinâmica. Este é um cenário mais avançado e geralmente não é necessário para uma tarefa simples de **duplicate pivot table**.

---

## Exemplo Completo em Funcionamento (Todas as Etapas Combinadas)

Abaixo está a classe Java completa, pronta‑para‑executar. Basta substituir `YOUR_DIRECTORY` pelo caminho real da pasta na sua máquina.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook containing the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Define the exact range that holds the pivot table
        // Adjust "A1:G20" to match your pivot's size
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 3: Create a brand‑new workbook that will receive the copy
        Workbook dstWb = new Workbook(); // creates an empty workbook with one sheet
        Worksheet dstWs = dstWb.getWorksheets().get(0);

        // Step 4: Copy the pivot (and any surrounding data) to the new workbook
        srcRange.copy(dstWs.getCells().createRange("A1"));

        // Step 5: Save the destination file – now it contains the duplicated pivot table
        dstWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");

        System.out.println("Pivot table copied successfully! Check CopyPivotResult.xlsx.");
    }
}
```

Execute o programa (`java CopyPivotTableDemo`) e você verá a mensagem no console confirmando o sucesso.

---

## Dicas Profissionais & Melhores Práticas

- **Valide o intervalo** antes de copiar. Use `srcWs.getCells().maxDisplayRange` para descobrir programaticamente a área usada se você não quiser codificar `"A1:G20"`.
- **Desative o cálculo** temporariamente para workbooks enormes a fim de acelerar a cópia:

  ```java
  srcWb.getSettings().setCalculateFormulaOnOpen(false);
  ```

- **Libere recursos** (`srcWb.dispose(); dstWb.dispose();`) em serviços de longa duração para evitar vazamentos de memória.
- **Compatibilidade de versão:** O código funciona com Aspose.Cells 23.12 e posteriores. Versões mais antigas podem exigir `srcRange.copyTo` em vez de `copy`.

---

## Próximos Passos

Agora que você dominou **create new workbook** e **copy pivot table**, você pode explorar:

- **How to copy pivot** entre várias planilhas em um job em lote.
- Adicionar **copy excel range** para tabelas de dados regulares ao lado da tabela dinâmica.
- Automatizar a criação de **duplicate pivot table** para o relatório de cada mês usando um loop.
- Exportar a tabela dinâmica duplicada para PDF ou HTML com os renderizadores embutidos do Aspose.Cells.

Cada um desses tópicos se baseia na fundação estabelecida aqui, e todos se beneficiam da mesma abordagem limpa e programática.

---

## Conclusão

Percorremos todo o processo de **create new workbook**, definir o **copy excel range** de origem e **copy pivot table** para produzir uma **duplicate pivot table** em Java usando Aspose.Cells. A solução é concisa, totalmente funcional e pronta para uso em produção. Sinta‑se à vontade para ajustar o intervalo, experimentar diferentes arquivos fonte ou incorporar essa lógica em um pipeline de relatórios maior.

Se você encontrar algum problema ou tiver ideias para expandir este tutorial, deixe um comentário abaixo. Feliz codificação!

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como Criar Tabelas Dinâmicas no Excel Usando Aspose.Cells para Java&#58; Um Guia Abrangente](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Como Atualizar a Fonte da Tabela Dinâmica do Excel com Aspose.Cells para Java&#58; Um Guia Abrangente](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Manipulação de Tabelas Dinâmicas do Excel com Aspose.Cells Java&#58; Um Guia Abrangente](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}