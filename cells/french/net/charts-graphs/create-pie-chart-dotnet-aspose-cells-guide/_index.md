---
"date": "2025-04-05"
"description": "Un tutoriel de code pour Aspose.Cells Net"
"title": "Créer un graphique à secteurs dans .NET avec Aspose.Cells - Un guide complet"
"url": "/fr/net/charts-graphs/create-pie-chart-dotnet-aspose-cells-guide/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Comment créer un graphique à secteurs dans .NET avec Aspose.Cells : guide étape par étape

## Introduction

Créer des représentations visuelles de données est une compétence essentielle, notamment pour transmettre des informations complexes de manière simple et efficace. Que vous travailliez sur un rapport d'activité ou que vous analysiez des statistiques démographiques, les diagrammes à secteurs offrent un moyen simple d'illustrer les parties d'un ensemble. Ce guide vous guidera dans la création d'un diagramme à secteurs dans .NET à l'aide d'Aspose.Cells, une bibliothèque puissante qui simplifie la manipulation de documents Excel par programmation.

**Ce que vous apprendrez :**
- Comment initialiser et configurer un classeur Excel.
- Remplissage de données dans les cellules de la feuille de calcul pour la visualisation.
- Création et configuration d'un graphique à secteurs à l'aide d'Aspose.Cells pour .NET.
- Personnalisation des couleurs des tranches dans le graphique à secteurs pour un attrait visuel amélioré.
- Ajustement automatique des colonnes et enregistrement de votre classeur.

Découvrons comment utiliser Aspose.Cells pour créer facilement des diagrammes à secteurs percutants. Avant de commencer, assurez-vous de remplir les conditions préalables pour suivre la procédure sans difficulté.

## Prérequis

Pour commencer ce tutoriel, assurez-vous d'avoir :

- **Bibliothèques requises :** Vous aurez besoin de la bibliothèque Aspose.Cells pour .NET. Assurez-vous que votre projet est configuré pour l'utiliser.
- **Configuration requise pour l'environnement :** Un environnement de développement approprié tel que Visual Studio installé sur votre système.
- **Prérequis en matière de connaissances :** Compréhension de base de la programmation C# et familiarité avec les structures de documents Excel.

## Configuration d'Aspose.Cells pour .NET

Avant de vous lancer dans le code, vous devez installer la bibliothèque Aspose.Cells dans votre projet. Voici comment :

### Installation via CLI
Ouvrez votre terminal ou votre invite de commande et exécutez :
```bash
dotnet add package Aspose.Cells
```

### Installation via le gestionnaire de paquets
Si vous utilisez Visual Studio, ouvrez la console du gestionnaire de packages NuGet et exécutez :
```powershell
PM> Install-Package Aspose.Cells
```

#### Étapes d'acquisition de licence
Vous pouvez commencer par un essai gratuit pour évaluer Aspose.Cells. Pour une utilisation prolongée, envisagez d'obtenir une licence temporaire ou de l'acheter directement sur leur site web.

#### Initialisation et configuration de base

Pour initialiser la bibliothèque dans votre projet C# :
```csharp
using Aspose.Cells;

// Créer une instance de la classe Workbook
Workbook workbook = new Workbook();
```

Cette configuration de base vous permet de commencer à travailler avec des fichiers Excel par programmation.

## Guide de mise en œuvre

### Fonctionnalité 1 : Initialiser le classeur et la feuille de calcul

**Aperçu:** Cette fonctionnalité configure un nouveau classeur et accède à sa première feuille de calcul, préparant ainsi la scène pour la saisie des données et la création de graphiques.

#### Initialisation étape par étape
```csharp
using Aspose.Cells;

class InitializeWorkbook {
    public void Run() {
        // Créer un nouvel objet de classeur
        Workbook workbook = new Workbook();
        
        // Accéder à la première feuille de calcul du classeur
        Worksheet worksheet = workbook.Worksheets[0];
    }
}
```
Ici, `Workbook` représente un fichier Excel et accède `Worksheets[0]` vous donne la première feuille.

### Fonctionnalité 2 : Remplir les données du graphique à secteurs

