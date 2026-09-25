---
category: general
date: 2026-04-07
description: Escreva data e hora no Excel usando C#. Aprenda como inserir data na
  planilha, lidar com o valor de data da célula do Excel e converter datas do calendário
  japonês em apenas alguns passos.
draft: false
keywords:
- write datetime to excel
- excel cell date value
- insert date into worksheet
- convert japanese calendar date
language: pt
og_description: Escreva data e hora no Excel rapidamente. Este guia mostra como inserir
  data na planilha, gerenciar o valor de data da célula do Excel e converter datas
  do calendário japonês com C#.
og_title: Escreva data e hora no Excel – Tutorial passo a passo em C#
tags:
- C#
- Excel automation
- Aspose.Cells
title: Escreva data e hora no Excel – Guia completo para desenvolvedores C#
url: /pt/net/excel-custom-number-date-formatting/write-datetime-to-excel-complete-guide-for-c-developers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Escrevendo datetime no Excel – Guia Completo para Desenvolvedores C#

Já precisou **escrever datetime no Excel** mas não tinha certeza de qual chamada de API realmente armazena uma data correta do Excel? Você não está sozinho. Em muitas ferramentas corporativas precisamos inserir um `DateTime` C# em uma planilha, e o resultado deve se comportar como uma verdadeira data do Excel—ordenável, filtrável e pronta para tabelas dinâmicas.  

Neste tutorial vamos percorrer os passos exatos para *inserir data na planilha* usando Aspose.Cells, explicar por que definir a cultura é importante e até mostrar como **converter data do calendário japonês** em um `DateTime` regular antes de gravá‑la. Ao final, você terá um trecho de código autônomo que pode copiar‑colar em qualquer projeto .NET.

## O que você precisará

- **.NET 6+** (ou qualquer versão recente do .NET; o código também funciona no .NET Framework)  
- **Aspose.Cells for .NET** – um pacote NuGet que permite manipular arquivos Excel sem precisar do Office instalado.  
- Um entendimento básico de `DateTime` C# e culturas.  

Sem bibliotecas extras, sem interop COM e sem necessidade de instalação do Excel. Se você já tem uma instância de planilha (`ws`), está pronto para prosseguir.

## Etapa 1: Configurar a Cultura Japonesa (Converter Data do Calendário Japonês)

Quando você recebe uma data como `"R02/05/01"` (Reiwa 2, 1º de maio) é necessário informar ao .NET como interpretar os símbolos de era. O calendário japonês não é o calendário gregoriano padrão, então criamos um `CultureInfo` que substitui seu calendário por `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;
using Aspose.Cells;   // Make sure Aspose.Cells is referenced

// Assume you already have a worksheet instance named "ws"
Worksheet ws = /* your worksheet instance */;

// 1️⃣ Configure a Japanese culture that uses the Japanese calendar
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

**Por que isso importa:**  
Se você analisar a string com a cultura padrão, o .NET lançará uma exceção de formato porque não consegue mapear `R` (a era Reiwa) para um ano. Ao substituir por `JapaneseCalendar`, o analisador entende os símbolos de era e os traduz para o ano gregoriano correto.

## Etapa 2: Analisar a String baseada em Era em um `DateTime`

Agora que a cultura está pronta, podemos chamar com segurança `DateTime.ParseExact`. A string de formato `"ggyy/MM/dd"` indica ao analisador:

- `gg` – designador de era (ex.: `R` para Reiwa)  
- `yy` – ano de dois dígitos dentro da era  
- `MM/dd` – mês e dia.

```csharp
// 2️⃣ Parse a date string in the Japanese era format (ggyy/MM/dd)
string japaneseDate = "R02/05/01";          // Reiwa 2, May 1st
DateTime parsedDate = DateTime.ParseExact(
    japaneseDate,
    "ggyy/MM/dd",
    japaneseCulture,
    DateTimeStyles.None
);
```

**Dica profissional:** Se você puder receber datas em outros formatos (ex.: `"Heisei 30/12/31"`), envolva a análise em um `try/catch` e recorra a `DateTime.TryParseExact`. Isso impede que todo o seu processo de importação falhe por causa de uma única linha inválida.

## Etapa 3: Escrever o `DateTime` em uma Célula Excel (Valor de Data da Célula Excel)

Aspose.Cells trata um `DateTime` .NET como uma data nativa do Excel quando você usa `PutValue`. A biblioteca converte automaticamente os ticks no número serial do Excel (o número de dias desde 1900‑01‑00). Isso significa que a célula exibirá um **valor de data de célula Excel** adequado e você pode formatá‑la posteriormente usando os estilos de data incorporados do Excel.

```csharp
// 3️⃣ Write the resulting DateTime value into cell C1 of the worksheet
Cell targetCell = ws.Cells["C1"];
targetCell.PutValue(parsedDate);

