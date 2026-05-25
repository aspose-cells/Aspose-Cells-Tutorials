---
category: general
date: 2026-02-15
description: Tutoriel C# pour créer un classeur Excel montrant comment ajouter une
  propriété personnalisée, enregistrer le classeur au format XLSB et récupérer la
  valeur de la propriété — le tout en quelques lignes de code.
draft: false
keywords:
- create excel workbook c#
- save workbook as xlsb
- retrieve custom property value
- add custom property excel
language: fr
og_description: Créez un classeur Excel en C# étape par étape. Apprenez à ajouter
  une propriété personnalisée, à enregistrer le classeur au format XLSB et à récupérer
  la valeur de la propriété avec des exemples de code clairs.
og_title: Créer un classeur Excel en C# – Ajouter une propriété personnalisée et enregistrer
  au format XLSB
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Créer un classeur Excel en C# – Ajouter une propriété personnalisée et enregistrer
  au format XLSB
url: /fr/net/document-properties/create-excel-workbook-c-add-custom-property-save-xlsb/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un classeur Excel C# – Ajouter une propriété personnalisée et enregistrer en XLSB

Besoin de **créer un classeur Excel C#** et d’y intégrer des métadonnées personnalisées ? Dans ce guide, nous verrons comment ajouter une propriété personnalisée, **enregistrer le classeur au format XLSB**, puis **récupérer la valeur de la propriété personnalisée**—le tout avec du code concis, prêt à être exécuté.  

Si vous vous êtes déjà demandé pourquoi une feuille de calcul aurait besoin de données supplémentaires qui ne sont pas visibles dans les cellules, vous êtes au bon endroit. Pensez aux propriétés personnalisées comme des notes cachées qui voyagent avec le fichier, idéales pour lier un classeur à un ID de projet, un tag de version ou toute clé métier.

## Ce que vous allez apprendre

- Comment instancier un nouveau classeur avec Aspose.Cells pour .NET.  
- Les étapes exactes pour **ajouter une propriété personnalisée** à la manière d’Excel, en utilisant la collection `CustomProperties`.  
- Enregistrer le classeur au format binaire compact XLSB.  
- Charger à nouveau le fichier et extraire la propriété stockée.  

Pas de fichiers de configuration externes, pas de astuces obscures—juste du C# pur que vous pouvez coller dans une application console et voir fonctionner. La seule condition préalable est une référence à la bibliothèque Aspose.Cells (version d’essai gratuite ou version sous licence).  

Pourquoi s’en soucier ? Parce qu’intégrer des ID directement dans le fichier élimine le besoin d’une recherche dans une base de données séparée lorsque vous ouvrez le classeur plus tard. C’est une petite habitude qui peut faire gagner des heures de débogage dans des solutions de reporting à grande échelle.

---

