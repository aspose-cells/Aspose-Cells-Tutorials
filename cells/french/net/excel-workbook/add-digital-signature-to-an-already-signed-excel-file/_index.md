---
"description": "Découvrez comment ajouter une signature numérique à un fichier Excel déjà signé à l’aide d’Aspose.Cells pour .NET avec ce guide détaillé étape par étape."
"linktitle": "Ajouter une signature numérique à un fichier Excel déjà signé"
"second_title": "Référence de l'API Aspose.Cells pour .NET"
"title": "Ajouter une signature numérique à un fichier Excel déjà signé"
"url": "/fr/net/excel-workbook/add-digital-signature-to-an-already-signed-excel-file/"
"weight": 30
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter une signature numérique à un fichier Excel déjà signé

## Introduction

À l'ère du numérique, sécuriser les documents est plus important que jamais. Les signatures numériques permettent de garantir l'authenticité et l'intégrité de vos fichiers, notamment lorsqu'il s'agit d'informations sensibles. Si vous travaillez avec des fichiers Excel et souhaitez ajouter une nouvelle signature numérique à un classeur déjà signé, vous êtes au bon endroit ! Dans ce guide, nous vous expliquerons comment ajouter une signature numérique à un fichier Excel déjà signé avec Aspose.Cells pour .NET. Alors, c'est parti !

## Prérequis

Avant de passer aux choses sérieuses du codage, il y a quelques éléments que vous devez mettre en place :

