---
title: Ajouter une signature numérique au fichier Excel signé
linktitle: Ajouter une signature numérique au fichier Excel signé
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment ajouter une signature numérique à un fichier Excel déjà signé à l'aide d'Aspose.Cells pour .NET dans ce guide étape par étape. Sécurisez vos documents.
weight: 12
url: /fr/net/workbook-operations/add-digital-signature-to-signed-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter une signature numérique au fichier Excel signé

## Introduction
Dans le monde numérique d'aujourd'hui, il est essentiel de garantir l'authenticité et l'intégrité des documents. Les signatures numériques constituent un moyen fiable de vérifier qu'un document n'a pas été modifié et qu'il provient d'une source légitime. Si vous travaillez avec des fichiers Excel dans .NET et que vous souhaitez ajouter une signature numérique à un fichier déjà signé, vous êtes au bon endroit ! Dans ce guide, nous vous expliquerons le processus d'ajout d'une nouvelle signature numérique à un fichier Excel signé existant à l'aide d'Aspose.Cells pour .NET. 
## Prérequis
Avant de plonger dans le vif du sujet, assurons-nous que vous disposez de tout ce dont vous avez besoin pour commencer :
1.  Aspose.Cells pour .NET : tout d'abord, vous devez avoir installé Aspose.Cells dans votre environnement .NET. Vous pouvez le télécharger à partir du[page de sortie](https://releases.aspose.com/cells/net/).
2. .NET Framework : assurez-vous que .NET Framework est installé sur votre ordinateur. Ce guide suppose que vous connaissez les concepts de base de la programmation .NET.
3. Certificat numérique : vous aurez besoin d'un certificat numérique valide (au format .pfx) pour créer une signature numérique. Si vous n'en avez pas, vous pouvez créer un certificat auto-signé à des fins de test.
4. Environnement de développement : un éditeur de code ou un IDE comme Visual Studio dans lequel vous pouvez écrire et exécuter votre code C#.
5. Exemple de fichier Excel : vous devez disposer d'un fichier Excel déjà signé numériquement. C'est à ce fichier que nous ajouterons une autre signature.
Ces prérequis étant posés, passons au code !
## Paquets d'importation
Avant de commencer à coder, assurez-vous d'importer les espaces de noms nécessaires. Voici ce que vous devez inclure en haut de votre fichier C# :
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Ces espaces de noms vous donneront accès aux classes et méthodes nécessaires pour manipuler les fichiers Excel et gérer les signatures numériques.
Décomposons maintenant le processus en étapes faciles à gérer. Nous allons parcourir chaque étape pour nous assurer que vous comprenez comment ajouter une signature numérique à un fichier Excel déjà signé.
## Étape 1 : Définissez vos répertoires
Tout d'abord, vous devez spécifier où se trouvent vos fichiers sources et où enregistrer le fichier de sortie. C'est simple mais crucial :
```csharp
// Répertoire des sources
string sourceDir = "Your Document Directory"; // Remplacez par votre répertoire actuel
// Répertoire de sortie
string outputDir = "Your Document Directory"; // Remplacez par votre répertoire actuel
```
 Remplacer`"Your Document Directory"` avec le chemin réel où vos fichiers sont stockés. Cela définit le contexte de vos opérations sur les fichiers.
## Étape 2 : charger le classeur signé existant
Ensuite, vous chargez le classeur Excel existant qui est déjà signé. C'est ici que la magie commence :
```csharp
// Chargez le classeur qui est déjà signé numériquement pour ajouter une nouvelle signature numérique
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(sourceDir + "sampleDigitallySignedByCells.xlsx");
```
 Cette ligne initialise une nouvelle`Workbook` objet avec le fichier spécifié. Assurez-vous que le nom du fichier correspond à votre fichier Excel signé existant.
## Étape 3 : Créer une collection de signatures numériques
Pour gérer vos signatures numériques, vous devez créer une collection. Cela vous permet de conserver plusieurs signatures si nécessaire :
```csharp
// Créer la collection de signatures numériques
Aspose.Cells.DigitalSignatures.DigitalSignatureCollection dsCollection = new Aspose.Cells.DigitalSignatures.DigitalSignatureCollection();
```
Cette collection sera l'endroit où vous ajouterez votre nouvelle signature numérique avant de l'appliquer au classeur.
## Étape 4 : chargez votre certificat
Il est maintenant temps de charger votre certificat numérique. Ce certificat sera utilisé pour créer la nouvelle signature :
```csharp
// Fichier de certificat et son mot de passe
string certFileName = sourceDir + "AsposeDemo.pfx"; // Votre fichier de certificat
string password = "aspose"; //Votre mot de passe de certificat
// Créer un nouveau certificat
System.Security.Cryptography.X509Certificates.X509Certificate2 certificate = new System.Security.Cryptography.X509Certificates.X509Certificate2(certFileName, password);
```
 Assurez-vous de remplacer`AsposeDemo.pfx` avec le nom de votre fichier de certificat et mettez à jour le mot de passe en conséquence. Cette étape est cruciale car sans le certificat correct, vous ne pourrez pas créer de signature valide.
