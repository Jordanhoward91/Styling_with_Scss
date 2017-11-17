#Chapter 3 Scss Mixins

###Creating Your First Mixin

This lesson examines how you can build a basic Mixin that can be called from anywhere in the application's Scss files.

I've updated the starter code that we have here and as you can see we now have a few different components.

#### HTML Code

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
        <div class="description">
          <p>
            Cras mattis consectetur purus sit amet fermentum. Aenean eu leo quam. Pellentesque ornare sem lacinia quam venenatis vestibulum. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor.
          </p>          
        </div>

        <div class="sidebar">
          <h1>About us</h1>

          <div class="subheading">
            <h4>
              <a href="#">My subheading</a>
            </h4>
          </div>
        </div>

      </div>
    </div>
  </div>
</div>
```

#### Scss Starter Code

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
  $featured-color: RoyalBlue;

  .featured {
    color: Tomato;
    .subheading a {
      color: LightSteelBlue;
      text-decoration: none;
      &:hover {
        color: LightSkyBlue;
        text-decoration: underline;
      }
    }
  }

  .page-content {
    background-color: $featured-color;
    padding: 42px;
    color: $off-white;

    .container {
      height: 60px !important;
      font-family: courier;

      .description {
        float: left;
        width: 75%;
      }

      .sidebar {
        font-family: Verdana;
        text-align: right;
        float: right;
        width: 25%;
        color: Tomato;
        .subheading a {
          color: LightSteelBlue;
          text-decoration: none;
          &:hover {
            color: LightSkyBlue;
            text-decoration: underline;
          }
        }
      }
    }
  }
}
```

If you look on the HTML side I've added a description, also I've added a sidebar div and class. And as you may have noticed it is literally identical to what we have right here. So something that you'll come across quite a bit as you're developing applications, is when you have identical styles or very very close to the same style that needs to be placed throughout an entire application and that is where we get into how we can leverage mixins.


 We've talked about how variables are excellent at helping in cleaning up duplication but variables can only go so far when you need to be able to store a large amount of items or when you need to have dynamic behavior. That is where mixins really start to show how helpful they are. It's a huge reason why SCSS has become so popular through the years, because it lets you wrap up functionality that you use quite a bit and call it from anywhere in the application. If you're used to working with methods or functions in a programming language you can think about SCSS mixins very much in the same way.



So let's look at the code we have here. So we have a two components are completely identical and one is in the sidebar. The other is there in the featured section. If you come inside of the nested feature class you can see we have a color of tomato and a nested subheading link with its own respective hover state. Now if you come down all the way down to the bottom you can see we have a sidebar class and inside of the sidebar class we're calling things such as the font family, text align right float and all of these kinds of components. So what we have here is identical but we do have a few things that we've added on. So this is going to show how mixins can be called. So what we're going to do is come into the featured section and I'm going to cut all of it out. And as you can see this will change just to the basic defaults. At the very top of the file we are going to create a mixin and I'm going to call it featured and just leave it at that. And inside a curly braces I'm going to paste in all of those styles.

