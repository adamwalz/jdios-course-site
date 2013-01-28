---
layout: lecture
title: Intro to Objective-C - Part 1
excerpt: This lecture should give you the appropriate background material for the course. We being iwht a look at some code in Objective-C without the need for Xcode. This is all about syntax. 
category: lectures
tags:
- objective c
---
<iframe width="560" height="315" src="http://www.youtube.com/embed/CcwQbZqkzlk?rel=0" frameborder="0" allowfullscreen></iframe>

# Objective-C Syntax

## Getting Started
Suppose we want to create a Spaceship class so we can later create
objects of type Spaceship.

In Objective-C, we'll define our Spaceship in two different source
files: the header file and the implementation file. This is unlike
Java where your method declarations and implementation is all
within the same file.

### The Skeleton of the Header File
The header file contains everything about the object that you want to
make public, while the implemetnation file constains the inner
workings of the object. 

The header file for the Spaceship class is name `Spaceship.h` and it
will conian the information that tells other people what they can ask
a Spaceship instance or the Spaceship class itself to do. 

Suppose the Spaceship class is a subclass of Vehicle. Then the header
file `Spaceship.h` might look like this

{% highlight objectivec %}
#import "Vehicle.h"

@interface Spaceship : Vehicle
	
@end
{% endhighlight %}

We'll add to thie header file in a bit. Let's look at the
corresponding implementation file. 

### The Bar-Bones Implementation File
There's not much to our `Spaceship.m` implementation file when we
start.

Together, the header and the implementation file define the Spaceship
class. Anything that needs to be public is in the header
file. Consider the contnts of the implementation file as being
private.

{% highlight objectivec %}
#import "`Spaceship.h`"

@implementation Spaceship

@end
{% endhighlight %}

## A Pair of Interfaces
Out header files contain the punlic interfaces of our class. That's
where we declare variables, methods, or properties that we want to
allow others to have access to. Here's a look at where we place each
type of declaration in the publc interface. 

{% highlight objectivec %}
#import "Vehicle.h"

@interface Spaceship : Vehicle {
    // public declaration of instance variable
}
    // public declaration of properties

	// public declaration of methods
@end
{% endhighlight %}

Sometimes we need to declare a variable or property before we use it
but don't want to make it public. We don't want to let anyone else use
our variable or property so we need a secret hiding place.

What we're looking for is a private interface. If it is to be private
it would need to be palced in the implementation file. Coming from a
Java background, you should recognize this as *encapsulation* or
information hiding. We hide as many details as we can from consumers
of our classes. 

We call this private interface a class extension. Its syntax is very
similar to the interface you see in the header file except we don't
include the super class as that information is already present in the
header. We also append open and close parenthesis to the name. 

So the class extension for Spaceship would be named Spaceship().

{% highlight objectivec %}
#import "`Spaceship.h`"

@interface Spaceship() {
    // declaration of private variables
}

    // declaration of private properties
    // declaration of private methods

@end
	
@implementation Spaceship

@end

{% endhighlight %}

Class extensions will turn out to be very useful for other things, and
this is just one of the uses for them, but I will get to that in a
later lecture. 

## Declaring Methods
The key to object-oriented programming is messages. This is similar to
calling a method in Java. The syntax for declaring, implementing, and
sending messages in Objective-C may take some getting used to.

Let's start by declaring methods in our header file. We'll declar two
methods named planetToOrbit and topSpeed that take no
parameters. We'll also declare another method named setTopSpeed: which
taks a single parameter, and a last method named
orbitPlanet:atAltitude: which takes two parameters. The colons are
actually part ofthe method name. 

### Declaring methods with no parameters
The simplest methods to declare are those that don't rake any
parameters. 

{% highlight objectivec %}
#import "Vehicle.h"
#import "Planet.h"

@interface Spaceship : Vehicle
- (Planet*)planetToOrbit;
- (double)topSpeed;
	
@end
{% endhighlight %}

At this point, the syntax should look somewhat like the syntax you've
seen in Java, with some notable exceptions. 

### Declaring methods with one parameter
In Java parameters come after the method name and inside of
parenthesis

{% highlight  java %}
public class String
{
    public boolean equals(String otherString)
    {
        // comparison code
    }
}
{% endhighlight %}

With Objective-C the parameters are sprinkled in along the way, inside
the method name. This allows the various parts of the long method
names to describe each parameter. Many people initially struggle with
this distinction. 

We'll start by looking at a method that takes a single parameter. 

{% highlight objectivec %}
#import "Vehicle.h"
#import "Planet.h"

@interface Spaceship : Vehicle
- (Planet*)planetToOrbit;
- (double)topSpeed;
- (void)setTopSpeed:(double)percentSpeedOfLight;

@end
{% endhighlight %}

### Declaring methods with multiple parameters
This next step is a big one. The main different between this and other
languages, like Java, is that the parameters don't appear at the
end. Every time the moethod name contains a colon, we place the
parameter at that position.

