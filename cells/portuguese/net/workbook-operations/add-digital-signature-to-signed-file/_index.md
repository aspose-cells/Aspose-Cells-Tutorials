---
title: Adicionar assinatura digital ao arquivo Excel assinado
linktitle: Adicionar assinatura digital ao arquivo Excel assinado
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda como adicionar uma assinatura digital a um arquivo Excel já assinado usando Aspose.Cells for .NET neste guia passo a passo. Proteja seus documentos.
weight: 12
url: /pt/net/workbook-operations/add-digital-signature-to-signed-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar assinatura digital ao arquivo Excel assinado

## Introdução
No mundo digital de hoje, garantir a autenticidade e a integridade dos documentos é crucial. Assinaturas digitais servem como um meio robusto de verificar se um documento não foi alterado e se ele vem de uma fonte legítima. Se você estiver trabalhando com arquivos do Excel no .NET e quiser adicionar uma assinatura digital a um arquivo que já está assinado, você está no lugar certo! Neste guia, nós o guiaremos pelo processo de adicionar uma nova assinatura digital a um arquivo assinado existente do Excel usando o Aspose.Cells para .NET. 
## Pré-requisitos
Antes de nos aprofundarmos nos detalhes, vamos garantir que você tenha tudo o que precisa para começar:
1.  Aspose.Cells para .NET: Primeiro e mais importante, você precisará ter o Aspose.Cells instalado em seu ambiente .NET. Você pode baixá-lo do[página de lançamento](https://releases.aspose.com/cells/net/).
2. .NET Framework: Certifique-se de ter o .NET Framework configurado em sua máquina. Este guia pressupõe que você esteja familiarizado com conceitos básicos de programação .NET.
3. Certificado Digital: Você precisará de um certificado digital válido (em formato .pfx) para criar uma assinatura digital. Se não tiver um, você pode criar um certificado autoassinado para fins de teste.
4. Ambiente de desenvolvimento: um editor de código ou IDE como o Visual Studio, onde você pode escrever e executar seu código C#.
5. Arquivo Excel de Exemplo: Você deve ter um arquivo Excel existente que já esteja assinado digitalmente. Este será o arquivo ao qual adicionaremos outra assinatura.
Com esses pré-requisitos resolvidos, vamos ao código!
## Pacotes de importação
Antes de começar a codificar, certifique-se de importar os namespaces necessários. Aqui está o que você precisa incluir no topo do seu arquivo C#:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Esses namespaces darão acesso às classes e métodos necessários para manipular arquivos do Excel e lidar com assinaturas digitais.
Agora, vamos dividir o processo em etapas gerenciáveis. Passaremos por cada etapa para garantir que você entenda como adicionar uma assinatura digital a um arquivo Excel já assinado.
## Etapa 1: Defina seus diretórios
Primeiro, você precisa especificar onde seus arquivos de origem estão localizados e onde salvar o arquivo de saída. Isso é simples, mas crucial:
```csharp
// Diretório de origem
string sourceDir = "Your Document Directory"; // Substitua pelo seu diretório atual
// Diretório de saída
string outputDir = "Your Document Directory"; // Substitua pelo seu diretório atual
```
 Substituir`"Your Document Directory"` com o caminho real onde seus arquivos estão armazenados. Isso prepara o cenário para suas operações de arquivo.
## Etapa 2: Carregue a pasta de trabalho assinada existente
Em seguida, você carregará a pasta de trabalho existente do Excel que já está assinada. É aqui que a mágica começa:
```csharp
// Carregue a pasta de trabalho que já está assinada digitalmente para adicionar uma nova assinatura digital
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(sourceDir + "sampleDigitallySignedByCells.xlsx");
```
 Esta linha inicializa um novo`Workbook` objeto com o arquivo especificado. Certifique-se de que o nome do arquivo corresponde ao seu arquivo Excel assinado existente.
## Etapa 3: Crie uma coleção de assinaturas digitais
Para gerenciar suas assinaturas digitais, você precisa criar uma coleção. Isso permite que você mantenha várias assinaturas, se necessário:
```csharp
// Crie a coleção de assinaturas digitais
Aspose.Cells.DigitalSignatures.DigitalSignatureCollection dsCollection = new Aspose.Cells.DigitalSignatures.DigitalSignatureCollection();
```
Esta coleção será onde você adicionará sua nova assinatura digital antes de aplicá-la à pasta de trabalho.
## Etapa 4: Carregue seu certificado
Agora, é hora de carregar seu certificado digital. Este certificado será usado para criar a nova assinatura:
```csharp
// Arquivo de certificado e sua senha
string certFileName = sourceDir + "AsposeDemo.pfx"; // Seu arquivo de certificado
string password = "aspose"; //Sua senha de certificado
// Criar novo certificado
System.Security.Cryptography.X509Certificates.X509Certificate2 certificate = new System.Security.Cryptography.X509Certificates.X509Certificate2(certFileName, password);
```
 Certifique-se de substituir`AsposeDemo.pfx` com o nome do seu arquivo de certificado e atualize a senha de acordo. Este passo é crucial porque sem o certificado correto, você não conseguirá criar uma assinatura válida.
## Etapa 5: Crie uma nova assinatura digital
Com seu certificado carregado, você pode agora criar uma nova assinatura digital. Esta assinatura será adicionada à sua coleção:
```csharp
// Crie uma nova assinatura digital e adicione-a na coleção de assinaturas digitais
Aspose.Cells.DigitalSignatures.DigitalSignature signature = new Aspose.Cells.DigitalSignatures.DigitalSignature(certificate, "Aspose.Cells added new digital signature in existing digitally signed workbook.", DateTime.Now);
dsCollection.Add(signature);
```
Aqui, você fornece uma mensagem que descreve a assinatura, o que pode ser útil para manutenção de registros. O timestamp garante que a assinatura esteja associada ao momento correto no tempo.
## Etapa 6: Adicionar a coleção de assinaturas à pasta de trabalho
Depois de criar a assinatura, é hora de adicionar toda a coleção à pasta de trabalho:
```csharp
// Adicionar coleta de assinatura digital dentro da pasta de trabalho
workbook.AddDigitalSignature(dsCollection);
```
Esta etapa aplica efetivamente sua nova assinatura digital à pasta de trabalho, marcando-a com autenticidade adicional.
## Etapa 7: Salve a pasta de trabalho
Por fim, salve a pasta de trabalho com a nova assinatura digital incluída. Este é o momento em que todo o seu trabalho duro vale a pena:
```csharp
//Salve a pasta de trabalho e descarte-a.
workbook.Save(outputDir + "outputDigitallySignedByCells.xlsx");
workbook.Dispose();
```
Certifique-se de especificar um nome para seu arquivo de saída. Esta será a nova versão do seu arquivo Excel, completa com a assinatura digital adicional.
## Etapa 8: Confirme o sucesso
Para finalizar, é uma boa ideia fornecer feedback quando a operação for concluída com sucesso:
```csharp
Console.WriteLine("AddDigitalSignatureToAnAlreadySignedExcelFile executed successfully.\r\n");
```
Esta linha imprimirá uma mensagem de confirmação no console, informando que tudo ocorreu sem problemas.
## Conclusão
E aí está! Você adicionou com sucesso uma nova assinatura digital a um arquivo Excel já assinado usando o Aspose.Cells for .NET. Este processo não só aumenta a segurança dos seus documentos, mas também garante que eles sejam confiáveis e verificáveis. 
Assinaturas digitais são essenciais no cenário digital de hoje, especialmente para empresas e profissionais que precisam manter a integridade de seus documentos. Seguindo este guia, você pode gerenciar facilmente assinaturas digitais em seus arquivos Excel, garantindo que seus dados permaneçam seguros e autênticos.
## Perguntas frequentes
### O que é uma assinatura digital?
Uma assinatura digital é um esquema matemático para verificar a autenticidade e integridade de mensagens ou documentos digitais. Ela garante que o documento não foi alterado e confirma a identidade do signatário.
### Preciso de um certificado especial para criar uma assinatura digital?
Sim, você precisa de um certificado digital emitido por uma autoridade de certificação (CA) confiável para criar uma assinatura digital válida.
### Posso usar um certificado autoassinado para testes?
Claro! Você pode criar um certificado autoassinado para fins de desenvolvimento e teste, mas para produção, é melhor usar um certificado de uma CA confiável.
### O que acontece se eu tentar adicionar uma assinatura a um documento não assinado?
Se você tentar adicionar uma assinatura digital a um documento que ainda não esteja assinado, funcionará sem problemas, mas a assinatura original não estará presente.
### Onde posso encontrar mais informações sobre o Aspose.Cells?
 Você pode verificar o[Documentação do Aspose.Cells](https://reference.aspose.com/cells/net/) para guias detalhados e referências de API.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
