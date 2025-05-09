---
"description": "Automatize a formatação de números no Excel usando o Aspose.Cells para .NET. Aprenda a aplicar formatos de data, porcentagem e moeda programaticamente."
"linktitle": "Usando formatos numéricos integrados no Excel programaticamente"
"second_title": "API de processamento do Excel Aspose.Cells .NET"
"title": "Usando formatos numéricos integrados no Excel programaticamente"
"url": "/pt/net/number-and-display-formats-in-excel/using-built-in-number-formats/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Usando formatos numéricos integrados no Excel programaticamente

## Introdução
Neste tutorial, mostraremos como usar os formatos numéricos integrados do Excel com o Aspose.Cells para .NET. Abordaremos tudo, desde a configuração do seu ambiente até a aplicação de diferentes formatos, como datas, porcentagens e moedas. Seja você um profissional experiente ou esteja apenas começando a se familiarizar com o ecossistema .NET, este guia ajudará você a formatar células do Excel com facilidade.
## Pré-requisitos
Antes de mergulhar, certifique-se de ter o seguinte:
- Biblioteca Aspose.Cells para .NET instalada. Você pode [baixe aqui](https://releases.aspose.com/cells/net/).
- Conhecimento prático de C# e programação básica de .NET.
- Visual Studio ou qualquer IDE .NET instalado na sua máquina.
- Uma licença Aspose válida ou [licença temporária](https://purchase.aspose.com/temporary-license/).
- .NET framework instalado (versão 4.0 ou superior).
  
Se estiver faltando alguma das opções acima, siga os links fornecidos para configurar tudo. Pronto? Vamos para a parte divertida!
## Pacotes de importação
Antes de começarmos o tutorial, certifique-se de importar os namespaces necessários para trabalhar com o Aspose.Cells para .NET:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Depois de importá-los, você estará pronto para manipular arquivos do Excel programaticamente. Agora, vamos mergulhar no guia passo a passo!
## Etapa 1: Crie ou acesse sua pasta de trabalho do Excel
Nesta etapa, você criará uma nova pasta de trabalho. Pense nisso como abrir um novo arquivo do Excel, só que por meio de código!
```csharp
// O caminho para o diretório de documentos.
string dataDir = "Your Document Directory";
// Crie um diretório se ele ainda não estiver presente.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Instanciando um objeto Workbook
Workbook workbook = new Workbook();
```
Aqui, estamos simplesmente instanciando um novo `Workbook` objeto. Ele atua como seu arquivo do Excel, pronto para manipulação de dados. Você também pode carregar um arquivo existente informando seu caminho.
## Etapa 2: Acesse a planilha
As pastas de trabalho do Excel podem conter várias planilhas. Nesta etapa, acessaremos a primeira planilha da sua pasta de trabalho:
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Agora estamos acessando a primeira planilha da pasta de trabalho. Se precisar manipular planilhas adicionais, você pode referenciá-las usando o índice ou o nome delas.
## Etapa 3: Adicionar dados às células
Vamos começar a adicionar alguns dados a células específicas. Primeiro, vamos inserir a data atual do sistema na célula "A1":
```csharp
worksheet.Cells["A1"].PutValue(DateTime.Now);
```
Esta linha insere a data atual na célula A1. Muito legal, né? Imagine fazer isso manualmente para centenas de células — seria um pesadelo. Agora, vamos passar para a formatação!
## Etapa 4: formatar a data na célula "A1"
Em seguida, vamos formatar essa data em um formato mais legível, como "15-out-24". É aqui que o Aspose.Cells realmente se destaca:
1. Recuperar o estilo da célula:
```csharp
Style style = worksheet.Cells["A1"].GetStyle();
```
Aqui, estamos capturando o estilo da célula A1. Pense nisso como capturar o "estilo" da célula antes de fazer qualquer ajuste.
2. Defina o formato da data:
```csharp
style.Number = 15;
```
Definindo o `Number` propriedade 15 aplica o formato de data desejado. Este é um código de formato numérico integrado para exibir datas no formato "d-mmm-aa".
3. Aplique o estilo à célula:
```csharp
worksheet.Cells["A1"].SetStyle(style);
```
Esta linha aplica as alterações de estilo à célula. Agora, em vez do formato de data padrão, você verá algo muito mais intuitivo, como "15-out-24".
## Etapa 5: adicione e formate uma porcentagem na célula "A2"
Vamos passar para a formatação de porcentagens. Imagine que você queira inserir um valor e exibi-lo como uma porcentagem. Nesta etapa, adicionaremos um valor numérico à célula "A2" e o formataremos como uma porcentagem:
1. Inserir valor numérico:
```csharp
worksheet.Cells["A2"].PutValue(20);
```
Isso insere o número 20 na célula A2. Você pode estar pensando: "É só um número simples — como transformo em porcentagem?" Bem, estamos prestes a chegar lá.
2. Recupere o estilo e defina o formato percentual:
```csharp
style = worksheet.Cells["A2"].GetStyle();
style.Number = 9;  // Formato como porcentagem
worksheet.Cells["A2"].SetStyle(style);
    ```
Setting the `Number` property to 9 applies the built-in percentage format. Now the value in A2 will be displayed as "2000%." (Yes, 20 is treated as 2000% in percentage formatting).
## Step 6: Add and Format Currency in Cell "A3"
Now, let’s add a numeric value in cell A3 and format it as currency. This is a common use case for financial reports.
1. Insert Numeric Value:
```csharp
worksheet.Cells["A3"].PutValue(2546);
```
Aqui, estamos adicionando 2546 à célula A3. Em seguida, formataremos esse número para que apareça como moeda.
2. Recupere o estilo e defina o formato da moeda:
```csharp
style = worksheet.Cells["A3"].GetStyle();
style.Number = 6;  // Formatar como moeda
worksheet.Cells["A3"].SetStyle(style);
```
Definindo o `Number` A propriedade 6 aplica o formato de moeda. Agora, o valor na célula A3 será exibido como "2.546,00", completo com vírgulas e duas casas decimais.
## Etapa 7: Salve o arquivo do Excel
Agora que aplicamos toda a mágica da formatação, é hora de salvar o arquivo:
```csharp
// Salvando o arquivo Excel
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
Esta linha salva o arquivo Excel no formato Excel 97-2003. Você pode alterar o `SaveFormat` para atender às suas necessidades. E assim, você criou e formatou um arquivo Excel programaticamente!
## Conclusão
Parabéns! Você aprendeu com sucesso a usar o Aspose.Cells para .NET para aplicar formatos numéricos integrados a células em um arquivo do Excel. De datas a porcentagens e moedas, abordamos algumas das necessidades de formatação mais comuns para o processamento de dados do Excel. Agora, em vez de formatar células manualmente, você pode automatizar todo o processo, economizando tempo e reduzindo erros.
## Perguntas frequentes
### Posso aplicar formatos numéricos personalizados usando o Aspose.Cells para .NET?
Sim! Além dos formatos integrados, o Aspose.Cells também suporta formatos numéricos personalizados. Você pode criar formatos altamente específicos usando o `Custom` propriedade no `Style` aula.
### Como posso formatar uma célula como uma moeda com um símbolo específico?
Para aplicar um símbolo de moeda específico, você pode usar a formatação personalizada definindo o `Style.Custom` propriedade.
### Posso formatar linhas ou colunas inteiras?
Com certeza! Você pode aplicar estilos a linhas ou colunas inteiras usando o `Rows` ou `Columns` coleções no `Worksheet` objeto.
### Como posso formatar várias células de uma só vez?
Você pode usar o `Range` objeto para selecionar várias células e aplicar estilos a todas elas de uma só vez.
### Preciso ter o Microsoft Excel instalado para usar o Aspose.Cells?
Não, o Aspose.Cells funciona independentemente do Microsoft Excel, então você não precisa do Excel instalado na sua máquina.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}