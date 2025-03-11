---
title: Adicionar assinatura digital a um arquivo Excel já assinado
linktitle: Adicionar assinatura digital a um arquivo Excel já assinado
second_title: Referência da API Aspose.Cells para .NET
description: Aprenda como adicionar uma assinatura digital a um arquivo Excel já assinado usando o Aspose.Cells para .NET com este guia passo a passo detalhado.
weight: 30
url: /pt/net/excel-workbook/add-digital-signature-to-an-already-signed-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar assinatura digital a um arquivo Excel já assinado

## Introdução

No mundo digital de hoje, proteger documentos é mais importante do que nunca. Assinaturas digitais fornecem uma maneira de garantir a autenticidade e integridade dos seus arquivos, especialmente ao lidar com informações confidenciais. Se você estiver trabalhando com arquivos do Excel e quiser adicionar uma nova assinatura digital a uma pasta de trabalho que já foi assinada, você está no lugar certo! Neste guia, nós o guiaremos pelo processo de adicionar uma assinatura digital a um arquivo do Excel já assinado usando o Aspose.Cells para .NET. Então, vamos mergulhar!

## Pré-requisitos

Antes de começarmos a trabalhar nos detalhes da codificação, há algumas coisas que você precisa ter em mente:

1.  Aspose.Cells para .NET: Certifique-se de ter a biblioteca Aspose.Cells instalada em seu projeto .NET. Você pode baixá-la do[site](https://releases.aspose.com/cells/net/).
2.  Arquivo de certificado: você precisará de um arquivo de certificado válido (geralmente um`.pfx`arquivo) que contém seu certificado digital. Certifique-se de saber a senha para este arquivo.
3. Ambiente de desenvolvimento: configure seu ambiente de desenvolvimento com o Visual Studio ou qualquer outro IDE que suporte .NET.
4. Conhecimento básico de C#: A familiaridade com a programação em C# ajudará você a acompanhar sem problemas.
5. Arquivos de amostra: Tenha um arquivo Excel de amostra que já esteja assinado digitalmente. Este será o arquivo ao qual você adicionará uma nova assinatura.

Agora que temos tudo pronto, vamos começar a codificar!

## Pacotes de importação

Para começar, você precisará importar os pacotes necessários no seu arquivo C#. Veja como fazer isso:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Esses namespaces permitirão que você trabalhe com arquivos do Excel e lide com assinaturas digitais sem problemas.

## Etapa 1: configure seus diretórios de origem e saída

Antes de poder manipular seus arquivos do Excel, você precisa definir onde seus arquivos de origem estão localizados e onde você quer salvar o arquivo de saída. Veja como fazer isso:

```csharp
// Diretório de origem
string sourceDir = "Your Document Directory";
// Diretório de saída
string outputDir = "Your Document Directory";
```

Nesta etapa, estamos usando um método para obter os caminhos para os diretórios de origem e saída. Certifique-se de que esses diretórios existam e contenham os arquivos necessários.

## Etapa 2: Carregue a pasta de trabalho já assinada

 Em seguida, você precisará carregar a pasta de trabalho do Excel que deseja modificar. Isso é feito criando uma instância do`Workbook` classe e passando o caminho do arquivo assinado.

```csharp
// Carregue a pasta de trabalho que já está assinada digitalmente
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(sourceDir + "sampleDigitallySignedByCells.xlsx");
```

 Aqui, estamos carregando a pasta de trabalho chamada`sampleDigitallySignedByCells.xlsx`. Certifique-se de que este arquivo já esteja assinado.

## Etapa 3: Crie uma coleção de assinaturas digitais

Agora, vamos criar uma coleção de assinaturas digitais. Essa coleção conterá todas as assinaturas digitais que você deseja adicionar à pasta de trabalho.

```csharp
// Crie a coleção de assinaturas digitais
Aspose.Cells.DigitalSignatures.DigitalSignatureCollection dsCollection = new Aspose.Cells.DigitalSignatures.DigitalSignatureCollection();
```

Esta etapa é crucial porque permite que você gerencie diversas assinaturas, se necessário.

## Etapa 4: Crie um novo certificado

 Você precisa carregar seu arquivo de certificado para criar uma nova assinatura digital. É aqui que você especifica o caminho para seu`.pfx` arquivo e sua senha.

```csharp
// Arquivo de certificado e sua senha
string certFileName = sourceDir + "AsposeDemo.pfx";
string password = "aspose";

// Criar novo certificado
System.Security.Cryptography.X509Certificates.X509Certificate2 certificate = new System.Security.Cryptography.X509Certificates.X509Certificate2(certFileName, password);
```

 Certifique-se de substituir`AsposeDemo.pfx` a senha com o nome real do arquivo do certificado e a senha.

## Etapa 5: Crie a assinatura digital

Com o certificado em mãos, você pode criar uma assinatura digital. Você também vai querer fornecer um motivo para a assinatura e a data e hora atuais.

```csharp
// Crie uma nova assinatura digital e adicione-a na coleção de assinaturas digitais
Aspose.Cells.DigitalSignatures.DigitalSignature signature = new Aspose.Cells.DigitalSignatures.DigitalSignature(certificate, "Aspose.Cells added new digital signature in existing digitally signed workbook.", DateTime.Now);
```

Esta etapa adiciona a nova assinatura à sua coleção, que você aplicará posteriormente à pasta de trabalho.

## Etapa 6: Adicionar a coleção de assinaturas digitais à pasta de trabalho

Agora é hora de adicionar a coleção de assinaturas digitais à pasta de trabalho. É aqui que a mágica acontece!

```csharp
// Adicionar coleta de assinatura digital dentro da pasta de trabalho
workbook.AddDigitalSignature(dsCollection);
```

Ao executar esta linha, você estará efetivamente anexando a nova assinatura digital à pasta de trabalho já assinada.

## Etapa 7: Salvar e descartar a pasta de trabalho

Por fim, você deve salvar a pasta de trabalho modificada no diretório de saída e liberar todos os recursos que estão sendo usados.

```csharp
//Salve a pasta de trabalho e descarte-a.
workbook.Save(outputDir + "outputDigitallySignedByCells.xlsx");
workbook.Dispose();
```

Esta etapa garante que suas alterações sejam salvas e que a pasta de trabalho seja descartada corretamente para liberar recursos.

## Etapa 8: Confirmar execução

Para finalizar, é uma boa ideia confirmar que seu código foi executado com sucesso. Você pode fazer isso com uma simples mensagem de console.

```csharp
Console.WriteLine("AddDigitalSignatureToAnAlreadySignedExcelFile executed successfully.\r\n");
```

Isso fornece um feedback de que sua operação foi bem-sucedida, o que é sempre bom ver!

## Conclusão

E aí está! Você adicionou com sucesso uma nova assinatura digital a um arquivo Excel já assinado usando o Aspose.Cells para .NET. Assinaturas digitais são uma maneira poderosa de garantir a autenticidade dos seus documentos, e agora você sabe como gerenciá-los programaticamente. Não importa se você está trabalhando em documentos financeiros, contratos ou qualquer informação sensível, implementar assinaturas digitais pode aumentar a segurança e a confiança.

## Perguntas frequentes

### O que é uma assinatura digital?
Uma assinatura digital é um método criptográfico usado para validar a autenticidade e a integridade de uma mensagem ou documento.

### Posso adicionar várias assinaturas digitais ao mesmo arquivo do Excel?
Sim, você pode criar uma coleção de assinaturas digitais e adicionar várias assinaturas à mesma pasta de trabalho.

### Quais formatos o Aspose.Cells suporta para assinaturas digitais?
 Aspose.Cells suporta vários formatos, incluindo`.pfx` para certificados.

### Preciso de uma versão específica do .NET para usar o Aspose.Cells?
 Verifique o[Documentação do Aspose.Cells](https://reference.aspose.com/cells/net/) para compatibilidade com sua versão do .NET.

### Como posso obter uma licença temporária para o Aspose.Cells?
 Você pode solicitar uma licença temporária em[Página de compras da Aspose](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
