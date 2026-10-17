---
date: '2026-08-16'
description: Aprenda a adicionar globalização em Java usando Aspose.Cells, personalize
  mensagens de erro do Excel e configure a dependência Maven.
keywords:
- how to add globalization
- custom excel error messages
- aspose.cells maven dependency
lastmod: '2026-08-16'
og_description: Aprenda a adicionar globalização em Java usando Aspose.Cells, personalize
  mensagens de erro do Excel e configure a dependência Maven. Siga o guia passo a
  passo.
og_image_alt: Guide showing Java code that customizes Excel globalization with Aspose.Cells
og_title: Como adicionar globalização em Java com Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-16'
  description: Learn how to add globalization in Java using Aspose.Cells, customize
    Excel error messages, and set up the Maven dependency.
  headline: How to add globalization in Java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. Create a single `RussianGlobalization` instance and pass it to each
      workbook via `setGlobalizationSettings`.
    question: Can I apply the same globalization settings to multiple workbooks at
      once?
  - answer: Override additional methods such as `getCurrencySymbol` and `getDatePattern`
      in your subclass to return appropriate RTL symbols.
    question: What if I need to support a language that uses right‑to‑left script?
  - answer: No. The trial version fully supports `GlobalizationSettings`; only evaluation
      watermarks appear on certain output formats.
    question: Is a license required for the trial version to use custom globalization?
  - answer: Insert `System.out.println` statements inside your overridden methods
      to verify the input `err` value matches your switch cases.
    question: How do I debug incorrect error strings?
  - answer: Negligibly. The library looks up the string only when rendering cell values,
      not during intermediate calculation steps.
    question: Does this affect formula calculation speed?
  type: FAQPage
tags:
- globalization
- Aspose.Cells
- Java internationalization
- Excel localization
title: Como adicionar globalização em Java com Aspose.Cells
url: /pt/java/calculation-engine/custom-globalization-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Como adicionar globalização em Java com Aspose.Cells

## Introdução

Adicionar globalização ao seu workbook Java permite que você apresente mensagens de erro, valores booleanos e outras strings específicas de localidade no idioma que seus usuários esperam. Neste tutorial você aprenderá **como adicionar globalização** para russo, mas o mesmo padrão funciona para qualquer idioma. Ao final do guia você será capaz de:

- Substituir o texto de erro padrão e as representações booleanas.
- Aplicar suas configurações personalizadas a qualquer instância de `Workbook`.
- Integrar a solução em um projeto Java típico baseado em Maven.

Pronto para tornar seus arquivos Excel realmente multilíngues? Primeiro, vamos verificar se seu ambiente de desenvolvimento atende aos pré‑requisitos.

## Respostas rápidas
- **O que é globalização no Aspose.Cells?** É um conjunto de strings sensíveis à localidade (erros, booleanos, etc.) que você pode substituir por texto personalizado.  
- **Qual artefato Maven é necessário?** `com.aspose:aspose-cells:25.3`.  
- **Posso direcionar idiomas além do russo?** Sim – estenda `GlobalizationSettings` e substitua os métodos necessários para cada localidade.  
- **Preciso de uma licença para desenvolvimento?** Um teste gratuito funciona para testes; uma licença permanente remove as marcas d'água de avaliação.  
- **A solução é thread‑safe?** Aplique as configurações por workbook; o objeto `GlobalizationSettings` em si é imutável após a criação.

## O que é globalização no Aspose.Cells?

`GlobalizationSettings` é o objeto de configuração do Aspose.Cells que controla strings específicas de localidade, como mensagens de erro, valores booleanos, símbolos de moeda e padrões de data. Ao fornecer sua própria subclasse, você informa à biblioteca qual texto exibir para cada cultura, permitindo substituir as strings padrão em inglês por traduções que correspondam ao idioma e às convenções regionais do usuário final.

## Por que adicionar globalização personalizada?

Aspose.Cells suporta **mais de 50 formatos de entrada e saída** – incluindo XLSX, CSV, PDF e ODS – e pode processar workbooks com **até 200 000 linhas** sem carregar o arquivo inteiro na memória. Personalizar a globalização garante que os usuários finais vejam mensagens em seu idioma nativo, reduzindo os tickets de suporte em cerca de **30 %** para implantações multinacionais.

## Pré‑requisitos

- **Java Development Kit** 8 ou superior.
- **IDE** como IntelliJ IDEA ou Eclipse.
- **Aspose.Cells for Java** versão 25.3 (ou posterior) adicionada via Maven ou Gradle.

### Configurando Aspose.Cells para Java

Adicione a dependência Maven ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
    <classifier>jdk17</classifier>
</dependency>
```
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Ou, se preferir Gradle, insira o seguinte em `build.gradle`:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Aquisição de licença

Aspose oferece várias opções de licenciamento:

- **Free trial** – avaliação com todos os recursos por 30 dias.  
- **Temporary license** – avaliação ilimitada sem marcas d'água.  
- **Commercial license** – pronta para produção, com suporte prioritário.

Depois de obter um arquivo de licença, configure-o uma vez na inicialização da aplicação:

```java
com.aspose.cells.License license = new com.aspose.cells.License();
license.setLicense("Aspose.Cells.lic");
```
```java
import com.aspose.cells.*;

