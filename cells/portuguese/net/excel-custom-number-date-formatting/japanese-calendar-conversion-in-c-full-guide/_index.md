---
category: general
date: 2026-07-13
description: Conversão de calendário japonês em C# com código passo a passo. Aprenda
  a extrair DateTime do Excel e lidar eficientemente com datas de eras japonesas.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- japanese calendar conversion
- extract datetime from excel
- excel date parsing c#
- aspnet excel cultureinfo
- japanese era date handling
language: pt
lastmod: 2026-07-13
og_description: Conversão do calendário japonês em C# explicada. Domine a extração
  de DateTime de células do Excel e a conversão de strings de era japonesa para datas
  gregorianas.
og_image_alt: Code screenshot illustrating Japanese calendar conversion in a C# console
  app
og_title: Conversão do Calendário Japonês em C# – Guia Completo de Programação
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Japanese calendar conversion in C# with step‑by‑step code. Learn how
    to extract DateTime from Excel and handle Japanese era dates efficiently.
  headline: Japanese Calendar Conversion in C# – Full Guide
  type: TechArticle
- description: Japanese calendar conversion in C# with step‑by‑step code. Learn how
    to extract DateTime from Excel and handle Japanese era dates efficiently.
  name: Japanese Calendar Conversion in C# – Full Guide
  steps:
  - name: Recognizes era names (e.g., *Meiji*, *Taishō*, *Shōwa*, *Heisei*, *Reiwa*).
    text: Recognizes era names (e.g., *Meiji*, *Taishō*, *Shōwa*, *Heisei*, *Reiwa*).
  - name: Parses the year number relative to the era’s start.
    text: Parses the year number relative to the era’s start.
  - name: Constructs the corresponding Gregorian `DateTime`.
    text: Constructs the corresponding Gregorian `DateTime`.
  type: HowTo
tags:
- C#
- Excel
- DateTime
- Localization
title: Conversão do Calendário Japonês em C# – Guia Completo
url: /pt/net/excel-custom-number-date-formatting/japanese-calendar-conversion-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Conversão de Calendário Japonês em C# – Guia Completo

Já precisou de **japanese calendar conversion** ao extrair dados de uma planilha Excel? Você não é o único coçando a cabeça sobre como transformar “Reiwa 3‑04‑01” em um `DateTime` .NET adequado. Neste tutorial, vamos percorrer uma solução limpa, de ponta a ponta, que não só converte datas de era japonesa, mas também mostra como **extract datetime from excel** células usando Aspose.Cells. Ao final, você terá um aplicativo console pronto para executar e uma compreensão sólida de por que as configurações de cultura são importantes.

Cobriremos tudo o que você pode perguntar: definir a cultura correta, analisar a string da era, lidar com casos extremos como anos bissextos e, finalmente, imprimir o resultado gregoriano. Nenhuma documentação externa necessária — basta copiar, colar e executar.

## Pré-requisitos

- .NET 6.0 ou posterior (o código funciona tanto no .NET Core quanto no .NET Framework)
- Aspose.Cells para .NET (pacote NuGet de avaliação gratuita `Aspose.Cells`)
- Familiaridade básica com C# e aplicativos de console
- Um arquivo Excel (ou uma nova pasta de trabalho) onde a data está armazenada como uma string no formato de era japonesa

Se você estiver sem nenhum desses, obtenha o pacote NuGet com:

```bash
dotnet add package Aspose.Cells
```

Agora vamos mergulhar.

## Etapa 1: Criar uma Pasta de Trabalho e Definir a Cultura Japonesa

A primeira coisa que você precisa fazer é informar ao Aspose.Cells que a pasta de trabalho deve interpretar datas usando o calendário japonês. É aqui que **japanese calendar conversion** realmente começa.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook instance
        Workbook workbook = new Workbook();

        // 2️⃣ Apply Japanese culture (Japanese calendar) to the workbook settings
        workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("ja-JP-u-ca-japanese");

        // The rest of the steps follow...
