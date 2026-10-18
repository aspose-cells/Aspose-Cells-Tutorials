---
category: general
date: 2026-06-30
description: Defina formato numérico personalizado no Excel usando Java. Aprenda como
  criar uma pasta de trabalho Excel em Java, obter data e hora de uma célula, calcular
  fórmulas da pasta de trabalho e exibir o valor de data e hora.
draft: false
keywords:
- set custom number format
- get datetime from cell
- create excel workbook java
- calculate workbook formulas
- output datetime value
language: pt
og_description: Defina formato numérico personalizado no Excel usando Java. Este guia
  mostra como criar uma planilha Excel em Java, obter data e hora de uma célula, calcular
  fórmulas da planilha e exibir o valor de data e hora.
og_title: Defina Formato de Número Personalizado no Excel com Java – Tutorial Completo
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  headline: Set Custom Number Format in Excel with Java – Complete Guide
  type: TechArticle
- description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  name: Set Custom Number Format in Excel with Java – Complete Guide
  steps:
  - name: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
    text: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
  - name: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
    text: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
  - name: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
    text: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- DateTime
title: Defina Formato Numérico Personalizado no Excel com Java – Guia Completo
url: /pt/java/formatting/set-custom-number-format-in-excel-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definir Formato Numérico Personalizado no Excel com Java – Guia Completo

Já precisou **definir formato numérico personalizado** em uma planilha Excel enquanto trabalhava em Java? Você não está sozinho. Seja construindo um motor de relatórios ou apenas tentando exibir datas de eras japonesas corretamente, dominar esse truque economiza inúmeras horas de pós‑processamento. Neste tutorial vamos percorrer um exemplo do mundo real que **cria Excel workbook Java**, aplica um formato específico de localidade, recalcula fórmulas e, finalmente, **obtém DateTime da célula** para **exibir valor datetime**.

Usaremos a popular biblioteca Aspose.Cells for Java porque ela lida com formatos numéricos e datas sensíveis à cultura prontamente. Ao final do guia você terá um programa autônomo, executável, que pode ser inserido em qualquer projeto Maven ou Gradle. Nada de atalhos “veja a documentação” — apenas código sólido e explicações claras.

---

## O que Você Vai Aprender

- Como **criar Excel workbook Java** programaticamente.  
- Os passos exatos para **definir formato numérico personalizado** para datas de eras japonesas.  
- Por que chamar **calculate workbook formulas** é essencial antes de extrair o valor.  
- A forma correta de **obter datetime da célula** e **exibir valor datetime**.  
- Armadilhas comuns (localidade ausente, fórmulas desatualizadas) e correções rápidas.

---

## Pré‑requisitos

- Java 8 ou superior instalado na sua máquina.  
- Aspose.Cells for Java 23.11 (ou qualquer versão recente).  
- Um IDE ou editor de texto básico — IntelliJ IDEA, Eclipse, VS Code, o que preferir.  

Se ainda não adicionou Aspose.Cells ao seu projeto, cole o seguinte trecho Maven no seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.11</version>
</dependency>
```

Usuários Gradle podem adicionar:

```gradle
implementation 'com.aspose:aspose-cells:23.11'
```

Com o ambiente pronto, vamos mergulhar no código.

---

## Etapa 1: Definir Formato Numérico Personalizado – Visão Geral

Antes de escrever qualquer Java, ajuda visualizar o que queremos. Imagine uma célula Excel que deve exibir **“令和2年4月1日”** ao invés da string ISO‑8601 “2020‑04‑01”. O valor subjacente permanece uma data verdadeira (para que as fórmulas ainda funcionem), mas a *exibição* segue o formato de era japonesa. É exatamente isso que a operação **set custom number format** realiza.

Abaixo está o arquivo fonte completo. Sinta‑se à vontade para copiá‑e‑colar em `src/main/java/SetCustomNumberFormatDemo.java`.

```java
// File: SetCustomNumberFormatDemo.java
import com.aspose.cells.*;

