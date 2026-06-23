---
category: general
date: 2026-03-21
description: Apprenez à enregistrer des fichiers xlsb en C# tout en ajoutant une propriété
  personnalisée telle que ProjectId. Ce guide montre comment créer un classeur Excel,
  ajouter une propriété personnalisée et la vérifier.
draft: false
keywords:
- how to save xlsb
- add custom property
- create excel workbook
- how to add custom property
- add project id
language: fr
og_description: Découvrez comment enregistrer des fichiers xlsb et ajouter une propriété
  personnalisée telle que ProjectId en C#. Guide étape par étape avec le code complet.
og_title: Comment enregistrer un fichier XLSB – Ajouter une propriété personnalisée
  en C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Comment enregistrer un fichier XLSB – Ajouter une propriété personnalisée en
  C#
url: /fr/net/document-properties/how-to-save-xlsb-add-custom-property-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment enregistrer un XLSB – Ajouter une propriété personnalisée en C#

Vous êtes-vous déjà demandé **comment enregistrer des fichiers xlsb** tout en y glissant un morceau de métadonnées ? Peut‑être construisez‑vous un moteur de reporting qui a besoin d’un ProjectId caché, ou vous voulez simplement taguer des feuilles de calcul pour un traitement en aval. **Comment enregistrer un xlsb** n’est pas de la science-fiction, mais le combiner avec une propriété personnalisée ajoute une petite nuance que de nombreux développeurs négligent.

Dans ce tutoriel, nous allons créer un classeur Excel, ajouter une propriété personnalisée (oui, *add custom property*), persister le fichier en tant que classeur binaire **XLSB**, puis le recharger pour prouver que la propriété est bien restée. En chemin, nous aborderons également **how to add custom property** comme un ProjectId, afin que vous repartiez avec un modèle réutilisable pour vos projets futurs.

> **Astuce :** Si vous utilisez déjà la bibliothèque Aspose.Cells (le code ci‑dessous le fait), vous bénéficiez d’un support natif des propriétés personnalisées sans les tracas du COM interop.

---

## Prérequis

- .NET 6+ (ou .NET Framework 4.6+).  
- Aspose.Cells pour .NET – installer via NuGet : `Install-Package Aspose.Cells`.  
- Connaissances de base en C# – rien de compliqué, juste quelques instructions `using`.  

C’est tout. Pas d’installation d’Office, pas d’interop, uniquement du code géré pur.

---

## Étape 1 : Comment enregistrer un XLSB – Créer un classeur Excel

La toute première chose à faire est de créer un nouvel objet workbook. Pensez‑y comme à l’ouverture d’un fichier Excel vierge qui vit uniquement en mémoire jusqu’à ce que vous décidiez de l’écrire sur le disque.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook workbook = new Workbook();

        // (Optional) Give the first worksheet a friendly name
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Name = "DataSheet";

        // From here we can start adding data or properties…
```

Pourquoi commencer par un workbook ? Parce que **create excel workbook** est la base de toute manipulation ultérieure—que vous insériez plus tard des formules, des graphiques ou des propriétés personnalisées. La classe `Workbook` abstrait l’ensemble du fichier, tandis que `Worksheets` vous donne accès aux onglets individuels.

---

## Étape 2 : Ajouter une propriété personnalisée à la feuille

Vient maintenant la partie amusante—**add custom property**. Dans Aspose.Cells, vous pouvez attacher une propriété directement à une feuille (ou au classeur lui‑même). Ici, nous allons stocker un ProjectId numérique que les services en aval pourront lire sans toucher aux cellules visibles.

```csharp
        // Step 2: Add a custom property called "ProjectId"
        // The value 12345 could come from your database, config, etc.
        sheet.CustomProperties.Add("ProjectId", 12345);

        // You can also add string or date properties:
        // sheet.CustomProperties.Add("Author", "Jane Doe");
        // sheet.CustomProperties.Add("GeneratedOn", DateTime.UtcNow);