```

**Por que isso importa:** `CultureInfo` carrega não apenas o idioma, mas também informações de calendário. Ao mudar para `"ja-JP-u-ca-japanese"` habilitamos a biblioteca a entender nomes de eras como *Reiwa* ou *Heisei* quando aparecem nas células.

## Etapa 2: Escrever uma Data de Era Japonesa em uma Célula

Para demonstração, vamos colocar uma string de era japonesa diretamente na célula **A1**. Em um cenário real, você provavelmente estaria lendo uma pasta de trabalho existente, mas o princípio permanece o mesmo.

```csharp
        // 3️⃣ Write a Japanese era date string into cell A1 (row 0, column 0)
        workbook.Worksheets[0].Cells[0, 0].PutValue("Reiwa 3-04-01");
```

> **Dica profissional:** Se o Excel de origem já armazenar datas como números seriais adequados do Excel, você pode pular a etapa `PutValue` e ir direto à extração. A lógica de conversão funciona de qualquer forma.

## Etapa 3: Extrair DateTime do Excel – O Núcleo de “extract datetime from excel”

Agora vem a parte onde nós **extract datetime from excel**. Aspose.Cells fornece um método conveniente `GetDateTime` que respeita as configurações de cultura da pasta de trabalho.

```csharp
        // 4️⃣ Retrieve the cell value as a .NET DateTime object
        DateTime gregorianDate = workbook.Worksheets[0].Cells[0, 0].GetDateTime();
```

Nos bastidores, o Aspose observa a cultura que definimos anteriormente, analisa “Reiwa 3‑04‑01” e retorna a data gregoriana equivalente (`2021‑04‑01`).

## Etapa 4: Exibir o Resultado

Finalmente, vamos imprimir a data convertida no console para que você possa verificar se a **japanese calendar conversion** foi bem-sucedida.

```csharp
        // 5️⃣ Show the converted Gregorian date
        Console.WriteLine(gregorianDate.ToString("yyyy‑MM‑dd"));
        // Expected output: 2021‑04‑01
    }
}
```

Execute o programa (`dotnet run`) e você deverá ver:

```
2021‑04‑01
```

Esse é o ciclo completo: criar uma pasta de trabalho, definir a cultura japonesa, escrever uma data de era, extrair um `DateTime` e exibi-lo.

---

## Mergulho Profundo: Como o Calendário Japonês Funciona no .NET

O calendário japonês é um sistema *lunissolar* que agrupa anos em eras nomeadas após o imperador reinante. A classe `JapaneseCalendar` do .NET mapeia cada era para um intervalo de anos gregorianos. Quando você solicita um `CultureInfo` que inclui `-u-ca-japanese`, o runtime automaticamente:

1. Reconhece nomes de eras (por exemplo, *Meiji*, *Taishō*, *Shōwa*, *Heisei*, *Reiwa*).
2. Analisa o número do ano relativo ao início da era.
3. Constrói o correspondente `DateTime` gregoriano.

Se você precisar converter no sentido oposto — de gregoriano para era japonesa — pode usar:

```csharp
var japaneseCal = new System.Globalization.JapaneseCalendar();
int era = japaneseCal.GetEra(gregorianDate);
string eraName = japaneseCal.Eras[era - 1]; // .Eras is zero‑based
int yearInEra = japaneseCal.GetYear(gregorianDate);
Console.WriteLine($"{eraName} {yearInEra:D2}-{gregorianDate:MM-dd}");
```

### Lidando com Casos Extremos

| Situação | O que observar | Correção sugerida |
|-----------|-------------------|---------------|
| **Missing era name** (e.g., “03‑04‑01”) | `GetDateTime` lançará uma `FormatException`. | Pré‑valide a string ou recorra a `DateTime.ParseExact` com um padrão customizado. |
| **Future era** (new emperor) | O `JapaneseCalendar` atual pode não conhecer a nova era até uma atualização do SO. | Atualize o runtime .NET ou use uma tabela de mapeamento customizada até que o SO seja atualizado. |
| **Mixed calendars in one workbook** | Algumas células podem usar o calendário gregoriano enquanto outras usam o japonês. | Defina `CultureInfo` por célula usando `cell.Style.CultureInfo` se necessário. |

## Extraindo DateTime de Arquivos Excel Existentes

Se você já tem um arquivo `.xlsx` com datas japonesas, o código de extração é quase idêntico — basta substituir a criação da pasta de trabalho por uma chamada de carregamento:

```csharp
Workbook workbook = new Workbook("Path/To/YourFile.xlsx");
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("ja-JP-u-ca-japanese");