**Aperçu:** Le remplissage des données est crucial, car il constitue la base de votre graphique. Cette étape consiste à saisir les noms des pays et leurs pourcentages de population mondiale correspondants dans des cellules spécifiques.

#### Population de données étape par étape
```csharp
using Aspose.Cells;

class PopulateData {
    public void Run() {
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
        
        // Saisissez les données du pays dans la colonne C
        worksheet.Cells["C3"].PutValue("India");
        worksheet.Cells["C4"].PutValue("China");
        worksheet.Cells["C5"].PutValue("United States");
        worksheet.Cells["C6"].PutValue("Russia");
        worksheet.Cells["C7"].PutValue("United Kingdom");
        worksheet.Cells["C8"].PutValue("Others");

        // Saisissez les données en pourcentage dans la colonne D
        worksheet.Cells["D2"].PutValue("% of world population");
        worksheet.Cells["D3"].PutValue(25);
        worksheet.Cells["D4"].PutValue(30);
        worksheet.Cells["D5"].PutValue(10);
        worksheet.Cells["D6"].PutValue(13);
        worksheet.Cells["D7"].PutValue(9);
        worksheet.Cells["D8"].PutValue(13);
    }
}
```
Cette étape garantit que vos données sont prêtes à être visualisées.

### Fonctionnalité 3 : Créer et configurer un graphique à secteurs

**Aperçu:** Cette fonctionnalité implique la création d'un graphique à secteurs, la définition de ses données de série et la configuration de diverses propriétés telles que le titre et la position de la légende.

#### Création d'un graphique à secteurs étape par étape
```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;

class CreatePieChart {
    public void Run() {
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
        
        // Ajouter un graphique à secteurs à la feuille de calcul
        int pieIdx = worksheet.Charts.Add(ChartType.Pie, 1, 6, 15, 14);
        Chart pie = worksheet.Charts[pieIdx];

        // Définir la série de données pour le graphique
        pie.NSeries.Add("D3:D8", true);

        // Définir les données de catégorie et configurer le titre
        pie.NSeries.CategoryData = "=Sheet1!$C$3:$C$8";
        pie.Title.LinkedSource = "D2";
        pie.Legend.Position = LegendPositionType.Bottom;
        pie.Title.Font.Name = "Calibri";
        pie.Title.Font.Size = 18;
    }
}
```
Ce code crée un graphique visuellement attrayant lié à vos données.

### Fonctionnalité 4 : Personnaliser les couleurs des tranches dans un graphique à secteurs

**Aperçu:** La personnalisation de l'apparence de chaque tranche améliore la lisibilité et l'esthétique. Cette étape consiste à attribuer des couleurs uniques à chaque tranche.

#### Personnalisation des couleurs étape par étape
```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;

class CustomizeSliceColors {
    public void Run() {
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        int pieIdx = worksheet.Charts.Add(ChartType.Pie, 1, 6, 15, 14);
        Chart pie = worksheet.Charts[pieIdx];
        
        Series srs = pie.NSeries[0];

        // Attribuer des couleurs personnalisées à chaque tranche
        srs.Points[0].Area.ForegroundColor = Color.FromArgb(0, 246, 22, 219);
        srs.Points[1].Area.ForegroundColor = Color.FromArgb(0, 51, 34, 84);
        srs.Points[2].Area.ForegroundColor = Color.FromArgb(0, 46, 74, 44);
        srs.Points[3].Area.ForegroundColor = Color.FromArgb(0, 19, 99, 44);
        srs.Points[4].Area.ForegroundColor = Color.FromArgb(0, 208, 223, 7);
        srs.Points[5].Area.ForegroundColor = Color.FromArgb(0, 222, 69, 8);
    }
}
```
Cette étape ajoute une touche dynamique à votre graphique.

### Fonctionnalité 5 : Ajuster automatiquement les colonnes et enregistrer le classeur

**Aperçu:** Les dernières étapes consistent à ajuster la largeur des colonnes pour une meilleure visibilité des données et à enregistrer le classeur au format Excel.

