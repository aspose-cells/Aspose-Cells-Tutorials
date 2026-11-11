---
date: '2026-10-28'
description: Aprenda a colar valores usando as opções de copiar e colar do Aspose.Cells
  em Java, com código passo a passo, configuração de dependência Maven e dicas de
  licenciamento.
keywords:
- how to paste values
- aspose cells maven dependency
- java generate excel report
- aspose cells license java
- copyoptions refertodestinationsheet
lastmod: '2026-10-28'
og_description: Aprenda a colar valores usando as opções de copiar e colar do Aspose.Cells
  em Java, com código passo a passo, configuração de dependência Maven e dicas de
  licenciamento.
og_image_alt: Developer guide showing Java code for copying and pasting Excel data
  with Aspose.Cells
og_title: Como colar valores com as opções de copiar e colar do Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to paste values using Aspose.Cells copy and paste options
    in Java, with step‑by‑step code, Maven dependency setup, and licensing tips.
  headline: How to paste values with Aspose.Cells copy and paste options
  type: TechArticle
- questions:
  - answer: It rewrites formula references so they point to the destination sheet
      after a copy, ensuring reporting formulas stay correct.
    question: What is `CopyOptions.ReferToDestinationSheet` used for?
  - answer: Set `PasteOptions.setOnlyVisibleCells(true)` and choose `PasteType.VALUES`.
    question: How do I paste only visible cells?
  - answer: Yes, a free trial or temporary license is available for evaluation, but
      a permanent license is required for production.
    question: Can I use Aspose.Cells without purchasing a license?
  - answer: Double‑check that `ReferToDestinationSheet` is enabled **before** the
      copy operation and that the source formulas don’t contain external workbook
      links.
    question: Why are some references still wrong after copying?
  - answer: Dispose of `Workbook` objects when finished, process large files in chunks,
      and monitor JVM heap usage.
    question: What memory‑management best practices should I follow?
  type: FAQPage
tags:
- paste values
- Aspose.Cells
- Java Excel automation
- copy options
- paste options
title: Como colar valores com as opções de copiar e colar do Aspose.Cells
url: /pt/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como colar valores com opções de copiar e colar do Aspose.Cells

Automatizar a geração de relatórios em Excel no Java significa que você pode gerar, consolidar e formatar pastas de trabalho sem nunca abrir o Excel manualmente. Com **Aspose.Cells** você tem controle total sobre fórmulas, linhas ocultas e valores de células, de modo que seus relatórios permaneçam precisos e leves. Neste tutorial você aprenderá como usar **CopyOptions.ReferToDestinationSheet** para manter as fórmulas corretas e **PasteOptions** para colar apenas os valores visíveis de que precisa.

## Respostas rápidas
- **O que `CopyOptions.ReferToDestinationSheet` faz?** Ele reescreve as fórmulas para que apontem para a planilha de destino após uma operação de cópia.  
- **Como posso colar apenas células visíveis?** Chame `PasteOptions.setOnlyVisibleCells(true)` junto com `PasteType.VALUES`.  
- **Qual versão da biblioteca é necessária?** Aspose.Cells 25.3 ou posterior.  
- **Preciso de uma licença para produção?** Sim – uma licença permanente ou temporária remove os limites de avaliação.  
- **Posso usar Maven ou Gradle?** Ambos são suportados; veja os trechos de dependência abaixo.

## O que é “automatizar relatórios em Excel”?
Automatizar relatórios em Excel significa gerar e atualizar pastas de trabalho do Excel programaticamente, permitindo criar, mesclar e formatar relatórios sem copiar‑colar manual, o que reduz erros e economiza horas de trabalho repetitivo. Essa abordagem é ideal para trabalhos em lote agendados, painéis orientados por dados e pipelines de consolidação financeira.

## Por que usar CopyOptions e PasteOptions para relatórios?
Essas duas classes permitem que você mantenha as referências de fórmulas intactas ao copiar dados **e** extraia apenas as células que estão visíveis após filtragem ou ocultação de linhas. Usá‑las juntas reduz a quantidade de dados transferidos em até 80 % em cenários típicos de tabelas filtradas e garante que as fórmulas continuem calculando corretamente na planilha de destino.

## Pré-requisitos
- Java 8 ou superior.  
- Maven ou Gradle para gerenciamento de dependências.  
- Aspose.Cells 25.3+ (licença de avaliação, temporária ou permanente).  

## Configurando Aspose.Cells para Java

Adicione a biblioteca ao seu projeto com uma das opções a seguir:

**Maven**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**  
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Aquisição de licença
- **Free trial** – conjunto completo de recursos para avaliação.  
- **Temporary license** – remove os limites da avaliação enquanto você testa.  
- **Permanent license** – recomendado para cargas de trabalho de produção.

