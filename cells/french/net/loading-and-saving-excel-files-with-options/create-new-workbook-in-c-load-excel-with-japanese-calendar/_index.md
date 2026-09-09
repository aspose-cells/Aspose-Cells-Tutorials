---
category: general
date: 2026-02-26
description: Créez un nouveau classeur en C# et apprenez à charger des fichiers Excel,
  à définir le calendrier en japonais et à extraire les dates d’Excel sans effort.
draft: false
keywords:
- create new workbook
- how to load excel
- how to set calendar
- extract date from excel
- read japanese dates
language: fr
og_description: Créez un nouveau classeur en C# et apprenez rapidement comment charger
  Excel, définir un calendrier japonais et extraire les dates des fichiers Excel.
og_title: Créer un nouveau classeur en C# – Charger Excel avec le calendrier japonais
tags:
- C#
- Excel
- Aspose.Cells
- DateTime
title: Créer un nouveau classeur en C# – Charger Excel avec le calendrier japonais
url: /fr/net/loading-and-saving-excel-files-with-options/create-new-workbook-in-c-load-excel-with-japanese-calendar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un nouveau classeur en C# – Charger Excel avec le calendrier japonais

Vous avez déjà eu besoin de **create new workbook** en C# mais vous ne saviez pas comment faire en sorte qu’Excel respecte le calendrier japonais ? Vous n’êtes pas seul. Dans de nombreux scénarios d’entreprise, vous recevrez des feuilles de calcul qui stockent les dates selon le système d’ère japonais, et extraire correctement ces dates peut ressembler à décoder un langage secret.

Voici le truc : vous pouvez **create new workbook**, indiquer au chargeur d’interpréter les dates en utilisant le calendrier japonais, puis **extract date from excel** en quelques lignes de code seulement. Dans ce guide, nous parcourrons *how to load excel*, *how to set calendar* pour les dates japonaises, et enfin *read Japanese dates* depuis une cellule. Pas de fioritures — juste un exemple complet et exécutable que vous pouvez copier‑coller dans votre projet.

## Prérequis

- .NET 6.0 ou version ultérieure (le code fonctionne également sur .NET Framework 4.6+)  
- La bibliothèque **Aspose.Cells** (version d’essai gratuite ou version sous licence). Installez‑la via NuGet :

```bash
dotnet add package Aspose.Cells
```

- Un fichier Excel (`JapanDates.xlsx`) contenant des dates d’ère japonaise dans la cellule A1.

C’est tout. Si vous avez cela, nous pouvons commencer immédiatement.

---

## Créer un nouveau classeur et définir le calendrier japonais

La première étape consiste à créer un objet **create new workbook** et à configurer le `LoadOptions` afin que l’analyseur sache quel calendrier utiliser.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateReader
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook workbook = new Workbook();

        // Step 2: Set load options to interpret dates using the Japanese calendar
        workbook.LoadOptions = new LoadOptions { Calendar = CalendarType.Japanese };

        // Step 3: Load the workbook from a file
        workbook.Load("YOUR_DIRECTORY/JapanDates.xlsx");

        // Step 4: Access cell A1 – it now contains a proper DateTime value
        var cellA1 = workbook.Worksheets[0].Cells["A1"];
        DateTime dateValue = cellA1.GetDateTime();

        Console.WriteLine($"The Japanese date in A1 is: {dateValue:yyyy-MM-dd}");
    }
}
```

> **Astuce :** La propriété `LoadOptions.Calendar` accepte plusieurs énumérations (`Gregorian`, `Japanese`, `Hijri`, etc.). Choisir la bonne garantit que la bibliothèque traduit le texte d’ère (par ex., « 令和3年 ») en un `DateTime` .NET.

![exemple de création d'un nouveau classeur](image-url.png "Capture d'écran montrant une instance de classeur avec les paramètres du calendrier japonais"){: .align-center alt="exemple de création d'un nouveau classeur"}

### Pourquoi cela fonctionne

- **Workbook creation**: `new Workbook()` vous donne une page blanche—pas de feuilles cachées, pas de données par défaut.
- **LoadOptions**: En assignant `CalendarType.Japanese` *avant* d’appeler `Load`, l’analyseur traite les chaînes basées sur les ères comme des dates plutôt que comme du texte brut.
- **GetDateTime()**: Après le chargement, `cellA1.GetDateTime()` renvoie un véritable objet `DateTime`, vous permettant d’effectuer des opérations arithmétiques, du formatage ou des insertions en base de données sans étapes de conversion supplémentaires.

---

## Comment charger correctement un fichier Excel

Vous vous demandez peut‑être : « Existe‑t‑il une façon particulière de **how to load excel** lorsqu’on travaille avec des calendriers non gregoriens ? » La réponse est oui — définissez toujours le `LoadOptions` *avant* d’appeler `Load`. Si vous chargez d’abord puis changez le calendrier, les dates ont déjà été analysées de façon incorrecte.

```csharp
// Example of a wrong order – will treat Japanese dates as plain strings
Workbook badWorkbook = new Workbook();
badWorkbook.Load("JapanDates.xlsx");          // Loads with default Gregorian calendar
badWorkbook.LoadOptions.Calendar = CalendarType.Japanese; // Too late!
```

L’extrait ci‑dessus montre un piège courant. L’ordre correct (comme indiqué dans la section précédente) garantit que le moteur interprète les cellules *comme des dates* dès le départ.

---

## Comment définir le calendrier pour les dates japonaises

Si vous devez changer de calendrier à la volée—par exemple, traiter un lot de fichiers utilisant différents systèmes d’ère—vous pouvez réutiliser le même objet `Workbook` avec un nouveau `LoadOptions` à chaque fois.

```csharp
void LoadWithCalendar(string filePath, CalendarType calendar)
{
    Workbook wb = new Workbook
    {
        LoadOptions = new LoadOptions { Calendar = calendar }
    };
    wb.Load(filePath);
    // Now you can read dates according to the chosen calendar
}
```

Appeler `LoadWithCalendar("JapanDates.xlsx", CalendarType.Japanese)` donne le même résultat que notre exemple principal, tandis que `CalendarType.Gregorian` traiterait la même cellule comme une simple chaîne (ou lancerait une exception si le format est incompréhensible).

---

## Extraire la date d’Excel – Lire les dates japonaises

Maintenant que le classeur est chargé avec le calendrier approprié, extraire la date est simple. La méthode `Cell.GetDateTime()` renvoie un `DateTime` qui respecte la conversion d’ère.

```csharp
DateTime ExtractJapaneseDate(Workbook wb, string address)
{
    var cell = wb.Worksheets[0].Cells[address];
    return cell.GetDateTime(); // Returns a .NET DateTime
}

