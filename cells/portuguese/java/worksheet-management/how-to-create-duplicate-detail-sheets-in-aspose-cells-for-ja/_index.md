---
category: general
date: 2026-08-17
description: Aprenda como criar planilhas de detalhes duplicadas com Aspose.Cells
  para Java e permitir nomes de planilhas duplicados usando SmartMarkerProcessor.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicate detail sheets
- allow duplicate sheet names
language: pt
lastmod: 2026-08-17
og_description: Crie planilhas de detalhes duplicadas no Aspose.Cells para Java e
  permita nomes de planilhas duplicados. Siga este tutorial completo para obter resultados
  instantâneos.
og_image_alt: Generated Excel workbook showing multiple detail sheets with the same
  name
og_title: Crie planilhas de detalhes duplicadas no Aspose.Cells para Java – guia passo
  a passo
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Learn how to create duplicate detail sheets with Aspose.Cells for Java
    and allow duplicate sheet names using SmartMarkerProcessor.
  headline: How to create duplicate detail sheets in Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create duplicate detail sheets with Aspose.Cells for Java
    and allow duplicate sheet names using SmartMarkerProcessor.
  name: How to create duplicate detail sheets in Aspose.Cells for Java
  steps:
  - name: Load the master template workbook.
    text: Load the master template workbook.
  - name: Configure `SmartMarkerProcessor` to **allow duplicate sheet names**.
    text: Configure `SmartMarkerProcessor` to **allow duplicate sheet names**.
  - name: Process the workbook so that a new detail sheet is created for each data
      group.
    text: Process the workbook so that a new detail sheet is created for each data
      group.
  - name: Save the resulting workbook that now contains duplicated detail sheets.
    text: Save the resulting workbook that now contains duplicated detail sheets.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Como criar folhas de detalhe duplicadas no Aspose.Cells para Java
url: /pt/java/worksheet-management/how-to-create-duplicate-detail-sheets-in-aspose-cells-for-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar planilhas de detalhe duplicadas no Aspose.Cells para Java

Se você precisar **criar planilhas de detalhe duplicadas** em uma pasta de trabalho Excel, o Aspose.Cells para Java torna isso simples. Este tutorial mostra exatamente como permitir nomes de planilha duplicados ao gerar planilhas de detalhe com SmartMarkerProcessor, para que você possa produzir uma pasta de trabalho que contenha várias planilhas com o mesmo nome.

Você verá um exemplo completo e executável, uma análise de cada opção de configuração e dicas para lidar com casos de borda comuns, como colisões de nomes e grandes conjuntos de dados. Nenhuma referência externa é necessária — tudo o que você precisa está incluído no código abaixo.

## Pré-requisitos

Antes de começar, certifique-se de que você tem:

* Java Development Kit (JDK) 8 ou mais recente.
* Maven ou Gradle para gerenciar dependências.
* Biblioteca Aspose.Cells para Java (versão 23.9 ou posterior). Adicione a seguinte dependência Maven ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

* Uma pasta de trabalho modelo mestre (`master_template.xlsx`) que contém uma região Smart Marker para os dados de detalhe.

## Visão geral da solução

A solução segue quatro etapas lógicas:

1. Carregar a pasta de trabalho modelo mestre.
2. Configurar `SmartMarkerProcessor` para **permitir nomes de planilha duplicados**.
3. Processar a pasta de trabalho para que uma nova planilha de detalhe seja criada para cada grupo de dados.
4. Salvar a pasta de trabalho resultante que agora contém planilhas de detalhe duplicadas.

Cada etapa é explicada em detalhe abaixo, e o arquivo de código-fonte completo é fornecido ao final do guia.

## Etapa 1: Carregar a pasta de trabalho modelo mestre

A primeira operação cria uma instância `Workbook` que representa o arquivo modelo. O modelo deve conter um placeholder Smart Marker (por exemplo, `&=DetailData`) que instrui o processador onde inserir os dados.

```java
import com.aspose.cells.*;

public class DuplicateDetailSheet {
    public static void main(String[] args) throws Exception {
        // Load the master template workbook from the file system
        Workbook workbook = new Workbook("YOUR_DIRECTORY/master_template.xlsx");
```

**Por que isso importa:** Carregar o modelo isola o layout e a formatação da lógica de geração de dados, o que mantém seu código limpo e facilita reutilizar o mesmo modelo para diferentes conjuntos de dados.

## Etapa 2: Configurar SmartMarkerProcessor para permitir nomes de planilha duplicados

Por padrão, o Aspose.Cells gera nomes de planilha únicos ao criar planilhas de detalhe. Para **permitir nomes de planilha duplicados**, defina a opção `DetailSheetNewName` para um valor constante. O processador reutilizará esse nome para cada planilha gerada.

```java
        // Create a SmartMarkerProcessor instance
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // Enable duplicate detail sheet names by assigning a fixed name
        processor.getOptions().setDetailSheetNewName("DetailSheet");

        // Optional: if you want to keep the original sheet after processing, set this flag
        // processor.getOptions().setKeepOriginalDetailSheet(true);
```

