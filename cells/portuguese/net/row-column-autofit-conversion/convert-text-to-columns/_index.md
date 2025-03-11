---
title: Converter texto em colunas no Aspose.Cells .NET
linktitle: Converter texto em colunas no Aspose.Cells .NET
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda a converter texto em colunas sem esforço usando o Aspose.Cells para .NET neste tutorial detalhado passo a passo.
weight: 15
url: /pt/net/row-column-autofit-conversion/convert-text-to-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converter texto em colunas no Aspose.Cells .NET

## Introdução
No mundo acelerado de gerenciamento de dados de hoje, eficiência é essencial. Seja você um analista que processa números ou um profissional de negócios que prepara relatórios, muitas vezes você precisa manipular dados de forma rápida e precisa. Se você já teve que lidar com nomes em uma única célula que precisava dividir em colunas separadas, sabe o quão tedioso isso pode ser. Felizmente, o Aspose.Cells para .NET fornece uma solução elegante para dividir texto em colunas. Neste guia, vamos percorrer o processo de conversão de texto em colunas usando o Aspose.Cells.
## Pré-requisitos
Antes de começarmos, vamos garantir que você esteja tudo pronto. Aqui está o que você precisa:
1.  Visual Studio: Certifique-se de ter o Visual Studio instalado em sua máquina. Se você ainda não o tem, você pode baixá-lo em[Site da Microsoft](https://visualstudio.microsoft.com/downloads/).
2. .NET Framework: Certifique-se de que você está trabalhando em um projeto que tem como alvo uma versão compatível do .NET Framework. O Aspose.Cells é compatível com .NET Core, .NET Framework e outras plataformas.
3.  Biblioteca Aspose.Cells: Você precisa ter a biblioteca Aspose.Cells baixada e referenciada em seu projeto. Você pode obtê-la em[Página de downloads do Aspose](https://releases.aspose.com/cells/net/).
4. Conhecimento básico de C#: A familiaridade com a programação em C# ajudará você a entender este tutorial com mais facilidade.
## Pacotes de importação
Para começar, precisaremos importar os pacotes Aspose.Cells necessários. Veja como você pode fazer isso:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Isso permite que você acesse todas as funcionalidades necessárias do Aspose.Cells para manipular seus dados.
Agora que temos tudo pronto, vamos começar dividindo a conversão de texto em colunas em várias etapas fáceis de seguir.
## Etapa 1: Configurar o diretório de documentos
Primeiro, você precisa configurar o diretório onde você salvará seu arquivo de saída. É sempre uma boa ideia estruturar seus arquivos de forma organizada; isso facilita o gerenciamento deles.
```csharp
// O caminho para o diretório de documentos.
string dataDir = "Your Document Directory";
```
-  Substituir`"Your Document Directory"`com o caminho real onde você deseja salvar seu arquivo. Por exemplo, você pode usar`C:\\Documents\\AsposeOutput\\`.
## Etapa 2: Criar uma instância de pasta de trabalho
Em seguida, vamos criar nossa pasta de trabalho. Esse é essencialmente o arquivo onde todos os seus dados serão processados.
```csharp
// Crie uma instância de pasta de trabalho.
Workbook wb = new Workbook();
```
- Pense na pasta de trabalho como uma tela em branco. Você pode pintar como quiser!
## Etapa 3: Acesse a primeira planilha
Agora que temos uma pasta de trabalho, precisamos acessar a primeira planilha para começar a adicionar nossos dados.
```csharp
// Acesse a primeira planilha.
Worksheet ws = wb.Worksheets[0];
```
- A planilha é como uma página na sua pasta de trabalho. Você pode ter várias páginas, mas vamos focar na primeira para simplificar.
## Etapa 4: Adicionar dados à planilha
Vamos preencher nossa planilha com alguns nomes. Vamos inserir uma lista de nomes onde o primeiro e o último nome são separados por um espaço.
```csharp
// Adicione nomes de pessoas na coluna A. Nome e sobrenome são separados por espaço.
ws.Cells["A1"].PutValue("John Teal");
ws.Cells["A2"].PutValue("Peter Graham");
ws.Cells["A3"].PutValue("Brady Cortez");
ws.Cells["A4"].PutValue("Mack Nick");
ws.Cells["A5"].PutValue("Hsu Lee");
```
- Você vai querer ajustar seus nomes conforme necessário; talvez você queira testar com sua própria lista de nomes ou criar um conjunto mais diversificado.
## Etapa 5: Criar opções de carregamento de texto
Antes de dividir os nomes, precisamos definir como queremos dividir o texto. Neste caso, usaremos um espaço como delimitador.
```csharp
// Crie opções de carregamento de texto com espaço como separador.
TxtLoadOptions opts = new TxtLoadOptions();
opts.Separator = ' ';
```
- Ao definir espaço como nosso separador, informamos ao Aspose que é aqui que ele deve dividir os nomes.
## Etapa 6: Divida a coluna em várias colunas
 Aí vem a mágica! Agora vamos dividir o conteúdo da coluna A em duas colunas separadas (primeiros nomes na coluna A e sobrenomes na coluna B) usando o`TextToColumns` método.
```csharp
// Divida a coluna A em duas colunas usando o método TextToColumns().
// Agora a coluna A terá o primeiro nome e a coluna B terá o sobrenome.
ws.Cells.TextToColumns(0, 0, 5, opts);
```
- Este passo tira todo o trabalho duro dos seus ombros. É como ter um pequeno ajudante diligente que sabe exatamente o que fazer!
## Etapa 7: Salve a pasta de trabalho
Por fim, vamos salvar nossa pasta de trabalho com as alterações que fizemos. É sempre gratificante ver seu trabalho salvo de forma limpa!
```csharp
// Salve a pasta de trabalho no formato xlsx.
wb.Save(dataDir + "outputTextToColumns.xlsx");
```
- Certifique-se de dar ao arquivo um nome significativo. Neste caso, estamos salvando-o como`outputTextToColumns.xlsx`, mas fique à vontade para renomeá-lo como achar melhor.
## Conclusão
 E aí está! Você acabou de aprender como converter texto em colunas usando o Aspose.Cells para .NET. É uma ferramenta poderosa que simplifica o manuseio de dados, permitindo que você execute operações que antes levavam horas em apenas algumas linhas simples de código. Agora, da próxima vez que precisar dividir nomes ou outro texto, você pode fazer isso com facilidade. Não se esqueça de explorar[Documentação do Aspose](https://reference.aspose.com/cells/net/) para recursos e personalizações mais avançados que podem elevar suas habilidades de processamento de dados!
## Perguntas frequentes
### O que é Aspose.Cells?
Aspose.Cells é uma biblioteca .NET robusta que permite aos desenvolvedores criar, manipular e converter planilhas do Excel de forma eficiente, sem precisar instalar o Microsoft Excel.
### Posso usar o Aspose.Cells gratuitamente?
 Sim! Você pode começar com um teste gratuito disponível em[Página de teste do Aspose](https://releases.aspose.com/).
### Onde posso encontrar suporte para o Aspose.Cells?
 Para quaisquer dúvidas ou problemas, você pode visitar o[Fórum de suporte Aspose](https://forum.aspose.com/c/cells/9).
### É fácil aprender Aspose.Cells?
Absolutamente! Com exemplos diretos e documentação extensa, até mesmo iniciantes podem aprender rapidamente.
### Quais outros recursos o Aspose.Cells oferece?
Além da manipulação de texto, o Aspose.Cells oferece suporte à criação de gráficos, validação de dados, cálculos de fórmulas e muito mais!

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
