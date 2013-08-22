# General notes, advice and guidelines for Multibrands project

It is important that we all work in a unified way in order to, among other things:

* Keep stylesheets maintainable
* Keep code transparent and readable
* Keep stylesheets scalable


HTML Document Anatomy
CSS Document Anatomy
JS Document Anatomy

## Contents

<!-- * [HTML document anatomy](#html-document-anatomy)
* [CSS document anatomy](#css-document-anatomy)
  * [General](#general)
  * [One file vs. many files](#one-file-vs-many-files)
  * [Table of contents](#table-of-contents)
  * [Section titles](#section-titles)
* [Source order](#source-order)
* [Anatomy of rulesets](#anatomy-of-rulesets)
* [Naming conventions](#naming-conventions)
  * [JS hooks](#js-hooks)
  * [Internationalisation](#internationalisation)
* [Comments](#comments)
  * [Comments on steroids](#comments-on-steroids)
    * [Quasi-qualified selectors](#quasi-qualified-selectors)
    * [Tagging code](#tagging-code)
    * [Object/extension pointers](#objectextension-pointers)
* [Writing CSS](#writing-css)
* [Building new components](#building-new-components)
* [OOCSS](#oocss)
* [Layout](#layout)
* [Sizing UIs](#sizing-uis)
  * [Font sizing](#font-sizing)
* [Shorthand](#shorthand)
* [IDs](#ids)
* [Selectors](#selectors)
  * [Over qualified selectors](#over-qualified-selectors)
  * [Selector performance](#selector-performance)
* [CSS selector intent](#css-selector-intent)
* [`!important`](#important)
* [Magic numbers and absolutes](#magic-numbers-and-absolutes)
* [Conditional stylesheets](#conditional-stylesheets)
* [Debugging](#debugging)
* [Preprocessors](#preprocessors)
* [JS document anatomy](#js-document-anatomy) -->
---

## Sublime text

### Plugins indispensables

* [SassBeautify](https://github.com/badsyntax/SassBeautify)
* [DocBlockr](https://github.com/Warin/Sublime/tree/master/DocBlockr)
* Jade
* Sass

### Preferences

Go to preferences menu > Settings user and copy-past these lines :

```
{
  "bold_folder_labels": true,
  "default_encoding": "UTF-8",
  "detect_slow_plugins": false,
  "ensure_newline_at_eof_on_save": true,
  "fade_fold_buttons": false,
  "font_options":
  [
    "no_bold",
    "no_italic",
    "subpixel_antialias"
  ],
  "font_size": 10,
  "highlight_line": true,
  "ignored_packages":
  [
    "Vintage"
  ],
  "open_files_in_new_window": false,
  "shift_tab_unindent": true,
  "tab_size": 2,
  "translate_tabs_to_spaces": true,
  "trim_automatic_white_space": true,
  "trim_trailing_white_space_on_save": true
}
```

## HTML Document Anatomy


```
views
├── boxes
│   ├── box1
│   ├── box2
│   ├── box3
│   └── box5
├── layout
│   ├── desktop
│   │   ├── footer.jade
│   │   ├── header.jade
│   │   ├── layout-01.jade
│   │   ├── layout-02.jade
│   │   └── layout-03.scss
│   ├── mobile
├── modules
│   ├── footer.scss
│   ├── header.scss
│   └── main.scss
├── modules
│   ├── blocks
│   ├── footer
│   ├── header
│   ├── main
│   └── nav
├── index-01.jade
└── article.jade
```



## CSS Document Anatomy

No matter the document, we must always try and keep a common formatting. This means consistent commenting, consistent syntax and consistent naming.

### Table of contents

At the top of stylesheets, you need maintain a table of contents which will detail the sections contained in the document, for example:

```
#!css

/*------------------------------------*\
    $CONTENTS
\*------------------------------------*/
/**
 * CONTENTS............You’re reading it!
 * RESET...............Set our reset defaults
 * FONT-FACE...........Import brand font files
 */
```

This will tell the next developer(s) exactly what they can expect to find in this file. Each item in the table of contents maps directly to a section title.

If you are working in one big stylesheet, the corresponding section will also be in that file. If you are working across multiple files then each item in the table of contents will map to an include which pulls that section in.

## Section titles

The table of contents would be of no use unless it had corresponding section titles. Denote a section thus:

```
#!css

/*------------------------------------*\
    $NAME OF CATEGORIE
\*------------------------------------*/
```

You need to install [DocBlockr] on Sublime text if you want to facilitate comments.

```
#!css

/**
 * A comment in one line
 */


/**
 * A comment
 * in two lines
 */

```


You can check out the source of this page to see how that's done, and make sure to bookmark [the vast library of Pygment lexers][lexers], we accept the 'short name' or the 'mimetype' of anything in there.
[lexers]: http://pygments.org/docs/lexers/



## Coding Style

* Use soft-tabs with a two space indent.
* Put spaces after : in property declarations.
* Put spaces before { in rule declarations.
* Use hex color codes #000 unless using rgba.
* Use // for comment blocks (instead of /* */).

### Order

- Render and view
- Position
- Box sizing
- Typography
- Transformation and positions


* 1Le rendu et l’affichage : la propriété display pour modifier le mode de rendu du
composant, visilibity pour définir si ce dernier est affiché ou masqué et clip
pour spécifier la zone visible de l’élément.

* 2 Le positionnement : les propriétés float, position, top, right, bottom et left
pour modifier le positionnement de l’élément, z-index pour changer son ordre
d’empilement, clear pour rétablir le flux après l’utilisation d’un flottant et
vertical-align pour préciser son alignement vertical.

* 3 Le modèle de boîte (dans le sens extérieur-intérieur) : la propriété margin pour
fixer les marges externes de l’élément, border, padding, min-height, height, maxheight,
min-width, width, max-width pour spécifier ses dimensions, overflow pour
gérer les débordement de contenu et zoom pour conférer le layout à IE 6 et IE 7.

* 4 La typographie : la propriété font pour définir les caractéristiques globales de la
police de caractères, line-height pour spécifier son interlignage, text-align pour
gérer l’alignement horizontal, text-indent pour mettre la première ligne en retrait
et word-wrap pour choisir le style de renvoi à la ligne. Purement décoratives, les
autres propriétés telles que letter-spacing, word-spacing, text-transform, color
ou text-decoration sont également définies ici.

* 5 Les transformations et les transitions : les différentes valeurs de la propriété
transform pour appliquer une transformation à l’élément (rotate pour une
rotation, scale pour un redimensionnement, skewX et skewY pour une distorsion et
translate pour une translation) et transition pour assurer un effet de transition.

* 6 L’habillage : l’ensemble des propriétés qui n’ont pas encore été définies et qui
sont destinées à décorer l’élément, comme outline pour ajouter un contour,
opacity pour rendre l’élément partiellement transparent, cursor pour modifier
l’apparence du curseur ou encore background pour ajouter un arrière-plan.

* 7 Et enfin, le contenu généré grâce aux pseudo-éléments :before et :after.





## SCSS Style

Any $variable or @mixin that is used in more than one file should be put in globals/. Others should be put at the top of the file where they're used.
As a rule of thumb, don't nest further than 3 levels deep. If you find yourself going further, think about reorganizing your rules (either the specificity needed, or the layout of the nesting).

* List @extend(s) First
* List "Regular" Styles Next
* List @include(s) Next

Maximum Nesting: 50 Lines
Maximum Nesting: Three Levels Deep
Variablize All Common Numbers, and Numbers with Meaning
Be Generous With Comments



## Specificity (classes vs. ids)

It's important to use only **class name** in your html elements.
You only can put an id on form's elements.

### Smacss



## File Organization


```
sass
├── base
│   ├── forms
│   └── listings.scss
├── generic
│   ├── clearfix.scss
│   ├── debug.scss
│   ├── grid.scss
│   ├── helpers.scss
│   ├── mixins.scss
│   ├── normalize.scss
│   ├── utilities.scss
├── layout
│   ├── footer.scss
│   ├── header.scss
│   └── main.scss
├── modules
│   ├── article.scss
│   ├── box.scss
│   ├── breadcrumb.scss
│   ├── column.scss
│   ├── mobile-menu.scss
│   ├── navbar.scss
└── plugins
    ├── forms.scss
    └── markdown.scss
```



## JS Document Anatomy


Hierarchy
Do not use .block--left or .block--right
Do use .block--a and .block--b to semantically establish hierarchy

## Images

* bg-* for backgrounds
* icon-* for icons
* logo-* for logos
* img-* for generic images