Here's what declaring a method with more than one parameter might look
like in the `Spaceship.h` header file. The method named
orbitPlanet:atAltitude: takes two parameters - one for each colon

{% highlight objectivec %}
#import "Vehicle.h"
#import "Planet.h"

@interface Spaceship : Vehicle
- (Planet*)planetToOrbit;
- (double)topSpeed;
- (void)setTopSpeed:(double)percentSpeedOfLight;
- (void)orbitPlanet:(Planet*)aPlanet atAltitude:(double)km;

@end
{% endhighlight %}

Your eye may need to adjust a bit to this syntax. In time I have come
to really like orbitPlanet:atAltitude: and prefer the interleaved
parameters to seing them pile up at the end of the line.

## Implementing Methods
The methods we declare in the header file are a promise. To fulfill
that promise we need to implement those methods in `Spaceship.m`

The methods that we declared in `Spaceship.h` are essentially getters
and setters for the planet we'll be orbiting, the altitude at which
we'll orbit, and our spaceship's top speed.

We have to declare instance variables that will hold these
values. These instance variables don't need to be public. Let's hide
them away and declare them inside of our @implementation section of
`Spaceship.m`.

Use `_planet`, `_topSpeed`, and `_altitude` as the names
of the variables. 

Wow that looks pretty ugly. _Why _name _our _variables _like _that _?

I'm using the leading underbar because it is widely used for instance
variables in iOS programming, and the convention is so closely held by
iOS developers that Xcode actually rewards using it and will allow you
to write less code because of it. We'll see more about that when we
get to *properties*. 

Here is an overly simplistic stubbing of what our implemation file
will look like

{% highlight objectivec %}
@implementation Spaceship {
    Planet* _planet;
    double _topSpeed;
    double _altitude;
}
- (Planet*)planetToOrbit {
    return _planet;
}
- (double)topSpeed {
    return _topSpeed;
}
- (void)setTopSpeed:(double)percentSpeedOfLight {
    _topSpeed = percentSpeedOfLight;
}
- (void)orbitPlanet:(Planet*)aPlanet atAltitude:(double)km {
    _planet = aPlanet;
	_altitude = km;
}

@end
{% endhighlight %}

## Sending Messages
To illustrate sending messages, I've stubbed out a class named
`MissionControl` that has a private instance variable named
`spaceship`.

{% highlight objectivec %}
- (Planet*)planetForSpaceship {
    return [spaceship planetToOrbit];
}
- (void)takeSpaceShipToMaximumSpeed {
    [spaceship setTopSpeed:1];
}
- (void)sendSpaceshipOnMission {
   [spaceship orbitPlanet:mars atAltitude:12000];
}
{% endhighlight %}

In Objective-C, square brackets enclose the object to which the
method is being sent (the receiver) and the message being sent. Each
colon signals that the next item is one of the method's parameters.

<iframe width="560" height="315"
src="http://www.youtube.com/embed/hQX-ymfWk3Y?rel=0" frameborder="0"
allowfullscreen></iframe>

## Creating Properties
We can think of properties in Objective-C as wrapper around instance
variables. Not only that, but they can be used to easily send messages
to the accessors (getters and setters) of an object.

To begin with, let's replace the declaration of getters and setters in
`Spaceship.h` with properties. 

In this code listing, where you see `@property` for `topSpeed`, this
is the same as declaring two methods: a getter named `topSpeed` and a
setter named `setTopSpeed:`. The `@property`  for `planetToOrbit` is
marked `readonly`. This is the same as declaring the getter method
named `planetToOrbit` without a setter. 

{% highlight objectivec %}
#import "Vehicle.h"
#import "Planet.h"

@interface Spaceship : Vehicle
@property (strong, nonatomic, readonly)Planet* planetToOrbit;
@property (nonatomic)double topSpeed;
- (void)orbitPlanet:(Planet*)aPlanet atAltitude:(double)km;
@end
{% endhighlight %}

### Synthesizing Properties the Old-School Way
(For at least this quarter we will be old-school, just FYI)

We will use the `synthesize` directive so the compiler can create the
getter and setter for our properties automatically. Our `Spaceship.m`
file will change to account for this.

{% highlight objectivec %}
#import "Spaceship.h"

@implementation Spaceship {
    double _altitude;
}
@synthesize planetToOrbit = _planetToOrbit;
@synthesize topSpeed = _topSpeed;

- (void)orbitPlanet:(Planet*)aPlanet atAltitude:(double)km {
    _planetToOrbit = aPlanet;
    _altitude = km;
}
@end

{% endhighlight %}

### Synthesize by Default
As of Xcode 4.5, you no longer need to type the `@synthesize`
line. Again however, we will be doing it the old-school way, this is
just for reference. 

If you declare a property named `example` in the header file or in the
class extension, then three things are generated for you: a getter
named `example`, a setter named `setExample:`, and an instance
variable named `_example`.

