---
category: general
date: 2026-03-25
description: Comment rédiger un modèle en utilisant les Smart Markers et apprendre
  à répéter les lignes, lier les données, générer un rapport et créer un modèle sans
  effort.
draft: false
keywords:
- how to write template
- how to repeat rows
- how to bind data
- how to generate report
- how to create template
language: fr
og_description: Comment créer un modèle avec les Smart Markers. Découvrez comment
  répéter des lignes, lier des données, générer un rapport et créer un modèle en C#.
og_title: Comment rédiger un modèle avec des marqueurs intelligents – Guide complet
tags:
- Aspose.Cells
- C#
- SmartMarkers
title: Comment rédiger un modèle avec des marqueurs intelligents – Guide étape par
  étape
url: /fr/net/smart-markers-dynamic-data/how-to-write-template-with-smart-markers-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment rédiger un modèle avec les Smart Markers – Tutoriel complet  

Vous êtes-vous déjà demandé **comment rédiger un modèle** qui s’étend automatiquement en fonction de vos données ? Vous n’êtes pas seul — de nombreux développeurs se retrouvent bloqués lorsqu’ils ont besoin d’un rapport Excel dynamique mais ne savent pas quelle fonctionnalité de l’API exploiter. La bonne nouvelle ? Avec les Smart Markers d’Aspose.Cells, vous pouvez créer un modèle dans une seule cellule, lier des données hiérarchiques, et laisser la bibliothèque répéter les lignes pour vous. Dans ce guide, nous couvrirons également **comment répéter des lignes**, **comment lier des données**, et même **comment générer un rapport** sans boucler manuellement sur les feuilles de calcul.

À la fin de ce tutoriel, vous disposerez d’un exemple complet et exécutable montrant **comment créer un modèle** pour des scénarios maître‑détail, ainsi que des astuces pour les cas limites et des astuces de performance. Aucun document externe n’est requis — tout ce dont vous avez besoin se trouve ici.

---

## Ce que vous allez créer

Nous allons générer un classeur Excel qui liste les commandes (le maître) et leurs lignes de détail (le détail). Le modèle se trouve dans la cellule **A1**, et les Smart Markers l’étendront en un tableau correctement formaté. La feuille finale ressemblera à :

```
Order1
   A
   B
Order2
   C
```

C’est le scénario classique de « comment générer un rapport », et le code fonctionne avec .NET 6+ et Aspose.Cells 23.x (ou version ultérieure).

---

## Prérequis

- SDK .NET 6 (ou toute version .NET récente)  
- Visual Studio 2022 ou VS Code  
- Aspose.Cells pour .NET (installer via NuGet : `Install-Package Aspose.Cells`)  

Si vous avez tout cela, vous êtes prêt à démarrer.

---

## Étape 1 : Configurer le projet et ajouter Aspose.Cells  

```csharp
// Create a new console app (run this in a terminal)
// dotnet new console -n SmartMarkerDemo
// cd SmartMarkerDemo
// dotnet add package Aspose.Cells
```

```csharp
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new workbook with a single worksheet
            var workbook = new Workbook();
            var worksheet = workbook.Worksheets[0];
```

*Pourquoi c’est important* : Commencer avec un `Workbook` vierge garantit une toile propre. L’objet `Worksheet` est l’endroit où nous placerons notre modèle.

---

## Étape 2 : Écrire le modèle Smart Marker  

Le modèle utilise `${Master.Name}` pour le titre de la commande et `${Detail:Repeat}` pour itérer sur chaque ligne de détail.

```csharp
            // Step 2: Define a Smart Marker template that repeats detail rows for each master record
            string smartMarkerTemplate = @"${Master.Name}
${Detail:Repeat}
   ${Detail.Item}
${/Detail}";
            
            // Write the template into cell A1
            worksheet.Cells["A1"].PutValue(smartMarkerTemplate);
```

> **Astuce pro** : Conservez le modèle dans une seule cellule ; les Smart Markers l’étendront automatiquement sur plusieurs lignes.  

*Comment cela résout le problème* : En intégrant le bloc de répétition directement dans la cellule, vous évitez l’insertion manuelle de lignes — Aspose s’en charge pour vous.

---

## Étape 3 : Construire les données hiérarchiques qui correspondent au modèle  

Nos données doivent refléter la structure du modèle : une collection `Master`, chacune contenant un tableau `Detail`.

```csharp
            // Step 3: Create hierarchical data matching the template structure
            var orderData = new
            {
                Master = new[]
                {
                    new
                    {
                        Name = "Order1",
                        Detail = new[]
                        {
                            new { Item = "A" },
                            new { Item = "B" }
                        }
                    },
                    new
                    {
                        Name = "Order2",
                        Detail = new[]
                        {
                            new { Item = "C" }
                        }
                    }
                }
            };
```

*Pourquoi nous lient les données de cette façon* : Les Smart Markers utilisent une liaison de type réflexion, donc les noms de propriétés doivent correspondre exactement aux espaces réservés. C’est le cœur de **comment lier des données** pour des rapports dynamiques.

---

## Étape 4 : Traiter le modèle – Laisser les Smart Markers faire le gros du travail  

```csharp
            // Step 4: Process the Smart Markers – the template will be expanded using the data above
            worksheet.SmartMarkerProcessor.Process(orderData);
```

Après le traitement, la feuille de calcul contiendra les lignes étendues. Aucun boucle, aucune écriture manuelle de cellules.

---

## Étape 5 : Enregistrer le classeur  

```csharp
            // Save the result to an XLSX file
            workbook.Save("SmartMarkerReport.xlsx", SaveFormat.Xlsx);
            System.Console.WriteLine("Report generated: SmartMarkerReport.xlsx");
        }
    }
}
```

