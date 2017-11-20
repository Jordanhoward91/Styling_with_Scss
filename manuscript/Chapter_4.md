#Chapter 4 Advanced Scss

##Scss Lists, @each Directive, and String InterpolationScss Lists, @each Directive, and String Interpolation

This guide will help you demonstrate how to utilize lists, the Scss @each directive, and string interpolation in order to dynamically generate classes.

I think we're going to have a lot of fun with this guide. We're going to learn many different new things. And part of the reason for it is because these would each topics that really work best together. I have seen them where they're presented one at a time. And one thing that I came across with the feeling of was that it was very hard to understand why they were important in unless they were actually all grouped together so you could see how they interact with each other. The things that were going to cover in this guide are going to be lists and then we're also going to talk about the each directive inside of Scss and then we're going to finish off with string interpolation. If some of those things sound very fuzzy and you've never heard of them that is perfectly fine we're going to go through them. And I think we are going to have a really fun example.

So at the very top here I have a few images so I have a Tesla image a Maserati image and a Porsche image. Now I am going to grab these you URLs and I'll just paste each one of them in. So we have a Porsche we have a Tesla and then we have a Maserati. So we have each one of these. What I want is to be able to have HTML divs here and I want to dynamically generate the class names inside of our Scss. That's something that is possible from within Scss and it is a great way of performing tasks such as I imagine that you had a list of icons or you had something in your assets directory and you wanted to iterate through and you didn't want to manually just type the class name then pull in the image URL and do that for every single one. If you only have two or three like this example it may not seem like a big deal but imagine that you have an application with hundreds of icons or images and literally all you're trying to do is to change a certain number of values such as setting the background image or having a size or setting it to no repeat or anything like that. You don't want to perform that task over and over again that's a bad programming practice. Then also any time you add other icons you don't want to have to go and repeat all of it again.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/HTML+CSS+images/scss/image4.png)

So let's see how we can leverage each one of those things we're going to once again this guide is going to be all about lists. It's going to be about the each directive and it's going to be about string interpellation. So I'm going to bring this down here and I'm in fact I'm just going to comment all of these out just so they don't get in the way of the rest of our code and I'm going to create a few more divs here so I'm going to create a div of class car dash Maserati and then I'm just going to repeat this a few times for each of the other cars so we have Mazarati, we have tesla, and then we have a Porsche so that is all we need on the HTML side which is going to be pretty cool. This means that if you have an application that you have this type of behavior built in to with what we're going to build in Scss then you could bring in entire code components just with these little div calls.

```html
<div class="car-maserati"></div>
<div class="car-tesla"></div>
<div class="car-porsche"></div>
```

So now with Scss Let's talk about what we need to do. First thing we're going to implement is a list. So here I'm going to add comments. You know if you follow many of my blogs and other courses that I'm not a big fan of comments but I will do implement comments here just so you can see them. It shows what each one of these elements are for using it for your own reference. So here we're going to create a list called cars and with cars. I'm just going to pick out the names that we want. So are you going to say Mazarati then Tesla. And lastly we're going to go with Porsche. And so if you have this they are building a car Web site. Then you could have each one of your images in the asset directory just like this and give it whatever name is going to be called and then it can iterate through and it can build all of these for you. So now I'm going to come down and we're going to use our each directive now or each directive is going to look a lot like the if conditional or the mix in. So we're going to say each directive and hear what that means is it's going to start with an @ symbol and then we're going to say each and the very first thing that we pass to each is going to be what's called an iterator variable. So here I'm going to say car name. Now if you notice there's nothing called a car name that we've declared yet. What each does is you the very first argument you pass it is going to be whatever the car is every time that it goes in it's loop. So with each the first time that iterates over cars car name the first time is going to be Mazarati the second time it's going to be Tesla. And the third time it's going to be Porsche. So here we have each car name in and then I can just pass in our list so I can say each car name in cars and then from there I can now pass in everything that we want to happen.

