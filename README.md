# SassTest

This is learn SASS crash course note.

[the original web here](https://sass-lang.com/guide).



# Install

### Install Anywhere (npm)

If you use Node.js, you can also install SASS using [npm] by running

    npm install -g sass


D:mytest> npm install -g sass

mytest: your project name


**However, please note** that this will install the pure JavaScript implementation of Sass, which runs somewhat slower than the other options listed here. But it has the same interface, so it'll be easy to swap in another implementation later if you need a bit more speed!

[npm]:https://www.npmjs.com/

### Install Anywhere (Standalone)

You can install Sass on Windows, Mac, or Linux by downloading the package for your operating system from [GitHub] and adding it to your [PATH]. 

That's all—there are no external dependencies and nothing else you need to install.

[GitHub]:https://github.com/sass/dart-sass/releases/tag/1.17.2
[PATH]:https://katiek2.github.io/path-doc/


[more infomation here](https://sass-lang.com/install)

# Sass build Command

When you write done your Sass/Scss file everytime, you need to build it by CSS preprocessor to pure CSS file.

That mean you need to build the  new file to update / override it.

They are two commands to use.

**Way one (manually)**

Type it in your CMD .

    sass source/index.scss output/index.css

**Way two (automatically)**
You can use `watch` to watch file. when the file have changes, the file will auto build it.

Type it in your CMD

    sass --watch input.scss output.css

**Way three (automatically files)**
You can use `watch` all files. when any file have changes, the file will auto build it.

Type it in your CMD

    sass --watch app/sass:public/stylesheets

Sass would watch all files in the app/sass folder for changes, and compile CSS to the public/stylesheets folder.


# CSS Preprocessors

A CSS preprocessor is a program that lets you generate CSS from the preprocessors own unique syntax.

There are many CSS preporcessors to choose from however most CSS preporcessors will add some features

That donts exist in pure CSS such as [variable] , [mixin], [nesting selector], [inheritance selector], and so on. 

[variable]:https://github.com/ootuskaai/SassTest/blob/master/README.md#variables
[mixin]:https://github.com/ootuskaai/SassTest/blob/master/README.md#variables
[nesting selector]:https://github.com/ootuskaai/SassTest/blob/master/README.md#variables
[inheritance selector]:https://github.com/ootuskaai/SassTest/blob/master/README.md#variables

# Variables

Sass uses the $ symbol to make something a variable.

You can store things like colors, font stacks, or any CSS value you think you'll want to reuse.

```scss
$font-size: 50px;
$primary-color: #333;

body {
  font: $font-size;
  color: $primary-color;
}
```

Variables are only available within the level of nested selectors where they're defined. 

If they're defined outside of any nested selectors, they're available everywhere.

This is local variable in h1 tag.

```scss
h1 {
  $testVariableColor: #333;
  color: $testVariableColor;
}
```

This is global variable.

```scss
$testVariableColor: #333;

h1 { 
  color: $testVariableColor;
}

h2 {
  color: $testVariableColor;
}
```

They can also be defined with the `!global` flag, in which case they're also available everywhere.
 
 ```scss
 #main {
  $midWidth: 5em !global;
  width: $midWidth;
}

#sidebar {
  width: $midWidth;
}
 ```
 
 
 # Nesting 
 
 Sass will let you nest your CSS selectors in a way that follows the same visual hierarchy of your HTML.
 
 You'll notice that the .redbox selectors are nested inside the #main p selector. 
 
 This is a great way to organize your CSS and make it more readable.
 
 ```scss
#main p {
  color: #00ff00;
  width: 97%;

  .redbox {
    background-color: #ff0000;
    color: #000000;
  }
}
 ```
 
 is compiled to:
 
 ```scss
  #main p {
   color: #00ff00;
   width: 97%; 
  }
  #main p .redbox {
    background-color: #ff0000;
    color: #000000; 
  }
 ```
 
 
 # Partials
 
 You can create partial Sass files that contain little snippets of CSS that you can include in other Sass files. 
 
 This is a great way to modularize your CSS and help keep things easier to maintain. 
 
 A partial is simply a Sass file named with a leading underscore. 
 
 You might name it something like _partial.scss. 
 
 The underscore lets Sass know that the file is only a partial file and that it should not be generated into a CSS file. 
 
 Sass partials are used with the **@import directive**.
 
 Normally we will partial Sass to following parts 
 
 **style.scss variable.scss  mixin.scss  reset.scss**
 
 `style.scss` this file is main scss file
 
 `variable.scss` this file is save global variable file
 
 `mixin.scss` this file is save mixin file
 
 `reset.scss` this file is save reset CSSs file
 
 
 
 # Import
 
 Sass will take the file that you want to import and combine it with the file 

 You're importing into so you can serve a single CSS file to the web browser.
 
 Sass supports all CSS3 **@-rules**, as well as some additional Sass-specific ones known as **directives**.
 
 These have various effects in Sass.

 reset.scss
 ```scss
 html,
 body,
 ul,
 ol {
   margin:  0;
   padding: 0;
 }
 ```
 
 variable.scss
 ```scss
 $titleFontSize: 30px;
 $titleBgColor: #333;
 ```
 
 mixin.scss
 ```scss
 @mixin banner {
    width: 100%;
    position: relative;
    color: white;
    
    .banner-content {
        position: absolute;
        top: 50px;
        width: 100%;
       }
 }
 
 ```
 
 style.scss
 ```scss
 @import "reset";
 @import "variable";
 @import "mixin";
 
 .lessons-banner{
  @include banner;
  text-align: right;

  ul{
    float: left;
    text-align: left;
  }

  li{
    text-transform: uppercase;
    font-size: titleFontSize;
    max-width: 650px;
    margin: 60px 0;
    font-weight: bold;
    background-color: titleBgColor;
  }
}
 
 ```
 Let's say you have a couple of Sass files, reset.scss, style.scss, variable.scss, mixin.scss. 
 We want to import their into style.scss.
 
 # Mixin 
 
 Mixins allow you to define styles that can be re-used throughout the stylesheet 
 
 without needing to resort to non-semantic classes like .float-left. 
 
 Mixins can also contain full CSS rules, and anything else allowed elsewhere in a Sass document. 
 
 They can even take arguments which  allows you to produce a wide variety of styles with very few mixins.
 
 
 ### Defining a Mixin: @mixin
 
 Mixins are defined with the @mixin directive. 
 
 It's followed by the name of the mixin and optionally the arguments, and a block containing the contents of the mixin. 
 
 For example, the large-text mixin is defined as follows:
 
 ```scss
 @mixin large-text {
  font: {
    family: Arial;
    size: 20px;
    weight: bold;
  }
  color: #ff0000;
}
 ```
 
 Mixins may also contain selectors, possibly mixed with properties. 
 
 The selectors can even contain [parent references](). 
 
 For example:
 
 ```scss
 @mixin clearfix {
  display: inline-block;
  &:after {
    content: ".";
    display: block;
    height: 0;
    clear: both;
    visibility: hidden;
  }
  * html & { height: 1px }
}
 ```
For historical reasons, mixin names (and all other Sass identifiers) can use hyphens and underscores interchangeably. 

For example, if you define a mixin called **add-column**, you can include it as **add_column, and vice versa**.

### Including a Mixin: @include

Mixins are included in the document with the @include directive. 

This takes the name of a mixin and optionally arguments to pass to it, 

and includes the styles defined by that mixin into the current rule.

```scss
.page-title {
  @include large-text;
  padding: 4px;
  margin-top: 10px;
}
```
is compiled to:

```scss
.page-title {
  font-family: Arial;
  font-size: 20px;
  font-weight: bold;
  color: #ff0000;
  padding: 4px;
  margin-top: 10px; 
 }
```

### Mixin Arguments 

Mixins can take SassScript values as arguments, 

which are given when the mixin is included and made available within the mixin as variables.

When defining a mixin, the arguments are written as variable names separated by commas, 

all in parentheses after the name. Then when including the mixin, values can be passed in in the same manner.

```scss
@mixin sexy-border($color, $width) {
  border: {
    color: $color;
    width: $width;
    style: dashed;
  }
}

p { @include sexy-border(blue, 1in); }
```
is compiled to:
```scss
p {
   border-color: blue;
   border-width: 1in;
   border-style: dashed; 
 }
```

**Default values**

Mixins can also specify default values for their arguments using the normal variable-setting syntax. 

Then when the mixin is included, if it doesn't pass in that argument, the default value will be used instead.

```scss
@mixin sexy-border($color, $width: 1in) {
  border: {
    color: $color;
    width: $width;
    style: dashed;
  }
}
p { @include sexy-border(blue); }
h1 { @include sexy-border(blue, 2in); }
```
is compiled to :
```scss
p {
  border-color: blue;
  border-width: 1in;
  border-style: dashed; 
}

h1 {
  border-color: blue;
  border-width: 2in;
  border-style: dashed; 
}
```

**Variable Arguments**

Sometimes it makes sense for a mixin or function to take an unknown number of arguments. 

For example, a mixin for creating box shadows might take any number of shadows as arguments.

For these situations, Sass supports **variable arguments**,

which are arguments at the end of a mixin or function declaration 

that take all leftover arguments and package them up as a list. 

These arguments look just like normal arguments, but are followed by .... For example:

```scss
@mixin box-shadow($shadows...) {
  -moz-box-shadow: $shadows;
  -webkit-box-shadow: $shadows;
  box-shadow: $shadows;
}

.shadows {
  @include box-shadow(0px 4px 5px #666, 2px 6px 10px #999);
}
```
is compiled to :
```scss
.shadows {
  -moz-box-shadow: 0px 4px 5px #666, 2px 6px 10px #999;
  -webkit-box-shadow: 0px 4px 5px #666, 2px 6px 10px #999;
  box-shadow: 0px 4px 5px #666, 2px 6px 10px #999;
}
```
