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

### Nesting
When writing HTML you have probably noticed its clear visual heirarchy. Css on the other hand doesnt. Sass will let you nest your Css selectors in a way that follows the same visual hierachy of your HTML. Be aware that overly nested rules will result in over-qualified css that could prove hard to maintain and is considered bad practice. An example of this would be 
```scss
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li { display: inline-block; }

  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}
```
You'll notice that the `ul`, `li`, and a selectors are nested inside the nav selector. This is a great way to organize your CSS and make it more readable.

### Bem Nesting

The best thing about the ability of nesting in sass is when you use the Bem naming conventions. Bem stands for Block element modifier I will not go into detail about it here but its almost like nesting class names and example would be.
```html
<form class="form form--theme-xmas form--simple">
  <input class="form__input" type="text" />
  <input
    class="form__submit form__submit--disabled"
    type="submit" />
</form>
```
See how there is a main form class called `form` and the nested classes are all labled with `form` and two underscores then a more detailed name. This is the Bem naming convention. With Sass you can make nesting look even better when using this naming convention and example of this code block using Sass would be.

```scss
.form {
    &__input {
        color: red
    }
    &__submit {
        font-size: 16px;
    }
}
```

With including the `&` and the `__` It is an easier way to nest the Sass. 

### Partials

You can create partial Sass files that contain little snippets of CSS that you can include in other Sass files. This is a great way to modularize your CSS and help keep things easier to maintain. A partial is simply a Sass file named with a leading underscore. You might name it something like `_partial.scss`. The underscore lets Sass know that the file is only a partial file and that it should not be generated into a CSS file. Sass partials are used with the `@import` directive.

### Import
Css has an import option that lets you split your Css into smaller, more maintainable portions. The only drawback is that each time you use `@import` in Css it creates another HTTP request. Sass builds on top of the current Css `@import` but instead of requiring an HTTP request, Sass will take the file that you want to import and combine it with the file you're importing into so you can serve a single Css file to the web browser. 

Let's say you have a couple of Sass files, `_reset.scss` and `base.scss`. We want to import `_reset.scss` into `base.scss`.

```scss
// _reset.scss

html,
body,
ul,
ol {
  margin:  0;
  padding: 0;
}
```

```scss
// base.scss

@import 'reset';

body {
  font: 100% Helvetica, sans-serif;
  background-color: #efefef;
}
```

Notice the import in the `base.scss` file. When you import a file you dont need to include the file extension. So now base.scss will have all the reset available.