So what I want to happen is I want to dynamically generate all of these class names. So if you were to build this by hand you do something like this. You could say car-tesla, and then you would build all of your classes just like this. However, because of the each directive because of string interpellation and lists we don't have to do that. We can't actually just make one class and it will dynamically generate all of this for you if you come from any language programming language like Ruby and you've ever worked with metaprogramming. This is very similar to metaprogramming. And if you're about to start learning more about Ruby and metaprogramming this is a great introduction because essentially what we're doing here is something that many people would say is incredibly advanced development because we're dynamically creating code on the fly. We're essentially writing code that is going in turn and it's writing code. So the next thing we're going to implement so so far we have lists. Now we have our each directive.

```sass
// List
$cars: 'maserati', 'tesla', 'porsche';

// Each directive
@each $car-name in $cars {
  // String interpolation
  .car-#{$car-name} {
    background-image: url('https://s3.amazonaws.com/bottega-devcamp/scss/cars/#{$car-name}.jpg');
    background-repeat: no-repeat;
    height: 300px;
    width: 500px;
    object-fit: fill;
    float: left;
  }
}
```

The next thing we're going to put in place is string interpellation. So here you use a string interpellation and let me just fix the indentation. There you go. So the way that you use string interrelation inside of Scss is by using the same syntax as if you're coming from the Ruby programming language. So what you do is you start with a hash then use the curly brackets and then you put anything inside of it that you want. In this case we're going to use our iterator variable. So this car name it's going to be Mazarati the first time which means it's going to say car-Mazarati which you notice is right here. So because we have access to a Mazarati that means that we get to place it right in here and this is going to generate this class for us whenever the Scss compiles. So this is a first part. This is going to generate our three class names. Right now they're empty though so let's go and let's build it in with some more unstring interpellation. So I'm going to say. Background image and pass in a URL and the URL we're going to pass in is going to be this one except we're going to change the name. So instead of it being Porche Tesla or Mazarati, we're not going to have to hardcode it. We're going to pass it in using string interpolation. So here again make sure you finish off with a semicolon. So here what we're going to do is take this car name and I'm going to take the entire thing here and we'll say instead of and you make sure you keep the jpeg on there. But instead of Porsche it's going to say car name and then dot Jpeg so the first time it comes around. It'll be Mazarati. So we'll get this image then it's going to hit Tesla. So it's going to grab this image. Then Porsche and it's going to grab this image. So that is the first part.

```sass
// List
$cars: 'maserati', 'tesla', 'porsche';

// Each directive
@each $car-name in $cars {
  // String interpolation
  .car-#{$car-name} {
    background-image: url('https://s3.amazonaws.com/bottega-devcamp/scss/cars/#{$car-name}.jpg');
    background-repeat: no-repeat;
    height: 300px;
    width: 500px;
    object-fit: fill;
    float: left;
  }
}
```

Now let's add a few more styles. I'm going to say background. Repeat set the sequel to no repeat then height. Set to three hundred pixels height. And as you can see right there we're already pulling in our images and also all of these image URLs you can use your own or if you want to follow along exactly. Then I am making them available in the show notes, then I'll say this is five hundred pixels and next one object-fit will be fill and then let's say we're going to float this to the left so that is all side by side and look at that. We have everything that we need right here. So what we've done here is pretty neat. Instead of simply having to copy and paste this code like we would have technically if you didn't use each in these lists then you'd have to have one of these classes that's completely identical except for having a slightly different URL. Now this is something you could also use a mixin for but I think this is in this case using the each directive is probably the most intuitive.

Now if you don't believe me about the classes being dynamically generated Let's take a look. If I come and click inspect right here this brings everything up and look at that. We have a class called car dash Mazarati. Even though we don't actually have anywhere in our Scss file where we've created that class we've all we've done it all dynamically we've done it all when the preprocessor hit and started running. So if we look at the other one here we have car-Tesla. And for the last one, we have car-Porsche.

So this is something that's pretty cool this is a nother way. Remember that one of the top goals that Scss looks to accomplish is to help you as a developer be as efficient as possible with your code to remove duplication and to be able to organize your code in a way that it's intuitive and scalable. And that's what these three components do.



