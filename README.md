# Introduction

Here you’ll find a quick guide on CSS for the KnowNative app. KnowNative uses SASS with SCSS syntax and BEM as the naming convention. BEM is used somewhat loosely here. The only rule enforced is that all class names must be prefixed by the component name. This prevents class name conflicts.

# Getting Started

## Installation

SASS is likely already installed. If not, follow these steps in the terminal to bring SASS into your project:

```
cd client
npm install
```

## Converting a CSS file to SASS

All the files in the project should already have the .scss extension. If not, simply rename the file from

```.css``` to ```.scss```

SCSS files interpret vanilla CSS automatically. The build tool (currently Vite) will also automatically watch these files and compile them to CSS in the background as you make changes.

## Rule One

All class names must be prefixed by the component name

🚫 These class names can lead to problems because title is a repeated class and pollutes the namespace.

```
<!-- Card Component -->
<div class="card">
  <h2 class="title">Card Title</h2>
</div>

<!-- Modal Component -->
<div class="modal">
  <h2 class="title">Modal Title</h2>
</div>
```

✅ Much better!

```
<!-- Card Component -->
<div class="card">
  <h2 class="card__title">Card Title</h2>
</div>

<!-- Modal Component -->
<div class="modal">
  <h2 class="modal__title">Modal Title</h2>
</div>
```

\*\*the double underscore ```__``` is a BEM naming convention. Learn more about BEM below.

## Rule Two

When creating SASS variables, use ```$``` instead of ```--var```.

Both syntaxes are valid. The SASS syntax has been chosen to ensure consistency and conciseness across the codebase.

🚫 Vanilla CSS syntax can be verbose
```
:root {
  --primary-color: #3498db;
  --font-size-large: 1.5rem;
  --spacing-unit: 16px;
}
button {
  background-color: var(--primary-color);
  font-size: var(--font-size-large);
  padding: var(--spacing-unit);
}
```

✅ Much better!
```
$primary-color: #3498db;
$font-size-large: 1.5rem;
$spacing-unit: 16px;

button {
  background-color: $primary-color;
  font-size: $font-size-large;
}
```

# FAQs

## What’s SASS?

Sass, or Syntactically Awesome Style Sheets, is a CSS pre-processor. SASS Basics

## Why do we need SASS?

CSS has a lot of modern features but browser support is often missing. Nesting, mixins, loops, and functions are all available to use but many browsers do not render this CSS correctly.

CSS pre-processors like SASS take these advanced features and compile them into vanilla CSS that can be rendered correctly by a majority of browsers.

## What’s the difference between SASS and SCSS?

SASS has two different syntaxes. The first is .sass and the second is .scss. KnowNative uses the SCSS syntax.

The great thing about SCSS is that it accepts vanilla CSS. This means developers can continue to write CSS as they always have and bring in advanced SASS features only as needed.

SCSS Syntax - uses {} and ; - accepts vanilla CSS
```
.primary-navigation {
    padding: 1rem;

    ul {
      display: flex;
      gap: 1rem;
      list-style: none;
      margin: 0;
      padding: 0;
    }

    a {
      text-transform: uppercase;
      text-decoration: none;
    }
}
```

SASS Syntax - more concise - doesn’t accept vanilla CSS
```
.primary-navigation
  padding: 1rem
  ul
    display: flex
    gap: 1rem
    list-style: none
    margin: 0
    padding: 0
  a
    text-transform: uppercase
    text-decoration: none
```

Read more at @Sass Fundamentals

## What’s BEM?

BEM (Block, Element, Modifier) is a naming convention for classes in HTML and CSS. Basically, it is a methodology to help write more readable CSS code. Introduction to BEM

## Why do we need BEM?

BEM prevents class name conflicts and helps keep code more organized.

Consider this example:

HTML
```
<div class="card card--light">
   <img class="card__image src="https://unsplash.it/300 alt="">
   <h2>I'm a light card</h2>
   <p class="card__body">And here would be the content of my card</p>
</div>

<div class="card card--dark">
   <img class="card__image src="https://unsplash.it/300 alt="">
   <h2>I'm a dark card</h2>
   <p class="card__body">And here would be the content of my card</p>
</div>
```
CSS
```
.card {
  margin: 2em;
  max-width: 300px;
  padding: 2em;
  box-shadow: 0 10px 30px -10px rgba(0,0,0..45);
}

.card--light {
  background: #eee
  color: black;
}

.card--dark {
  background: #333;
  color: white;
}
```
This example was pulled from Kevin Powell’s excellent tutorial: link here

Explanation:

Each of the cards is a block (parent)

The image is an element (child) of the card and is thus prefixed by the parent name card and a double underscore ```__```

Variants of a block or element are called modifiers and are prefixed by a double hyphen ```--```

Try it yourself:

If we wanted to add a new subtitle to both cards and one card’s subtitle is red, we can name the new CSS class as

```card__subtitle--red```

As mentioned above, KnowNative is not super strict with the BEM naming convention. BEM is more of a guide to make writing CSS class names easier and more readable. If you would like to learn more about BEM, take a look at the best practices section below.

# Best Practices

## Using SASS to prefix all class names with the component name

Manually prefixing all CSS class names with the component name can be tedious. Thankfully SASS has a feature that makes it much easier. Here’s how nesting and the & selector can make CSS code more readable:

Pre-compiled .scss file
```
.card {
  background-color: #fff;
  border: 1px solid #ddd;
    &--header {
    font-size: 1.5em;
    padding: 10px;
    }
  &__body {
    padding: 15px;

    &--highlighted {
      background-color: #f0f8ff;
    }
  }
  &__footer {
    padding: 10px;
    text-align: right;
  }
}
```
Compiled .css file
```
.card {
  background-color: #fff;
  border: 1px solid #ddd;
}
.card__header {
  font-size: 1.5em;
  padding: 10px;
}
.card__body {
  padding: 15px;
}
.card__body--highlighted {
  background-color: #f0f8ff;
}
.card__footer {
  padding: 10px;
  text-align: right;
}
```
Explanation:

The & syntax in SASS refers to the parent selector, creating prefixed class names.

The ```__``` (double underscore) syntax is used for elements inside the parent selector.

The ```--``` (double hyphen) syntax is used for modifiers such as --highlighted or --active .

This method ensures all classes within .card are properly namespaced.

## Avoid ‘grandchild’ selectors with multiple underscores ```__```

If an Element is nested two levels deep inside of a Block, just use one double underscore ```__```

🚫 Multiple underscores leads to really long class names
```
<div class="c-card">
    <div class="c-card__header">
        <!-- Here comes the grandchild… -->
        <h2 class="c-card__header__title">Title text here</h2>
    </div>
    <div class="c-card__body">
        <img class="c-card__body__img" src="some-img.png" alt="description">
        <p class="c-card__body__text">Lorem ipsum dolor sit amet, consectetur</p>
        <p class="c-card__body__text">Adipiscing elit.
            <a href="/somelink.html" class="c-card__body__text__link">Pellentesque amet</a>
        </p>
    </div>
</div>
```
✅ Much better!
```
<div class="c-card">
    <div class="c-card__header">
        <h2 class="c-card__title">Title text here</h2>
    </div>
    <div class="c-card__body">
        <img class="c-card__img" src="some-img.png" alt="description">
        <p class="c-card__text">Lorem ipsum dolor sit amet, consectetur</p>
        <p class="c-card__text">Adipiscing elit.
            <a href="/somelink.html" class="c-card__link">Pellentesque amet</a>
        </p>
    </div>
</div>
```
## Use classes instead of tags

🚫 Let’s say you have a table with these style rules:
```
td.data { background-color: white }
td.summary { background-color: yellow }
```
However, in another component, you need to redefine the background of a particular cell:
```
.final-summary { background-color: green }
```
This wouldn’t work because tag.class always has a higher specificity than just .class.

You would add a tag name to the rule to make it work:
```
td.final-summary { background-color: green }
```
✅ Code is simpler and specificity is low and consistent across all three selectors
```
.cell__data { background-color: white }
.cell__summary { background-color: yellow }
.cell__final-summary { background-color: green }
```
## Avoid nesting classes (whenever possible)

🚫 Specificity is high

SCSS
```
.navbar {
  .list__item {
  margin: 0;
  padding: 0;
  list-style: none;
  }

  .navbar__list { display: inline-block; }
}
```
Compiled CSS
```
.navbar .list__item {
  margin: 0;
  padding: 0;
  list-style: none;
}
.navbar .navbar__list {
  display: inline-block;
}
```
✅ Specificity is low and code is more readable

SCSS
```
.list__item {
  margin: 0;
  padding: 0;
  list-style: none;
}

.navbar__list {
  display: inline-block;
}
```
Compiled CSS
```
.list__item {
  margin: 0;
  padding: 0;
  list-style: none;
}
.navbar__list {
  display: inline-block;
}
```
## Avoid using IDs

🚫 High specificity that is difficult to overwrite further down in the cascade
```
#paragraphOne {  
  text-align: center;  color: red;
}
```
✅ Low specificity that is easy to overwrite
```
.paragraph-one {  
  text-align: center;  color: red;
}
```

# File Structure (in development)

scss/

├── base/

│ ├── \_reset.scss // CSS reset or normalize styles

│ ├── \_typography.scss // Global typography styles

│ ├── \_variables.scss // Variables for colors, fonts, etc.

│ ├── \_mixins.scss // Reusable mixins

│ └── \_global.scss // Other global styles

├── layout/

│ ├── \_header.scss // Header styles

│ ├── \_footer.scss // Footer styles

│ ├── \_grid.scss. // Grid and layout-related styles

│ └── \_container.scss // Container and wrappers

├── dashboard/ //This is based on the demo. This will be subject to change based on final app decisions

│ ├── \_sidenav.scss //side navigation styles

│ ├── \_topnav.scss //top navigation styles

│ ├── \_read.scss. //what the dashboard will look like

│ └── \_study.scss

│ └── translate.scss

├── components/

│ ├── \_buttons.scss // Button styles

│ ├── \_cards.scss // Card component styles

│ └── \_forms.scss // Form styles

├── pages/

│ ├── \_home.scss // Homepage-specific styles

│ ├── \_about.scss // About page-specific styles

│ └── \_contribute.scss // Contact page-specific styles

├── themes/

│ ├── \_dark.scss // Dark mode styles

│ └── \_light.scss // Light mode styles

└── main.scss // Main entry point that imports all partials
