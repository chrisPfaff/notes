# css 

##### types of selectors

* universal selector ```css * { } ```
* type selector ```css h1, h2 { } ```
* class selector ```css .anyclass { } ```
* id selector ```css #anyid { } ```
* child selector ```css li>a { } ``` Matches an element that is a direct child
* decsendent selector ```css p a { } ``` Matches an element that is descendent not just specific child
* adjacent selector ```css li+p { } ``` Matches an element tjay is nexy sibling of another
* general sibling selector ```css h1~p { } ``` Matches the element that is a sibling of another although it does not have to be the directly preceding element

##### cascading style sheets

If you specify the font family of color properties on the body element this will apply to most child elements. The reason for this is because css always apply a parent elements style unless specifically told not to. An example would be

```css
    body {
        color: red;
    }
    .div {
        color: gray;
    }
```

In this instance the text color of what ever is inside the body would be red except for that class with the name div, the text in that element would be gray.

##### color

The color property allows you to specify the color of the text in the element

```css
* {
     color: red;
}
```

This would make all text color red on the webpage.
You can use different values to change the color as well not just the name of the color.

rgb values
```css
* {
     color: rgb(100, 100, 90);
}
```
Hex codes
```css
* {
     color: #999fff;
}
```
Rgb specifies how much Red Green and Blue you want in the color and hex codes are a six digit code that represents the amount of red green and blue as well it is prefaced by a hash.

##### background color

Since css treats each HTML element as if it appears in a box the background-color property sets the color of the background for that box, if you do not specify a background color the background is transparent. Background color can use the same color values as before being Hex codes, name and Rgb.

```css
* {
    background-color: #ffffff
}
```

##### css filter property
The filter property defines visual effects usually for images but can also be applied to text.  The css below would blur the "p" element by 1px.
```css
p {
     filter: blur(1px, em, rem);
}
```
 Other filter properies along with their values are.
* brightness(%)
* contrast(%)
* filter:drop-shadow(8px 8px 10px gray);
* grayscale(%)
* hue-rotate(deg)
* invert(%)
* opacity(%)
* saturate(%)
* sepia(%)
* url()	looks for a url for a svg filter

##### Text

Text and font styles are very important when it comes to css. They can affect the readability and look of your page dramatically. If you wanted to change the font of some text you would use the font-family property. In this case selecting more than one font would protext you against a user not having a specific font, it would fallback to next font.
```css
    p {
        font-family: Georgia, Times, serif
    }
```

There are also other ways to include multiple fonts on your page. [Google Fonts is a great resource](https://fonts.google.com/). You can either include the stylesheet as a <link>  in your HTML page or @import the font directly into your css file. Once included you just have to specify the font-family as the new font you would like.

Other font properties with what they do are
* font-size: px, em, rem (see note below)
* @font-face { font-family: ( file on computer )} // This allows you to download a font and use it locally but have it accessible on someone elses computer as well
* font-weight: normal, bold // Changes the boldness of a font
* font-style: italic, normal, oblique
* text-transform: uppercase, lowercase, capitalize
* text-decoration: none, underline, overline, line-through, blank
* line-height: px, em, rem
* letter-spacing: px, em, rem
* word-spacing: px, em, rem
* text-align: left, right, center, jutisfy
* vertical-align: text-top, baseline, text-bottom (mostly used with text along images)
* text-indent: px em rem (indent first line of text)
* text-shadow: px px px color (creates a shadow for text)

## Note: Px, Em, Rem

When to use what attribute when sizing. Ems and Rems are relative units meaning when you set a font size to 2em or 2rem it will be two times the relative size of the parents size the difference being that with rem its always the root parent element and ems will go up the tree until it finds another attribute that is the same attribute in a parent element. example if you had a p element with a font size of 2em it would search for a parent element that had a fontsize set and be twice the size of that. An example of Ems use case is if you have a page with a header and a subheader with some text and a footer which will all have different fontsizes and if you ever want to scale up the entire page you have to set the font size on the entire page and then use different em font sizes on each element. As long as they are not nested these elements will find the parent font size and be relative to that and not each other. A trick you can use is to manual set the font size on your html to 10px then everything is base ten and can be calculated out with rems from there. You can also set the font-size to 62.5 % and it also does something along the same lines of setting the base html elements font-size to 10px.


##### psudo selectors
