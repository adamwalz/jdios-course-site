---
layout: lecture
title: Intro to Objective-C - Part 2
excerpt: In this lecture we're going to look at more of the details of working with Objective-C, specifically we'll use properties and dot notation to gain an understanding of the underlying instance variables, we'll cover when to use strong and weak for memory attributes, we'll explain the difference btween instance methods and class methods, and you'll learn ot create objects and work with types
category: lectures
tags:
- objective c
- foundation framework
- strong vs weak
- properties
---

## Instance Variables and Properties

<iframe width="560" height="315" src="http://www.youtube.com/embed/usMDPUCI86g?rel=0" frameborder="0" allowfullscreen></iframe>

In Object-Oriented Programming, an instance variable is a variable defined in a class, for which each object of the class has a separate copy. You may have heard of these as member variables in Java. This is in contrast to a class variables which is declared as `static` in Java and is shared across all instances of the class, and may not even need an instance. 

In Objective-C we prefer to use properties instead of instance variables for safety and subclassability reasons. As much as possible your should access and change state through the getter and setter and not through the underlying instance variable.  A public property exposes the *getter* method if the property is  `readonly` and both the *getter* and *setter* methods of the property is `readwrite`. 

In this class, we'll always use the leading underscore naming convention for the instance variabke that backs a property. When possible, we'll also depend on the **synthesize-by-default** feature to synthesize the accessor methods and the instance variable for us. 

There are two situations where we need to explitely There are two situations where we need to explitely synthesize the methods and variable

+ If we have a rad only property and we create our own getter, then we need to type in the `@synthesize` ourselves to generate the instance variable.
+ If we have a read write property and we create our own getter and setter, we need to type in the `@synthesize` to generate the instance variable

Here is what that syntax looks like

{% highlight objectivec %}
@synthesize ship = _ship;
{% endhighlight %}

Using Automatic Reference Counting, there are only three places you would ever use the instance variable directly unstead of the property. 

+ Writing your own getter
+ Writing your own setter
+ Initializing a property inside of an `init` method

Other than that, always refer to properties using dot notation, and not the underlying instance variable. 

### Dot Notation

Sending the getter or setter message to an object can be accomplished with square brackets just like any other method.

{% highlight objectivec %}
NSString* name = [ship1 name]; // getter
[ship2 setName:name]; // setter
{% endhighlight %}

But when the message is the getter or setter, a much more consise option would be to use dot notation. 

{% highlight objectivec %}
NSString* name = ship1.name; // getter
ship2.name = name; // setter
{% endhighlight %}

These two versions are exactly the same to the compiler. This will also look more familiar coming from a Java background. Your code is a conversation, dots separate the properties from other messages that are being sent.

## Strong Vs. Weak Pointers

<iframe width="560" height="315" src="http://www.youtube.com/embed/7SX6mTskHtk?rel=0" frameborder="0" allowfullscreen></iframe>

We're using ARC in this course. ARC was introduced along with iOS 5 and included two new keywords for memory: `strong` and `weak`.

Before Automatic Reference Counting we had to manage memory manually in code. With ARC, the compiler decorates our code with instructions on when to hold on to objects in memory and when to let them go.

When you work with objects, remember that the variables are really pointers to those objects. We might have a lot of different objects pointing to the same object in memory. When there are no objects remaining that care about a given object, that object needs to be cleaned up or else we have a memory leak.

The word `strong` says, "Keep this object around at least until I don't care about it anymore". The guarantee is that this object will be there as long as at least one object needs it and it will be gone as soon as no objects need it. With memory management we think selfishly about our own needs. 

In our first assignment, the controller needs to hold on to the `NSMutableArray* planner`. If the `planner` disappears while the controller is still managing the buttons and display, then no more TODO items can be added. Thats why we declare the `planner` property like this in `JDViewController.h`.

{% highlight objectivec %}
@property (strong, readonly, nonatomic) NSMutableArray* planner;
{% endhighlight %}

On the other hand, there are times when you only want to use a property as long as it's around. When it disappears, you just won't use it anymore. For those cases, you use the keyword `weak`

In assignment 1, we declare a `weak` reference to the `plannerItemText`

{% highlight objectivec %}
@property (weak, nonatomic) IBOutlet UITextView *plannerItemText;
{% endhighlight %}

The only object holding on to the `plannerItemText` is its superview. When the view is gone, then the `plannerItemText` is no longer visible, so it doesn't make any sense to hold on to it in the view controller. We would be updating the text of an element that isn't on the screen any more. 

**Note:** Collections and containers have `strong` references to the objects they contain. This is why the superview was holding on to `plannerTextItem`. A superview has `strong` references to all of its subviews and an array has `strong` references to all of the objects in that array.

One of the really nice things about `weak` is that when the object is removed from memory, our reference to it is set to `nil` automatically. The advantage of this is that messages sent to `nil` do absolutely nothing. In programming terms this is called a no-op.

`nil` means that the pointer is zero. The pointer does't point to anything. All instance variables that point to objects are initially `nil`. We need to initialize the property somehow. 

Objective-C programmers don't tend to program defensively. We don't need to check if something is non-nil before sending it a message, but there are times when we need to make sure an objects exists before performing an action. You can use an implicit `if` statement to check whether an object is `nil`

{% highlight objectivec %}
if (self.planner) { // same as if (self.planner != nil)
}
{% endhighlight %}


## Instance and Class Methods

