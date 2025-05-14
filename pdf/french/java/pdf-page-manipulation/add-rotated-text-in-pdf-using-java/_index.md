---
"description": "Apprenez à insérer du texte pivoté dans un document PDF avec Java. Suivez ce guide détaillé, étape par étape, avec des exemples de code pour enrichir vos PDF avec du texte pivoté."
"linktitle": "Ajouter du texte pivoté dans un PDF à l'aide de Java"
"second_title": "API de traitement PDF Java Aspose.PDF"
"title": "Ajouter du texte pivoté dans un PDF à l'aide de Java"
"url": "/fr/java/pdf-page-manipulation/add-rotated-text-in-pdf-using-java/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter du texte pivoté dans un PDF à l'aide de Java


## Introduction

Dans ce tutoriel complet, nous allons explorer le processus d'ajout de texte pivoté à un document PDF avec Java. Que vous ayez besoin d'étiqueter des diagrammes, de créer des filigranes ou d'ajouter des effets spéciaux à vos PDF, ce guide vous guidera pas à pas. Nous utiliserons Aspose.PDF pour Java, une puissante bibliothèque de manipulation de PDF, pour illustrer le processus.

## Prérequis

Avant de commencer, assurez-vous que les conditions préalables suivantes sont en place :

1. Environnement de développement Java : assurez-vous que Java est installé sur votre système.

2. Aspose.PDF pour Java : Téléchargez et intégrez la bibliothèque Aspose.PDF à votre projet Java. Vous trouverez le lien de téléchargement. [ici](https://releases.aspose.com/pdf/java/).

## Étape 1 : Créer un nouveau document PDF

Commençons par créer un nouveau document PDF avec Aspose.PDF. Ce document servira de canevas pour notre texte pivoté.

```java
// Initialiser le document PDF
com.aspose.pdf.Document pdfDocument = new com.aspose.pdf.Document();
```

## Étape 2 : Ajouter une page

Ensuite, ajoutez une page au document PDF où vous souhaitez insérer le texte pivoté :

```java
// Ajouter une nouvelle page au document
com.aspose.pdf.Page page = pdfDocument.getPages().add();
```

## Étape 3 : Définir le texte pivoté

Définissons maintenant le texte à insérer et à faire pivoter. Vous pouvez personnaliser le texte, la police et l'angle de rotation selon vos besoins :

```java
// Définir le contenu du texte
String text = "Rotated Text Example";

// Créer un objet TextFragment
com.aspose.pdf.TextFragment textFragment = new com.aspose.pdf.TextFragment(text);

// Définir la taille et le style de la police
textFragment.getTextState().setFontSize(12);
textFragment.getTextState().setFont(com.aspose.pdf.FontRepository.findFont("Arial"));

// Définir l'angle de rotation (en degrés)
textFragment.setTextRotation(45);
```

Dans cet exemple, nous avons défini le texte sur « Exemple de texte pivoté », choisi la police Arial, défini la taille de police sur 12 et pivoté le texte de 45 degrés. Ajustez ces paramètres selon vos besoins.

## Étape 4 : Positionnez le texte pivoté

Spécifiez la position sur la page où vous souhaitez placer le texte pivoté :

```java
// Définir la position du texte
textFragment.setPosition(new com.aspose.pdf.Position(100, 200));
```

Ici, nous avons positionné le texte aux coordonnées (100, 200) sur la page. Modifiez ces coordonnées pour placer le texte précisément là où vous le souhaitez.

## Étape 5 : Ajouter du texte pivoté à la page

Maintenant, ajoutez le texte pivoté à la page :

```java
// Ajouter le texte pivoté à la page
page.getParagraphs().add(textFragment);
```

## Étape 6 : Enregistrer le PDF

Enfin, enregistrez le document PDF avec le texte pivoté :

```java
// Enregistrer le document PDF
pdfDocument.save("output.pdf");
```

## Conclusion

Dans ce tutoriel, nous avons exploré le processus d'ajout de texte pivoté à un document PDF avec Java et Aspose.PDF pour Java. Vous avez appris à créer un PDF, à définir du texte pivoté avec des styles personnalisés, à le positionner sur la page et à enregistrer le PDF modifié.

Le texte pivoté peut être un ajout précieux à vos PDF à diverses fins, telles que l'étiquetage de diagrammes, le filigrane ou l'ajout d'éléments créatifs à vos documents.

Améliorez vos documents PDF en incorporant facilement du texte pivoté, grâce aux fonctionnalités d'Aspose.PDF pour Java.

---

## FAQ (Foire aux questions)

### 1. Puis-je faire pivoter le texte selon différents angles dans le même PDF ?
   Oui, vous pouvez ajouter plusieurs occurrences de texte pivoté sous différents angles au même document PDF. Répétez simplement la procédure décrite dans ce tutoriel pour chaque occurrence de texte pivoté.

### 2. Comment puis-je changer la couleur du texte pivoté ?
   Pour changer la couleur du texte, utilisez le `textFragment.getTextState().setForegroundColor` et spécifiez la couleur au format RVB. Par exemple, pour définir la couleur du texte sur rouge, utilisez `textFragment.getTextState().setForegroundColor(com.aspose.pdf.Color.getRed());`.

### 3. Aspose.PDF pour Java est-il une bibliothèque gratuite ?
   Aspose.PDF pour Java est une bibliothèque commerciale puissante, mais une version d'essai gratuite est disponible pour les tests et l'évaluation. Selon les besoins de votre projet, vous pouvez choisir une option de licence adaptée.

### 4. Puis-je faire pivoter le texte de 90 degrés pour créer du texte vertical ?
   Oui, vous pouvez faire pivoter le texte de 90 degrés pour créer un texte vertical. Réglez simplement l'angle de rotation à 90 degrés pour que le texte s'affiche verticalement sur la page.

### 5. Existe-t-il d’autres bibliothèques permettant de travailler avec des fichiers PDF en Java ?
   Oui, plusieurs bibliothèques, telles qu'iText et PDFBox, sont disponibles pour la manipulation de PDF en Java. Chaque bibliothèque possède ses propres fonctionnalités ; choisissez donc celle qui correspond le mieux aux besoins de votre projet.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}