![](https://s3-us-west-2.amazonaws.com/bottegarails/SCSS/Screen+Shot+2017-10-19+at+10.29.11+AM.png)

Now in order to code this all I have to do is call it like this.

![](https://s3-us-west-2.amazonaws.com/bottegarails/SCSS/Screen+Shot+2017-10-19+at+10.31.05+AM.png)

So now we can make changes in our mixin and they are reflected where ever we have used them. Let's see how we can do the same thing down below for our Sidebar. So even though our Sidebar has a few items that are different and unique we can still just call these mixins and the system will do the remainder of the work for us.

![](https://s3-us-west-2.amazonaws.com/bottegarails/SCSS/Screen+Shot+2017-10-19+at+1.27.47+PM.png)


I personally like to think about mixins like a method where they can be called from anywhere in the application. I also liken them to very powerful variables, kind of like the way where we made a change to just one value of a variable at the very beginning and it populated to the rest of the application. Same thing with mixins. Now this is just one part of mix ins and this is very helpful to create reusable code components that can be called from anywhere else in any other SCSS file and you can just reuse those without having to copy and paste a full set of style definitions.


#### Code with Mixins

```sass
$off-white: #f6f6f6;
$featured-color: DarkRed;

@mixin featured {
  color: Tomato;
  .subheading a {
    color: LightSteelBlue;
    text-decoration: none;
    &:hover {
      color: LightSkyBlue;
      text-decoration: underline;
    }
  }
}

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
  $featured-color: RoyalBlue;

  .featured {
    @include featured;
  }

  .page-content {
    background-color: $featured-color;
    padding: 42px;
    color: $off-white;

    .container {
      height: 60px !important;
      font-family: courier;

      .description {
        float: left;
        width: 75%;
      }

      .sidebar {
        font-family: Verdana;
        text-align: right;
        float: right;
        width: 25%;
        @include featured;
      }
    }
  }
}
```

###Working with Scss Conditionals

This lesson walks through how to implement conditionals in Scss to dynamically change how styles are rendered on the screen.

In the last guide, we walk through how to pass arguments into mixins And that's incredibly powerful. In this guide, we're going to extend that knowledge and we're going to talk about conditionals. You know if you're coming from a general purpose programming language like Ruby or javascript then the concept of conditionals may be relatively familiar to you. It gives you the ability to have a situation where you can ask if something happens then I want you to perform one set of actions if something else happens though I want you to change your behavior and do something different. And Scss allows us to have that same type of flexibility and the same type of power. Right. In the system. This is a very powerful way of being able to dynamically change how mixins behave.

Now I've taken the code that I put in last time out for the most part. And as you can see right here I've just hardcoded the link colors in and I'm going to leave those there for right now because I don't want to be distracted on what I want to show which is how to change these heading colors and to make them dynamic, based on the background color that they're on. This is something that is a very common practice where you run into a situation where you have a certain number of styles and say 90 percent of them will work for many different situations and so you want to be able to share those styles. But there are a few things that need to change.

So great example is let's say we have this featured mix in here we want just about all of these things to be the same. The only thing that we want to be different is we want this color and obviously we have a few other items that can be different but for the sake of this example we want it to be just the color that we don't want to pass in the color the way we did in the last guide because there may be times where we simply do not want to make something that arbitrary. Especially say that you're building some type of code library that other people are going to use. If you just allow them to pass any color and it might break the style guide and there might be some issues. Instead what you can do is you can pass in some other types of values or you can require some other values to be passed in.

So what we're going to do here is I'm going to add a new argument here and it's going to be called it's going to be called `$bg-color: 'dark'` and I'm going to pass it in so it has dark as a default to remember from the last guide. This is the syntax for setting a default value for an argument in Scss. And now the syntax for just a basic conditional is sane. If with an ant symbol in front of it. Now if you're coming from another language that may look weird but this is a way that the preprocessor with Scss works. So we're going to say if $bg-color is equal to dark and remember to do two equal signs then I want to change this color so I want to change the color of this tomato right here. This is going to give us exactly the same behavior. Now, why is this giving us this behavior as a quick review of how the arguments into arguments work. We scroll down right now. We're not calling or passing any arguments into this featured mixin call either here or here. And because of that with the way to fall arguments work that doesn't mean it's always going to be dark. Now if we say that if the background color is light then right then it's going to just default to whatever the value is. So right now this one changes to light and this one changes to dark and that is just because of how the other types of settings are there.

So we have a subheading with a and we have some other elements on the rest of the page. So inside of the container right here we have our color of being off-white in this page content wrapper. So that's a reason why this about us is in white. So we definitely do not want that to happen. So what we need to do is make sure we catch each one of the scenarios. So I say if the background color is light then I want to do tomato coming down to a featured call right here I'm going to pass in light. And so this one is now going to be tomato. You see how that works it just changed right there because we passed in an argument that matched exactly with what our conditional said.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/HTML+CSS+images/scss/image1.png)

Now here for featured. I'm going to pass it and say this one has a dark background and it goes back to whatever the default is. And coming up what we can do is there's a number of ways we can implement it conditional. I'm going to show you one way of doing it. And that is if we want to just capture certain cases so say that we want to say OK if the background color is a light then I want to be tomato. If it's dark then I just want it to be white just like this or I guess to make it a little bit easier we could go with because this was already the default. We could just. So you can see that it is changing. We could go with one of our blues or something like that. This is not a good UI UX this is more just to show you how to change these colors. So that's one way of doing it. And that's fine for certain circumstances. And in fact when we go into our more advanced project and we build out an entire module entire mix in module just for flex box then I am going to do this because I like to in certain cases organize each one of my scenarios into its own conditional. That's one way. But there's also an alternative syntax for more straightforward conditionals and that is by using ELSE IF

##ELSE IF

So here what I can do is actually bring this up top and say else if and it's two words say. Else if the background color is dark then I want you to change the color to blue. And as you can see everything here remained exactly the same. So we can combine both the conditionals into one.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/HTML+CSS+images/scss/image2.png)

Now let's do one more because this is fine but what happens if somebody passes in a completely different color as the background. Well we can set up a another default. We have a full set up here but we could also set up another one that says any other scenario we can pass in. And so here we can change it to red or something like that. And now if I come all the way down to the bottom if someone calls this mix in and they call it and say oh it has a blue background you can see it goes to that final conditional it goes to that final else. This is a smart way of building your system because you don't want to run into a situation where you haven't captured all of the different scenarios that could occur.

So we've we have ourselves covered in two ways. One we make it possible to call this feature mix and without any arguments and we set up just a regular default. This would be a scenario where you know in a very large percentage of the situations where this mix is going to be called it's going to be on a dark background so it's perfectly fine to set this up as the default value. But you also want to make sure that somebody who maybe they have a typo maybe they have some type of issue with how they call it. You want to make sure that you have some shrewd defaults so if they call anything besides this dark if they call different than light or dark then we're still capturing that and everything still is working properly. So this is how you implement a just a regular conditional along with a compound conditional inside of Scss.


## Scss Source Code for Conditionals

```sass
$off-white: #f6f6f6;
$featured-color: DarkRed;

@mixin featured($bg-color: 'dark') {
  @if $bg-color == 'light' {
    color: Tomato;  
  } @else if $bg-color == 'dark' {
    color: blue;  
  } @else {
    color: red;
  }

  .subheading a {
    color: black;
    text-decoration: none;
    &:hover {
      color: black;
      text-decoration: underline;
    }
  }
}

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
  $featured-color: RoyalBlue;

  .featured {
    @include featured('light');
  }

  .page-content {
    background-color: $featured-color;
    padding: 42px;
    color: $off-white;

    .container {
      height: 60px !important;
      font-family: courier;

      .description {
        float: left;
        width: 75%;
      }

      .sidebar {
        font-family: Verdana;
        text-align: right;
        float: right;
        width: 25%;
        @include featured('blue');
      }
    }
  }
}
```

###Project: Build a Flexbox Mixin with Scss

This lesson walks through the steps needed in order to build the Scss Mixin project.

I'm excited about this guide because in this guide I'm going to walk through some of the real power that you can get out of sass mix ins and how you can combine really a lot of the things that we've been learning throughout this course into one guide. And so what we're going to do is we're going to build a flexbox mix then.

Now if you've never heard of flexbox before that is perfectly fine. It will also be a nice introduction for you on how flexbox works. It's a very powerful way of writing your CSS code for doing things such as aligning items. If you've ever struggled with getting a title or something to line up in a central alinement or anything like that some things that seem like they'd be easy but can be surprisingly challenging. Fluxbox is a great option for modern front-end development. However, this is this guy is not about flex Xbox it's actually about something that I don't like about flexbox and so I decided to build a mix and in order to fix it.

![picture](https://s3-us-west-2.amazonaws.com/devcamp-pictures/HTML+CSS+images/scss/image3.png)

So this is a prototype and a component I was building for dev camp and what is here is a set of cards and these cards have a title a subtitle they have an image and then they have some action item links. Now they look a lot better on dev camp. This was just a prototype before the designer got it and it has more to learn how flexbox could be used to do things like align these buttons here and to put an image here. If you try doing this just purely in CSS this would be a very challenging task so I utilize flexbox in order to do that. Now let's look at the CSS as we have here a display of flex for the entire container and I'm going to give you access to the HTML and the CSS so that you can see all of it first how it started. And then also how we're going to factor it. So we have this container and every time that you want something to utilize flexbox you have to say display flex so you can see that we have it here. Then we have this item class. We also have it here then we have this content item. We have it here, metadata. We have it here, button group. You kind of get the point. It is everywhere.

So each one of these elements and some of them are nested some of some of them are outside but all of them are in this container class. They have some form of a flexbox component whether it's one or whether it's four or five. And we need the ability to simply remove all that duplication and simply call a single mixin. You know everything that you need to know in order to do this I'm going to let you know the different components that we're going to be utilizing. So we're going to use the flex item, we're going to be using the display flex element here, we will use justify content we're going to use flex direction, and we have aligned items, that is it.

So each one of those items we are going to take and we're going to build into a mix and but as you may have noticed each component is a little bit different. They each need a different set of these values. So everything that you've learned so far whether it is just a standard mix in arguments default values conditionals all of those things are what you need in order to build this project. So you have access to the starter code here. But the well and the Scss while and I want you to go and take all of the Flexbox content out so each one of those items and put it into a mix and so that you only call a single mix and every spot that has flex box go through that do it. And then you can watch how I personally did it in the solution.



The flexbox elements needed for the project are:

- display: flex
- justify-content
- flex
- flex-direction
- align-items

## Project Starter HTML Code:

```html
<div class='container'>
  <div class='item'>
    <div class='content'>
      <img
        src='https://d32xj74kbqkoqn.cloudfront.net/uploads/campsite/campsite_image/129/dissecting-rails-icon.jpg'
        width='200px'
        height='120px'
      >
      <div class='metadata'>
        <h1 class='title'>My amazing title</h1>
        <h3>And a subtitle</h3>
      </div>
    </div>
    <div class='btn-group'>
      <div class='button'>
        <a href="#">+</a>
      </div>
      <div class='button'>
        <a href="#">x</a>
      </div>
    </div>
  </div>
  <div class='item'>
    <div class='content'>
      <img
        src='https://d32xj74kbqkoqn.cloudfront.net/uploads/guide/video_image/43/foundations-video-thumb.jpg'
        width='200px'
        height='120px'
      >
      <div class='metadata'>
        <h1 class='title'>Another amazing post</h1>
      </div>
    </div>
    <div class='btn-group'>
      <div class='button'>
        <a href="#">+</a>
      </div>
      <div class='button'>
        <a href="#">x</a>
      </div>
    </div>
  </div>
</div>
```

## Project Starter Scss Code

```sass
.container {
  display: flex;
  .item {
    flex: 1;
    display: flex;
    justify-content: space-between;
    border: 1px solid grey;
    border-radius: 5px;
    margin-bottom: 10px;
    .content {
      display: flex;
      .metadata {
        display: flex;
        flex-direction: column;
        justify-content: center;
        margin-left: 20px;
        .title {
          margin: 0px;
        }
      }
    }
    .btn-group {
      display: flex;
      align-items: flex-end;
      align-items: center;
      .button {
        height: 100%;
        display: flex;
        align-items: center;
        flex-direction: row;
        width: 42px;
        justify-content: center;
        font-size: 2em;
        a {
          color: green;
          text-decoration: none;
        }
        &:hover {
          background-color: maroon;
          cursor: pointer;
          a {
           color: white;
          }
        }
      }
    }
  }
}
```

###Project Solution: Build a Flexbox Mixin with Scss

This solution guide examines how to build the Flexbox Scss Mixin by incorporating: conditionals, mixins, variables, default mixin arguments and named arguments.

Hopefully, that project went well for you. Let us walk through what my solution was and also talk about the process that I used when I was building it out. So the very first thing I did is I came up and I just created a new mix in. I called it mix in Flex config and then I'm going to pass some arguments and I'm not going worry about them at this moment. I'm just going to make some space for it just like that. And then I came and I just added some comments just so that I could keep track of everything.

So I knew that I needed display flex. So I know that's going to have to be there and let me just come down and I'm going to do some other comments. This ID has a few different keyboard shortcuts and I'm used to using. So just display flex and then I know that I need justify content. And then after justify content, I knew I needed flex After that I needed flex direction. And then lastly I know I needed align items. So with these in place now I can organize my code.

Now the one thing I do know if you look at all of this code and you don't need any flex box kind of skill in order to know this is not a prerequisite at all. If you look at each item whenever we call display flex or any of the five items that we need to contain You may notice display flex is in all of them. So what that tells me is we don't need to take display flex as an option. It is always needed. So the nice thing about that, that means that our first one is taken care of for us. So I can just say display flex and that one's done. So any time that we call this flex config then it's going to be set.

Now the other thing I know that I need is each one of these other ones is optional. So I'm going to set these as different variables so up here they're going to be their own set of arguments. So just very content then it's going to be $ flex then we're going to have $ flex direction. And lastly we're going to have $ align items now as a review just remember these are our arguments now because of the way that these work. It's very important that we do one new thing here. We should say it would make life a lot easier on us later on. If I leave these just like this then I'm going to have to always have this order memorized and I just know myself and I'm not very good at memorizing that kind of stuff so I'm not going to do that. I'm going to use what are called named arguments. Technically you could have got the whole thing working without named arguments because they're not something that we specifically went over yet. But you'll see it's actually the exact same syntax as using defaults.

So the way this is going to work is I want to set up each one of these defaults to be false. So every one of these is going to be false by default. What that's going to allow me to do is now whenever I check and whenever I set up my conditionals I'm going to be able to check to see if the element is true or false or I should say if it's false if it is not false that tells me that it has some type of value and I need to set that value if it is false. So if it's taking in the default It means that when I called that it meant that it wasn't ever set and if that is about as clear as mud don't worry we're going to go through in detail.

So let's set up some pretty basic conditionals. I'm going to set up my first one. It's going to say if justify content is not equal to false. So in other words, if it is set. So by default it's going to be false so if when I call this like we're going to call this very first one when I call flex config justify content flex flex direction all these are going to be false because I'm not going to pass in any values for those. So I'm going save justify content is not false. Then I want to set the justify-content value and that's it. So I'm going to say justify content and here what we're going to say is justified content and just set it just like we're doing right here and this is obviously going to take the value of the variable and it's going to pipe it right in here. And so it's going to set that value.

So now with that in place what I can do is I can just go and populate each of the other ones so that second one is going to be flex this one's going to be flex direction. Then this last one is going to be align items and I'm going to get rid of my comments since I now have these up there as my arguments. We have justify content. Now let's take care of flex since that's our second one. Now let's take care of flex direction so this is going to be the third one and last but not least we're going to take care of align items. So we have to make sure we're also setting the actual value. So this one's going to be Flex direction. And lastly this is going to be flex. Believe it or not, that is it. We now have a full flex mix in a full flex box mix in. And now we can get to the fun part which is cleaning up all of our code. So the very first thing we're going to do is we are going to say import or include I get those mixed up a lot so I'm going to say include flex config right here. As you can see the air went away. Look at this. Everything's still the same. That's good. The whole goal of this project is everything would be the same when you're done with it. So that is a good sign. Now this is our most basic one because remember when we're calling this all of these items are going to be false because we're not setting any values we're not passing in any arguments at all. So each one of these when it checks to see it's going to say OK is justified content false, no, it is or it is false so we don't have to worry about this. Let's get a check for Flex then extraction Let's go see that all of them are still false and because of that all it's going to do is set the one display flex value.

So that is the first one we're getting there. Now I'm going to put this right at the top of our item. So here we have flex display flex and we know we can get rid of this par justify content and that's it. So here we have those two. You know the way that you can set these are the way you can use named arguments here is I can say flex just like that. Then I can say justify content same thing. Now I can get rid of all of this. And now you can see everything is still working. All the buttons are there the images are lined up. The item is still working. If we were to delete these items you can see that it no longer works. So that is a great sign. We are well on our way. So I'm going to just come copy this again and you can see that we have our identical just display flex. I'll get rid of that one. And technically we can leave that in there but I like to be nice and uniform with all of the calls.

This next one we have three elements so we have display flex which we can get rid of and then we have a flex direction and then a justified content. So let's add these as arguments. So Flex direction is column and then justify content just like that except now we need to add in the dollar sign make sure you always add that in. That's how it knows what it is. And look at that were back up and running. Everything is working and our code is looking so much cleaner.  

Next moving down right here. We have this button group and it looks like in the starter code I had a duplicate call so we don't have to worry about putting flex and on that just line items center. So display flex We don't need we only need a line items center. So I'm going to pull that out and then just replace these items there. And now everything all of our items are back up and running. So we are moving along. Next one is the button. So with this button, we know that we don't need to display flex. We already have a line item center so that when we already had in there from what we copied in and then we need to have this flex direction set. So here I'm going to say flex direction row and then we also need justify content center so paste that in and let's get rid of our old lines and everything is back up and running. And if you look at everything else we're done.

So every one of our code elements that used to rely on all those manually typed in Flexbox style definitions and that full list. Now they are completely encapsulated in this nice set of mix in elements so now this one mix and can manage all of our flexbox type of behavior throughout the entire application. This just makes life much easier it's much easier to know what I have access to. And if you notice we cut off a number of lines from this specific file. Now you may say that I added 19 lines with this mix and but when you think of a massive application. So, for example, dev camp has tens of thousands of lines of CSS code. When you have a lot of flexbox it's utilized throughout tens and actually hundreds of CSS files then you're going to have this type of container wrapper in each one of those files that all had a lot of flexbox a lot of duplicate code in there. And so it with a 19 line mix in I was able to go and eliminate all that from the entire application. So that makes the code much more efficient  it's organized so much better it's much easier to make changes on the fly. And for future CSS files or future Scss files that I create, I know that I don't have to worry about manually typing out all of those different mixing elements I can or all those flexbox elements I can just call a mix and just like we did right here. So if you went through that. Excellent job. That is definitely a non-trivial type of mixin to implement. It included everything from conditionals to named end to fall argument types to using variables all kinds of different things like that. So very nice work.


In the code below I've created a 'flex-config' mixin that completely removes all of the messy flex style rules:

```sass
@mixin flex-config($justify-content: false, $flex: false, $flex-direction: false, $align-items: false) {
  display: flex;

  @if $justify-content != false {
    justify-content: $justify-content;
  }

  @if $flex != false {
    flex: $flex;
  }

  @if $flex-direction != false {
    flex-direction: $flex-direction;
  }

  @if $align-items != false {
    align-items: $align-items;
  }
}

.container {
  @include flex-config;
  .item {
    @include flex-config($flex: 1, $justify-content: space-between);
    border: 1px solid grey;
    border-radius: 5px;
    margin-bottom: 10px;
    .content {
      @include flex-config;
      .metadata {
        @include flex-config($flex-direction: column, $justify-content: center);
        margin-left: 20px;
        .title {
          margin: 0px;
        }
      }
    }
    .btn-group {
      @include flex-config($align-items: center);
      .button {
        @include flex-config($flex-direction: row, $align-items: center, $justify-content: center);
        height: 100%;
        width: 42px;
        font-size: 2em;
        a {
          color: green;
          text-decoration: none;
        }
        &:hover {
          background-color: maroon;
          cursor: pointer;
          a {
           color: white;
          }
        }
      }
    }
  }
}
```

So what exactly is going on? Let's walk through it line by line:

- I'm setting a full list of variables that could potential be used for this flexbox implementation and I'm setting all of them to false by default.
- Inside of the mixin I always have the 'display: flex' rule set since that is needed for each time that the mixin is included.
- Then I check to see if each variable is not false (this means that the variable was used). If so, I set the style rule to the value passed in as the argument.
- From there I simply include the mixin in each place where the old flexbox code was.
- For the locations where only the 'display' rule was called I can call the mixin with no arguments.
- In the locations that had a set of rules, such as align-items or flex-direction, I pass in the values with named arguments.
- And that's it. Not only is this container class cleaned up, but not I can call this mixin from anywhere else in the application that uses flexbox.
