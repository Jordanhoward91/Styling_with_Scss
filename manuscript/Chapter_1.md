# Styling with SCSS

##Chapter 1 Introduction to Scss

####The Who, What, When, Where, Why, and How of SCSS

Welcome to the first lesson in this getting DRY with SCSS course. In this guide what we're going to discuss are the who, what, when, where, why and how and of what SCSS is. By getting some background and learning about who created the framework, that gives us a little bit of insight on the problem that they were trying to solve, if they were successful in doing it and also if that's going to help you as you try to integrate and learn that system.

####Who

SCSS was created by Hampton Catlin. Hampton is somewhat of a celebrity in the Rails community because he has created some incredibly popular libraries. Things that you may have already been using and didn't even realize it. In addition to SCSS he also created the Hammell templating library and Mobile Wikipedia.


####What


Moving on to the what. SCSS is short for Sassy Cascading Style Sheets and it was created over 10 years ago. It's gone through some incredible upgrades that have allowed us to use it in pretty powerful ways.


####Where


And that leads directly into the where. Where can we use SCSS? That's something that's really neat about how it was built, even though early on it was something that was considered to be a Rails library. It now can be used in pretty much any kind of framework that you have. Whether it's a mobile framework to a javascript front end. It's not connected or locked into working with one type of stack or another. And in fact when we're going through this course we're going to use a completely separate system in order to build our stylesheets just so you can see that it's completely agnostic to whatever stack you happen to be working on.


####Why


So far we've covered the who, the what and the where. And we're going to get to my favorite one which is the why. Why is it important and why is it helpful to learn about SCSS? That is something that I try to impress on any student when they're coming through the program and they want to get into more advanced topics when it's coming to front end design. SCSS allows us to be able to streamline our entire design implementation process. So if up to this point you've always written just in pure CSS that's perfectly fine. It is a great place to start but what SCSS allows you to do is to streamline that process. Everything that SCSS does revolves around being able to take out any kind of repetitive processes. So if you find yourself writing the same type of code snippets or even very similar types of CSS styles on a regular basis, SCSS allows you to stop all that repetition and start using shared code.


Throughout this course you're going to see how pretty much all of the tools that are built into SCSS are giving you the ability to make all of your style sheets much more scalable. Everything from being able to build mixins, where you can load a bunch of functionality inside of one type of element and then shared across your entire system, to using conditionals to be able to check if one style is what you want in one situation and it's something you wanted in a different situation, those styles can actually change dynamically. Which is something that before this, we had to use things such as implementing code inside of our views or building view helpers in order to create that same type of feature. Now that's all available directly in the SCSS file it works like a programming language.


In addition to tools like mixins, SCSS also gives us the concept of variables. If you've ever had a situation where you had a CSS style sheet and you had some color definition in 20 spots and then decided you maybe wanted to change the color just a little bit. You would need to change that color in every single location that you called it. With SCSS you can define all of your styles, colors and sizes at the top and then reference those throughout the application. So when you want to make that change, you make it in one spot and it auto populates every place else. Like I said everything in SCSS revolves around being able to create shared code that is much more DRY and follows best practices.


####How


So how is all that possible? That leads directly to the last question we're going to answer in this guide, which is the how. What SCSS does is it allows you to write CSS type styles. It looks a lot like CSS with some nice layers on top. Technically SCSS is what's called a preprocessor. Which means that it's really just a type of scripting language that the browser can't interpret. As that preprocessor runs it takes all of the code that you wrote, all of those SCSS styles, and converts it directly into CSS. It takes all of the different efficiency's, the variables, the mixins and the functions, the conditionals and then it builds your own CSS files directly for you.


In the next guide we're going to go through a screencast demo where you can see exactly how that process unfolds.


##SCSS Preprocessor Demo: How the SCSS Magic Happens

Now that you have a little bit of an overview on what SCSS is, we're going to walk through the process. We're going to see exactly what it does and how it's able to build out all of the different features that we have talked about.We are going to take a high level view of what SCSS is actually doing so that we can see there really is nothing magical about it. It simply is one type of markup language that can be converted into something much more complex.

If you have worked with other types of libraries like JQuery or Angular which are JavaScript libraries and frameworks, then those are very similar to SCSS in the sense that they sit on top of another language and then they are converted into something that is much more complex.

That's essentially what SCSS does every time we use it, regardless of how complex it may be. Technically all of this could be performed with CSS. In regards to the output, we use SCSS so that we can streamline our processes and so we can better organize our code.

So right here we have a Code Pen. We are going to be using Code Pen throughout this entire course.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Javascript+images/codepen.png)

 On the left we have HTML, and on the right is the SCSS file. If I just put this into a normal CSS file, the browser would not interpret it and it wouldn't give us the desired functionality.

 It would throw an error because CSS doesn't know what a mixin is, it doesn't know what a variable is and it doesn't know what to do with the include statement . All of these are elements of SCSS. All of these thing are going to be converted into pure CSS because that's what browsers are able to render.

Now to see what this looks like in CSS you can click the right hand side dropdown and view compiled CSS.

