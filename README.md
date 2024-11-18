Introduction

Hello Team! Here you’ll find a quick guide on how we do CSS for the KnowNative app. KnowNative uses SASS with SCSS syntax and BEM as the naming convention.

Installation

SASS is likely already installed. If not, follow these steps in the terminal to bring SASS into your project:

cd client
npm install

Converting a CSS file to SASS

All the files in the project should already have the .scss extension. If not, simply rename the file from

.css

to

.scss

And you’re done! Vite will automatically watch these files and compile them to CSS in the background as you make changes.

What’s SASS?

SASS is a pre-processor - it adds functionality not available in plain ‘ole CSS

Why do we need SASS?

CSS has a lot of modern features but browser support for these features is often missing. So while you can use advanced features like nesting and mixins and functions, many browsers would not render this CSS correctly.

CSS pre-processors like SASS take these advanced features and compile them into Vanilla CSS that can be rendered correctly by a majority of browsers.

What’s the difference between SASS and SCSS?

SASS has two different file types or syntaxes. The first is .sass and the second is .scss. Which one you use is personal preference but here at KnowNative we use the SCSS syntax.

The great thing about SCSS is that you can write vanilla CSS in .scss file. This means even if you don’t know anything about SASS, you can still create a file and just write plain CSS like you always have.

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

Show how to install SASS and migrate a file from CSS to SASS

Install SASS by running npm install sass in your terminal in the client folder (make sure to ^C first on the client server in case you were already running that).

You will be able to see the SASS package listed under dependencies in the package.json file once SASS is finished downloading.

To create your first .scss file, go into any component folder in the src folder that has a .jsx file name within and duplicate its accompanying css file and then rename the file extension to .scss.

You’ll then want to go into the accompanying .jsx folder, and at the top, import your .scss file

You’re all set! Now you can go ahead and start styling with SCSS!

SASS vs SCSS

Sass vs. CSS Comments

/_ I can still write comments like this _/

// I can write single line comments as well, but this one won't show up in the .css file!

Single-line comments (with // ) will not be compiled into your CSS file.

Read more at @Sass Fundamentals

Flat selectors

Access all elements through classes

Avoid nesting more than two levels

Avoid id’s, and tags as much as possible

All selectors should have specificity of 10 (selected by class) so that styles can be overwritten easily further down in the cascade

(need a picture of good and bad selectors) Renna

Naming should be clear enough to not need comments

SASS

All classes in a component should be prefixed by the component name (to avoid class conflicts)

Show how to use nesting and the & to prefix all classes with the component name

(need a picture showing how SASS compiles to CSS and the accompanying HTML) JP

BEM

Don’t use margins on blocks

Don’t nest blocks more than one level deep

(need a little tutorial on BEM)

To be discussed 11/21

File Structure

Using partials?

Keep Code DRY (Don’t Repeat Yourself)

Any code that is repeated should be put into a mixin for re-use
