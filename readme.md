# TP3 - Les formulaires en Symfony

Étudiant : Kissami Youssef  
Date :11 Décembre 2025  
Sujet : Création d'un formulaire de commande produit avec Symfony

## Description du projet

Ce projet implémente une page produit avec un formulaire de commande utilisant "Symfony" et "Bootstrap 5.3".

## Fonctionnalités implémentées

-  Affichage d'une page produit (Premium Wireless Headphones)
-  Formulaire avec validation (quantité entre 1 et 10)
-  Sélection de couleur (Matte Black, Pearl White, Silver)
-  Utilisation des Form Types Symfony
-  Personnalisation du formulaire avec Bootstrap via Twig
-  Message de confirmation après soumission (FlashMessages)

## Technologies utilisées

- Symfony 7.4 - Framework PHP
- Bootstrap 5.3 - Framework CSS
- Twig - Moteur de templates
- PHP 8.3
- Composer 2.9

## Structure du projet
```
src/
├── Controller/
│   └── ProductController.php    # Contrôleur gérant l'affichage et la soumission du formulaire
├── Form/
│   └── ProductOrderType.php     # Form Type définissant les champs du formulaire
templates/
├── base.html.twig               # Layout de base avec Bootstrap CDN
└── product/
    └── index.html.twig          # Page produit avec formulaire Symfony/Twig
```

## Installation et lancement
```bash
# Cloner le projet
git clone https://github.com/1youssef108/TP3_KissamiYoussef.git

# Accéder au dossier
cd TP3_KissamiYoussef

# Installer les dépendances
composer install

# Lancer le serveur
php -S 127.0.0.1:8001 -t public/
```

Puis ouvrir : **http://127.0.0.1:8001**

## Points techniques réalisés

### 1. Form Type (ProductOrderType)
- Utilisation de "IntegerType" pour la quantité avec contrainte `Range(min: 1, max: 10)`
- Utilisation de "ChoiceType" pour la sélection de couleur
- Attribution des classes Bootstrap directement dans les options du formulaire
- Ajout d'un bouton de soumission avec "SubmitType"

### 2. Controller (ProductController)
- Gestion de la soumission du formulaire avec `handleRequest()`
- Validation automatique avec `isValid()`
- Utilisation des "FlashMessages" pour afficher une confirmation
- Redirection après soumission (pattern PRG - Post/Redirect/Get)

### 3. Vue Twig (index.html.twig)
- Utilisation des fonctions Twig pour le rendu du formulaire :
  - `form_start()` et `form_end()`
  - `form_label()`, `form_widget()`, `form_errors()`
- Personnalisation des labels avec l'option `label_attr`
- Affichage des messages flash avec Bootstrap
- Structure responsive avec Bootstrap Grid (col-md-6)

### 4. Layout de base (base.html.twig)
- Import de Bootstrap 5.3 via CDN
- Structure HTML5 standard
- Bloc Twig pour l'extension des templates

## Explication du code

### ProductController.php
Le contrôleur crée le formulaire, gère sa soumission et affiche un message de confirmation :
```php
$form = $this->createForm(ProductOrderType::class);
$form->handleRequest($request);

if ($form->isSubmitted() && $form->isValid()) {
    $data = $form->getData();
    $this->addFlash('success', 'Produit ajouté au panier');
    return $this->redirectToRoute('app_product');
}
```

### ProductOrderType.php
Le Form Type définit la structure du formulaire avec validation :
php
->add('quantity', IntegerType::class, [
    'constraints' => [new Range(['min' => 1, 'max' => 10])]
])
->add('color', ChoiceType::class, [
    'choices' => ['Matte Black' => 'black', ...]
])

### index.html.twig
La vue utilise les fonctions Twig pour générer le formulaire HTML :
   twig
{{ form_start(form) }}
    {{ form_widget(form.quantity) }}
    {{ form_widget(form.color) }}
    {{ form_widget(form.submit) }}
{{ form_end(form) }}


## Ce que j'ai appris

- Comment créer et utiliser des "Form Types" dans Symfony
- Comment gérer la "validation" des formulaires
- Comment personnaliser les formulaires avec "Bootstrap" via Twig
- Comment utiliser les "FlashMessages" pour les notifications
- Comment structurer un projet Symfony de manière professionnelle

## Captures d'écran

La page affiche :
- Une image du produit (casque audio)
- Le titre et le prix ($129.99)
- Une description détaillée
- Les spécifications (Brand, Color, Connectivity, Battery Life)
- Un formulaire avec quantité et sélection de couleur
- Un bouton "Add to Cart"

## Améliorations possibles

- Ajout d'une base de données pour stocker les commandes
- Système de panier complet avec session
- Gestion de plusieurs produits
- Page de confirmation de commande
- Espace administration
- Authentification utilisateur

## Auteur

Kissami Youssef
EHEI 2025/2026  
TP3 - Les formulaires en Symfony