<iframe width="560" height="315" src="http://www.youtube.com/embed/bKlGSko5C0c?rel=0" frameborder="0" allowfullscreen></iframe>

Some messages need to be sent to objects and some need to be sent to classes. 

For example, the `UIButton` class has a pair of methods `titleForState:` and `setTitle:forState:` that get and set the button title for a given state of the button (normal, highlighted, disabled, or selected).

These are messages that require a particular button in order to set its title. You wouldn't want to set the title of every button together.

If you look at the documentation for `UIButton`, you'll see that these methods are declared like this

{% highlight objectivec %}
- (NSString*)titleForState:(UIControlState)state;
- (void)setTitle:(NSString*)title forState:(UIControlState)state;
{% endhighlight %}

The minus sign in front of each method indicates that they are instance methods and the receiver of each is an instance of `UIButton`. You send this message like this

{% highlight objectivec %}
[self.myButton setTitle:@"Done" forState:UIControlStateNormal];
{% endhighlight %}

`UIButton` also has a method `buttonWithType:` that is declared like this

{% highlight objectivec %}
+ (id)buttonWithType:(UIButtonType)type;
{% endhighlight %}

The plus sign out front indicates that this is a class method. You send this message to the `UIButton` class itself, not an instance of the class. This call creates a new round rect button

{% highlight objectivec %}
UIButton* button = [UIButton buttonWithType:UIButtonTypeRoundedRect];
{% endhighlight %}

You need to look at the docs to see whether a method is an instance method (preceded by a `-`) or a class method (preceded by a `+`)

## Instantiation

<iframe width="560" height="315" src="http://www.youtube.com/embed/EeBC4pJOEg8?rel=0" frameborder="0" allowfullscreen></iframe>

There are five basic ways to get an object that you'll assign to a property or local variable.

1.. Ask another object to create one for you. Here a string returns a new strong create from the first. 

{% highlight objectivec %}
[self.plannerTextItem.text stringByAppendingString:digit];
{% endhighlight %}

2.. Ask another object to return a pointer to an object that already exists

{% highlight objectivec %}
[self.planner lastObject];
{% endhighlight %}

3.. Create an object from scratch and initialize it. The most common way to do this in with `alloc init`

{% highlight objectivec %}
NSMutableArray* _planner = [[NSMutableArray alloc] init];
{% endhighlight %}

Even though the calls to `alloc` and `init` are two separate messages, we never perform them separately. We would't send the alloc message and then later send init. We always do them together. We would't send the `alloc` message and then later send `init`. 

`alloc` is a class method that creates enough room in memory for the object and it zero initializes all of the instance variables. 

Before you use your object you need to initialize it. You initialize an object by sending some variation of the instance method `init` to the object that was just created using `alloc`.

In assignment 1, we *lazy initialize* `planner`. The key is that the `planner` has to be initialized before we use it. So the first time we try to access `planner` using the getter, the getter create an instance of `planner` like this

{% highlight objectivec %}
_planner = [[NSMutableArray alloc] init];
{% endhighlight %}

Some classes provide multiple initialization methods. All of these methods start with `init<something>`. For example, `NSMutableArray` provides an initialized called

{% highlight objectivec %}
- (id)initWithCapacity:(int)capacity;
{% endhighlight %}

If you have multiple initializers, one must be your *designated initializer*. All other initializers must call this initializer and this designated initializer is the only one to call the superclass' designated initializer.

You have to document which method is your designated initializer. Add a comment to the header file indicating the designated initializer. If you don't explicitly say which method is the designated initializer, there's no way for someone using your code to know.

**Note:** `init` doesn't return our class' type; it returns `id`. 

## Object Types

All `init` methods return an object of type `id`. The `id` type is a pointer to any object. We can send an `id` any valid method and the compiler won't complain. 

Along with not complaining however, the compiler also cannot help us out if we make a mistake if we use `id`. It is better to statically type our objects so the compiler knows what we are doing and can point out our errors. Always store the object returned by `alloc init` in a statically typed variable like this

{% highlight objectivec %}
// storing object of type id into variable of type NSMutableArray
NSMutableArray* _planner = [[NSMutableArray alloc] init];
{% endhighlight %}

There are some times that we get an object back and we may not know what class it is. For example if we have an array with multiple different types of elements, we can later check if an element we retrieve is a number and store it into a `double` variable.

{% highlight objectivec %}
id element = [self.array lastObject];
if ([element isKindOfClass:[NSNumber class]]) {
  result = [element doubleValue];
}
{% endhighlight %}

More commonly, we don't care what an object's class is, we just care that it can perform some task before we send a message. We can use `respondsToSelector:` instead of `isKindOfClass:`

{% highlight objectivec %}
if ([self.thing respondsToSelector:@selector(doThis)])
  [self.thing doThis];
{% endhighlight %}

This is sending `respondsToSelector` something of type `SEL`. This is a selector. It's essentially the method name. 

## Foundation Framework Objects

You should have enough of a feel for Objective-C by now to write fairly sophisticated programs. The following videos help with that by providing a look into Apple's foundation building blocks for building applications. You may use these as a reference, but watching them is not required and you will not be quizzed on them. 

<iframe width="560" height="315" src="http://www.youtube.com/embed/tkTD0EItIqA?rel=0" frameborder="0" allowfullscreen></iframe>

## Foundation Framework Collections

<iframe width="560" height="315" src="http://www.youtube.com/embed/rvULryB_6Kg?rel=0" frameborder="0" allowfullscreen></iframe>