**Por que isso importa:** Definir `DetailSheetNewName` indica ao mecanismo que ele deve reutilizar o mesmo nome para cada planilha de detalhe, atendendo diretamente ao requisito de **permitir nomes de planilha duplicados**. Essa abordagem é útil quando ferramentas subsequentes identificam planilhas pela posição em vez do nome.

## Etapa 3: Processar a pasta de trabalho para gerar as planilhas de detalhe

Após a configuração, invoque `process` na pasta de trabalho. O processador lê a região Smart Marker, cria uma nova planilha para cada grupo de dados e a preenche com as linhas correspondentes.

```java
        // Process the workbook; this creates the duplicate detail sheets
        processor.process(workbook);
```

**Por que isso importa:** A chamada `process` realiza o trabalho pesado — analisar os Smart Markers, clonar a planilha modelo e inserir os dados. Como a opção `DetailSheetNewName` já está definida, cada nova planilha recebe o mesmo nome, resultando em nomes de planilha duplicados no arquivo final.

## Etapa 4: Salvar a pasta de trabalho resultante

Finalmente, grave a pasta de trabalho modificada em um novo arquivo. O arquivo de saída conterá tantas abas “DetailSheet” quantos forem os grupos de dados.

```java
        // Save the workbook with duplicated detail sheets
        workbook.save("YOUR_DIRECTORY/duplicate_detail.xlsx");
    }
}
```

**Por que isso importa:** Salvar o arquivo finaliza as alterações feitas pelo processador. A pasta de trabalho resultante pode ser aberta no Microsoft Excel, LibreOffice ou qualquer outro aplicativo de planilhas que suporte o formato XLSX.

## Código-fonte completo

Juntando todas as peças, aqui está o programa completo que você pode copiar, colar e executar:

```java
import com.aspose.cells.*;

public class DuplicateDetailSheet {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the master template workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/master_template.xlsx");

        // Step 2: Create a SmartMarkerProcessor and allow duplicate detail sheet names
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.getOptions().setDetailSheetNewName("DetailSheet"); // same name allowed for each detail sheet

        // Step 3: Process the workbook to generate the detail sheets
        processor.process(workbook);

        // Step 4: Save the resulting workbook with duplicated detail sheets
        workbook.save("YOUR_DIRECTORY/duplicate_detail.xlsx");
    }
}
```

### Saída esperada

Ao abrir `duplicate_detail.xlsx`, você verá várias abas nomeadas **DetailSheet**. Cada aba contém o conjunto de dados que corresponde a um grupo específico de Smart Marker no modelo. O layout, a formatação e as fórmulas do modelo mestre são preservados em cada planilha duplicada.

## Lidando com armadilhas comuns

| Problema | Explicação | Solução |
|----------|------------|---------|
| Excel mostra um aviso sobre nomes de planilha duplicados | O Excel permite nomes duplicados, mas pode exibir um aviso ao abrir o arquivo. | O aviso é inofensivo; a pasta de trabalho funciona corretamente. Se preferir suprimir o aviso, renomeie as planilhas após o processamento usando `Workbook.getWorksheets().get(i).setName("DetailSheet" + i);`. |
| Conjuntos de dados grandes causam alto uso de memória | Cada planilha duplicada cria uma cópia completa do modelo, o que pode consumir RAM. | Habilite o modo de streaming com `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);` antes de carregar o modelo. |
| Região Smart Marker não encontrada | O processador não consegue localizar `&=DetailData` no modelo. | Verifique se a sintaxe do placeholder corresponde à fonte de dados e se a planilha do modelo não está oculta. |

## Dica profissional: personalizando o esquema de nomenclatura duplicada

Se você precisar de um padrão de nomenclatura previsível enquanto ainda permite duplicatas, combine um nome base com um índice:

```java
processor.getOptions().setDetailSheetNewName("DetailSheet_{0}");
```

O placeholder `{0}` é substituído pelo índice da planilha, produzindo nomes como `DetailSheet_1`, `DetailSheet_2`, etc. Isso ainda satisfaz o requisito de **permitir nomes de planilha duplicados** porque o nome base permanece constante.

## Próximos passos

Agora que você pode **criar planilhas de detalhe duplicadas**, pode explorar os seguintes tópicos:

* **Preencher planilhas de detalhe com imagens** – use objetos `Picture` para incorporar logotipos ou gráficos.
* **Aplicar formatação condicional** – adicione regras `FormatCondition` para destacar linhas com base em valores.
* **Exportar para PDF** – chame `workbook.save("output.pdf", SaveFormat.PDF);` para gerar uma versão PDF das planilhas duplicadas.

Cada uma dessas extensões se baseia no mesmo fluxo de trabalho Smart Marker demonstrado aqui, permitindo que você automatize tarefas complexas de relatórios Excel com confiança.

---

*Você aprendeu como criar planilhas de detalhe duplicadas no Aspose.Cells para Java e como permitir nomes de planilha duplicados usando SmartMarkerProcessor. Aplique o código, adapte o modelo e integre a técnica em seus pipelines de relatórios.*

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Criar e acessar planilhas Excel, adicionar marcadores PDF usando Aspose.Cells para Java](/cells/english/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [Criar e acessar planilhas Excel, adicionar marcadores PDF Aspose Cells Java](/cells/german/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [Criar e acessar planilhas Excel, adicionar marcadores PDF Aspose Cells Java](/cells/french/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}