![](https://s3-us-west-2.amazonaws.com/bottegarails/SCSS/Screen+Shot+2017-10-06+at+2.50.48+PM.png)

Here we can see a completely different set of styles. One is called error and the other is success. Notice there's a lot of duplication. We have identical width, height, text alignment, font size, font border, border radius and margin. The only big differences we see is the colors.

If we decided to write this in pure CSS we would have quite a bit of duplication. This would be a messy way to write it due to the fact that if we wanted to make a change we would have to change every instance.

 If we go back and look at what we created you can see that we don't have any of that duplication inside of our SCSS file. We simply have this mixin. At this point, don't worry about the syntax, right now we are just looking at what occurs and just walk through the fact that SCSS and the browsers by alone would not be able to know what we're doing. You wouldn't be able to define two different classes like this.

The other thing that you may notice is that the entire concept of a mixin was skipped over. When the process starts, it ignores the mixin. It simply takes all of that code and it adds it into a master CSS preprocessed file, then sends it to the browser. So now the browser doesn't care about duplication.

If we wanted to add a new type of style, we have success and error, but I want to have warning. We can simply create this new class and change the background color, the font color and then the border if we want it to be different.

![](https://s3-us-west-2.amazonaws.com/bottegarails/SCSS/Screen+Shot+2017-10-06+at+3.33.59+PM.png)

If we go back and view the compiled CSS, you can see now we have our warning class and it has all of those elements.

As you start going through the course, one thing that I'll definitely recommend for you to do is play around with switching between viewing the SCSS file and what it compiles to. This will allow you to learn a lot more about what is going on behind the scenes with CSS, especially when we get into more complicated topics such as nesting and nested pseudo selectors. Those are things that if you're brand new to front end development it may be a little bit intimidating. Using SCSS and seeing the CSS version will drive home the importance and functionality that SCSS provide us.

##Differences Between Sass and SCSS

So far we have been through a full overview of SCSS, walked through the preprocessors step so you can see what code was written and then we looked at how it got translated into something the browser could understand.There is something that might be a little bit confusing whether it's in some type of coding interview situation or just in general as reading documentation. There are actually two different types of SASS syntax.  There is SASS and then there is SCSS. Now technically both of those are called SASS which makes for some kind of confusing component when you're first starting to learn it. Here we are going to talk about what the differences there are between the two and what we are going to be using for the course.

SASS was the original version. It does not look anything like CSS and it cares about things such as indentation. When using SASS all of your code has to be segmented and it has to have the right number of spaces right in front of each set of style definitions. It doesn't have curly braces, it has plus signs and equal signs all over the place. If you've ever worked with Hammill or slim, you may notice it looks very similar to that type of setup.

What you will see more often is SCSS and that's what we're going to be using in this entire course. There are many reasons why SCSS is used so widely. One is that it looks exactly like CSS. Also It it uses curly braces and semi colons to end each style definition. This makes it much more familiar and the learning curve is also much lower. Also if you want to write just pure CSS code a SCSS file will still process it where the original version of SASS would actually throw an error.

I wanted to go over these differences due to the fact that during your research you are going to run into both syntax. Without this brief overview it may seem very confusing.

##How to Configure Codepen to Process Scss Files

We are now going to walk through how we can start working with SCSS. If you're just writing pure CSS you don't need a tool like this because there is no preprocessor component. Since we are using SCSS we need to be able to convert all of our SCSS styles into something the browser can actually understand. There are a number of options. You can simply install the entire SCSS preprocessor locally. This is pretty rare that I ever have to do that myself. So I'm going to teach you different skills and knowledge that you'll need when you're using this in a real world type of application. Usually we would use some type of web framework whenever we need to implement SCSS. So if you have a Rails application you can follow along throughout the entire course doing the same exact styles because rails provides that pre compilation process.


We are going to use CodePen for a few reasons. First, it doesn't require any setup. Also, it will run the same regardless of whether you are working on a PC or a Mac. The goal of this course is provide you with a foundation that you can apply to any project, regardless of what language you are using.

You can either sign up for an account with CodePen, which I would recommend since it is free and it allows you to save your progress. Once you have decided which option, lets then go to create new pen.

![](https://s3-us-west-2.amazonaws.com/bottegarails/SCSS/Screen+Shot+2017-10-17+at+12.55.42+PM.png)

You will then be presented with a new project.

![](https://s3-us-west-2.amazonaws.com/bottegarails/SCSS/Screen+Shot+2017-10-17+at+1.07.40+PM.png)

We are going to get rid of the javascript window. Everything that we are doing in this portion is in HTML & SCSS. The changes that we make here will be automatically rendered in the browser shown below our code boxes. Now there is a little change you have to make before it will automatically recognize the styles.

First we need to click on the gear in the top left of the CSS box
![](https://s3-us-west-2.amazonaws.com/bottegarails/SCSS/Screen+Shot+2017-10-17+at+1.59.39+PM.png)

Then we need to change our preprocessor to use SCSS
![](https://s3-us-west-2.amazonaws.com/bottegarails/SCSS/Screen+Shot+2017-10-17+at+2.00.49+PM.png)


Once we make that change we will notice we now have syntax highlighting and it will pick up the difference between CSS and SCSS. It also changes the heading so we know we are working in SCSS now.

![](https://s3-us-west-2.amazonaws.com/bottegarails/SCSS/Screen+Shot+2017-10-17+at+2.03.25+PM.png)

Now we are all set and ready to go.
