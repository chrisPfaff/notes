# Sass

Sass is just a type of style sheet language that was designed to allow for different concepts than Css. It still needs to be preprocessed so that it can be interpredted or compiled into css. Sass lets you use features that dont exsist in css like mixins, variables, nesting and inheritance.

### Preprocessing

Sass needs to be preprocessed in order for it to be compiled into readable css. The most direct way is to use your terminal. You can use the `sass` command to tell which file to buld from and where to output the css to. For example running `sass input.scss output.css` would take input.scss and compile it to a file called output.css.
You can also watch certain files with the `--watch` flag. This will all for file changes and automatic re compiling on your css file. An example command for this would be `sass --watch input.scss output.css` You can also watch whole directories if you have multiple sass files  like this
`sass --watch app/sass:public/stylesheets` this will watch all files in the `app/sass` folder and compile to `public/stylesheets` folder

### Variables

Variables like in Js or any other programming language are a way to store information. In Sass you can store things like colors, font stacks and themes. Sass uses the `$` symbol to make something a variable.

```scss 
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
    font: $font-stack;
    color: $primary-color;
}
```

When the Sass is processed, it takes the variables we define for the `$font-stack` and `$primary-color` and outputs normal CSS with our variable values placed in the CSS. This can be extremely powerful when working with brand colors and keeping them consistent throughout the site.