```

**Comment ajouter une propriété personnalisée** ? Il suffit d’appeler `CustomProperties.Add(name, value)`. L’API gère automatiquement le XML sous‑jacent, vous n’avez donc pas à vous soucier des détails de bas niveau. C’est la façon la plus sûre d’embarquer des métadonnées invisibles à l’utilisateur final.

---

## Étape 3 : Enregistrer le classeur au format XLSB

Le classeur est prêt et la propriété personnalisée attachée, il est temps de **how to save xlsb**. Le format XLSB stocke les données sous forme binaire, ce qui est généralement plus petit et plus rapide à ouvrir que le classique XLSX.

```csharp
        // Step 3: Define the output path – adjust as needed
        string outputPath = @"C:\Temp\WithCustomProp.xlsb";

        // Save the workbook in XLSB format
        workbook.Save(outputPath, SaveFormat.Xlsb);

        Console.WriteLine($"Workbook saved to {outputPath}");
```

Enregistrer en XLSB est aussi simple que de passer `SaveFormat.Xlsb` à la méthode `Save`. Si vous vous demandez si cela supprime la propriété personnalisée—rassurez‑vous, Aspose.Cells préserve les propriétés au niveau du classeur et de la feuille dans le fichier binaire.

---

## Étape 4 : Vérifier la propriété personnalisée

Une bonne pratique consiste à recharger le fichier et à confirmer que la propriété a survécu au aller‑retour. Cela montre également **how to add custom property** ultérieurement si vous devez la mettre à jour.

```csharp
        // Step 4: Load the saved XLSB to verify the property
        Workbook loaded = new Workbook(outputPath);

        // Retrieve the first worksheet again
        Worksheet loadedSheet = loaded.Worksheets[0];

        // Access the "ProjectId" custom property
        var projectId = loadedSheet.CustomProperties["ProjectId"].Value;

        Console.WriteLine($"Loaded ProjectId: {projectId}"); // Should print 12345
    }
}
```

Si la console affiche `12345`, vous avez réussi à **how to save xlsb** *et* **add project id** en une seule opération. La propriété vit dans les métadonnées internes du fichier, invisible dans l’interface mais parfaitement lisible par le code.

---

## Conseils supplémentaires : Ajouter plusieurs propriétés & cas particuliers

### Ajouter plus d’une propriété

Vous pouvez empiler autant de propriétés que vous le souhaitez :

```csharp
sheet.CustomProperties.Add("Department", "Finance");
sheet.CustomProperties.Add("IsConfidential", true);
```

### Mettre à jour une propriété existante

Si une propriété existe déjà, il suffit d’affecter une nouvelle valeur :

```csharp
sheet.CustomProperties["ProjectId"].Value = 67890; // Overwrites the old ID
```

### Gérer les propriétés manquantes

Tenter de lire une propriété inexistante lève une `KeyNotFoundException`. Protégez‑vous contre cela :

```csharp
if (sheet.CustomProperties.ContainsKey("ClientCode"))
{
    var clientCode = sheet.CustomProperties["ClientCode"].Value;
    // Use clientCode...
}
else
{
    Console.WriteLine("ClientCode property not found.");
}
```

### Compatibilité inter‑versions

XLSB fonctionne sur Excel 2007 + et sur la version web d’Excel. En revanche, les versions Office plus anciennes (< 2007) ne peuvent pas ouvrir les fichiers XLSB. Si vous avez besoin d’une compatibilité plus large, envisagez d’enregistrer une seconde copie au format XLSX.

### Considérations de performance

Les fichiers binaires XLSB sont généralement 30‑50 % plus petits que les XLSX, et ils se chargent plus rapidement. Pour de gros jeux de données (des centaines de milliers de lignes), le gain de vitesse peut être notable.

---

## Exemple complet

Voici le programme complet que vous pouvez copier‑coller dans un projet console. Il inclut toutes les étapes, la gestion des erreurs et les commentaires nécessaires pour être opérationnel immédiatement.

```csharp
using Aspose.Cells;
using System;

