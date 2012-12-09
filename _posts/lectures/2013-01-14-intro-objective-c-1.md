---
layout: lecture
title: Intro to Objective-C - Part 1
excerpt: Intro to Objective-C - Part 1
category: lectures
tags:
- objectiveC
---
<iframe width="560" height="315" src="http://www.youtube.com/embed/s7L2PVdrb_8" frameborder="0" allowfullscreen></iframe>

{% highlight objectivec %}
    # import "Forwarder.h"
     
    @implementation Forwarder
     
    - (retval_t)forward:(SEL)sel args:(arglist_t) args {
     /*
     * Check whether the recipient actually responds to the message.
     * This may or may not be desirable, for example, if a recipient
     * in turn does not respond to the message, it might do forwarding
     * itself.
     */
     if([recipient respondsToSelector:sel]) {
     return [recipient performv:sel args:args];
     } else {
     return [self error:"Recipient does not respond"];
     }
    }
     
    - (id)setRecipient:(id)_recipient {
     [recipient autorelease];
     recipient = [_recipient retain];
     return self;
    }
     
    - (id) recipient {
     return recipient;
    }
    @end
{% endhighlight %}

