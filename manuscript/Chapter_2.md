#Chapter 2 SCSS Basics

###Introduction to Variables in Scss

This guide examines the syntax for declaring and calling variables in Scss files.

One of the most powerful parts of using SCSS in development is the ability to make your code more efficient. If you're coming from a programming language such as Ruby or Python then the concept of having variables is a pretty common thing that you would implement into a program.

A variable is simply a container that can store a value and then can be called from anywhere else in the application. So you don't have to put identical code all through the entire app. So let's take a look at this basic example.

![](https://s3-us-west-2.amazonaws.com/bottegarails/SCSS/Screen+Shot+2017-10-18+at+10.48.14+AM.png)

So you should already have your CSS lined up and have the SCSS property set so that it compiles and it can actually process the SCSS as opposed to simply treating it like regular CSS. What we are going to be talking about here are variables.

What we want to talk about is how we can leverage variables. If we look we can see that we have some duplication here. We have the background color and whenever you see six F's in a row that's going to be the color white. We also have this dark red color. All of this is fine but imagine that you have a CSS file that is a few thousand lines long. An example of that is if you pulled in some kind of template or you're building a template and the client informs you that he would like to change all the instances of dark red to dark green. This means that you would have to search and make sure you change every instance.  Part of the logic behind using SCSS is the fact that you can implement the same type of mindset that Rails has with "Do No Repeat Yourself".

That's where variables come in. We would want to set our variables at the very top. Here we can see how we set variables in SCSS.

![](https://s3-us-west-2.amazonaws.com/bottegarails/SCSS/Screen+Shot+2017-10-18+at+12.55.34+PM.png)

Now all we have to do is use that variable to change your styles across the CSS file. Imagine our client from earlier, now if he came to us with a change to make to our color scheme. We only have to change the value of that variable and it will reflect everywhere we used that variable.   

We will go ahead and change the places that we had duplicate calls for `#ffffff` with out new variable.

![](https://s3-us-west-2.amazonaws.com/bottegarails/SCSS/Screen+Shot+2017-10-18+at+1.02.50+PM.png)

Now everything is working and we've cleaned up and remove the duplication by leveraging variables in SCSS.

Here is a demo where I use variables to manage the background color and font color for a page.

```sass
$white: #ffffff;
$master-site-color: DarkGreen;

body {
  background-color: $white;
  height: 100vh;
  height: 100vw;
}

.container {
  font-family: Verdana;
  font-size: 0.8rem;
}

.page-wrapper {
  padding: 21px;

  .featured {
    color: $master-site-color;
  }

  .page-content {
    background-color: $master-site-color;
    padding: 42px;
    color: $white;
    .container {
      font-family: courier;
    }
  }
}
```

###Using Default Variables in Scss

We've walked through how to work with variables in Scss to make it possible to make a single change that populates a number of style definitions. To take this knowledge a step further, in this guide we'll examine how to set default variable values in Scss.

We've walked through how to work with variables in Scss to make it possible to make a single change that populates a number of style definitions. To take this knowledge a step further, in this guide we'll examine how to set default variable values in Scss.

This may not seem like a big topic to learn because it's mainly important in situations where you are white labeling styles in an application. However, I think it can be a helpful skill to understand and it also is a good introduction to learning about how Scss manages variable scope.

Variable scope is the process that programming languages use to control where variables can be accessed throughout a program.

Example of Using Variables in Scss
For this example, let's imagine a scenario where you are building a set of styles that are going to be utilized on multiple websites. Services such as Wix and Squarespace have to implement this type of behavior throughout their entire systems. For our example, we want our color scheme to have a dark red set of colors for heading text and section backgrounds.

We'll implement Scss mixins and add variables with the !default flag on them. If you're not familiar with mixins, we'll dive into them later on, for right now just think of them like reusable code snippets that can be called. You can see the results below:

```sass
$off-white: #f6f6f6;

@mixin heading-feature-styling {
  $featured-color: DarkRed !default;
  color: $featured-color;
}

@mixin section-feature-styling {
  $featured-color: DarkRed !default;
  background-color: $featured-color;
  padding: 42px;
  color: #ffffff;
}

body {
  background-color: $off-white;
  height: 100vh;
  height: 100vw;
}

.page-wrapper {
  padding: 21px;

  .featured {
    @include heading-feature-styling;
  }

  .page-content {
    @include section-feature-styling;
  }
}
```

Don't worry about understanding all of the code if it looks different than you're used to. Simply focus on seeing how we're setting the default colors in each of the mixins, which results in the dark red color that we're looking for.

Making the Variables Dynamic with the !default Flag
Now, let's imagine that we have two clients come along. The first client likes the red color, so we don't have to make any changes. However, the second client wants to have a dark cyan color for their application. If we didn't use the !default flag, we'd have to go throughout the entire application and change all of the values. Additionally, if the application is dynamic we'd need to figure out a way to perform an override on the value, such as using inline styles, which can be buggy and breaks a number of best practices.

However, because we used the !default flag in our mixins, we can simply add a single line at the top of the file that will be viewed as the new 'master' color. Because the other color variables have the !default flag, Scss will ignore those variable declarations and will only use the new one that's provided.

```sass
$featured-color: DarkCyan;
$off-white: #f6f6f6;

@mixin heading-feature-styling {
  $featured-color: DarkRed !default;
  color: $featured-color;
}

@mixin section-feature-styling {
  $featured-color: DarkRed !default;
  background-color: $featured-color;
  padding: 42px;
  color: #ffffff;
}

body {
  background-color: $off-white;
  height: 100vh;
  height: 100vw;
}

.page-wrapper {
  padding: 21px;

  .featured {
    @include heading-feature-styling;
  }

  .page-content {
    @include section-feature-styling;
  }
}
```

###Guide to Variable Scope in Scss

Variable scoping in Scss is relatively intuitive if you're familiar with how variable scope works in general purpose programming languages.

If the concept of variable scoping is a little 'blurry', a dead simple explanation is:

Variable scope sets the access of variables by all of the components of a program.

For an example, if you have a variable called $master-site-color, and you want to call that color from a different part of the stylesheet, such as a paragraph tag, variable scope is the programming mechanism that allows for that paragraph tag to have access to the $master-site-color variable.

#### Basic Example of Variable Scope

In the example below you can see that I've set the $master-site-color variable at the top of the stylesheet. That is the master color and the rest of the stylesheet has access to it. However, given the cascading nature of CSS, each time we re-define the variable, the nested styles that call the variable will use the variable value that is the most closely targeted.

```sass
$master-site-color: #3AE39F;
$off-white: #f6f6f6;

body {
  background-color: $off-white;
  height: 100vh;
  height: 100vw;
}
.page-wrapper {
  $master-site-color: DodgerBlue;
  padding: 21px;

  .featured {
    color: $master-site-color;
  }

  .page-content {
    $master-site-color: LightCoral;
    background-color: $master-site-color;
    padding: 42px;
    color: #ffffff;
  }
}

.secondary-page-content {
  color: $master-site-color;
}
```

If you notice, the secondary-page-content class is the only page element that uses the variable value declared at the top of the stylesheet. This is because the other classes have more specific variable definitions.


#### Example of Scss Variable Scope with Mixins

Variable scope is the most critical when it comes to using Scss mixins. If you have a mixin that re-defines a variable, it will override any previous variable definitions, as shown in the example below:

```sass
$master-site-color: #3AE39F;
$off-white: #f6f6f6;

@mixin featured-page-content() {
  $master-site-color: LightCoral;
  background-color: $master-site-color;
  padding: 42px;
  color: #ffffff;
}

body {
  background-color: $off-white;
  height: 100vh;
  height: 100vw;
}
.page-wrapper {
  $master-site-color: DodgerBlue;
  padding: 21px;

  .featured {
    $master-site-color: DodgerBlue;
    color: $master-site-color;
  }

  .page-content {
    @include featured-page-content;
  }
}

.secondary-page-content {
  color: $master-site-color;
}
```

###Guide to Scss Nesting

One of the most popular features of Scss is the ability to nest style definitions, and that's what we're going to walk through in this guide.

In traditional CSS it's possible to say that you want to define a set of styles for one or more classes, such as with code like this:

```sass
.my-class > .etc-class {
  color: DarkRed;
}
```

However, it gets trickier when you want to implement styles for DOM elements that are nested within other elements.

For example, if you want to have two container classes on a page:

1. For the entire page
2. For spots on the page that have code snippets

You might think that you'd need to rename the container classes to have two separate classes. However, that would mean that each time you alter the styles in one container you'll have to remember to go change each of the other similar classes. There are a few ways to share the style definitions in pure CSS (remember that Scss is simply a translator into CSS), however it can be a bit complex.

Thankfully Scss offers an intuitive way to nest styles.

In the example below, we have two container classes. Notice how we have one 'master' container class definition that has a font family and font size. And then if you traverse down to inside of the page-content class I've nested another call to the container class. However, this nested container class is more specific, so the styles that are defined in it will only apply to the DOM elements that are stored inside of the container class nested inside of the page-content div.

```sass
$off-white: #f6f6f6;
$featured-color: DarkRed;

body {
  background-color: $off-white;
  height: 100vh;
  height: 100vw;
}

.container {
  font-family: Verdana;
  font-size: 0.8rem;
}

.page-wrapper {
  padding: 21px;
  $featured-color: LightCoral;

  .featured {
    color: $featured-color;
    .subheading {
      color: Red;
    }
  }

  .page-content {

    background-color: $featured-color;
    padding: 42px;
    color: $off-white;
    .container {
      font-family: courier;
    }
  }
}
```

###Scss Pseudo Selector Nesting

This guide walks through how to work with nested pseudo selectors in Scss files, specifically examining how to customize a link's hover state.

So far we've discussed how we can implement nesting in SCSS and how we can use that to be able to organize our class definitions and make sure that the styles that we're defining are the ones we actually want to implement inside of the HTML doc. So what we're going to talk about in this guide is how we can implement nesting with pseudo selectors.

Pseudo selectors give you the ability to select the style that you give an element given a different state than just the standard one. For example if we decide to make a subheading into a link, By using an `<a>` tag that will create the link.

And so this text is going to be nested inside of this link. And as you can see right here we have my subheading.

![](https://s3-us-west-2.amazonaws.com/bottegarails/SCSS/Screen+Shot+2017-10-18+at+1.17.04+PM.png)

Now this is pretty ugly. This is the standard HTML blue with the underline and it's exactly what you would get just out of the box with HTML. So let's work on that. The first thing we're going to do is change the subheading color. And the reason why this color is not working anymore, because you can see subheading is still nested inside of feature. We didn't change that part. But what's different now is we created an `<a>` tag. So now there's another element that's actually inside of our subheading.

So whenever we style links we actually have to define the way we're styling them and we have to tell SCSS that we're going to define the style for a link. So now if I add in an `a` right here right after subheading you can see that the color has now changed to red.

![](https://s3-us-west-2.amazonaws.com/bottegarails/SCSS/Screen+Shot+2017-10-18+at+1.20.05+PM.png)

I'm going to update this again and we're going to change it to cornflower blue. I have no idea how they came up with some of the names that they have. The HTML full set of color guides has some very interesting names and I like to play with these. So here we have cornflower blue. Now if I hover over you can see nothing changes. So first and foremost I want to take away the underline. So the way I can do that is by saying text-decoration and say none here and now you can see that the underlining disappears.

![](https://s3-us-west-2.amazonaws.com/bottegarails/SCSS/Screen+Shot+2017-10-18+at+1.22.41+PM.png)

Right now there's nothing happening but when I hover, I want to change the color and then I also want to add the underlining back in. So the way that you can do that is to perform another set of nesting. The way that you use a pseudo selector is by starting with an ampersand followed by a colon and then say hover and then inside of that you give your different style definition.

![](https://s3-us-west-2.amazonaws.com/bottegarails/SCSS/Screen+Shot+2017-10-18+at+1.26.38+PM.png)

If you hover over the link now, we can see that the changes have taken place.

Now this is one that it may look kind of weird right now. One of the main reasons I wanted to put it in the course one is because it's important and helpful to use but also as you're going through other people's SCSS files if you come across something that looks like this that may look a little bit weird. If you've never seen it before so I'd definitely recommend trying this out on a few different projects that you're working on.

#### HTML Code from Guide

```html
<div class="container">
  <div class="page-wrapper">
    <div class="featured">
      <h1>About us</h1>

      <div class="subheading">
        <h4>
          <a href="#">My subheading</a>
        </h4>
      </div>
    </div>

    <div class="page-content">
      <div class="container">
        <p>Cras mattis consectetur purus sit amet fermentum. Aenean eu leo quam. Pellentesque ornare sem lacinia quam venenatis vestibulum. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor.</p>
      </div>
    </div>
  </div>
</div>
```


#### Scss Code Example of Pseudo Selector Nesting

```sass
$off-white: #f6f6f6;
$featured-color: DarkRed;

body {
  background-color: $off-white;
  height: 100vh;
  height: 100vw;
}

.container {
  font-family: Verdana;
  font-size: 0.8rem;
}

.page-wrapper {
  padding: 21px;
  $featured-color: LightCoral;

  .featured {
    color: $featured-color;
    .subheading a {
      color: CornflowerBlue;
      text-decoration: none;
      &:hover {
        color: DarkOliveGreen;
        text-decoration: underline;
      }
    }
  }

  .page-content {

    background-color: $featured-color;
    padding: 42px;
    color: $off-white;
    .container {
      font-family: courier;
    }
  }
}
```
