---
"date": "2025-04-08"
"description": "Apprenez à utiliser Aspose.Cells pour Java pour ajouter des zones de texte et définir l'interligne dans vos classeurs Excel. Améliorez la présentation de vos classeurs avec des formes de texte stylisées."
"title": "Ajouter une zone de texte et définir l'espacement des lignes dans Excel à l'aide d'Aspose.Cells pour Java"
"url": "/fr/java/images-shapes/aspose-cells-java-add-text-box-line-spacing/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Ajouter une zone de texte et définir l'espacement des lignes dans Excel à l'aide d'Aspose.Cells pour Java

## Introduction

Créer des rapports Excel dynamiques nécessite souvent une mise en forme de texte personnalisée, comme l'ajout de zones de texte avec un interligne spécifique. Avec Aspose.Cells pour Java, cela devient simple et efficace. Ce tutoriel vous guidera dans l'amélioration des présentations de vos classeurs grâce à Aspose.Cells pour Java pour ajouter des formes de texte stylisées.

À la fin de ce guide, vous apprendrez à :
- Créez un nouveau classeur Excel et accédez à ses feuilles de calcul
- Ajouter une forme de zone de texte à une feuille de calcul
- Définir un espacement de ligne personnalisé à l'intérieur d'une forme de texte
- Enregistrez votre classeur formaté au format XLSX

Commençons par configurer votre environnement.

### Prérequis

Avant de commencer, assurez-vous d’avoir les éléments suivants :
- Java Development Kit (JDK) installé sur votre machine
- Un IDE ou un éditeur pour écrire du code Java
- Système de build Maven ou Gradle configuré pour gérer les dépendances

Une compréhension de base de la programmation Java et une familiarité avec les structures de fichiers Excel seront bénéfiques.

## Configuration d'Aspose.Cells pour Java

Incluez Aspose.Cells dans la gestion des dépendances de votre projet à l'aide de Maven ou Gradle :

**Maven**

Ajoutez le bloc de dépendance suivant à votre `pom.xml` déposer:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**

Incluez ceci dans votre `build.gradle` déposer:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

Ensuite, acquérez une licence pour Aspose.Cells en optant pour un essai gratuit, en demandant une licence temporaire ou en achetant une licence complète.

### Initialisation d'Aspose.Cells

Une fois la bibliothèque incluse dans votre projet, initialisez-la au sein de votre application Java :

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) {
        // Initialiser une instance de Workbook (représente un fichier Excel)
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## Guide de mise en œuvre

### Créer un classeur et accéder à une feuille de calcul

Commencez par créer un nouveau classeur Excel et accédez à sa première feuille de calcul. C'est ici que vous ajouterez votre zone de texte.

#### Aperçu

La création d'un nouveau classeur fournit une ardoise vierge pour ajouter des données, des formes et une mise en forme selon les besoins.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

public class ExcelDemo {
    public static void main(String[] args) {
        // Créer un nouveau classeur (fichier Excel)
        Workbook workbook = new Workbook();
        
        // Accéder à la première feuille de calcul
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        System.out.println("Workbook and first worksheet accessed.");
    }
}
```

### Ajouter une zone de texte à la feuille de calcul

Ajoutez ensuite une zone de texte à la feuille de calcul sélectionnée. Cette zone peut contenir le texte de votre choix.

#### Aperçu

Les zones de texte sont des outils polyvalents permettant d'inclure des textes personnalisés tels que des notes ou des instructions directement dans une feuille Excel.

```java
import com.aspose.cells.Shape;
import com.aspose.cells.MsoDrawingType;

public class ExcelDemo {
    public static void main(String[] args) {
        // Créer un nouveau classeur (fichier Excel)
        Workbook workbook = new Workbook();
        
        // Accéder à la première feuille de calcul
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Ajouter une forme de zone de texte à la feuille de calcul
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        System.out.println("Text box added.");
    }
}
```

### Définir le texte dans la forme

Une fois votre zone de texte prête, définissez son contenu et formatez le texte qu'elle contient.

```java
import com.aspose.cells.Shape;

public class ExcelDemo {
    public static void main(String[] args) {
        // Créer un nouveau classeur (fichier Excel)
        Workbook workbook = new Workbook();
        
        // Accéder à la première feuille de calcul
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Ajouter une forme de zone de texte à la feuille de calcul
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Définir le contenu du texte à l'intérieur de la forme
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        System.out.println("Text set in shape.");
    }
}
```

### Accéder aux paragraphes de texte dans Shape

Vous pouvez accéder à des paragraphes individuels dans une zone de texte pour appliquer une mise en forme spécifique.

```java
import com.aspose.cells.TextParagraph;

public class ExcelDemo {
    public static void main(String[] args) {
        // Créer un nouveau classeur (fichier Excel)
        Workbook workbook = new Workbook();
        
        // Accéder à la première feuille de calcul
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Ajouter une forme de zone de texte à la feuille de calcul
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Définir le contenu du texte à l'intérieur de la forme
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Accéder au deuxième paragraphe de la forme
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);
        
        System.out.println("Accessed second paragraph in text box.");
    }
}
```

### Définir l'espacement des lignes du paragraphe

Personnaliser l'interligne peut améliorer la lisibilité. Voici comment le configurer :

```java
import com.aspose.cells.LineSpaceSizeType;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Créer un nouveau classeur (fichier Excel)
        Workbook workbook = new Workbook();
        
        // Accéder à la première feuille de calcul
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Ajouter une forme de zone de texte à la feuille de calcul
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Définir le contenu du texte à l'intérieur de la forme
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Accéder au deuxième paragraphe de la forme
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Définir l'espacement des lignes à 20 points
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // Configurer l'espace avant et après le paragraphe
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        System.out.println("Line spacing set.");
    }
}
```

### Enregistrer le classeur

Enfin, enregistrez votre classeur avec la zone de texte nouvellement ajoutée et formatée.

```java
import com.aspose.cells.SaveFormat;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Créer un nouveau classeur (fichier Excel)
        Workbook workbook = new Workbook();
        
        // Accéder à la première feuille de calcul
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Ajouter une forme de zone de texte à la feuille de calcul
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Définir le contenu du texte à l'intérieur de la forme
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Accéder au deuxième paragraphe de la forme
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Définir l'espacement des lignes à 20 points
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // Configurer l'espace avant et après le paragraphe
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        // Enregistrer le classeur
        workbook.save("StyledTextShape.xlsx", SaveFormat.XLSX);
    }
}
```

## Conclusion

Vous avez appris à ajouter une zone de texte et à définir l'interligne dans un classeur Excel avec Aspose.Cells pour Java. Cela vous permet de créer des rapports dynamiques et attrayants.

## Recommandations de mots clés
- « Aspose.Cells pour Java »
- « Ajouter une zone de texte dans Excel »
- « Définir l'espacement des lignes dans Excel »
- « Classeur Excel avec texte stylisé »
- « Java et Aspose.Cells »


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}