## Étape 5 : Créer une nouvelle signature numérique
Une fois votre certificat chargé, vous pouvez maintenant créer une nouvelle signature numérique. Cette signature sera ajoutée à votre collection :
```csharp
// Créez une nouvelle signature numérique et ajoutez-la à la collection de signatures numériques
Aspose.Cells.DigitalSignatures.DigitalSignature signature = new Aspose.Cells.DigitalSignatures.DigitalSignature(certificate, "Aspose.Cells added new digital signature in existing digitally signed workbook.", DateTime.Now);
dsCollection.Add(signature);
```
Ici, vous fournissez un message qui décrit la signature, ce qui peut être utile pour la conservation des enregistrements. L'horodatage garantit que la signature est associée au bon moment dans le temps.
## Étape 6 : ajouter la collection Signature au classeur
Après avoir créé la signature, il est temps d'ajouter l'intégralité de la collection au classeur :
```csharp
// Ajouter une collection de signatures numériques à l'intérieur du classeur
workbook.AddDigitalSignature(dsCollection);
```
Cette étape applique efficacement votre nouvelle signature numérique au classeur, le marquant avec une authenticité supplémentaire.
## Étape 7 : Enregistrer le classeur
Enfin, enregistrez le classeur avec la nouvelle signature numérique incluse. C'est le moment où tous vos efforts portent leurs fruits :
```csharp
//Enregistrez le classeur et jetez-le.
workbook.Save(outputDir + "outputDigitallySignedByCells.xlsx");
workbook.Dispose();
```
Assurez-vous de spécifier un nom pour votre fichier de sortie. Il s'agira de la nouvelle version de votre fichier Excel, complétée par la signature numérique supplémentaire.
## Étape 8 : Confirmer le succès
Pour conclure, c'est une bonne idée de fournir un retour d'information une fois l'opération terminée avec succès :
```csharp
Console.WriteLine("AddDigitalSignatureToAnAlreadySignedExcelFile executed successfully.\r\n");
```
Cette ligne imprimera un message de confirmation sur la console, vous informant que tout s'est bien passé.
## Conclusion
Et voilà ! Vous avez ajouté avec succès une nouvelle signature numérique à un fichier Excel déjà signé à l'aide d'Aspose.Cells pour .NET. Ce processus améliore non seulement la sécurité de vos documents, mais garantit également qu'ils sont fiables et vérifiables. 
Les signatures numériques sont essentielles dans le paysage numérique actuel, en particulier pour les entreprises et les professionnels qui doivent préserver l'intégrité de leurs documents. En suivant ce guide, vous pouvez facilement gérer les signatures numériques dans vos fichiers Excel, garantissant ainsi la sécurité et l'authenticité de vos données.
## FAQ
### Qu'est-ce qu'une signature numérique ?
Une signature numérique est un système mathématique permettant de vérifier l'authenticité et l'intégrité de messages ou de documents numériques. Elle garantit que le document n'a pas été altéré et confirme l'identité du signataire.
### Ai-je besoin d’un certificat spécial pour créer une signature numérique ?
Oui, vous avez besoin d’un certificat numérique émis par une autorité de certification (CA) de confiance pour créer une signature numérique valide.
### Puis-je utiliser un certificat auto-signé pour les tests ?
Absolument ! Vous pouvez créer un certificat auto-signé à des fins de développement et de test, mais pour la production, il est préférable d'utiliser un certificat provenant d'une autorité de certification de confiance.
### Que se passe-t-il si j'essaie d'ajouter une signature à un document non signé ?
Si vous essayez d'ajouter une signature numérique à un document qui n'est pas déjà signé, cela fonctionnera sans problème, mais la signature d'origine ne sera pas présente.
### Où puis-je trouver plus d'informations sur Aspose.Cells ?
 Vous pouvez vérifier le[Documentation d'Aspose.Cells](https://reference.aspose.com/cells/net/) pour des guides détaillés et des références API.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