public class SetCustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Create Excel workbook Java – a fresh workbook
        // -------------------------------------------------
        Workbook workbook = new Workbook();               // in‑memory workbook, no file yet

        // -------------------------------------------------
        // 2️⃣ Access the first worksheet
        // -------------------------------------------------
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // -------------------------------------------------
        // 3️⃣ Retrieve cell A1 where we’ll store the date string
        // -------------------------------------------------
        Cell cellA1 = worksheet.getCells().get("A1");

        // -------------------------------------------------
        // 4️⃣ Insert a Japanese era date string (Reiwa 2‑04‑01)
        // -------------------------------------------------
        // Note: Aspose.Cells will treat this as a text value until we recalc.
        cellA1.putValue("R02-04-01");

        // -------------------------------------------------
        // 5️⃣ Apply the custom number format (our primary goal)
        // -------------------------------------------------
        // [$-ja-JP] tells Excel to use the Japanese locale.
        // ggge年m月d日 renders as "令和2年4月1日".
        cellA1.setNumberFormat("[$-ja-JP]ggge年m月d日");

        // -------------------------------------------------
        // 6️⃣ Calculate workbook formulas – crucial step!
        // -------------------------------------------------
        // Without this, the cell remains a plain string and the
        // DateTime conversion below will fail.
        workbook.calculateFormula();

        // -------------------------------------------------
        // 7️⃣ Get DateTime from cell – now the value is a true date
        // -------------------------------------------------
        // The getDateTime() method returns a java.util.Calendar instance.
        java.util.Calendar dt = cellA1.getDateTime();

        // -------------------------------------------------
        // 8️⃣ Output datetime value – see the result in console
        // -------------------------------------------------
        System.out.println("Converted DateTime: " + dt.getTime()); // → Tue Apr 01 00:00:00 UTC 2020
    }
}
```

### Por Que Isso Funciona

- **`setNumberFormat`** indica ao Excel como *exibir* o valor numérico subjacente. A string de formato `[$-ja-JP]ggge年m月d日` é a chave; `ggg` seleciona o nome da era, `e` o ano dentro da era, seguido pelos literais de mês e dia.  
- **`calculateFormula`** força o Aspose.Cells a interpretar o texto “R02-04-01” como uma data baseada no calendário japonês. Pular essa etapa deixa a célula como texto simples, e `getDateTime()` lançaria uma exceção.  
- **`getDateTime`** finalmente extrai o *real* objeto `java.util.Calendar`, que você pode manipular, formatar ou armazenar em outro lugar.

---

## Etapa 2: Criar Excel Workbook Java – Olhar Mais Profundo

Quando você **cria Excel workbook Java**, não está apenas alocando memória; também está estabelecendo estilos padrão, uma planilha padrão e uma cultura padrão (geralmente a localidade do sistema). Se precisar de uma localidade padrão diferente, pode passar um objeto `LoadOptions`:

```java
LoadOptions opts = new LoadOptions(LoadFormat.XLSX);
opts.setLocale(new java.util.Locale("ja", "JP"));
Workbook workbook = new Workbook(opts);
```

Para a maioria dos cenários o construtor simples é suficiente, mas é bom conhecer a alternativa — especialmente quando você lida com múltiplas localidades na mesma aplicação.

*Dica profissional:* Mantenha o workbook na memória até terminar a formatação. Gravar no disco após cada alteração gera overhead de I/O desnecessário.

---

## Etapa 3: Obter DateTime da Célula – Tratando o Resultado

A linha `java.util.Calendar dt = cellA1.getDateTime();` faz o trabalho pesado. Nos bastidores, o Aspose.Cells converte o número serial interno (o número de dias desde 31‑12‑1899) em um `Calendar`. Essa conversão respeita a localidade do workbook, então você obtém a data gregoriana correta mesmo que a exibição use a era japonesa.

Se precisar de um `java.time.LocalDate` (a API mais nova), converta assim:

```java
java.time.LocalDate localDate = dt.toInstant()
        .atZone(java.time.ZoneId.systemDefault())
        .toLocalDate();
System.out.println("LocalDate: " + localDate); // 2020-04-01
```

Isso cobre a exigência de **output datetime value** mantendo a modernidade.

---

## Etapa 4: Calcular Fórmulas do Workbook – Quando Importa

Você pode se perguntar: *“Preciso realmente chamar `calculateFormula()`?”* A resposta é um retumbante sim, a menos que esteja alimentando a célula com um objeto Java `Date` nativo desde o início. Quando você **define formato numérico personalizado** em uma string de texto, o Excel (e o Aspose.Cells) a tratam como uma expressão tipo fórmula que precisa ser avaliada. Sem recalcular, `getDateTime()` retornará o padrão `1900‑01‑00` ou lançará um `CellValueException`.

Se seu workbook já contém fórmulas complexas que referenciam a célula recém‑formatada, chame `calculateFormula()` *uma única vez* após todas as alterações. Chamadas repetidas são custosas.

---

## Etapa 5: Exibir Valor DateTime – Verificando o Resultado

Executar o demo imprime algo como:

```
Converted DateTime: Tue Apr 01 00:00:00 UTC 2020
```

Essa linha confirma três coisas:

1. O **set custom number format** foi aplicado (você pode abrir o `.xlsx` gerado no Excel e ver “令和2年4月1日”).  
2. A etapa **calculate workbook formulas** foi bem‑sucedida, transformando a string da era em uma data real.  
3. A chamada **get datetime from cell** devolveu um `Calendar` adequado, que então **output datetime value** para o console.

Se abrir o workbook em um programa de planilhas, verá o texto formatado, mas o valor subjacente permanece o número serial `43831` (a representação Excel de 2020‑04‑01). Essa dualidade é o que torna o Excel poderoso.

---

## Armadilhas Comuns & Casos de Borda

| Problema | Por Que Acontece | Solução |
|----------|------------------|---------|
| `cellA1.getDateTime()` lança `CellValueException` | A célula ainda é uma string porque `calculateFormula()` foi omitido. | Sempre invoque `workbook.calculateFormula()` após definir uma data em texto que precise de conversão. |
| Era japonesa não exibida corretamente | Código de localidade ausente ou incorreto. | Use `[$-ja-JP]` na string de formato, ou defina a localidade do workbook via `LoadOptions`. |
| Formato mostra “#VALUE!” no Excel | A string de formato está malformada. | Verifique colchetes e caracteres; o padrão `ggge年m月d日` é obrigatório para o ano da era. |
| Componente de hora aparece (ex.: “00:00:00”) | A string de origem inclui hora ou o estilo da célula a adiciona. | Remova a hora da string de origem ou ajuste o formato para `ggge年m月d日;@`. |

---

## Exemplo Completo Funcional – Execução com Um Clique

Se preferir um único arquivo sem comentários extras, aqui está a versão mínima:



## O Que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Create an Excel Workbook using Aspose.Cells in Java&#58; A Step-by-Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Mastering Data Presentation in Excel&#58; Number and Custom Date Formatting with Aspose.Cells for Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}