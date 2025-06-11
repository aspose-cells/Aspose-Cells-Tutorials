---
"date": "2025-04-05"
"description": "Apprenez à convertir des fichiers Excel aux formats PNG, TIFF et PDF en utilisant des polices personnalisées avec Aspose.Cells pour .NET. Assurez une typographie cohérente pour toutes les conversions de documents."
"title": "Convertir Excel en PNG, TIFF et PDF avec des polices personnalisées dans .NET à l'aide d'Aspose.Cells"
"url": "/fr/net/workbook-operations/render-excel-custom-fonts-aspose-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Convertir des fichiers Excel en PNG, TIFF et PDF avec des polices personnalisées à l'aide d'Aspose.Cells pour .NET

## Introduction

Préserver l'intégrité des polices lors de la conversion de fichiers Excel en images ou PDF est essentiel à la cohérence de votre marque. Aspose.Cells pour .NET offre une solution robuste en vous permettant de spécifier des polices par défaut personnalisées lors de la conversion de vos documents.

Dans ce tutoriel, nous vous guiderons dans le rendu de fichiers Excel aux formats PNG, TIFF et PDF avec Aspose.Cells pour .NET et des polices par défaut personnalisées. Idéal si :
- Visez une typographie cohérente dans les documents rendus.
- Besoin de personnaliser les paramètres de police lors des conversions.
- Vous souhaitez explorer les options de configuration dans Aspose.Cells pour .NET.

Configurons votre environnement et mettons en œuvre ces fonctionnalités de manière transparente.

### Prérequis

Avant de commencer, assurez-vous d'avoir les éléments suivants :
- **Environnement .NET**:Installez sur votre machine (de préférence .NET Core ou .NET Framework).
- **Bibliothèque Aspose.Cells pour .NET**:Installé dans votre projet.
- **Fichier Excel**:Un classeur Excel avec des données à convertir.

### Configuration d'Aspose.Cells pour .NET

Pour commencer, ajoutez la bibliothèque Aspose.Cells à votre projet :

**Utilisation de .NET CLI :**
```bash
dotnet add package Aspose.Cells
```

**Utilisation du gestionnaire de paquets :**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