There are a couple of disclaimers. First, if you write your own getter
and setter, then the instance variable will not be generated for you
unless you explicitly write the `@synthesize` line yourself. 

If `example` is readonly, then only the getter named `example` and the
instance variable named `_example` will be generated. In this case, if
you write your own getter then the instance variable will also not be
created. 

Here is the code using Synthesize by Default. It gets cleaned up a
little bit. 

{% highlight objectivec %}
#import "Spaceship.m"

@implementation Spaceship {
    double _altitude;
}
- (void)orbitPlanet:(Planet*)aPlanet atAltitude:(double)km {
    _planetToOrbit = aPlanet;
    _altitude = km;
}
{% endhighlight %}

## Using Properties
When we use properties, the syntax for using the getters and setters
will change from square brackets to dot notation. 

### Getters
Here's how we used the getter in `planetForSpaceship` in the
`MissionControl` class to return an instance of the `Planet` our
`Spaceship` should orbit.

{% highlight objectivec %}
- (Planet*)planetForSpaceship {
    return [spaceship planetToOrbit];
]
{% endhighlight %}

We use our square bracket notation to send the `planetToOrbit` message
to `spaceship`. 

There's nothing wrong with using square brackets. It still works. But
`planetToOrbit` is a property in the `Spaceship` class, so we prefer
to use dot notation instead. To represent the getter, we don't enclose
the receiver and the property name in square brackets; instead we join
them with a dot like this

{% highlight objectivec %}
- (Planet*)planetForSpaceship {
    return spaceship.planetToOrbit;
}
{% endhighlight %}

### Setters
Here's an example of a setter form the `takeShipToMaximumSpeed` method
in `MissionControl`. We send spaceship the message `setTopSpeed:` and
pass the `double 1` as the argument

{% highlight objectivec %}
- (void)takeSpaceshipToMaximumSpeed {
    [spaceship setTopSpeed:1];
}
{% endhighlight %}

This square bracket notation continues to work even with
properties. But because `topSpeed` is a property of `Spaceship`, we
again prefer to use dot notation. 

The square brackets and colon are replaced by a dot and an equals sign
like this

{% highlight objectivec %}
- (void)takeSpaceshipToMaximumSpeed {
    spaceship.topSpeed = 1;
}
{% endhighlight %}

### Properties or instance variables?
You should always prefer to talk to properties and not instance
variables when you can. Getting and setting values through accessor
methods is safer than directly accessing the instance variables. 

When do you have to use instance variables? There are two situations.

The first exception to always using properties arises if you write
your own getter or setter. Inside of the getter and setter you have to
use the instance variable instead of the property. For example, here's
a possible getter for `planetToOrbit`.

{% highlight objectivec %}
- (Planet*)planetToOrbit {
    if (_planetToOrbit == nil) {
        _planetToOrbit = [[Planet alloc] initWithName:@"Mars"];
    }
    return _planetToOrbit;
}
{% endhighlight %}

In the next lecture we'll take a closer look at this kind of
getter. It is often called a *lazy initializer* becuase we wait until
the first time that someone needs the `planetToOrbit` before creating
and initializing it. 

The second exception to always using instance variables and not
properties is inside an `init` method. Suppose `Planet` has a property
`name`. Here is an example of a custom `init` method named
`initWithName:` that might be used in the `Planet` class.

{% highlight objectivec %}
- (id)initWithName:(NSString *)name {
    if ((self = [super init])) {
        _name = name;
    }
    return self;
}
{% endhighlight %}

Notice we don't initialize the `name` property, but rather the
instance variable directly. 

Other than custom getters and setters or `init` methods, your should
always use properties instead of accessing the underlying instance
variables directly. 

## Class Extensions
The interface in the header file is reserved for those properties and
methods that need to be publicly accessible to other objects. This is
where you announce to the world that these are the attributes you can
get and set and these are the messages that you can send.

On the other hand, the class extension is a private interface. Use it
to declare properties that you will only use internally. 

You can also declare a property to be publicly readonly in the header
file, and redeclare it as writable in the class extension. This way,
other objects can get the value, but they can't change it. 

Using class extensions, here is how the implementation file
`Spaceship.m` will look.

{% highlight objectivec %}
#import "Spaceship."

@interface Spaceship ()
@property (nonatomic) double altitude;
@property (strong, nonatomic, readwrite) Planet* planetToOrbit;
@end

@implementation Spaceship
- (void)orbitPlanet:(Planet*)aPlanet atAltitude:(double)km {
    self.planetToOrbit = aPlanet;
    self.altitude = km;
}
@end
{% endhighlight %}

Notice that not only can we now set `altitude` using a property which
we did not have before, but we can *set* `aPlanet` using a property
which is readonly in the public header file by redeclaring it in the
private interface. To the outside world this property can only be read,
but inside our class we can read and write to our heart's content.