class SaveXlsbWithCustomProperty
{
    static void Main()
    {
        try
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Name = "DataSheet";

            // 2️⃣ Add a custom property (ProjectId) – this is how to add custom property
            sheet.CustomProperties.Add("ProjectId", 12345);
            sheet.CustomProperties.Add("CreatedBy", Environment.UserName);
            sheet.CustomProperties.Add("GeneratedOn", DateTime.UtcNow);

            // 3️⃣ Save as XLSB – this shows how to save xlsb
            string path = @"C:\Temp\WithCustomProp.xlsb";
            workbook.Save(path, SaveFormat.Xlsb);
            Console.WriteLine($"✅ Workbook saved as XLSB to {path}");

            // 4️⃣ Load the file back and verify the property
            Workbook loaded = new Workbook(path);
            Worksheet loadedSheet = loaded.Worksheets[0];

            if (loadedSheet.CustomProperties.ContainsKey("ProjectId"))
            {
                var projId = loadedSheet.CustomProperties["ProjectId"].Value;
                Console.WriteLine($"🔎 Loaded ProjectId: {projId}"); // Expected: 12345
            }
            else
            {
                Console.WriteLine("❗ ProjectId not found after loading.");
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }
}
```

**Sortie attendue**

```
✅ Workbook saved as XLSB to C:\Temp\WithCustomProp.xlsb
🔎 Loaded ProjectId: 12345
```

Si vous voyez le résultat ci‑dessus, vous avez maîtrisé **how to save xlsb**, **add custom property**, et **add project id**—le tout dans un extrait propre et réutilisable.

---

## FAQ

**Q : Cela fonctionne‑t‑il avec .NET Core ?**  
R : Absolument. Aspose.Cells est compatible .NET Standard, donc le même code fonctionne sur .NET 5/6/7 et sur .NET Framework.

**Q : Puis‑je ajouter une propriété personnalisée à l’ensemble du classeur plutôt qu’à une seule feuille ?**  
R : Oui. Utilisez `workbook.CustomProperties.Add("Key", value);` pour l’attacher au niveau du classeur.

**Q : Et si je dois stocker une longue chaîne (par ex. JSON) comme propriété ?**  
R : L’API accepte des chaînes de toute longueur, mais gardez à l’esprit que des blobs très volumineux peuvent augmenter la taille du fichier. Pour des données massives, envisagez une feuille cachée à la place.

**Q : La propriété personnalisée est‑elle visible dans l’interface d’Excel ?**  
R : Pas directement. Les utilisateurs peuvent la voir via **Fichier → Infos → Propriétés → Propriétés avancées → Personnalisées**, mais elle n’apparaît pas dans la grille.

---

## Conclusion

Nous avons couvert **how to save xlsb** en C# tout en **ajoutant une propriété personnalisée** telle qu’un ProjectId. En suivant le schéma pas à pas—**create excel workbook**, **add custom property**, **save as XLSB**, et **verify**—vous disposez maintenant d’une référence solide, citable, qui fonctionne tant pour les moteurs de recherche que pour les assistants IA.

Ensuite, vous pourriez explorer :

- **How to add custom property** à plusieurs feuilles dans une boucle.  
- Exporter des données depuis un DataTable vers le classeur avant l’enregistrement.  
- Chiffrer le fichier XLSB pour une sécurité supplémentaire.

N’hésitez pas à expérimenter, à modifier les noms de propriétés, ou à remplacer le format binaire par XLSX si vous avez besoin d’une compatibilité plus large. Vous avez un scénario difficile ? Laissez un commentaire, et nous résoudrons le problème ensemble. Bon codage !  

![how to save xlsb example](

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}