Inicialize o Aspose.Cells no seu código Java:  
```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Guia passo a passo

### 1. copyOptions com referToDestinationSheet

#### Visão geral
`CopyOptions` é o objeto de configuração do Aspose.Cells que controla como fórmulas e referências de células são tratadas durante uma operação de cópia. Definir `CopyOptions.ReferToDestinationSheet` como `true` reescreve as referências de fórmula para que apontem para a nova planilha após a operação de cópia.

#### Etapa 1: inicializar workbook e worksheets  
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Etapa 2: configurar copyOptions  
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Etapa 3: executar operação de cópia  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Por que isso importa*: As fórmulas que originalmente referenciavam `Sheet1` agora referenciarão corretamente `DestSheet`, mantendo seus relatórios automatizados confiáveis.

**Dica de solução de problemas**: Se as fórmulas ainda referenciam a planilha antiga, certifique‑se de que `setReferToDestinationSheet(true)` seja chamado **antes** da cópia.

### 2. pasteOptions para valores‑apenas de células visíveis

#### Visão geral
`PasteOptions` é o objeto de configurações do Aspose.Cells que define o que será colado. Usar `PasteType.VALUES` junto com `onlyVisibleCells=true` copia apenas os valores exibidos, ignorando linhas/colunas ocultas e formatação.

#### Etapa 1: inicializar workbook e worksheets  
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Etapa 2: configurar pasteOptions  
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Etapa 3: executar operação de colagem  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Por que isso importa*: Ideal para extrair dados filtrados ou gerar relatórios limpos sem linhas ocultas ou ruído de formatação.

**Dica de solução de problemas**: Verifique se as linhas/colunas estão realmente ocultas no Excel antes de copiar; caso contrário, serão incluídas.

## Aplicações práticas
1. **Financial consolidation** – mesclar planilhas mensais em uma pasta de trabalho mestre mantendo todas as fórmulas precisas.  
2. **Filtered data export** – extrair apenas as linhas visíveis de uma tabela filtrada para uma planilha de resumo.  
3. **Scheduled report generation** – automatizar a criação de relatórios Excel noturnos com valores de célula precisos e referências corretas.

## Considerações de desempenho
- **Dispose of workbooks** quando concluído (`wb.dispose();`) para liberar recursos nativos.  
- **Batch operations** – agrupe várias chamadas de copy/paste para reduzir a sobrecarga.  
- **Monitor memory** – workbooks grandes podem exigir aumento de heap (`-Xmx2g`).  
- Aspose.Cells suporta **50+ formatos de entrada e saída** e pode processar workbooks com **até 2 milhões de linhas** sem carregar o arquivo inteiro na memória, oferecendo desempenho de alta taxa de transferência para cargas de trabalho corporativas.

## Perguntas frequentes

**Q: Para que serve `CopyOptions.ReferToDestinationSheet`?**  
A: Ele reescreve as referências de fórmula para que apontem para a planilha de destino após uma cópia, garantindo que as fórmulas de relatório permaneçam corretas.

**Q: Como colar apenas células visíveis?**  
A: Defina `PasteOptions.setOnlyVisibleCells(true)` e escolha `PasteType.VALUES`.

**Q: Posso usar Aspose.Cells sem comprar uma licença?**  
A: Sim, uma avaliação gratuita ou licença temporária está disponível para avaliação, mas uma licença permanente é necessária para produção.

**Q: Por que algumas referências ainda estão erradas após a cópia?**  
A: Verifique novamente se `ReferToDestinationSheet` está habilitado **antes** da operação de cópia e se as fórmulas de origem não contêm links para workbooks externos.

**Q: Quais são as melhores práticas de gerenciamento de memória que devo seguir?**  
A: Faça o dispose dos objetos `Workbook` quando terminar, processe arquivos grandes em partes e monitore o uso de heap da JVM.

**Q: É possível combinar CopyOptions e PasteOptions em uma única operação?**  
A: Sim, você pode encadeá‑los primeiro copiando com `CopyOptions` e depois aplicando `PasteOptions` na faixa de destino.

## Recursos
- **Documentação**: [Referência Aspose.Cells Java](https://reference.aspose.com/cells/java/)  
- **Download**: [Lançamentos Aspose.Cells para Java](https://releases.aspose.com/cells/java/)  
- **Compra**: [Comprar Aspose.Cells](https://purchase.aspose.com/buy)  
- **Teste gratuito**: [Teste gratuito Aspose.Cells](https://releases.aspose.com/cells/java/)  
- **Licença temporária**: [Solicitar uma licença temporária](https://purchase.aspose.com/temporary-license/)  
- **Fórum de suporte**: [Suporte Aspose](https://forum.aspose.com/c/cells)

---

**Última atualização:** 2026-10-28  
**Testado com:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose

## Tutoriais Relacionados

- [Ler Arquivo Excel Java – Manipulação de Células de Workbook com Aspose.Cells](/cells/java/cell-operations/aspose-cells-java-workbook-cell-manipulation/)
- [Adicionar Dados a Célula no Excel Usando Aspose.Cells para Java](/cells/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Converter Índices de Linha e Coluna de Células Excel com Aspose.Cells Java](/cells/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}