// Assuming the date is in B2 (row 1, column 1)
DateTime dateFromFile = workbook.Worksheets[0].Cells[1, 1].GetDateTime();
Console.WriteLine(dateFromFile);
```

Observe como **extract datetime from excel** permanece a mesma chamada de método; a única etapa extra é carregar o arquivo.

## Exemplo Completo Funcional (Pronto para Copiar‑Colar)

Abaixo está o programa completo que você pode inserir em um projeto de console. Ele inclui todas as diretivas `using` necessárias, comentários e tratamento de erros para uma sensação de nível de produção.

```csharp
using System;
using Aspose.Cells;

class JapaneseCalendarDemo
{
    static void Main()
    {
        try
        {
            // Initialize workbook
            Workbook wb = new Workbook();

            // Apply Japanese calendar culture
            wb.Settings.CultureInfo = new System.Globalization.CultureInfo("ja-JP-u-ca-japanese");

            // Insert a Japanese era date string (could be read from an existing file)
            wb.Worksheets[0].Cells[0, 0].PutValue("Reiwa 3-04-01");

            // Extract as .NET DateTime – this is the core of "extract datetime from excel"
            DateTime gregDate = wb.Worksheets[0].Cells[0, 0].GetDateTime();

            // Output in ISO format
            Console.WriteLine(gregDate.ToString("yyyy-MM-dd"));
        }
        catch (Exception ex)
        {
            // Simple error handling – in real apps you might log this
            Console.Error.WriteLine($"Error during conversion: {ex.Message}");
        }
    }
}
```

**Saída esperada no console**

```
2021-04-01
```

Execute-o, e você verá a data gregoriana que corresponde à entrada da era japonesa.

## Perguntas Frequentes

**Q: Isso funciona com arquivos Excel mais antigos (.xls)?**  
Sim. Aspose.Cells abstrai o formato do arquivo, então a mesma chamada `GetDateTime` funciona tanto para `.xls` quanto para `.xlsx`.

**Q: E se a célula contiver uma data real do Excel (número serial) em vez de uma string?**  
Aspose ainda respeitará a cultura da pasta de trabalho e retornará o `DateTime` gregoriano correto. Nenhuma análise extra necessária.

**Q: Posso converter uma coluna inteira de datas japonesas de uma vez?**  
Absolutamente. Percorra as linhas:

```csharp
for (int i = 0; i < worksheet.Cells.MaxDataRow + 1; i++)
{
    DateTime dt = worksheet.Cells[i, 0].GetDateTime();
    // Do something with dt
}
```

**Q: Há impacto de desempenho ao definir a cultura?**  
Negligível para conjuntos de dados típicos. A cultura é aplicada uma vez por pasta de trabalho, não por célula.

## Conclusão

Acabamos de concluir um walkthrough de **japanese calendar conversion** que mostra exatamente como **extract datetime from excel** usando Aspose.Cells. Ao definir o `CultureInfo` da pasta de trabalho para `"ja-JP-u-ca-japanese"` você desbloqueia a análise perfeita de strings de era como *Reiwa 3‑04‑01* em objetos `DateTime` padrão do .NET. O código é compacto, robusto e pronto para produção.

O que vem a seguir? Tente carregar uma pasta de trabalho real, converter uma coluna inteira ou até escrever as datas gregorianas de volta em uma nova planilha. Você também pode explorar outras localidades — calendário republicano francês, calendário islâmico Hijri — trocando a string de cultura. O padrão permanece o mesmo.

Tem alguma variação que gostaria de compartilhar? Deixe um comentário, e feliz codificação!

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Domine o Sistema de Data 1904 no Excel Usando Aspose.Cells Java para Operações de Célula Eficazes](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Conversão de Referência de Célula do Excel Usando Aspose.Cells .NET: Um Guia Abrangente](/cells/english/net/cell-operations/excel-cell-reference-conversion-aspose-cells-net/)
- [Domine a Conversão de HTML para Excel Usando Aspose.Cells para .NET](/cells/english/net/workbook-operations/aspose-cells-net-html-layout-conversion/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}