![exemple de création de classeur Excel C#](https://example.com/images/create-excel-workbook-csharp.png "exemple de création de classeur Excel C#")

*L’image montre un projet console C# minimal qui crée un classeur Excel, ajoute une propriété personnalisée et l’enregistre au format XLSB.*

## Étape 1 : Initialiser le classeur et ajouter une propriété personnalisée

La toute première chose dont vous avez besoin est un objet `Workbook` frais. Une fois que vous l’avez, la collection `Worksheets[0].CustomProperties` vous offre un endroit propre pour stocker des paires clé/valeur.

```csharp
using Aspose.Cells;

namespace ExcelCustomPropDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Create a new workbook instance
            Workbook workbook = new Workbook();

            // Step 2 – Add a custom property named "ProjectId" with a numeric value
            // This is the "add custom property excel" part of the tutorial.
            workbook.Worksheets[0].CustomProperties.Add("ProjectId", 12345);
```

**Pourquoi c’est important :**  
- `Workbook()` crée une représentation en mémoire d’un fichier Excel, sans I/O disque pour l’instant.  
- Ajouter la propriété à la *première* feuille (indice 0) garantit qu’elle est stockée au niveau du classeur, ce qui la rend accessible quel que soit l’onglet affiché par l’utilisateur.  

> **Astuce :** Les propriétés personnalisées peuvent contenir des chaînes, des nombres, des dates ou même des valeurs booléennes. Choisissez le type qui correspond le mieux aux données que vous souhaitez stocker.

## Étape 2 : Enregistrer le classeur au format XLSB

XLSB (Excel Binary Workbook) est un format compact et rapide à charger—idéal pour les gros jeux de données. La méthode `Save` prend un chemin de fichier et une énumération `SaveFormat`.

```csharp
            // Step 3 – Save the workbook to disk in XLSB format
            string outputPath = @"C:\Temp\CustomProp.xlsb";
            workbook.Save(outputPath, SaveFormat.Xlsb);

            // At this point the file on disk already contains the custom property.
```

**Pourquoi utiliser le XLSB ?**  
- Il réduit la taille du fichier jusqu’à 70 % par rapport au XLSX classique.  
- Le stockage binaire accélère les opérations d’écriture et de lecture, ce qui est pratique pour l’automatisation côté serveur.

## Étape 3 : Charger le classeur enregistré et récupérer la propriété

Nous inversons maintenant le scénario : ouvrez le fichier que nous venons d’écrire et extrayez la valeur cachée. Cela montre que la propriété a survécu au aller‑retour.

```csharp
            // Step 4 – Load the workbook we just saved
            Workbook loadedWorkbook = new Workbook(outputPath);

            // Step 5 – Retrieve the value of the "ProjectId" custom property
            object projectIdValue = loadedWorkbook.Worksheets[0]
                                                .CustomProperties["ProjectId"]
                                                .Value;

            // Display the retrieved value
            System.Console.WriteLine($"Retrieved ProjectId: {projectIdValue}");
        }
    }
}
```

**Ce que vous devriez voir :**  
```
Retrieved ProjectId: 12345
```

Si le nom de la propriété est mal orthographié ou n’existe pas, l’indexeur `CustomProperties` lève une `KeyNotFoundException`. Une approche défensive serait :

```csharp
if (loadedWorkbook.Worksheets[0].CustomProperties.Contains("ProjectId"))
{
    // safe to read
}
```

## Exemple complet fonctionnel (toutes les étapes combinées)

Voici le programme complet, prêt à être copié‑collé dans un nouveau projet console. Aucun scaffolding supplémentaire n’est requis.

```csharp
using Aspose.Cells;
using System;

namespace ExcelCustomPropDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Add a custom property named "ProjectId" (add custom property excel)
            workbook.Worksheets[0].CustomProperties.Add("ProjectId", 12345);

            // 3️⃣ Save the workbook as XLSB (save workbook as xlsb)
            string filePath = @"C:\Temp\CustomProp.xlsb";
            workbook.Save(filePath, SaveFormat.Xlsb);

            // 4️⃣ Load the saved workbook back into memory
            Workbook loaded = new Workbook(filePath);

            // 5️⃣ Retrieve the custom property value (retrieve custom property value)
            object retrieved = loaded.Worksheets[0].CustomProperties["ProjectId"].Value;
            Console.WriteLine($"Retrieved ProjectId: {retrieved}");
        }
    }
}
```

Exécutez le programme, ouvrez `C:\Temp\CustomProp.xlsb` dans Excel, et vous ne remarquerez rien d’anormal en surface—car les propriétés personnalisées sont cachées par conception. Pourtant les données y résident, prêtes à être exploitées par tout processus en aval.

## Cas limites et variantes

| Situation | Ce qu’il faut ajuster |
|-----------|-----------------------|
| **Plusieurs feuilles** | Ajoutez la propriété à n’importe quelle feuille ; elle sera répliquée au niveau du classeur. |
| **Propriété chaîne** | `CustomProperties.Add("Status", "Approved")` – fonctionne de la même façon. |
| **Propriété manquante** | Utilisez `Contains` avant d’indexer pour éviter les exceptions. |
| **ID numériques volumineux** | Stockez‑les en `long` ou `string` pour éviter le débordement. |
| **Multiplateforme** | Aspose.Cells fonctionne sur .NET Core, .NET Framework et même Mono, donc le même code s’exécute dans des conteneurs Linux. |

## Questions fréquentes

**Q : Cette fonctionnalité fonctionne‑t‑elle avec la version d’essai gratuite d’Aspose.Cells ?**  
R : Oui. La version d’essai prend en charge pleinement `CustomProperties` et l’enregistrement en XLSB ; il suffit de garder à l’esprit le filigrane sur le fichier de sortie.

**Q : Puis‑je voir les propriétés personnalisées dans Excel ?**  
R : Dans Excel, allez dans *Fichier → Informations → Propriétés → Propriétés avancées → Personnalisées*. Votre “ProjectId” y sera répertorié.

**Q : Et si je dois supprimer une propriété ?**  
R : Appelez `CustomProperties.Remove("ProjectId")` avant d’enregistrer.

## Conclusion

Vous savez maintenant comment **créer un classeur Excel C#**, y intégrer une propriété personnalisée, **enregistrer le classeur au format XLSB**, puis **récupérer la valeur de la propriété personnalisée**. L’ensemble du flux tient dans une seule méthode, ce qui le rend très simple à intégrer dans des pipelines de reporting plus larges ou des services de génération de documents.

### Et après ?

- Explorez **l’ajout de plusieurs propriétés personnalisées** pour le versionnage, l’auteur ou les codes de département.  
- Combinez cette technique avec **des données au niveau des cellules** pour créer des rapports auto‑descriptifs.  
- Examinez **la lecture des propriétés personnalisées** à partir de fichiers XLSX tiers existants—Aspose.Cells les gère également.

N’hésitez pas à modifier l’exemple, à remplacer l’ID numérique par un GUID, ou à expérimenter avec d’autres formats de fichier. L’API est directe ; la vraie puissance réside dans la façon dont vous exploitez les métadonnées cachées dans votre logique métier.

Bon codage ! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}