public class InitializeAspose {
    public static void main(String[] args) {
        // Set the license if you have one
        License license = new License();
        try {
            license.setLicense("PathToYourLicenseFile.lic");
        } catch (Exception e) {
            System.out.println("Error setting license: " + e.getMessage());
        }

        // Create a new workbook instance
        Workbook workbook = new Workbook();
    }
}
```

## Como adicionar globalização para Russo?

Um objeto `Workbook` representa um arquivo Excel carregado na memória, fornecendo acesso às suas planilhas, células e configurações. Carregue seu workbook, crie uma subclasse de `GlobalizationSettings` e anexe-a ao workbook. A resposta direta é: **instanciar uma classe personalizada `GlobalizationSettings`, sobrescrever `getErrorValueString` e `getBooleanValueString`, então chamar `workbook.setGlobalizationSettings(customSettings)`**. Essa abordagem em duas etapas substitui as strings padrão em russo pelas suas próprias.

### Definindo as configurações personalizadas

Na primeira vez que você referenciar `GlobalizationSettings` neste guia, observe a definição:

`GlobalizationSettings` é a classe base que o Aspose.Cells usa para recuperar strings específicas de localidade.  

Agora crie uma subclasse que retorne texto específico para russo:

```java
class RussianGlobalization extends GlobalizationSettings {
    @Override
    public String getErrorValueString(String err) {
        switch (err) {
            case "#DIV/0!": return "Деление на ноль";
            case "#N/A":    return "Недоступно";
            default:        return err; // fallback to original
        }
    }

    @Override
    public String getBooleanValueString(Boolean bv) {
        return bv ? "ИСТИНА" : "ЛОЖЬ";
    }
}
```
```java
import com.aspose.cells.*;

class RussianGlobalization extends GlobalizationSettings {
    public String getErrorValueString(String err) {
        switch (err.toUpperCase()) {
            case "#NAME?":
                return "#RussianName-имя?";
        }
        return "RussianError-ошибка";
    }

    public String getBooleanValueString(Boolean bv) {
        return bv ? "RussianTrue-правда" : "RussianFalse-ложный";
    }
}
```

### Aplicando as configurações a um workbook

Depois de definir a subclasse, anexe-a a qualquer instância de `Workbook`:

```java
Workbook wb = new Workbook("input.xlsx");
wb.setGlobalizationSettings(new RussianGlobalization());
wb.save("output.xlsx");
```
```java
import com.aspose.cells.*;
import AsposeCellsExamples.Utils; // Placeholder import

public void Run() throws Exception {
    String dataDir = "YOUR_DATA_DIRECTORY";
    String outDir = "YOUR_OUTPUT_DIRECTORY";

    Workbook wb = new Workbook(dataDir + "/sampleRussianGlobalization.xlsx");
    wb.getSettings().setGlobalizationSettings(new RussianGlobalization());
    
    wb.calculateFormula();
    wb.save(outDir + "/outputRussianGlobalization.pdf");
}
```

## Aplicações práticas

- **Financial reporting** – exibir códigos de erro no idioma nativo do contador, reduzindo interpretações errôneas.  
- **Enterprise‑wide tools** – incorporar a mesma lógica de globalização em dezenas de utilitários internos baseados em Excel.  
- **Automated data pipelines** – garantir que sistemas downstream recebam valores sensíveis à localidade sem etapas adicionais de tradução.

## Considerações de desempenho

Quando você habilita a globalização personalizada, o Aspose.Cells ainda processa fórmulas e I/O com o mesmo alto desempenho. Para manter o uso de memória baixo:

- Liberar referências ao workbook (`wb.dispose()`) após salvar.  
- Use `CalculationOptions.setEnableIterativeCalculation(true)` somente quando necessário.  
- Ajuste o heap da JVM (`-Xmx2g`) para workbooks maiores que 100 MB.

## Perguntas frequentes

**Q: Posso aplicar as mesmas configurações de globalização a vários workbooks ao mesmo tempo?**  
A: Sim. Crie uma única instância `RussianGlobalization` e passe-a a cada workbook via `setGlobalizationSettings`.

**Q: E se eu precisar suportar um idioma que usa script da direita para a esquerda?**  
A: Sobrescreva métodos adicionais como `getCurrencySymbol` e `getDatePattern` em sua subclasse para retornar os símbolos RTL apropriados.

**Q: É necessária uma licença para a versão de teste usar globalização personalizada?**  
A: Não. A versão de teste suporta totalmente `GlobalizationSettings`; apenas marcas d'água de avaliação aparecem em certos formatos de saída.

**Q: Como depurar strings de erro incorretas?**  
A: Insira instruções `System.out.println` dentro dos seus métodos sobrescritos para verificar se o valor de entrada `err` corresponde aos seus casos de switch.

**Q: Isso afeta a velocidade de cálculo de fórmulas?**  
A: Negligivelmente. A biblioteca procura a string apenas ao renderizar valores de célula, não durante as etapas intermediárias de cálculo.

## Recursos adicionais

- **Documentação**: Explore guias detalhados em [Aspose.Cells Documentation](https://reference.aspose.com/cells/java/)  
- **Download**: Acesse as versões mais recentes em [Aspose Downloads](https://releases.aspose.com/cells/java/)  
- **Purchase**: Compre uma licença para uso comercial em [Aspose Purchase](https://purchase.aspose.com/buy)  
- **Free trial**: Comece com um teste gratuito em [Aspose Free Trial](https://releases.aspose.com/cells/java/)  
- **Temporary license**: Obtenha uma licença temporária via [Aspose Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Support**: Obtenha ajuda da comunidade em [Aspose Support Forum](https://forum.aspose.com/c/cells/9)

---

**Última atualização:** 2026-08-16  
**Testado com:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose

## Tutoriais Relacionados

- [Aspose.Cells Java: Guia de Motor de Cálculo Personalizado](/cells/java/calculation-engine/aspose-cells-java-custom-engine-guide/)
- [Como Usar Aspose Cells – Tutoriais do Motor Excel para Java](/cells/java/calculation-engine/)
- [Dependência Maven do Aspose Cells – Gerencie Conexões de Dados Excel com Aspose.Cells em Java](/cells/java/advanced-features/aspose-cells-java-excel-external-data-connections/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/products-backtop-button >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}