###HTML Code

```html
<div class="car-maserati"></div>
<div class="car-tesla"></div>
<div class="car-porsche"></div>
```

###Scss Code

```sass
// List
$cars: 'maserati', 'tesla', 'porsche';

// Each directive
@each $car-name in $cars {
  // String interpolation
  .car-#{$car-name} {
    background-image: url('https://s3.amazonaws.com/bottega-devcamp/scss/cars/#{$car-name}.jpg');
    background-repeat: no-repeat;
    height: 300px;
    width: 500px;
    object-fit: fill;
    float: left;
  }
}
```

###Image URLs

- https://s3.amazonaws.com/bottega-devcamp/scss/cars/tesla.jpg
- https://s3.amazonaws.com/bottega-devcamp/scss/cars/maserati.jpg
- https://s3.amazonaws.com/bottega-devcamp/scss/cars/porsche.jpg


##Real World Example of the Scss @import Directive

This lesson walks through a real world production application and examines how the @import directive is used to organize a full project.

We're making our way nicely through the Scss course. And in this guide we're going to talk about the import directive inside of Scss and instead of us going and looking at a few sample pieces of code I wanted to show you a real-world production application because the import directive specifically was made to be able to manage your code especially for larger applications. Right here we have a decent size application. And so if I go in this is a Rails app but Scss can be used in any programming language and framework. So you do not have if you work in something else such as PHP or dot net or something like that then you can absolutely still use Scss.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/HTML+CSS+images/scss/image5.png)

This is just the example. So I'm going to go into where I have my main application file and you can see here it is application dot Scss. So in order to use this statement, it has to be a dot Scss file extension and right here instead of seeing styles what you actually see are a bunch of import statements. So what does that mean. Well what the import directive does is it allows you to as you may have guessed import other files. Now sometimes these files can be partials and then other times they can be entire other sets of Scss files. So we're going to walk through what that actually looks like. This is a very common pattern you'll see where you have one master application Scss file and then it imports all kinds of other Scss files to be able to organize the code and it also accomplishes one other task that is very important. If you remember Cascading Style Sheets is what represent CSS that's the acronym. The whole cascading nature of stylesheets means that it's very easy to accidentally have one style override another one if you're using a framework such as the bootstrap framework like we're using right here it's incredibly important to be able to override certain styles that you don't want to keep.

So for bootstrap it has a number of buttons and the buttons may be greyed out of the box for certain prototype applications, but they're not what you would use in a production one. So you have to make sure that your custom styles that override this are called afterwards and by leveraging import statements then it makes that much easier to control that.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/HTML+CSS+images/scss/image6.png)

So if you were to go in the full stylesheet directory you'd see all kinds of other styles here. So a really good one to look at was the very first one at the top. You may have noticed was a variable call so we're importing variables. And just like you've seen throughout this entire course here we have a full set of variables and when. By me importing this at the very top. What this allows for is for every one of these files it has the ability to call this. So now from the profile file right here I can call any of the variables inside of the variables Scss file. So this is a way of organizing the code and being able to still call all of those different things such as variables and mix and quite efficiently. So what does this actually look like. Well if we open up the application here and go to inspect and then go to sources you go to assets you'll see that this is partly Scss and then also rails.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/HTML+CSS+images/scss/image7.png)

So Rails has its own compilation process but if you click on the application CSS file all of those styles all of those import statements all got brought into a single file and then from there Rail's also it condensed all of it so it minified it. It made it removed any of the excess whitespace to help shrink the size of the file. But then before that even happen Scss performed its precompilation process so none of these styles that you would see such as using things like variables or nested elements none of that is actually inside of here. It is all compiled straight into regular CSSA. So that is a real-world example of how to use the import directive inside of Scss.



###Reference Project

