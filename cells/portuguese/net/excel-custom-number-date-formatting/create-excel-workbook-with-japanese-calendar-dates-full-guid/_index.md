---
category: general
date: 2026-06-17
description: Criar uma pasta de trabalho do Excel e escrever a data no Excel usando
  o calendário japonês. Aprenda a usar CultureInfo, definir a data/hora da célula
  e lidar com os formatos de era japonesa.
draft: false
keywords:
- create excel workbook
- write date to excel
- use japanese calendar
- how to use cultureinfo
- set cell datetime
language: pt
og_description: Crie uma pasta de trabalho do Excel e escreva a data no Excel usando
  o calendário japonês. Este guia mostra como usar CultureInfo e definir a data e
  hora da célula corretamente.
og_title: Criar Pasta de Trabalho Excel – Manipulação de Datas do Calendário Japonês
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Create Excel workbook and write date to Excel using Japanese calendar.
    Learn how to use CultureInfo, set cell datetime, and handle Japanese era formats.
  headline: Create Excel Workbook with Japanese Calendar Dates – Full Guide
  type: TechArticle
- description: Create Excel workbook and write date to Excel using Japanese calendar.
    Learn how to use CultureInfo, set cell datetime, and handle Japanese era formats.
  name: Create Excel Workbook with Japanese Calendar Dates – Full Guide
  steps:
  - name: What if the Japanese era changes next year?
    text: The `CultureInfo` object always references the latest era data baked into
      Windows/.NET. When a new era begins, Microsoft updates the underlying calendar
      data via Windows updates. So your code will continue to work without changes—just
      keep the OS patched.
  - name: Can I write multiple dates in a loop?
    text: Absolutely. Just move the parsing and `PutValue` logic inside a `for` loop
      or LINQ query. Remember to adjust the cell address each iteration (e.g., `"A"
      + rowNumber`).
  - name: How does this differ from using `DateTimeOffset`?
    text: '`DateTimeOffset` includes timezone information, which Excel ignores. For
      pure date values, stick with `DateTime`. If you need to preserve UTC offsets,
      store the offset in a separate column.'
  type: HowTo
tags:
- excel
- csharp
- cultureinfo
- datetime
title: Criar Pasta de Trabalho Excel com Datas do Calendário Japonês – Guia Completo
url: /pt/net/excel-custom-number-date-formatting/create-excel-workbook-with-japanese-calendar-dates-full-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Pasta de Trabalho Excel com Datas do Calendário Japonês – Guia Completo

Já precisou **criar uma pasta de trabalho Excel** que respeite o calendário de eras japonês? Você não está sozinho—muitos desenvolvedores se deparam com dificuldades ao tentar analisar datas como “令和3年5月1日” e inseri‑las em uma planilha. A boa notícia? É muito simples quando você conhece os passos corretos.

Neste tutorial vamos percorrer como **escrever data no Excel** usando convenções do **calendário japonês**, explicar **como usar CultureInfo** para análise de eras e mostrar o código exato para **definir a data/hora da célula**. Ao final, você terá um exemplo pronto‑para‑executar que pode ser inserido em qualquer projeto .NET.

## Pré‑requisitos — O Que Você Precisa

- .NET 6+ (ou .NET Framework 4.7+). As APIs que usamos fazem parte da biblioteca de classes base, portanto nenhum pacote NuGet extra é necessário para a parte de análise de datas.
- Uma referência a uma biblioteca de planilhas que forneça as classes `Workbook`, `Worksheet` e `Cell`. O trecho abaixo usa **Aspose.Cells**, mas você pode substituí‑lo por EPPlus, ClosedXML ou qualquer outra biblioteca com um modelo de objetos semelhante.
- Conhecimento básico de C#—nada sofisticado, apenas o suficiente para acompanhar.
- (Opcional) Visual Studio 2022 ou VS Code para um teste rápido.

Tudo pronto? Ótimo—vamos começar.

## Criar Pasta de Trabalho Excel – Visão Geral Passo a Passo

A seguir está o roteiro de alto nível que seguiremos:

1. **Inicializar** uma nova pasta de trabalho e obter a primeira planilha.  
2. **Definir** a cultura do calendário japonês usando `CultureInfo`.  
3. **Analisar** uma string de data em era japonesa para um `DateTime`.  
4. **Escrever** a data analisada em uma célula específica.  
5. **Salvar** a pasta de trabalho para que você possa abri‑la no Excel e verificar o resultado.