// Optional: apply a standard date format so users see "yyyy-MM-dd"
targetCell.Style.Number = 14;   // built‑in Excel format ID for "m/d/yy"
```

**O que você verá no Excel:**  
A célula C1 agora contém o número serial `44796`, que o Excel renderiza como `2020‑05‑01` (ou qualquer formato que você aplicou). O valor subjacente é uma data real, não uma string, portanto a ordenação funciona como esperado.

## Etapa 4: Salvar a Pasta de Trabalho (Conclusão)

Se ainda não salvou a pasta de trabalho, faça isso agora. Esta etapa não trata estritamente de gravar o datetime, mas completa o fluxo de trabalho.

```csharp
// Save the workbook to a file (or a MemoryStream if you need it in‑memory)
Workbook workbook = ws.Workbook;   // get the parent workbook
workbook.Save("Output.xlsx", SaveFormat.Xlsx);
```

É isso—quatro etapas concisas, e você conseguiu **escrever datetime no Excel**, lidando com uma data de era japonesa ao longo do caminho.

---

![exemplo de escrita de datetime no excel](/images/write-datetime-to-excel.png "Captura de tela mostrando um projeto C# escrevendo um DateTime na célula C1 do Excel")

*A imagem acima ilustra o arquivo Excel final com a data exibida corretamente na célula C1.*

## Perguntas Frequentes & Casos Limite

### E se a variável da planilha ainda não estiver pronta?

Você pode criar uma nova pasta de trabalho dinamicamente:

```csharp
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];   // default first sheet
```

### Como preservar a string original da era japonesa na planilha?

Se você precisar tanto da string original quanto da data analisada, escreva‑as em células adjacentes:

```csharp
ws.Cells["B1"].PutValue(japaneseDate);   // original text
ws.Cells["C1"].PutValue(parsedDate);     // parsed DateTime
```

### Isso funciona com versões mais antigas do .NET?

Sim. `JapaneseCalendar` existe desde o .NET 2.0, e Aspose.Cells suporta .NET Framework 4.5+. Apenas certifique‑se de referenciar o assembly correto.

### E quanto aos fusos horários?

`DateTime.ParseExact` retorna um **Kind** de `Unspecified`. Se as datas de origem forem UTC, converta‑as primeiro:

```csharp
DateTime utcDate = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
DateTime localDate = utcDate.ToLocalTime();
targetCell.PutValue(localDate);
```

### Posso definir um formato de data personalizado (ex.: “yyyy年MM月dd日”)?

Absolutamente. Use a propriedade `Style.Custom`:

```csharp
targetCell.Style.Custom = "yyyy\"年\"mm\"月\"dd\"日\"";
```

Agora o Excel mostrará `2020年05月01日` enquanto ainda armazena um valor de data real.

## Recapitulação

Cobremos tudo o que você precisa para **escrever datetime no Excel** a partir de C#:

1. **Configure** uma cultura japonesa com `JapaneseCalendar` para **converter datas do calendário japonês**.  
2. **Parse** uma string baseada em era usando `DateTime.ParseExact`.  
3. **Insert** o `DateTime` resultante em uma célula, garantindo um **valor de data de célula Excel** adequado.  
4. **Save** a pasta de trabalho para que os dados persistam.

Com essas quatro etapas você pode **inserir data na planilha** com segurança, independentemente do formato de origem. O código é totalmente executável, requer apenas Aspose.Cells e funciona em qualquer runtime .NET moderno.

## Próximos Passos?

- **Importação em massa:** Percorrer linhas de um CSV, analisar cada data japonesa e escrevê‑las em células consecutivas.  
- **Estilização:** Aplicar formatação condicional para destacar datas vencidas.  
- **Desempenho:** Usar cache de `WorkbookDesigner` ou `CellStyle` ao lidar com milhares de linhas.  

Sinta‑se à vontade para experimentar—trocar a era japonesa pelo calendário gregoriano, mudar a célula de destino ou exportar para um formato de arquivo diferente (CSV, ODS). A ideia central permanece a mesma: analisar, converter e **escrever datetime no Excel** com confiança.

Boa codificação, e que suas planilhas sempre ordenem corretamente!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}