#### Ajustement et enregistrement des colonnes étape par étape
```csharp
using Aspose.Cells;

class SaveWorkbook {
    public void Run() {
        string outputDir = "YOUR_OUTPUT_DIRECTORY";
        
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
        
        // Ajuster automatiquement les colonnes pour s'adapter au contenu
        worksheet.AutoFitColumns();

        // Enregistrer le classeur sous forme de fichier Excel
        workbook.Save(outputDir + "outputCustomSliceSectorColorsPieChart.xlsx", SaveFormat.Xlsx);
    }
}
```
Cela garantit que votre document final est soigné et prêt à être présenté.

## Applications pratiques

- **Rapports d'activité :** Utilisez des graphiques à secteurs pour représenter la répartition des ventes par région.
- **Études démographiques :** Visualisez les données démographiques dans différents pays ou régions.
- **Outils pédagogiques :** Créez des aides visuelles attrayantes pour les étudiants des cours de statistiques.
- **Analyse des soins de santé :** Afficher la répartition des données des patients au sein des établissements de santé.

## Considérations relatives aux performances

Pour garantir des performances optimales lors de l'utilisation d'Aspose.Cells, tenez compte des éléments suivants :

- **Traitement efficace des données :** Gérez de grands ensembles de données en les traitant par morceaux si nécessaire.
- **Gestion de la mémoire :** Éliminez les objets correctement pour libérer des ressources et éviter les fuites de mémoire.
- **Configurations de graphiques optimisées :** Minimisez les calculs complexes ou le rendu lors de la création de graphiques pour des performances plus rapides.

## Conclusion

Vous savez maintenant comment créer un graphique à secteurs dans .NET avec Aspose.Cells. Cette puissante bibliothèque simplifie la manipulation des documents Excel et vous permet de vous concentrer sur l'analyse des données plutôt que sur les complexités de la gestion des fichiers. Testez différents types de graphiques et options de personnalisation disponibles dans Aspose.Cells pour optimiser vos applications.

**Prochaines étapes :**
- Explorez d’autres types de graphiques tels que les graphiques à barres ou à courbes.
- Intégrez les fonctionnalités d'Aspose.Cells dans des projets .NET plus vastes pour des rapports automatisés.

Prêt à améliorer vos compétences en visualisation de données ? Explorez les fonctionnalités d'Aspose.Cells et commencez à les implémenter dans vos projets dès aujourd'hui !

## Section FAQ

1. **À quoi sert Aspose.Cells ?**
   - Il s'agit d'une bibliothèque permettant de gérer des fichiers Excel par programmation, vous permettant de créer, modifier et analyser des feuilles de calcul.

2. **Puis-je utiliser Aspose.Cells sans licence ?**
   - Oui, mais avec certaines limitations. Un essai gratuit ou une licence temporaire permet d'accéder à toutes les fonctionnalités.

3. **Comment personnaliser davantage l’apparence de mon graphique à secteurs ?**
   - Utilisez des propriétés supplémentaires comme `pie.NSeries[0].Area.Formatting` pour plus de contrôle sur l'esthétique.

4. **Quels sont les problèmes courants lors de la création de graphiques dans Aspose.Cells ?**
   - Assurez-vous que les plages de données sont correctement spécifiées et que vous avez configuré toutes les propriétés de graphique nécessaires avant le rendu.

5. **Comment puis-je intégrer Aspose.Cells avec d’autres bibliothèques .NET ?**
   - Utilisez Aspose.Cells dans le cadre d’une solution .NET plus vaste, en exploitant ses capacités aux côtés d’autres bibliothèques pour des applications complètes.

## Ressources

- **Documentation:** [Documentation d'Aspose.Cells](https://reference.aspose.com/cells/net/)
- **Télécharger:** [Aspose.Cells publie](https://releases.aspose.com/cells/net/)
- **Achat:** [Acheter Aspose.Cells](https://purchase.aspose.com/buy)
- **Essai gratuit :** [Essai gratuit d'Aspose.Cells](https://releases.aspose.com/cells/net/)
- **Licence temporaire :** [Obtenir un permis temporaire](https://purchase.aspose.com/temporary-license/)
- **Soutien:** [Forum Aspose](https://forum.aspose.com/c/cells/9)

En suivant ce guide, vous serez désormais équipé pour créer des graphiques à secteurs attrayants dans vos applications .NET avec Aspose.Cells. Bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}