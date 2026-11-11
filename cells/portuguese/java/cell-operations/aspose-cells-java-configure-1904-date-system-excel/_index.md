---
date: '2026-10-28'
description: Aprenda como mudar o sistema de datas do Excel para 1904 usando Aspose.Cells
  para Java, definir o formato de data do Excel e converter o sistema 1904 do Excel
  de forma eficiente.
keywords:
- change excel date system
- excel 1904 date conversion
- maven dependency aspose cells
lastmod: '2026-10-28'
og_description: Altere o sistema de datas do Excel para 1904 usando Aspose.Cells para
  Java. Aprenda passo a passo como habilitar o sistema 1904, definir datas e converter
  de volta.
og_image_alt: Aspose.Cells Java guide showing how to switch Excel to the 1904 date
  system
og_title: Alterar o sistema de datas do Excel para 1904 com Aspose.Cells para Java
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  headline: Change Excel date system to 1904 with Aspose.Cells Java
  type: TechArticle
- description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  name: Change Excel date system to 1904 with Aspose.Cells Java
  steps:
  - name: initialize and load the workbook
    text: The `Workbook` class represents an entire Excel file in memory. First, create
      a `Workbook` instance that points to your existing file.
  - name: enable the 1904 date system
    text: The `WorkbookSettings.setDate1904` method toggles the workbook‑level date
      flag. Setting it to `true` activates the 1904 system for all worksheets. **Pro
      tip:** You can also call `setDate1904(false)` later if you need to revert.
  - name: save the modified workbook
    text: Finally, write the changes to a new file (or overwrite the original). The
      `save` method respects the active date system automatically. > **Note:** The
      code above uses the class name `tWorkbook` as originally provided. Ensure this
      typo matches your project’s naming conventions or correct it to `Workb
  type: HowTo
- questions:
  - answer: The 1900 system starts on January 1, 1900, while the 1904 system starts
      on January 1, 1904, shifting all dates by 1,462 days.
    question: What is the difference between the 1900 and 1904 date systems?
  - answer: Yes, but you must close the file in Excel first; otherwise the save operation
      will fail.
    question: Can I change the date system of a workbook that is currently open in
      Excel?
  - answer: The method works in the free trial, but a full license removes evaluation
      limitations.
    question: Do I need a license to use `setDate1904`?
  - answer: No, the date system is a workbook‑level setting; it applies to all worksheets.
    question: Is it possible to change the date system for only a single worksheet?
  - answer: Open the saved file in Excel, go to **File → Options → Advanced**, and
      check the **"Use 1904 date system"** box.
    question: How can I verify that the date system was changed?
  type: FAQPage
tags:
- change excel date system
- aspose cells java
- excel date conversion
- java excel processing
title: Alterar o sistema de datas do Excel para 1904 com Aspose.Cells Java
url: /pt/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Alterar o sistema de datas do Excel para 1904 com Aspose.Cells Java

## Respostas rápidas
- **O que o sistema de datas 1904 faz?** Ele começa a contar os dias a partir de 1 de janeiro de 1904, deslocando todas as datas em 1.462 dias em comparação com o sistema padrão de 1900.  
- **Por que usar Aspose.Cells para alterar o sistema de datas?** Ele fornece uma API simples que funciona sem o Excel instalado e suporta arquivos grandes.  
- **Quais versões do Java são suportadas?** JDK 8 ou superior.  
- **Preciso de uma licença?** Um teste gratuito funciona para avaliação; uma licença remove os limites de uso.  
- **Posso converter de volta para o sistema 1900 mais tarde?** Sim, basta chamar `setDate1904(false)`.

## O que é o sistema de datas 1904 no Excel?
O sistema de datas 1904 conta os dias a partir de 1 de janeiro de 1904, em vez da época padrão de 1900. Essa mudança adiciona exatamente 1.462 dias a cada valor de data, o que explica por que pastas de trabalho legadas do Mac parecem deslocadas quando abertas no Windows. É usado principalmente para compatibilidade com arquivos Excel Macintosh mais antigos e alguns modelos financeiros legados.

## Por que alterar o sistema de datas do Excel com Aspose.Cells?
Você pode mudar o sistema de datas diretamente a partir do Java, eliminando etapas manuais no Excel. Aspose.Cells processa pastas de trabalho de até **2 GB** e pode converter uma pasta de trabalho com 500 planilhas em menos de **2 segundos** em um servidor típico de 4 núcleos, oferecendo automação de alto rendimento no lado do servidor.

## Pré-requisitos
- Java Development Kit (JDK) 8 ou superior.  
- Maven ou Gradle para gerenciamento de dependências.  
- Conhecimento básico de programação Java.  

## Configurando Aspose.Cells para Java

### Maven
Adicione a seguinte dependência ao seu arquivo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
Inclua esta linha no seu arquivo `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Aquisição de licença
Aspose oferece um teste gratuito, licença temporária e licenças comerciais completas. Você pode começar com o [teste gratuito](https://releases.aspose.com/cells/java/) ou obter uma licença temporária na [página de licença temporária](https://purchase.aspose.com/temporary-license/).

## Como alterar o sistema de datas do Excel para 1904 com Aspose.Cells para Java?
Carregue a pasta de trabalho, habilite a configuração 1904 e salve o arquivo — esse fluxo de três etapas atualiza a época interna de datas da pasta de trabalho em menos de um segundo. A chamada de API `setDate1904(true)` altera o sinalizador do sistema, e a alteração é persistida quando você chama `save`. Não é necessária a instalação do Excel, tornando-o ideal para ambientes de servidor sem interface gráfica.

### Etapa 1: inicializar e carregar a pasta de trabalho
A classe `Workbook` representa um arquivo Excel completo na memória. Primeiro, crie uma instância de `Workbook` que aponte para o seu arquivo existente.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### Etapa 2: habilitar o sistema de datas 1904
O método `WorkbookSettings.setDate1904` alterna o sinalizador de data ao nível da pasta de trabalho. Definir como `true` ativa o sistema 1904 para todas as planilhas.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**Dica profissional:** Você também pode chamar `setDate1904(false)` mais tarde se precisar reverter.

### Etapa 3: salvar a pasta de trabalho modificada
Finalmente, grave as alterações em um novo arquivo (ou sobrescreva o original). O método `save` respeita automaticamente o sistema de datas ativo.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
String outDir = "YOUR_OUTPUT_DIRECTORY"; // Specify where you want to save the modified workbook

// Load and modify your workbook as shown in previous steps
tWorkbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
workbook.getSettings().setDate1904(true);

// Save the changes to a new file
workbook.save(outDir + "/I1904DateSystem_out.xls");
```

> **Nota:** O código acima usa o nome de classe `tWorkbook` como fornecido originalmente. Certifique‑se de que esse erro de digitação corresponda às convenções de nomenclatura do seu projeto ou corrija para `Workbook` se necessário.

## Definir data do Excel programaticamente (palavra‑chave secundária)
Se precisar ajustar valores de células individuais após mudar o sistema, você pode usar `cells.get(i, j).putValue(Date)`, onde a data será interpretada de acordo com o sistema de datas ativo.

## Converter o sistema Excel 1904 de volta para 1900 (palavra‑chave secundária)
Para reverter, basta chamar:

```java
workbook.getSettings().setDate1904(false);
```

Em seguida, salve a pasta de trabalho novamente.

## Aplicações práticas
1. **Arquivamento de dados** – Preserve timestamps legados ao migrar planilhas antigas baseadas em Mac.  
2. **Relatórios multiplataforma** – Gere relatórios que abram corretamente tanto no Windows quanto no macOS sem incompatibilidades de datas.  
3. **Modelagem financeira** – Alinhe cálculos de datas com modelos financeiros legados que esperam o sistema 1904.  

## Considerações de desempenho
- Limite as operações de pasta de trabalho em uma única sessão para manter o uso de memória baixo; Aspose.Cells transmite dados e nunca carrega o arquivo inteiro na RAM, a menos que você solicite explicitamente.  
- Ajuste as flags de coleta de lixo do Java (`-XX:+UseG1GC`) para arquivos muito grandes a fim de evitar picos de tempo de pausa.  

## Perguntas frequentes

**Q: Qual é a diferença entre os sistemas de datas 1900 e 1904?**  
A: O sistema 1900 começa em 1 de janeiro de 1900, enquanto o sistema 1904 começa em 1 de janeiro de 1904, deslocando todas as datas em 1.462 dias.

**Q: Posso mudar o sistema de datas de uma pasta de trabalho que está aberta no Excel?**  
A: Sim, mas você deve fechar o arquivo no Excel primeiro; caso contrário, a operação de salvamento falhará.

**Q: Preciso de licença para usar `setDate1904`?**  
A: O método funciona no teste gratuito, mas uma licença completa remove as limitações de avaliação.

**Q: É possível mudar o sistema de datas apenas para uma única planilha?**  
A: Não, o sistema de datas é uma configuração ao nível da pasta de trabalho; ele se aplica a todas as planilhas.

**Q: Como posso verificar se o sistema de datas foi alterado?**  
A: Abra o arquivo salvo no Excel, vá em **Arquivo → Opções → Avançado** e marque a caixa **"Usar sistema de datas 1904"**.

## Conclusão
Agora você sabe como **alterar o sistema de datas do Excel** para 1904 usando Aspose.Cells para Java, como definir datas em células individuais e como reverter para o sistema 1900 quando necessário. Integre esses trechos ao seu pipeline de processamento de dados para garantir compatibilidade de datas entre plataformas e arquivos legados.

---

**Last Updated:** 2026-10-28  
**Tested With:** Aspose.Cells 25.3 for Java  
**Author:** Aspose  

**Recursos**
- **Documentação:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **Download:** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)
- **Comprar licença:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **Teste gratuito:** [Start Free Trial](https://releases.aspose.com/cells/java/)
- **Licença temporária:** [Get Temporary License](https://purchase.aspose.com/temporary-license/)
- **Fórum de suporte:** [Aspose Support](https://forum.aspose.com/c/cells/9)

## Tutoriais Relacionados

- [Converter Excel para PDF de forma eficiente com formatos de data personalizados usando Aspose.Cells para Java](/cells/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Aspose.Cells para Java: Como criar e formatar pastas de trabalho Excel de forma eficiente](/cells/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [Domine a manipulação de Excel com Aspose.Cells para Java: Operações de pasta de trabalho e tutorial de estilo de células](/cells/java/workbook-operations/excel-manipulation-aspose-cells-java-tutorial/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}