Acquérir une licence pour accéder à toutes les fonctionnalités :
- **Essai gratuit**: Visite [Essai gratuit d'Aspose](https://releases.aspose.com/cells/net/) pour l'accès initial.
- **Permis temporaire**:Obtenez-le auprès de [Licence temporaire Aspose](https://purchase.aspose.com/temporary-license/).
- **Achat**:Pour une licence permanente, rendez-vous sur [Achat Aspose](https://purchase.aspose.com/buy).

Après avoir acquis votre licence, initialisez Aspose.Cells dans votre application :
```csharp
// Définissez la licence pour Aspose.Cells.
License license = new License();
license.SetLicense("path_to_your_license_file");
```

## Guide de mise en œuvre

### Rendu au format PNG avec une police par défaut personnalisée

Convertir une feuille de calcul Excel en PNG avec une police par défaut personnalisée garantit une cohérence visuelle. Voici comment :

#### Étape 1 : Configurer les options d’image

Configurez les options de rendu pour votre sortie d’image.
```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Spécifier les répertoires.
string SourceDir = @"YOUR_SOURCE_DIRECTORY";
string outputDir = @"YOUR_OUTPUT_DIRECTORY";

// Ouvrir un fichier Excel.
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// Configurer les options de rendu d'image.
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false; // Utilisez une police personnalisée pour les polices manquantes dans le classeur.
imgOpt.DefaultFont = "Times New Roman";
```

#### Étape 2 : Rendu et enregistrement

Affichez votre feuille de calcul dans un fichier image à l’aide de ces paramètres.
```csharp
// Rendre la première feuille de calcul dans une image PNG.
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```

### Rendu au format TIFF avec une police par défaut personnalisée

Le format TIFF est idéal pour les images de haute qualité. Voici comment convertir un classeur entier en fichier TIFF :

#### Étape 3 : Configurer les options d’image pour TIFF

Configurez les options de rendu spécifiquement pour la sortie TIFF.
```csharp
// Réutilisez les répertoires précédemment définis et ouvrez le fichier Excel.
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// Configurer les options de rendu d’image pour TIFF.
imgOpt.ImageType = Drawing.ImageType.Tiff;
```

#### Étape 4 : Rendre l'intégralité du classeur au format TIFF

Convertissez l’intégralité du classeur en un seul fichier TIFF.
```csharp
// Rendre le classeur sous forme d’image TIFF.
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```

### Rendu au format PDF avec une police par défaut personnalisée

Enregistrer un classeur Excel au format PDF tout en garantissant la cohérence des polices est essentiel pour la documentation professionnelle.

#### Étape 5 : Configurer les options d’enregistrement PDF

Configurez les options nécessaires pour enregistrer votre fichier au format PDF.
```csharp
using Aspose.Cells;

// Rouvrir le classeur.
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// Configurer les options d’enregistrement PDF.
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false; // Utilisez une police personnalisée pour les polices manquantes dans le classeur.
```

#### Étape 6 : Enregistrer au format PDF

Exportez votre classeur dans un document PDF.
```csharp
// Enregistrez le classeur sous forme de fichier PDF.
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```

## Applications pratiques

- **Rapports d'activité**: Assurez une image de marque cohérente dans tous les rapports exportés en utilisant des polices personnalisées.
- **Archivage de documents**:Convertissez les fichiers Excel hérités en PDF pour un partage et un archivage faciles avec une typographie uniforme.
- **Conception graphique**: Créez des images TIFF haute résolution de données Excel pour des présentations ou des projets de conception.

L'intégration avec d'autres systèmes, tels que les plateformes CRM ou les solutions de gestion de documents, peut encore améliorer ces cas d'utilisation en automatisant les exportations en fonction de déclencheurs ou d'événements spécifiques.

## Considérations relatives aux performances

L’optimisation de votre processus de rendu est cruciale :
- **Gestion de la mémoire**: Jeter `Workbook`, `SheetRender`, et `WorkbookRender` objets rapidement pour libérer des ressources.
- **Traitement par lots**:Si vous traitez plusieurs fichiers, implémentez le traitement par lots pour une gestion efficace.
- **Opérations asynchrones**:Utilisez des méthodes asynchrones lorsque cela est possible pour améliorer la réactivité des applications.

## Conclusion

Vous maîtrisez désormais le rendu de classeurs Excel aux formats PNG, TIFF et PDF, tout en définissant des polices par défaut personnalisées grâce à Aspose.Cells pour .NET. Cette fonctionnalité garantit l'intégrité visuelle de vos documents sur différentes plateformes et utilisations.

Découvrez les fonctionnalités supplémentaires offertes par Aspose.Cells pour améliorer encore la gestion des documents. Pour plus d'informations ou d'assistance, consultez le [Forum Aspose](https://forum.aspose.com/c/cells/9).

## Section FAQ

**1. Qu'est-ce qu'Aspose.Cells pour .NET ?**
   — Aspose.Cells pour .NET est une bibliothèque qui fournit des fonctionnalités robustes pour gérer et convertir des fichiers Excel par programmation.

**2. Puis-je utiliser Aspose.Cells dans des applications Web ?**
   — Oui, Aspose.Cells peut être intégré à ASP.NET ou à toute autre application Web basée sur .NET.

**3. Comment gérer les polices manquantes lors du rendu ?**
   — En définissant le `CheckWorkbookDefaultFont` à faux et en spécifiant un `DefaultFont`, vous vous assurez que tout le texte utilise la police que vous avez choisie, même si l'original n'est pas disponible.

**4. Existe-t-il un support pour d’autres formats que PNG, TIFF et PDF ?**
   — Oui, Aspose.Cells prend en charge divers formats d’image tels que JPEG, BMP, etc., et offre des capacités étendues de conversion de documents.

**5. Quelles sont les meilleures pratiques pour utiliser Aspose.Cells dans des applications à grande échelle ?**
   — Utilisez des techniques efficaces de gestion de la mémoire, un traitement par lots pour gérer plusieurs fichiers et envisagez des opérations asynchrones pour améliorer les performances des applications.

## Ressources
- **Documentation**: [Documentation d'Aspose.Cells](https://reference.aspose.com/cells/net/)
- **Télécharger**: [Aspose.Cells publie](https://releases.aspose.com/cells/net/)
- **Achat**: [Acheter Aspose.Cells](https://purchase.aspose.com/buy)
- **Essai gratuit**: [Essayez Aspose.Cells gratuitement](https://releases.aspose.com/cells/net/)
- **Permis temporaire**: [Obtenir un permis temporaire](https://purchase.aspose.com/temporary-license/) 


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}