- [Source code](https://github.com/jordanhudgens/daily-smarty/blob/master/app/assets/stylesheets/application.scss)
- [Application](http://www.dailysmarty.com/)


##How to Use the @content Directive in Scss to Allow for Mixin Flexibility

This lesson examines the @content directive in Scss and specifically walks through how to refactor a mixin by yielding to a set of custom styles.

In this guide we're going to talk about the content directive now the content directive is a very helpful little tool that we can use with mixins that allow us to make a little bit more flexible kinds of interfaces for those mixins. So right here I already have a standard mix in with three arguments right here and this is for a set of a alert device.

![](https://s3-us-west-2.amazonaws.com/bottegarails/SCSS/Screen+Shot+2017-10-27+at+10.57.16+AM.png)

So we have HTML with these divs right here and then we have a mixin called notification that has a number of styles. Everything from a width and height to a border radius and the three that are dynamic the three values that are dynamic are the background color the text font color and then the border. We're bringing those in as arguments. Now this is fine this works perfectly fine our end result is going to result in the exact same CSS code once it gets compiled. However there is another way of doing this. In certain circumstances using the content directive can be a little bit more intuitive than what we're doing right here. Here we are manually setting all these values and we're setting all these arguments and then we're calling them. In this case I would take a different approach. Instead of placing these content items inside of the mixin and I would actually use the content directive.


We can get rid of all of the code right here. So now  it looks like this.

![](https://s3-us-west-2.amazonaws.com/bottegarails/SCSS/Screen+Shot+2017-10-27+at+11.08.37+AM.png)

What I'm going to do is pass in `@content` and this is going to do is it's going to allow us to essentially place any other styles that we want and this content directive is then going to yield to whatever we pass in.

![](https://s3-us-west-2.amazonaws.com/bottegarails/SCSS/Screen+Shot+2017-10-27+at+11.11.54+AM.png)

In regards to this first error notification, the way that you can call this content directive or how you can pass data to it is by opening up curly brackets and setting our values to what we want like below.

![](https://s3-us-west-2.amazonaws.com/bottegarails/SCSS/Screen+Shot+2017-10-27+at+11.37.04+AM.png)


So now all of this is working perfectly.  The important thing to know is we're not limited by these items I know we started with these but if I wanted to do anything else then I could place all of that right here in this content.


So if I wanted to, I could actually override the width here and I could say 15 pixels or something like that it would shrink. Obviously that would be a little bit weird because you wouldn't be able to see it but the whole point is to show that it is now completely dynamic so we can override any of those values that we want. The whole point of using the content directive is not to replace the arguments for mixins because there are plenty of times where you're going to want to do that.

I personally love using arguments in mixins. It makes it very easy, it's very much like writing Ruby code or javascript code. However, there are times where I want a little bit more flexibility and that's what this content directive allows me to have. Here I don't have to worry about passing in all kinds of crazy variables and arguments and worrying about default types and those kind of things. I can simply call the content directive right here and pass in any other types of styles overrides additional items right in there and it'll all work very nicely. So that is how you can use the content directive in SCSS.



###HTML Code

```html
<div class="error">
  There was an error processing your request.
</div>

<div class="success">
  Your request was processed successfully.
</div>
```

###Starter Scss Code

```sass
@mixin notification($background-color, $color, $border) {
  width: 99%;
  height: 35px;
  text-align: center;
  padding-top: 10px;
  font-size: 1.2em;
  font-family: Verdana;
  border-radius: 3px;
  margin: 10px;
  background-color: $background-color;
  color: $color;
  border: $border;
}

.error {
  @include notification($background-color: DarkRed, $color: white, $border: 1px solid LightSlateGray);
}

.success {
  @include notification($background-color: MediumSeaGreen, $color: MintCream, $border: 1px solid LightSalmon);
}
```


###Refactored Scss Code with @content Directive

```sass
@mixin notification {
  width: 99%;
  height: 35px;
  text-align: center;
  padding-top: 10px;
  font-size: 1.2em;
  font-family: Verdana;
  border-radius: 3px;
  margin: 10px;
  @content;
}

.error {
  @include notification {
    background-color: DarkRed;
    color: white;
    border: 1px solid LightSlateGray;
  }
}

.success {
  @include notification {
    background-color: MediumSeaGreen;
    color: MintCream;
    border: 1px solid LightSalmon;
  }
}
```