// Usage
DateTime japaneseDate = ExtractJapaneseDate(workbook, "A1");
Console.WriteLine($"Extracted date: {japaneseDate:d}");
```

### Cas limites et scénarios « What‑If »

| Situation                              | Que faire                                                                                               |
|----------------------------------------|----------------------------------------------------------------------------------------------------------|
| La cellule contient du **texte** au lieu d’une date | Appelez d’abord `cell.GetString()`, validez avec `DateTime.TryParse`, ou imposez une validation des données dans Excel. |
| Plusieurs feuilles de calcul nécessitent un traitement    | Parcourez `workbook.Worksheets` et appliquez la même logique d’extraction à chaque feuille.                   |
| Les dates sont stockées sous forme de **nombres** (séries Excel) | `cell.GetDateTime()` fonctionne toujours car Aspose.Cells convertit automatiquement les nombres de série.            |
| Le fichier est **protégé par mot de passe**         | Utilisez `LoadOptions.Password = "yourPwd"` avant d’appeler `Load`.                                           |

---

## Exemple complet fonctionnel (prêt à copier‑coller)

Voici le programme complet que vous pouvez insérer dans une application console. Il inclut la gestion des erreurs et montre les quatre mots‑clés secondaires dans leur contexte.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateReader
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // 1️⃣  Create new workbook and configure calendar (primary keyword)
        // --------------------------------------------------------------------
        Workbook workbook = new Workbook
        {
            LoadOptions = new LoadOptions { Calendar = CalendarType.Japanese }
        };

        // --------------------------------------------------------------------
        // 2️⃣  How to load excel – correct order matters (secondary keyword)
        // --------------------------------------------------------------------
        try
        {
            workbook.Load("YOUR_DIRECTORY/JapanDates.xlsx");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load Excel file: {ex.Message}");
            return;
        }

        // --------------------------------------------------------------------
        // 3️⃣  How to set calendar – already done before loading (secondary)
        // --------------------------------------------------------------------
        // (If you need to change it later, see the LoadWithCalendar method above.)

        // --------------------------------------------------------------------
        // 4️⃣  Extract date from excel – read Japanese dates (secondary keywords)
        // --------------------------------------------------------------------
        try
        {
            var cell = workbook.Worksheets[0].Cells["A1"];
            DateTime japaneseDate = cell.GetDateTime(); // Proper DateTime thanks to the calendar setting
            Console.WriteLine($"Japanese date in A1 → {japaneseDate:yyyy-MM-dd}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error extracting date: {ex.Message}");
        }
    }
}
```

**Sortie attendue** (en supposant que A1 contient « 令和3年5月12日 ») :

```
Japanese date in A1 → 2021-05-12
```

Si la cellule contient une date grégorienne comme « 2021‑05‑12 », le même code fonctionne toujours car la bibliothèque revient élégamment à l’interprétation grégorienne.

## Conclusion

Vous savez maintenant comment **create new workbook**, **how to load excel** correctement, définir le **how to set calendar** approprié, et enfin **extract date from excel** tout en **read Japanese dates** sans aucun parsing manuel. L’essentiel à retenir est que le calendrier doit être défini *avant* le chargement ; une fois le classeur en mémoire, les dates sont déjà matérialisées en objets `DateTime` appropriés.

### Et après ?

- **Batch processing** : Parcourez un dossier de fichiers, en appelant `LoadWithCalendar` pour chacun.  
- **Export to other formats** : Utilisez `workbook.Save("output.csv")` après conversion.  
- **Localization** : Combinez `CultureInfo` avec `DateTime.ToString` pour afficher les dates dans la langue préférée de l’utilisateur.

N’hésitez pas à expérimenter—remplacez `CalendarType.Japanese` par `CalendarType.Hijri` ou `CalendarType.Gregorian` et observez le même code s’adapter automatiquement. Si vous rencontrez des problèmes, laissez un commentaire ci‑dessous ou consultez la documentation d’Aspose.Cells pour des informations API plus approfondies.

Bon codage, et profitez de la transformation de ces mystérieuses dates d’ère japonaise en valeurs .NET `DateTime` propres !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}