1. Aspose.Cells pour .NET : Assurez-vous que la bibliothèque Aspose.Cells est installée dans votre projet .NET. Vous pouvez la télécharger depuis le [site](https://releases.aspose.com/cells/net/).
2. Fichier de certificat : vous aurez besoin d’un fichier de certificat valide (généralement un `.pfx` (fichier) contenant votre certificat numérique. Assurez-vous de connaître le mot de passe de ce fichier.
3. Environnement de développement : configurez votre environnement de développement avec Visual Studio ou tout autre IDE prenant en charge .NET.
4. Connaissances de base de C# : la familiarité avec la programmation C# vous aidera à suivre en douceur.
5. Exemples de fichiers : Utilisez un exemple de fichier Excel déjà signé numériquement. C'est sur ce fichier que vous ajouterez une nouvelle signature.

Maintenant que tout est en place, commençons à coder !

## Importer des packages

Pour commencer, vous devez importer les packages nécessaires dans votre fichier C#. Voici comment procéder :

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Ces espaces de noms vous permettront de travailler avec des fichiers Excel et de gérer les signatures numériques de manière transparente.

## Étape 1 : Configurez vos répertoires source et de sortie

Avant de pouvoir manipuler vos fichiers Excel, vous devez définir l'emplacement de vos fichiers sources et celui où vous souhaitez enregistrer le fichier de sortie. Voici comment procéder :

```csharp
// Répertoire source
string sourceDir = "Your Document Directory";
// Répertoire de sortie
string outputDir = "Your Document Directory";
```

Dans cette étape, nous utilisons une méthode pour obtenir les chemins d'accès aux répertoires source et de sortie. Assurez-vous que ces répertoires existent et contiennent les fichiers requis.

## Étape 2 : Charger le classeur déjà signé

Ensuite, vous devrez charger le classeur Excel à modifier. Pour ce faire, créez une instance de `Workbook` classe et en passant le chemin du fichier signé.

```csharp
// Charger le classeur qui est déjà signé numériquement
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(sourceDir + "sampleDigitallySignedByCells.xlsx");
```

Ici, nous chargeons le classeur nommé `sampleDigitallySignedByCells.xlsx`Assurez-vous que ce fichier est déjà signé.

## Étape 3 : Créer une collection de signatures numériques

Créons maintenant une collection de signatures numériques. Cette collection contiendra toutes les signatures numériques que vous souhaitez ajouter au classeur.

```csharp
// Créer la collection de signatures numériques
Aspose.Cells.DigitalSignatures.DigitalSignatureCollection dsCollection = new Aspose.Cells.DigitalSignatures.DigitalSignatureCollection();
```

Cette étape est cruciale car elle permet de gérer plusieurs signatures si besoin.

## Étape 4 : Créer un nouveau certificat

Vous devez charger votre fichier de certificat pour créer une nouvelle signature numérique. C'est ici que vous spécifiez le chemin d'accès à votre `.pfx` fichier et son mot de passe.

```csharp
// Fichier de certificat et son mot de passe
string certFileName = sourceDir + "AsposeDemo.pfx";
string password = "aspose";

// Créer un nouveau certificat
System.Security.Cryptography.X509Certificates.X509Certificate2 certificate = new System.Security.Cryptography.X509Certificates.X509Certificate2(certFileName, password);
```

Assurez-vous de remplacer `AsposeDemo.pfx` et le mot de passe avec votre nom de fichier de certificat et votre mot de passe réels.

## Étape 5 : Créer la signature numérique

Une fois le certificat en main, vous pouvez créer une signature numérique. Vous devrez également indiquer le motif de la signature, ainsi que la date et l'heure du jour.

```csharp
// Créez une nouvelle signature numérique et ajoutez-la à la collection de signatures numériques
Aspose.Cells.DigitalSignatures.DigitalSignature signature = new Aspose.Cells.DigitalSignatures.DigitalSignature(certificate, "Aspose.Cells added new digital signature in existing digitally signed workbook.", DateTime.Now);
```

Cette étape ajoute la nouvelle signature à votre collection, que vous appliquerez ensuite au classeur.

## Étape 6 : Ajouter la collection de signatures numériques au classeur

Il est maintenant temps d'ajouter la collection de signatures numériques au classeur. C'est là que la magie opère !

```csharp
// Ajouter une collection de signatures numériques à l'intérieur du classeur
workbook.AddDigitalSignature(dsCollection);
```

En exécutant cette ligne, vous attachez effectivement la nouvelle signature numérique au classeur déjà signé.

## Étape 7 : Enregistrer et supprimer le classeur

Enfin, vous souhaiterez enregistrer le classeur modifié dans votre répertoire de sortie et libérer toutes les ressources utilisées.

```csharp
// Enregistrez le classeur et jetez-le.
workbook.Save(outputDir + "outputDigitallySignedByCells.xlsx");
workbook.Dispose();
```

Cette étape garantit que vos modifications sont enregistrées et que le classeur est correctement supprimé pour libérer des ressources.

## Étape 8 : Confirmer l’exécution

Pour conclure, il est judicieux de confirmer que votre code s'est exécuté correctement. Vous pouvez le faire avec un simple message de console.

```csharp
Console.WriteLine("AddDigitalSignatureToAnAlreadySignedExcelFile executed successfully.\r\n");
```

Cela permet de savoir si votre opération a réussi, ce qui est toujours agréable à voir !

## Conclusion

Et voilà ! Vous avez ajouté une nouvelle signature numérique à un fichier Excel déjà signé avec Aspose.Cells pour .NET. Les signatures numériques sont un moyen puissant de garantir l'authenticité de vos documents, et vous savez désormais les gérer par programmation. Que vous travailliez sur des documents financiers, des contrats ou toute autre information sensible, l'utilisation de signatures numériques peut renforcer la sécurité et la confiance.

## FAQ

### Qu'est-ce qu'une signature numérique ?
Une signature numérique est une méthode cryptographique utilisée pour valider l’authenticité et l’intégrité d’un message ou d’un document.

### Puis-je ajouter plusieurs signatures numériques au même fichier Excel ?
Oui, vous pouvez créer une collection de signatures numériques et ajouter plusieurs signatures au même classeur.

### Quels formats Aspose.Cells prend-il en charge pour les signatures numériques ?
Aspose.Cells prend en charge divers formats, notamment `.pfx` pour les certificats.

### Ai-je besoin d’une version spécifique de .NET pour utiliser Aspose.Cells ?
Vérifiez le [Documentation d'Aspose.Cells](https://reference.aspose.com/cells/net/) pour la compatibilité avec votre version .NET.

### Comment puis-je obtenir une licence temporaire pour Aspose.Cells ?
Vous pouvez demander une licence temporaire auprès de [Page d'achat d'Aspose](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}