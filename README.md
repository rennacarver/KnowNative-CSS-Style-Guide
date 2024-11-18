**_KnowNative is in the process of migrating from CSS to SASS & BEM. Please disregard this guide until this message is removed. Thanks!!_**. November 17th, 2024, Renna Carver

Introduction

Hello Team! Here you’ll find a quick guide on how we do CSS for the KnowNative app. KnowNative uses SASS with SCSS syntax and BEM as the naming convention. We use BEM very loosely here. The only rule we enforce is that all class names must be prefixed by the component name. This prevents class name conflicts.

Only one rule: All class names must be prefixed by the component name

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
