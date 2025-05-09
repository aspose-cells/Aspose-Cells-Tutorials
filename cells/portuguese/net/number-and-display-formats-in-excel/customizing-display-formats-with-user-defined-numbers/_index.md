---
"description": "Aprenda a personalizar formatos de exibição com o Aspose.Cells para .NET. Formate datas, porcentagens e moedas usando este guia passo a passo."
"linktitle": "Personalizando formatos de exibição com números definidos pelo usuário"
"second_title": "API de processamento do Excel Aspose.Cells .NET"
"title": "Personalizando formatos de exibição com números definidos pelo usuário"
"url": "/pt/net/number-and-display-formats-in-excel/customizing-display-formats-with-user-defined-numbers/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Personalizando formatos de exibição com números definidos pelo usuário

## Introdução
Trabalhar com arquivos do Excel geralmente requer formatação personalizada de células para apresentar os dados de uma forma mais significativa e intuitiva. Imagine que você está criando um arquivo do Excel para um relatório. Você não quer apenas números brutos. Você quer que datas, porcentagens e moedas tenham uma aparência elegante e profissional, certo? É aí que entram os formatos de exibição personalizados. Neste tutorial, vamos nos aprofundar no Aspose.Cells para .NET para mostrar como personalizar o formato de exibição de números usando configurações definidas pelo usuário.
## Pré-requisitos
Antes de começar, certifique-se de ter tudo pronto para acompanhar este tutorial. Veja o que você precisa:
- Aspose.Cells para .NET instalado. [Baixe aqui](https://releases.aspose.com/cells/net/).
- Conhecimento básico de C# e .NET framework.
- Uma licença válida para Aspose.Cells. Se você não tiver uma, pegue uma [teste gratuito](https://releases.aspose.com/) ou solicitar um [licença temporária](https://purchase.aspose.com/temporary-license/).
- Um IDE como o Visual Studio.
- .NET Framework 4.0 ou superior.
Se estiver faltando alguma coisa, não se preocupe. Você sempre pode revisitar estes links para baixar os arquivos necessários ou buscar ajuda do [Fórum de suporte Aspose](https://forum.aspose.com/c/cells/9).
## Importar namespaces
Antes de começar a usar o código, você precisa importar os namespaces necessários para acessar todas as funcionalidades necessárias do Aspose.Cells.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Esses dois namespaces serão suas principais ferramentas neste tutorial. Agora, vamos para a parte divertida:
## Etapa 1: Configurando o diretório do projeto
Primeiro, você precisa de um local para armazenar seus arquivos, certo? Vamos criar um diretório para salvar o arquivo Excel resultante. Nesta etapa, também verificaremos se o diretório existe antes de salvar qualquer coisa.
```csharp
// O caminho para o diretório de documentos.
string dataDir = "Your Document Directory";
// Crie um diretório se ele ainda não estiver presente.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- Estamos definindo um `dataDir` variável para armazenar o caminho onde o arquivo de saída do Excel irá.
- Em seguida, verificamos se o diretório existe usando `System.IO.Directory.Exists()`.
- Se o diretório não existir, ele será criado usando `System.IO.Directory.CreateDirectory()`.
## Etapa 2: Crie uma nova pasta de trabalho e adicione uma planilha
Agora que temos nosso diretório, vamos criar uma nova pasta de trabalho do Excel e adicionar uma planilha a ela.
```csharp
// Instanciando um objeto Workbook
Workbook workbook = new Workbook();
// Adicionando uma nova planilha ao objeto Excel
int i = workbook.Worksheets.Add();
// Obtendo a referência da planilha recém-adicionada passando seu índice de planilha
Worksheet worksheet = workbook.Worksheets[i];
```
- Primeiro, criamos um novo `Workbook` objeto. Pense nisso como seu arquivo do Excel.
- Adicionamos uma nova planilha a esta pasta de trabalho usando o `Add()` método e armazenar o índice na variável `i`.
- Referenciamos esta planilha usando o `workbook.Worksheets[i]`.
## Etapa 3: Adicionar data a uma célula e personalizar seu formato
Agora, vamos inserir a data atual em uma célula e formatá-la para ser exibida de forma personalizada. Em vez do formato de data padrão, definiremos um formato personalizado como `d-mmm-yy`.
```csharp
// Adicionando a data atual do sistema à célula "A1"
worksheet.Cells["A1"].PutValue(DateTime.Now);
// Obtendo o estilo da célula A1
Style style = worksheet.Cells["A1"].GetStyle();
// Definir o formato de exibição personalizado para mostrar a data como "d-mmm-aa"
style.Custom = "d-mmm-yy";
// Aplicando o estilo à célula A1
worksheet.Cells["A1"].SetStyle(style);
```
- Adicionamos a data atual do sistema à célula `A1` usando `PutValue(DateTime.Now)`.
- Recuperamos o estilo atual da célula `A1` usando `GetStyle()`.
- Modificamos o estilo da célula definindo `style.Custom = "d-mmm-yy"`, que formata a data para mostrar o dia, o mês abreviado e o ano.
- Por fim, aplicamos o novo estilo à célula com `SetStyle()`.
## Etapa 4: Formatando uma célula como porcentagem
A seguir, vamos trabalhar com números. Adicionaremos um valor numérico a outra célula, digamos `A2`e formate-o como uma porcentagem.
```csharp
// Adicionando um valor numérico à célula "A2"
worksheet.Cells["A2"].PutValue(20);
// Obtendo o estilo da célula A2
style = worksheet.Cells["A2"].GetStyle();
// Definir o formato de exibição personalizado para mostrar o valor como porcentagem
style.Custom = "0.0%";
// Aplicando o estilo à célula A2
worksheet.Cells["A2"].SetStyle(style);
```
- Nós adicionamos o valor `20` para a célula `A2`.
- Recuperamos o estilo da célula `A2` e defina o formato personalizado para `0.0%` para exibir o valor como uma porcentagem (ou seja, 20%).
- Por último, aplicamos o estilo à célula usando `SetStyle()`.
## Etapa 5: Formatando uma célula como moeda
Vamos adicionar outro valor, digamos, à célula `A3`formatá-lo para ser exibido como moeda. Para tornar as coisas mais interessantes, usaremos um formato que exibe valores positivos como moeda em libras e valores negativos em dólares.
```csharp
// Adicionando um valor numérico à célula "A3"
worksheet.Cells["A3"].PutValue(2546);
// Obtendo o estilo da célula A3
style = worksheet.Cells["A3"].GetStyle();
// Definir o formato de exibição personalizado para mostrar o valor como moeda
style.Custom = "£#,##0;[Red]$-#,##0";
// Aplicando o estilo à célula A3
worksheet.Cells["A3"].SetStyle(style);
```
- Nós adicionamos o valor `2546` para a célula `A3`.
- Definimos um formato personalizado `£#,##0;[Red]$-#,##0`, que exibe valores positivos com um símbolo de libra e valores negativos em vermelho com um símbolo de dólar.
- Aplicamos o estilo à célula usando `SetStyle()`.
## Etapa 6: Salvando a pasta de trabalho
A etapa final é salvar a pasta de trabalho como um arquivo Excel. Usaremos o formato Excel 97-2003 para este tutorial.
```csharp
// Salvando o arquivo Excel
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
- O `Save()` O método salva a pasta de trabalho no diretório especificado.
- Nós escolhemos `SaveFormat.Excel97To2003` para garantir compatibilidade com versões mais antigas do Excel.
## Conclusão
Pronto! Acabamos de criar um arquivo do Excel, adicionamos formatos personalizados de data, porcentagem e moeda a células específicas usando o Aspose.Cells para .NET e salvamos o arquivo. A formatação personalizada torna seus arquivos do Excel muito mais legíveis e profissionais. Não se esqueça de explorar outras opções de formatação no Aspose.Cells, como a formatação condicional, para ter ainda mais controle sobre a aparência dos seus dados.
## Perguntas frequentes
### Como posso aplicar opções de formatação mais complexas no Aspose.Cells?
Você pode combinar diferentes estilos de formatação, como cor da fonte, bordas e cores de fundo, com formatos numéricos personalizados.
### Posso aplicar um formato numérico personalizado a um intervalo de células?
Sim, o Aspose.Cells permite que você aplique um estilo a um intervalo de células usando o `Range.SetStyle()` método.
### Em quais outros formatos de arquivo posso salvar a pasta de trabalho?
O Aspose.Cells suporta diversos formatos, incluindo XLSX, CSV e PDF. Basta alterar o `SaveFormat` no `Save()` método.
### Posso formatar números negativos de forma diferente?
Com certeza! Você pode usar formatos numéricos personalizados para exibir números negativos com cores ou símbolos diferentes.
### O Aspose.Cells para .NET é gratuito?
O Aspose.Cells oferece um teste gratuito, mas para funcionalidade completa, você precisará de uma licença válida. Você pode obter uma [licença temporária aqui](https://purchase.aspose.com/temporary-license/).


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}