Ouvrez le fichier généré et vous verrez la mise en page maître‑détail exactement comme décrite précédemment. C’est **comment générer un rapport** avec une seule ligne de code de traitement.

---

## Vue d’ensemble visuelle  

![Excel report generated by Smart Markers – how to write template](/images/smart-marker-report.png "how to write template")

*Texte alternatif* : "how to write template" – capture d’écran du fichier Excel final montrant les lignes répétées pour chaque commande.

---

## Analyse approfondie : Pourquoi les Smart Markers sont une révolution  

### Comment répéter des lignes sans boucle  

L’automatisation Excel traditionnelle vous oblige à calculer la dernière ligne, insérer de nouvelles lignes et copier les styles — des tâches sujettes aux erreurs. Les Smart Markers remplacent cela par un bloc déclaratif `${Detail:Repeat}`. Le moteur analyse le bloc, clone la ligne pour chaque élément de la collection, et injecte les valeurs. Cette approche est **comment répéter des lignes** de manière efficace.

### Liaison d’objets complexes  

Vous pouvez lier des objets imbriqués, des collections, ou même des DataTables. Tant que les noms de propriétés correspondent, le processeur parcourra le graphe d’objets. C’est l’essence de **comment lier des données** : vous fournissez au processeur un simple objet CLR (ou un type anonyme, comme nous l’avons fait) et il le mappe automatiquement.

### Génération de différents formats  

Bien que notre exemple enregistre en XLSX, vous pouvez remplacer `SaveFormat.Pdf` ou `SaveFormat.Csv` par une simple modification de ligne. C’est un chemin rapide vers **comment générer un rapport** dans plusieurs formats sans toucher au modèle.

### Réutilisation du modèle  

Si vous avez besoin de **comment créer un modèle** pour d’autres feuilles, copiez simplement le contenu de la cellule dans une autre feuille ou stockez‑le dans une ressource chaîne. Le même appel de processeur fonctionne partout, rendant votre code DRY et maintenable.

---

## Questions fréquentes & cas limites  

| Question | Réponse |
|----------|--------|
| *Que se passe‑t‑il si un maître n’a aucune ligne de détail ?* | Le bloc `${Detail:Repeat}` sera ignoré, ne laissant que le nom du maître. Aucune ligne vide n’est créée. |
| *Puis‑je styliser les lignes répétées ?* | Oui—appliquez le formatage à la ligne modèle (police, bordures, etc.) avant le traitement. Le style est copié sur chaque ligne générée. |
| *Dois‑je disposer du classeur ?* | Le `Workbook` implémente `IDisposable`. Enveloppez‑le dans un bloc `using` pour le code de production, mais pour une petite démo console c’est optionnel. |
| *Quelle taille maximale pour les données ?* | Les Smart Markers sont économes en mémoire, mais des collections très volumineuses (des centaines de milliers) peuvent nécessiter du paging ou du streaming. |
| *Puis‑je utiliser un fichier JSON au lieu d’un objet ?* | Absolument—désérialisez le JSON en un POCO qui correspond au modèle, puis passez‑le à `Process`. |

---

## Exemple complet fonctionnel (prêt à copier‑coller)

```csharp
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize workbook
            var workbook = new Workbook();
            var worksheet = workbook.Worksheets[0];

            // Define template
            string smartMarkerTemplate = @"${Master.Name}
${Detail:Repeat}
   ${Detail.Item}
${/Detail}";

            worksheet.Cells["A1"].PutValue(smartMarkerTemplate);

            // Prepare data
            var orderData = new
            {
                Master = new[]
                {
                    new
                    {
                        Name = "Order1",
                        Detail = new[]
                        {
                            new { Item = "A" },
                            new { Item = "B" }
                        }
                    },
                    new
                    {
                        Name = "Order2",
                        Detail = new[]
                        {
                            new { Item = "C" }
                        }
                    }
                }
            };

            // Process template
            worksheet.SmartMarkerProcessor.Process(orderData);

            // Save file
            workbook.Save("SmartMarkerReport.xlsx", SaveFormat.Xlsx);
            System.Console.WriteLine("Report generated: SmartMarkerReport.xlsx");
        }
    }
}
```

Exécutez le programme (`dotnet run`) et ouvrez *SmartMarkerReport.xlsx* — vous verrez les lignes maître‑détail correctement disposées.

---

## Récapitulatif  

Nous avons répondu à **comment rédiger un modèle** en utilisant les Smart Markers d’Aspose.Cells, démontré **comment répéter des lignes**, montré **comment lier des données** avec des objets hiérarchiques, et illustré **comment générer un rapport** en XLSX (ou tout autre format supporté). Le même schéma vous permet de **comment créer un modèle** pour des factures, des inventaires, ou toute mise en page maître‑détail que vous pouvez imaginer.

---

## Et après ?  

- **Styliser la sortie** : appliquez des styles de cellule à la ligne modèle avant le traitement.  
- **Exporter en PDF** : changez `SaveFormat.Xlsx` en `SaveFormat.Pdf` pour un rapport imprimable.  
- **En‑têtes dynamiques** : ajoutez des espaces réservés `${Headers}` pour générer les titres de colonnes à la volée.  
- **Multiples feuilles** : répétez le processus sur d’autres feuilles de calcul pour des rapports à sections multiples.  

N’hésitez pas à expérimenter—remplacez la source de données, ajoutez d’autres niveaux imbriqués, ou combinez avec des formules. La flexibilité des Smart Markers vous fait passer moins de temps à coder des boucles et plus de temps à livrer de la valeur.

---

*Bon codage ! Si vous rencontrez des difficultés, laissez un commentaire ci‑dessous ou contactez‑moi sur Stack Overflow avec le tag `aspose-cells`. Continuons la conversation.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}