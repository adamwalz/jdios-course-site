---
layout: lecture
title: Model, View, Controller
excerpt: Model, View Controller
category: lectures
tags:
- mvc
---
<iframe width="560" height="315" src="http://www.youtube.com/embed/y4wrXLjFmbo?rel=0" frameborder="0" allowfullscreen></iframe>

Hi everyone, 

This lecture is on the Model, View, Controller design pattern that is prevelant in all iOS applications on the market today. 

Each iOS application is made up of many objects sending messages to one another. Model View Controller is a classic way of organizing your objects into three camps. 

###Model
The model consists of objects that capture what out application *is*. This is independant of how the application is *displayed*. 

If we had a spaceship game for example, the model objects could be of type Spaceship, Planet, MissionControl, etc. These model objects would capture all of the information about the current *state* of our application, but tell us nothing about what the application *looks* like. 

Another example might be a table-based application. In this case the model contains the data that is displayed, but it doesn't know how this information will be displayed.

###Controller
In iOS you'll hear a lot about view controllers. These are our controller objects. You will spend most of your time writing code for objects in this camp.

The controller is the intermediary between the model and the view. The controller is responsible for how your model is presented to the user. This is where the UI logic goes. It might determine, for example, how to represent a planet and the spaceship orbiting the planet at a given altitude.

###View
You will use generic objects to make up your view. The goal is to use the buttons and labels and other objects that Apple has created for us and manage them using your view controllers. This is why we say that the view is your controller's minions. 

This is important for iOS programming. Your view is made up of simple-minded objects that do their master's bidding. We don't tend to subclass these generic objects as your might see in other languages. 

#Fundamental Communication
In MVC there are three basic settings for configuration.

1. Completely **unrestricted** in a certain direction
2. **Forbidden** between objects in a certain direction
3. Conducted in a **stylized** way where an object knows very little, if anything, about the object with which it is communicating.

###Controller to Model
The controller's job is to get the model on the screen. This means that the controller must be able to communicate with the model to ask it questions. This communication is **unrestricted**.

In code, the controller needs to import the header files for the model objects so that it can send messages and access the properties declared in the header files. 

###Controller to view
The controller must also have unresetricted access to the view that it controls as well as the subviews that this view contains. In other words, the controller must have access to view its minions or it won't be able to control what the user sees on the screen. 

In code, indicating that communication flows in this direction looks a bit different than when we import a local file. 

Instead of importing the header files for a label, a button, and so on, we import the umbrella header file named UIKit.h from the UIKit framework. The import statement is 
{% highlight objectivec %}
    #import <UIKit/UIKit.h>
{% endhighlight %}
This in turn imports the header files for UILabel, UIButton, and the other individual components. 

We can create GUI objects in two ways. Most often, we'll create them visually and then connect to them from code. As you'll see in the next lecture, we'll use outlets to enable this communication. Less commonly, we will create the GUI objects in code in the view controller. 

###Model and View
The model never talks to the view. One reason for this is it allows the model to be UI Independent.

The views will never talk to the model. One reason is it allows us to use generic and reusable view components and the other is that it makes it easier for us to manage the flow of information and control through our application. 

<iframe width="560" height="315" src="http://www.youtube.com/embed/DhFXarxTtRo?rel=0" frameborder="0" allowfullscreen></iframe>

#Messages from the View
How does a button, label, or table communicate with the controller when the user presses the button or types text? 

In iOS, the communication from the view to the controller is both blind and structured. The view objects don't know much about the controllers. The view obects only know about certain roles that the controller is able to play. 

Lets explore two techniques:

1. Target Action
2. Delegates

###Target Action
Suppose we have a view controller that implements the method we wish to call when the user taps a button. The view controller object hangs a target on itself and it hands out an action to the button. 

An action is simply a method that the view controller implements. 

When the user touches the button, the button sends the message specified in the action to the view controller.

This allows the button to talk to the view controller without knowing very much about the view controller. 

All that button knows is that the view controller implements the method specified by the action. 

To sum up, the target action mechanism allows us to connect a view object to a particular method in a particular controller object. This method is triggered when the user iteracts with the view object in a designated way without the view object knowing anything else about the controller object.

###Delegate
Sometimes the view needs to contact the view controller and tell it something *did* happen, or something *will* happen, or ask it if something *should* be allowed to happen. 

The controller can freely communicate with the view, so the controller sends the view object the message to set the controller object as the view object's delegate.

