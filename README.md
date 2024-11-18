**_KnowNative is in the process of migrating from CSS to SASS & BEM. Please disregard this guide until this message is removed. Thanks!!_**. November 17th, 2024, Renna Carver

Must-Know

Introduction

Hello Team! Here you’ll find a quick guide on how we do CSS for the KnowNative app. KnowNative uses SASS with SCSS syntax and BEM as the naming convention. We use BEM very loosely here. The only rule we enforce is that all class names must be prefixed by the component name. This prevents class name conflicts.

Only ONE rule

All class names must be prefixed by the component name!

👀🚫 These class names can lead to problems because title is a repeated class and pollutes the namespace

<!-- Card Component -->
<div class="card">
  <h2 class="title">Card Title</h2>
</div>

<!-- Modal Component -->
<div class="modal">
  <h2 class="title">Modal Title</h2>
</div>

✅ Much better!

<!-- Card Component -->
<div class="card">
  <h2 class="card__title">Card Title</h2>
</div>

<!-- Modal Component -->
<div class="modal">
  <h2 class="modal__title">Modal Title</h2>
</div>

\*\*the double underscore \_\_ is a BEM naming convention. Learn more about BEM below!

Using SASS to prefix all class names with the component name

While you can manually prefix all of your class names with your component name, SASS has a feature that makes it much easier. Here’s how you can use nesting and the & selector to make your code more readable:

Pre-compiled .scss file

.card {
background-color: #fff;
border: 1px solid #ddd;
&**header {
font-size: 1.5em;
padding: 10px;
}
&**body {
padding: 15px;
&--highlighted {
background-color: #f0f8ff;
}
}
&\_\_footer {
padding: 10px;
text-align: right;
}
}

Compiled .css file

.card {
background-color: #fff;
border: 1px solid #ddd;
}
.card**header {
font-size: 1.5em;
padding: 10px;
}
.card**body {
padding: 15px;
}
.card**body--highlighted {
background-color: #f0f8ff;
}
.card**footer {
padding: 10px;
text-align: right;
}

Explanation:

The & syntax in SASS refers to the parent selector, creating prefixed class names.

The \_\_ (double underscore) syntax is used for elements inside the parent selector, following BEM conventions.

The -- (double hyphen) syntax is used for modifiers such as --highlighted or --active .

This method ensures all classes within .card are properly namespaced.

Installation

SASS is likely already installed. If not, follow these steps in the terminal to bring SASS into your project:

cd client
npm install

Converting a CSS file to SASS

All the files in the project should already have the .scss extension. If not, simply rename the file from

.css

to

.scss

And you’re done! The build tool (currently Vite) will automatically watch these files and compile them to CSS in the background as you make changes.

FAQs

What’s SASS?

SASS is a pre-processor - it adds functionality not available in plain ‘ole CSS

Why do we need SASS?

CSS has a lot of modern features but browser support for these features is often missing. So while you can use advanced features like nesting, mixins, and functions, many browsers would not render this CSS correctly.

CSS pre-processors like SASS take these advanced features and compile them into vanilla CSS that can be rendered correctly by a majority of browsers.

What’s the difference between SASS and SCSS?

SASS has two different file types or syntaxes. The first is .sass and the second is .scss. Which one you use is personal preference (see the examples below) but here at KnowNative we use the SCSS syntax.

The great thing about SCSS is that you can write vanilla CSS in .scss file. This means even if you don’t know anything about SASS, you can still create a SASS file and just write plain CSS like you always have.

That being said, we hope you’ll dive into all of the extra features SASS has to offer!

SCSS Syntax - uses {} and ; (accepts vanilla CSS)

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

SASS Syntax (it’s cleaner but doesn’t accept vanilla CSS)

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

Read more at @Sass Fundamentals

What’s BEM?

BEM (Block, Element, Modifier) is a naming convention for classes in HTML and CSS that was developed by Yandex. Basically, it is a methodology to help you write better and more readable CSS code.

Why do we need BEM?

Do you often find yourself struggling with naming your CSS classes? BEM (prounounced ‘behm’) is here to help. Let’s see how. Consider this example:

HTML

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

CSS

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

This example was pulled from Kevin Powell’s excellent tutorial here: link here

Explanation:

Each of the cards is a block (parent)

The image is an element (child) of the card and is thus prefixed by the parent name card and a double underscore \_\_

Variants of a block or element are called modifiers and are prefixed by a double hyphen --

Try it yourself:

If we wanted to add a new subtitle to both cards and one card’s subtitle is red, we can name the new CSS class as

card\_\_subtitle--red

And that’s it! As mentioned above, we are not super strict with our BEM naming convention except for the ONE rule listed above. BEM is more of a guide to helping you think less when writing your CSS and keeping your code more organized. If you would like to learn more about BEM, take a look at best practices down below.

Best Practices (in development)

Flat selectors

Access all elements through classes

Avoid nesting more than two levels

Avoid id’s (specificity is too high and is hard to overwrite further down in the cascade)

Avoid tags (tags are low specificity however tags don’t have meaning. class names are preferred)

All selectors should have specificity of 10 (selected by class) so that styles can be overwritten easily further down in the cascade

(need a picture of good and bad selectors) Renna

Naming should be clear enough to not need comments

Nesting can cause problems!

Things can get very messy if you aren't careful when creating descendant selectors or using the parent selector & to create compund selectors.

A general rule of thumb is trying to stick to a maximum of 2 or 3 nesting levels deep.

Nesting can make your code harder to search, because the classes in your Sass do not match the selectors in the compiles CSS file.

File Structure (in development)

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