Cada passo está detalhado em sua própria seção, com código, explicações e alguns “pro tips” que você vai apreciar mais adiante.

![Captura de tela da criação da pasta de trabalho Excel](https://example.com/create-excel-workbook.png "Captura de tela de uma pasta de trabalho Excel recém‑criada")

## Passo 1: Criar Pasta de Trabalho Excel e Acessar a Primeira Planilha

A primeira coisa que precisamos é um objeto de pasta de trabalho novo. Pense nele como uma tela em branco onde cada operação subsequente será pintada.

```csharp
using Aspose.Cells;          // Replace with your library's namespace
using System;
using System.Globalization;

// Step 1: Instantiate a new workbook
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0)
Worksheet ws = workbook.Worksheets[0];
```

**Por que isso importa:**  
Criar a pasta de trabalho programaticamente permite evitar a sobrecarga de abrir um arquivo existente apenas para adicionar uma data. Também garante que a pasta de trabalho comece em um estado conhecido e limpo—perfeito para geração automática de relatórios.

> **Pro tip:** Se você estiver usando EPPlus, o equivalente seria `var package = new ExcelPackage(); var ws = package.Workbook.Worksheets.Add("Sheet1");`.

## Passo 2: Usar Calendário Japonês – Definindo o CultureInfo

Datas japonesas são expressas usando eras (ex.: “令和” para Reiwa). O .NET pode lidar com isso via uma *cultura* que inclui o calendário japonês.

```csharp
// Step 2: Define the Japanese era culture
CultureInfo japaneseEra = new CultureInfo("ja-JP-u-ca-japanese");
```

**O que está acontecendo aqui?**  
O identificador `"ja-JP-u-ca-japanese"` indica ao .NET para usar a localidade japonesa **e** o calendário japonês (`ca-japanese`). Isso significa que qualquer análise ou formatação de data entenderá automaticamente os símbolos de era.

> **Armadilha comum:** Esquecer o sufixo `-u-ca-japanese` fará o analisador tratar a string como uma data gregoriana padrão, resultando em um `FormatException`.

## Passo 3: Analisar uma String de Data que Usa a Era Japonesa

Agora transformamos uma data japonesa legível por humanos em um objeto `DateTime` que o Excel pode armazenar.

```csharp
// Step 3: Parse the Japanese era date string
DateTime eraDate = DateTime.Parse("令和3年5月1日", japaneseEra);
```

**Por que analisar dessa forma?**  
`DateTime.Parse` respeita a cultura que passamos, então `"令和3年5月1日"` torna‑se **1 de maio de 2021** no calendário gregoriano (Reiwa 3 corresponde a 2021). O `DateTime` resultante é independente de fuso horário, exatamente o que o Excel espera para o valor de uma célula.

> **Caso extremo:** Se a string contiver mês ou dia sem zero à esquerda (ex.: “5月1日”), o analisador ainda funciona—apenas certifique‑se de que o nome da era corresponda à era atual, ou você receberá um erro.

## Passo 4: Escrever Data no Excel – Definindo o DateTime da Célula

Com o `DateTime` em mãos, podemos inseri‑lo em qualquer célula. Aqui usamos **A1**, mas você pode usar qualquer endereço que preferir.

```csharp
// Step 4: Write the parsed date into cell A1
Cell cell = ws.Cells["A1"];
cell.PutValue(eraDate);               // Aspose.Cells method
cell.Style.Number = 14;               // Apply a date format (e.g., mm/dd/yyyy)
```

**Explicação:**  
- `PutValue` detecta automaticamente o tipo .NET e o armazena como um *Date* do Excel (um número de ponto flutuante nos bastidores).  
- Definir `cell.Style.Number = 14` aplica o formato de data curta interno do Excel, garantindo que o valor apareça como uma data legível ao abrir o arquivo.

> **Bibliotecas alternativas:** Com EPPlus você escreveria `cell.Value = eraDate; cell.Style.Numberformat.Format = "mm/dd/yyyy";`.

## Passo 5: Salvar a Pasta de Trabalho – Verificando o Resultado

Por fim, gravamos a pasta de trabalho no disco para que você possa abri‑la no Excel e confirmar que a data aparece corretamente.

```csharp
// Step 5: Save the workbook (adjust the path as needed)
string outputPath = @"C:\Temp\JapaneseDateDemo.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Ao abrir o arquivo, a célula **A1** deve exibir **1/5/2021** (ou o formato de data que você escolheu). Se mudar a cultura para outra—por exemplo, `"ja-JP-u-ca-japanese"` com uma era diferente—você verá a conversão acontecer automaticamente.

> **Pro tip:** Se precisar que a célula retenha o formato de era japonesa ao ser aberta no Excel, você pode aplicar um formato numérico personalizado como `[$-ja-JP]ggge"年"M"月"d"日"`—mas isso está além do escopo deste guia básico.

## Perguntas Frequentes & Armadilhas

### E se a era japonesa mudar no próximo ano?

O objeto `CultureInfo` sempre referencia os dados de era mais recentes incorporados ao Windows/.NET. Quando uma nova era começa, a Microsoft atualiza os dados do calendário subjacentes via atualizações do Windows. Assim, seu código continuará funcionando sem alterações—basta manter o sistema operacional atualizado.

### Posso escrever várias datas em um loop?

Com certeza. Basta mover a lógica de análise e `PutValue` para dentro de um `for` ou consulta LINQ. Lembre‑se de ajustar o endereço da célula a cada iteração (ex.: `"A" + rowNumber`).

### Como isso difere de usar `DateTimeOffset`?

`DateTimeOffset` inclui informações de fuso horário, que o Excel ignora. Para valores puramente de data, use `DateTime`. Se precisar preservar deslocamentos UTC, armazene o offset em uma coluna separada.

## Exemplo Completo Funcional (Todos os Passos Combinados)

Abaixo está um programa pronto‑para‑copiar‑e‑colar que reúne tudo. Ele compila com .NET 6 e Aspose.Cells, mas você pode substituir as chamadas da biblioteca conforme mencionado anteriormente.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class JapaneseDateExcelDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Define the Japanese calendar culture (Japanese era)
        CultureInfo japaneseEra = new CultureInfo("ja-JP-u-ca-japanese");

        // 3️⃣ Parse a date string that uses the Japanese era format
        //    Example: Reiwa 3 (2021) May 1st
        DateTime eraDate = DateTime.Parse("令和3年5月1日", japaneseEra);

        // 4️⃣ Write the parsed date into cell A1
        Cell cell = ws.Cells["A1"];
        cell.PutValue(eraDate);
        cell.Style.Number = 14; // Short date format

        // 5️⃣ (Optional) Save the workbook to see the result
        string outputPath = @"C:\Temp\JapaneseDateDemo.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Saída esperada:**  
Ao executar o programa, ele imprime `Workbook saved to C:\Temp\JapaneseDateDemo.xlsx`. Abrindo o arquivo, você verá **1/5/2021** (ou a data curta do seu locale) na célula **A1**.

## Recapitulação – O Que Cobremos

- **Criar pasta de trabalho Excel** do zero usando uma biblioteca .NET de planilhas.  
- **Escrever data no Excel** analisando uma string de era japonesa com `CultureInfo`.  
- **Usar calendário japonês** (`ja-JP-u-ca-japanese`) para lidar automaticamente com símbolos de era.  
- **Como usar CultureInfo** para calendários personalizados e análise específica de locale.  
- **Definir datetime da célula** e aplicar um formato numérico de data para exibição correta.

## Próximos Passos & Tópicos Relacionados

Agora que você domina a inserção de datas japonesas, considere explorar:

- **Formatar células com formatos numéricos personalizados de era japonesa** (`ggge"年"M"月"d"日"`).  
- **Gerar relatórios multilíngues** alternando `CultureInfo` dinamicamente.  
- **Importar em massa datas de CSV** onde cada linha usa sistemas de calendário diferentes.  
- **Automatizar a criação de pastas de trabalho** com modelos—ideal para faturamento ou folha de pagamento.

Se estiver curioso sobre como lidar com outros calendários não gregorianos (ex.: Hebraico, Islâmico), o mesmo padrão `CultureInfo` se aplica—basta trocar o identificador de cultura.

---

Sinta‑se à vontade para experimentar: altere a string de data, teste outra célula ou até adicione um gráfico que referencie a coluna de datas. A flexibilidade do `CultureInfo` do .NET combinada com uma biblioteca Excel robusta torna tudo isso possível.

Feliz codificação, e que suas planilhas sempre mostrem a era correta!

## O Que Você Deve Aprender a Seguir?

Os tutoriais abaixo cobrem tópicos intimamente relacionados que expandem as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Excel Automation with Aspose.Cells .NET&#58; Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Load an Excel Workbook & Set Printer Sizes Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/load-workbook-set-printer-sizes-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}