Being the delegate means that the controller has agreed to play a specific role. More formally, we say that the controller has agreed to conform to a particular protocol. 

A protocol is a collection of methods. Some may be required while others may be optional. By agreeing to conform to the protocol, the controller has committed to implementing all of the required methods and it is free to implement any of the optional methods. 

Now when the view comes to a situation where it needs to tell its delegate that it *will* or *did* do something or when it needs to ask its delegate if it *should* do something, it sends the appropriate message from the protocol to the controller. 

As with the target action pattern, this relationship is blind and structured. 

All the view objects knows about the controller object is that it is an object that implements this protocol. This view object knows it can safely send the controller any of the required messages declared in the protocol. The view object can also send any of the optional messages declared in the protocol after first asking the controller object whether it implements this optional method.

A text field uses a delegate so that the view controller can determine what happens when, for example, the user taps on a return button or clears a text field. A table view uses two different delegates: one to respond to the user interaction with the table, and the other to fill the table view with data from the model. 

A table view **doesn't own** the data it displays. It turns to the controller and asks, "what goes here?" The controller plays the role of the "data source'. It usually turns to the model for help. The controller sits between the model and the view and helps the model get its data on screen. 

#Broadcasts from the Model
What if there are changes to the model that the view controller needs to represent on the screen?

For example, suppose you're displaying news items that your receive from a network feed. Your controller needs to know when the model has new data so it can refresh the screen with the breaking news. 

The model can't send a direct message to the controller. The model may be shared in your application by many different controllers and it would become brittle and hard to maintain if the model had to know about each controller that depended on it. 

Instead, any controller interested in knowing when some aspect of the model has changed needs to register that it is interested. 

Then the model must send out a notification that says "Hey, this thing you're interested in has changed." The model doesn't know anything about the controllers. 

As with our communication form the view to the controller, this communication is blind and structured. 

###Notifications
Remember, the model doesn't know anything about the controller, so it can't send a direct message to the controller saying "Hey, I've changed."

Our solution is to use notifications. Any controller interested in hearing about changes to the model registers this interest with the applications notification center. There is only one notification center for each application.

Then, when there are changes to the model, the model posts a notification to the notification center.

The notification center is then responsible for passing this news on to all of the objects that registered interest in the notification. 

The notification center bundles up information about the notification. it tells all of the interested parties the name of the notification. It also passes along a dictionary that can be filled with information about the notification. 

The beauty of this arrangement is that objects that know nothing about each other can pass information around by posting and registering to receive notifications.

###Key Value Observing
You can implement this broadcast mechanism without using the notification center if the controller can communicate with the model. Key value observing (KVO) is essentially a private notification. 

The controller object sends the model a message saying, "I'm interested in knowing when this property changes."

The model object then needs to update the property in a way that is observable. For instance, if it uses the setter method to set the value of the property being observed, then the private notification will be sent.

The controller object receives a message that says, "One of the properties you are interested in has changed its value."

Along with that message, the controller receives information that includes which object sent the message and which property was changed.

With KVO, the model is able to communicate this change to the controller object without knowing anything about the controller except that it's interested in hearing about this particular change.

#Multiple Controllers
As you add functionality to your application you won't be able to group your objects into  a single model camp, a single controller camp, and a single view camp. 

Each scene will be managed by a different view controller. A view controller may need help from other controllers to get the right data on the screen. These controller need to communicate with each other. 

As with communication between controllers and model objects or controllers and view objects, we want to make sure that out controllers are not overly coupled. The communication between controllers should take place in one direction. 

Usually if your have one scene on the screen and it is about to be replaced by another scene, the controller managing the current view knows about the controller managing the view about to be displayed. 

To communicate in the other direction, you might create your own custom protocol so that the first view controller can act as a delegate for the second. 

Notice that one controller isn't directly managing another controller's views. The view objects are the minions of a single view controller.

One view controller just passes information and possibly control to another view controller and lets it communicate the new information to its own minions. 

More than one controller object might talk to the same model object or objects. In fact, there might be a single core group of model objects that all of the controllers can address. 

#Summary
So far we've been describing the structure of our applications and how the objects are organized. At this point, these ideas aren't specific at all. In the next lecture we will take out first look at Objective-C and show how Xcode makes building applications simple. We'll use the MVC principles we've detailed in this lecture in a much more concrete way than was possible in this lecture. 